<template>
    <div class="container">
        <div id="button-container">
            <button v-on:click="prevPage" v-if="this.currentPage > 1" id="prevButton">Previous Page</button>
            <button v-on:click="nextPage" id="nextButton" v-if="this.currentPage < this.allPages">Next Page</button>
        </div>

        <div v-for="movie in movies" v-bind:key="movie.id" class="movie-container">
            <div class="text-container">
                <h2 class="title"> {{ movie.original_title }} </h2>
                <p class="overview"> {{ movie.overview }}</p>
            </div>
            <div class="image-container">
                <img class="poster" v-bind:alt="'Poster for ' + movie.original_title"
                     v-bind:src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path">
            </div>
        </div>
    </div>
</template>

<script>
    import axios from "axios";

    //let this.currentPage = 1;

    export default {
        name: "Card",
        props: {
            apiKey: {
                type: String,
            }
        },
        methods: {
            fetchMovieList(apiKey, currentPage) {
                axios.get(`https://api.themoviedb.org/3/movie/now_playing?api_key=${apiKey}&language=en-US&page=${currentPage}`)
                    .then(res => {
                        this.movies = res.data.results;
                        this.allPages = res.data.total_pages;
                        //console.log(this.movies);
                        //console.log(this.allPages)
                    });
            }
            ,
            nextPage() {
                console.log("forth " + this.currentPage);
                this.currentPage += 1;
                this.fetchMovieList(this.apiKey, this.currentPage);
            }
            ,
            prevPage() {
                console.log("back " + this.currentPage);
                if (this.currentPage > 1) {
                    this.currentPage -= 1;
                }
                this.fetchMovieList(this.apiKey, this.currentPage);
            }
        }
        ,
        data:
            function () {
                return {
                    movies: [],
                    allPages: Number,
                    currentPage: 1,
                }
            }
        ,
        mounted() {
            this.fetchMovieList(this.apiKey, 1);
        }
    }
</script>

<style scoped>
    .container {
    }

    #button-container {
    }

    .movie-container {
        border: 1px blue solid;
        margin: auto;
        display: flex;
        justify-content: space-between;
        text-align: left;
        max-width: 1200px;
    }

    .movie-container:nth-child(odd) {
        flex-direction: row-reverse;
        text-align: right;
    }

    .text-container .image-container {
        margin: 4px;
        padding: 4px;
    }

    .text-container {
        border: 1px red solid;
    }

    .image-container {
        border: 3px green solid;
        float: right;
    }


    .title {
    }

    .overview {
    }

</style>
