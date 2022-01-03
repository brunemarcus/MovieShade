<template>
    <div v-if="!error.status">
        <div class="col-sm-3 mb-3">
            <div class="row">
                <select class="form-select mb-3" @change="filterMovies($event)">
                    <option value="0" selected>Filtrar resultado...</option>
                    <option value="5" v-text="5"></option>
                    <option value="10" v-text="10"></option>
                    <option value="15" v-text="15"></option>
                </select>
            </div>
        </div>
        <div class="col-">
            <div class="row">
                <div class="card mb-3" style="width: 18rem;margin-right:3%;" v-for="item in popularMovies" :key="item.original_title">
                    <img class="card-img-top" v-bind:src="'https://image.tmdb.org/t/p/original/' + item.poster_path">
                    <div class="card-body">
                        <h5 class="card-title" v-text="item.original_title"></h5>
                        <p class="card-text text-truncate" v-text="item.overview"></p>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div v-else>
        <div class="alert alert-danger d-flex" role="alert">
            <h4 v-text="error.message"></h4>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        name: "app",
        data() {
            return {
                popularMovies: {},
                filter: 0,
                Page: 1,
                error: {
                    status: false,
                    message: "Erro ao consultar filmes, aguarde alguns instantes!"
                }
            }
        },
        methods: {
            filterMovies(event) {
                this.filter = event.target.value
                this.getMovies()
            },
            getMovies() {
                axios.get('https://api.themoviedb.org/3/movie/popular?api_key='+ process.env.VUE_APP_API_KEY +'&language=en-US&page=1')
                .then((response) => {
                    if(this.filter == 0) this.popularMovies = response.data.results
                    else this.popularMovies = response.data.results.slice(0,this.filter)
                })
                .catch((err) => {
                    console.log(err)
                    this.error.status = true
                })
            }
        },
        mounted: function(){
            this.getMovies()
        }
    }
</script>