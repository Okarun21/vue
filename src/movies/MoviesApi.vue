<script setup>
import { ref } from 'vue';
import { RouterLink } from 'vue-router';

const api_key = 'df47d5296dfd08d97ac5519faa2478ad'
const base_url = `https://api.themoviedb.org/3/movie/popular?api_key=${api_key}`

const nowplaying = ref([])
const getNowPlayingMovies = async () => {
    const resp = await fetch(base_url);
    const data = await resp.json()
    nowplaying.value = data.results.map((movie) => {
        return {
            id: movie.id,
            title: movie.title,
            overview: movie.overview,
            poster_path: movie.poster_path
        }
    })
}

getNowPlayingMovies()

</script>


<template>
    <div class="container">
        <h3 class="display-6 mt-3">Most Popular Movies</h3>
        <div class="movie-list">
            <template v-for="m in nowplaying" :key="m.id">
                <div class="card" style="width: 18rem; margin-bottom: 20px;">
                    <img :src="`https://image.tmdb.org/t/p/w500${m.poster_path}`" class="card-img-top"
                        alt="Poster of {{ m.title }}" />
                    <div class="card-body">
                        <h5 class="card-title">{{ m.title }}</h5>
                        <RouterLink class="btn btn-primary" :to="`/movie/${m.id}`">Ver Detalles</RouterLink>
                    </div>
                </div>
            </template>
        </div>
    </div>
</template>

<style>
.movie-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
}

.card {
    margin: 10px;
}
</style>