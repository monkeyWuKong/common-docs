# [python threading](https://docs.python.org/2/library/threading.html#module-threading)

## 方法与对象

返回当前active的线程数
```python
threading.active_count()
threading.activeCount()
```

条件变量(一个条件变量允许一个或者多个线程等待直到被其它线程通知到)
```
threading.Condition()
```

返回当前的线程对象
```
threading.current_thread()
threading.currentThread()
```

返回一列当前active的线程对象
```
threading.enumerate()
```

生成一个event对象（True or False with `set()`）
```
threading.Event()
```

基本锁(一旦线程获取了它，后续获取它的尝试就会被阻塞，直到它被释放；任何线程都可能释放它。)
```python
threading.Lock()
Lock.acquire([blocking])#Acquire a lock, blocking or non-blocking.
Lock.release()#Release a lock.
```

可重入的锁（谁获取谁释放，其它的线程也可以继续获取这个锁）

[资料 - 可重入锁和不可重入锁](https://www.cnblogs.com/dj3839/p/6580765.html)
```
threading.RLock()
```

信号量
```
threading.Semaphore([value])
```

有限信号量
```
threading.BoundedSemaphore([value])
```

线程类
```
class threading.Thread
```

定时器
```
class threading.Timer
```





