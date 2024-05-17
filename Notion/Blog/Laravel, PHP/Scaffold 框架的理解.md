1. [安装](https://github.com/zgldh/scaffold)

  

2. [[Criteria 的使用]]

3. 理解

- 具体Controller 查询方法
    
    ```PHP
    /**
       * list
       *
       * @queryParam filters  filter option. example createdAt[]: '2020-01-01', createdAt[]: '2020-10-17'
       * @queryParam consentFormId int consent form id
       * @queryParam start integer start item, = (page - 1) * length
       * @queryParam length integer every page item count
       */
      public function index(IndexRequest $request)
      {
        if (@$request->_export && !count($request->getColumns())) {
          $columns = $this->handleExportFields();
          $related = $this->handleExportRelatedFields($columns);
          $columns = $related['columns'];
          $request['_with'] = $related['with'];
          $request['columns'] = $columns;
        }
        $data = $this->repository->pushCriteria(new SdkInformationCriteria($request))->applyCriteriaOnModel()->datatables(null, ['app'])
          ->search($request->getColumns(), null)
          ->result($request->getExportFileName());
          if (@$request->_export) {
            return $data;
          } else {
            $total = $data->getData()->recordsTotal;
            $result = [
              'data' => $data->getData()->data,
              'total' => $total
            ];
          }
        return $this->success('Success', $result);
    
      }
    ```
    
- BaseController
    
    ```PHP
    <?php namespace App\Scaffold;
    
    use App\Http\Controllers\Controller;
    use App\Http\Requests\BundleRequest;
    use App\Http\Requests\ExportRequest;
    use App\Http\Requests\IndexRequest;
    use App\UtilHelper;
    use Modules\SdkInformation\Models\SdkInformation;
    
    /**
     * Class AppBaseController
     */
    class AppBaseController extends Controller
    {
      /**
       * @var BaseRepository
       */
      protected $repository;
    
      public function handleExportFields()
      {
        $model = $this->repository->model();
        $fields = $model::$exportFields;
        $columns = [];
        foreach ($fields as $index => $field) {
          $columns[$index]['name'] = $field;
          $columns[$index]['data'] = $field;
          $columns[$index]['label'] = ucfirst(UtilHelper::camelizeWithBlank($field));
        }
        return $columns;
      }
    
      public function handleExportRelatedFields($columns = [])
      {
        $model = $this->repository->model();
        $fields = $model::$exportRelatedFields;
        $with = [];
        foreach ($fields as $name => $related) {
          $with[] = $name;
          $count = count($columns);
          $columns[$count]['name'] = $related['value'];
          $columns[$count]['data'] = $related['value'];
          $columns[$count]['label'] = $related['label'];
        }
        $with = implode(',', $with);
        return [
          'with' => $with,
          'columns' => $columns
        ];
      }
    
      public function sendResponse($result, $message)
      {
        return \Response::json([
          'success' => true,
          'data' => $result,
          'message' => $message,
        ]);
      }
    
    
      public function sendError($error, $code = 404)
      {
        return \Response::json([
          'success' => false,
          'message' => $error,
        ], $code);
      }
    
      /**
       * @hideFromAPIDocumentation
       * 批量操作
       * 如果想让一个 Repository 的函数支持批量操作，则要求该函数第一个参数一定是对象的ID
       * @param BundleRequest $request
       * @return \Illuminate\Http\JsonResponse
       */
      public function bundle(BundleRequest $request)
      {
        $action = $request->input('action');
        if (!method_exists($this->repository, $action)) {
          return $this->sendError("Action {$action} does not exist.");
        }
        $indexes = $request->input('indexes');
        $options = $request->input('options');
        $data = [];
        $messages = [];
        foreach ($indexes as $index) {
          try {
            $data[] = [
              'index' => $index,
              'data' => call_user_func_array([$this->repository, $action], [$index, $options])
            ];
          } catch (\Exception $e) {
            $messages[] = [
              'index' => $index,
              'message' => $e->getMessage()
            ];
          }
        }
        return $this->sendResponse($data, $messages);
      }
    }  
    ```
    
- 查询和导出excel
    
    导出用到的库: [Laravel Excel](https://docs.laravel-excel.com/3.1/exports/from-query.html)
    
    - `$request` 里有 `_export` 的返回下载的 excel, 反之返回列表
    - `$request->columns` 里的是要打印的字段，比如:
        
        ```PHP
        			$columns[0]['name'] = 字段名;
              $columns[0]['data'] = 字段名;
              $columns[0]['label'] = Excel 里的字段名;
        ```
        
    - `$request->_with` 是关联的表，比如 `sdkInformation.php` 关联了 `consentForm`, 现在 `skdInformation.php` 里写好关联关系, 具体:
        
        ```PHP
        <?php namespace Modules\SdkInformation\Models;
        
        use Illuminate\Database\Eloquent\Model;
        use Spatie\Activitylog\Traits\HasActivity;
        use Illuminate\Database\Eloquent\SoftDeletes;
        
        class SdkInformation extends Model
        {
          use HasActivity;
          use SoftDeletes;
        
          public $table = 'sdk_information';
        
        	// 导出没有关联的字段
          public static $exportFields = [
            "app_key",
            "advertising_id",
            "email",
            "applications_installed",
            "i_m_e_i",
            "operating_system",
            "language_setting",
            "location",
            "device_make",
            "device_model",
            "ip_address",
            "m_c_c/_m_n_c",
            "privacy_consent/_c_m_p",
            "user_agent",
            "device_id",
            "android_id",
            "serial",
            "country"
          ];
        
         // 导出关联关系的字段
          public static $exportRelatedFields = [
            "consentForm" => [
              "label" => "Consent Form",
              "value" => "consentForm.value"
            ]
          ];
        
          public $fillable = [
            "app_id",
            "app_key",
            "advertising_id",
            "email",
            "applications_installed",
            "i_m_e_i",
            "operating_system",
            "language_setting",
            "location",
            "device_make",
            "device_model",
            "ip_address",
            "m_c_c/_m_n_c",
            "privacy_consent/_c_m_p",
            "user_agent",
            "device_id",
            "serial",
            "android_id",
            "country",
            "consent_form_id",
            "created_by"
          ];
        
          protected static $logOnlyDirty = true;
          protected static $logAttributes = [
            "app_id",
            "app_key",
            "advertising_id",
            "email",
            "applications_installed",
            "i_m_e_i",
            "operating_system",
            "language_setting",
            "location",
            "device_make",
            "device_model",
            "ip_address",
            "m_c_c/_m_n_c",
            "privacy_consent/_c_m_p",
            "user_agent",
            "device_id",
            "android_id",
            "consent_form_id",
            "serial",
            "country",
            "created_by"
          ];
        
          /**
           * The attributes that should be casted to native types.
           *
           * @var  array
           */
          protected $casts = [
            'app_id' => 'integer',
            'app_key' => 'string',
            'advertising_id' => 'string',
            'email' => 'string',
            'applications_installed' => 'array',
            'i_m_e_i' => 'string',
            'operating_system' => 'string',
            'language_setting' => 'string',
            'location' => 'string',
            'device_make' => 'string',
            'device_model' => 'string',
            'ip_address' => 'string',
            'm_c_c/_m_n_c' => 'string',
            'privacy_consent/_c_m_p' => 'string',
            'user_agent' => 'string',
            'serial' => 'string',
            'device_id' => 'string',
            'android_id' => 'string',
            'country' => 'string',
            'created_by' => 'integer',
            'consent_form_id' => 'integer',
            'created_at' => 'timestamp',
            'updated_at' => 'timestamp',
          ];
          protected $dates = ['deleted_at'];
        
          /**
           * Validation rules
           *
           * @var  array
           */
          public static $rules = [
            'app_id' => '',
            'app_key' => 'required',
            'advertising_id' => '',
            'email' => '',
            'applications_installed' => '',
            'i_m_e_i' => '',
            'operating_system' => '',
            'language_setting' => '',
            'location' => '',
            'device_make' => '',
            'device_model' => '',
            'ip_address' => '',
            'm_c_c/_m_n_c' => '',
            'privacy_consent/_c_m_p' => '',
            'user_agent' => '',
            'created_by' => '',
          ];
        
          /**
           * @return  \Illuminate\Database\Eloquent\Relations\BelongsTo
           **/
          public function app()
          {
            return $this->belongsTo('Modules\App\Models\App', 'app_id', 'id');
          }
        
          /**
           * @return  \Illuminate\Database\Eloquent\Relations\BelongsTo
           **/
          public function user()
          {
            return $this->belongsTo('Modules\User\Models\User', 'created_by', 'id');
          }
        
          public function consentForm()
          {
            return $this->belongsTo('Modules\ConsentForm\Models\ConsentForm', 'consent_form_id', 'id');
          }
        }
        ```
        
        实现之后的效果就是:
        
        ```PHP
         $request->_with = consentForm
         $request->columns[0][data] = 'consentForm.value'
         $request->columns[0][name] = 'consentForm.value'
         $request->columns[0][label] = 'Consent Form'
        ```