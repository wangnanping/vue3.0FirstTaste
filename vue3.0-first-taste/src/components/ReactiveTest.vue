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
import { ref, reactive, toRefs, isRef } from "vue";

export default {
  //   name: "ReactiveTest",
  //   created() {},
  //   beforeCreate() {},
  setup() {
    // 创建响应式数据对象 refNum，初始值为 0
    const refNum = ref(0);
    // 如果要访问 ref() 创建出来的响应式数据对象的值，必须通过 .value 属性才可以，只有在setup内部才需要 .value 属性
    // console.log(refNum.value); // 输出 0
    // 让 refNum 的值 +1
    refNum.value++;
    // 再次打印 refNum 的值
    // console.log(refNum.value); // 输出 1
    const refC1 = ref(0);
    console.log(isRef(refC1)); // isRef判断是否为ref创建

    // 创建响应式数据对象，得到的 state 类似于 vue 2.x 中 data() 返回的响应式对象
    const state = reactive({
      refC1,
      refNum, // 当把 ref() 创建出来的响应式数据对象，挂载到 reactive() 上时，会自动把响应式数据对象展开为原始的值
      count: 0,
      age: [
        {
          ageNumber: 1
        }
      ]
    });
    state.refNum += 1;
    state.count += 1;
    // console.log(state);

    // 旧的ref会被替换为新的ref
    const refC2 = ref(9);
    // state.refC1 = refC2; // 会报错 但是这里refC1会被替换为refC1
    state.refC1 = refC2.value;
    state.refC1++;
    console.log(state.refC1);
    console.log(refC2.value);
    console.log(refC1.value);

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
