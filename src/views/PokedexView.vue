<template>
  <v-container class="grey lighten-5" fluid>
     <v-dialog
      persistent
      v-model="loading"
      max-width="600px"
      transition="dialog-transition"
    >
     
     <v-img src="@/assets/pokemon-pokeball.gif" ></v-img>
      
    </v-dialog>
    <v-row class=" mb-4 mx-4">
        <v-col cols="12" md="3" sm="3">
            <template >
                <v-text-field
                v-model="search"
                label="Search"
                ></v-text-field>
            </template>
        </v-col>

        <v-col  cols="12" md="2" sm="6">
          <v-select
            v-model="typeFilter"
            :items="types"
            chips
            label="Types"
            multiple
            solo
          ></v-select>
        </v-col>

        <v-col>
          <v-tooltip top>
          <template v-slot:activator="{on, attrs}">
            <v-btn small depressed class="mr-5 grey--text" @click="sortBy('id')" v-bind="attrs" v-on="on">
              <v-icon left small>mdi-account</v-icon>
              <span class="caption text-lowercase">By id</span>
            </v-btn>
              
          </template>
          <span>Sort pokemons by Id</span>
          </v-tooltip>
          <v-tooltip top>
            <template v-slot:activator="{on, attrs}">
              <v-btn small depressed class="mr-5 grey--text" @click="sortBy('name')" v-bind="attrs" v-on="on">
                <v-icon left small>mdi-account</v-icon>
                <span class="caption text-lowercase">By name</span>
              </v-btn>
                
            </template>
            <span>Sort pokemons by name</span>
          </v-tooltip>
        </v-col>

    </v-row>

    <p v-if="filteredPokemonList.length == 0">Results not found</p>
    <v-row>
      <v-col v-for="pokemon in filteredPokemonList" :key="pokemon.name" cols="12" xl="3" lg="3" md="4"  sm="6" :search="search">

        <v-card class="mb-10 text-center fill-height " elevation="6">
            

            <v-img
              :style="{backgroundColor:pokemon.avgColor}"
              :src="pokemon.sprite"
              :lazy-src="pokemon.sprite"
            >
              <template v-slot:placeholder>
                <v-row
                  class="fill-height ma-0"
                  align="center"
                  justify="center"
                >
                  <v-progress-circular
                    indeterminate
                    color="grey lighten-5"
                  ></v-progress-circular>
                </v-row>
              </template>
            </v-img>

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
    <div class="text-center">
      <v-pagination
        :length="120"
        :total-visible="7"
        v-model="page"
        circle
        @input="next"
      ></v-pagination>
    </div>

  </v-container>

  
</template>




<script>

  import analyze from 'rgbaster'

  export default {

    data(){
      return{
        pokemonList: [],
        filteredlist: [],
        search: "",
        types:["normal", "fire", "water", "grass", "flying", "fighting", "poison", "electric", 
        "ground", "rock", "psychic", "ice", "bug", "ghost", "steel", "dragon", "dark", "fairy"],
        typeFilter: [],
        loading: true,
        page: 1,
        ascending: true,
      }
    },

    components: {
    },

    methods: {

        editApi(pokemon, data){
            pokemon.id = data.id
            pokemon.name = pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)
            pokemon.types = data.types
            pokemon.sprite = data.sprites.front_default
            const result = analyze(pokemon.sprite)
            result.then(result => pokemon.avgColor = result[0].color);

            const baseStats = []

            data.stats.map(stat =>{
            baseStats.push(stat.base_stat)
            })

            pokemon.stats = baseStats

            return pokemon
        },

        next(){
          this.getPokemonApi((this.page - 1) * 8)
        },

        filterPokemonSearch(search){
            this.filteredlist = this.filteredlist.filter(pokemon => {return pokemon.name.toUpperCase().startsWith(search.toUpperCase())})
        },

        filterPokemonTypes(){
            this.filteredlist = this.filteredlist.filter(pokemon => {
              var valid = false
              pokemon.types.forEach(type => {
                this.typeFilter.forEach(typeFilter =>{
                  if(type.type.name == typeFilter){
                     valid = true
                  }
                })
              });
              return valid
              })
        },

        resetFilter(){
          this.filteredlist = this.pokemonList
        },

        sortBy(prop){
          if(!this.ascending){
            this.pokemonList.sort((a,b)=> a[prop] < b[prop] ? -1 : 1)
            this.ascending = true
          }else{
            this.pokemonList.sort((a,b)=> a[prop] < b[prop] ? 1 : -1)
            this.ascending = false
          }
        },

        getPokemonApi(offset){
          this.loading = true 
          this.pokemonList = []
          fetch(`https://pokeapi.co/api/v2/pokemon?limit=14&offset=${offset}`).then(response => response.json())
            .then(data => data.results.map(pokemon =>{
              fetch(pokemon.url).then(response => response.json())
                .then(detailedData => {
                  this.pokemonList.push(this.editApi(pokemon, detailedData))

                })
          }))
        setTimeout(() => {
          this.loading = false
          
        }, 3500);
        }
        

    },

    computed: {
        filteredPokemonList(){
            var filters = []

            this.resetFilter()

            if (this.typeFilter.length != 0){
              filters.push("type")
              this.filterPokemonTypes(this.types)
            }
            
            if (this.search != ""){
              filters.push("search")
              this.filterPokemonSearch(this.search)
            }

            if(filters.length == 0){
              return this.pokemonList
            }else{
              return this.filteredlist
            }
        }
    },

    mounted(){
      this.getPokemonApi(0)
    },

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

