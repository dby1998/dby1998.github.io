---
layout: post
title: "Vue-cli-axios"
date: 2020-05-19 
description: "HEXO配置，HEXO+Github，搭建自己的博客"

tag: 博客 
---   
# 1.Vue-cli

## 1. 什么是Vue CLI

> 1. 如果你只是简单写几个Vue的Demo程序, 那么你不需要Vue CLI.
>
> 2. 如果你在开发大型项目, 那么你需要, 并且必然需要使用Vue CLI
>    1. 使用Vue.js开发大型应用时，我们需要考虑代码目录结构、项目结构和部署、热加载、代码单元测试等事情。
>    2. 如果每个项目都要手动完成这些工作，那无疑效率比较低效，所以通常我们会使用一些脚手架工具来帮助完成这些事情。
> 3. 那究竟什么是Vue-CLI呢？
>    1. CLI（Command Line Interface）.翻译为命令行界面，就是我们所说的脚手架。
>    2. Vue CLI是一个官方发布的vue项目脚手架
>    3. 使用vue-cli可以快速搭建Vue环境和webpack配置



## 2. Vue CLI使用准备

### Node版本

> Vue CLI 需要Node.js 8.9 或者更高版本（推荐使用 8.11.0+）。你可以使用`nvm` 或 `nvm-window`来管理电脑上面的Node版本。



**安装Vue CLI脚手架的包：**

```js
// 全局安装npm
npm install -g @vue/cli 
# OR
yarn global add @vue/cli
```

安装之后，你就可以在命令行中访问 `vue` 命令。你可以通过简单运行 `vue`，看看是否展示出了一份所有可用命令的帮助信息，来验证它是否安装成功。

你还可以用这个命令来检查其版本是否正确 ：

```bash
vue --version
```



如果安装比较慢，可以把npm切换成淘宝的源：

```
npm config set registry https://registry.npm.taobao.org/
```



## 3. 创建项目

### 初始化项目

**vue create**

运行以下命令来创建一个新项目：

```js
vue create hello-world
```



你会被提示选取一个 preset。你可以选默认的包含了基本的 Babel + ESLint 设置的 preset，也可以选“手动选
择特性”来选取需要的特性。

选择 Manually select features

![](img/cli-new-project.png)

这个默认的设置非常适合快速创建一个新项目的原型，而手动设置则提供了更多的选项，它们是面向生产的项目更加需要的。

![CLI é¢è§](img/cli-select-features.png)

![](./img/20200327143328.png)

如果你决定手动选择特性，在操作提示的最后你可以选择将已选项保存为一个将来可复用的 preset

rd hellow word  //进入安装好的cli脚手架文件
npm run serve  //运行cli 项目

