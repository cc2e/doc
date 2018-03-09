#  Angular

angular5 特征

构建优化，删除不必要的代码的应用程序

角度通用状态转移API和DOM支持

改进了角编译器以支持增量编译。

跨浏览器增加标准化

一个新的HttpClient

支持组件和指令的多个名称。

生命周期事件路由器

reflectiveinjector已与staticinjector更换，减少大多数开发者应用程序的大小

CLI 1.5默认情况下会创建角5项目。

rxjs响应程序库已经更新到版本5.5.2或后消除副作用的代码分裂









起步：

1. ```javascript
   npm i -g @angular/cli
   ```

2. ```javascript
   ng new my-app   //创建项目
   ```

3. ```javascript
   cd my-app 、 ng serve --open   // 启动服务器 并打开浏览器 http://localhost:4200
   ```

4. ```javascript
   目录结构
   src
    |
    |--/app
    |	 |--app.component.ts  //根组件
    |	 |--app.component.css  //根组件样式表
    |	 |--app.component.html //根组件模版
    |	 |--app.module.ts   //该模块依赖声明
    |
    |--／assts 			//这个放一些图片或其它的，打包时会自动copy到包中
    |--environmetns // 常用环境变量配置项，
    |--index.html   //入口文件
    |--main.ts     //应用入口点，并启动AppModule 打开浏览器 
   	
   ```


#### Angular组件生命周期

- constructor  构造器函数，一般用于注入服务

1. ngOnchanges   有数据输入时 
2. ngOnInit      组件初始化
3. ngDoCheck    手动触发更新检查
4. ngAfterContentInit    内容初始化到组件后
5. ngAfterContentChecked    内容变更检测后
6. ngAfterViewInit    视图初始化
7. ngAfterViewChecked  视图发生变化检查
8. ngOnDestroy    组件注销 该消毁 该移除就在这弄- 路由跳转时会执行该钩子，销毁该组件

```JAVASCRIPT
export class myComponent implements Onchages,Oninit,Docheck,AfterContentInit,AfterContentChecked,AfterViewInit,AfterViewChecked,OnDestroy{
    
}
```








```javascript

// 引入 ajax 和 jsonp 模块
import{HttpModule,JsonpModule} from '@angular/http'; //app.module.ts use

import {Http,Jsonp} from '@angular/http';  // component.ts  use 
 constructor(private http: Http ,private getJson: Jsonp){
     this.http.get('/api/items').subscribe(data=>{
 		console.log(data);
     })
  }


// Router模块
import {RouterModule, Routes} from '@angular/router';

import NgModule from '@angular/core';
import FormsModule from '@angular/froms'
```

######  *ngIf 

```javascript

  <div *ngIf="condition"><p>condition=true P不显示</p></div>

  <div *ngIf="condition;the thenBlock else elseBlock"></div>

  <ng-template #thenBlock"></ng-template>

  <ng-template #elseBlock"></ng-template>
  
  <div *ngIf="condition as value;else elseBlock"></div>

	<ng-template #elseBlock"></ng-template>
```





## Router 



##### 学好路由的大纲

1. angular 命令创建一个配置好的路由项目
2. angular自己创建路由
3. angular routerlink页面路转 默认跳转路由
4. angular routerUnkActive 设置routerLink默认选中路由
5. 路由动态传值
6. 路由的js跳转
7. 路由的js路转get传值
8. 父子路由



```javascript
ng new demo --routing   // 创建带路由功能的项目   “--routing”



{
  path: 'article',
  component:ArticleComponent
},
{
	path: 'articleDetail/:aid',  //动态路由配置
    component:ArticleDetailComponent
},
{
    path: '**', //任意路由
    component: NewsComponent
},
{
    path: '**',
    redirectTo:'home'   //重定向到home
},
{
    path:'news',
    component:'NewsComponent',
        childrens:[   //子路由
            {
                path:'tech',
            	component:'TechComponent'
            },
            {
                path:'fashion',
                component:'FashionComponent'
            }
        ]
}


<a routerLink="/article/tech" routerLinkActive="active">技术</a>
<a routerLink="/article/fashion" routerLinkActive="active">时尚</a>


<router-outlet> </router-outlet>


constructor(private router: Router){}

goNav() {
    this.router.navigator(['/newscontent',123]); //JS 跳转
}






goArticle(aid,id){
	let navigationExtras: NavigationExtras ={
    	queryParams: {'aid':aid,'id':id}
	}
    this.router.navigate(['/articledetail'],navigationExtras)
}

import{Router, NavigationExtras} from '@angular/router';

constructor(private router: ActivedRoute){}

this.router.queryParams.subscribe(function(data){
    console.log(data);
})  //获取get传值

```












  ```

#### 子组件通过 @Input 执行 父组件 属性 和 方法

  ```typescript
import {Input} from '@angular/core';

<child-component [propertyName]="propertyName" [fmethod]="fmethod"><\child-component> 
    // @规范    向子组件中传递 父组件的成员名称， key和v一定要一致，否则会无效 


// child-component.ts 
@Input() propertyName;   // 引入父组件的属性名 
@Input() fmethod;   // 引入父组件方法名


childMethod () {
  
    this.fmethod(); // 子组件方法调用父组件方法
}




  ```


### 子组件通过 @Output 向父组件传值

```javascript
1 子组件中引入  Output EventEmitter
import {Compontnt,OnInit,Input,Output,EventEmitter} from '@angular/core';

2 子组件中实例化 EventEmitter
@Output() private outer=new EventEmitter<String>();

3 子组件中 通过 EventEmitter 对象outer 实例广播数据
sendParent() {
	this.outer.emit("msg from child");
}

4 父组件调用子组件的时候，定义接收事件，outer就是子组件的EventEmitter对象 outer
<app-handle (outer)="runParent($event)"></app-handler>

5 父组件接收到数据会调用自己的 runParent()方法 ，这时就能拿到子组件的数据

子组件：handler-component
父组件  app-component
```



### @ViewChild  父子组件传值

```javascript
// 父组件调用子组件中的方法

//父组件ts文件
dataSet = [
    {"id":0,"name":"张三"},
    {"id":1,"name":"李四"}
  ]
  //@ViewChild(子组件名称)  随便命名:子组件名称
  @ViewChild(ChildComponent) child:ChildComponent;
  father(){
    //调用子组件方法
    this.child.childFn();
  }

//父组件html代码
<li *ngFor="let item of dataSet">
  <app-child [names] = "item" (click)="father()"></app-child>
</li>
```





