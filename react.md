# react总结

## 业务组件剥离
一个页面有很多个部件[也可以理解为块]构成,每当`setstate`时,无需更新的部件也会引发重新渲染,这完全是不需要的。所以可以将页面每一块分离成组件[这里的组件是更具体的业务组件],所有的组件共享一个页面的state,组件内部通过`shouldComponentUpdate`来与上一个`state`对比,来决定自己是否更新,避免不必要的性能消耗,提升用户体验。

## 生命周期[参考](http://www.jianshu.com/p/4784216b8194)
更好的使用react必须了解它的生命周期,以便知道你该在什么时候干什么事。

1. 组件初始化 `constructor[设置初始化props、state] -> componentWillMount -> render -> componentDidMount`。
2. setState `shouldComponentUpdate -> componentWillUpdate -> render -> componentDidUpdate`。这里只有`shouldComponentUpdate`返回true或者调用forceUpdate才会执行后续步骤。
3. 父组件调用render时 `componentWillReceiveProps -> shouldComponentUpdate -> componentWillUpdate -> render -> componentDidUpdate`。这里只有`shouldComponentUpdate`返回true或者调用forceUpdate才会执行后续步骤。
4. forceUpdate `componentWillUpdate -> render -> componentDidUpdate`。
5. 卸载组件[可以这样 React.unmountComponentAtNode ] `componentWillUnmount`。

禁止在render、componentWillUpdate 中修改props、state。
