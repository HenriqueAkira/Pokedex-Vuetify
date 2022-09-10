<template>
  <div >
    <div class="intro-img"></div>
    <div class="intro-text">
      <v-icon x-large color="red">mdi-pokemon-go</v-icon>
      <h1 class="subtitle-7 ">POKEDEX<span class="font-weight-light"> VUE</span></h1>
      <h4 class="overline subtitle" id="subtitle">Your customized pokedex made with Vue.js</h4>
      <p class="overline">Another Nintendo franchise, Pokémon, is the fourth best-selling series of all time</p>
    </div>
  </div>
  
</template>

<script>
export default {

}
</script>

<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100;300&display=swap');

.intro-img{
  height: 45em;
  background-image: url("@/assets/background.gif");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  filter: blur(4px);
}

.intro-text {
  font-size: 2em;
  font-family: 'Montserrat', sans-serif;
  font-weight: bold;
  position: absolute;
  top: 30%;
  left: 50%;
  right: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
  width: 80%;
  text-align: center;
}


h4#subtitle.overline.subtitle{
  font-size: 1em !important
}

@media screen and (max-width: 600px) {
        .intro-text{
            font-size: 1.2em;
        }
    }   

</style>