- 监听鼠标点击事件
- js 文件引入 js
- 判断是否 undefined
- select.change失效
- jQuery判断元素是否显示与隐藏
- Chart.js 自定义html legend
- 多个ajax,需要停止其余
- 绑定回车键

  

# PadEnd 和 Start 问题

- 长度超过了字符串的长度,返回原字符串…上如果填充的 chars+string > length,截断的是 chars...

可以使用

```JavaScript
function stringFixedStart (content, length, char = ' ') {
  let target
  if (content.length > length) {
    target = content.substring(0, length - 3) + '...'
  } else {
    target = padStart(content, length, ' ')
  }
  return target
}

function stringFixedEnd (content, length, char = ' ') {
  let target
  if (content.length > length) {
    target = content.substring(0, length - 3) + '...'
  } else {
    target = padEnd(content, length, char)
  }
  return target
}
```

# 监听鼠标点击事件

```Plain
document.onmousedown=function(event){ 
 console.log(event);
 //1 左键 2中建 3 右键
}
```

# js 文件引入 js

`document.write(”<script language=javascript src='/js/2.js'><\/script>”)`

# 判断是否 undefined

```Plain
var exp = undefined;
if (typeof(exp) == "undefined")
{
    alert("undefined");
}
```

# select.change失效

`$('\#TCPChoose').change(function () {});` 如果不执行的话,可以用:

```Plain
$(function () {
        $('\#TCPChoose').change(function () {
          
        })
      })
```

# jQuery判断元素是否显示与隐藏

`if($("\#username").is(":hidden")){ }`

_**我感觉**_`_**$(function())**_`_**里面的方法就类似于咱的**_`_**viewdidload**_`_**， 进来就会调一下，但是那个元素如果不存在的话就无效**_

# Chart.js 自定义html legend

```Plain
options: {
           legend: false,
           legendCallback: function (chart) {
             var text = [];
             text.push('<ul>');
             for (var i = 0; i < chart.data.datasets[0].data.length; i++) {
               text.push('<li style="white-space: nowrap;">');
               text.push('<span style="color:' + chart.data.datasets[0].backgroundColor[i] + '">' + '&\#9608' + '</span>');
               if (chart.data.labels[i]) {
                 text.push(chart.data.labels[i]);
               }
               text.push('</li>');
             }
             text.push('</ul>');
             return text.join("");
           }
           
$("\#storeNamesLabel").html(storeNameChart.generateLegend());
```

最后把`generateLegend()`生成的html赋予需要的地方.

# 多个ajax,需要停止其余

```Plain
var ajaxRequest = null;
      function todayButtonClicked() {
        resetButtons();
        $("\#allButton").button('loading');
        if (ajaxRequest){
          ajaxRequest.abort();
        }
        ajaxRequest = $.ajax({
          url: "{{ path('statementConfirmed') }}",
          type: 'POST',
          data: {},
          success: function (data) {
            $("\#todayTableDiv").html("");
            $("\#todayTableDiv").append(data);
            setSpendingLabel();
            resetButtons();
            $("\#allButton").button('toggle');
          },
          failed: function () {
            console.log('failed');
//            resetButtons();
//            $("\#allButton").button('toggle');
          }
        });
      }
      function confirmButtonClicked() {
        resetButtons();
        $("\#confirmedButton").button('loading');
        if (ajaxRequest){
          ajaxRequest.abort();
        }
        ajaxRequest = $.ajax({
          url: "{{ path('statementToday') }}",
          type: 'POST',
          data: {},
          success: function (data) {
            $("\#todayTableDiv").html("");
            $("\#todayTableDiv").append(data);
            setSpendingLabel();
            resetButtons();
            $("\#confirmedButton").button('toggle');
          },
          failed: function () {
            console.log('failed');
//            resetButtons();
//            $("\#confirmedButton").button('toggle');
          }
        });
      }
```

# 绑定回车键

```Plain
$("\#searchBar").bind('keypress',function (event) {
      if (event.keyCode == '13'){
        searchButtonClicked();
        return false;
      }
    });
```

