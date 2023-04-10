keep-alive 是 Vue 提供的一个内置组件，用来对组件进行缓存，在组件切换过程中将状态保留在内存中，防止重复渲染 DOM。 如果为一个组件包裹了 keep-alive，那么它会多出两个生命周期：deactivated、activated。同时，beforeDestroy 和 destroyed 就不会再被触发了，因为组件不会被真正销毁。 当组件被换掉时，会被缓存到内存中、触发 deactivated 生命周期； 当组件被切回来时，再去缓存里找这个组件、触发 activated 钩子函数。

参考[keep-alive](https://github.com/answershuto/learnVue/blob/master/docs/%E8%81%8A%E8%81%8Akeep-alive%E7%BB%84%E4%BB%B6%E7%9A%84%E4%BD%BF%E7%94%A8%E5%8F%8A%E5%85%B6%E5%AE%9E%E7%8E%B0%E5%8E%9F%E7%90%86.MarkDown)
参考[官网](https://cn.vuejs.org/guide/built-ins/keep-alive.html)