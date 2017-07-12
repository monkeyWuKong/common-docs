
## Requirements for Packaging and Distributing

1. 确定已经满足[requirements for installing packages](https://packaging.python.org/tutorials/installing-packages/#installing-requirements)

2. 安装 twine
   
   `pip install twine`
   
    上传你的发布的包到PyPI会用到这个。

## Configuring your Project

### 初始化文件

#### setup.py

setup.py是你工程的根目录的最重要的文件。例如，你可以参考[PyPA sample project](https://github.com/pypa/sampleproject)里的[setup.py](https://github.com/pypa/sampleproject/blob/master/setup.py).

setup.py主要有2个作用：

1. 你的项目的各个方面的配置信息会在这个文件里面。setup.py的主要特点就是包含了一个全局的`setup()`函数。这个函数的参数值指明了你的项目如何被定义。重要的参数会在下面的段落解释说明。

2. 运行各种和打包任务相关的命令行的接口， 想获取可用的命令有哪些，执行`python setup.py --help-commands`。

#### setup.cfg

setup.cfg是一个ini文件，包含了对于setup.py 命令的默认选项。可以参见例子： [setup.cfg](https://github.com/pypa/sampleproject/blob/master/setup.cfg).

#### README.rst

一个项目应该包含一个readme文件用来说明项目的目的。通用的做法是使用reStructuredText语法编写，拓展名为“rst”，不过不是必须。

例子： [README.rst](https://github.com/pypa/sampleproject/blob/master/README.rst)

#### MAINFEST.in

在某些场景下，有些额外的文件没有被自动包含到发布中，你想增加进去，这个时候可以使用MAINFEST.in。  查看包含了哪些，查看章节[Specifying the files to distribute](https://docs.python.org/3.4/distutils/sourcedist.html#specifying-the-files-to-distribute).

例子： [MAINFEST.in](https://github.com/pypa/sampleproject/blob/master/MANIFEST.in)

编写MAINFEST.in的更多详细细节参见[The MAINFEST.in template](https://docs.python.org/2/distutils/sourcedist.html#the-manifest-in-template)

#### LICENSE.txt

每个软件包都应包括对于发布的详细条款的许可证文件。在很多管辖范围之内， 没有许可证的软件包是无法被其他人合法的使用或者发布的，除了软件持有者。如果你清楚你自己该选择哪个许可证， 可以点击资源： [ GitHub’s Choose a License](https://choosealicense.com/). 或者向律师咨询。

例子： [LICENSE.txt](https://github.com/pypa/sampleproject/blob/master/LICENSE.txt)

#### <你的包>

虽然并不是必须的， 最佳实践就是在根目录下放上你的模块，模块名字和你的工程一模一样，或者很相似也可以。

例子： [sample](https://github.com/pypa/sampleproject/tree/master/sample)

### setup() args

As mentioned above, The primary feature of `setup.py` is that it contains a global `setup()` function. The keyword arguments to this function are how specific details of your project are defined.

最有用的参数说明：

#### name

即你的工程的名字。决定了你的项目会如何显示在[PyPI](https://packaging.python.org/glossary/#term-python-package-index-pypi)中.根据[PEP 508](https://www.python.org/dev/peps/pep-0508), 合法的名字必须如下：

* 仅包含ASCII字符，数字，下划线(`_`), 横杠(`-`), 句点(`.`)

* 开始和结尾必须是ASCII字符或者数字

项目名字的比较是不区分大小写的。中间可以有任意多个分隔符(`_`,`-`,`.`).

举例，用户下载你的包时可以使用如下任何一个名字：

```
Cool-Stuff
cool.stuff
COOL_STUFF
CoOl__-.-__sTuFF
```

#### version

`version='1.2.0'`

即你的项目的当前版本号。

参见 [Choosing a versioning scheme](https://packaging.python.org/tutorials/distributing-packages/#choosing-a-versioning-scheme)获取更多，看你想通过版本号传递给用户哪些通用信息。

If the project code itself needs run-time access to the version, the simplest way is to keep the version in both setup.py and your code. If you’d rather not duplicate the value, there are a few ways to manage this. See the “Single-sourcing the package version” Advanced Topics section.

#### description

```
description='A sample Python project',
long_description=long_description,
```

项目的简单描述。

These values will be displayed on PyPI if you publish your project.

#### url

`url='https://github.com/pypa/sampleproject',`

你的项目的主页

#### author

```
author='The Python Packaging Authority',
author_email='pypa-dev@googlegroups.com',
```

作者信息

#### license

`license=''MIT`

你使用的许可证

#### classifiers

```
classifiers=[
    # How mature is this project? Common values are
    #   3 - Alpha
    #   4 - Beta
    #   5 - Production/Stable
    'Development Status :: 3 - Alpha',

    # Indicate who your project is intended for
    'Intended Audience :: Developers',
    'Topic :: Software Development :: Build Tools',

    # Pick your license as you wish (should match "license" above)
     'License :: OSI Approved :: MIT License',

    # Specify the Python versions you support here. In particular, ensure
    # that you indicate whether you support Python 2, Python 3 or both.
    'Programming Language :: Python :: 2',
    'Programming Language :: Python :: 2.6',
    'Programming Language :: Python :: 2.7',
    'Programming Language :: Python :: 3',
    'Programming Language :: Python :: 3.2',
    'Programming Language :: Python :: 3.3',
    'Programming Language :: Python :: 3.4',
],
```

提供对项目进行分类的分类器列表。For a full listing, see [https://pypi.python.org/pypi?%3Aaction=list_classifiers]([https://pypi.python.org/pypi?%3Aaction=list_classifiers).

Although the list of classifiers is often used to declare what Python versions a project supports, this information is only used for searching & browsing projects on PyPI, not for installing projects. To actually restrict what Python versions a project can be installed on, use the python_requires argument.

#### keywords

```
keywords='sample setuptools development',
```

列出你工程中的关键词

#### packages

```
packages=find_packages(exclude=['contrib', 'docs', 'tests*']),
```

列出要被包含到项目的[packages](https://packaging.python.org/glossary/#term-import-package).  虽然可以手工的包含进去, `setuptools.find_packages`会自动查找。

`exclude`参数可以忽略不需要的包。

#### install_requires

`install_requires=['peppercorn'],`

install_requires应该指定项目需要哪些依赖才能正常运行。 当项目被pip安装时， 这个设置可以帮助安装依赖包。

更多信息： [install_requires vs Requirements files](https://packaging.python.org/discussions/install-requires-vs-requirements/#install-requires-vs-requirements-files).

#### python_requires

当你的项目必须使用某个版本的python时，设置python_requires。 值按照合适的[PEP 440](https://www.python.org/dev/peps/pep-0440) 版本说明字符串， 这样可以阻止项目安装在不合法的python环境中。举例你想设置为 Python 3+ , 这么写:

`python_requires='>=3'`

If your package is for Python 3.3 and up but you’re not willing to commit to Python 4 support yet, write:

`python_requires='~=3.3',`

If your package is for Python 2.6, 2.7, and all versions of Python 3 starting with 3.3, write:

`python_requires='>=2.6, !=3.0.*, !=3.1.*, !=3.2.*, <4',`

>**Note**: Support for this feature is relatively recent. Your project’s source distributions and wheels (see Packaging your Project) must be built using at least version 24.2.0 of setuptools in order for the python_requires argument to be recognized and the appropriate metadata generated.
In addition, only versions 9.0.0 and higher of pip recognize the python_requires metadata. Users with earlier versions of pip will be able to download & install projects on any Python version regardless of the projects’ python_requires values.

#### package_data

```
package_data={
    'sample': ['package_data.dat'],
},
```

经常，额外的文件需要被集成到[package](https://packaging.python.org/glossary/#term-import-package)中.这些文件通常是与包实现密切相关的数据，或者包含有可能使用程序包的程序员感兴趣的文档的文本文件。这些文件称为“包数据”。

该值必须是一个从包名称映射到应该复制到包中的相对路径名列表。路径被解释为与包含包的目录相对应。

更多参见 [Including Data Files](https://setuptools.readthedocs.io/en/latest/setuptools.html#including-data-files)

#### data_files

`data_files=[('my_data', ['data/data_file'])],`

虽然配置package_data满足大多数需求，在某些情况下，您可能需要将数据文件你包外。data_files指令允许你这样做。

#### scripts

虽然`setup()`用`scripts` 参数支持在正式安装之前预先配置，推荐的方法来实现跨平台的兼容性是使用[console_scripts](https://packaging.python.org/tutorials/distributing-packages/#console-scripts)入口点（见下文）。

#### entry_points

```
entry_points={
  ...
},
```

Use this keyword to specify any plugins that your project provides for any named entry points that may be defined by your project or others that you depend on.

For more information, see the section on [Dynamic Discovery of Services and Plugins](https://setuptools.readthedocs.io/en/latest/setuptools.html#dynamic-discovery-of-services-and-plugins) from the [setuptools](https://packaging.python.org/key_projects/#setuptools) docs.

用的最多的entry point是 `console_scripts`,见如下：

#### [console_scripts](https://packaging.python.org/tutorials/distributing-packages/#console-scripts)

```
entry_points={
    'console_scripts': [
        'sample=sample:main',
    ],
},
```

### Choosing a versioning scheme

## Working in "Development Mode"

## [Packaging your Project](https://packaging.python.org/tutorials/distributing-packages/#console-scripts)

### Source Distribuytions

配置好之后，在项目的根目录执行：

```
python setup.py sdist
```

### Wheels

**wheel** : 构建好了的包，可以无需构建而直接安装。安装wheel比安装源码包快得多。

If your project is pure python (i.e. contains no compiled extensions) and natively supports both Python 2 and 3, then you’ll be creating what’s called a *Universal Wheel* (see section below).

If your project is pure python but does not natively support both Python 2 and 3, then you’ll be creating a “Pure Python Wheel” (see section below).

If you project contains compiled extensions, then you’ll be creating what’s called a *Platform Wheel* (see section below).

Before you can build wheels for your project, you’ll need to install the wheel package:

`pip install wheel`

#### Universal Wheels



#### Pure Python Wheels

#### Pure Python Wheels