<template>
  <div class="test-viewport">
    测试文字
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.test-viewport{
  width: 750px;
  height: 100px;
  font-size: 100px;
  text-align: center;
  line-height: 100px;
  background-color: skyblue;
}
</style>
