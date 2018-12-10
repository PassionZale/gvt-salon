目标
===

拟定缘由
-----------

此开发规范, 基于官网所推荐的风格指南, 结合本人过往的开发经验、技术栈整理所得, 旨在统一前端代码书写风格、一致性、易读性等.

补充说明
-------

大部分的规范, 会详细的描述**怎么做**, 少量的规范, 会解释 **为什么**, 带有 **为什么** 的规范, 你需要更加注意, 因为这可能是来自官网推荐, 也可能是来自本人的开发经验, 建议你一定遵守, 因为它们通常是最优解.

书写风格
=======

输入法设置
---------

虽然现在很多 idea 或 编辑器有了错误提示, 但是作为一个程序员, 个人觉得, 首先请将你的输入法进行如下设置:

- 默认英文输入法

- 中文情况下使用英文标点

- 任何情况都使用半角符

缩进与换行
---------

在任何情况下, 缩进为 2 个空格, 花括号收尾需换行, 如:

```javascript
export default {
  data() {
    return {}
  }
}
```

样式命名
-------

样式命名有许多规则, 此次我们统一使用 ```-``` 连接样式名称, 如:

```css
.gvt-header {}

.gvt-sidebar {}

.gvt-menu {}

.gvt-menu-item {}
```

引号的使用
---------

在任何情况下, 如: ```.html```、```.js```、```.css``` 文件中, 请使用 **双引号** 包裹字符串

```html
<!-- .html -->
<div id="app"></div>
```

```js
// .js
const company = "gvt";
export const project_name = `${company}-standard`;
```

```css
/* .css */
#app {
  color: "#000";
}
```

>为什么?

模板字符串使用反引号,如:`` 来代替普通字符串中的用双引号和单引号. 在一些编辑器中, 反引号与单引号可能看起来会是一样的, 如:'', 因此查阅代码时, 若双引号和单引号混用, 会带来迷惑性, 因此推荐统一使用双引号: "" 

目录结构
=======

项目结构 (SPA)
-------

```shell
gvt-frontend-spa/

    - build/                # 编译后代码存放目录, 服务端部署目录

    - static/               # 静态资源文件夹

        - libs/             # 存放第三方依赖库源码,如: vue、vue-router、vuex、axios ...

        - images/           # 图片等

    - src/

        - api/              # 全部的 API

        - components/       # 组件, 如一些公共的布局组件等等

        - directives/       # 指令

        - filters/          # 过滤器

        - routers/          # 路由

        - utils/            # 工具

        - views/            # 视图组件

        - vuex/             # 状态管理

        - App.vue           # 根组件
    
        - main.css          # 主样式表

        - main.js           # 主入口文件

    .npmrc                  # npm 配置项, 通常用于指定 npm local source

    .babelrc                # babel 配置项

    index.ejs               # 编译时所使用的模板

    index.html              # 开发时所使用的视图

    package.json            # pacakge.json

    webpack.config.js       # webpack config
```

项目结构 (MPA)
-------

```shell
gvt-frontend-mpa/

    - build/                # 编译后代码存放目录, 服务端部署目录

    - static/               # 静态资源文件夹

        - libs/             # 存放第三方依赖库源码,如: vue、vue-router、vuex、axios ...

        - images/           # 图片等

    - src/

        - api/              # 全部的 API

        - components/       # 组件, 如一些公共的布局组件等等

        - directives/       # 指令

        - filters/          # 过滤器

        - routers/          # 路由

        - utils/            # 工具

        - views/            # 视图组件

        - vuex/             # 状态管理

        - pages/            # 页面 (假设多页面应用分别为: admin.html、index.html)

            - admin/

                - App.vue

                - main.js

            - index/
                - App.vue

                - main.js
    
        - main.css          # 主样式表

    .npmrc                  # npm 配置项, 通常用于指定 npm local source

    .babelrc                # babel 配置项

    index.ejs               # 编译时所使用的模板

    admin.html              # admin Application HTML           

    index.html              # index Application HTML

    package.json            # pacakge.json

    webpack.config.js       # webpack config
```

说明
----

基于实际开发情况, 可能会增加额外配置, 如: webpack.config.js 可以依据项目的复杂程度拆分成多个 *.config.js 等等, 但 ```src/``` 模块拆分及目录层级结构不准更改, 各个子项目必须 **保持一致**.


在实际项目中, 无需考虑上述问题, 只需使用统一项目模板, 通过脚手架进行初始化即可.


这里列出上述 SPA & MPA 目录结构只是作为参考.

常量约定
=======

