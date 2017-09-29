---
title: 使用 nginx + uWSGI 部署 Sanic
categories:
- 技术
tags:
- Python
- Web
- Sanic
- nginx
- uWSGI
---

## Sanic 是什么

首先，简单介绍一下 [Sanic](https://github.com/channelcat/sanic)。

Sanic 是和 Flask 非常像的一个基于 Python 的 Web 框架，比 Flask 相比，它是基于 Python 3.5 的异步框架。由于使用到了基于 uvloop 的 IO 模型，并发及运行效率都很高。所以 Sanic 自称：Gotta go fast!

同时我们公司的小伙伴也在工作中建立了一个CMS：[Sanic-CMS](https://github.com/JoshYuJump/sanic-cms)


## http_proxy

比较简单的方法是使用 nginx 的 http_proxy。

Sanic 自带 Web server，直接通过 `python3 app.py` 的方式即可运行。

```
location / {
    proxy_pass http://localhost:8000;
} 
```

虽然这样比较简单，但也有几个比较突出的问题：
1. Sanic 自带的 Web server 能不能像 tornado 自带的 server 一样用于生产环境
2. nginx 与 Sanic 应用通过 http 通讯不算是一种高效的方式



## uWSGI 

Sanic 官方文档推荐使用 Gunicorn。

这个 section 本来应该有一堆 benchmark 的，基于两点不想继续写接下来的篇幅：

1. 最近在读 Sanic 源码，感觉是个糟糕的应用

2. 忙/懒


## 结论

Sanic 以 asyncio 而出名，网红级的新框架。当然很多粉丝只是看到了网上传递的神奇 benchmark。
个人认为 Sanic 本身的代码是需要重构才能是一个合格的框架的！
