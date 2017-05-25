[TOC]



# celery的工作流

## 任务的签名

### 生成签名

####signature()

通过`signature()`函数，传入任务函数名，任务函数的参数，任务执行的选项，可以生成一个任务的签名。

```python
>>> from celery import signature
>>> signature('tasks.add', args=(2, 2), countdown=10)
tasks.add(2, 2)
```

#### 任务自带的signature()函数

```python
>>> add.signature((2, 2), countdown=10)
tasks.add(2, 2)
```

**缩写**

```python
>>> add.s(2, 2)
tasks.add(2, 2)
```

**支持Keyword arguments**

```python
>>> add.s(2, 2, debug=True)
tasks.add(2, 2, debug=True)
```

**查询签名的各个属性**

```python
>>> s = add.signature((2, 2), {'debug': True}, countdown=10)
>>> s.args
(2, 2)
>>> s.kwargs
{'debug': True}
>>> s.options
{'countdown': 10}
```

签名也支持`delay()`和 `apply_async()`的调用方式，当然也包括直接调用。

```python
>>> ss = add.s(2,5)
>>> r = ss.delay()
>>> r.get()
7
```

**apply_async**

```python
>>> add.apply_async(args, kwargs, **options)
>>> add.signature(args, kwargs, **options).apply_async()

>>> add.apply_async((2, 2), countdown=1)
>>> add.signature((2, 2), countdown=1).apply_async()

```

对于`s()`方法， 你无法指定任务执行选项（options），但是你可以使用`set`方法。

```python
>>> add.s(2, 2).set(countdown=1)
proj.tasks.add(2, 2)
```

### [Partials可分性](http://docs.celeryproject.org/en/latest/userguide/canvas.html#partials) 

对签名指定额外的`args, kwargs, or options`， 针对`apply_async/delay`。

```python
>>> partial = add.s(2)          # incomplete signature
>>> partial.delay(4)            # 4 + 2
>>> partial.apply_async((4,))   # same
```

-

```python
>>> s = add.s(2, 2)
>>> s.delay(debug=True)                    # -> add(2, 2, debug=True)
>>> s.apply_async(kwargs={'debug': True})  # same
```

**options覆盖**

```python
>>> s = add.signature((2, 2), countdown=10)
>>> s.apply_async(countdown=1)  # countdown is now 1
```

**对签名克隆衍生（变异）**

```python
>>> s = add.s(2)
proj.tasks.add(2)

>>> s.clone(args=(4,), kwargs={'debug': True})
proj.tasks.add(4, 2, debug=True)
```

###[Immutability 不可变性](http://docs.celeryproject.org/en/latest/userguide/canvas.html#immutability)

有时你希望指定一个回调不会被增加任何额外的参数，你可以将签名设置成永不可变的。

```python
>>> add.apply_async((2, 2), link=reset_buffers.signature(immutable=True))
```

 `.si()`是缩写，也可以用来设置不可变。

```python
>>> add.apply_async((2, 2), link=reset_buffers.si())
```

对于不可变的参数，只有` execution options`可以被设置，因此，额外的`args/kwargs`将不支持。

**Note**

In this tutorial I sometimes use the prefix operator ~ to signatures. You probably shouldn’t use it in your production code, but it’s a handy shortcut when experimenting in the Python shell:

```python
>>> ~sig

>>> # is the same as
>>> sig.delay().get()
```

### [Callbacks](http://docs.celeryproject.org/en/latest/userguide/canvas.html#callbacks)

对于 `apply_async`方法使用`link`参数可以将callbacks添加到任意任务。

```python
add.apply_async((2, 2), link=other_task.s())
```

-

```python
add.apply_async((2, 2), link=add.s(8))
```

先执行2+2，另外一个任务会执行4+8.

## [The Primitives](http://docs.celeryproject.org/en/latest/userguide/canvas.html#the-primitives) 原语

### 概述

**group**

包含了一组平行任务的任务签名。

**chain**

让我们可以将任务以链条的形式组织起来，一个接着一个的执行。

**chord**

一个group头和一个body，当group中所有的任务都执行完毕后，再执行body中的任务。

**map**



**starmap**

**chunks**



###Chains

###Groups

###Chords

###Map & Starmap

###Chunks

