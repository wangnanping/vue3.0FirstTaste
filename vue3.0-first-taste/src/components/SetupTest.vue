<template>
  <div class="hello">
    <p>setup:----------------------------------------</p>
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
    name: Number
  },
  created() {
    // console.log(this.$listeners)
    console.log("created");
  },
  setup(props, ctx) {
    console.log(props);
    console.log(ctx);
    console.log(this);
    console.log("setup");
  },
  beforeCreate() {
    console.log("beforCreate");
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
