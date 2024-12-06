<script setup>

import { ref} from 'vue';
import { RouterLink } from 'vue-router';

const base_url = `https://fakestoreapi.in/api/products/category?type=mobile`;
const products = ref([]);

const fetchProducts = async () => {
    try {
        const response = await fetch(base_url);
        const data = await response.json();
        products.value = data.products; 
    } catch (error) {
        console.error('Error al obtener los productos:', error);
    }
};

fetchProducts(); 

</script>

<template>
    <div id="" class="container">
        <h2 class="display-6 mt-3" >Phones</h2>
        <div class="product-list">
            <template v-for="product in products" :key="product.id">
                <div class="card" style="width: 18rem; margin-bottom: 20px;">
                    <img :src="product.image" class="card-img-top" alt="Imagen de {{ product.title }}" />
        
                    <div class="card-body">
                        <h5 class="card-title">{{ product.title }}</h5>
                        <RouterLink :to="`/phone/${product.id}`" class="btn btn-primary">Ver Detalles</RouterLink>
                    </div>
                </div>
            </template>
        </div>
    </div>
</template>

<style>
.product-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
}

.card {
    margin: 10px;
}
</style>