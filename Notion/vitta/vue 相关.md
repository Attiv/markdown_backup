- css
- 界面渲染完
- this
- 引入外部 js
- 获取鼠标点击事件
- 编辑时 select 选择值不变
- lodash 退出forEach()
- 在 component里 input不自动 blur
- 几个控件中间宽度动态变化
- 上传文件使用 change事件
- 使用string变量调用方法
- @click.stop 失效

# css

`&:hover, &:active, &:focus` 中 `&`是父类`.class1, .class2{}` 是两个类同时的css

# 界面渲染完

```Plain
this.$nextTick(() => {
        let topHeight = $('.top-card').height()
        $('.boxes').height('calc(100% - ' + topHeight + 'px)')
      })
```

# this

`this.$emit(name, param)` 执行名字为'name'的方法

`function` 里使用 `this`

1. 函数外定义:
    
    ```Plain
    const self = this
    function (data) {
        self.a;
    }
    ```
    
2. 函数绑定:
    
    ```Plain
    function (data) {
        this.a
    }.bind(this)
    ```
    
3. 使用箭头函数
    
    ```Plain
    data => {
    this.a
    }
    ```
    

# 引入外部 js

比如:

```Plain
import vueCookie from 'vue-cookie'
import vueAxios from 'axios'

/*  基本 url 配置 */
const webapp = '/api'
const host = ''
var myUrl = host
myUrl += webapp

// 定义变量
var currentUserToken = vueCookie.get('loginToken')
var currentUserId = vueAxios.get('loginUser')
// var currentUserName = this.axios.get('loginNameexport ')
// var accountFullName = this.axios.get('accountName')// 姓名
// var accountUser = this.axios.get('accountUserName')// 用户名
// var accountEmail = this.axios.get('accountEmail')// 邮箱

var currentModuleId = getUrlParam('module') ? parseInt(getUrlParam('module')) : null
var currentProjectId = getUrlParam('project') ? parseInt(getUrlParam('project')) : null
var parentProjectId = getUrlParam('parent') ? parseInt(getUrlParam('parent')) : null
var viewUserId = getUrlParam('use1r') ? parseInt(getUrlParam('user')) : null

// 获取url参数值
function getUrlParam (name) {
  var reg = new RegExp('(^|&)' + name + '=([^&]*)(&|$)') // 构造一个含有目标参数的正则表达式对象
  var r = window.location.search.substr(1).match(reg)  // 匹配目标参数

  if (r != null) {
    return unescape(r[2])
  } else {
    return null // 返回参数值
  }
}

function bAjax (method, url, headers, dataInfo, conType, timeout, successCallback, errorCallback, async, enctype, processData) {
  let deviceType
  let header2 = {'X-Requested-With': 'XMLHttpRequest', 'Content-type': 'application/json'}
  if (headers) {
    Object.assign(headers, header2)
  } else {
    headers = header2
  }
  if (currentUserToken) {
    let autho = {'authorization': currentUserToken}
    if (headers === null) {
      headers = autho
    } else {
      Object.assign(headers, autho)
    }
  }
  if (/Android|webOS|iPhone|iPod|iPad|BlackBerry/i.test(navigator.userAgent)) {
    deviceType = 2
  } else {
    deviceType = 1
  }
  vueAxios({
    method: method,
    url: url + '?deviceType=' + deviceType,
    dataType: 'json',
    contentType: conType,
    headers: headers,
    // auth: headers,
    timeout: timeout,
    cache: false,
    enctype: enctype,
    processData: processData,
    xhrFields: {
      withCredentials: true
    },
    data: dataInfo,
    async: async,
    withCredentials: true
    // success: successCallback,
    // error: errorCallback
    // xhr: xhrCallback
  }).then(successCallback)
    .catch(errorCallback)
}

export default {
  webapp,
  host,
  myUrl,
  bAjax,
  currentUserToken,
  currentUserId,
  currentModuleId,
  currentProjectId,
  parentProjectId,
  viewUserId
}
```

# 获取鼠标点击事件

```Plain
<button @click="btnClicked(item, $event)">

<script>
btnClicked(item, event) {
    // event就是鼠标点击事件
}
</script>
```

