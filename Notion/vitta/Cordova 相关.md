[toc]

## <video> 在iPhone上自动全屏

在 `src-cordova/config.xml` 里 加入:  
  
`<preference name="AllowInlineMediaPlayback" value="true" />`  
在 html里加入  
`playsinline`:  
  
`<video controls autoplay playsinline></video>`