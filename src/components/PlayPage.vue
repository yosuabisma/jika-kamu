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
      <center>
        <h6>Swipe untuk mengganti planet</h6>
        <h6>Tap pada suatu planet untuk melihat fakta menarik</h6>
      </center>
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
      <div class="calculation" v-if="chosenPlanetID != null">
        <center>
          <h3> Jika kamu di planet {{ planets[chosenPlanetID].namaPlanet }}, maka kamu berusia {{ Math.floor(planets[chosenPlanetID].period * umur) }} tahun dan memiliki bobot {{ Math.floor((planets[chosenPlanetID].grav/9.798) * berat) }} kg.</h3>
          <br/>
          <h6 class="blueColor2">1 tahun (revolusi planet) di Planet {{ planets[chosenPlanetID].namaPlanet }} sama dengan {{ planets[chosenPlanetID].period }} tahun di Bumi dengan gaya gravitasi {{ planets[chosenPlanetID].grav }} m/s<sup>2</sup>.</h6>
        </center>
        <br/><br/>
        <center>
          <div class="fact">
            <h5>{{planets[chosenPlanetID].factList[randomIndex].text}}</h5>
          </div>
        </center>
        <!-- <h2>{{ getUmur(planets[chosenPlanetID].period) }} </h2> -->
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
        randomIndex:null,
        planets: [
          {
            namaPlanet: 'Merkurius',
            idPlanet: 0,
            imageLink: 'mercury.svg',
            imageSize: 'width: 70px; height: 70px;',
            period: 0.241,
            grav:3.7,
            factList: [
              {text: 'Planet merkurius telah dikenal manusia setidaknya 5.000 tahun yang lalu.'},
              {text: 'Bangsa Sumeria mengaitkan planet ini dengan Tuhan mereka yang disebut Nabu.'},
              {text: 'Suhu permukaan Merkurius bisa mencapai 450 derajat celcius.'},
              {text: 'Merkurius tidak memiliki atmosfer.'},
              {text: 'Setahun di Merkurius hanya 88 hari.'},
              {text: 'Merkurius adalah planet terpadat kedua setelah Bumi, dengan inti logam yang membentang antara 3.600-3.800 kilometer.'},
              {text: 'Mariner 10, pesawat ruang angkasa pertama yang mengunjungi Merkurius.'},
              {text: 'Merkurius memiliki ukuran sekitar 1/3 kali ukuran bumi.'},
              {text: 'Merkurius bergerak mengelilingi matahari dengan kecepatan 180.000 kilometer perjam.'},
              {text: 'Satu hari di Merkurius setara dengan 59 hari di Bumi.'},
            ]
          },
          {
            namaPlanet: 'Venus',
            idPlanet: 1,
            imageLink: 'mars.svg',
            imageSize: 'width: 80px; height: 80px;',
            period: 0.615,
            grav:8.87,
            factList: [
              {text: 'Diameter planet Venus adalah 12.100 kilometer.'},
              {text: 'Venus sering disebut saudara kembar Bumi karena planet ini paling dekat dengan Bumi, lalu juga ukurannya yang hampir sama dengan Bumi.'},
              {text: 'Venus tidak memiliki satelit.'},
              {text: 'Kecepatan orbital Venus adalah 35 kilometer per-detik.'},
              {text: 'Venus adalah planet terbesar keenam di tata surya.'},
              {text: 'Atmosfer Venus terdiri dari karbon dioksida (96%) dan nitrogen (3%) beserta gas-gas lainnya.'},
              {text: 'Venus adalah planet paling terpanas di tata surya.'},
              {text: 'Venus adalah planet paling terterang di tata surya.'},
              {text: 'Permukaan Venus yang sangat kering mungkin terbentuk oleh banyaknya aktivitas vulkanik.'},
              {text: 'Awan yang mengelilingi Venus sebagian besar terdiri dari asam sulfat.'},
            ]
          },
          {
            namaPlanet: 'Bumi',
            idPlanet: 2,
            imageLink: 'planet-earth.svg',
            imageSize: 'width: 90px; height: 90px;',
            period: 1,
            grav:9.798,
            factList: [
              {text: 'Nama “Earth” (Bumi) diambl dari Bahasa Inggris Kuno dan Bahasa Jerman Inggil Kuno (oerthe dan erda, yang artinya “tanah”).'},
              {text: 'Bumi mempunyai berat hampir 6 septillion kg.'},
              {text: 'Pada 2200 tahun yang lalu Eratosthenes telah memperkirakan lingkar Bumi dengan menggunakan matematika tanpa meninggalkan Mesir.'},
              {text: 'Satu kali rotasi Bumi sebenarnya bukan selama 24 jam, tetapi 23 jam, 56 menit dan 4 detik.'},
              {text: 'Bumi dijuluki Planet Biru, karena 70% permukaan Bumi tertutup oleh air.'},
              {text: 'Di inti Bumi megandung emas yang cukup untuk menutupi seluruh permukaan bumi dengan ketebalan 1,5 kaki.'},
              {text: 'Diameter Bumi adalah 12.756 km. '},
              {text: 'Kecepatan orbit Bumi adalah 29,8 km per detik.'},
              {text: 'Jarak Bumi dari matahari adalah minimal 146 juta km, maksimal 152 juta km.'},
              {text: 'Bumi adalah planet yang paling padat dalam sistem tata surya.'},
            ]
          },
          {
            namaPlanet: 'Mars',
            idPlanet: 3,
            imageLink: 'venus.svg',
            imageSize: 'width: 80px; height: 80px;',
            period: 1.881,
            grav:3.71,
            factList: [
              {text: 'Mars adalah planet keempat terdekat dari matahari.'},
              {text: 'Mars adalah planet terbesar ketujuh.'},
              {text: 'Mars adalah sebuah planet terestrial dengan permukaan padat.'},
              {text: 'Permukaan Mars paling mirip dengan bumi dibandingkan planet-planet lain.'},
              {text: 'Mars merupakan tempat alternatif terbaik untuk dihuni selain bumi.'},
              {text: 'Mars memiliki dua satelit kecil yang mengorbit sangat dekat dengan permukaannya yaitu Phobos dan Deimos.'},
              {text: 'Mars memiliki beberapa karakteristik geologi yang luar biasa.'},
              {text: 'Mars memiliki 37,5% dari gravitasi yang bumi miliki.'},
              {text: 'Karena Mars memiliki hampir tidak ada atmosfer, Sunrise dan sunset muncul dengan warna biru.'},
              {text: 'Galileo Galilea adalah orang pertama yang mengamati Mars melalui teleskop, di 1609.'},
            ]
          },
          {
            namaPlanet: 'Jupiter',
            idPlanet: 4,
            imageLink: 'jupiter.svg',
            imageSize: 'width: 120px; height: 120px;',
            period: 11.86,
            grav:24.92,
            factList: [
              {text: 'Jupiter punya hari terpendek dibandingkan seluruh planet. (9 jam, 55 menit).'},
              {text: 'Satelit alami Jupiter yang bernama Ganymede adalah satelit alami terbesar di solar sistem.'},
              {text: '8 pesawat luar angkasa telah mengunjungi Planet Jupiter.'},
              {text: 'Kamu bisa merayakan tahun baru di planet Jupiter setiap 11.8 tahun bumi.'},
              {text: 'Nama Jupiter berasal dari raja dari segala dewa yang menguasai langit dan petir dalam mitologi Romawi.'},
              {text: 'Jupiter adalah planet terbesar di tata surya.'},
              {text: 'Jupiter adalah objek langit paling terang ke empat setelah, Matahari, Bulan, Venus.'},
              {text: 'Jupiter memiliki hari terpendek dari planet lainnya.'},
              {text: 'Satelit alami terbesar di Jupiter adalah Ganymede.'},
              {text: 'Karena kemiringan Jupiter yang sangat kecil, dan terkecil setelah Merkurius, disana tidak ada musim yang terjadi.'},
            ]
          },
          {
            namaPlanet: 'Saturnus',
            idPlanet: 5,
            imageLink: 'saturn.svg',
            imageSize: 'width: 100px; height: 100px;',
            period: 29.46,
            grav:10.44,
            factList: [
              {text: 'Planet Saturnus bisa kita lihat dengan mata telanjang.'},
              {text: 'Saturnus mempunyai cincin planet yang paling besar dibandingkan planet2 yang lain.'},
              {text: 'Saturnus punya 150 bulan.'},
              {text: 'Saturnus terbuat dari gas hidrogen.'},
              {text: 'Cincin Saturnus terbuat dari batuan meteorit.'},
              {text: 'Angin di Saturnus bergerak lebih cepat dari angin tornado.'},
              {text: 'Nama Saturnus berarti dewa petani.'},
              {text: 'Satelit alami Saturnus terbesar adalah Titan.'},
              {text: 'Planet Saturnus berbentuk sebagai planet paling lonjong.'},
              {text: 'Planet Saturnus dinamai menurut nama dewa pertanian Romawi, Saturnus, yang juga ayah dari dewa Romawi Jupiter.'},
            ]
          },
          {
            namaPlanet: 'Uranus',
            idPlanet: 6,
            imageLink: 'uranus.svg',
            imageSize: 'width: 80px; height: 80px;',
            period: 84.32,
            grav:8.87,
            factList: [
              {text: 'Planet Uranus pertama kali ditemukan pada tahun 1781 oleh Sir William Herschel.'},
              {text: 'Planet Uranus dinobatkan sebagai planet terdingin.'},
              {text: 'Satelit alami dari planet Uranus diambil dari karakter (Oberon, Titania dan Miranda) yang dicipatakan William Shakespeare dan Paus Alexander.'},
              {text: 'Hanya satu pesawat luar agkasa yang pernah terbang melintasi planet Uranus. Voyager 2, Tahun 1986.'},
              {text: 'Sudut kemiringan sumbu Uranus adalah 97 derajat! Ini berarti bahwa kutub selatan Uranus mengarah lurus ke bumi.'},
              {text: 'Atmosfer di planet ini terutama terdiri dari hidrogen, helium, dan metana.'},
              {text: 'Dibutuhkan waktu sekitar 84 tahun bagi Uranus untuk sekali mengorbit matahari.'},
              {text: 'Kecepatan orbit Uranus adalah 6,6 km/detik.'},
              {text: 'Seperti Venus, Uranus berputar dari timur ke barat, yang merupakan kebalikan dari arah rotasi bumi.'},
              {text: 'Uranus membutuhkan waktu 17 jam, 14 menit untuk berotasi.'},
            ]
          },
          {
            namaPlanet: 'Neptunus',
            idPlanet: 7,
            imageLink: 'neptune.svg',
            imageSize: 'width: 70px; height: 70px;',
            period: 164.8,
            grav:11.15,
            factList: [
              {text: 'Planet Neptunus pertama kali ditemukan pesawat Voyager 2 pada tahun 1989.'},
              {text: 'Salah satu badai yang pernah tercatat dan terbesar di planet Neptunus pada tahun 1989, berlangsung selama 5 tahun.'},
              {text: 'Planet Neptunus mebutuhkan waktu sekitar 16 jam untuk berganti hari.'},
              {text: 'Planet Neptunus mengelilingi matahari dalam waktu 165 tahun (164.8 tahun).'},
              {text: 'Neptunus merupakan planet terkecil dalam jajaran 4 planet terluar tata surya.'},
              {text: 'Neptunus memiliki cincin, namun cincinya sangat redup.'},
              {text: 'Neptunus tidak dapat dilihat dengan mata telanjang dan pertamakali di observasi tahun 1846.'},
              {text: 'Nama Neptunus berasal dari Kepercayaan orang Romawi Kuno yang berarti dewa air dan laut.'},
              {text: 'Iklim di Neptunus sangat aktif.'},
              {text: 'Neptunus memiliki atmosfir yang sangat tebal yang terdiri dari 74% hidrogen, 25% helium dan metana kira-kira 1%.'},
            ]
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
        this.randomIndex=Math.floor(Math.random() * Math.floor(10));
      },
      getUmur(val) {
        return this.setUmur(val);
      }
    },
    computed: {
      setUmur(foo) {
        return foo * this.umur;
      }
    }
  }
</script>
<style>
  .blueColor{
    color: #008080;
  }
  .blueColor2{
    color: #00FFFF;
  }
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
  .fact{
    background-color: #A3E4D7;
    border-radius: 10px;
    color:#0E6251;
    padding: 10px 10px;
    border: 4px solid #0E6251;
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
    border-radius: 16px;
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
