<script setup>
import { RouterLink, useRoute } from 'vue-router';
import { ref, onMounted } from 'vue';
import axios from 'axios';

const phone = ref({});
const error = ref(null);
const route = useRoute();

const fetchPhoneDetails = async () => {
    const phoneId = route.params.id; 
    try {
        const response = await axios.get(`https://fakestoreapi.in/api/products/${phoneId}`);
        phone.value = response.data.product; 
    } catch (err) {
        error.value = 'Error al obtener los detalles del móvil: ' + err.message;
    }
};
onMounted(fetchPhoneDetails);
</script>

<template>
    <div class="container mt-4">
        <h3>Detalles del celular</h3>
        <div v-if="error" class="alert alert-danger">{{ error }}</div>
        <div v-else-if="phone" class="card">
            <div class="row g-0">
                <div class="col-md-4">
                    <img :src="phone.image" class="img-fluid rounded-start" alt="Imagen del celular" />
                </div>
                <div class="col-md-8">
                    <div class="card-body">
                        <h4 class="card-title">{{ phone.title }}</h4>
                        <p><strong>Características:</strong> {{ phone.description }}</p>
                        <p><strong>Precio:</strong> {{ phone.price }}</p>
                    </div>
                </div>
            </div>
        </div>
        <div v-else>Cargando...</div>
        <RouterLink class="btn btn-light mt-3 mb-3" to="/phone">Volver</RouterLink>
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