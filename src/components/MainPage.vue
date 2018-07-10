<template>
  <div class="main-page">
    <div class="about">
      <img v-on:click="gotoPage('/about')" class="spanCornerLeft" v-bind:src="'src/assets/img/Information_White.svg'" height="30px"/>
    </div>
    <div class="title">
      <br/><br/>
      <center>
        <img v-bind:src="'src/assets/img/Group 4.png'"/>
      </center>
    </div>
    <br/>
    <div class="bottomBtn">
      <center>
        <div class="buttonPlay" v-on:click="gotoPage('/play')">
          <img v-bind:src="'src/assets/img/Play_White.svg'" width="60px" height="50px"/>
        </div>
      </center>
    </div>
  </div>
</template>
<script>
  export default {
    methods: {
      gotoPage(route) {
        this.$router.push(route);
      },


    }
  }
</script>
<style>
  /*FONT*/
  .size72{
    font-size:72px;
  }
  .size60{
    font-size:60px;
  }
  .size36{
    font-size:36px;
  }
  .size20{
    font-size: 20px;
  }
  .size24{
    font-size: 24px;
  }
  .white{
    color:#f2f2f2;
  }
  .blue{
    color: #47a8e5;
  }
  .spanCornerRight{
    float: right;
  }
  .purple{
    color:#5856ff;
  }
  .height1{
    line-height: 67.5px;
  }
  .height2{
    line-height: 22.5px;
  }

  .main-page {
    padding:30px 30px;
    background: #0f0d0d;
    color: #fff;
    cursor:pointer;
    max-height: 640px;
    max-width: 360px;
    height: 640px;
    width: 360px;
  }
  .title{
    margin-top:50px;
  }
  .bottomBtn{
    margin-top: 10px;
  }
  .buttonPlay{
    color:#ff6f69;
    background-color: #c43416;
    border-radius:100%;
    border:5px solid #fff;
    padding: 10px 10px;
    width: 80px;
    height: 80px;
  }
  td{
    padding: 10px 10px;
  }
</style>
