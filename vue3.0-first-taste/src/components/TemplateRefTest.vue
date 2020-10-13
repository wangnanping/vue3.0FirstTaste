<template>
  <div class="hello">
    <p>TemplateRefTest:--------------------</p>
    <span ref="spanDom">被获取的dom</span>
    <TemplateRefSonTest ref="sonDom" />
  </div>
</template>

<script>
import TemplateRefSonTest from "./son/TemplateRefSonTest";
import { ref, onMounted } from "vue";
export default {
  name: "Proveide/inject",
  components: {
    TemplateRefSonTest
  },
  setup() {
    console.log("TemplateRefTest--------------------");
    // 创建一个 DOM 引用
    const spanDom = ref(null);

    // 获取子组件
    const sonDom = ref(null);

    // 在 DOM 首次加载完毕之后，才能获取到元素的引用
    onMounted(() => {
      // 为 dom 元素设置字体颜色
      // spanDom.value 是原生DOM对象
      spanDom.value.style.color = "red";

      console.log(sonDom.value.num);
      sonDom.value.setNum();
      console.log(sonDom.value.num);
    });

    // 把创建的引用 return 出去
    return {
      spanDom,
      sonDom
    };
  }
};
</script>

