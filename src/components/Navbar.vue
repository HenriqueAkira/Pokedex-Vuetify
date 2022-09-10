<template>
  <nav>
    <v-app-bar flat app>

        <v-app-bar-nav-icon @click="drawer = !drawer" class="grey--text d-none d-md-block" ></v-app-bar-nav-icon>

        <v-toolbar-title class="text-uppercase grey--text title">
            <v-icon color="red">mdi-pokemon-go</v-icon>
            <span class="font-weight-light">Pokedex</span>
            <span> Vue</span>
        </v-toolbar-title>

        <v-spacer></v-spacer>

        <a v-for="midia in midias" :key="midia.text" target="self" :href="midia.link" class="d-none d-sm-block">
            <v-btn text color="grey" class="text-sm-caption text-xs-caption"> 
                <span class="d-none d-md-block">{{midia.text}}</span>
                <v-icon >{{midia.icon}}</v-icon>
            </v-btn>
        </a>
    </v-app-bar>

    <v-navigation-drawer app class="primary" temporary v-model="drawer">  
        <v-list>
            <v-list-item v-for="link in links" :key="link.text" router :to="link.route">
                <v-list-item-action>
                    <v-icon class="white--text">{{link.icon}}</v-icon>
                </v-list-item-action>
                <v-list-item-content>
                    <v-list-item-title class="white--text ">{{link.text}}</v-list-item-title>
                </v-list-item-content>
            </v-list-item>
        </v-list>
    </v-navigation-drawer>

  </nav>
</template>

<script>


export default {
    components:{
    },

    data(){
        return{
            drawer: false,
            links: [
                {icon: 'mdi-home', text: 'Home', route:'/'},
                {icon: 'mdi-pokeball', text: 'Pokedex', route:'/pokedex'},
                {icon: 'mdi-account-group', text: 'About', route:'/about'},
            ],
            midias:[
                {icon: 'mdi-linkedin', text: 'Linkedin', link: "https://www.linkedin.com/in/henrique-akira-yasuda/"},
                {icon: 'mdi-github', text: 'Github', link: "https://github.com/HenriqueAkira"},
                {icon: 'mdi-instagram', text: 'Instagram', link: "https://www.instagram.com/henriqueyasuda/"},
            ]
        }
    },
    
    methods:{
    },


}
</script>

<style>

    a{
        text-decoration: none;
    }


    @media screen and (max-width: 600px) {
        .title span{
            font-size: 0.56em;
        }
    }   


</style>