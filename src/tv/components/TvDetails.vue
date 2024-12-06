<script setup>
import { RouterLink,useRoute } from 'vue-router';
import { ref, onMounted } from 'vue';
import axios from 'axios';

//TODO: TRaer todos los datos de una pelicula en particular por su id    
const tv = ref(null);
const error = ref(null);
const route = useRoute();
const api_key = 'df47d5296dfd08d97ac5519faa2478ad'; // Asegúrate de reemplazar esto con tu clave API real

const fetchtvDetails = async () => {
    const tvId = route.params.id; // Obtener el ID de la película desde los parámetros de la ruta
    try {
        const response = await axios.get(`https://api.themoviedb.org/3/tv/${tvId}?api_key=${api_key}`);
        tv.value = response.data; // Almacenar los datos obtenidos en la variable reactiva
    } catch (err) {
        error.value = 'Error al obtener los detalles de la película: ' + err.message;
    }
};

onMounted(fetchtvDetails);
</script>

<template>
    <div class="container mt-4">
        <h3>Detalles del Tv Show</h3>
        <div v-if="error" class="alert alert-danger">{{ error }}</div>
        <div v-else-if="tv" class="card">
            <div class="row g-0">
                <div class="col-md-4">
                    <img :src="`https://image.tmdb.org/t/p/w500${tv.poster_path}`" class="img-fluid rounded-start" alt="Poster del TV Show" />
                </div>
                <div class="col-md-8">
                    <div class="card-body">
                        <h4 class="card-title">{{ tv.name }}</h4>
                        <p><strong>Fecha de Estreno:</strong> {{ tv.release_date }}</p>
                        <p><strong>Resumen:</strong> {{ tv.overview }}</p>
                        <p><strong>Calificación:</strong> {{ tv.vote_average }}</p>
                    </div>
                </div>
            </div>
        </div>
        <div v-else>Cargando...</div>
        <RouterLink class="btn btn-light  mt-3 mb-3" to="/tv">Volver</RouterLink>
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