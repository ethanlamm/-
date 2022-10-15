### axios的封装(项目封装使用)

##### 安装：

```js
npm install axios
```

##### 步骤：

`request.js`

```js
import axios from 'axios'
import store from '@/store'
import router from '@/router'

const instance=axios.create({
	baseURL,
	timeout:5000
})

// 请求拦截
instance.interceptors.request.use(
	config=>{
		// 拦截业务：token
		return config
	},
	error=>{
		return Promise.reject(error)
	}
)

// 响应拦截
instance.interceptors.response.use(
	res=>{
		// 判断响应状态码进行处理
		if(res.code!==200){
			// 响应失败
			// ....
			return Promise.reject(new Error(res.message) || 'Error')
		}else{
            // 响应成功，对返回的数据进行处理
            return res.data
        }
	},
	error=>{
        // 401(未授权，要求身份验证)
        if(error.response && error.response===401){
            // 1.清空用户无效信息
        	// 2.跳转至登录页
        	// 3.重定向
            store.commit('user/setUser', {})
            const fullPath = encodeURIComponent(router.currentRoute.value.fullPath)
            outer.push('/login?redirectUrl=' + fullPath)
        }
        return Promise.reject(error)
    }
)

/**
 * 请求工具函数
 * @params {String} url 		请求路径
 * @params {String} method 		请求方式
 * @params {参考文档} submitData  请求参数
 */
export default (url,method,submitData)=>{
    return instance({
        url,
        method,
        [method.toLowerCase() === 'get' ? 'params' : 'data']: submitData
    })
}
```



`api/moduleA.js`

```js
import request from 'request.js'

// 定义一个请求接口
export const getCartList = () => {
  return request('/member/cart', 'get')
}
.....
```

##### 使用

`Demo.vue`

```js
import { getCartList } from '@/api/moduleA.js'

setup(){
	const data=ref(null)
	data.value=getCartList()
	return { data }
}
```



##### 另，可统一挂载至vue原型上

`api/index.js`

```js
import * as moduleA from './moduleA.js'
import * as moduleB from './moduleB.js'
....

export default {
	moduleA, moduleB...
}
```

`main.js`

```js
import API from '@/api/index.js'

// vue2.x
new Vue({
  el: '#app',
  beforeCreate() {
      Vue.prototype.$api = API
  },
  render: h => h(App)
})
```



##### `request.js` 中，baseURL的情况

###### 1.直接写

```js
export const baseURL='http://example.com'
```

###### 2.代理

- 设置接口请求前缀：根据开发、测试、生产环境的不同，前缀需要加以区分

`main.js`

```js
if (process.env.NODE_ENV === 'development') {
  axios.defaults.baseURL = 'http://dev.xxx.com'
} else if (process.env.NODE_ENV === 'production') {
  axios.defaults.baseURL = 'http://prod.xxx.com'
}
```

- `vue.config.js` ：配置 `devServer` 实现代理转发

```js
devServer: {
    proxy: {
        // '/proxyApi'是代理标识，用于告诉node，url前面是/proxyApi的就是使用代理的
      '/proxyApi': {
        target: 'http://dev.xxx.com', //目标地址，一般是指后台服务器地址
        changeOrigin: true, //是否跨域
        // pathRewrite 的作用是把实际Request Url中的'/proxyApi'用 "" 代替
        pathRewrite: {
          '/proxyApi': ''
        }
      }
    },
    open:true	// vue项目启动时自动打开浏览器
  }
```



##### # axios的配置选项

```js
const service=axios.create({
    baseURL:String,
    timeout:Number(毫秒数)
})

service({
    url:String,
    method:String,
    // 当method为get时--params
    params:[Object,URLSearchParams],
    // 当method为post、put、delete、patch时--data
    data:[String,Object,ArrayBuffer,URLSearchParams],
})
```

##### # axios支持Promise API

##### # axios的取消请求

```js
const controller = new AbortController();

axios.get('/foo/bar', {
   signal: controller.signal
}).then(function(response) {
   //...
});
// 取消请求
controller.abort()
```



axios封装，回答

1.设置请求前缀：根据开发、测试、生产环境(`process.env.NODE_ENV`)的不同，前缀(`axios.defaults.baseURL`)需要加以区分

2.设置超时事件：`timeout`

3.设置请求拦截和响应拦截

4.封装请求方法(默认暴露)
