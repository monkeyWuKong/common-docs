# application

Celery使用之前必须先实例化，此实例（instance）称为一个应用（application）或者简称为app。

application是线程安全的（thread-safe），因此多个不同配置、组件、任务的celery application可以在一个进程空间之内共存。

```
>>> from celery import Celery
>>> app = Celery()
>>> app
<Celery __main__:0x100469fd0>
```

上面代码中最后一行表示了： app 类的名字（Celery）， 当前主模块的名字（`__main__`）， 对象app在内存中的地址（0x100469fd0）。

## Main Name 

当你在Celery中下发一个task message的时候，message 不会包含任何源代码，只有你想执行的任务的名字。 这个跟internet中host names的工作方式有点类似： 每个worker会维护一个任务名字的表（mapping of task names），映射到任务真正的function， 叫做任务注册表（task registry）。

```
>>> @app.task
... def add(x, y):
...     return x + y

>>> add
<@task: __main__.add>

>>> add.name
__main__.add

>>> app.tasks['__main__.add']
<@task: __main__.add>
```

这里又出现了`__main__`， 不管什么时候，只要Celery找不到任务所属的模块(module)， Celery会使用main module name去生成任务名的开头(begging of the task name)。

这只是在有限的使用场景中的一个问题（开头会出现`__main__`）:

* 如果任务所在的模块以一个程序运行时
* application在python shell 中创建时

看下面的代码：

```
from celery import Celery
app = Celery()

@app.task
def add(x, y): return x + y

if __name__ == '__main__':
    app.worker_main()
```

当上面的模块作为一个程序单独执行的时候，任务名会以`__main__`开头； 当模块被import到另外一个进程中时，调用任务时，任务名的开头就会是“tasks”(任务所在模块的名字)。

```
>>> from tasks import add
>>> add.name
tasks.add
```

你也可以给任务模块指定其它的名字：

```
>>> app = Celery('tasks')
>>> app.main
'tasks'

>>> @app.task
... def add(x, y):
...     return x + y

>>> add.name
tasks.add
```

参考资料 [Names](http://docs.celeryproject.org/en/latest/userguide/tasks.html#task-names)

## Configuration

一系列的配置可以用于指定Celery的工作方式。你可以直接对Celery实例（app instance）进行设置，也可以用专门的模块来设置。

对于实例化了的Celery对象app， 配置属性为 `app.conf`.

```
>>> app.conf.timezone
'Europe/London'
```

你可以直接更改配置：

```
>>> app.conf.enable_utc = True
```

或者你可以一次更新多个配置，你可以用`update` 方法：

```
>>> app.conf.update(
...     enable_utc=True,
...     timezone='Europe/London',
...)
```

configration 对象包含了多个配置字典，优先顺序如下：

1. 运行环境（run-time）中的改变
2. 专门的配置模块（如果有的话）
3. 默认配置（[celery.app.defaults](http://docs.celeryproject.org/en/latest/reference/celery.html#celery.Celery.add_defaults)）

>see also:

>[Configuration reference](http://docs.celeryproject.org/en/latest/userguide/configuration.html#configuration)
>
>完整的配置列表以及它们的默认值。

## config_from_object

`app.config_from_object()`可以从configuration object加载配置。

object可以是一个配置模块，或者任何一个包含了配置的object。

注意，之前设置的配置会被config_from_object的调用重置，因此如果想增加额外的配置你最好是在config_from_object调用之后。

### 例子1 ： 使用模块的名字

` app.config_from_object()`可以完全兼容python 模块的名字， 或者python attribute 的名字如： `celeryconfig`, `myproj.config.celery`, or `myproj.config:CeleryConfig`.

```
from celery import Celery

app = Celery()
app.config_from_object('celeryconfig')
```

`celeryconfig`可能如下：

`celeryconfig.py`

```
enable_utc = True
timezone = 'Europe/London'
```

 app可以直接`import celeryconfig`来使用。
 
### 例子2： 传入一个真实的模块对象

你可以直接传入一个已经imported的module object， 但是一般不建议这么做。

>**Tip**
>
>Using the name of a module is recommended as this means the module does not need to be serialized when the prefork pool is used. 如果你碰到configuration problems 或者 pickle errors 你可以试着使用此种方法.

```
import celeryconfig

from celery import Celery

app = Celery()
app.config_from_object(celeryconfig)
```

### 例子3 ： 使用 configuration class/object

```
from celery import Celery

app = Celery()

class Config:
    enable_utc = True
    timezone = 'Europe/London'

app.config_from_object(Config)
# or using the fully qualified name of the object:
# app.config_from_object('module:Config')
```

## config_from_envvar

config_from_envvar()从环境变量获取配置模块的名字。

例如，从一个指定的环境变量 CELERY_CONFIG_MODULE 加载配置模块。

```
import os
from celery import Celery

#: Set default configuration module name
os.environ.setdefault('CELERY_CONFIG_MODULE', 'celeryconfig')

app = Celery()
app.config_from_envvar('CELERY_CONFIG_MODULE')
```

然后你就可以通过环境变量指定配置模块:

```
$CELERY_CONFIG_MODULE="celeryconfig.prod" celery worker -l info
```

## Censored configuration经过检查的配置

如果你想打印配置，当作调试信息，你可能想过滤出敏感信息，诸如密码，API的密钥（key）。这里，Celery有一些工具可以展示配置信息，其中一个就是[humanize()](http://docs.celeryproject.org/en/latest/reference/celery.app.utils.html#celery.app.utils.Settings.humanize)。

```
>>> app.conf.humanize(with_defaults=False, censored=True)
```

这个方法将配置信息返回为字符串列表，虽然仅包含对默认配置做出的修改，但是你可以使能 `with_defaults` 参数将内建的默认键值对包含进来。

If you instead want to work with the configuration as a dictionary, you can use the `table()` method:

```
>>> app.conf.table(with_defaults=False, censored=True)
```

注意：Celery不会移除所有敏感的信息。Celery是使用正则表达式去搜寻key的名字，如果添加包含敏感信息的自定义设置，则应使用芹菜标识为secret的名称命名key。

包含如下子字符串的设置会被检查：

`API, TOKEN, KEY, SECRET, PASS, SIGNATURE, DATABASE`

[Laziness](http://docs.celeryproject.org/en/latest/userguide/application.html#laziness)

application instance is lazy， 如果不是需要，不会被计算（evaluated）。

创建一个Celery实例只会做如下动作：

1. 创建一个逻辑的clock instance， 被所有event使用。






















