<template>
  <div >
    <div class="intro-img"></div>
    <div class="intro-text">
      <v-icon x-large color="red">mdi-pokemon-go</v-icon>
      <h1 class="subtitle-7 ">POKEDEX<span class="font-weight-light"> VUE</span></h1>
      <h4 class="overline subtitle" id="subtitle">Your customized pokedex made with Vue.js</h4>
      <p class="overline">Another Nintendo franchise, Pokémon, is the fourth best-selling series of all time</p>
    </div>

    <v-parallax dark height="900" class="parallax" src="@/assets/grass-background.jpg">
      <v-row align="center" class="mt-10">
        <v-col class="text-center" cols="12" md="6">
          <h1><v-icon color="red" x-large>mdi-pokeball</v-icon></h1>
          <p class="parallax-title text-uppercase">
            The <span class="red--text font-weight-bold text-uppercase">Pokédex section</span> has a wealth of information on all the Pokémon creatures from the entire game series. 
          </p>
          <p class="parallax-text ">
            On the main list pages you can see the various stats of each Pokémon. See a detailed page with Pokédex data,
             descriptions, sprites, evolutions and stats!
          </p>
        </v-col>

        <v-col cols="12" md="6" align="center" >
          <div class="pokedex-parallax ">
              <v-carousel
              height="600"
              hide-delimiter-background
              show-arrows-on-hover
            >
              <v-carousel-item
                v-for="(pokemon, i) in pokemonsBanner"
                :key="i"
              >
                <v-sheet
                  
                  color="rgba(211,211,211,0.8)"
                  height="90%"
                >
                  <v-row
                    id="carousel-item"
                    class="fill-height"
                    align="center"
                  >
                    <v-col cols="6">
                      <v-img :src="pokemon.sprite" width="400" height="auto" contain></v-img>
                    </v-col>

                    <v-col cols="5" >
                      
                      <v-row class="pa-3">
                        <div class="icon icon-banner pa-1 mr-4 mb-4" :class="`${type.type.name}`" v-for="type in pokemon.types" :key="type.type.name">
                          <v-img contain :src="require(`@/assets/${type.type.name}.svg`)"></v-img>
                        </div>
                      </v-row>
                        
                      <div class="text-overline">
                      #{{pokemon.id}} {{pokemon.name}}
                      </div>
                      
                      <div>
                        HP
                        <v-progress-linear color="red lighten-1" height="15" :value="pokemon.stats[0]"> <strong>{{pokemon.stats[0]}}</strong> </v-progress-linear>
                        Attack
                        <v-progress-linear color="deep-orange lighten-3" height="15" :value="pokemon.stats[1]"><strong>{{pokemon.stats[1]}}</strong></v-progress-linear>
                        Defense
                        <v-progress-linear height="15" :value="pokemon.stats[2]" color="light-blue"><strong>{{pokemon.stats[2]}}</strong></v-progress-linear>
                        Speed
                        <v-progress-linear :value="pokemon.stats[5]" height="15" color="light-green lighten-2"><strong>{{pokemon.stats[5]}}</strong></v-progress-linear>
                      </div>
                    </v-col>
                  </v-row>
                </v-sheet>
              </v-carousel-item>
            </v-carousel>
          </div>
        </v-col>
      </v-row>
    </v-parallax>

  </div>
  
</template>

<script>
export default {
  data () {
      return {
        pokemonsBanner: [],
        slides: [
          'First',
          'Second',
          'Third',
          'Fourth',
          'Fifth',
        ],
      }
    },

    methods: {
      editApi(pokemon, data){
            pokemon.id = data.id
            pokemon.name = pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)
            pokemon.types = data.types
            pokemon.sprite = data.sprites.front_default


            const baseStats = []

            data.stats.map(stat =>{
              baseStats.push(stat.base_stat)
            })

            pokemon.stats = baseStats

            return pokemon
        },

        getPokemonApi(){
          
          this.pokemonList = []
          fetch(`https://pokeapi.co/api/v2/pokemon?limit=5`).then(response => response.json())
            .then(data => data.results.map(pokemon =>{
              fetch(pokemon.url).then(response => response.json())
                .then(detailedData => {
                  this.pokemonsBanner.push(this.editApi(pokemon, detailedData))

                })
          }))
        }

    },
      
    

    mounted(){
      this.getPokemonApi()
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

.parallax-title{
  font-size: 2em;
  font-family: 'Montserrat', sans-serif;
}

.parallax-text{
  font-size: 1.4em;
  font-family: 'Montserrat', sans-serif;
}

.intro-text {
  font-size: 2em;
  font-family: 'Montserrat', sans-serif;
  font-weight: bold;
  position: absolute;
  top: 20%;
  left: 50%;
  right: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
  width: 80%;
  text-align: center;
}


.icon-banner{
  width: 2.4em;
}


h4#subtitle.overline.subtitle{
  font-size: 1em !important
}

div.v-sheet.theme--light {
  border-radius: 10% !important;
}


@media screen and (max-width: 600px) {
        .intro-text, .parallax-title{
          font-size: 1.2em;
        }
        .parallax-text{
          font-size: 1em;
        }
        .intro-img{
          height: 45em;
        }
    }   

</style>