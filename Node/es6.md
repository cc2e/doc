### 解构赋值 

```javascript
var [a,b,c]=[1,2,3];
let [,,d]=['foo','too','ccc']
let [kkk,...a] = [1,3,4,5,6]
//kkk  1
//a  [3,4,5,6]

let [x,y,...z] =['a']
//x  a
//y  undefined
//z  []

let [ a,b]=[111]
//a = 111
//b = undefined

var map = new Map()
map.set('我是key','hello')
map.set('我是key2','world')
for(let [key,value] of map){
    
}




```



**==知识点==**

for... in  和 for...of的区别 

for...in 可以遍历数组和对象 (能获取数组的index, 能得到对象的key)

for...of 可以遍历数组 和 带有iterator接口的对象如map (能得到数组的值，iterator对象的 key和value)





**遍历对象属性的6种方法**

1. for...in   （不含symbol 属性 和可枚举的）
2. Object.keys(obj)  返回一个数组（所有可枚举的属性，不含symbol)
3. Object.getOwnPropertyName(obj) 返加一个数组，包含对象自身的属性 与上2个一致
4. Object.getOwnPropertySymbols(obj) 返加一个数组，只包含symbol属性
5. Reflect.ownKeys(obj)   利用反射 返回对象的所有属性不区分类型