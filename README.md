<<<<<<< HEAD
# redux
redux入门
=======
# redux使用说明书

**对比于vue中的vuex**

1. vuex是为vue框架量身定制的，内部封装了方法，使得用起来简单
2. redux不是还专门为react产生的，在很多场景只要你想用就可以使用，比较灵活，使用场景多

## redux初级使用

1. 安装redux

   ```
   yard add redux --save
   ```

2. 创建**reducer**用来处理store仓库中的数据

   ```
   const counter = (state= 0,action) =>{ 
   // 接受两个参数，第一个是state,也就是初始化redux仓库数据，第二个是 动作 action，表示处理哪种操作
       switch(action.type){
           case "INCREMENT":
               console.log("执行+操作");
               return state + 1;
           case "DECREMENT":
               return state - 1;
           default:
               return state
       }
   }
   export default counter
   ```

3. 创建一个store

   ```
   import {createStore} from 'redux'
   import reduxer from '***' // 导入reducer
   const store = createStore(reduxer)
   ```

4.  在页面中使用，通过方法来进行派发 dispatch

   ```
   const decrementFn = () => {
   	store.dispatch({type；'INCREMENT'})
      	// store.dispatch(decrement()) 
      	// 或者创建一个action.js用来到处要处理的dispath操作
   }
   ```

5. 发现更改store中的数据后，页面内容没有改变，我们就需要 subscribe来发现store数据改变

   ```
   store.subScribe(()=>{
   	// store.getState()用来获取store中state数据
   	setCount(store.getState())
   })
   ```

## redux高级使用

1. 安装react-redux

   ```
   yard add react-redux --save
   ```

2. 创建一个store仓库

   ```
   import {createStore} from 'redux'
   
   import Reducer from './reducer/count'
   
   // 创建 store 对象
   const store = createStore(Reducer)
   
   export default store
   ```

3. 在最根级组件引入 provider和store包裹着所有组件

   ```
   import {provider}from 'react-redux' 
   // 将store数据传给provider,这样在所有组件都可以通过props.state来接收数据
   ReactDOM.render(
     <Provider store={store}>
       <Router />
     </Provider>,
     document.getElementById('root')
   );
   ```

4. 搞清楚派发者，和接收者

   ```
   // 如果一个组件要派发数据到 store 仓库中 那么就需要 mapDispatchToProps，
   // 如果一个组件要进行接收数据从store仓库中  那么需要 mapStateToProps
   // 通过connect连接仓库和组件
   import {connect } from 'react-redux'
   const mapStateToProps = state =>{
       return {state}
   }
   const mapDispatchToProps = dispatch =>{
       return {
           increment: ()=>{
               dispatch({ // 此处的dispatch也可以从action里面引入
                   type: 'INCREMENT'
               })
           },
           decrement:()=>{
               dispatch({
                   type: 'DECREMENT'
               })
           }
       }
   }
   export default connect(mapStateToProps,mapDispatchToProps)(Home)
   // mapStateToProps 要在 mapDispatchToProps 之前
   ```

个人推荐比较好的redux视频教学 [b站](https://www.bilibili.com/video/BV1oE411V7RW)
>>>>>>> 396ab0a (redux)
