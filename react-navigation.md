# React Navigation
路由的跳转方法push内部没有处理路由栈是否依旧存在当前的路由，在存在的情况下push之前的相同路由并不会被卸载，还会造成相同的路由再次挂载，
可以改变路由state中的路由索引index来实现重复路由跳转，来实现刚刚说明的问题
```javascript
const navReducer = (state = initialState, action) => {
  //解决路由栈中存在相同路由 依旧push的问题
      const { routes } = state;
      for (let i = 0; i < routes.length; i++) {
        const { routeName } = routes[i];
        if (routeName === nextRouteName) {
          //改变路由栈中当前激活路由的索引 带上路由的参数
          routes[i].params = action.payload.params;
          return Object.assign({}, state, {
            index: i,
            params: action.payload.params
          });
        }
      }
};
```