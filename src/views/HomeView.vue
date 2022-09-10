<template>
  <div >
    <div class="intro-img"></div>
    <div class="intro-text">
      <v-icon x-large color="red">mdi-pokemon-go</v-icon>
      <h1 class="subtitle-7 ">POKEDEX<span class="font-weight-light"> VUE</span></h1>
      <h4 class="overline subtitle" id="subtitle">Your customized pokedex made with Vue.js</h4>
      <p class="overline">Another Nintendo franchise, Pokémon, is the fourth best-selling series of all time</p>
    </div>

    <v-parallax dark height="900" class="parallax" src="@/assets/xerneas.jpg">
      <div class="pokedex-parallax mx-auto">
          <v-carousel
          cycle
          height="600"
          hide-delimiter-background
          show-arrows-on-hover
        >
          <v-carousel-item
            v-for="(slide, i) in slides"
            :key="i"
          >
            <v-sheet
              :color="colors[i]"
              height="100%"
            >
              <v-row
                class="fill-height"
                align="center"
                justify="center"
              >
                <div class="text-h2">
                  {{ slide }} Slide
                </div>
              </v-row>
            </v-sheet>
          </v-carousel-item>
        </v-carousel>
      </div>
    </v-parallax>
  </div>
  
</template>

<script>
export default {
  data () {
      return {
        colors: [
          'indigo',
          'warning',
          'pink darken-2',
          'red lighten-1',
          'deep-purple accent-4',
        ],
        slides: [
          'First',
          'Second',
          'Third',
          'Fourth',
          'Fifth',
        ],
      }
    },

}
</script>

<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100;300&display=swap');

.intro-img{
  height: 55em;
  background-image: url("@/assets/background.gif");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  filter: blur(4px);
}

.parallax{
  height: 100%;
  width: 100% !important;
  transform: none !important;
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

.pokedex-parallax{
  width: 80vw;
}


h4#subtitle.overline.subtitle{
  font-size: 1em !important
}

@media screen and (max-width: 600px) {
        .intro-text{
            font-size: 1.2em;
        }
        .intro-img{
          height: 45em;
        }
    }   

</style>