%0A%5Btoc%5D%0A%23%23%20%E7%9B%91%E5%90%AC%E9%BC%A0%E6%A0%87%E7%82%B9%E5%87%BB%E4%BA%8B%E4%BB%B6%20%23%23%0A%60%60%60%0Adocument.onmousedown%3Dfunction(event)%7B%20%0A%20console.log(event)%3B%0A%20%2F%2F1%20%E5%B7%A6%E9%94%AE%202%E4%B8%AD%E5%BB%BA%203%20%E5%8F%B3%E9%94%AE%0A%7D%0A%60%60%60%0A%0A%0A%23%23%20js%20%E6%96%87%E4%BB%B6%E5%BC%95%E5%85%A5%20js%20%23%23%0A%60%0Adocument.write(%E2%80%9D%3Cscript%20language%3Djavascript%20src%3D'%2Fjs%2F2.js'%3E%3C%5C%2Fscript%3E%E2%80%9D)%60%0A%0A%23%23%20%E5%88%A4%E6%96%AD%E6%98%AF%E5%90%A6%20undefined%20%23%23%0A%0A%60%60%60%0Avar%20exp%20%3D%20undefined%3B%0Aif%20(typeof(exp)%20%3D%3D%20%22undefined%22)%0A%7B%0A%20%20%20%20alert(%22undefined%22)%3B%0A%7D%0A%0A%60%60%60%0A%0A%23%23%20select.change%E5%A4%B1%E6%95%88%20%23%23%0A%60%20%20%24('%23TCPChoose').change(function%20()%20%7B%7D)%3B%60%20%E5%A6%82%E6%9E%9C%E4%B8%8D%E6%89%A7%E8%A1%8C%E7%9A%84%E8%AF%9D%2C%E5%8F%AF%E4%BB%A5%E7%94%A8%3A%0A%60%60%60%0A%20%20%20%20%24(function%20()%20%7B%0A%20%20%20%20%20%20%20%20%24('%23TCPChoose').change(function%20()%20%7B%0A%20%20%20%20%20%20%20%20%20%20%0A%20%20%20%20%20%20%20%20%7D)%0A%20%20%20%20%20%20%7D)%0A%20%60%60%60%0A%20%0A%20%23%23%20jQuery%E5%88%A4%E6%96%AD%E5%85%83%E7%B4%A0%E6%98%AF%E5%90%A6%E6%98%BE%E7%A4%BA%E4%B8%8E%E9%9A%90%E8%97%8F%0A%20%0A%20%60if(%24(%22%23username%22).is(%22%3Ahidden%22))%7B%20%20%0A%7D%20%20%0A%60%0A%20%0A%20***%E6%88%91%E6%84%9F%E8%A7%89%60%24(function())%60%E9%87%8C%E9%9D%A2%E7%9A%84%E6%96%B9%E6%B3%95%E5%B0%B1%E7%B1%BB%E4%BC%BC%E4%BA%8E%E5%92%B1%E7%9A%84%60viewdidload%60%EF%BC%8C%20%E8%BF%9B%E6%9D%A5%E5%B0%B1%E4%BC%9A%E8%B0%83%E4%B8%80%E4%B8%8B%EF%BC%8C%E4%BD%86%E6%98%AF%E9%82%A3%E4%B8%AA%E5%85%83%E7%B4%A0%E5%A6%82%E6%9E%9C%E4%B8%8D%E5%AD%98%E5%9C%A8%E7%9A%84%E8%AF%9D%E5%B0%B1%E6%97%A0%E6%95%88***%0A%20%0A%20%23%23%20Chart.js%20%E8%87%AA%E5%AE%9A%E4%B9%89html%20legend%0A%20%60%60%60%0A%20%20options%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20legend%3A%20false%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20legendCallback%3A%20function%20(chart)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20var%20text%20%3D%20%5B%5D%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20text.push('%3Cul%3E')%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20for%20(var%20i%20%3D%200%3B%20i%20%3C%20chart.data.datasets%5B0%5D.data.length%3B%20i%2B%2B)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20text.push('%3Cli%20style%3D%22white-space%3A%20nowrap%3B%22%3E')%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20text.push('%3Cspan%20style%3D%22color%3A'%20%2B%20chart.data.datasets%5B0%5D.backgroundColor%5Bi%5D%20%2B%20'%22%3E'%20%2B%20'%26%239608'%20%2B%20'%3C%2Fspan%3E')%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20if%20(chart.data.labels%5Bi%5D)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20text.push(chart.data.labels%5Bi%5D)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20text.push('%3C%2Fli%3E')%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20text.push('%3C%2Ful%3E')%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20return%20text.join(%22%22)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%0A%20%24(%22%23storeNamesLabel%22).html(storeNameChart.generateLegend())%3B%0A%60%60%60%0A%E6%9C%80%E5%90%8E%E6%8A%8A%60generateLegend()%60%E7%94%9F%E6%88%90%E7%9A%84html%E8%B5%8B%E4%BA%88%E9%9C%80%E8%A6%81%E7%9A%84%E5%9C%B0%E6%96%B9.%0A%0A%23%23%20%E5%A4%9A%E4%B8%AAajax%2C%E9%9C%80%E8%A6%81%E5%81%9C%E6%AD%A2%E5%85%B6%E4%BD%99%0A%60%60%60%0A%20var%20ajaxRequest%20%3D%20null%3B%0A%20%20%20%20%20%20function%20todayButtonClicked()%20%7B%0A%20%20%20%20%20%20%20%20resetButtons()%3B%0A%20%20%20%20%20%20%20%20%24(%22%23allButton%22).button('loading')%3B%0A%20%20%20%20%20%20%20%20if%20(ajaxRequest)%7B%0A%20%20%20%20%20%20%20%20%20%20ajaxRequest.abort()%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20ajaxRequest%20%3D%20%24.ajax(%7B%0A%20%20%20%20%20%20%20%20%20%20url%3A%20%22%7B%7B%20path('statementConfirmed')%20%7D%7D%22%2C%0A%20%20%20%20%20%20%20%20%20%20type%3A%20'POST'%2C%0A%20%20%20%20%20%20%20%20%20%20data%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%20%20success%3A%20function%20(data)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%24(%22%23todayTableDiv%22).html(%22%22)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%24(%22%23todayTableDiv%22).append(data)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20setSpendingLabel()%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20resetButtons()%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%24(%22%23allButton%22).button('toggle')%3B%0A%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20failed%3A%20function%20()%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20console.log('failed')%3B%0A%2F%2F%20%20%20%20%20%20%20%20%20%20%20%20resetButtons()%3B%0A%2F%2F%20%20%20%20%20%20%20%20%20%20%20%20%24(%22%23allButton%22).button('toggle')%3B%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D)%3B%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20function%20confirmButtonClicked()%20%7B%0A%20%20%20%20%20%20%20%20resetButtons()%3B%0A%20%20%20%20%20%20%20%20%24(%22%23confirmedButton%22).button('loading')%3B%0A%20%20%20%20%20%20%20%20if%20(ajaxRequest)%7B%0A%20%20%20%20%20%20%20%20%20%20ajaxRequest.abort()%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20ajaxRequest%20%3D%20%24.ajax(%7B%0A%20%20%20%20%20%20%20%20%20%20url%3A%20%22%7B%7B%20path('statementToday')%20%7D%7D%22%2C%0A%20%20%20%20%20%20%20%20%20%20type%3A%20'POST'%2C%0A%20%20%20%20%20%20%20%20%20%20data%3A%20%7B%7D%2C%0A%20%20%20%20%20%20%20%20%20%20success%3A%20function%20(data)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%24(%22%23todayTableDiv%22).html(%22%22)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%24(%22%23todayTableDiv%22).append(data)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20setSpendingLabel()%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20resetButtons()%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%24(%22%23confirmedButton%22).button('toggle')%3B%0A%20%20%20%20%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20failed%3A%20function%20()%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20console.log('failed')%3B%0A%2F%2F%20%20%20%20%20%20%20%20%20%20%20%20resetButtons()%3B%0A%2F%2F%20%20%20%20%20%20%20%20%20%20%20%20%24(%22%23confirmedButton%22).button('toggle')%3B%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D)%3B%0A%20%20%20%20%20%20%7D%0A%60%60%60%0A%0A%23%23%20%E7%BB%91%E5%AE%9A%E5%9B%9E%E8%BD%A6%E9%94%AE%0A%0A%60%60%60%0A%24(%22%23searchBar%22).bind('keypress'%2Cfunction%20(event)%20%7B%0A%20%20%20%20%20%20if%20(event.keyCode%20%3D%3D%20'13')%7B%0A%20%20%20%20%20%20%20%20searchButtonClicked()%3B%0A%20%20%20%20%20%20%20%20return%20false%3B%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D)%3B%0A%60%60%60