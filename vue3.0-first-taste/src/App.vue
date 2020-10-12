<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld name="王先生" msg="Welcome to Your Vue.js App" />
    <ReactiveTest></ReactiveTest>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import ReactiveTest from "./components/ReactiveTest.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    ReactiveTest
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
