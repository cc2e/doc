# Experience

微信视频全屏方式 

```
<video
  id="videoALL" 
  src="video/01.mp4" 
  poster="images/1.jpg" /*视频封面*/
  preload="auto" 
  webkit-playsinline="true" /*这个属性是ios 10中设置可以
                     让视频在小窗内播放，也就是不是全屏播放*/  
  playsinline="true"  /*IOS微信浏览器支持小窗内播放*/ 
  x-webkit-airplay="allow" 
  x5-video-player-type="h5"  /*启用H5播放器,是wechat安卓版特性*/
  x5-video-player-fullscreen="true" /*全屏设置，
                     设置为 true 是防止横屏*/>
  x5-video-orientation="portraint" /*播放器支付的方向，
                     landscape横屏，portraint竖屏，默认值为竖屏*/
  style="object-fit:fill">
</video>
```


- sass install for mac

```ruby
gem list    
gem souce -a  https://ruby.taobao.org
gem source -l 
sudo gem install sass

which sass   // /usr/local/bin/sass    sass安装目录

webstorm ->preferences -> file Watchers >  Program:/usr/local/bin/sass


vue 配置
npm i --save-dev  sass-node  sass-loader
//不安装无法配置
npm i ;
```





- element全屏显示API

```js
element.webkitRequestFullscreen();
element.requestFullscreen()

```



---

# [切图相关]

```html
<meta name="viewport" content="width=device-width,initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">

<meta name="viewport" content="target-densitydpi=device-dpi" /> 
//像素比标识[device-dpi,high-dpi,medium-dpi,low-dpi]

<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1"> 

<!--搜索引擎-->
<meta name="applicable-device" content="mobile"> 
<meta name="applicable-device" content="pc">

<!--缓存-->
<meta http-equiv="Expires" CONTENT="0">
<meta http-equiv="Cache-Control" CONTENT="no-cache">
<meta http-equiv="Cache-Control" CONTENT="no-store">
<meta http-equiv='Cache-Control' content=''>
<!--跳转-->
<meta http-equiv="refresh" content="0:url=https://gitee.com/ssvnet">


<meta name="format-detection" content="telephone=no">    //不识别电话号码
<meta name="apple-mobile-web-app-capable" content="no" >   //不识别电话号


<!--私有模式-->
<!-- QQbrowser mobile-->
<meta name="x5-orientation"content="portrait｜landscape">        //强制 肖像 风景模式
<meta name='x5-fullscreen' content='true'>                       //fullpage
<meta name='x5-page-mode' content='app'>           //appmodel

<!--uc browser-->
<meta name='full-screen' content='yes'>    //uc  全屏显示
<meta name='viewport' content='uc-fitscreen=no|yes'>              //UC 缩放不出滚动条
<meta name="screen-orientation"content="portrait | landscape">   //uc 强制竖屏或横屏
<meta name='layoutmode' content='fitscreen｜standard'>   //uc 排版模式  简化版  和   标准版
<meta name='nightmode' content='enable｜disable'>    //UC 夜间模式
<meta name='browsermode' content='application'>        //应用模式 禁止长按菜单 手势 默认全屏
<meta name='imagemode' content='force'>   //隐藏所有 图片  省流量版


```



- 常用字体

```

"Microsoft YaHei",'Hiragino Sans GB','SimHei','Helvetica',sans-serif,Arial;

hiragino sans gb,microsoft yahei,simsun;

arial,"Hiragino Sans GB","Hiragino Sans GB W3",Sim Sun;   


```





- 清除浮动防止高度塌陷

```
IE8 不支持 after

.clearfix:after{
    display:block;
    clear:both;
    content:'';
    visibility:hidden;
    height:0
}

```



- 盒模型 

```scss
box-sizing:border-box; //元素宽高不变的情况下 渲染内容的宽高
box-szing:content-box; //内容的宽高会影响元素的宽高

.box{ 
	display:-webkit-box;
    -webkit-box-orient:[horizontal|vertical]
 	-webkit-box-direction:[normal|reverse|inherit]  //
    -webkit-box-align:[start|end|center|baseline|stretch]  ／／Y轴
    -webkit-box-pack:[start|end|center|justify]  ／／X轴
    
    .child{
		-webkit-box-flex:1  //子元素比例
    }
}





.flex{
   display:flex;
    // 主轴对齐 X轴   
   justify-content:[flex-start|flex-end|center|space-between|space-around] 
   
   // Y轴对齐属性
   align-items:[flex-start|flex-end|center|baseline|stretch]
   
   // 一组元素时（多行）  定义组元素Y轴所在位置 （单行元素时无效）
   align-content:[flex-start|flex-end|center|space-between|space-around|stretch]
    
    .child{
    	order:1; //html排序 0~N  ,越小越在靠前
        flex-grow:1;    //等分空间比例，子项目的放大比例默认为0,空间足够就放大
        flex-shrink:1   //子项目的缩小比例，flex-shrink:0:视为不缩小
        flex-basis:200px;   //固定空间写法默认auto
        flex:[flex-grow|flex-shrink|flex-basis]  //简写 flex:1 0 auto
        
        //inherit父，可覆盖父样式 
        align-self:[auto|flex-start|flex-end|center|baseline|stretch] 
        
            
            
    }
 }
   
```