> ~/.vuerc
>
> 被保存的 preset 将会存在用户的 home 目录下一个名为 `.vuerc` 的 JSON 文件里。如果你想要修改被保存的 preset / 选项，可以编辑这个文件。
>
> 在项目创建的过程中，你也会被提示选择喜欢的包管理器或使用[淘宝 npm 镜像源](https://npm.taobao.org/)以更快地安装依赖。这些选择也将会存入 `~/.vuerc`。



### 使用图形化界面

你也可以通过 `vue ui` 命令以图形化界面创建和管理项目：

```bash
vue ui
```

上述命令会打开一个浏览器窗口，并以图形化界面将你引导至项目创建的流程。

![图形化界面预览](img/ui-new-project.png)



### 项目结构

node_modules: 项目依赖模块(第三方库)
package.json : 整个项目的配置文件
src: 开发代码的地方
     ----main.js: 整个项目的入口文件(webpack)
	

**项目目录**

![1569235847530](img/1569235847530.png)



```js
node_modules
public // 静态资源文件
    |-favicon.ico
    |-index.html
src // 项目源代码，书写代码的地方
    |-assets
    |-App.vue
    |-main.js
.browserslistrc    // 浏览器相关支持情况
.eslintrc.js       // 代码相关支持情况
.gitignore         // Git忽略文件
babel.config.js    // babel配置ES语法 转换
package-lock.json  // npm安装依赖库的具体信息
package.json       // npm依赖库版本信息
postcss.config.js  // css相关转换
README.md          // 项目说明
vue.config.js      // Vue及webpack配置项
```

cli 注释和一些格式报错  将LintOnSave: false 写入到配置中  或者在构建项目的时候将Linter取消  Linter相当于严格模式

![](./img/20200327193813.png)

### vue.config.js

`vue.config.js` 是一个可选的配置文件，如果项目的 (和 `package.json` 同级的) 根目录中存在这个文件，那么它会被 `@vue/cli-service` 自动加载。你也可以使用 `package.json` 中的 `vue` 字段，但是注意这种写法需要你严格遵照 JSON 的格式来写。

这个文件应该导出一个包含了选项的对象：

```js
// vue.config.js
 
  // 选项...
}
```



**webpack中添加别名**

```js
module.exports = {
    //1.基础的配置方式 
    configureWebpack: {
      resolve: {
        alias: {
          'components': '@/components',
          'pages': '@/pages'
        }
      }
    },

    //2.利用webpack4的webpack-chain来配置 
    chainWebpack: (config) => {
      config.resolve.alias
        .set('@', resolve('src'))
        .set('components', resolve('src/components'))
    }
  }
```

# 2.mixin

> 混入 (mixin) 提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。一个混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被“混合”进入该组件本身的选项。

## 1. 全局混入

```js
// main.js
Vue.mixin({
    created() {
        console.log('全局created')；
    }
})
```

**注意：**

请谨慎使用全局混入，因为它会影响每个单独创建的 Vue 实例 (包括第三方组件)。大多数情况下，只应当应用于自定义选项，就像上面示例一样。推荐将其作为插件发布，以避免重复应用混入。



## 2. 选项合并

**src/mixin/test.js**

```js
export default {
  created() {
    console.log('123')
  },
  methods: {
    jumpDetail() {
      
    }
  }
}
```

**src/views/Home.vue**

```js
<template>
  <div>我的
    <div @click="jumpDetail">商品详情：123</div>
  </div>
  
</template>

<script>
import testMixin from "@/mixins/test.js";
export default {
  mixins: [testMixin],
  methods: {
    jumpDetail() {
      //
    }
  },
  created() {
    console.log('---------------')
  }
}
</script>

<style>

</style>
```

**注意：**

值为对象的选项，例如 `methods`、`components` 和 `directives`，将被合并为同一个对象。两个对象键名冲突时，取组件对象的键值对。



# 3. vue.config.js

## 1. 修改项目端口

> 脚手架启动默认端口是8080，如果需要修改那就通过`vue.config.js`来修改我们的项目

```js
// vue.config.js
module.exports = {
    devServer: {
        port: 5353 // 指定项目监听的端口
    }
}
```



## 2. 修改部署应用包时的基本 URL

> 默认情况下，Vue CLI 会假设你的应用是被部署在一个域名的根路径上，例如 `https://www.my-app.com/`。如果应用被部署在一个子路径上，你就需要用这个选项指定这个子路径。例如，如果你的应用被部署在 `https://www.my-app.com/my-app/`，则设置 `publicPath` 为 `/my-app/`

```js
module.exports = {
  publicPath: process.env.NODE_ENV === 'production'
    ? '/my-app/'
    : '/'
}
```



## 3. 代理API

> 如果你的前端应用和后端 API 服务器没有运行在同一个主机上，你需要在开发环境下将 API 请求代理到 API 服务器。这个问题可以通过 `vue.config.js` 中的 `devServer.proxy` 选项来配置。

```js
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'http://www.xxx.com'
      },
      '/foo': {
        target: 'http://localhost:8081'
      }
    }
  }
}
```



# 4. 网络请求

## 安装

```
npm i axios -S
```

格式

```
import axios from 'axios'
axios.post('http://kumanxuan1.f3322.net:8084/tokens').then(res => {

})
```

解决跨域问题

​			跨域报错

![](./img/20200406130038.png)

![](./img/20200406125904.png)

```
// vue.config.js 配置文件
module.exports = {
  devServer: {
      port: 8888, // 指定项目监听的端口
      proxy: {
      // 代理规则
          '/tokens': {
              // 目标地址
              target: 'http://kumanxuan1.f3322.net:8084'  
          }
      },
  },
}

// 组件内
import axios from 'axios'
axios.post('/tokens').then(res => {

})
```

请求参数类型为 : X-WWW-FORM-URLENCODED

>username , password  根据接口文档填写
>
>

```
import qs from 'qs'
axios.post('/tokens',qs.stringify({
   username: this.ruleForm2.username,  
   password: this.ruleForm2.password
  })).then(res => {

})
```



## 1. axios

> Vue中发送网络请求，为什么选择axios呢？

![1570419641088](D:/Desktop/Vue/img/1570419641088.png)



## 2. 请求方式

> 支持多种请求方式：
>
> - axios(config)
> - axios.request(config)
> - axios.get(url[, config])
> - axios.delete(url[, config])
> - axios.head(url[, config])
> - axios.post(url[, data[, config]])
> - axios.put(url[, data[, config]])
> - axios.patch(url[, data[, config]])



## 3. 封装网络请求

![1570421730327](D:/Desktop/Vue/img/1570421730327.png)

> `api.js`放具体的请求的文件，而`request.js`封装axios请求（请求前拦截、返回结果后拦截）



**request.js**

```js
import axios from 'axios'

// 调用create方法创建实例
const instance = axios.create({
  timeout: 5000
})

// 请求前拦截
instance.interceptors.request.use(config => {
   return config
}, err => {
  return Promise.reject(err)
})

// 返回结果拦截
instance.interceptors.response.use(result => {
  return result
}, err => {
  return Promise.reject(err)
})

export default instance
```



**api.js**

```js
import request from './request'

export const getTopics = (params) => request.get('/api/v1/topics', {params:params})
```



**request/api.js**

```
import axios from 'axios'
import qs from 'qs' // from-data格式

export const getLogin = (data) => axios.post('/api/tokens', qs.stringify(data))

export const getDepartment = (data) => axios.get("/api/departments", {params: data});
```

**vue.config.js**

```
// 出现多个代理封装
"^/api": {
        // 目标地址
        target: "http://kumanxuan1.f3322.net:8084",
        pathRewrite: {
            '/api': '' // 最后将/api替换成空  相当于将/api删除掉
        }
      },
```




**src/views/Home.vue**

```vue
<template>
  <div>我的
    <div @click="jumpDetail">商品详情：123</div>
  </div>
  
</template>

<script>
// 1.引入api中需要用到的请求
import { getTopics } from "@/request/api";

export default {
  methods: {
    jumpDetail() {
      
    }
  },
  created() {
    // 2.调用请求
    getTopics({
      page: 1,
      tab: 'job',
      limit: 10
    }).then(res => {
		if (res.data.success) {
          console.log(res);
        }
    })
  }
}
</script>

<style>

</style>
```

## 4. 出现跨域情况

>1.因为浏览器里面同源策略
>
>2.只要是协议，域名，端口（三个其中一个不一样就会出现跨域）,
>*发送的请求和当前的服务比较（[https://36kr.com](https://36kr.com/)和[http://localhost](http://localhost/):8002/）
>
>3.协议（https）域名（36kr.com）端口（https的默认端口443http的默认端口是80）
>
>4.为什么cnodejs的请求没有出现跨域，是因为服务器设置允许跨域，所以不会出现跨域情况，
>*但是36kr这个没有设置，所以才会出现跨域
>
>5.vue-cli项目《开发环境》中解决跨域问题，通过vue.config.js上面的代理来解决（通过代理发送这个请求出去）

vue.config.js

```javascript
module.exports = {
    devServer: {
        port: 8888, // 指定项目监听的端口
        proxy: {
        // 代理规则
            '^/pp': {
                // 目标地址
                target: 'https://36kr.com'  
            }
        },
    },
    publicPath: process.env.NODE_ENV === 'production' ? './' : '/',
}
```

git请求

```
axios.get('地址',{params:{
	
}}).then(res => {
	
})
```

post请求

```
axios.post('地址',{}).then(res => {

})
```









