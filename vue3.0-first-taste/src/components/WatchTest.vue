<template>
  <div class="hello">
    <p>watch:----------------------------------------</p>
    <!-- <p>监视单个ref值{{refCount}}</p> -->
    <!-- <p>监视多个ref值{{refCount1}}/{{refCount2}}</p> -->
    <!-- <p>监视 reactive 的数据源{{user.age}}</p> -->
    <p>监听reactive多个数据源{{user.age}}{{getNum.number}}</p>
  </div>
</template>

<script>
import { watch, reactive } from "vue";

export default {
  name: "watch",
  setup() {
    console.log("watch:-----------------------------------------");
    //watch() 函数用来监视某些数据项的变化，从而触发某些特定的操作
    //watch 进来就会执行一次 (如果不想执行需要设置{ lazy: false })

    // // 单个ref监视--------------------
    // const refCount = ref(0);
    // //refCount发生变化就会触发watch 进来就会执行一次 (如果不想执行需要设置{ lazy: false })
    // watch(() => console.log(refCount.value), { lazy: false });
    // setInterval(() => {
    //   refCount.value += 1;
    // }, 5000);
    // return {
    //   refCount
    // };

    // // 监视多个ref---------------------------
    // const refCount1 = ref(0);
    // const refCount2 = ref(0);
    // //refCount发生变化就会触发watch 进来就会执行一次 (如果不想执行需要设置{ lazy: false })
    // watch(
    //   [refCount1, refCount2],
    //   ([NewrefCount1, OldrefCount1], [NewrefCount2, OldrefCount2]) => {
    //     console.log(NewrefCount1, OldrefCount1);
    //     console.log(NewrefCount2, OldrefCount2);
    //   },
    //   { lazy: false }
    // );
    // setInterval(() => {
    //   refCount1.value += 1;
    //   refCount2.value -= 1;
    // }, 5000);
    // return {
    //   refCount1,
    //   refCount2
    // };

    // // 单个reactive 监视-----------------------------
    // const state = reactive({
    //   user: {
    //     age: 0
    //   }
    // });
    // watch(
    //   () => state.user.age,
    //   (newVal, oldVal) => {
    //     console.log(newVal);
    //     console.log(oldVal);
    //   },
    //   { lazy: true }
    // );
    // setInterval(() => {
    //   state.user.age += 1;
    // }, 2000);
    // return state;

    // // 多个reactive 监视-----------------------------
    const state = reactive({
      user: {
        age: 0
      },
      getNum: {
        number: 0
      }
    });
    watch(
      [() => state.user.age, () => state.getNum.number],
      ([newVal, oldVal], [getNumNew, getNumOld]) => {
        console.log(newVal);
        console.log(oldVal);
        console.log(getNumNew);
        console.log(getNumOld);
      },
      { lazy: true }
    );
    setInterval(() => {
      state.user.age += 1;
      state.getNum.number += 1;
    }, 2000);
    return state;
  }
};
</script>
