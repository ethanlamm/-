Nuxt项目搭建

一、安装

```sh
npx nuxi init nuxt3-app
```

坑1：报错 could not fetch remote https://github.com/nuxt/starter

原因：网络问题，换淘宝镜像源。`nrm use tabao`

二、打开项目(vscode)

安装依赖：`npm install/cnpm install `

三、运行项目

`npm run dev`

四、使用[Naive UI](https://www.naiveui.com/zh-CN/light/docs/installation)

1）安装	`npm i -D naive-ui`

2）[服务端渲染需要额外配置](https://www.naiveui.com/zh-CN/light/docs/ssr)

1.安装 `naive-ui` 和 `@css-render/vue3-ssr`

2.在 `nuxt.config.ts` 增添下列配置

```tsx
export default defineNuxtConfig({
  build: {
    transpile:
      process.env.NODE_ENV === 'production'
        ? [
            'naive-ui',
            'vueuc',
            '@css-render/vue3-ssr',
            '@juggle/resize-observer'
          ]
        : ['@juggle/resize-observer']
  },
  vite: {
    optimizeDeps: {
      include:
        process.env.NODE_ENV === 'development'
          ? ['naive-ui', 'vueuc', 'date-fns-tz/esm/formatInTimeZone']
          : []
    }
  }
})
```

3.在 Nuxt 项目的 `plugins` 文件夹增加这个[插件](https://github.com/07akioni/naive-ui-nuxt-demo/blob/main/plugins/naive-ui.ts)

- 新增目录 `plugins`
- 在该目录下新建 `navie-ui.ts`
- 复制粘贴代码(不用管标红的代码，可运行)

3）Naive UI的使用

1.vscode安装插件 `Naive Ui Snippets`

2.[在 SFC 中使用 - Naive UI](https://www.naiveui.com/zh-CN/light/docs/usage-sfc)

```vue
<template>
  <div>
    <n-button type="primary" size="medium" @click="">按钮</n-button>
  </div>
</template>
<script setup>
import { NButton } from 'naive-ui'
</script>
```

五、使用[Windi CSS](https://windicss.org/guide/installation.html)

1）选择Nuxt

<img src="https://raw.githubusercontent.com/ethanlamm/notes/image/img/image-20220820173541774.png" alt="image-20220820173541774" style="zoom:50%;" />

2）安装	`npm i nuxt-windicss -D`

3）[配置](https://windicss.org/integrations/nuxt.html#usage)

```tsx
export default {
  buildModules: [
    'nuxt-windicss',
  ],
}
```

4）使用	vscode安装插件 `WindiCSS IntelliSense`