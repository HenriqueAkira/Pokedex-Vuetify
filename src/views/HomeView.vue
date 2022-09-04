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
        pokemonList: [{img:"@/assets/logo.png", name:"Pikachu", content:"Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quidem qui commodi ipsam modi molestiae nobis est, assumenda explicabo, dignissimos rerum incidunt quam beatae doloremque alias voluptates, nihil impedit placeat esse!"},
        {img:"@/assets/logo.png", name:"Pikachu2", content:"Lorem ipsum doing elit. Quidem qui commodi ipsam modi molestiae nobis est, assumenda explicabo, dignissimos rerum incidunt quam beatae doloremque alias voluptates, nihil impedit placeat esse!"},
        {img:"@/assets/logo.png", name:"Pikachu3", content:"sit, amet consectetur adipisicing elit. Quidem qui commodi ipsam modi molestiae nobis est, assumenda explicabo, dignissimos rerum incidunt quam beatae doloremque alias voluptates, nihil impedit placeat esse!"}]
      }
    },

    components: {
    },
  }
</script>
