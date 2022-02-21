<template>
  <h1>{{ count }}</h1>
  <h2>{{handleComputedCount}}</h2>
  <button @click="handleCount">数量点击</button>
  <br>
  <h2>{{state.name}}{{state.age}}</h2>
  <button @click="handleReactive">reactive点击</button>
</template>

<script>
// ref 模块是用来声明简单数据类型的，例如,string , number ,boolean 等
// reactive 模块是用来声明复杂数据类型的，例如，数组，对象等

import {ref, reactive, toRefs, computed, toRef, watchEffect, watch} from 'vue'
export default {
  name: 'HelloWorld',
  setup() {
    const count = ref(0);
    const state = reactive({
      name: '李四',
      age: 12,
    })

    const handleComputedCount = computed(() => {
      return count.value += 2
    });

    watchEffect(() => {
      console.log(count.value,'111');
    });

    watch(count, (count, prevCount) => {
      console.log(count, prevCount)
    })

    watch([count, ()=> state.age], (count, prevCount) => {
      console.log(count, prevCount)
    })

    const handleCount = () =>{
      count.value++;
    }

    const handleReactive = () =>{
      console.log(this,111,state,222,state.name);
      state.age++;
    }

    console.log(handleComputedCount.value)
    return {
      count,
      state,
      ...toRefs(state),
      handleCount,
      handleReactive,
    }
  }
}
</script>
