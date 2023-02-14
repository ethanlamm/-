##### 一、XMLHttpRequest（XHR）

浏览器提供XMLHttpRequest 对象，用于与服务器进行交互数据

通过 `XMLHttpRequest` 可以在不刷新页面的情况下请求特定 URL，获取数据。这允许网页在不影响用户操作的情况下，更新页面的局部内容。

**传统Ajax（原生JS的Ajax）——基于XHR**

1.通过`new`关键字创建XHR异步对象

2.设置回调函数

3.使用`XHR.open`方法与服务器建立连接

4.使用`XHR.send`方法向服务器发送数据

5.通过`XHR.onreadystatechange`事件监听通信状态

```js
const xhr = new XMLHttpRequest()

xhr.onreadystatechange = function(){
    if(xhr.readyState === 4){ // 整个请求过程完毕
        if(xhr.status >= 200 && xhr.status <= 300){
            console.log(xhr.responseText) // 服务端返回的结果
        }else if(xhr.status >=400){
            console.log("错误信息：" + xhr.status)
        }
    }
}

xhr.open(method, url, [async][, user][, password])
/*
参数说明：
method：表示当前的请求方式，常见的有GET、POST
url：服务端地址
async：布尔值，表示是否异步执行操作，默认为true
user: 可选的用户名用于认证用途；默认为 null
password: 可选的密码用于认证用途，默认为 null
*/

xhr.send([body])
/*
body: 在 XHR 请求中要发送的数据体，如果不传递数据则为 null
如果使用GET请求发送数据的时候，需要注意如下：
	将请求数据添加到open()方法中的url地址中
	发送请求数据中的send()方法中参数设置为null
*/
```



##### 二、jQuery中的Ajax

指的是 jquery 对 XHR 的封装，XHR 是 ajax 功能实现所依赖的对象

- jquery已内部实现对XHR的封装==> $.ajax，使用如下

```js
const $ = require('jquery')

$.ajax({
    url:String
    [method|type]:String,
    data:[Object,String],
    datatype:[json,jsonp,script...],
    success:function (data) {},
    error:function (error) {}
})
```



- 手动封装（理解源代码）

```js
// 封装一个ajax请求
function ajax(options){
    // 处理请求参数的函数
     function formsParams(data){
        var arr = [];
        for(var prop in data){
            arr.push(prop + "=" + data[prop]);
        }
        return arr.join("&");
    }
    
    //创建XMLHttpRequest对象
    const xhr = new XMLHttpRequest()
    
    //初始化参数的内容
    options = options || {}
    // 默认GET请求
    options.type = (options.type || 'GET').toUpperCase()
    // 默认json格式
    options.dataType = options.dataType || 'json'
    // 请求数据
    const params = options.data	// options.data 需要是一个对象
    
    //发送请求
    if (options.type === 'GET') {
        xhr.open('GET', options.url + '?' + formsParams(params), true)
        xhr.send(null)
    } else if (options.type === 'POST') {
        xhr.open('POST', options.url, true)
        xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded")
        xhr.send(params)
    
     //接收请求
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
            let status = xhr.status
            if (status >= 200 && status < 300) {
                options.success && options.success(xhr.responseText)
            } else {
                options.error && options.error(status)
            }
        }
    }
}
```

使用方式如下

```js
ajax({
    url : "https://xxxx",  // url---->地址
    type : "POST",   // type ---> 请求方式
    data : {        //传入信息
        name : "张三",
        age : 18
    },
    success : function(data){   //返回接受信息
        console.log(data);
    },
    error : function(error){
        // error...
    }
})
```



##### XHR、Ajax、Axios的区别

1）XHR：浏览器提供XMLHttpRequest 对象，用于与服务器进行交互数据

2）Ajax：Jquery对XHR的封装

3）Axios：基于 Promise，实现对Ajax的封装

Axios特点：

​	   1、在浏览器中创建 XMLHttpRequests

　　2、在node.js则创建http请求

　　3、支持Promise API

　　4、支持拦截请求和响应

　　5、转换请求和响应数据

　　6、取消请求

　　7、自动转换成JSON数据格式

　　8、客户端支持防御`XSRF`