# Javascript

## ES6

### String

- `String.codePointAt()`
- `String.fromCodePoint()`
- `String.at()`
- `String.padStart()`
- `String.padEnd()`
- `String.startsWith()`
- `String.endsWith()`
- `String.includes()`
- `String.repeat()`
- `String.raw()`
- `String.normalize()`

字符串的遍历接口

`for x of items`

### Array
## 跨域请求问题

解决方法：

1. 如果浏览器支持HTML5，那么就可以一劳永逸地使用新的跨域策略：CORS了。

  Access-Control-Allow-Origin其中Origin代表本域,因为浏览器同源策略的原因，对于域不同的访问是禁止的
  如果在服务器响应头中添加`Access-Control-Allow-Origin`为`*(或自己网站的ip)`
  就可以直接利用Ajax进行请求了
2. 利用JSONP，限制是只能发送GET请求，其原理是浏览器允许跨域引Javascript资源。
```html
<html>
  <head>
    <script src="http://example.com/abc.js"></script>
    ...
  </head>
<body>
...
</body>
</html>
```
   但方式需要前后端配合，约定一个接口 即:前端定义一个回调函数`callback`动态创建script发送请求，后端返回一个该回调函数调用的字符串`callback(data)`

3. 前端使用代理

小问题： 对网页中出现`ERR_UNKNOWN_URL_SCHEME`的解决方案是：添加协议`http://` or `https://`
