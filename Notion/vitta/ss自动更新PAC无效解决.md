[转自](https://www.jianshu.com/p/8046e9930705)

原因是gfwlist.txt对应的google code链接失效，解决方法是手动下载gfwlist.txt, 转成pac之后放到默认存放位置.

获取gfwlist.txt, 最新地址:

> https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt.

`wget https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt`

安装gfwlist2pac`pip install gfwlist2pac`  
转pac  
`gfwlist2pac -i gfwlist.txt -f gfwlist.js -p "SOCKS5 127.0.0.1:1080;"`  
拷贝新生成的gfwlist.js到ss pac目录.  
首先ss点击编辑自动模式的PAC会打开一个目录，该目录就是PAC的默认存放位置，mac下为~/.ShadowsocksX。然后把生成的gfwlist.js copy到目录覆盖之前的文件。  

%5B%E8%BD%AC%E8%87%AA%5D(https%3A%2F%2Fwww.jianshu.com%2Fp%2F8046e9930705)%0A%0A%E5%8E%9F%E5%9B%A0%E6%98%AFgfwlist.txt%E5%AF%B9%E5%BA%94%E7%9A%84google%20code%E9%93%BE%E6%8E%A5%E5%A4%B1%E6%95%88%EF%BC%8C%E8%A7%A3%E5%86%B3%E6%96%B9%E6%B3%95%E6%98%AF%E6%89%8B%E5%8A%A8%E4%B8%8B%E8%BD%BDgfwlist.txt%2C%20%E8%BD%AC%E6%88%90pac%E4%B9%8B%E5%90%8E%E6%94%BE%E5%88%B0%E9%BB%98%E8%AE%A4%E5%AD%98%E6%94%BE%E4%BD%8D%E7%BD%AE.%0A%0A%E8%8E%B7%E5%8F%96gfwlist.txt%2C%20%E6%9C%80%E6%96%B0%E5%9C%B0%E5%9D%80%3A%0A%3E%20https%3A%2F%2Fraw.githubusercontent.com%2Fgfwlist%2Fgfwlist%2Fmaster%2Fgfwlist.txt.%0A%0A%60wget%20https%3A%2F%2Fraw.githubusercontent.com%2Fgfwlist%2Fgfwlist%2Fmaster%2Fgfwlist.txt%60%0A%0A%E5%AE%89%E8%A3%85gfwlist2pac%0A%60pip%20install%20gfwlist2pac%60%0A%E8%BD%ACpac%0A%60gfwlist2pac%20-i%20gfwlist.txt%20-f%20gfwlist.js%20-p%20%22SOCKS5%20127.0.0.1%3A1080%3B%22%60%0A%E6%8B%B7%E8%B4%9D%E6%96%B0%E7%94%9F%E6%88%90%E7%9A%84gfwlist.js%E5%88%B0ss%20pac%E7%9B%AE%E5%BD%95.%0A%E9%A6%96%E5%85%88ss%E7%82%B9%E5%87%BB%E7%BC%96%E8%BE%91%E8%87%AA%E5%8A%A8%E6%A8%A1%E5%BC%8F%E7%9A%84PAC%E4%BC%9A%E6%89%93%E5%BC%80%E4%B8%80%E4%B8%AA%E7%9B%AE%E5%BD%95%EF%BC%8C%E8%AF%A5%E7%9B%AE%E5%BD%95%E5%B0%B1%E6%98%AFPAC%E7%9A%84%E9%BB%98%E8%AE%A4%E5%AD%98%E6%94%BE%E4%BD%8D%E7%BD%AE%EF%BC%8Cmac%E4%B8%8B%E4%B8%BA~%2F.ShadowsocksX%E3%80%82%E7%84%B6%E5%90%8E%E6%8A%8A%E7%94%9F%E6%88%90%E7%9A%84gfwlist.js%20copy%E5%88%B0%E7%9B%AE%E5%BD%95%E8%A6%86%E7%9B%96%E4%B9%8B%E5%89%8D%E7%9A%84%E6%96%87%E4%BB%B6%E3%80%82%0A