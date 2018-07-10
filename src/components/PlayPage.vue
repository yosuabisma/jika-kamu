<template>
  <div class="play-page">
    <div v-if="beratBadan===true&&umurDiri===true"class="game">
      <center>
        <h1 class="white">Jika Kamu...</h1>
        <div v-if="beratBadan===true" class="popQuestBerat">
          <br/>
          <center>
            <h2>Berat badan kamu</h2>
            <br/>
            <input class="inputWeight" v-model="berat" maxlength="3"/><span> Kg</span>
            <br/><br/>
          </center>
        </div>
        <div v-if="umurDiri===true" class="popQuestUmur">
          <br/>
          <center>
            <h2>Umur kamu</h2>
            <br/>
            <input class="inputAge" v-model="umur" maxlength="3"/><span> Tahun</span>
            <br/><br/>
          </center>
        </div>
        <br/><br/>
        <div class="lanjutBTN" v-on:click="beratBadan=false;umurDiri=false;">
          <center><h1>Lanjut</h1></center>
        </div>
      </center>
    </div>


    <!--NAVIGATION-->
    <div class="navigation">
      <h1 class="size20" v-on:click="gotoPage('/')"><b>Home</b></h1>
    </div>
  </div>
</template>
<script>
  export default{
    data(){
      return{
        beratBadan:true,
        umurDiri:true,
        berat:0,
        umur:0,
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
  .size20{
    font-size: 20px;
  }
  .play-page{
    padding: 30px 30px;
    height: 640px;
    width: 360px;
    cursor:pointer;
    background-color: #0f0d0d;
    color: #fff;
  }
  .popQuestBerat{
    margin-top: 40px;
    padding: 10px 10px;
    background-color: #A3E4D7;
    border-radius: 10px;
    color:#0E6251;
    border: 4px solid #0E6251;
    width:250px;
  }
  .popQuestUmur{
    margin-top: 40px;
    padding: 10px 10px;
    background-color: #F1948A;
    border-radius: 10px;
    border: 4px solid #B03A2E;
    color:#B03A2E;
    width:250px;
  }
  .inputWeight{
    border:none;
    border-bottom: 3px solid #0E6251;
    background-color: #A3E4D7;
    font-size: 28px;
    text-align: center;
    width: 120px;
    color:#0E6251;
  }
  .inputAge{
    border:none;
    border-bottom: 3px solid #B03A2E;
    background-color: #F1948A;
    font-size: 28px;
    text-align: center;
    width: 120px;
    color:#B03A2E;
  }
  .white{
    color:#fff;
  }
  .lanjutBTN{
    background-color: #F39C12;
    padding: 10px 10px;
    width:250px;
    color:#fff;
    border-radius: 10px;
    border: 4px solid #fff;
  }
  .navigation{
    color:#fff;
    margin-top: 30px;
  }
</style>
