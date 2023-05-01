#

## 一、切换 node 环境

`nvm use node`

## 二、创建项目

`npm init vite saas`

## 三、安装 router

2.1 执行命令

`pnpm install vue-router@4 -S`

2.2 进入项目，创建 router 目录，再去创建 index.js

`mkdir src/router && touch src/router/index.js`

2.3 配置 src/router/index.js 文件内容

```js
import { createRouter, createWebHistory } from "vue-router";
import Home from "../views/Home.vue";

const routes = [
  {
    path: "/",
    name: "Home",
    component: Home,
  },
  {
    path: "/about",
    name: "About",
    component: () =>
      import(/* webpackChunkName: "about" */ "../views/About.vue"),
  },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});

export default router;
```

2.4 在 src 目录新建 views/Home.vue 和 About.vue

`mkdir src/views && touch src/views/Home.vue && touch src/views/About.vue`

Home.vue 和 About.vue 随便写入点内容即可

2.5 App.vue 文件内容修改

```js
// 改成
<template>
  <router-view />
</template>
```

2.6 main.js 挂载使用 router

```js
import { createApp } from "vue";
// import "./style.css";
import App from "./App.vue";
import router from "./router";

createApp(App).use(router).mount("#app");
```

## 四、unplugin-auto-import 插件

4.1 下载安装

`pnpm i unplugin-auto-import -D`

4.2 在 vite.config.js 中进行配置

```js
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";
//引入插件
import AutoImport from "unplugin-auto-import/vite";
import path from "path";

export default defineConfig({
  plugins: [
    vue(),
    //配置插件
    AutoImport({
      imports: ["vue", "vue-router"],
    }),
  ],
  resolve: {
    // 配置路径别名
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
});
```

## 五、element-plus

5.1 下载安装

```shell
pnpm install element-plus --save

pnpm install @element-plus/icons-vue  # 使用icon需要单独h安装
```

5.2 按需引入某 ui 组件

- 安装插件

`pnpm install -D unplugin-vue-components unplugin-auto-import`

- 配置 vite.config.ts

```js
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";
//引入插件
import AutoImport from "unplugin-auto-import/vite";
import path from "path";
import Components from "unplugin-vue-components/vite";
import { ElementPlusResolver } from "unplugin-vue-components/resolvers";

export default defineConfig({
  plugins: [
    vue(),
    //配置插件
    AutoImport({
      imports: ["vue", "vue-router"],
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
  resolve: {
    // 配置路径别名
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
});
```

## 六、resetcss

6.1 在 src/assets 目录新建 css/reset.css

`mkdir src/assets/css && touch src/assets/css/reset.css`

6.2 官网地址：[reset.css](https://meyerweb.com/eric/tools/css/reset/)

6.3 配置 reset.css

```css
/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html,
body,
div,
span,
applet,
object,
iframe,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
pre,
a,
abbr,
acronym,
address,
big,
cite,
code,
del,
dfn,
em,
img,
ins,
kbd,
q,
s,
samp,
small,
strike,
strong,
sub,
sup,
tt,
var,
b,
u,
i,
center,
dl,
dt,
dd,
ol,
ul,
li,
fieldset,
form,
label,
legend,
table,
caption,
tbody,
tfoot,
thead,
tr,
th,
td,
article,
aside,
canvas,
details,
embed,
figure,
figcaption,
footer,
header,
hgroup,
menu,
nav,
output,
ruby,
section,
summary,
time,
mark,
audio,
video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  display: block;
}
body {
  line-height: 1;
}
ol,
ul {
  list-style: none;
}
blockquote,
q {
  quotes: none;
}
blockquote:before,
blockquote:after,
q:before,
q:after {
  content: "";
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
```

6.4 main.js 中引入

```js
import { createApp } from "vue";
// import "./style.css";
import "./assets/css/reset.css";
import App from "./App.vue";
import router from "./router";

createApp(App).use(router).mount("#app");
```
