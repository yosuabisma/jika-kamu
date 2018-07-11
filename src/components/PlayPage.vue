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
    <div class="results" v-if="beratBadan===false&&umurDiri===false">
      <carousel-3d class="planets" :space="200">
        <!-- <slide :index="0" class="planet-slider">
          <center>
            <img v-bind:src="'src/assets/img/planet-earth.svg'" style="width: 120px; height: 120px;" />
          </center>
        </slide>
        <slide :index="1" class="planet-slider">
          <center>
            <img v-bind:src="'src/assets/img/mars.svg'" style="width: 120px; height: 120px;" />
          </center>
        </slide>
        <slide :index="2" class="planet-slider">
          <center>
            <img v-bind:src="'src/assets/img/jupiter.svg'" v-bind:style="'width: 120px; height: 120px;'" />
          </center>
        </slide> -->
        <slide  v-for="planet in planets" :index="planet.idPlanet" class="planet-slider">
          <center>
            <div class="test" style="width:50%;" v-on:click="test(planet.idPlanet)">
              <img v-bind:src="'src/assets/img/' + planet.imageLink" v-bind:style="planet.imageSize"/>
              <h1>{{ planet.namaPlanet }}</h1>
            </div>
          </center>
        </slide>
      </carousel-3d>
      <div class="calculation" v-if="this.chosenPlanetID !== null">
      </div>
    </div>


    <!--NAVIGATION-->
    <div class="navigation">
      <h1 class="size20" v-on:click="gotoPage('/')"><b>Home</b></h1>
    </div>
  </div>
</template>
<script>
  import { Carousel3d, Slide } from 'vue-carousel-3d';

  export default{
    data(){
      return{
        beratBadan:true,
        umurDiri:true,
        berat:0,
        umur:0,
        chosenPlanetID: null,
        planets: [
          {
            namaPlanet: 'Merkurius',
            idPlanet: 0,
            imageLink: 'mercury.svg',
            imageSize: 'width: 70px; height: 70px;'
          },
          {
            namaPlanet: 'Venus',
            idPlanet: 1,
            imageLink: 'mars.svg',
            imageSize: 'width: 80px; height: 80px;'
          },
          {
            namaPlanet: 'Bumi',
            idPlanet: 2,
            imageLink: 'planet-earth.svg',
            imageSize: 'width: 90px; height: 90px;'
          },
          {
            namaPlanet: 'Mars',
            idPlanet: 3,
            imageLink: 'venus.svg',
            imageSize: 'width: 80px; height: 80px;'
          },
          {
            namaPlanet: 'Jupiter',
            idPlanet: 4,
            imageLink: 'jupiter.svg',
            imageSize: 'width: 120px; height: 120px;'
          }
        ]
      }
    },
    components: {
      'carousel-3d': Carousel3d,
      'slide': Slide
    },
    methods: {
      gotoPage(route) {
        this.$router.push(route);
      },
      refresh(){
        location.reload();
      },
      test(x) {
        this.chosenPlanetID = x;
      }
    },
    computed: {
      getData(foo) {
        return foo * 2;
      }
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
  .planets {
    border-radius: 8px;
    border: 2px solid white;
  }
  .planet-slider {
    border: none;
    width: 180px;
    height: 100px;
    margin-top: 40px;
    background-color: transparent;
  }
</style>
