一、Router

vue2.0

`router/index.js`

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import routes from './routes'	// 路由表

Vue.use(VueRouter)

const router = new VueRouter({
    mode:'history',		// 默认是hash模式
    routes,
    scrollBehavior(to, from, savedPosition) {
        return { y: 0 }
    }
})
export default router
```

history模式需要后台配置支持：[HTML5 History 模式](https://v3.router.vuejs.org/zh/guide/essentials/history-mode.html#后端配置例子)

`main.js`

```js
import router from '@/router'

new Vue({
  render: h => h(App),
  // 注册路由，则组件上有$router和$route
  router
}).$mount('#app')
```



vue3.0

`router/index.js`

```js
import { createRouter, createWebHashHistory } from 'vue-router'
import routes from './routes'	// 路由表

const router = createRouter({
  // 使用hash模式
  history: createWebHashHistory(process.env.BASE_URL),
  // history: createWebHistory(process.env.BASE_URL)
  routes,
  scrollBehavior () {
    return { left: 0, top: 0 }
  }
})

export default router
```

history模式需要后台配置支持：[History模式](https://router.vuejs.org/zh/guide/essentials/history-mode.html#服务器配置示例)

`main.js`

```js
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

createApp(App).use(router).mount('#app')
```



---

二、Store

vue2.0

`store/index.js`

```js
import Vue from "vue";
import Vuex from 'vuex'

// 引入小仓库
import homeOptions from "./home";
import searchOptions from "./search";
import detailOptions from "./detail";

Vue.use(Vuex)

export default new Vuex.Store({
    // 模块化
    modules: {
        homeOptions, 
        searchOptions, 
        detailOptions,
        ...
    }
})
```

`store/home/index.js`

```js
export default {
    namespaced:true,
    state:{},
    getters:{},
    mutations:{},
    actions:{}
}
```

`main.js`

```js
import store from '@/store'

new Vue({
  render: h => h(App),
  // 注册vuex，则组件上有$store
  store,
}).$mount('#app')
```



vue3.0

`store/index.js`

```js
import { createStore } from 'vuex'

// 引入其他仓库
import cart from './modules/cart'
import category from './modules/category'
import user from './modules/user'

export default createStore({
  modules: {
    cart, category, user
  }
})
```

`modules/cart.js`

```js
export default {
    namespaced:true,
    state:{},
    getters:{},
    mutations:{},
    actions:{}
}
```

`main.js`

```js
import { createApp } from 'vue'
import App from './App.vue'
import store from './store'

createApp(App).use(store).mount('#app')
```

