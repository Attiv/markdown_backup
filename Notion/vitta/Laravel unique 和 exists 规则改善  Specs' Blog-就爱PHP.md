[__](https://9iphp.com/)[首页](https://9iphp.com/) » [Web技术](https://9iphp.com/web) » [Laravel](https://9iphp.com/web/laravel) » 正文

# Laravel unique 和 exists 规则改善

 2016/10/11 | 

[Laravel](https://9iphp.com/web/laravel)

| 

[暂无评论](https://9iphp.com/web/laravel/laravel-5_3-unique-and-exists-validation.html#comments)

|   (3评) |

[![](https://www.notion.soLaravel%20unique%20%E5%92%8C%20exists%20%E8%A7%84%E5%88%99%E6%94%B9%E5%96%84%20%7C%20Specs'%20Blog-%E5%B0%B1%E7%88%B1PHP.resources/laravel-validation-rule.png)](https://www.notion.soLaravel%20unique%20%E5%92%8C%20exists%20%E8%A7%84%E5%88%99%E6%94%B9%E5%96%84%20%7C%20Specs'%20Blog-%E5%B0%B1%E7%88%B1PHP.resources/laravel-validation-rule.png)

使用 Laravel 的 `ValidatesRequests` trait 验证请求是非常简单的，该 trait 已经通过 `BaseController` 被自动包含进来。它的功能非常强大，并为常用的情况提供了多个有用的规则。其中 `exists()` 和 `unique()` 用于验证数据是否在数据库中存在，通常使用方式如下：

**PHP**`// exists 例子'email'=>'exists:staff,account_id,1'// unique 例子'email'=>'unique:users,email_address,$user->id,id,account_id,1'`

你可以看到，这种方式不便于记忆，有时候你可能经常需要去查看文档。

从 Laravel v5.3.18 开始，这两个规则都通过新引入的 `Rule` 类被简化了。

使用上面相同的例子，通过下面这个更流畅的例子可以达到相同的效果：

**PHP**`'email'=>['required',Rule::exists('staff')->where(function($query){ $query->where('account_id',1);}),],`

**PHP**`'email'=>['required',Rule::unique('users')->ignore($user->id)->where(function($query){ $query->where('account_id',1);})],`

这两个方法都支持下面的方法：

- `where`
- `whereNot`
- `whereNull`
- `whereNotNull`

`unique` 方法包含额外的 `ignore` 方法，所以你可以验证其他的数据。

这个新特性的另一个福利是旧的方式依然完全支持，实现方式是通过 [formatWheres](https://github.com/laravel/framework/blob/5.3/src/Illuminate/Validation/Rules/Unique.php#L143-L153) 方法转换为旧的字符串方式：

**PHP**`protectedfunction formatWheres(){return collect($this->wheres)->map(function($where){return $where['column'].','.$where['value'];})->implode(',');}`

要获取最新版本你需要运行 `composer update`，一旦获取到 v5.3.18 你就可以使用这种全新的流畅的方式了。

Update On 2016-10-16：

demisions 规则也将在 Laravel v5.3.19 中加入新的方式：

[![](https://www.notion.soLaravel%20unique%20%E5%92%8C%20exists%20%E8%A7%84%E5%88%99%E6%94%B9%E5%96%84%20%7C%20Specs'%20Blog-%E5%B0%B1%E7%88%B1PHP.resources/laravel-rule-dimensions.jpg)](https://www.notion.soLaravel%20unique%20%E5%92%8C%20exists%20%E8%A7%84%E5%88%99%E6%94%B9%E5%96%84%20%7C%20Specs'%20Blog-%E5%B0%B1%E7%88%B1PHP.resources/laravel-rule-dimensions.jpg)

via: [laravel-news](https://laravel-news.com/2016/10/unique-and-exists-validation/)

 赞 (2) or [__](https://9iphp.com/donate) [打赏](https://9iphp.com/donate)

[#Laravel](https://9iphp.com/tag/laravel) [#Laravel 5.3](https://9iphp.com/tag/laravel-5-3) [#验证](https://9iphp.com/tag/%e9%aa%8c%e8%af%81)

### **转载请注明来源：**[**Laravel unique 和 exists 规则改善**](https://9iphp.com/web/laravel/laravel-5_3-unique-and-exists-validation.html) **-** [**Specs' Blog-就爱PHP**](https://9iphp.com/)

- [上一篇](https://9iphp.com/web/laravel/laravel-5-3-recap.html)
- [下一篇](https://9iphp.com/web/laravel/php-datetime-package-carbon.html)

你可能也喜欢：

- [通过 View::first 使用 Laravel Blade 的动态模板](https://9iphp.com/web/php/view-first-in-blade.html)
- [[ne]]
- [[laravelmailab]]
- [[resourcefulcontrolle]]
- [[whatpackagesdoyouinstallon]]

### **发表评论**

__

*

__

*

点击此处进行验证

