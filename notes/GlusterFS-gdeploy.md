

## 什么是 gdeploy

一个工具，用来安装部署GlusterFS。

用到了[ansible](https://linux.cn/article-4215-1.html)。

>**ansible** 是新出现的自动化运维工具，基于Python开发，集合了众多运维工具（puppet、cfengine、chef、func、fabric）的优点，实现了批量系统配置、批量程序部署、批量运行命令等功能。
>
>ansible是基于模块工作的，本身没有批量部署的能力。真正具有批量部署的是ansible所运行的模块，ansible只是提供一种框架。主要包括：
>
>(1)、连接插件connection plugins：负责和被监控端实现通信；
>
>(2)、host inventory：指定操作的主机，是一个配置文件里面定义监控的主机；
>
>(3)、各种模块核心模块、command模块、自定义模块；
>
>(4)、借助于插件完成记录日志邮件等功能；
>
>(5)、playbook：剧本执行多个任务时，非必需可以让节点一次性运行多个任务。

gdeploy 是依据模块化的特点来设计的，根据你的配置文件，可以用来部署任意软件。

gdeploy 可以用来设置GlusterFS的bricks，创建GlusterFS的卷，以及将其挂载到一个或者多个安装了ansible的服务器。

## github主页

[https://github.com/gluster/gdeploy](https://github.com/gluster/gdeploy)