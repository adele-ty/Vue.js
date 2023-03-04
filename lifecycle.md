## beforeCreate & created
beforeCreate 和 created 函数都是在实例化 Vue 的阶段。beforeCreate 和 created 的钩子调用是在 initState 的前后，initState 的作用是初始化 props、data、methods、watch、computed 等属性，那么显然 beforeCreate 的钩子函数中响应式的数据和方法都未初始化，就不能获取到 props、data 中定义的值，也不能调用 methods 中定义的函数。在created中实例的响应式数据和方法已经初始化，但尚未挂载到DOM上。
## beforeMount & mounted
在执行 vm._render() 函数渲染 VNode 之前，执行了 beforeMount 钩子函数，在执行完 vm._update() 把 VNode patch 到真实 DOM 后，执行 mounted 钩子。beforeMount 和 mounted 分别在 DOM 挂载前后执行，在对于同步渲染的子组件而言，mounted 钩子函数的执行顺序是先子后父。
## beforeUpdate & updated
beforeUpdate 和 updated 的钩子函数执行时机都是在数据更新的时候，当视图中的数据发生变化，beforeUpdate 就会执行，之后 updated 随即进行，DOM 节点更新。
## beforeDestory & destoryed
beforeDestroy 和 destroyed 钩子函数的执行时机在组件销毁的阶段。beforeDestroy 钩子函数的执行时机是在 $destroy 函数执行最开始的地方，接着执行了一系列的销毁动作，包括从 parent 的 $children 中删掉自身，删除 watcher，当前渲染的 VNode 执行销毁钩子函数等，执行完毕后再调用 destroyed 钩子函数。beforeDestory 在Vue实例销毁之前调用，此时实例仍然可以访问。destoryed 在Vue实例销毁之后调用，此时实例和DOM元素都已经被销毁，无法再访问。  

这些钩子函数可以让我们在组件的不同生命周期阶段执行自定义操作。例如，可以在created钩子函数中进行组件数据的初始化，或者在mounted钩子函数中进行DOM操作。在beforeDestroy钩子函数中可以清除定时器、取消事件监听器等资源，以避免内存泄漏。通过钩子函数，我们可以更好地掌握组件的生命周期，更好地管理组件的状态，从而提高组件的性能和可维护性。

详细请参考[Vue.js生命周期](https://ustbhuangyi.github.io/vue-analysis/v2/components/lifecycle.html#beforecreate-created)