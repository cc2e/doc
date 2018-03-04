# Vue	

1.vue-cli  项目结构详解

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

### Vue 生命周期

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
          message : "xuxiao is boy" 
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



---

### Vue 基础



- 插值 v-html, v-once, v-model="inputmsg"  

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


- v-bind, v-on ,v-for,v-if

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

```
<div v-bind:class="{active:isActive,'text-danger':hasError}"></div>  


data{
    isActive:true,
    hasError:false
}

```

