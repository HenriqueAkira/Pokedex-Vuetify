<template>
    <nav>
        <v-bottom-navigation  fixed hide-on-scroll grow>
            <v-btn value="recent" router to="/">
            <span>Home</span>

            <v-icon>mdi-home</v-icon>
            </v-btn>

            <v-btn value="favorites" router to="/pokedex">
            <span>Pokemon list</span>

            <v-icon>mdi-pokeball</v-icon>
            </v-btn>

            <v-btn value="nearby" router to="/about">
            <span>About</span>

            <v-icon>mdi-account-group</v-icon>
            </v-btn>
        </v-bottom-navigation>
    </nav>
</template>

<script>
export default {
    data: () => ({ value: 'recent' }),
}
</script>

<style>

</style>