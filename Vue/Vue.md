# Vue	

1.vue-cli  项目结构详解

> 
>
> npm i -g  @vue-cli   //最新版 3.0 暂时不用
>
> 
>
> npm  i -g  vue-cli     //2.2
>
> vue   init  webpack my-vue   //进行项目初始配置
>
> 
>
> 

必备模块

```javascript
import Vue from 'vue';   //核心
import vueRouter from 'vue-router';   //组件切换
import axios from 'axios';   //http请求库
```



**component property**

```Javascript
$options
$parent
$refs
$root
$scopedSlots
$slots
$vnode
$attrs
$children
$el
$props
$route    //读取query 和 params 参数用
$router  //路由器地址 注入工具
$data

```



**路由传参**

```vue
//路由中传参
:to="{name:routeName,params:{id:123}}" //隐式传参  name:组件的name  params 不会真正的地址栏中显示
//获取参数
{{$route.params.id}}/123


:to="{path:"/blog/js,query:{id:123}}"  //显示传参 ／blog/js?id=123
{{$route.query.id}}//123
```



**父组件方问子组件** 

```
this.$children: :array
```



 **子组件访问父组件**

```javascript
this.$parent 
```



组件个数较多时，我们难以记住各个组件的顺序和位置，通过序号访问子组件不是很方便。
在子组件上使用 **ref ** 指令，可以给子组件指定一个索引 ID。

```javascript
//this.$refs:array
<child-component1 ref="cid1"/>
<child-component2 ref="cid2"/>
<button @click="showChildComponentData">显示子组件的数据</button>
showChildComponentData(){
    console.log(this.$refs.cid1)
}
```



**路由重定向**

> path:/originpath,       
>
> redirect : '/routepath'

```javascript
普通重定向
{
    path:'webgl',    //访问 webgl会转到react
    redirect:'react',
    name:'Webgl',
    component:Webgl
}

动态返回重定向
{
    path:'/a',
        redirect:to=>{
            //计算返回路由的path
            return '/cc';
        }
}



```



**别名 alias**

```
routes:[
    {
       // home 是 index的别名
        path:'/index',component:Index,alias:"/home"
    }
]
```







---

# 组件通信 



**通过props子获取父组件传递的参数**

```javascript
//父组件
<childComponent v-bind:parentArg="msg">

//子组件
export default{
	props:['parentArg'],
}    

    
```



**父组件获取子组件传递的消息**  

> v-on:child-msg="childmsg"  

> this.$emit("childmsg","我是子组件的消息");

```javascript
//父组件
<childComponent v-on:child-msg="childmsg"></childComponetn>
export default{
    methods:{
        valueUp(msg){
            //接收子组件递来的消息
            this.childMsg=msg;
        }
    }
}


//子组件件环境，通过事件发送消息
method:{
    enterFather(){
        this.$emit("childMsg","我是向父组件递交的消息");
    }
}



```





---

**获取自定义属性**   

```javascript
<h5 class="left t-title" @click='getDataId(item.id)' :data-id="item.id"></h5>

<script>
    methods: {
        getDataId(id) {
            console.log(id);
        }
      },
    
</script>
```









---

## Vue项目结构

```javascript
build/
	|-build.js       //项目构建相关码,webpack配置
	|-check-versions.js	   node,npm版本检查 
	|-dev-client.js			客户端热加载
	|-dev-server.js			构建本地服务器
	|-utils.js				构建配置公用工具
	|-vue-loader.conf.js		vue加载器
	|-webpack.base.conf.js		基础配置
	|-webpack.dev.conf.js		开发环境配置
	|-webpack.prod.conf.js		生产环境配置
config/	
	|-dev.env.js   开发环境变量
	|-index.js		项目环境变量
	|-prod.env.js	生产环境变量
node_modules/
src/
	|-assets/   资源目录
    	|-logo.png 
	|-components/  公共组件目录
		|-Hello.vue
    |-router/
   		|-index.js 路由配置目录	
    |-App.vue   页面入口文件(根组件)
	|-main.js	程序入口文件（入口JS文件）
static/     静态文件，图片
.babelrc   	babel语法编译配置
.editorconfig	定义代码格式
index.html	 入口页面
package.json


```



