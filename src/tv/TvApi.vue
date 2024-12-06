<script setup>
import { ref } from 'vue';
import { RouterLink } from 'vue-router';

const api_key = 'df47d5296dfd08d97ac5519faa2478ad'
const base_url = `https://api.themoviedb.org/3/tv/popular?api_key=${api_key}`


const nowplaying = ref([])
const getNowPlayingTvs = async () => {
    const resp = await fetch(base_url);
    const data = await resp.json()
    nowplaying.value = data.results.map((tvshow) => {
        return {
            id: tvshow.id,
            title: tvshow.name,
            overview: tvshow.overview,
            poster_path: tvshow.poster_path
        }
    })
}

getNowPlayingTvs()

</script>

<template>
    <div class="container">
        <h3 class="display-6 mt-3">Most Popular TV Shows</h3>
        <div class="tv-list">
            <template v-for="t in nowplaying" :key="t.id">
                <div class="card" style="width: 18rem; margin-bottom: 20px;">
                    <img :src="`https://image.tmdb.org/t/p/w500${t.poster_path}`" class="card-img-top"
                        alt="Poster of {{ t.title }}" />
                    <div class="card-body">
                        <h5 class="card-title">{{ t.title }}</h5>
                        <RouterLink class="btn btn-primary" :to="`/tv/${t.id}` ">Ver Detalles</RouterLink>
                    </div>
                </div>
            </template>
        </div>
    </div>
</template>

<style>
.tv-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
}

.card {
    margin: 10px;
}
</style>