<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const posts = ref([]);

const fetchPosts = async () => {
    try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts');
        posts.value = response.data;
    } catch (error) {
        console.error('Error al obtener los posts:', error);
    }
};

onMounted(fetchPosts);
</script>

<template>
  <div class="container mt-4">
    <h3>Lista de Posts</h3>
    <div class="row">
      <div class="col-md-4" v-for="post in posts" :key="post.id">
        <div class="card mb-4">
          <div class="card-body">
            <h5 class="card-title">{{ post.title }}</h5>
            <p class="card-text">{{ post.body }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>