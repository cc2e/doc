

### NPM 上传包 

1. ```
   npm init  //先编写package.json 文件
   ```


2. 创建一个 README.md的说明文件

3. 在根中运行指令

   ```shell
   npm link
   ```

4. ```shell
   执行完上一步会生成一个 node_modules／ 目录，我们将该目录排除
   echo node_modules/ >> .gitignore
   ```

5. ```shell
   npm adduser  //添加用户  https://www.npmjs.com  在这里注册的帐号
   ```

6. ```shell
   npm publish   //发布
   ```

   > 注意 如果你的镜像地址是 用的 taobao(只读）的那请更改为 默认地址否则无法发布包
   >
   >  淘宝镜像
   >
   > 　 npm config set registry http://registry.npm.taobao.org/
   >
   > 默认镜像
   >
   > 　 npm config set registry https://registry.npmjs.org/



7. 常见的问题就是403 error ，1是你发的包名和线上的有重复，2回复你的邮箱验证

8. 以后每发一版 需要更新 package.json中的 version

9. ```
   npm who am i  查看当前登录帐号
   ```

   ​