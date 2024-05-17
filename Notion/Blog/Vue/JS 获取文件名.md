1. 正则法

```Plain
var file=$("input[name='file']").val();  
var filename=file.replace(/.*(\\/|\\\\)/, "");  
var fileExt=(/[.]/.exec(filename)) ? /[^.]+$/.exec(filename.toLowerCase()) : ''; 
```

**filename**得到文件名

**fileExt**得到后缀名

```Plain
var location=$("input[name='file']").val();  
 var point = location.lastIndexOf(".");  
  
 var type = location.substr(point);  
 if(type==".jpg"||type==".gif"||type==".JPG"||type==".GIF"){  
           
 }  
```