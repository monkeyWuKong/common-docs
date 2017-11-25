# [WSGI](https://en.wikipedia.org/wiki/Web_Server_Gateway_Interface)

**Web Server Gateway Interface** ，a specification for simple and universal [interface](https://en.wikipedia.org/wiki/Interface_(computer_science)) between [web servers](https://en.wikipedia.org/wiki/Web_server) and [web applications](https://en.wikipedia.org/wiki/Web_application) or [frameworks](https://en.wikipedia.org/wiki/Web_framework) for the Python programming language。

> “和CGI类似，都是定义web服务器与web应用之间的简单接口规范。”

最初是由Phillip J定义于[PEP 333](https://www.python.org/dev/peps/pep-0333/)中，发布于**2003年12月7号日**。

现在已经被采纳为python web 应用开发的一个标准。最新版为[PEP 3333](https://www.python.org/dev/peps/pep-3333/), V1.0.1,发布于**2010年9月26日**。

WSGI包含两部分，一部分叫server或者gateway（一般是是web服务器，如Apache或者Nginx）；另外一部分是application或者framework（python scripts）。

处理一个WSGI请求时，server端执行应用，提供一些环境信息和一个回调给应用端。应用程序处理请求，并使用提供的回调函数将响应返回给服务器端。

> "原来之前写的东西都属于应用端（application）"

在server和application之间一般会有中间件（middleware）。中间件可能的作用有：

* 在更改环境变量之后，根据目标URL将请求路由到不同的应用程序对象
* 允许多个应用程序或框架在同一进程中并行运行。
* 通过在网络上转发请求和响应，进行负载平衡和远程处理
* 执行内容的后处理，如应用XSLT样式表



