 formidable    文件上传包   

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







