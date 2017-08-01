### AJAX 是与服务器交换数据并更新部分网页的艺术，在不重新加载整个页面的情况下。

####  请求  请求头和请求体 请求头是客户端的信息


####  Async = true
当使用 async=true 时，请规定在响应处于 onreadystatechange 事件中的就绪状态时执行的函数：
xmlhttp.onreadystatechange=function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  }
xmlhttp.open("GET","test1.txt",true);
xmlhttp.send();




#### GET 和POST


post 是往后台传数据

```
<script>
var xml=new XMLHttpRequest()
xml.onreadystatechange=function(){
  if (xml.readyState==4 && xml.status==200){
    console.log(JSON.parse(xml.responseText))
    // box.innerHTML=JSON.parse(xml.responseText).login
  }
}
console.log(xml)
xml.open('POST','https://cnodejs.org/api/v1/accesstoken',true)
xml.setRequestHeader("Content-type","application/json")
let data={
  accesstoken:"3f77acb1-d753-4393-b784-44913190e6a8"
}
xml.send(JSON.stringify(data))
</script>

```


设置请求头 数据类型换成json



## jq AJAX   
* get 请求
```
<script>
  $.ajax({
    url:'https://cnodejs.org/api/v1/topics',
    success: function(data){
      console.log(data)
    },
    error: function(){
      console.log('我是上边的错误')
    }
  }).done(function(data){
      console.log(data)
  }).fail(function(){
      console.log('我是下边的错误')
  }).always(function(){
      console.log('请求完毕')
  })
  console.log($.ajax)
</script>

```
* post   
```
<script>
  $.ajax({
    method:'post',
    dataType:'json',//期望后台返回的数据类型
    contentType:'application/json',//发往后台的数据类型
    url:'https://cnodejs.org/api/v1/accesstoken',
    data:JSON.stringify({accesstoken:'3f77acb1-d753-4393-b784-44913190e6a8'}),

    success: function(data){
      console.log(data)
    },
    error: function(){
      console.log('我是上边的错误')
    }
  }).done(function(data){
      console.log(data)
  }).fail(function(){
      console.log('我是下边的错误')
  }).always(function(){
      console.log('请求完毕')
  })
  console.log($.ajax)
</script>

```

##  跨域请求
豆瓣的api
免费的api

Access-Control-Allow-Origin:*
连接控制允许源
协议,域名,端口,都相同就是同源
一般都是后台解决
jq的
jsonp
```
method:'post',
dataType:'jsonp',//期望后台返回的数据类型
jsonp:'callback',
contentType:'application/json',//发往后台的数据类型
url:'https://api.douban.com/v2/book/1220562',
data:JSON.stringify({accesstoken:'3f77acb1-d753-4393-b784-44913190e6a8'}),

success: function(data){
  console.log(data)
},
error: function(){
  console.log('我是上边的错误')
}
}).done(function(data){
  console.log(data)
}).fail(function(){
  console.log('我是下边的错误')
}).always(function(){
  console.log('请求完毕')
})
console.log($.ajax)

```
##  es6的 fetch 的 get 请求
 ```
 fetch('https://api.github.com/users/newming')
   .then(function(response){
     return response.json()
   }).then(function(json){
     console.log(json)
   })

 ```
 post请求
 ```
 为了执行POST提交，我们可以将method属性值设置为post，并且在body属性值中设置需要提交的数据。

fetch(url,{
    method:"post",
    headers:{
        "Content-type":"application:/x-www-form-urlencoded:charset=UTF-8"
    },
    body:"name=lulingniu&age=40"
})
.then(status)
.then(json)
.then(function(data){
    console.log("请求成功，JSON解析后的响应数据为:",data);
})
.catch(function(err){
    console.log("Fetch错误:"+err);
});

 ```
.catch是失败的结果
.then是成功的结果

## 用 axios 发ajax请求
```
从github 直接搜axios
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script>
  axios.get('https://api.github.com/users/newming')
  .then((res)=>console.log(res.data))
</script>

```
