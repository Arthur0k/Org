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
### Object

#### Object.setPrototypeOf() and Object.getPrototypeOf()
```javascript
a = {}
a.__proto__ === Object.getPrototypeOf(a)  // true
```

`Object.getPrototypeof()`  ---  获取对象的prototype属性
`Object.setPrototypeof()`  ---  设置对象的prototype属性

---
#### Object.assign()
`Object.assign(target, source, source2, ...)`  --  将source的属性添加到target中，如果target中有相同的属性则会覆盖，且此方法是浅拷贝

---
#### Object.is()
`Object.is(a, b)`判断两个对象是否相等（`===`），返回布尔值,
其中与`===`不同的是:
```javascript
+0 === -0    // true
NaN === NaN //false
Object.is(+0, -0)    // false
Object.is(NaN, NaN) // true
```
---

#### 遍历
- Object.keys()
- Object.values()
- Object.entries()
```javascript
let obj = {a: 1, b: 2, c: 3}
Object.keys(obj)  // [a, b, c]
Object.values(obj)  // [1, 2, 3]
Object.entries(obj)  // [['a', 1], ['b', 2], ['c', 3]]
```
- for ... in ...  // 遍历可枚举的属性包括继承的属性 (exclude Symbol)
- Object.getOwnPropertyNames  //遍历自己的属性 (exclude Symbol)
- Object.getOwnPropertySymbols //遍历自身的所有Symbol属性
- Reflect.ownKeys // 自身的所有属性 不管`enumberable: true | false`

---

#### 解构赋值 and 扩展运算符
>解构赋值必须是最后一个参数
>扩展运算符等同Object.assign()方法
```javascript
const {x, y, ...z} = {x: 1, y: 2, d: 4, b: 5}
x // 1
y // 2
z // {d: 4, b: 5}

let a = {x: 1, y: 2, z: 3, d: 'foo'}
let c = {...a}
//等同于
let c = Object.assign({}, a)

let example = {ball: 'basketball', name: 'arthur'}
let example2 = {age: 15, hobby: 'computer'}
let target = {...example, ...example2}
//等同于
let target = Object.assign(example, example2)
```


## 跨域请求问题

解决方法：

1. 如果浏览器支持HTML5，那么就可以一劳永逸地使用新的跨域策略：CORS了。

  Access-Control-Allow-Origin其中Origin代表本域,因为浏览器同源策略的原因，对于域不同的访问是禁止的
  如果在服务器响应头中添加`Access-Control-Allow-Origin`为`*(或自己网站的ip)`,express框架中可添加如下代码

  ```javascript
app.all('*', function(req, res, next) {
  res.header("Access-Control-Allow-Origin", "*");
  res.header("Access-Control-Allow-Headers", "X-Requested-With");
  res.header("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");
  res.header("X-Powered-By",' 3.2.1');
  res.header("Content-Type", "application/json;charset=utf-8");
  next();
});
  ```
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
