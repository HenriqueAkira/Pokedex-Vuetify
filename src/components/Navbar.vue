<template>
    <nav>
        <v-bottom-navigation v-model="value" fixed hide-on-scroll horizontal>
            <v-btn value="recent">
            <span>Recent</span>

            <v-icon>mdi-history</v-icon>
            </v-btn>

            <v-btn value="favorites">
            <span>Favorites</span>

            <v-icon>mdi-heart</v-icon>
            </v-btn>

            <v-btn value="nearby">
            <span>Nearby</span>

            <v-icon>mdi-map-marker</v-icon>
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