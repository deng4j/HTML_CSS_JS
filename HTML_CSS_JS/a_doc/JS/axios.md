- 基于promise用于浏览器和node.js的http客户端
- 支持浏览器和node.js
- 支持promise
- 能拦截请求和响应
- 自动转换JSON数据
- 能转换请求和响应数据

```js
axios.get('http://localhost:3000/adata').then(function(ret){ 
  #  拿到 ret 是一个对象，所有的对象都存在 ret 的data 属性里面
  // 注意data属性是固定的用法，用于获取后台的实际数据
  // console.log(ret.data)
  console.log(ret)
  })
```

```js
// 通过params形式传递参数 
axios.get('http://localhost:3000/axios', {
      params: {
        id: 789
      }
    }).then(function(ret){
      console.log(ret.data)
    })
```

```js
// axios delete 请求传参，传参的形式和 get 请求一样
axios.delete('http://localhost:3000/axios', {
  params: {
    id: 111
  }
}).then(function(ret){
  console.log(ret.data)
})
```

```js
// axios 的 post 请求
// 通过选项传递参数
axios.post('http://localhost:3000/axios', {
  uname: 'lisi',
  pwd: 123
}).then(function(ret){
  console.log(ret.data)
})

// 通过 URLSearchParams传递参数
var params = new URLSearchParams();
params.append('uname', 'zhangsan');
params.append('pwd', '111');
axios.post('http://localhost:3000/axios', params).then(function(ret){
  console.log(ret.data)
})
```

```js
// axios put 请求传参和post请求一样 
axios.put('http://localhost:3000/axios/123', {
  uname: 'lisi',
  pwd: 123
}).then(function(ret){
  console.log(ret.data)
})
```

------

**axios同步请求**

```js
async getFunc(){
  const { data: res } = await axios.get('http://localhost:3000/getData')
  console.log(res)
}
```

------

**axios 全局配置**

```js
#  配置公共的请求头 
axios.defaults.baseURL = 'https://api.example.com';
#  配置 超时时间
axios.defaults.timeout = 2500;
#  配置公共的请求头
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
# 配置公共的 post 的 Content-Type
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```

**axios 拦截器**

- 请求拦截器：作用是在请求发送前进行一些操作；例如在每个请求体里加上token，统一做了处理如果以后要改也非常容易
- 响应拦截器：作用是在接收到响应后进行一些操作；例如在服务器返回登录状态失效，需要重新登录的时候，跳转到登录页

```js
# 1. 请求拦截器 
axios.interceptors.request.use(function(config) {
  console.log(config.url)
  # 1.1  任何请求都会经过这一步   在发送请求之前做些什么   
  config.headers.mytoken = 'nihao';
  # 1.2  这里一定要return   否则配置不成功  
  return config;
}, function(err){
  #1.3 对请求错误做点什么    
  console.log(err)
})
```

```js
#2. 响应拦截器 
axios.interceptors.response.use(function(res) {
  #2.1  在接收响应做些什么  
  var data = res.data;
  return data;
}, function(err){
  #2.2 对响应错误做点什么  
  console.log(err)
})
```

# 