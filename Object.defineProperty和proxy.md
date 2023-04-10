# 为什么 Vue3 用 proxy 代替了 Vue2 中的 Object.defineProperty?
### Vue2 中使用 Object.defineProperty 实现数据劫持，其主要缺点包括：
* 只能劫持对象的属性，无法劫持数组等数据类型。  
* 需要遍历对象的所有属性，对于大型对象来说，遍历的开销较大，性能较低。  
* 需要在对象初始化时对属性进行劫持，无法劫持后添加的属性。  

下面是简单的示例代码：
```c
const obj = {}
for (let i = 0; i < 100000; i++) {
  obj[`prop${i}`] = i
}

for (let prop in obj) {
  Object.defineProperty(obj, prop, {
    get() {
      return obj[prop]
    },
    set(value) {
      obj[prop] = value
    }
  })
}
```
在上面的代码中，我们创建了一个包含 100000 个属性的对象 obj，并使用 for-in 循环遍历对象的所有属性，并使用 Object.defineProperty 对每个属性进行劫持。对于大型对象来说，遍历的开销较大，性能较低。  

为了解决这些问题，Vue3 中采用了 Proxy 对象来实现数据劫持。Proxy 对象是 ES6 中新增的一个特性，可以对整个对象进行劫持，而不仅仅是对象的属性。与 Object.defineProperty 不同的是，Proxy 对象可以在对象初始化后添加新的属性，而且可以监听数组的变化。
### Vue3 中使用 Proxy 对象的主要优点包括：
* 劫持整个对象，而不仅仅是对象的属性，可以监听数组的变化。  
* 可以在对象初始化后添加新的属性，而不必在初始化时对属性进行劫持。  
* 性能更好，因为 Proxy 对象只会在访问对象属性时才被触发，而不必遍历对象的所有属性。  

下面是一个简单的示例代码：
```c
const obj = {
  name: 'Alice',
  age: 18,
  gender: 'female'
}

const proxy = new Proxy(obj, {
  get(target, key) {
    console.log(`get ${key}`)
    return target[key]
  },
  set(target, key, value) {
    console.log(`set ${key}=${value}`)
    target[key] = value
  }
})

proxy.name  // 访问对象属性时触发 get 拦截器，打印 "get name"
proxy.age   // 访问对象属性时触发 get 拦截器，打印 "get age"
proxy.gender  // 访问对象属性时触发 get 拦截器，打印 "get gender"
```
从这个示例代码中可以看出，Proxy 对象只会在访问对象属性时才被触发，而不必遍历对象的所有属性。这样做的好处是，可以大大提高数据劫持的性能，避免不必要的操作。