pm2  监控Node

forever 监控Node

Beanstalkd  消息队列



 # 全局变量

Buffer
__dirname
__filename
clearImmediate(immediateObject)
clearInterval(intervalObject)
clearTimeout(timeoutObject)
console
exports
global
module
process
require()
setImmediate(callback[, ...args])
setInterval(callback, delay[, ...args])
setTimeout(callback, delay[, ...args])



---

formidable 上传包

https://www.npmjs.com/package/formidable

```
const formidable = require('formidable');
let form = new formidable.IncomingForm();

form.encoding = 'utf-8';
form.uploadDir = "/uploadFile";
form.keepExtensions = true;


form.maxFieldsSize = 2*1024*1024; //2MB
form.maxFields = 1000;  //分段 0 = unlimited(无限)

form.hash=false; //上传文件的校验码 sha1 or md5
form.multiples=false; //是否支持多文件上传


// read

form.bytesReceived; //接收字节数
form.type;  //文件类型 mime
form.bytesExpected; //返回将要接收的表单数据大小

//form.parse(request,(err,fields,files)=>{ 
    console.log(JSON.stringify({fields:fields,fiels}))
})// parse upload file info


form.on('field')


```



### process 

global.process Nodejs进程相关信息，无需require() 就可引用

1. 事件
   - disconnect 
   - exit 
   - message 
   - rejectionHandled    拒绝处理事件
   - uncaughtException  未捕获的异常
   - unhandledRejection 事件
   - warning 事件

```javascript
process.on('unhandleRejection,(reason,p)=>{
    console.log('未处理的 rejection:',p,'原因：',reason);
})
process.on('waring',(warning)=>{
    console.warn(warning.message);
    console.warn(warning.name);
    console.warn(warning.stack);
})
```



1.  process.config

   > 属性返回一个javascript对象，此对象描述了用于编译当前Node.js执行程序时涉及的配置项信息

2. process.connected

   > 如果Node.js进程是由 IPC channel方式创建的

3. process.cpuUsage()

4. process.cwd()

5. process.disconnect()

6. process.emitWarning()

7. process.env  用户环境信息对象

8. process.execPath

9. process.exit([code]);  /终止进程

10. process.exitCode

11. process.getegid()    //方法返回Node.js进程的有效数字标记的组ID

12. process.kill(pid)

13. process.mainModule

14. process.memoryUsage()

15. process.pid   //进程id

16. process.platform    //平台标识

17. process.send(message)




---

**Buffer**：缓冲（二进制在内存中的形式，可以按照stream的形式传递到其它对象中） 、

**Stream** ：是数据传输对象，如果需要在传输过程中对数据进行处理，则需要处理流数据，如果把文件比做装数据的容器，那流是容器间数据传输的一个过程，流传输的对象就是Buffer数据

**fs** : 文件操作对象，文件在硬盘中的形式，读取数据会放入Buffer 才能对数据进行操作，写入数据前数据也要先放入Buffer对象中再写入文件中，fs读写文件时，数据是按流Stream形式进行传递的

---

### fs 

```
fs.readFileSync();  
fs.exists(fs,callback(err,stats:boolean));
fs.stat(path,callback(err,stats:object));
fs.open(path,flags[mode],callback(err,fd));   // {mode:[r,r+,rs+,w,wx,w+,a,ax,a+,ax+]});
fs.read(fd,buffer,offset,length,position,callback(err,readByte));
fs.write(fd, buffer, offset, length[, position], callback(err,readByte))
fs.close(fd,callback(err))
fs.unlink(path,callback);
fs.readdir(path,callback(err,files));
fs.mkdir(path[,mode],callback(err));
fs.rmdir(path,callback(err));
```



# path

```
normalize(); 文件路径处理规范化路径字符串
path.join([path1],[,path2],[,...]); 路径连接
path.resolve([from...],to);  //将多个路径解析为一个规范化的路径
path.relative(from,to); //查找两个绝对路径的相对关系
path.dirname();
path.basename();
path.extname();

```





# EventEmitter

事件驱动IO, Events是Nodejs的核心模块之一，许多模块都继承自Event

会有一个事件发射器及一个或多个事件监听器，事件发射器可以发射事件对象

```
let http = require('http');
let server = http.createServer();
server.on('request',function(req,res){
    res.writeHead(200,{'Content-type':'text/plain'});
    res.end('hello world');
}).listen(3000);
```



# querystring

- querystring.escape(str);
- querystring.parse(str[,sep[,eq[,options]]])
- querystring.stringify(obj[,sep[,eq[,options]]])
- querystring.unescape(str)