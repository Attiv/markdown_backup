- 代码结构
- 跳转
- 数据库中
- assets.js
- 记录
- 鼠标变成小手
- 删除数组中的某一元素
- Angularjs 里面
- 数据库更新
- 清除缓存
- form
- 数组中是否含有元素
- vue相关
- twig获取get请求的参数
- WorkMan
- 判断变量类型
- nl2br 失效问题
- 数据表软删除
- 截取字符串中数字之前的字符串
- php如何判断一个字符串是否包含另一个字符串
- PHP数组排序
- findBy Order
- 截取指定字符串
- 只且只有一个值为true的判断语句

# 代码结构

- `app/` 里存放的大部分是配置信息
- `src/` 存放的是php代码
- `vendor` 存放的是第三方的库
- `web/` 存放的是前端代码  
    <!--more-->  
    

在`src/`里 `M`:`Entity`,`V`:`web/`(根目录里的),`C`:`Controller`

html文件再`web/partials`里

在开发中修改了.pug 或者 es5/6 文件,想要看到效果需要执行 `gulp watch`

前端开发中添加控件使用了第三方库 [Bootstrap](http://v3.bootcss.com/css/) 关于这个库在学习中我会另外记录.

# 跳转

`$state.go('frame.a-b')` 跳转到`web/scripts/states/a/b.js`

b.js里面在angular.module里含有`frame.a-b`,等学习了angular之后再补充

# 数据库中

`$query = $this->em()->getRepository('AppBundle:Company')``$result = $query->getQuery()->getResult();`  
query可以添加语句 result 就是查询到的结果  
比如:  

```Plain
$posTransactions = Util::em()->createQuery( 'SELECT uct FROM CoreBundle:UserCardTransaction uct
                WHERE (uct.userCard = :userCard) AND (uct.tranDesc LIKE :tranCode)order by uct.txnTime desc')
                ->setParameter('userCard', $uc)
                ->setParameter('tranCode', Transaction::POS_PURCHASE.'%')
                ->getResult();
```

查找`UserCardTransaction`表中`userCard`等于`$uc`, 并且 `tranDesc` 以 `Transaction::POS_PURCHASE` 开头的.

# assets.js

添加完js文件(路由文件)之后需要在`web/scripts/assets.js`添加

# 记录

如果`ng-table="ctrl.tableParams"` ,在对应的angular中需要写`controller as ctrl`

js中用`debugger`进行调试

日期格式: 比如 `p(ng-bind="item.checkOutTime | moment: 'L LT'")` L 是日期 LT是时间

`ng-bind="item.checkOutTime` 返回的数据item有checkOutTime属性才行

`template-pagination="ng-table/pagination.html"` 表格分页

导入数据库后要记得清下cookie

使用`queryList`的才使用`sliceQueryArray`方法分页

sql语句里带有`?`后面就需要使用bindValue绑定值

php请求里所有的变量在发送的时候都会初始化

# 鼠标变成小手

`<a style="cursor:pointer">CSS鼠标手型效果</a>`

# 删除数组中的某一元素

```Plain
for ($i = 0; $i < count($r['locations']); $i++) {
            if ('inactive' == $r['locations'][$i]->getStatus())
            {
                unset($r['locations'][$i]);
            }
        }
```

# Angularjs 里面

如果要用`$rootscope` services里面的function 里面也要加上`$rootScope`

# 数据库更新

_**数据库中更新/新增字段:**_

1. 先在`Entity`实例文件里添加字段.
2. 执行`php bin/console g:d:entities Entity路径(php bin/console g:d:entities SalexUserBundle:User )` 生成Get和Set方法
3. 执行`php bin/console doctrine:schema:update --force`更新数据库

# 清除缓存

`php bin/console c:c --env=dev`

# form

需要添加的value存放在`UserType.php`里  
比如:  

```Plain
public function buildForm(FormBuilderInterface $builder, array $options)
{
$builder->add('status', ChoiceType::class, array(
                'choices' => array(
                    '' => '',
                    'Active' => 'active',
                    'Ban' => 'ban',
                    'Close' => 'close',
                    'Unload' => 'unload',
                ),
            ))
}
```

# 数组中是否含有元素

- 数组中含有key`array_key_exists('key',数组)`
- 数组中含有Value `$user->getId()`

# vue相关

- 如果twig和vue一起用的话,`{{}}`会冲突,vue可以用`v-text`或者`v-html`解决.
- `build.js`是***vue***生成的

# twig获取get请求的参数

`app.request.query.get("errorInfo")`  
可以获取到参数  
`?errorInfo`

# WorkMan

`Http`里面的东西可以在`span-web`里的`TestController`的`indexAction()`方法里调用

```Plain
Service::basic('FVTransaction', []);
        return new Response('');
```

第二个参数是传的数据,在`FVTransactionHandle`的`start()`方法里

```Plain
$this->connection->send('');
  //获取data
  $this->data['post'][''];
```

# 判断变量类型

```Plain
gettype()、is_array()、is_bool()、is_float()、is_double()、is_integer()、is_null()、is_numeric()、is_object()、is_resource()、is_scalar() 和 is_string()
```

# nl2br 失效问题

在PHP中不要使用`''`  
使用  
`""`就不会失效

# 数据表软删除

1. `给entity类加上 @Gedmo\SoftDeleteable() 注解`
2. `让entity类use SoftDeleteableEntity`
3. `提交代码`

# 截取字符串中数字之前的字符串

```Plain
$str = "dsasdas-asdfasdf-fg121ffdd"; 
$reg = "/(\D+)/"; 
preg_match($reg,$str,$m); 
echo $m[0];dsasdas-asdfasdf-fg
```

# php如何判断一个字符串是否包含另一个字符串

```Plain
strpos($a, $b) !== false 如果$a 中存在 $b，则为 true ，否则为 false。
用 !== false （或者 === false） 的原因是如果 $b 正好位于$a的开始部分，那么该函数会返回int(0)，那么0是false，但$b确实位于$a中，所以要用 !== 判断一下类型，要确保是严格的 false。
```

# PHP数组排序

```Plain
usort($allTransactions,function($a, $b){
            return $a['DATE'] < $b['DATE']?1:-1;
        });
```

# findBy Order

```Plain
$ens = $em->getRepository('AcmeBinBundle:Marks')
          ->findBy(
             array('type'=> 'C12'), 
             array('id' => 'ASC')
           );
```

# 截取指定字符串

`$str='123/456/789/abc';`  
截取第一个斜杠前面的内容可以这样来：  

```Plain
echo substr($str,0,strpos($str, '/'))
```

或者

```Plain
$array=explode('/', $str);
echo $array[0];
// 输出 123
```

截取第一个斜杠后面的内容可以这样来：

```Plain
echo substr($str,strpos($str,'/')+1);
//输出 456/789/abc
```

截取最后一个斜杠后面的内容可以这样来：

```Plain
echo trim(strrchr($str, '/'),'/');
```

或者如果知道斜杠的个数

```Plain
$array=explode('/', $str);
echo $array[3];
//输出 abc
```

但是问题来了；如果不知道有多少个斜杠呢？如果想要第二个斜杠和第三个斜杠中间的内容呢？  
下面我写的这个函数就可以轻松解决如上 所有问题；  

```Plain
/**
 * 按符号截取字符串的指定部分
 * @param string $str 需要截取的字符串
 * @param string $sign 需要截取的符号
 * @param int $number 如是正数以0为起点从左向右截  负数则从右向左截
 * @return string 返回截取的内容
 */
function cut_str($str,$sign,$number){
    $array=explode($sign, $str);
    $length=count($array);
    if($number<0){
        $new_array=array_reverse($array);
        $abs_number=abs($number);
        if($abs_number>$length){
            return 'error';
        }else{
            return $new_array[$abs_number-1];
        }
    }else{
        if($number>=$length){
            return 'error';
        }else{
            return $array[$number];
        }
    }
}
```

示例：

```Plain
echo cut_str($str,'/',0); //输出 123
echo cut_str($str,'/',2); //输出 789
echo cut_str($str,'/',-1);//输出 abc
echo cut_str($str,'/',-3);//输出 456
```

# 只且只有一个值为true的判断语句

`$a xor $b Xor（逻辑异或） TRUE，如果 $a 或 $b 任一为 TRUE，但不同时是。`

`明文加密`

```Plain
//比如 sha256加密
echo hash('sha256', '明文');
```