<template>
    <div id="app">
        <Card v-bind:apiKey="apiKey"></Card>
        <Movie v-bind:apiKey="apiKey"></Movie>
    </div>
</template>

<script>
    import Vue from 'vue'
    import VueRouter from 'vue-router'

    Vue.use(VueRouter);


    import Card from './components/Card/Card.vue'
    import Movie from './components/Movie/Movie.vue'

    export default {
        name: 'app',
        components: {
            Card,
            Movie
        },
        data() {
            return {
                apiKey: '3e1d91fffc7d9af3543cb63572d8475e'
        }
        }
    }
</script>

<style lang="scss">
    #app {
    }
</style>