环境变量
-------

基于我司开发流程, 细化为三个环境:

环境变量  | 说明 
------      | ------
development | 用于本地开发 
production  | 用于提测发布
release     | 用于生产发布

由于当前子系统菜单使用 UMS 配置数据, 因此在项目初期, 你可以根据当前环境变量, 灵活的处理侧边栏菜单的数据源

```javascript
export default {
  mounted() {
    // 本地开发时使用 Mock Data
    // 提测和生成使用 Ums Data
    this.menuData = ENV === "development" ? this.mockMenuData() : this.umsMenuData();
  }
}
```

分页参数
-------

基于前端所使用 iview Page 组件, 分页参数常量数据结构定义为:

键名 | 类型 | 说明 
--- | --- | ---
current | Number | 当前页, 默认为 1
total | Number | 总页数, 默认为 0
pageSize | Number | 每页显示条数, 默认为 pageSizeOpts[0]
pageSizeOpts | Array | 每页显示条数选项, 用于切换每页条数, 默认 [10, 20, 30, 40, 50]

```json
{
  "current": 1,
  "total": 0,
  "pageSize": 10,
  "pageSizeOpts": [10, 20, 30, 40, 50]
}
```

在与服务端对接 API 时, 请务必通过 ```Object.assign()``` 扩展视图组件中的 ```pagination``` 模型, 并根据服务端 当前页, 每页显示条数 给定参数名, 及时调整键名, 例如:

```javascript
import PAGE_PARAMS from "~/utils/constants";

export default {
  data() {
    return {
      // ===
      // 参数赋值
      // 必须使用 Object.assign() 扩展 PAGE_PARAMS
      pagination: Object.assign({}, PAGE_PARAMS)
      // 不允许直接赋值 !!!
      // pagination: PAGE_PARAMS
    }
  },

  created() {
    // 假定, 服务端"当前页","每页显示条数" 参数名为:
    // pageNum, pageSize
    const params = Object.assign(
      {}, 
      this.form, 
      {
        pageNum: this.pagination.current,
        pageSize: this.pagination.pageSize
      }
    )
  }
}
```

状态码
-----

前端通过 API Response Data Code 自行判断当前客户端登录是否过期, 与 UMS 约定状态码为:

- "110002"
- "110003"
- "110004"
- "110103"

它们全部为字符串, 你可以在 axios 拦截器中查看该状态码是如何被使用的, 它通常在如下目录:

```shell
./src/utils/ajax.js
```

```javascript
ajax.interceptors.response.use(response => {
  const code = response.data.code
  if (code === "110002" || code === "110003" || code === "110103" || code === "110004") {
    // Oops! UMS 403 FORBIDDEN !
    // 哇哦! UMS 卒!
    GO_BACK_UMS();
    return;
  }
  return response.data;
}, error => {
  return Promise.reject(error);
})
```

组件编写
=======

基于模块开发
-----------

始终基于模块的方式来构建你的 app,每一个子模块只做一件事情.

每一个 Vue 组件必须z专注于解决一个单一的问题, 如果你的组件做了太多事情或是变的臃肿, 你应该将其进行拆分.

组件命名
-------

请做到如下要求:

- 有意义

- 简短

- 具有可读性

- 单词大写开头(PascalCase)


```shell
components/ 

  - MyComponent.vue

  - todos/

    - TodoList.vue

    - TodoListItem.vue

    - TodoListItemButton.vue

  - bases/

    - BaseButton.vue

    - BaseTable.vue

    - BaseIcon.vue
```

组件使用
-------

组件使用有许多中方式, 例如:

```html
<!-- 在单文件组件、字符串模板和 JSX 中 -->
<MyComponent/>
<!-- 在 DOM 模板中 -->
<my-component></my-component>
```

这里, 我们统一使用第二种: ```<my-component></my-component>```

将 this 赋值给 component 变量
----------------------------

在 Vue.js 组件上下文中, ```this``` 指向了组件实例. 因此当你切换到了不同的上下文时, 要确保 ```this``` 指向一个可用的 ```component``` 变量.

如果你正在使用 ES6 的话, 就不要再编写 ```var self = this;``` 这样的代码了!

>为什么?

- 使用 ES6, 就不再需要将 ```this``` 保存到一个变量中了

- 一般来说, 当你使用箭头函数时, 会保留 ```this``` 的作用域

- 如果你没有使用 ES6, 那你必须将 ```this``` 保存到某个变量中

完整示例
-------

- 创建组件

```shell
# 创建一个 .vue 文件
touch UserProfileOptions.vue
```

