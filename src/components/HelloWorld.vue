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
    console.log(this.password)
    console.log(md5(this.password))
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