> 每个Vue应用都是通过 Vue函数创建一个新的Vue实例的







---

### Vue component 生命周期 8个钩子

> 创建和挂载：beforeCreate  -> created -> beforeMount -> mounted
>
> 更新：beforeUpdate -> updated
>
> 销毁：beforeDestroy -> destroyed

1. beforeCreate
2. created
3. beforeMount
4. mounted
5. beforeUpdate
6. updated
7. beforeDestroy
8. destroyed

```
<html>
<head>
    <title></title>
    <script type="text/javascript" src="https://cdn.jsdelivr.net/vue/2.1.3/vue.js"></script>
</head>
<body>

<div id="app">
     <p>{{ message }}</p>
</div>

<script type="text/javascript">
    
  var app = new Vue({
      el: '#app',
      data: {
          message : "the message" 
      },
       beforeCreate: function () {
                console.group('beforeCreate 创建前状态===============》');
               console.log("%c%s", "color:red" , "el     : " + this.$el); //undefined
               console.log("%c%s", "color:red","data   : " + this.$data); //undefined 
               console.log("%c%s", "color:red","message: " + this.message)  
        },
        created: function () {
            console.group('created 创建完毕状态===============》');
            console.log("%c%s", "color:red","el     : " + this.$el); //undefined
               console.log("%c%s", "color:red","data   : " + this.$data); //已被初始化 
               console.log("%c%s", "color:red","message: " + this.message); //已被初始化
        },
        beforeMount: function () {
            console.group('beforeMount 挂载前状态===============》');
            console.log("%c%s", "color:red","el     : " + (this.$el)); //已被初始化
            console.log(this.$el);
               console.log("%c%s", "color:red","data   : " + this.$data); //已被初始化  
               console.log("%c%s", "color:red","message: " + this.message); //已被初始化  
        },
        mounted: function () {
            console.group('mounted 挂载结束状态===============》');
            console.log("%c%s", "color:red","el     : " + this.$el); //已被初始化
            console.log(this.$el);    
               console.log("%c%s", "color:red","data   : " + this.$data); //已被初始化
               console.log("%c%s", "color:red","message: " + this.message); //已被初始化 
        },
        beforeUpdate: function () {
            console.group('beforeUpdate 更新前状态===============》');
            console.log("%c%s", "color:red","el     : " + this.$el);
            console.log(this.$el);   
               console.log("%c%s", "color:red","data   : " + this.$data); 
               console.log("%c%s", "color:red","message: " + this.message); 
        },
        updated: function () {
            console.group('updated 更新完成状态===============》');
            console.log("%c%s", "color:red","el     : " + this.$el);
            console.log(this.$el); 
               console.log("%c%s", "color:red","data   : " + this.$data); 
               console.log("%c%s", "color:red","message: " + this.message); 
        },
        beforeDestroy: function () {
            console.group('beforeDestroy 销毁前状态===============》');
            console.log("%c%s", "color:red","el     : " + this.$el);
            console.log(this.$el);    
               console.log("%c%s", "color:red","data   : " + this.$data); 
               console.log("%c%s", "color:red","message: " + this.message); 
        },
        destroyed: function () {
            console.group('destroyed 销毁完成状态===============》');
            console.log("%c%s", "color:red","el     : " + this.$el);
            console.log(this.$el);  
               console.log("%c%s", "color:red","data   : " + this.$data); 
               console.log("%c%s", "color:red","message: " + this.message)
        }
    })
</script>
</body>
</html>
```





## 组件 script结构

```javascript
<script>
export default {
  name:'App',
  components: {  },
  data () { //属性
      return {
          
      }
  },
  props: {
    txt: {
      type: String,
      default: '附近商家'
    }
  },
  watch: {},
  methods: {  //方法
         
  },
  filters: {},
  computed: {},
  created () {},
  mounted () {},
  destroyed () {}

}
</script>
```







---

### Vue 基础指令 



