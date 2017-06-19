# Sphinx Start

## 资料

[官网](http://www.sphinx-doc.org/en/stable/index.html)

[开始](http://www.sphinx-doc.org/en/stable/tutorial.html)

## start

安装环境: centos 7.2 64位

`pip install sphinx`


安装完毕之后的设置，逐个设置即可：

`sphinx-quickstart`


完毕之后的目录结构：

```
[root@node128 my_sphinx]# tree
.
├── build
├── make.bat
├── Makefile
└── source
    ├── conf.py
    ├── index.rst
    ├── _static
    └── _templates
```

**什么是master document**

包含`toctree`指令的文件。如上面的index.rst。

```
[root@node128 my_sphinx]# cat source/index.rst 
.. Athena documentation master file, created by
   sphinx-quickstart on Fri Jun 16 17:18:18 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Athena's documentation!
==================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
```

**document name**

对于reST语法类型的文件，会有不同的后缀名，sphinx不关心后缀名。

对于不同的操作系统，目录分隔符可能不一样，sphinx统一为斜杠`/`。

只要提到文件，sphinx默认去sphinx的根目录中去找。

合法的文件名： `index`,`library/zipfile`,`reference/datamodel/types`.


**[ref 跨文件引用](http://www.sphinx-doc.org/en/stable/markup/inline.html#role-ref)**

在要引用的内容前面加上引用标签：

`.. _lable-name`

用的时候：  ref:\`label-name\`


**[Documenting objects](http://www.sphinx-doc.org/en/stable/tutorial.html#enumerate)**

Sphinx的一个主要的目标就是将一个域内的对象合理的文档化。比如python是一个域，域内有function，class等对象。

> 用法其实和标签引用差不多，就是在代码前面加个标记，然后在其它的地方直接引用标记就可以。然后sphinx会给代码加上美化效果。sphinx默认的是python，其它域如c++需要自行配置。


## Installation on Windows

* Python installed.
* pip install sphinx
* How to make? -->  cd to your proj_dir , then `./make.bat html`. 