# 编辑时 select 选择值不变

[使用Vue的set方法](https://www.jianshu.com/p/358c1974d9a5)

# lodash 退出forEach()

```Plain
在 `_.forEach()` 里使用 `return false (break)`
`return`
```

# 在 component里 input不自动 blur

可以在 `button`事件里加上延时执行

# 几个控件中间宽度动态变化

只需要制定最后边的 `margin-right`，中间的 `margin-right: auto`

# 上传文件使用 `change`事件

```Plain
<input v-show="false" type="file" :ref="`upload`"
             @change="change($event)"/>
             
async change (evt, i) {
      if (!evt.target.files || !evt.target.files.length) {
        return
      }
      const files = await uploadFile(evt.target.files, 'issue', percent => {
        this.uploading = percent
      })
      this.uploading = 0
      if (files && files[0]) {
        this.images[i] = `/application/uploadfile/${files[0]}`
        this.firstUrl = this.images[0]
        this.$forceUpdate()
      }
    },
```

如果上传相同文件，不会触发上传方法  
可以修改  
`evt.srcElement.value = ''`即可触发

# 使用string变量调用方法

```Plain
import { Message } from 'element-ui'

function message(message, type) {
  Message[type](message)
}

export {
  message
}
```

> 类似 Message.type(message)

# @click.stop 失效

```Plain
.stop 
.prevent 
.capture 
.self 
.once
```

%5Btoc%5D%0A%0A%23%20css%20%23%0A%0A%60%26%3Ahover%2C%20%26%3Aactive%2C%20%26%3Afocus%60%20%E4%B8%AD%20%60%26%60%E6%98%AF%E7%88%B6%E7%B1%BB%0A%60.class1%2C%20.class2%7B%7D%60%20%E6%98%AF%E4%B8%A4%E4%B8%AA%E7%B1%BB%E5%90%8C%E6%97%B6%E7%9A%84css%0A%0A%23%20%E7%95%8C%E9%9D%A2%E6%B8%B2%E6%9F%93%E5%AE%8C%20%23%0A%60%60%60%0A%20%20%20%20%20%20this.%24nextTick(()%20%3D%3E%20%7B%0A%20%20%20%20%20%20%20%20let%20topHeight%20%3D%20%24('.top-card').height()%0A%20%20%20%20%20%20%20%20%24('.boxes').height('calc(100%25%20-%20'%20%2B%20topHeight%20%2B%20'px)')%0A%20%20%20%20%20%20%7D)%0A%60%60%60%0A%0A%0A%23%20this%20%23%0A%0A%60this.%24emit(name%2C%20param)%60%20%E6%89%A7%E8%A1%8C%E5%90%8D%E5%AD%97%E4%B8%BA'name'%E7%9A%84%E6%96%B9%E6%B3%95%0A%0A%60function%60%20%E9%87%8C%E4%BD%BF%E7%94%A8%20%60this%60%0A%0A1.%20%E5%87%BD%E6%95%B0%E5%A4%96%E5%AE%9A%E4%B9%89%3A%0A%20%20%20%20%60%60%60%0A%20%20%20%20const%20self%20%3D%20this%0A%20%20%20%20function%20(data)%20%7B%0A%20%20%20%20%20%20%20%20self.a%3B%0A%20%20%20%20%7D%0A%20%20%20%20%60%60%60%0A2.%20%E5%87%BD%E6%95%B0%E7%BB%91%E5%AE%9A%3A%0A%20%20%20%20%60%60%60%0A%20%20%20%20function%20(data)%20%7B%0A%20%20%20%20%20%20%20%20this.a%0A%20%20%20%20%7D.bind(this)%0A%20%20%20%20%60%60%60%0A3.%20%E4%BD%BF%E7%94%A8%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0%0A%20%20%20%20%60%60%60%0A%20%20%20%20data%20%3D%3E%20%7B%0A%20%20%20%20this.a%0A%20%20%20%20%7D%0A%20%20%20%20%60%60%60%0A%20%20%20%20%0A%23%20%E5%BC%95%E5%85%A5%E5%A4%96%E9%83%A8%20js%20%23%0A%0A%E6%AF%94%E5%A6%82%3A%20%0A%60%60%60%0Aimport%20vueCookie%20from%20'vue-cookie'%0Aimport%20vueAxios%20from%20'axios'%0A%0A%2F*%20%20%E5%9F%BA%E6%9C%AC%20url%20%E9%85%8D%E7%BD%AE%20*%2F%0Aconst%20webapp%20%3D%20'%2Fapi'%0Aconst%20host%20%3D%20''%0Avar%20myUrl%20%3D%20host%0AmyUrl%20%2B%3D%20webapp%0A%0A%2F%2F%20%E5%AE%9A%E4%B9%89%E5%8F%98%E9%87%8F%0Avar%20currentUserToken%20%3D%20vueCookie.get('loginToken')%0Avar%20currentUserId%20%3D%20vueAxios.get('loginUser')%0A%2F%2F%20var%20currentUserName%20%3D%20this.axios.get('loginNameexport%20')%0A%2F%2F%20var%20accountFullName%20%3D%20this.axios.get('accountName')%2F%2F%20%E5%A7%93%E5%90%8D%0A%2F%2F%20var%20accountUser%20%3D%20this.axios.get('accountUserName')%2F%2F%20%E7%94%A8%E6%88%B7%E5%90%8D%0A%2F%2F%20var%20accountEmail%20%3D%20this.axios.get('accountEmail')%2F%2F%20%E9%82%AE%E7%AE%B1%0A%0Avar%20currentModuleId%20%3D%20getUrlParam('module')%20%3F%20parseInt(getUrlParam('module'))%20%3A%20null%0Avar%20currentProjectId%20%3D%20getUrlParam('project')%20%3F%20parseInt(getUrlParam('project'))%20%3A%20null%0Avar%20parentProjectId%20%3D%20getUrlParam('parent')%20%3F%20parseInt(getUrlParam('parent'))%20%3A%20null%0Avar%20viewUserId%20%3D%20getUrlParam('use1r')%20%3F%20parseInt(getUrlParam('user'))%20%3A%20null%0A%0A%2F%2F%20%E8%8E%B7%E5%8F%96url%E5%8F%82%E6%95%B0%E5%80%BC%0Afunction%20getUrlParam%20(name)%20%7B%0A%20%20var%20reg%20%3D%20new%20RegExp('(%5E%7C%26)'%20%2B%20name%20%2B%20'%3D(%5B%5E%26%5D*)(%26%7C%24)')%20%2F%2F%20%E6%9E%84%E9%80%A0%E4%B8%80%E4%B8%AA%E5%90%AB%E6%9C%89%E7%9B%AE%E6%A0%87%E5%8F%82%E6%95%B0%E7%9A%84%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%AF%B9%E8%B1%A1%0A%20%20var%20r%20%3D%20window.location.search.substr(1).match(reg)%20%20%2F%2F%20%E5%8C%B9%E9%85%8D%E7%9B%AE%E6%A0%87%E5%8F%82%E6%95%B0%0A%0A%20%20if%20(r%20!%3D%20null)%20%7B%0A%20%20%20%20return%20unescape(r%5B2%5D)%0A%20%20%7D%20else%20%7B%0A%20%20%20%20return%20null%20%2F%2F%20%E8%BF%94%E5%9B%9E%E5%8F%82%E6%95%B0%E5%80%BC%0A%20%20%7D%0A%7D%0A%0Afunction%20bAjax%20(method%2C%20url%2C%20headers%2C%20dataInfo%2C%20conType%2C%20timeout%2C%20successCallback%2C%20errorCallback%2C%20async%2C%20enctype%2C%20processData)%20%7B%0A%20%20let%20deviceType%0A%20%20let%20header2%20%3D%20%7B'X-Requested-With'%3A%20'XMLHttpRequest'%2C%20'Content-type'%3A%20'application%2Fjson'%7D%0A%20%20if%20(headers)%20%7B%0A%20%20%20%20Object.assign(headers%2C%20header2)%0A%20%20%7D%20else%20%7B%0A%20%20%20%20headers%20%3D%20header2%0A%20%20%7D%0A%20%20if%20(currentUserToken)%20%7B%0A%20%20%20%20let%20autho%20%3D%20%7B'authorization'%3A%20currentUserToken%7D%0A%20%20%20%20if%20(headers%20%3D%3D%3D%20null)%20%7B%0A%20%20%20%20%20%20headers%20%3D%20autho%0A%20%20%20%20%7D%20else%20%7B%0A%20%20%20%20%20%20Object.assign(headers%2C%20autho)%0A%20%20%20%20%7D%0A%20%20%7D%0A%20%20if%20(%2FAndroid%7CwebOS%7CiPhone%7CiPod%7CiPad%7CBlackBerry%2Fi.test(navigator.userAgent))%20%7B%0A%20%20%20%20deviceType%20%3D%202%0A%20%20%7D%20else%20%7B%0A%20%20%20%20deviceType%20%3D%201%0A%20%20%7D%0A%20%20vueAxios(%7B%0A%20%20%20%20method%3A%20method%2C%0A%20%20%20%20url%3A%20url%20%2B%20'%3FdeviceType%3D'%20%2B%20deviceType%2C%0A%20%20%20%20dataType%3A%20'json'%2C%0A%20%20%20%20contentType%3A%20conType%2C%0A%20%20%20%20headers%3A%20headers%2C%0A%20%20%20%20%2F%2F%20auth%3A%20headers%2C%0A%20%20%20%20timeout%3A%20timeout%2C%0A%20%20%20%20cache%3A%20false%2C%0A%20%20%20%20enctype%3A%20enctype%2C%0A%20%20%20%20processData%3A%20processData%2C%0A%20%20%20%20xhrFields%3A%20%7B%0A%20%20%20%20%20%20withCredentials%3A%20true%0A%20%20%20%20%7D%2C%0A%20%20%20%20data%3A%20dataInfo%2C%0A%20%20%20%20async%3A%20async%2C%0A%20%20%20%20withCredentials%3A%20true%0A%20%20%20%20%2F%2F%20success%3A%20successCallback%2C%0A%20%20%20%20%2F%2F%20error%3A%20errorCallback%0A%20%20%20%20%2F%2F%20xhr%3A%20xhrCallback%0A%20%20%7D).then(successCallback)%0A%20%20%20%20.catch(errorCallback)%0A%7D%0A%0Aexport%20default%20%7B%0A%20%20webapp%2C%0A%20%20host%2C%0A%20%20myUrl%2C%0A%20%20bAjax%2C%0A%20%20currentUserToken%2C%0A%20%20currentUserId%2C%0A%20%20currentModuleId%2C%0A%20%20currentProjectId%2C%0A%20%20parentProjectId%2C%0A%20%20viewUserId%0A%7D%0A%0A%60%60%60%0A%0A%23%20%E8%8E%B7%E5%8F%96%E9%BC%A0%E6%A0%87%E7%82%B9%E5%87%BB%E4%BA%8B%E4%BB%B6%20%23%0A%0A%60%60%60%0A%3Cbutton%20%40click%3D%22btnClicked(item%2C%20%24event)%22%3E%0A%0A%3Cscript%3E%0AbtnClicked(item%2C%20event)%20%7B%0A%20%20%20%20%2F%2F%20event%E5%B0%B1%E6%98%AF%E9%BC%A0%E6%A0%87%E7%82%B9%E5%87%BB%E4%BA%8B%E4%BB%B6%0A%7D%0A%3C%2Fscript%3E%0A%60%60%60%0A%0A%23%20%E7%BC%96%E8%BE%91%E6%97%B6%20select%20%E9%80%89%E6%8B%A9%E5%80%BC%E4%B8%8D%E5%8F%98%0A%5B%E4%BD%BF%E7%94%A8Vue%E7%9A%84set%E6%96%B9%E6%B3%95%5D(https%3A%2F%2Fwww.jianshu.com%2Fp%2F358c1974d9a5)%0A%0A%23%20lodash%20%E9%80%80%E5%87%BAforEach()%20%0A%0A%20%20%20%20%E5%9C%A8%20%60_.forEach()%60%20%E9%87%8C%E4%BD%BF%E7%94%A8%20%60return%20false%20(break)%60%0A%20%20%20%20%60return%20(continue)%60%0A%0A%23%20%E5%9C%A8%20component%E9%87%8C%20input%E4%B8%8D%E8%87%AA%E5%8A%A8%20blur%0A%0A%E5%8F%AF%E4%BB%A5%E5%9C%A8%20%60button%60%E4%BA%8B%E4%BB%B6%E9%87%8C%E5%8A%A0%E4%B8%8A%E5%BB%B6%E6%97%B6%E6%89%A7%E8%A1%8C%0A%0A%23%20%E5%87%A0%E4%B8%AA%E6%8E%A7%E4%BB%B6%E4%B8%AD%E9%97%B4%E5%AE%BD%E5%BA%A6%E5%8A%A8%E6%80%81%E5%8F%98%E5%8C%96%0A%0A%E5%8F%AA%E9%9C%80%E8%A6%81%E5%88%B6%E5%AE%9A%E6%9C%80%E5%90%8E%E8%BE%B9%E7%9A%84%20%60margin-right%60%EF%BC%8C%E4%B8%AD%E9%97%B4%E7%9A%84%20%60margin-right%3A%20auto%60%0A%0A%23%20%E4%B8%8A%E4%BC%A0%E6%96%87%E4%BB%B6%E4%BD%BF%E7%94%A8%20%60change%60%E4%BA%8B%E4%BB%B6%0A%60%60%60%0A%20%3Cinput%20class%3D%22needsclick%22%20v-show%3D%22false%22%20type%3D%22file%22%20%3Aref%3D%22%60upload%60%22%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%40change%3D%22change(%24event)%22%2F%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%0Aasync%20change%20(evt%2C%20i)%20%7B%0A%20%20%20%20%20%20if%20(!evt.target.files%20%7C%7C%20!evt.target.files.length)%20%7B%0A%20%20%20%20%20%20%20%20return%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20const%20files%20%3D%20await%20uploadFile(evt.target.files%2C%20'issue'%2C%20percent%20%3D%3E%20%7B%0A%20%20%20%20%20%20%20%20this.uploading%20%3D%20percent%0A%20%20%20%20%20%20%7D)%0A%20%20%20%20%20%20this.uploading%20%3D%200%0A%20%20%20%20%20%20if%20(files%20%26%26%20files%5B0%5D)%20%7B%0A%20%20%20%20%20%20%20%20this.images%5Bi%5D%20%3D%20%60%2Fapplication%2Fuploadfile%2F%24%7Bfiles%5B0%5D%7D%60%0A%20%20%20%20%20%20%20%20this.firstUrl%20%3D%20this.images%5B0%5D%0A%20%20%20%20%20%20%20%20this.%24forceUpdate()%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%2C%0A%60%60%60%0A%0A%E5%A6%82%E6%9E%9C%E4%B8%8A%E4%BC%A0%E7%9B%B8%E5%90%8C%E6%96%87%E4%BB%B6%EF%BC%8C%E4%B8%8D%E4%BC%9A%E8%A7%A6%E5%8F%91%E4%B8%8A%E4%BC%A0%E6%96%B9%E6%B3%95%0A%E5%8F%AF%E4%BB%A5%E4%BF%AE%E6%94%B9%20%60evt.srcElement.value%20%3D%20''%60%E5%8D%B3%E5%8F%AF%E8%A7%A6%E5%8F%91%0A%0A%23%20%E4%BD%BF%E7%94%A8string%E5%8F%98%E9%87%8F%E8%B0%83%E7%94%A8%E6%96%B9%E6%B3%95%0A%60%60%60%0Aimport%20%7B%20Message%20%7D%20from%20'element-ui'%0A%0Afunction%20message(message%2C%20type)%20%7B%0A%20%20Message%5Btype%5D(message)%0A%7D%0A%0Aexport%20%7B%0A%20%20message%0A%7D%0A%0A%60%60%60%0A%3E%20%E7%B1%BB%E4%BC%BC%20%60Message.type(message)%60%0A%0A%23%20%40click.stop%20%E5%A4%B1%E6%95%88%0A%0A%60%60%60%0A.stop%20%0A.prevent%20%0A.capture%20%0A.self%20%0A.once%0A%0A%60%60%60