<template>
  <v-container class="grey lighten-5" fluid>

    <v-row>
      <v-col v-for="pokemon in pokemonList" :key="pokemon.name" cols="12" md="6" lg="3" sm="6">

        <v-card class="mb-10 text-center fill-height">
            <v-img contain height="150" src="@/assets/logo.png"></v-img>
            <v-divider></v-divider>
            <v-card-title>
              {{pokemon.name}}
            </v-card-title>
            <v-card-text>
              {{pokemon.content}}
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
        pokemonList: []
      }
    },

    components: {
    },

    methods: {
      editApi(data){
        data.map()
      }
    },

    computed: {
    },

    mounted(){
      fetch("https://pokeapi.co/api/v2/pokemon?limit=5").then(response => response.json())
        .then(data => data.results.map(pokemon =>{
          fetch(pokemon.url).then(response => response.json())
            .then(detailedData => {
              console.log(detailedData);
            })
      }))
    }

    

    
  }
</script>
