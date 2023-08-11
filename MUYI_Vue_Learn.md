# 0 看到第22节课

[2-22 案例：路飞学城（第一版）_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV16s4y1G7EY?p=22&spm_id_from=pageDriver&vd_source=c9b9da55d37a295c3ae7d4aae11b06f5)

# 1 初始学习

## 示例代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vite App</title>
    <!--    引入vue.js文件-->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
    <!--    这个模块里的数据是由vue接管的-->
    <div id="app">
        <h1>我是{{ name }}</h1>
        <h1>微信是{{ wechat }}</h1>
        <input type="button" value="点我" v-on:click="clickMe">
    </div>

    <!--    创建vue对象，并关联指定的HTML区域-->
    <script>
        var app = new Vue({
            // el指定管理的区域，这里是id是app的块
            el: '#app',

            data: {
                name: '哈哈',
                wechat: 'haha'
            },

            //存放函数
            methods: {
                clickMe: function () {
                    //获取this.name
                    //修改值this.name
                    this.name = '呼呼';
                    this.wechat = 'huhu';
                }
            }
        })

    </script>

</body>
</html>

```





# 2 Vue常见指令

## 1 插值表达式

**用于将js里的值引入到html里**

```html
{{name}} # 直接用变量

{{person.name}} # 直接用字典变量里的值

{{'haha'}} # 直接用常量

{{'haha' + 'huhu'}} # 字符串是可以相加来连接起来的

{{base + 1 + 1}} # 用js代码
{{1===1 ? 'haha' : 'huhu'}} # 用表达式

```



## 2 v-bind指令

- **对标签中的属性的值进行操作**

- **可以通过js代码来实现样式的动态改变**

- **html里的语法类似python**

- **v-bind是单向绑定，只能js影响html的值，不会html的值影响js里的值**

```html
<img src="abc"></img> # 原来

<img v-bind:src="imgUrl"></img> # 用v-bind，用vue里的data里的变量imgUrl来给src赋值
```

```html
# 使用字典，根据v1和v2的true和false值，来决定info和danger是否要使用，true就使用，false就不使用
<h1 v-bind:class="{info:v1,danger:v2}">
    haha
</h1>

# 字典可以直接写在data里，在html里直接用变量表示就好了
```

```html
# 使用列表，包含多个类
<h1 v-bind:class="[info,danger]">
    haha
</h1>

# 还可以这样
<h1 v-bind:class="[1===1?'x':'y',danger]">
    haha
</h1>
```

```html
# style样式也是可以的
# clr是vue里data里的变量，fontsize是直接最基本的style的写法
<h1 v-bind:style="{color:clr, fontsize:'19px'}">
    haha
</h1>
```

- **v-bind的简写**

```vue
<h1 v-bind:style="{color:clr, fontsize:'19px'}">
    haha
</h1>

等价于，可以不写v-bind，只写一个冒号

<h1 v-bind:style="{color:clr,  fontsize:'19px'}">
    haha
</h1>
```



## 3 v-model指令

- **是双向绑定的，js里的值和html里的值始终相等**
- **v-model记录的是最终输入或选择的结果**

```html
# 这里的v-model是会将data里的数据user显示在输入框中，同时因为双向绑定的特性，在html里输入的数据就会直接改变user变量的值
<input type="text" v-model="user">
```



## 4 v-for指令

- **就是循环遍历数据**

```vue
# 将datalist里的值循环显示出来
<li v-for="item in datalist">{{item}}</li>

# 将datalist里的值循环显示出来，这里的idx会是item的索引
<li v-for="(item，idx) in datalist">{{idx}}-{{item}}</li>

# 循环字典，先值后键
<li v-for="(value,key) in datalist">{{key}-{{value}}</li>

# 循环里面套循环
<li v-for="(item，idx) in datalist">{{idx}}-{{item}}
	<span v-for="(v,k) in item">{{k}}-{{v}}</span>
</li>
```



## 5 v-on指令

- **v-on可以简写成@**

```vue
# 常见属性
v-on:click
v-on:dbclick
v-on:mouseover
v-on:mouseout
v-on:change
v-on:focus
...
```



## 6 v-if指令

- **if里判断为false会直接不渲染标签**

```vue
# 根据isLogin的值，来决定显示的内容
<a v-if="isLogin">{{user}}</a>
<a v-else-if="isLogout">{{user}}</a> # 这两句可有可无
<a v-else>登录</a>                    # 这两句可有可无
```



## 7 v-show指令

- **功能类似v-if，只是v-show会渲染出标签，同时给不成立的标签里加入`display:none`**

```vue
# 只有这一句
<a v-show="isLogin">{{user}}</a>
```





# 3 Vue组件开发(组件感觉就是小的html页面)

## 1 局部组件

- **写在script里的**
- **template里是要显示的样式，其中的数据是从data里取出来的**

```vue
let Son = {
	 data(){
        return {
            
        }
    },
    methods:{
        
    },
    computed:{
        
    },
    create(){
	}
}
....
{
    template:`<Son />`,
    components:{
        Son
    }
}
```

- **同时要在vue对象里添加组件(挂载)**

```vue
components:{
	demo,     # 直接引用
	haha:ha   # 用ha来当haha的别名
}
```

- **在html里用组件**

```vue
# 直接
<demo></demo>
<ha></ha>
```



## 2 全局组件

- **不用在vue里挂载就能直接在html里使用**

```vue
vue.component('组件的名字',{
    data(){
        return {
            msg:'hahah'
        }
    },
    methods:{
        
    },
    computed:{
        
    },
    create(){
	}
    
    
})
```



# 4 vue-router使用

- **用于单页面开发，使用多组件实现类似多页面的效果**

```vue
 //如果以后是模块化编程，Vue.proptotype.$VueRouter = VueRouter
    //    Vue.use(VueRouter)
    const Home = {
        data() {
            return {}
        },
        template: `<div>我是首页</div>`
    }
    const Course = {
        data() {
            return {}
        },
        template: `<div>我是免费课程</div>`
    }
    //2.创建路由
    const router = new VueRouter({
        //3.定义路由规则
		// 一个路由一个组件
        mode:'history',
        routes: [
            {
              path:'/',
              redirect:'/home'
            },
            {
                path: '/home',
                component: Home
            },
            {
                path: '/course',
                component: Course
            }
        ]
    })
    let App = {
        data() {
            return {}
        },
//        router-link和router-view 是vue-router 提供的两个全局组件
        //router-view  是路由组件的出口
        //router-link默认会被渲染成a标签，to属性默认被渲染成href
        template: `
            <div>

                <div class="header">
					
                    <router-link to = '/home'>首页</router-link>
                    <router-link to = '/course'>免费课程</router-link>
                </div>
                <router-view></router-view>
            </div>

        `

    }
    new Vue({
        el: '#app',
        //4.挂载 路由对象
        router,
        data() {
            return {}
        },
        template: `<App />`,
        components: {
            App
        }
    })
```



