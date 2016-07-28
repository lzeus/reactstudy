## 组件生命周期
### 组件的生命周期包含三个主要部分：

1. 挂载： 组件被插入到DOM中。
2. 更新： 组件被重新渲染，查明DOM是否应该刷新。
3. 移除： 组件从DOM中移除。

React提供生命周期方法，你可以在这些方法中放入自己的代码。

我们提供will方法，会在某些行为发生之前调用，和did方法，会在某些行为发生之后调用。

#### 挂载
getInitialState(): object在组件被挂载之前调用。状态化的组件应该实现这个方法，返回初始的state数据。

componentWillMount()在挂载发生之前立即被调用。

componentDidMount()在挂载结束之后马上被调用。需要DOM节点的初始化操作应该放在这里。

#### 更新
componentWillReceiveProps(object nextProps)当一个挂载的组件接收到新的props的时候被调用。

该方法应该用于比较this.props和nextProps，然后使用this.setState()来改变state。

shouldComponentUpdate(object nextProps, object nextState): boolean当组件做出是否要更新DOM的决定的时候被调用。

实现该函数，优化this.props和nextProps，以及this.state和nextState的比较，如果不需要React更新DOM，则返回false。


componentWillUpdate(object nextProps, object nextState)在更新发生之前被调用。你可以在这里调用this.setState()。


componentDidUpdate(object prevProps, object prevState)在更新发生之后调用。

#### 移除
componentWillUnmount()在组件移除和销毁之前被调用。清理工作应该放在这里。


挂载的方法（Mounted Methods）
挂载的复合组件也支持如下方法：

findDOMNode(): DOMElement可以在任何挂载的组件上面调用，用于获取一个指向它的渲染DOM节点的引用。


forceUpdate()当你知道一些很深的组件state已经改变了的时候，可以在该组件上面调用，而不是使用this.setState()。

