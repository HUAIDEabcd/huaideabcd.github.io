---
title: Vue3.0其他
date: 2022-05-20 21:58:10
tags:
    Vue3
categories:
    Vue
---

## Vue3.0



## 1.支持多个根节点

vue3**template**内支持多个根节点

```HTML
<template>
   <div class="heade-box">
    公共头部
    </div>
    <div class='box'>
    内容区域
    </div>
</template>
```



## 2.组合API

在Vue3内，data数据和methods里的方法直接写在`setup`函数里，通过return抛出供给**template**使用

```js
 setup() {
    let num = 1
    return {
        num
    }
  },
```

`setup`可以接收2个参数：

**Props**：函数中的第一个参数是 `props`。 `props` 是响应式的，当传入新的 prop 时，它将被更新

**Context**：函数的第二个参数是 `context`。`context` 是一个普通的 JavaScript 对象，它包含了3个常用对象：

​		attrs：自定义属性

​		slots：插槽

​		emit：触发事件对象



执行 `setup` 时，组件实例尚未被创建。只能访问以下 选项：

- `props`
- `attrs`
- `slots`
- `emit`

可以访问以下组件选项：

- `data`
- `computed`
- `methods`

**在 `setup()` 内部，`this` 不是该活跃实例的引用**



## 3.响应式数据API

#### `reactive`

声明复杂类型数据为响应值数据

```js
const obj = reactive({
    count:1
})
obj.count++
console.log(obj.count) // 2
```

#### `isReactive`

检查对象是否是由 `reactive `创建的响应式代理

#### `toRaw`

将`reactive`类型的数组转为普通对象

#### `ref`

声明简单类型数据为响应值数据

```js
const count = ref(1)
count.value++
console.log(count.value) // 2
```

#### `toRef`

复制一个对象的引用，生成一个新的数据，但是新数据和原对象数据关联，修改会同步更改，但是不会引发页面更新

```js
setup(){
    let obj = {name : 'Tina', age : 18};
    let newObj= toRef(obj.name);
    function change(){
      newObj.value = 'Ace';//页面不会更新
      console.log(obj,newObj)
    }
    return {newObj,change}
  }
```

#### `toRefs`

接收一个对象作为参数，它会遍历对象身上的所有属性，然后挨个调用toRef执行

```js
setup(){
    let obj = {name : 'Tina', age : 18};
    let newObj= toRefs(obj);
    function change(){
      newObj.value = 'Ace';//页面不会更新
      console.log(obj,newObj)
    }
    return {newObj,change}
  }
```

#### `isRef`

检查值是否为一个 ref 对象



## 4.Computed

通过getter 函数返回的数据是一个不可更改地的响应式数据

```js
onst count = ref(1)
const plusOne = computed(() => count.value + 1)

console.log(plusOne.value) // 2

plusOne.value++ // 错误
```



添加`get` 和 `set` 函数来创建可写的 ref 对象

```js
const count = ref(1)
const plusOne = computed({
  get: () => count.value + 1,
  set: val => {
    count.value = val - 1
  }
})

plusOne.value = 1
console.log(count.value) // 0
```



## 5.watchEffect

**watchEffect**会在组件加载后立即执行传入的一个函数，同时响应式追踪其依赖，并在其依赖变更时重新运行该函数

```js
const count = ref(0)

watchEffect(() => console.log(count.value))
// -> logs 0

setTimeout(() => {
  count.value++
  // -> logs 1
}, 100)
```

**watchEffect**调用会返回一个对象，该对象可用于停止**watchEffect**监听

```js
const stop = watchEffect(() => {
  /* ... */
})

// later
stop()
```

调用**watchEffect**时传入的回调函数可以接收一个`onInvalidate `参数,onInvalidate需要是一个异步函数

`onInvalidate`只作用于异步函数，并且只有在如下两种情况下才会被调用：

（1）当回调函数被重新调用时

（2）当监听器被注销时（如组件被卸载了）

```js
let id=''
watchEffect( async (onInvalidate) => {
      onInvalidate(() => {
        console.log("清除副作用");
        clearInterval(id)
      });
      console.log(num.value)
     id= setInterval(()=>{console.log('jiujiu')},1000)
    });
```

**watchEffect**执行时机默认是组件**更新前**执行，如果想更改回调函数的执行时机可以更改`flush`参数

**pre**：更新前执行 （默认）

**post**：更新后执行

**sync**：同步执行（效率低）



## 6.watch

`watch`可以对单个数据进行监听，也可以对多个数据进行监听

#### 侦听单个数据源

```js
const state = reactive({ count: 0 })
watch(
  () => state.count,
  (count, prevCount) => {
    /* ... */
  }
)

// 直接侦听ref
const count = ref(0)
watch(count, (count, prevCount) => {
  /* ... */
})
```

#### 侦听多个数据源

```js
const firstName = ref('')
const lastName = ref('')

watch([firstName, lastName], (newValues, prevValues) => {
  console.log(newValues, prevValues)
})

firstName.value = 'John' // logs: ["John", ""] ["", ""]
lastName.value = 'Smith' // logs: ["John", "Smith"] ["John", ""]
```

#### 深度监听

使用侦听器来比较一个数组或对象的值，这些值是响应式的，要求它有一个由值构成的副本。

```js
const numbers = reactive([1, 2, 3, 4])

watch(
  () => [...numbers],
  (numbers, prevNumbers) => {
    console.log(numbers, prevNumbers)
  }
)

numbers.push(5) // logs: [1,2,3,4,5] [1,2,3,4]
```

尝试检查深度嵌套对象或数组中的 property 变化时，仍然需要 `deep` 选项设置为 true。

```js
const state = reactive({ 
  id: 1,
  attributes: { 
    name: '',
  }
})

watch(
  () => state,
  (state, prevState) => {
    console.log(
      'not deep',
      state.attributes.name,
      prevState.attributes.name
    )
  }
)

watch(
  () => state,
  (state, prevState) => {
    console.log(
      'deep',
      state.attributes.name,
      prevState.attributes.name
    )
  },
  { deep: true }
)

state.attributes.name = 'Alex' // 日志: "deep" "Alex" "Alex"
```



## 7.生命周期

可以通过在生命周期钩子前面加上 “on” 来访问组件的生命周期钩子。

下表包含如何在`setup()`内部调用生命周期钩子：

| 选项式 API        | Hook inside `setup` |
| ----------------- | ------------------- |
| `beforeCreate`    | --                  |
| `created`         | --                  |
| `beforeMount`     | `onBeforeMount`     |
| `mounted`         | `onMounted`         |
| `beforeUpdate`    | `onBeforeUpdate`    |
| `updated`         | `onUpdated`         |
| `beforeUnmount`   | `onBeforeUnmount`   |
| `unmounted`       | `onUnmounted`       |
| `errorCaptured`   | `onErrorCaptured`   |
| `renderTracked`   | `onRenderTracked`   |
| `renderTriggered` | `onRenderTriggered` |
| `activated`       | `onActivated`       |
| `deactivated`     | `onDeactivated`     |

因为 `setup` 是围绕 `beforeCreate` 和 `created` 生命周期钩子运行的，所以在这些钩子中编写的任何代码都应该直接在 `setup` 函数中编写

`setup`只能是同步的，不能是异步的

​      

