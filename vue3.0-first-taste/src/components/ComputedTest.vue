<template>
  <div class="hello">
    <p>computed计算属性:----------------------------------------</p>
    <!-- <p>只读计算属性：</p>
    <span>refNum:{{refNum}}</span>
    <button @click="refNum++">+1</button>
    <span>conputedCount:{{conputedCount}}</span>
    <button @click="conputedCount++">+1(无效)</button>-->
    <p>可读可写计算属性：</p>
    <span>refNum:{{refNum}}</span>
    <button @click="refNum++">+1</button>
    <span>conputedCount:{{conputedCount}}</span>
    <button @click="conputedCount++">+1</button>
  </div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  name: "ComputedTest",
  setup() {
    // 只读计算属性
    // const refNum = ref(0);
    // let conputedCount = computed(() => refNum.value + 1);
    // return {
    //   refNum,
    //   conputedCount
    // };

    // 可读可写
    const refNum = ref(0);
    let conputedCount = computed({
      // 取值函数
      get: () => refNum.value + 1,
      // 赋值函数
      set: () => {
        refNum.value = refNum.value + 1;
      }
    });
    // 为计算属性赋值
    conputedCount.value = 0;
    return {
      refNum,
      conputedCount
    };
  }
};
</script>
