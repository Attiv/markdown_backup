查找所有容器

```Plain
docker ps -a
```

[![](https://img-blog.csdn.net/20180122104017069?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJ3MTIxMzg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)](https://img-blog.csdn.net/20180122104017069?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJ3MTIxMzg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

找出我们想要的容器名字

查找容器长 ID

```Plain
docker inspect -f '{{.ID}}' python
```

[![](https://img-blog.csdn.net/20180122104105610?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJ3MTIxMzg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)](https://img-blog.csdn.net/20180122104105610?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJ3MTIxMzg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

拷贝本地文件到容器

```Plain
docker cp 本地路径 容器长ID:容器路径

docker cp /Users/xubowen/Desktop/auto-post-advance.py 38ef22f922704b32cf2650407e16b146bf61c221e6b8ef679989486d6ad9e856:/root/auto-post-advance.py
```

[![](https://img-blog.csdn.net/20180122104138604?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJ3MTIxMzg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)](https://img-blog.csdn.net/20180122104138604?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGJ3MTIxMzg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

> 本文由简悦 SimpRead 转码