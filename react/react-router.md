## 首先在react项目下装一个包 npm install react-router-dom --save

## 函数式创建组件  
可以直接收到一个参数props
  ```
  import React from 'react';
  import ReactDOM from 'react-dom';
  function App(props){
    console.log(props)
    return(
      <div>
        adds
      </div>
    )
  }

  ReactDOM.render(<App title='sdadsa'/>,document.getElementById('root'));

  ```
  下边把props解构赋值了一下

```
import React from 'react';
import ReactDOM from 'react-dom';
function App({title}){
  console.log(title)
  return(
    <div>
      adds
    </div>
  )
}

ReactDOM.render(<App title='sdadsa'/>,document.getElementById('root'));

```
###  小例子  
```
import React from 'react';
import {BrowserRouter as Router,Route,Link} from 'react-router-dom'
import About from './components/About.js';
import Home from './components/Home.js';
const Work = ()=>
  (
  <div>
    我是work
  </div>
  )

class App extends React.Component{
  render(){
    return (
      <Router>
        <div>
          <h1>欢迎光临</h1>
          <Link to='/'>首页</Link><br/>
          <Link to='/about'>about首页</Link><br/>
          <Link to='/work'>work</Link>

          <Route exact path='/' component={Home}/>
          <Route path='/about' component={About}/>
          <Route path='/work' component={Work}/>

        </div>
      </Router>
    )
  }
}
export default App

```
## 路由地址嵌入变量   
就是加个冒号
输入work下任意地址都能访问到Work组件了,冒号后面可以用任意名字.

```
  <Route path='/work/:work' component={Work}/>

```

## 路由的嵌套  
```
import React from 'react';
import {Route,Link} from 'react-router-dom'
const Dj=()=>(
  <h3>迪加</h3>
)
const Niu=()=>(
  <h3>牛老师</h3>
)
const Zhang=()=>(
  <h3>张老师</h3>
)
class About extends React.Component{
  constructor(props){
    super(props)
    console.log(props)
  }
  render(){
    let {match}=this.props
    return (
      <div>
        <h2>关于</h2>
        <Link to={`${match.url}`}>迪加</Link>
        <Link to={`${match.url}/zhang`}>张</Link>
        <Link to={`${match.url}/niu`}>牛</Link>

        <Route exact path={`${match.url}`} component={Dj}/>
        <Route path={`${match.url}/zhang`} component={Zhang}/>
        <Route path={`${match.url}/niu`} component={Niu}/>

      </div>
    )
  }
}
export default About

```


##  组件重定向  

```
import {BrowserRouter as Router,Route,Link,Redirect} from 'react-router-dom'
<Route path='/new' component={New}/>
<Redirect from='/old' to='/new'/>

```

##  Switch   
从上往下找 找到一个符合的就不往下找了 ,只会挂载一个  以前的话所有都挂载上
```
return (
  <Router>
    <div>
      <h1>欢迎光临</h1>
      <Link to='/'>首页</Link><br/>
      <Link to='/about'>about首页</Link><br/>
      <Link to='/work/55'>work</Link>
      <Link to='/ne'>old</Link>
      <Switch>
        <Route exact path='/' component={Home}/>
        <Route path='/about' component={About}/>
        <Route path='/about' component={About}/>

        <Route path='/work/:work' component={Work}/>
        <Route path='/new' component={New}/>
        <Redirect from='/old' to='/new'/>
      </Switch>
      版权所有
    </div>
  </Router>
)

```

## 404页面  
```
  <Notefinde component={Notefinde}/>
  //不写path  所有地址都能匹配到
  <Switch>
    <Route exact path='/' component={Home}/>
    <Route path='/about' component={About}/>
    <Route path='/about' component={About}/>

    <Route path='/work/:work' component={Work}/>
    <Route path='/new' component={New}/>
    <Notefinde component={Notefinde}/>
    <Redirect from='/old' to='/new'/>
  </Switch>
```

## NavLink  
```
<h1>欢迎光临</h1>
<NavLink exact activeClassName='nav' to='/'>首页</NavLink >
<NavLink  activeClassName='nav' to='/about'>about</NavLink >
<NavLink  activeClassName='nav' to='/work/55'>work</NavLink >
<NavLink  activeClassName='nav' to='/new'>old</NavLink >
<Switch>

```
用于给导航栏起class
默认的class名是active


##  用render挂载组件;  
```
    <Route path='/about' render={ props => this.state.admin ? <About{...props}/> : <Redirect to='/'/>}/>

```

##  porps 下的history

```
handleClick(){
  // this.props.history.goBack()//往回退一步
  // this.props.history.go(-2)//往回退两部
  this.props.history.goForward() //往前一部
}
```
## 组件下的组件传 porps  
```
import { withRouter } from 'react-router'

export default withRouter(MyComponent)

```
##  HashRouter 和 BrowserRouter
前者 不需要服务器支持 通过#(锚点) 一直返回同一个index.html
后者需要服务器支持   公司一般用后者   服务器就像一台电脑linux电脑  只有命令行
