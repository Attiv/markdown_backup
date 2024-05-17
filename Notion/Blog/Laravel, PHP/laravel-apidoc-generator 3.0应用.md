[laravel-apidoc-generator](https://github.com/mpociot/laravel-apidoc-generator)是一个生成 `laravel/lumen`接口文档并支持快捷导入`postman`的库，在版本`3.0.2`中使用如下:

> 安装使用根据github使用说明。3.0需要 PHP > 7, Laravel >= 5.5

1. 若使用 `php artisan vendor:publish --provider=Mpociot\\ApiDoc\\ApiDocGeneratorServiceProvider --tag=config` 命令并没有在`config`目录下生成 `apidoc.php` 文件，可以使用 `php artisan vendor:publish` 手动选择 apidoc.
2. 在 `apidoc.php` 里可以配置文档属性，比如在:

```Plain
'apply' => [
                /*
                 * Specify headers to be added to the example requests
                 */
                'headers' => [
                     'Authorization' => 'Bearer: {token}',
                    // 'Api-Version' => 'v2',
                ],
```

可以配置请求的 `headers`信息  
3. 注意在  

```Plain
   'response_calls' => [
                    /*
                     * API calls will be made only for routes in this group matching these HTTP methods (GET, POST, etc).
                     * List the methods here or use '*' to mean all methods. Leave empty to disable API calls.
                     */
                    'methods' => [],
```

`methods`需要改为`[]`,默认是 `get`,如果是`get`的话如果有 `get`请求的接口，文档的导入到`postman`链接会失效。  
4. 生成文档时跳过某接口:  

```Plain
在接口的方法里:
/**
 *@hideFromAPIDocumentation
*/
```

1. api参数:

```Plain
/**
     *  upload_callback
     *  上传成功回调
     *
     * @bodyParam path string required 上传路径
     * @bodyParam device_no string required 设备ID
     * @bodyParam record_time int 视频录制时间
     * @bodyParam upload_by int required 上传者
     * @bodyParam project_id int required 当前项目ID
     * @bodyParam hash string required 文件的hash
     * @bodyParam upload_type int required 1->视频, 2->检测文件, 3->身份认证, 4->环境认证
     *
     * @param UploadCallbackRequest $request
     *
     * @return \\Illuminate\\Http\\JsonResponse
     */
```

[![](http://wx1.sinaimg.cn/large/6c35e247ly1fwreucftsfj20r60wmjvr.jpg)](http://wx1.sinaimg.cn/large/6c35e247ly1fwreucftsfj20r60wmjvr.jpg)