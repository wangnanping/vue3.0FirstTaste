<template>
  <div class="ReactiveTest">
    <p>ref\reactive\toRefs:----------------------------------------</p>
    <!-- 在 template 中访问响应式数据 -->
    <p>reactive当前的 count 值为：{{count}}</p>
    <button @click="count += 1">+1</button>
    <p>ref当前的refNum值为: {{refNum}}</p>
    <button @click="refNum += 1">+1</button>
    <p>数组当前的ageNumber值为: {{age[0].ageNumber}}</p>
    <button @click="age[0].ageNumber += 1">+1</button>
  </div>
</template>

<script>
import { ref, reactive, toRefs } from "vue";

export default {
  //   name: "ReactiveTest",
  //   created() {},
  //   beforeCreate() {},
  setup() {
    const refNum = ref(0);
    // 创建响应式数据对象，得到的 state 类似于 vue 2.x 中 data() 返回的响应式对象
    const state = reactive({
      count: 0,
      age: [
        {
          ageNumber: 1
        }
      ]
    });
    state.count += 1;
    console.log(state);
    // setup 函数中将响应式数据对象 return 出去，供 template 使用
    return {
      refNum,
      ...toRefs(state)
    };
  }
};
</script>


<style scoped>
</style>
