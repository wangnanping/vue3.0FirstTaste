<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png" />
    <SetupTest name="王先生" msg="Welcome to Your Vue.js App" />
    <ReactiveTest />
    <ComputedTest />
    <WatchTest />
  </div>
</template>

<script>
import SetupTest from "./components/SetupTest.vue";
import ReactiveTest from "./components/ReactiveTest.vue";
import ComputedTest from "./components/ComputedTest.vue";
import WatchTest from "./components/WatchTest.vue";

export default {
  name: "App",
  components: {
    SetupTest,
    ReactiveTest,
    ComputedTest,
    WatchTest
  },
  methods: {
    start: () => {}
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
