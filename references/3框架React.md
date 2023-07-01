============================== React16.8- ==============================
Component
context
props
refs
state

# ES5原生组件
React.createClass({
  getInitialState() { return {} }
  getDefaultProps() { return {} }
  propTypes: {}
})

# ES6类组件
constructor() { this.state = {} }
static defaultProps = {}
static propTypes = {}

# ES6函数组件

static childContextTypes
static contextTypes
static contextType
static defaultProps 相当于React.createClass中的getDefaultProps()
static propTypes
static getDerivedStateFromError(error)
static getDerivedStateFromProps(props, state)


# 生命周期的3个过程
## 单一组件
挂载mount
  constructor(props)
    getInitialState()
  defaultProps
  UNSAFE_componentWillMount()
  render()
  componentDidMount()
更新update
  UNSAFE_componentWillReceiveProps(nextProps, nextContext)
  shouldComponentUpdate(nextProps, nextState, nextContext)
  UNSAFE_componentWillUpdate(nextProps, nextState)
  componentDidUpdate(prevProps, prevState, snapshot?)
卸载unmount
  componentWillUnmount()

## 父子组件
挂载mount
  父组件 constructor UNSAFE_componentWillMount render
  子组件 constructor UNSAFE_componentWillMount render componentDidMount
  父组件 componentDidMount
父组件更新update state
  父组件 shouldComponentUpdate(强制放行) UNSAFE_componentWillUpdate render
  子组件 UNSAFE_componentWillReceiveProps shouldComponentUpdate(返回false)
  父组件 componentDidUpdate
子组件更新update state
  子组件 shouldComponentUpdate(强制放行) UNSAFE_componentWillUpdate render componentDidUpdate
父传子update props
  父组件 shouldComponentUpdate UNSAFE_componentWillUpdate render
  子组件 UNSAFE_componentWillReceiveProps shouldComponentUpdate UNSAFE_componentWillUpdate render componentDidUpdate
  父组件 componentDidUpdate
子传父update callback
  父组件 shouldComponentUpdate UNSAFE_componentWillUpdate render
  子组件 UNSAFE_componentWillReceiveProps shouldComponentUpdate UNSAFE_componentWillUpdate render componentDidUpdate
  父组件 componentDidUpdate
卸载unmount
  父组件 componentWillUnmount
  子组件 componentWillUnmount



  componentDidCatch(error, info)

  forceUpdate(callback?)
  getChildContext()
  getSnapshotBeforeUpdate(prevProps, prevState)
  setState(nextState, callback?)
  getDerivedStateFromProps(props, state)
  getDerivedStateFromError(error)

PureComponent 纯粹的组件：界面完全由props和state决定
immutable 不可变数据结构：对于引用类型数据，不修改原值，而是复制后修改并返回新值 Object.assign({}, data, {...})

竞态

相比于类组件，React没有提供一个更简单、聪明、轻量级的原生添加状态和生命周期

# 虚拟DOM
用JS对象表示DOM结构，即React.createElement()返回的结果
  createElement() -> render(tree)得到rootTree
JS对象通过diff算法比较新老虚拟DOM的差异
  diff(oldTree, newTree) -> 得到差异对象patches
批量、异步、最小化的执行DOM变更，而不用全局更新
  patch(rootTree, patches) -> 把patches应用到rootTree节点上

diff算法时间复杂度：同层元素对比O(n)，完全对比O(n^3)

reconciler协调：使用react-dom等模块与真实DOM同步的过程

fiber树：存放组件树的相关信息，在更新时可以增量渲染相关DOM

性能对比：
innerHTML = 渲染html字符串O(字符串大小) + 重新创建所有的DOM元素O(DOM大小)
Virtual DOM = 渲染虚拟DOM O(DOM大小) + diff O(字符串大小) + 必要的DOM更新O(DOM差异)
也就是说：重建所有DOM元素的消耗 > diff + patch

优势在于：
跨平台，比如：Web、Native、Electron
减少页面的重绘回流

diff算法：
replace
text, props
reorder
同层对比，时间复杂度O(n)~O(nmlogm)
最小步数完成位移
  React 仅右移
  Vue 先左右夹击跳过不变的，再找到最长连续子串，保持不动，移动其它元素

JSX支持跨平台


性能差在哪里？


============================== React16.8+ ==============================
# Hook
原理

# 常用的hook
传感器Sensors
  useIdle
  useLocation
  useSearchParam
用户界面UI
动画Animations
  useInterval
  useTimeout
副作用Side-effects
  useAsync
  useCookie
  useDebounce
  useLocalStorage
  useThrottle
生命周期Lifecycles
  useEffect(cb, deps) 处理副作用和生命周期方法
状态State
  createMemo
  createReducer
  useObservable
  useState 创建保存更新state





============================== React-Router ==============================
children 是以<Outlet />插槽占位符的形式加载到父级页面的局部
  默认渲染path为''的一组

============================== Redux ==============================
组件之间的通信方式
props
context
Redux


React16.8之前 redux
  <react-redux.Provider store>
  store = redux.createStore(reducer, preloadedState, redux.applyMiddleware(arr))
  reducer = redux.combineReducers({ subReducers })
  subReducers 纯函数：接收action和旧的state，经过处理，返回新的state
  action 处理副作用
  react-redux.connect(mapStateToProps, mapDispatchToProps)(component)
    mapStateToProps 将特定state映射为props
    mapDispatchToProps 将dispatch(特定action)映射为props
  component 通过props获取state和dispatch(action)更新视图

React16.8之后 RTK @reduxjs/toolkit
  <react-redux.Provider store>
  store = @reduxjs/toolkit.configureStore(reducer, middleware)
  const slice = createSlice(name, initialState, reducers, extraReducers)
    name 对外访问特定state时的名称
    initialState 初始化特定state
    reducers 纯函数，对外暴露为actions
    extraReducers 处理副作用，也对外暴露
      createAsyncThunk 创建异步thunk 不能重名
  component 通过react-redux.useSelector和react-redux.useDispatch获取state和dispatch
    通过dispatch(action)更新视图
  【优化：1.action和子reducers合并到slice中，2.在component中获取state和dispatch，触发更新视图】

中间件
  redux-thunk
  redux-logger
  saga

持久化 Redux-persist

============================== SSR ==============================


============================== Next ==============================


============================== AntDesign==============================

