

##### 必备组件  koa开发 

```
let koa = require('koa');
let static = require('koa-static');
let router = require('koa-router');
let body = require('koa-body');
let path = require('path');
let fs = require('fs');
let os = require('os');

```





```javascript
const Koa = require('koa');
const app = new Koa();
const fs = require('fs');
const router = require('koa-router'); //路由
const static = require('koa-static');
const path = require('path');

let handler = ctx=>{
   try{
    // ctx.request.accepts('html')   [browser要接收什么 mime类型的数据]
    //ctx.response.type ='xml' mime 类型 [xml,html,text,json,....]
    //ctx.response.body = "hello";  
    //ctx.response.body = fs.createReadStream('./hello.html'); //读取模板数据
    
    
    //ctx.request.path!=='/'    手动路由，高级的可以使用 koa-router
    
   
    //ctx.response.redirect('/'); //手动重定向方法
    
    //ctx.throw(500);  错误处理
    
    //ctx.response.status=404;
    //ctx.response.body = 'page not found';
       
   }catch(err){
       console.log(err);
       //error 发射事件
       
       ctx.app.emit('error',err,ctx);
   }
}




 /*
     app.use(router.get("/",home));
     app.use(router.get("/handler",handler'))
     app.use(router.get('/about',about));
     
     //路由方式 重定向
	  app.use(router.get("/admin",redirect));
    */

// console.log(path.join(__dirname)) //输出当前目录的绝对地址
//app.use(static(path.join(__dirname))).listen(3000);  //静态服务器



//error监听器

const main = ctx=>{
    ctx.throw(500);
}

app.on('error',(err,ctx)=>{
    console.error('server error',err);
})




//cookie 
const login = function(ctx){
    const n = Number(ctx.cookies.get('view')||0)+1;
   	ctx.cookie.set('view',n);
    ctx.response.body = n+'views';
}

//表单数据
const koaBody = require('koa-body');
const reg = ctx=>{
    const body = ctx.request.body;
    if(!body.name)ctx.throw(400,'.name required');
    ctx.body = {name:body.name};
    /*
    	curl 测试
       curl -X POST --data 'name=hello' 127.0.0.1:3000
       curl -X POST --data 'name' 127.0.0.1:3000  //name required
    */
}
app.use(koaBody());



//文件上传
const os = require ('os');
const path = require('path');
const koaBody = require('koa-body');

const main =async (ctx)=>{
    const tmpdir = os.tmpdir();
    const filePaths = [];
    const files = ctx.request.body.files||{};
    for(let key in files){
        const file = files[key];
        const filePath = path.join(tmpdir,file.name);
        const reader = fs.createReadStream(file.path);
        const writer = fs.createWriteStream(filePath);
        reader.pipe(writer);
        filePaths.push(filePath);
    }
    ctx.body=filePaths;
}
app.use(koaBody({multipart:true}));

//curl 模拟提交
curl --form upload=@/path/to/file.jpg http://127.0.0.1:3000


app.listen(3000);

```

