<template>
  <v-container class="grey lighten-5" fluid>

    <v-row class=" mb-4 mx-4">

        <v-col cols="12" md="6" sm="6">
            <template >
                <v-text-field
                v-model="search"
                label="Search"
                ></v-text-field>
            </template>
        </v-col>


        <v-tooltip top>
        <template v-slot:activator="{on, attrs}">
            <v-btn small depressed class="mr-5 grey--text" @click="sortBy('person')" v-bind="attrs" v-on="on">
            <v-icon left small>mdi-account</v-icon>
            <span class="caption text-lowercase">By person</span>
            </v-btn>
            
        </template>
        <span>Sort project by person</span>
        </v-tooltip>
    </v-row>

    <v-row>
      <v-col v-for="pokemon in filteredPokemonList" :key="pokemon.name" cols="12" xl="3" lg="3" md="4"  sm="6" :search="search">

        <v-card class="mb-10 text-center fill-height" elevation="6">
            <v-img contain height="150" :src="pokemon.sprite"></v-img>
            <v-divider></v-divider>
            <v-list-item>
              <v-list-item-content class="text-overline">
                <div class="text-overline">
                   #{{pokemon.id}} {{pokemon.name}}
                </div>
              </v-list-item-content>

            </v-list-item>
            <v-card-text>
              <v-row class="pl-3"> 
                <v-col v-for="type in pokemon.types" :key="type.type.name" cols="2" >
                  <div class="icon pa-1" :class="`${type.type.name}`" >
                    <v-img  contain :src="require(`@/assets/${type.type.name}.svg`)"></v-img>
                  </div>
                </v-col>
                <v-spacer></v-spacer>
                <v-col cols="6" right>
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
            </v-card-text>
        </v-card>

      </v-col>
    </v-row>

  </v-container>
</template>




<script>

  export default {

    data(){
      return{
        pokemonList: [],
        filteredlist: [],
        search: ""
      }
    },

    components: {
    },

    methods: {

        getImgSrc(){
            return "@/assets/bug.svg"
        },

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

        filterPokemon(search){
                this.filteredlist = this.pokemonList.filter(pokemon => {return pokemon.name.toUpperCase().startsWith(search.toUpperCase())})
        },

        sortPokemon(){
            this.pokemonList.sort((a,b) => a.id < b.id? -1:1)
        }   

    },

    computed: {
        filteredPokemonList(){
            if (this.search){
                this.filterPokemon(this.search)
                return this.filteredlist
            }else{
                this.sortPokemon()
                return this.pokemonList
            }
        }
    },

    mounted(){
      fetch("https://pokeapi.co/api/v2/pokemon?limit=10").then(response => response.json())
        .then(data => data.results.map(pokemon =>{
          fetch(pokemon.url).then(response => response.json())
            .then(detailedData => {
              this.pokemonList.push(this.editApi(pokemon, detailedData))
            })
      }))
    }

  }
</script>

<style>

.icon {
    border-radius: 100%;
    transition: 200ms all;
}

.icon:hover{
    filter: saturate(200%);
    transform: scale(1.1);
    cursor: default;
}


.bug {
    background: #92BC2C;
    box-shadow: 0 0 20px #92BC2C;
}

.dark {
    background: #595761;
    box-shadow: 0 0 20px #595761;
}

.dragon {
    background: #0C69C8;
    box-shadow: 0 0 20px #0C69C8;
}

.electric {
    background: #F2D94E;
    box-shadow: 0 0 20px #F2D94E;
}

.fire {
    background: #FBA54C;
    box-shadow: 0 0 20px #FBA54C;
}

.fairy {
    background: #EE90E6;
    box-shadow: 0 0 20px #EE90E6;
}

.fighting {
    background: #D3425F;
    box-shadow: 0 0 20px #D3425F;
}

.flying {
    background: #A1BBEC;
    box-shadow: 0 0 20px #A1BBEC;
}

.ghost {
    background: #5F6DBC;
    box-shadow: 0 0 20px #5F6DBC;
}

.grass {
    background: #5FBD58;
    box-shadow: 0 0 20px #5FBD58;
}

.ground {
    background: #DA7C4D;
    box-shadow: 0 0 20px #DA7C4D;
}

.ice {
    background: #75D0C1;
    box-shadow: 0 0 20px #75D0C1;
}

.normal {
    background: #A0A29F;
    box-shadow: 0 0 20px #A0A29F;
}

.poison {
    background: #B763CF;
    box-shadow: 0 0 20px #B763CF;
}

.psychic {
    background: #FA8581;
    box-shadow: 0 0 20px #FA8581;
}

.rock {
    background: #C9BB8A;
    box-shadow: 0 0 20px #C9BB8A;
}

.steel {
    background: #5695A3;
    box-shadow: 0 0 20px #5695A3;
}

.water {
    background: #539DDF;
    box-shadow: 0 0 20px #539DDF;
}

</style>