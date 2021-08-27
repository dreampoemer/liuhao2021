<template>
  <div>
    {{ currentTime }}
  </div>
</template>

<script>
export default {
  name: 'getCurrentTime',
  data() {
    return {
      currentTime: ''
    }
  },
  mounted() {
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