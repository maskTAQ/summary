1. 根元素并不是html那样的html,而是body,所以如果设置全屏显示的时候需将根容器page设置高度为100%。
2. text渲染成span元素,对于行高有着不正确的处理[改为view包裹]。
3. scroll-view组件必须之定义个固定的px高度值[rpx无效,百分百无效],可以通过wx.getSystemInfo获取windowHeight动态计算高度。?不同端显示效果不一样下拉刷新失效
4. 1rpx在dpi高的设备中显示不出来用px替代。
5. 属性名不支持大写所以驼峰写法失效。
5. 页面内方法定义的闭包小程序初始化的时候定义,并不在onload是定义
6. 小程序内最多只能存在一个socket连接,据官方文档`如果当前已存在一个 WebSocket 连接，会自动关闭该连接，并重新创建一个 WebSocket 连接。`,
在实际中重新连接同一个socket地址,并不会触发`wx.onSocketClose(CALLBACK)`。
7. websocket监听句柄一直存在于小程序的存在周期中,并不会因为卸载页面而卸载掉此页面监听句柄

## 关于data的问题
当一个页面卸载后,一般情况下是用不到此页面的data数据了,如果像此前说的websocket回调句柄触发了那么卸载之后的data是什么了?初始值还是卸载前的值。经过测试时卸载前的值。