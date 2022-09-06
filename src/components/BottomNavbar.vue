<template>
    <nav>
        <v-bottom-navigation  fixed hide-on-scroll >
            <v-btn value="recent">
            <span>Home</span>

            <v-icon>mdi-home</v-icon>
            </v-btn>

            <v-btn value="favorites">
            <span>Pokemon list</span>

            <v-icon>mdi-pokeball</v-icon>
            </v-btn>

            <v-btn value="nearby">
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