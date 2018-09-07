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

   ***关于Vue-Router，我所爬过的坑***<br>
   A.初学新手的盲区1<br>
     1.同级多个路由，每个路由对应一个router-view--------------错误理解<br>
     【正确解析】同级多个路由，如果显示在一个页面的同一区域，那么只需要一个router-view<br>
                同级多个路由，如果显示在一个页面不同位置，那么参照[这里](https://jsfiddle.net/posva/6du90epg/)<br>
   B.初学新手的盲区2<br>
      1.同时使用路由传参（params）与keep-alive------------错误做法<br>
      【正确解析】同时使用了路由传参与keep-alive之后，第一次使用没问题，但是第二次使用的时候，我们会发现，保留了上一次的参数，keep-alive就适得其反失去了它的作用。<br>
   ***关于keep-alive的认知***<br>
   ```bash
   新增属性：
   
   include：匹配的 路由/组件 会被缓存
   exclude：匹配的 路由/组件 不会被缓存
   include和exclude支持三种方式来有条件的缓存路由：采用逗号分隔的字符串形式，正则形式，数组形式。
   
   正则和数组形式，必须采用v-bind形式来使用。
    <!-- 逗号分隔字符串 -->
       <keep-alive include="a,b">
         <component :is="view"></component>
       </keep-alive>
       
       <!-- 正则表达式 (使用 `v-bind`) -->
       <keep-alive :include="/a|b/">
         <component :is="view"></component>
       </keep-alive>
       
       <!-- 数组 (使用 `v-bind`) -->
       <keep-alive :include="['a', 'b']">
         <component :is="view"></component>
       </keep-alive>
       匹配规则：
       
       1.首先匹配组件的name选项，如果name选项不可用。
       2.正则则匹配它的局部注册名称。 (父组件 components 选项的键值)
       3.匿名组件，不可匹配。
       #比如路由组件没有name选项，并且没有注册的组件名。
       
       1.只能匹配当前被包裹的组件，不能匹配更下面嵌套的子组件。
       2.比如用在路由上，只能匹配路由组件的name选项，不能匹配路由组件里面的嵌套组件的name选项。
       
       文档：<keep-alive>不会在函数式组件中正常工作，因为它们没有缓存实例。
       exclude的优先级大于include
       也就是说：当include和exclude同时存在时，exclude生效，include不生效。
       ##当组件被exclude匹配，该组件将不会被缓存，不会调用activated 和 deactivated。
   ```
   -----》完整Vue生命周期[参考地址](https://blog.csdn.net/Honnyee/article/details/81162036)
>短期感悟

  ```bush
   
    书山有路勤为径，学海无涯苦作舟。
    
   ```
>完整Vue学习笔记

 [我在这儿呢，请点击这里!!!](https://github.com/Full-stack-project-team/Vue-Express--http-proxy-middleware-/blob/master/README.md)
>PubSub小记

--重中之中--【subscribe必须在publish之前】，两个惯用的套路就是
```bash
 套路1：在点击事件中发布消息，在mounted钩子函数中订阅消息
 套路2：在点击事件中发布消息，在created钩子函数中订阅消息
（套路2注意的是，在created生命周期中，Vue的this其实已经存在）
```


