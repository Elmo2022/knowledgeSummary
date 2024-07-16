## vue-router

> 学习自小满zs

#### 编程式导航 

 使用router实例对象的方法来实现

#### 历史记录

使用replace方法

#### 路由传参

query和params

**二者的区别**
1.query 传参配置的是 path，而 params 传参配置的是name，在 params中配置 path 无效

2.query 在路由配置不需要设置参数，而 params 必须设置

3.query 传递的参数会显示在地址栏中

4.params传参刷新会无效，但是 query 会保存传递过来的值，刷新不变 ;

5.路由配置

#### 嵌套路由

children

#### 命名视图

命名视图可以在同一级（同一个组件）中展示更多的路由视图，而不是嵌套显示。 命名视图可以让一个组件中具有多个路由渲染出口，这对于一些特定的布局组件非常有用。 命名视图的概念非常类似于“[具名插槽](https://so.csdn.net/so/search?q=具名插槽&spm=1001.2101.3001.7020)”，并且视图的默认名称也是 `default`。

#### 重定向

redirect

字符串形式配置

```typescript
const routes: Array<RouteRecordRaw> = [
    {
        path:'/',
        component:()=> import('../components/root.vue'),
        redirect:'/user1',
        children:[
            {
                path:'/user1',
                components:{
                    default:()=> import('../components/A.vue')
                }
            },
            {
                path:'/user2',
                components:{
                    bbb:()=> import('../components/B.vue'),
                    ccc:()=> import('../components/C.vue')
                }
            }
        ]
    }
]
```

对象形式配置

```typescript
const routes: Array<RouteRecordRaw> = [
    {
        path: '/',
        component: () => import('../components/root.vue'),
        redirect: { path: '/user1' },
        children: [
            {
                path: '/user1',
                components: {
                    default: () => import('../components/A.vue')
                }
            },
            {
                path: '/user2',
                components: {
                    bbb: () => import('../components/B.vue'),
                    ccc: () => import('../components/C.vue')
                }
            }
        ]
    }
]
```

函数模式（可以传参）

```typescript
const routes: Array<RouteRecordRaw> = [
    {
        path: '/',
        component: () => import('../components/root.vue'),
        redirect: (to) => {
            return {
                path: '/user1',
                query: to.query
            }
        },
        children: [
            {
                path: '/user1',
                components: {
                    default: () => import('../components/A.vue')
                }
            },
            {
                path: '/user2',
                components: {
                    bbb: () => import('../components/B.vue'),
                    ccc: () => import('../components/C.vue')
                }
            }
        ]
    }
]
```

#### 路由守卫

全局前置守卫

```typescript
router.beforeEach((to, form, next) => {
    console.log(to, form);
    next()
})
```

全局后置守卫



#### 路由元信息

meta中包含的信息（页面标题名称等等）

#### 动态路由

路由权限







### 面试题总结

#### hash路由和history路由

Vue Router 是 Vue.js 官方的路由管理器，它允许你构建单页面应用（SPA）。Vue Router 支持两种路由模式：hash 路由和 history 路由。这两种模式的主要区别在于 URL 的结构和浏览器历史记录的处理方式。

##### 1. Hash 路由

- **URL 结构**：使用 URL 的 hash 部分（即 `#` 后面的部分）来表示路由状态。例如：`http://example.com/#/home`。
- **兼容性**：由于 hash 部分不会包含在 HTTP 请求中，因此 hash 路由模式不会引起页面的重新加载或发送到服务器，这使得它在旧的浏览器中也能正常工作。
- **使用场景**：适合不需要服务器配置或不支持 HTML5 History API 的场景。
- **缺点**：URL 中的 `#` 可能会让用户感到困惑，且在一些情况下可能与页面内的锚点链接冲突。

##### 2. History 路由

- **URL 结构**：使用 HTML5 History API 来实现 URL 的变化，不包含 `#`。例如：`http://example.com/home`。
- **兼容性**：依赖于浏览器对 HTML5 History API 的支持，较新的浏览器通常都支持。
- **使用场景**：适合需要更“干净”的 URL 结构的应用，或者需要与服务器进行路由配置的应用。
- **服务器配置**：需要服务器支持，以便在用户直接访问 URL 时能够正确返回应用的入口文件（通常是 `index.html`）。服务器需要配置为对所有路由请求返回同一入口文件。

##### 比较

- **URL 可读性**：History 路由的 URL 更加简洁和可读，而 hash 路由的 URL 包含 `#`。
- **服务器要求**：History 路由需要服务器配置，而 hash 路由不需要。
- **SEO**：由于 History 路由的 URL 更接近传统的 URL 结构，因此在搜索引擎优化（SEO）方面可能更有利。
- **浏览器历史**：History 路由可以更好地利用浏览器的历史记录，例如前进和后退按钮，而 hash 路由则不会影响浏览器的历史记录。

### 示例配置

- **Hash 路由**：
  ```javascript
  import { createRouter, createWebHashHistory } from 'vue-router';
  
  const routes = [
    { path: '/home', component: Home },
    { path: '/about', component: About }
  ];
  
  const router = createRouter({
    history: createWebHashHistory(),
    routes
  });
  ```

- **History 路由**：
  ```javascript
  import { createRouter, createWebHistory } from 'vue-router';
  
  const routes = [
    { path: '/home', component: Home },
    { path: '/about', component: About }
  ];
  
  const router = createRouter({
    history: createWebHistory(),
    routes
  });
  ```

[vue路由中，history和hash两种模式有什么区别？- 题目详情 - 前端面试题宝典 (ecool.fun)](https://fe.ecool.fun/topic/e3a135b5-e6d4-4f1f-8e02-0c977e2ce768?orderBy=updateTime&order=desc&titleKey=路由)

