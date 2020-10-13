<template>
  <div class="hello">
    <span>{{num}}</span>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "TemplateRefTest",
  setup() {
    const num = ref(0);
    const setNum = () => {
      num.value = 3;
    };
    return {
      setNum,
      num
    };
  }
};
</script>

