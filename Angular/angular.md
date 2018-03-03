#  Angular4

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
   根组件
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
   ​






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



- ngIf

  ```javascript
  <div *ngIf="condition"><p>condition=true P不显示</p></div>
  ```


  <div *ngIf="condition;the thenBlock else elseBlock"></div>
  <ng-template #thenBlock"></ng-template>
  <ng-template #elseBlock"></ng-template>



  <div *ngIf="condition as value;else elseBlock"></div>
  <ng-template #elseBlock"></ng-template>

  ```

  
  ```