<template>
<div movie-container></div>
</template>

<script>
    import axios from "axios"
    let movieId = 1


    export default {
        name: "Movie",
        props: {
            apiKey: {
                type: String,
            }
        },
        methods: {
            fetchMovieDetails(apiKey, movieId) {
                axios.get(`https://api.themoviedb.org/3/movie/${movieId}?api_key=${apiKey}&language=en-US`)
                    .then(res => {
                        this.movies = res.data.results;
                        console.log(this.movies)
                    })
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>
