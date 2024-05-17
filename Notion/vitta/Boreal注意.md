- session问题
- 新建 model
- PHP中引入文件
- fastclick.js 导致mobile模式下input不生效

- 输出查询语句

# session问题

- `yarn run dev` 之后打开 Apache的 boreal，复制 `br_session` 到前段运行的地方粘贴

# 新建 model

1. 在 `models` 目录里新建 `model.php`
2. 在 `config\autoload.php` 文件里的 `$autoload['model']`数组里加入新建的model
3. 在 `CI_phpStorm` 里的 `CIController` 和 `CIModel` 类里添加 `@property model_name $model_name`

# PHP中引入文件

`require_once('application/helpers/Util.php');`

# fastclick.js 导致mobile模式下input不生效

在元素上加上

# 输出查询语句

`$this->db->last_query()`

%0A%5Btoc%5D%0A%23%20session%E9%97%AE%E9%A2%98%0A-%20%60yarn%20run%20dev%60%20%E4%B9%8B%E5%90%8E%E6%89%93%E5%BC%80%20Apache%E7%9A%84%20boreal%EF%BC%8C%E5%A4%8D%E5%88%B6%20%60br_session%60%20%E5%88%B0%E5%89%8D%E6%AE%B5%E8%BF%90%E8%A1%8C%E7%9A%84%E5%9C%B0%E6%96%B9%E7%B2%98%E8%B4%B4%0A%0A%23%20%E6%96%B0%E5%BB%BA%20model%0A1.%20%E5%9C%A8%20%60models%60%20%E7%9B%AE%E5%BD%95%E9%87%8C%E6%96%B0%E5%BB%BA%20%60model.php%60%0A2.%20%E5%9C%A8%20%60config%5Cautoload.php%60%20%E6%96%87%E4%BB%B6%E9%87%8C%E7%9A%84%20%60%24autoload%5B'model'%5D%60%E6%95%B0%E7%BB%84%E9%87%8C%E5%8A%A0%E5%85%A5%E6%96%B0%E5%BB%BA%E7%9A%84model%0A3.%20%E5%9C%A8%20%60CI_phpStorm%60%20%E9%87%8C%E7%9A%84%20%60CIController%60%20%E5%92%8C%20%60CIModel%60%20%E7%B1%BB%E9%87%8C%E6%B7%BB%E5%8A%A0%20%60%20%40property%20model_name%20%24model_name%60%0A%0A%23%20PHP%E4%B8%AD%E5%BC%95%E5%85%A5%E6%96%87%E4%BB%B6%0A%60require_once('application%2Fhelpers%2FUtil.php')%3B%60%0A%0A%23%20fastclick.js%20%E5%AF%BC%E8%87%B4mobile%E6%A8%A1%E5%BC%8F%E4%B8%8Binput%E4%B8%8D%E7%94%9F%E6%95%88%0A%0A%E5%9C%A8%E5%85%83%E7%B4%A0%E4%B8%8A%E5%8A%A0%E4%B8%8A%20%60class%3D%22needsclick%22%60%0A%0A%23%20%E8%BE%93%E5%87%BA%E6%9F%A5%E8%AF%A2%E8%AF%AD%E5%8F%A5%0A%60%24this-%3Edb-%3Elast_query()%60