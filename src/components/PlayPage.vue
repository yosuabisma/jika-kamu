<template>
  <div class="play-page">

  </div>
</template>
<script>
  export default{
    data(){
      return{
        ran:0,
        //secsLoad:9,
      }
    },
    methods: {
      gotoPage(route) {
        this.$router.push(route);
      },
      refresh(){
        location.reload();
      },
    }
  }
</script>
<style>
  .play-page{
    padding: 20px 20px;
    height: 640px;
    width: 360px;
    cursor:pointer;
    background-color: #0f0d0d;
    color: #fff;
  }
</style>
