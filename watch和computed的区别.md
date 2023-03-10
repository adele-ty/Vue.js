## watch
侦听属性用于观察和响应数据的变化。当侦听属性所依赖的数据发生变化时，它会执行相应的回调函数。在使用侦听属性时，我们需要在实例中定义一个回调函数，当依赖的数据发生变化时，这个回调函数会被自动执行。在回调函数中，我们可以执行任意的操作，例如发送网络请求、更新其他数据等。
* 深层侦听器  
watch 默认是浅层的：被侦听的属性，仅在被赋新值时，才会触发回调函数——而嵌套属性的变化不会触发。如果想侦听所有嵌套的变更，你需要深层侦听器：deep: true; 深度监听开销很大，使用时注意性能。
* 即时回调  
仅当数据源变化时，才会执行回调。但在某些场景中，我们希望在创建侦听器时，立即执行一遍回调。可以开启即时回调immediate: true; 回调函数的初次执行就发生在 created 钩子之前。Vue 此时已经处理了 data、computed 和 methods 选项，所以这些属性在第一次调用时就是可用的。
* 回调的触发时机  
默认情况下，用户创建的侦听器回调，都会在 Vue 组件更新之前被调用。这意味着你在侦听器回调中访问的 DOM 将是被 Vue 更新之前的状态。如果想在侦听器回调中能访问被 Vue 更新之后的 DOM，你需要指明 flush: 'post' 选项。
## computed
计算属性会根据一个或多个依赖进行计算，并返回计算结果，计算属性的值是根据它所依赖的数据动态计算得到的。计算属性通常用于处理复杂的逻辑，例如从多个数据源计算出一个结果。当数据源发生变化时，计算属性会自动重新计算。计算属性可以使用缓存，如果计算属性依赖的数据没有发生变化，那么它会直接返回缓存的计算结果，避免不必要的计算。  
相比之下，methods调用总是会在重新渲染发生时再次执行函数。