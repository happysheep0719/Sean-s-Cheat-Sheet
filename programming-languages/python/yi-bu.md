# Python异步编程

参考：

- [深入理解Python异步编程（上）](http://aju.space/2017/07/31/Drive-into-python-asyncio-programming-part-1.html)
- [代码参考](https://github.com/denglj/aiotutorial/blob/master/part_1/generator.py)
- [Tornado关于异步非阻塞IO的文档](http://www.tornadoweb.org/en/stable/guide/async.html)
- [Tornado关于协程的文档](http://www.tornadoweb.org/en/stable/guide/coroutines.html)
- [解释Future那一块的文字](https://www.binss.me/blog/analyse-the-implement-of-coroutine-in-tornado/)

假设存在业务逻辑 A --> B --> C

A，B，C内部都是同步的，并且把阻塞等待IO的操作用注册回调的方式取代了。

A，B，C可以是别人写好的异步库，也可以是自己写的异步的逻辑。

异步A，B负责：

- 调用注册回调函数，以便让程序进入下一个状态。
    1. 回调函数负责**提取IO返回的结果**，并存储在Future对象里
    2. 回调函数也负责执行**返回上文**操作。
- A，B都会返回Future对象，对象内部的内容记录了回调函数和A，B操作执行后IO返回的结果。

Future的设计目标是作为协程(coroutine)和IOLoop的媒介，从而将协程和IOLoop关联起来。

```python
class Future:
    def __init__(self):
        self.result = None
        self._callbacks = []

    def add_done_callback(self, fn):
        self._callbacks.append(fn)

    def set_result(self, result):
        self.result = result
        for fn in self._callbacks:
            fn(self)

```

协程写法可以如下：

```python
def app():
    yield A()
    yield B()
    yield C()
```

事件驱动的主Loop负责检查Event，然后执行注册Event的回调函数如下：

```python
def loop():
    events = selector.select()
    for event_key, event_mask in events:
        callback = event_key.data
        callback()
```

**使用Task对象的Step函数**

1. **调用上文，并把下文的入口放在上文里**
2. **把IO输出的结果输出给下文**

实现的方式是在上文返回的Future对象中，加入下文入口的回调函数采用。类似于Tornado的Runner：

```python
class Task:
    def __init__(self, coro):
        self.coro = coro
        f = Future()
        f.set_result(None)
        self.step(f)

    def step(self, future):
        # 1. 执行上文，得到返回的Future对象
        try:
            next_future = self.coro.send(future.result) 
        except StopIteration:
            return
 
        # 2. 把下文入口加入到上文的Future的回调中
        next_future.add_done_callback(self.step) 
```


为什么要大费周章发明异步框架？

- 性能好
- 代码逻辑易于理解（类同步写法）
