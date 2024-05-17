1. [安装](https://github.com/andersao/l5-repository)
2. 修改 `BaseRepository`
    - 内容
        
        ```PHP
        <?php namespace App\Scaffold;
        
        use Carbon\Carbon;
        use Exception;
        use Illuminate\Container\Container as Application;
        use Illuminate\Database\Eloquent\Model;
        use Illuminate\Database\Query\Builder;
        
        /**
         * Created by PhpStorm.
         * User: zgldh
         * Date: 2016/12/30
         * Time: 0:08
         */
        abstract class BaseRepository extends \Prettus\Repository\Eloquent\BaseRepository
        {
            private $uploadFileExpireHours = 12;
        
            public function __construct(Application $app)
            {
                parent::__construct($app);
                $this->scopeQuery(function ($model) {
                    return $this->getModuleScope($model);
                });
            }
        
            /**
             * 模型Scope
             */
            protected function getModuleScope($model)
            {
                return $model;
            }
        
            /**
             * @no-permission
             * @return static
             */
            public function applyCriteriaOnModel()
            {
                return $this->applyCriteria();
            }
        
        
            /**
             * @no-permission
             * @return static
             */
            public static function getInstance()
            {
                return app(static::class);
            }
        
            /**
             * @no-permission
             * @param $model
             * @param array $with
             * @return Datatables\Builder
             * @throws \Prettus\Repository\Exceptions\RepositoryException
             */
            public function datatables($model = null, array $with = [])
            {
                if ($model == null) {
                    $this->applyScope();
                    $query = $this->model;
                } elseif (is_a($model, Builder::class)) {
                    $query = $model;
                } elseif (is_a($model, \Illuminate\Database\Eloquent\Builder::class)) {
                    $query = $model;
                } elseif (is_a($model, Model::class)) {
                    $query = $model->newQuery();
                } elseif (is_string($model)) {
                    $query = call_user_func($model . '::query');
                } else {
                    $this->applyScope();
                    $query = $this->model;
                }
        
                if (is_a($query, Model::class)) {
                    $query = $query->newQuery();
                }
        
                $builder = new \App\Scaffold\Datatables\Builder($query, $with);
                $this->resetModel();
                return $builder;
            }
        
            // Inherit from InfyOm\Generator\Common\BaseRepository
        
            public function findWithoutFail($id, $columns = ['*'])
            {
                try {
                    return $this->find($id, $columns);
                } catch (Exception $e) {
                    return;
                }
            }
        
            /**
             * @no-permission
             */
            public function create(array $attributes)
            {
                // Have to skip presenter to get a model not some data
                $temporarySkipPresenter = $this->skipPresenter;
                $this->skipPresenter(true);
                $model = parent::create($attributes);
                $this->skipPresenter($temporarySkipPresenter);
        
                $model = $this->updateRelations($model, $attributes);
                $model->save();
        
                $result = $this->parserResult($model);
        
        
                $primaryKey = $model->getKey();
                $query = $model->newQuery();
                $query->withoutGlobalScopes();
                $model = $query->find($primaryKey);
                return $model;
            }
        
            /**
             * @no-permission
             */
            public function update(array $attributes, $id)
            {
                // Have to skip presenter to get a model not some data
                $temporarySkipPresenter = $this->skipPresenter;
                $this->skipPresenter(true);
                $model = parent::update($attributes, $id);
                $this->skipPresenter($temporarySkipPresenter);
        
                $model = $this->updateRelations($model, $attributes);
                $model->save();
        
                return $this->parserResult($model);
            }
        
        
            /**
             * @no-permission
             */
            public function updateRelations($model, $attributes)
            {
                $uploadModelClassName = config('upload.upload_model');
                $dealWithUpload = false;
                foreach ($attributes as $key => $val) {
                    if (isset($model) &&
                        method_exists($model, $key) &&
                        is_a(@$model->$key(), 'Illuminate\Database\Eloquent\Relations\Relation')
                    ) {
                        $relation = $model->$key($key);
        
                        // 处理上传
                        $isRelatedUpload = false;
                        if ($uploadModelClassName && is_a($relation->getRelated(), $uploadModelClassName)) {
                            $isRelatedUpload = true;
                            $dealWithUpload = true;
                        }
        
                        $methodClass = get_class($relation);
                        switch ($methodClass) {
                            case 'Illuminate\Database\Eloquent\Relations\BelongsToMany':
                                $newValues = array_get($attributes, $key, []);
                                $newValues = $newValues ?: [];
                                if (array_search('', $newValues) !== false) {
                                    unset($newValues[array_search('', $newValues)]);
                                }
        
                                if (count($newValues) && (is_object($newValues[0]) || is_array($newValues[0]))) {
                                    $newValues = array_map(function ($value) {
                                        return is_array($value) ? array_get($value, 'id') : object_get($value, 'id');
                                    }, $newValues);
                                }
        
                                $model->$key()->sync(array_values($newValues));
                                break;
                            case 'Illuminate\Database\Eloquent\Relations\BelongsTo':
                                $modelKey = $model->$key()->getForeignKey();
        //                        $newValue = array_get($attributes, $modelKey, null);
                                $newValue = array_get($attributes, $key, null);
                                $newValue = $newValue == '' ? null : $newValue;
                                $newValue = is_array($newValue) ? array_get($newValue, 'id', null) : $newValue;
                                $model->$modelKey = $newValue;
                                break;
                            case 'Illuminate\Database\Eloquent\Relations\HasOne':
                                break;
                            case 'Illuminate\Database\Eloquent\Relations\HasOneOrMany':
                                break;
                            case 'Illuminate\Database\Eloquent\Relations\HasMany':
                                $newValues = array_get($attributes, $key, []);
                                $newValues = $newValues ?: [];
                                if (array_search('', $newValues) !== false) {
                                    unset($newValues[array_search('', $newValues)]);
                                }
                                $modelKey = $model->$key($key)->getForeignKeyName();
        
                                foreach ($newValues as $index => $newValue) {
                                    $newValues[$index] = $newValue['id'];
                                }
        
                                foreach ($model->$key as $rel) {
                                    if (!in_array($rel->id, $newValues)) {
                                        $rel->$modelKey = null;
                                        $rel->save();
                                    }
                                }
        
                                if (count($newValues) > 0) {
                                    $related = get_class($model->$key()->getRelated());
                                    foreach ($newValues as $val) {
                                        if (is_string($val) || is_numeric($val)) {
                                            $rel = $related::find($val);
                                            $rel->$modelKey = $model->id;
                                            $rel->save();
                                        }
                                    }
                                }
                                break;
                        }
        
                        if ($isRelatedUpload) {
                            $userId = \Auth::user()->id;
                            switch ($methodClass) {
                                case 'Illuminate\Database\Eloquent\Relations\MorphOne':
                                    $newValue = array_get($attributes, $key, null);
                                    $uploadId = $this->getUploadId($newValue);
                                    // 1. Check upload obj is uploaded by current user
                                    $uploadObj = $uploadModelClassName::where('user_id', $userId)->where('id',
                                        $uploadId)->first();
                                    if ($uploadObj) {
                                        $oldUploadObject = $model->$key()->where('id', '<>', $uploadId)->first();
                                        if ($oldUploadObject) {
                                            // 2. Remove old one.
                                            $oldUploadObject->delete();
                                        }
                                        // 3. Update this upload obj to associate to this $model, setup a proper type
                                        $uploadObj->type = $key;
                                        $model->$key()->save($uploadObj);
                                    }
                                    break;
                                case 'Illuminate\Database\Eloquent\Relations\MorphMany':
                                    $newValues = array_get($attributes, $key, []);
                                    // 1. Unassociate old uploads to this $model
                                    $model->$key()->update(['uploadable_id' => null, 'uploadable_type' => null]);
                                    // 2. Loop
                                    $uploadIds = array_map(function ($newValue) {
                                        return $this->getUploadId($newValue);
                                    }, $newValues);
                                    $uploadModelClassName::where('user_id', $userId)->whereIn('id', $uploadIds)
                                        ->update(['uploadable_id' => $model->getKey(),
                                            'uploadable_type' => get_class($model),
                                            'type' => $key]);
                                    break;
                            }
                        }
                    }
                }
                // 处理上传
                if ($dealWithUpload && $userId) {
                    $expireTime = Carbon::now()->addHours(-$this->uploadFileExpireHours);
                    $query = call_user_func($uploadModelClassName . '::query');
                    $uploads = $query
                        ->where('user_id', $userId)
                        ->whereNull('uploadable_id')
                        ->where('created_at', '<', $expireTime)->get();
                    foreach ($uploads as $upload) {
                        $upload->delete();
                    }
                }
        
                return $model;
            }
        
            private function getUploadId($item)
            {
                if (is_numeric($item)) {
                    return $item;
                }
                return data_get($item, 'id', 0);
            }
        }
        ```
        

3. 创建一个 `CommonListCriteria`

- 内容
    
    ```PHP
    <?php
    
    namespace Modules\Report\Criteria;
    
    
    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Query\Builder;
    use Illuminate\Http\Request;
    use Illuminate\Support\Collection;
    use Prettus\Repository\Contracts\CriteriaInterface;
    use Prettus\Repository\Contracts\RepositoryInterface;
    
    class CommonListCriteria implements CriteriaInterface
    {
        /**
         * @var array|Collection
         */
        protected $filters = [];
    
        protected $fields = [];
    
        public function __construct(Request $request)
        {
            $this->filters = collect($request->get('filters', []));
        }
    
        /**
         * @param  Builder|Model  $model
         * @param  RepositoryInterface  $repository
         * @return mixed
         */
        public function apply($model, RepositoryInterface $repository)
        {
            foreach ($this->filters as $key => $value) {
    		      if (!in_array($key, $this->fields)) {
    		        continue;
    		      }
    		      $method = 'scope'.ucfirst($key);
    		      if (method_exists($this, $method)) {
    		        $model = $this->$method($model, $value);
    		      } else {
    						// 下划线转大驼峰，加上scope
    		        $newKey = UtilHelper::camelize($key);
    		        $newKey = str_replace('/', '', $newKey);
    		        $method = 'scope'.ucfirst($newKey);
    		        if (method_exists($this, $method)) {
    		          $model = $this->$method($model, $value);
    		        }
    		      }
    		    }
            return $model;
        }
    
        protected function scopeName($query, $name)
        {
            return $query->where(function($query) use ($name) {
                return $query->where('name', 'like', "%$name%")
                    ->orWhere('name_en', 'like', "%$name%");
            });
        }
    
        protected function scopeStatus($query, $status)
        {
            return $query->where('status', $status);
        }
    
        protected function scopeVendor($query, $vendor)
        {
            return $query->where('vendor_id', $vendor);
        }
    
        protected function scopeDepartment($query, $department)
        {
            return $query->where('dep_id', $department);
        }
    
        protected function scopeStore($query, $store)
        {
            return $query->where('store_id', $store);
        }
    }
    ```
    

4. 创建一个 `Criteria` 继承自 `CommonListCriteria`

- 内容
    
    ```PHP
    <?php
    
    namespace Modules\Recipe\Criteria;
    
    use Modules\Recipe\Models\RecipeCategory;
    use Prettus\Repository\Contracts\CriteriaInterface;
    use Modules\Report\Criteria\CommonListCriteria;
    
    class RecipeListCriteria extends CommonListCriteria implements CriteriaInterface
    {
    		// $fileds 是支持搜索的字段名, 支持小驼峰
        protected $fields = ['name', 'goods', 'inventory', 'component', 'category', 'store'];
    
        protected function scopeGoods($query, $goods)
        {
            return $query->where('goods_id', $goods);
        }
    
        protected function scopeInventory($query, $inventory)
        {
            return $query->where('as_inventory', $inventory);
        }
    
        protected function scopeComponent($query, $component)
        {
            return $query->where('as_component', $component);
        }
    
        protected function scopeCategory($query, $category_id)
        {
            $category = RecipeCategory::where('id', $category_id)->first();
            $categories = RecipeCategory::where('code', 'like', $category['code'] . '%')->get();
            if (empty($categories)) {
                return $query;
            }
            return $query->whereIn('category_id', array_unique(array_column($categories->toArray(), 'id')));
        }
    
        protected function scopeStore($query, $store)
        {
            return $query->whereIn('store_id', [0, $store]);
        }
    
    		protected function scopeCreatedAt($query, $date)
    	  {
    	    return $query->whereBetween('created_at', $date);
    	  }
    }
    ```
    

5. 在需要搜索的 `Controller` 里:

- 内容
    
    ```PHP
    public function __construct(RecipeBookRepository $repository)
        {
            $this->repository = $repository;// 这一句
            $this->middleware("auth:api");
        }
    
        /**
         * Display a listing of the RecipeBook.
         *
         * @param  IndexRequest  $request
         * @return  JsonResponse|\Illuminate\Http\Response|\Symfony\Component\HttpFoundation\BinaryFileResponse
         * @throws  \Exception
         */
        public function index(IndexRequest $request)
        {
    					// pushCriteria(new RecipeListCriteria($request))
              //  ->applyCriteriaOnModel() 是需要手动加的
            $data = $this->repository->pushCriteria(new RecipeListCriteria($request))
                ->applyCriteriaOnModel()
                ->datatables(null, $request->getWith())
                ->search($request->getColumns(), null)
                ->result($request->getExportFileName());
    
            return $data;
        }
    ```
    

  

6. 前端传参数:

- 内容
    
    ```PHP
    //比如传 created_at
     filters[createdAt][]: 2020-01-01
     filters[createdAt][]: 2020-10-17
    //也可以
     created_at[]: 2020-01-01
     created_at[]: 2020-10-17
    ```