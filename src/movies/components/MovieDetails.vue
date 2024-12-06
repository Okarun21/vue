<script setup>
import { RouterLink,useRoute } from 'vue-router';
import { ref } from 'vue';
import axios from 'axios';

//TODO: TRaer todos los datos de una pelicula en particular por su id    
const movie = ref(null);
const error = ref(null);
const route = useRoute();
const api_key = 'df47d5296dfd08d97ac5519faa2478ad'; 

const fetchMovieDetails = async () => {
    const movieId = route.params.id; 
    try {
        const response = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}?api_key=${api_key}`);
        movie.value = response.data; 
    } catch (err) {
        error.value = 'Error al obtener los detalles de la película: ' + err.message;
    }
};

fetchMovieDetails();
</script>

<template>
    <div class="container mt-4">
        <h3>Detalles de la Película</h3>
        <div v-if="error" class="alert alert-danger">{{ error }}</div>
        <div v-else-if="movie" class="card">
            <div class="row g-0">
                <div class="col-md-4">
                    <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" class="img-fluid rounded-start" alt="Poster de la película" />
                </div>
                <div class="col-md-8">
                    <div class="card-body">
                        <h4 class="card-title">{{ movie.title }}</h4>
                        <p><strong>Fecha de Estreno:</strong> {{ movie.release_date }}</p>
                        <p><strong>Resumen:</strong> {{ movie.overview }}</p>
                        <p><strong>Calificación:</strong> {{ movie.vote_average }}</p>
                    </div>
                </div>
            </div>
        </div>
        <div v-else>Cargando...</div>
        <RouterLink class="btn btn-light mt-3 mb-3" to="/movie">Volver</RouterLink>
    </div>
</template>

<style scoped>
.card {
    display: flex;
    flex-direction: row;
}
.img-fluid {
    max-width: 100%;
    height: auto;
}
</style>