显示Dashboard Widget数量的接口在DashboardHCOController.php里 indexAction里写接口  
在AreaRepository.php里写方法.  

`new Carbon` 服务器时间

`form-group ml-10` 里面 ml-10 是间距

`var_dump()` 调试  
  
`Util::dd()` 打印  
.pug会覆盖.html  
.es6会覆盖.es5  
  
`php bin/console c:c` 清缓存  
  
`php bin/console c:c --env=dev` 清缓存  
  
`failed to write` 权限问题

`isset(变量)` 如果定义了变量.

`ls -la var/mails/default/` 查看邮件

`/Users/test/WebProject/application-registration/bin/console swiftmailer:spool:send --message-limit=10 --env=prod >> /Users/test/WebProject/application-registration/var/logs/mail.log` 立即接收邮件

`Util::dd(Util::e2a(变量/对象));`  
Util::dd(Util::e2a());  

`php bin/console d:s:u --force`  
更新数据库  

`Util::formatTime2` 格式化日期,有时区转换,不可重复使用  
  
`Util::formatTime` 格式化日期,没有时区转换

`.git`目录里`config`和`configh`两个是提交账户

## 错误信息

如果出现`Undefined column` 就执行数据库迁移命令:`php bin/console d:s:u --force`

## 禁用缓存

Chrome 调试时'Network'里的'Disable cache' 要勾上

## 分页 搜索 bug

在搜索后选到最后一页,然后再搜索别的内容,出现有数据但是显示空的bug:

```Plain
if (config.params && config.params.pageIndex !== undefined && config.params.pageIndex > 1) {
                        if (!$._requests) {
                            $._requests = {};
                        }
                        var params = angular.copy(config.params);
                        delete params.pageIndex;
                        delete params.pageSize;
                        var paramsString = JSON.stringify(params);

                        if (!$._requests[config.url]) {
                            $._requests[config.url] = paramsString;
                        } else {
                            var last = $._requests[config.url];
                            if (last != paramsString) {
                                $._requests[config.url] = paramsString;
                                config.params.pageIndex = 1;

                                var table = $('table[ng-table]'),
                                    scope = table.scope(),
                                    key = table.attr('ng-table');
                                if (scope[key]) {
                                    scope[key].page(1);
                                }
                            }
                        }
                    }
```

## 添加第三方

使用 `bower install 第三方名` 安装

## 添加头文件

在 `web/scripts/assets.js`里加