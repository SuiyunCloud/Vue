# Vuex
1. normal usage
```js
// in store.js define vuex
Vue.use(Vuex)
const store = new Vuex.Store(
    {
        state:{
            count: 0,
            list: [1,2,5,10,45]
        },
        //mutations can only be used to change the value in vuex, can't async
        mutations:{
            increment(state) {
                state.count ++;
            }
        },
        //getters used to return processed original state variable
        getters: {
            filteredList: state => {
                return state.list.filter(item => item < 10>)
            }
        },

        //function like mutations, but can do async
        actions: {
            increment(state) {
                state.count ++;
            }
        }
    }
)

// in main.js, register store defined
new Vue({
  el: '#app',
  router,
  store,
  render: h => h(App)
})


// in other module
<template>
<div>{{global_count}}</div>
</template>

<script>
export default {
    computed: {
        global_count () {
            return this.$store.state.count  //use $store.state to get data in vuex
        }
    },
    methods: {
        // call mutations' function to change vuex in other module
        handleIncrement (){
            this.$store.commit('increment');
        }
    }
}
```

2. Module


# Vue router
1. setup
```sh
    npm install vue-router --save
```

2. Use router
```js
// in main.js
import VueRouter from 'vue-router'
Vue.use(VueRouter)


//1. create component and import component

//2. Define router
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar },
  {path: '*'}, //match any  route
  {path: '/user-*'} //match route start with /user-
]

//3. create router instance
const router = new VueRouter({
  routes // short for `routes: routes`
})

//4. mount router
const app = new Vue({
  router
}).$mount('#app')


//5. in  app.vue put position where to mount the router refered component
 <router-view></router-view>
```

3. redirect to router
```js
//in html
 <router-link to="/foo">Go to Foo</router-link>


 // in router definition
const routes = [
  { path: '/', redirect: '/hello' },
]
 ```

4. dynamic route
`:param` can get the parameters in specific position, `query` used to get key-value's value after `?`

```js
// 1. define the parameters in router
const routes = [
  { path: '/hello/:num', component: Hello },
  { path: '/queryUrl', component: Query }
]

//2. use the parameter in component
this.$route.params.num
this.$route.query.name

//3. spell the route when necessary
    //in Hello component
    <router-link :to="'/hello/' + item">{{ item }}</router-link>

    //in Query component
    <router-link :to="'/queryUrl?name=' + item">{{ item }}</router-link>
```

5. Named routes
Offer name for routes
```js
const router = new VueRouter({
  routes: [
    {
      path: '/user/:userId',
      name: 'user',
      component: User
    }
  ]
})

// route can be used as follows
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>
```

6. Programmatic Navigation

* router.push(location, onComplete?, onAbort?)
```js
// 字符串
this.$router.push('home')

// 对象
this.$router.push({ path: 'home' })

// 命名的路由
this.$router.push({ name: 'user', params: { userId: '123' }})

// 带查询参数，变成 /register?plan=private
this.$router.push({ path: 'register', query: { plan: 'private' }})

```

* router.replace(location, onComplete?, onAbort?)

    跟 router.push 很像，唯一的不同就是，它不会向 history 添加新记录，而是跟它的方法名一样 —— 替换掉当前的 history 记录

* router.go(n)

    这个方法的参数是一个整数，意思是在 history 记录中向前或者后退多少步，类似 window.history.go(n)。
    ```js
    // 在浏览器记录中前进一步，等同于 history.forward()
    router.go(1)

    // 后退一步记录，等同于 history.back()
    router.go(-1)

    // 前进 3 步记录
    router.go(3)

    // 如果 history 记录不够用，那就默默地失败呗
    router.go(-100)
    router.go(100)
    ```

7. Nested routes
```js
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User,
      children: [
        {
          // UserProfile will be rendered inside User's <router-view>
          // when /user/:id/profile is matched
          path: 'profile',
          component: UserProfile
        },
        {
          // UserPosts will be rendered inside User's <router-view>
          // when /user/:id/posts is matched
          path: 'posts',
          component: UserPosts
        }
      ]
    }
  ]
})
```

8. route Modular
```js
// 1. define a sub router constant in component package
import UserList from './UserList';
import UserDetail from './UserDetail';
import UserPosts from './UserPosts';

export const userRoutes = [
  { path: '/', component: UserList },
  {
    path: '/:userId',
    component: UserDetail,
    children: [{ path: '/:userId', component: UserPosts }],
  },
];

//2. in main.js
import { userRoutes } from '../components/user/user.routes';

const routes = [...userRoutes];

const router = new VueRouter({
  routes,
});
```

9. Passing Props to Route Components
```js
// pass para through props
const router = new VueRouter({
  routes: [
    { path: '/promotion/from-newsletter', component: Promotion, props: { newsletterPopup: false } }
  ]
})


const router = new VueRouter({
  routes: [
    { path: '/search', component: SearchUser, props: (route) => ({ query: route.query.q }) }
  ]
})


// use the para with props
props: ["newsletterPopup", "route],
```