- 插值 v-html,      v-once,     v-model="inputmsg"  

  ​

  ```javascript
  {{message.split('').reverse().join('')}}

  <p v-html="readHtml"></p>

  readHtml='<span>afdasdfs</span>'

  {{number+5}} 
  {{ok?'yes':'no'}}

  <div v-bind:id="'list'+id">vvvv</div>

  双向绑定
  <p>{{inputmsg}}</p>
  <input v-model="inputmsg" type='text'>

  ```

  ​


- v-bind,     v-on    ,v-if    v-else , v-show   ,
- v-for="item in items"   arrary:v-for="{item,index} in items"       object:v-for="{item,key,index} in items"

```javascript
{{meassge}}

v-bind
<a v-bind:href="url">...</a>
<a :href="url"></a>  缩写

v-on
<a v-on:click="doSomething">btn</a>
<a @click="doSomething">btn</a>
<form v-on:submit.prevent="onSubmit">..</form>  // .prevent 表示 event.preventDefault();



v-for
 <li class="osli" v-for="list in todos">
        {{list.text}}
 </li>

todos: [
        {text: '好好学习 天天向上'},
        {text: '绝世武神'},
        {text: '神默尘晕'}
      ],


```



**数组更新检测—触发视图更新的方法**

> push、pop、shift、unshift、splice、sort、reverse





插值

```javascript
<div id="example">
	<p>"{{message}}"</p>
	<p>"{{reversedMessage}}"</p>
</div>

var vm = new Vue({
    el:'#example",
    data:{  //属性
        message:'Hello',
        answer:'',
    },
    computed: { //计算属性
        reversedMessage: function(){
            return this.message.split('').reverse().join('');
        }
    },
    methods:{ //方法
        fn1: function(){
            
        },
        fn2: function(){
            
        },
        getAnswer:function(){
            axios.get('https://yeson.com/api).then(function(data){
                conole.log(data);
                vm.answer=data.text;
            }).catch(function(error){
               	console.log(error);
            })
        }
    },
    watch: { //监听器
        question: function(newString,oldString){
            this.answer="adfasdfadf';
            this.getAnswer();
        }
    }
})

// Hello
// olleH
```





#### class与Style

```javascript
<div v-bind:class="{active:isActive,'text-danger':hasError}"></div>  


data{
    isActive:true,
    hasError:false
}



<div v-bind:class="[activeClass,errorClass]"></div>
data(){
    return{
        activeClass:"active",
        errorClass:"text-danger"
    }
}


<div :style="{color:activeColor,fontSize:fontSize+'px'}"></div>
<div v-bind:style="styleObject"></div>


<div :style="{display:['-webkit-box','-ms-flexbox','flex']}"></div>

```





# 事件

事件监听，绑定  **v-on**

事件修饰符

> .stop      阻止事件冒泡
>
> .prevent    阻止默认事件
>
> .capture  事件捕获
>
> .self   只对该元素触发的事件
>
> .once  一次性事件，
>
> .passive  提修事件监听器的性能写法 addEventListener(obj,fn,passive)



#### 键盘修饰符   @keyup.enter="methodName"

>.enter
>
>.tab
>
>.delete
>
>.esc
>
>.space
>
>[.up|.down|.left|.right]   
>
>.ctrl
>
>.alt
>
>.shift
>
>.meta



#### 鼠标修饰符

> .left 
>
> .right
>
> .middle



**.exact** 精确模式

```
//宽松模式，必须的事件存在即可
<button @click.ctrl="eveFn">ctrl+click</button>

//必须 ctrl被按下时修改才触发click
<button @click.ctrl.exact="onCtrlClick"> </button>



```









```javascript
@contextmenu.prevent="show()"   //取消默认事件
@click="add($event)"

Vue 支持所有js 事件
```



# vue UI组件库

- [Element](https://github.com/ElemeFE/element)


- [bootstrapVue](https://github.com/bootstrap-vue/bootstrap-vue/)


- [mint UI](https://github.com/ElemeFE/mint-ui)


- [vum](https://github.com/vum-team/vum)


- [vue Material](https://github.com/marcosmoura/vue-material)
- [muse-ui](https://github.com/museui/muse-ui)
- [Framework7-vue](https://github.com/nolimits4web/Framework7-Vue)

