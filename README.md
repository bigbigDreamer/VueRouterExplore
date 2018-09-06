# vue

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
## VueRouter详解[编程式导航]
>路由去除/#/，采用浏览器history模式--mode:'History'
```bush
 import Vue from 'vue'
     import Router from 'vue-router'
     import Single from '../components/Single'
     import Panel from '../components/Panel'
     Vue.use(Router)
     
     export default new Router({
       mode: 'history',
       routes: [
         {
           path:'/',component: Panel
         },
         {path: '/single/:userId', component: Single,name:'single'}
       ]
 })
 ```
 >路由重定向---redirect属性
 ```bush
 import Vue from 'vue'
     import Router from 'vue-router'
     import Single from '../components/Single'
     import Panel from '../components/Panel'
     Vue.use(Router)
     
     export default new Router({
       mode: 'history',
       routes: [
         {
           path:'/',component: Panel,redirect:'/home'
         }
       ]
 })
```
>子路由--children
```
 import Vue from 'vue'
     import Router from 'vue-router'
     import Single from '../components/Single'
     import Panel from '../components/Panel'
     Vue.use(Router)
     
     export default new Router({
       mode: 'history',
       routes: [
         {
           path:'/',component: Panel,redirect:'/home',
           children:[
           {
              path:'/asp',component:Asp
           }
           ]
         }
       ]
 })
```
>路由守卫--做登录验证使用
```bush
    此处关于路由守卫的知识暂不做处理，等到后期做高级VueApp之时再做详尽了解
```
>编程式导航
```bush
   methods: {
      handleClick(index) {
        this.$router.push({ name: 'single',
        params: { 
        userId: index,
        content: this.$refs.li[index].innerText,
        topic:this.Persons[index].topic
        }
        })
        this.$pub.publish('d',this.$refs.li[index].innerHTML)
      }
    },
```
>相关总结

   关于Vue-Router，我所爬过的坑：<br>
   A.初学新手的盲区1<br>
     1.同级多个路由，每个路由对应一个router-view--------------错误理解<br>
     【正确解析】同级多个路由，如果显示在一个页面的同一区域，那么只需要一个router-view<br>
                同级多个路由，如果显示在一个页面不同位置，那么参照[这里](https://jsfiddle.net/posva/6du90epg/)<br>
   B.初学新手的盲区2<br>
      此处有待发现............<br>
>短期感悟

  ```bush
   
    书山有路勤为径，学海无涯苦作舟。
    
   ```
>完整Vue学习笔记

 [我在这儿呢，请点击这里!!!](https://github.com/Full-stack-project-team/Vue-Express--http-proxy-middleware-/blob/master/README.md)

