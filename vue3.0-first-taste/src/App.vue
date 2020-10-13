<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png" />
    <SetupTest name="王先生" msg="Welcome to Your Vue.js App" />
    <ReactiveTest />
    <ComputedTest />
    <WatchTest />
    <p>ProveideAndinject:----------------------------------------</p>
    <button @click="color = 'yellow'">黄色</button>
    <button @click="color ='blue'">蓝色</button>
    <button @click="color='green'">绿色</button>
    <ProveideAndInjectTest />
  </div>
</template>

<script>
import SetupTest from "./components/SetupTest.vue";
import ReactiveTest from "./components/ReactiveTest.vue";
import ComputedTest from "./components/ComputedTest.vue";
import WatchTest from "./components/WatchTest.vue";
import ProveideAndInjectTest from "./components/Proveide&injectTest.vue";

import { ref, provide } from "vue";

export default {
  name: "App",
  components: {
    SetupTest,
    ReactiveTest,
    ComputedTest,
    WatchTest,
    ProveideAndInjectTest
  },
  setup: () => {
    const color = ref("yellow");
    provide("provideColor", color);
    return {
      color
    };
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
