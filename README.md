# Vue3
Vue3练习

# 学习目标
1. ref
2. reactive
3. toRefs
4. computed
5. toRef
6. watchEffect
7. watch
8. setup
# 属性分解
## setup
1. 一个组件选项，在组件被创建之前，props 被解析之后执行。它是组合式 API 的入口
```
<script>
import {ref, reactive, toRefs, computed, toRef, watchEffect, watch} from 'vue'
export default {
  setup() {
    const count = ref(0);
    return {
      count
    }
  }
}
</script>
```
## ref和reactive
1. ref 模块是用来声明简单数据类型的，例如,string , number ,boolean 等
2. reactive 模块是用来声明复杂数据类型的，例如，数组，对象等
``` 代码示例
  const count = ref(0);
  const state = reactive({
    name: '李四',
    age: 12,
  })
```
## toRef和toRefs
1. 可以用来为源响应式对象上的某个 property 新创建一个 ref。然后，ref 可以被传递，它会保持对其源 property 的响应式连接。
2. 将响应式对象转换为普通对象，其中结果对象的每个 property 都是指向原始对象相应 property 的 ref
## computed、watch和watchEffect
1. 接受一个 getter 函数，并根据 getter 的返回值返回一个不可变的响应式 ref 对象。
```
const count = ref(1)
const plusOne = computed(() => count.value + 1)

console.log(plusOne.value) // 2

plusOne.value++ // 错误
```
1.1. 或者，接受一个具有 get 和 set 函数的对象，用来创建可写的 ref 对象。
```
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
2. watch监听具体的值。ref和reactive下的写法不同
```
ref属性下：
const count = ref(0);
watch(count, (count, prevCount) => {
  console.log(count, prevCount)
})
```
```
reactive
const count = ref(0);
const state = reactive({
  name: '李四',
  age: 12,
})
watch([count, ()=> state.age], (count, prevCount) => {
  console.log(count, prevCount)
})
```
2.1. 与 watchEffect 相比，watch 允许我们：

2.1.1. 惰性地执行副作用；

2.1.2. 更具体地说明应触发侦听器重新运行的状态；

2.1.3. 访问被侦听状态的先前值和当前值。

3. watchEffect,立即执行传入的一个函数，同时响应式追踪其依赖，并在其依赖变更时重新运行该函数。还是比较勤快的。
```
const count = ref(0)

watchEffect(() => console.log(count.value))
// -> logs 0

setTimeout(() => {
  count.value++
  // -> logs 1
}, 100)
```