- 元素顺序

```html
<!-- UserProfileOptions.vue -->
<template></template>
<script></script>
<style></style>
```

- 编写组件

```javascript
// 当你的组件开始觉得密集或难以阅读时
// 在多个属性之间添加空行可以让其变得容易
export default {
  // 通文件名称, 始终使用 PascalCase
  name: "UserProfileOptions",

  components: {},

  directives: {},

  filters: {},

  extends: {},

  mixins: [],

  // Prop 声明, 始终使用 camelCase
  // 若有多个 Prop, 请按字母将其排序
  // g -> i -> l -> v
  props: {
    greetingText: String,

    icon: String

    label: String,

    value: {
      type: String,
      required: true
    }
  },

  data() {
    return {
      form: {},

      table: {},

      pagination: {},
    }
  },

  computed: {},

  watch: {},

  // 生命周期钩子函数

  created() {},

  mounted() {},

  // ...

  methods: {}
}
```

- 使用组件

```html
<user-profile-options greeting-text="hi" value="val"></user-profile-options>
```

务必遵守
=======

必须为 v-for 设置键名
-------------------

```html
<ul>
  <li 
    v-for="todo in todos" 
    :key="todo.id"
  >
    {{ todo.text }}
  </li>
</ul>
```

严禁将 v-for 与 v-if 用在一起
----------------------------

- 为了过滤一个列表中的项目, 如: ```v-for="user in users" v-if="user.isActive"```, 在这种情形下, 请将 ```users``` 替换为一个计算属性 (比如 ```activeUsers```), 让其返回过滤后的列表。

```html
<ul>
  <li v-for="user in activeUsers" :key="user.id">
    {{ user.name }}
  </li>
</ul>
```

- 为了避免渲染本应该被隐藏的列表 (比如 ```v-for="user in users" v-if="shouldShowUsers"```). 这种情形下, 请将 ```v-if``` 移动至容器元素上 (比如 ```ul```,  ```ol```).

```html
<ul v-if="shouldShowUsers">
  <li
    v-for="user in users"
    :key="user.id"
  >
    {{ user.name }}
  </li>
</ul>
```

统一指令缩写
-----------

```html
<input 
  :value="value" 
  :placeholder="placeholder" 
  @click="onClick" 
  @focus="onFocus"
>
```

严禁使用 ```$``` 或 ```_``` 来声明任何属性
---------------------------------

>为什么?

Vue 使用 ```_``` 前缀来定义其自身的私有属性, 所以使用相同的前缀 (比如 ```_update```) 有覆写实例属性的风险. 即便你检查确认 Vue 当前版本没有用到这个属性名，也不能保证和将来的版本没有冲突.

对于 ```$``` 前缀来说，其在 Vue 生态系统中的目的是暴露给用户的一个特殊的实例属性，所以把它用于私有属性并不合适.

不过，推荐把这两个前缀结合为 ```$_```，作为一个用户定义的私有属性的约定，以确保不会和 Vue 自身相冲突。

```javascript
var myGreatMixin = {
  // ...
  methods: {
    $_myGreatMixin_update: function () {
      // ...
    }
  }
}
```

只在需要时创建组件
----------------

>为什么

Vue 是一个基于组件的框架, 如果你不知道何时创建组件可能会导致以下问题:

- 如果组件太大, 可能很难重用和维护;

- 如果组件太小, 你的项目就会（因为深层次的嵌套而）被淹没, 也更难使组件间通信;

>怎么做

- 始终记住为你的项目需求构建你的组件，但是你也应该尝试想到它们能够从中脱颖而出（独立于项目之外）。如果它们能够在你项目之外工作，就像一个库那样，就会使得它们更加健壮和一致。

- 尽可能早地构建你的组件总是更好的，因为这样使得你可以在一个已经存在和稳定的组件上构建你的组件间通信（```props``` & ```events```）。

>规则

- 首先，尽可能早地尝试构建出诸如模态框、提示框、工具条、菜单、头部等这些明显的（通用型）组件。总之，你知道的这些组件以后一定会在当前页面或者是全局范围内需要。

- 第二，在每一个新的开发项目中，对于一整个页面或者其中的一部分，在进行开发前先尝试思考一下。如果你认为它有一部分应该是一个组件，那么就创建它。

- 最后，如果你不确定，那就不要。避免那些“以后可能会有用”的组件污染你的项目。它们可能会永远的只是（静静地）待在那里。注意，一旦你意识到应该这么做，最好是就把它打破，以避免与项目的其他部分构成兼容性和复杂性。