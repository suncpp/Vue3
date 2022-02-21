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





