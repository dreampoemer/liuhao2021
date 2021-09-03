<template>
  <div>
    {{ currentTime }}
  </div>
</template>

<script>
import md5 from 'js-md5'
export default {
  name: 'getCurrentTime',
  data() {
    return {
      currentTime: '',
      password:'123456abc'
    }
  },
  mounted() {
    //获取当前页面的路由的path或name
    console.log(this.$route.path)
    console.log(this.$route.name)
    this.currentTime = 3;

    this.$nextTick(() => {
        let date = new Date()
        this.currentTime = date.getFullYear()
    });
    // setTimeout(() => {
    //   let date = new Date()
    //   this.currentTime = date.getFullYear()
    // }, 0);
  }
}
</script>