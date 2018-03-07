# React 

1. npm install -g create-react-app


2. create-react-app  my-react
   - yarn start
   - yarn build
   - yarn test
   - yarn eject
3.  cd  my-react
4. yarn add webpack webpack-dev-server path






React Lifecycle

> 组件本身就是一种状态机，输入 和输出一定确定，状态发生转换时触发不同的钩子函数，从而让开发者有机会做出响应



###  状态机： 初始化 ->运行时->销毁

##### 初始化时的钩子

1. getDefaultProps   (once,实例共享引用)

2. getInitialState   （初始化state）

3. componentWillMount  （可修改state）

4. render  ：(只能访问this.props,this.state,不允许修改state 和 DOM输出)

5. componentDidMount  (可以个修改 dom)

   ​

##### 运行中的钩子

1.  componentWillReceiveProps (将要接收更新)
2. shouldComponentUpdate  (手动触发是否需要更新)
3. componentWillUpdate  （将要更新）
4. render   （更新中）
5. componentDidUpdate （更新完毕）

##### 销毁

1. componentWillUnmount











- 知识点

```
class Square extends React.Component{
    constructor(){  
   		 super();   //子类构造 函数，要显示调用super()
	}
	render(){
        return (
        	<button className="square" onClick={()=>alert('click')}>
        		{this.props.value}
        	</button>
        );
	}
}

```














