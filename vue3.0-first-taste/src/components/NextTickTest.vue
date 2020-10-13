<template>
  <div class="hello">
    <button v-if="isShowInput === false" @click="showInput">展示文本框</button>
    <input type="text" v-else ref="ipt" />
  </div>
</template>

<script>
export default {
  name: "NextTickTest",
  data() {
    return {
      isShowInput: false
    };
  },
  methods: {
    showInput() {
      this.isShowInput = !this.isShowInput;
      // console.log(this.$refs)
      this.$nextTick(() => {
        this.$refs.ipt.focus();
      });
    }
  }
};
</script>

