

## tips

### RESTful API设计中如何实现批量操作

https://segmentfault.com/q/1010000001616176

https://www.npmjs.org/package/restful-api

```
POST /posts/batch
     Body: { 'delete': [1, 2, 3, 4, 5, 10, 42, 68, 99] }
```

http://backbonejs.org/#FAQ-tim-toady

```json
  {
    "create":  [array of models to create]
    "update":  [array of models to update]
    "destroy": [array of model ids to destroy]
  }
```

https://segmentfault.com/q/1010000004407452

有一些框架是允许delete伴随body发送的，这样你可以把所有的IDs一次放进去然后发送DELETE 请求。 另外一种写法是分成2步完成，第一步发送POST请求，集合所有要删除的IDs然后返回一个header,然后在利用这个header调用DELETE请求。具体步骤如下:

```
发送POST请求，集中所有的IDs (可以存到Redis或者普通数据库)
http://example.com/posts/deletes

成功后可以返回一个唯一的头文件：

HTTP/1.1 201 created, and a Location header to:
http://example.com/posts/deletes/KJHJS675

然后可以利用Ajax直接发送DELETE请求:
DELETE http://example.com/posts/deletes/KJHJS675

这样就可以在不暴露IDs的情况下更加安全的删除相关条目。
```

个人倾向`DELETE` id数组。

其他讨论：

https://www.v2ex.com/t/154258

