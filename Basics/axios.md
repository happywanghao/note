# axios

## 作用

一般认为是发ajax请求的（ajax是jquery）页面不刷新只是局部刷新，其实一句话总结就是来发http请求的
Axios 是一个基于 promise 的 HTTP 库，可以工作于浏览器中，也可以在 node.js 中使用，提供了一个API用来处理 XMLHttpRequests 和 node 的 http 接口

### 用 jquery 的 get/post 不就很好了，为什么要用 Axios？

（1）Axios 支持 node.js，jquery 不支持

（2）Axios 基于 promise 语法标准，jquery 在 3.0 版本中才全面支持
<!-- promise 用于做异步请求的一种方法-->

（3）Axios 是一个小巧而专业的 HTTP 库，jquery 是一个大而全的库，如果有些场景不需要使用jquery的其他功能，只需要HTTP相关功能，这时使用 Axios 会更适合

## 安装的3种方式

- 使用 npm

```
npm install axios --save
```


- 使用 bower

```
bower install axios
```


- 手动下载

```
https://github.com/mzabriskie/axios/tree/master/dist
```
## 使用


- node 中运行

```
var axios = require('axios')
axios.get('https://api.github.com/users/xxx');
```


- 浏览器中运行

```
<script src="./bower_components/axios/dist/axios.js"></script>
<script>
axios.get('https://api.github.com/xxx');
</script>
```
## 基本操作

- GET

```
axios.get('https://api.github.com/users/' + username)
  .then(function(response){
    console.log(response.data);
    console.log(response.status);
  });  
```

- POST

```
axios.post('/save', { firstName: 'Marlon', lastName: 'Bernardes' })
  .then(function(response){
    console.log('saved successfully');
  })
  .catch(function (error) {
    console.log(error);
  });
```

除了 get/post，还可以请求 delete,head,put,patch

### 同时执行多个请求

```
axios.all([
    axios.get('https://api.github.com/xxx/1'),
    axios.get('https://api.github.com/xxx/2')
  ])
  .then(axios.spread(function (userResp, reposResp) {
    // 上面两个请求都完成后，才执行这个回调方法
    console.log('User', userResp.data);
    console.log('Repositories', reposResp.data);
  }));

```
当所有的请求都完成后，会收到一个数组，包含着响应对象，其中的顺序和请求发送的顺序相同，可以使用 axios.spread 分割成多个单独的响应对象

#### 自定义 header

```
var config = {
  headers: {'X-My-Custom-Header': 'Header-Value'}
};

axios.get('https://api.github.com/users/xxx', config);
axios.post('/save', { firstName: 'Marlon' }, config);

```
#### 拦截器

可以在 then 或者 catch 之前对 requests/responses 进行拦截处理

- 添加

```
var myInterceptor = axios.interceptors.request.use(function () {/*...*/});

```
- 移除
```
axios.interceptors.request.eject(myInterceptor);
```
