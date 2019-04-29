# Happy hack Vue

## Router

### 创建路由实例


npm install --save-dev vue vue-router
```javascript
import Vue from 'vue';
import VueRouter from 'vue-router'

const router = new VueRouter({
    routes: [
        {path: '/', component: xx}
   ]
})
```
### 动态路径参数
某种模式匹配到的所有路由,全都映射到相同的组件上 假如这个组件是user,
所有以/user/为开头id各不相同的路由都会渲染相同的组件user,例如/user/123,
/user/2342ns, /usr/bin34等
```javascript
const router = new VueRouter({
    routes: [
        {path: '/user/:id', component: user}
    ]
})
```
路径参数是由`:`设置，所有的路径c参数默认被设置到`this.$route.params`中，
