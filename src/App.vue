<script setup>
import { RouterView, RouterLink } from 'vue-router';
</script>

<template>
  <nav class="navbar">
    <ul class="menu">
      <RouterLink to="/" class="link btn">Home</RouterLink>
      <RouterLink to="/phone" class="link btn">Phone</RouterLink>
      <RouterLink to="/movie" class="link btn">Movie</RouterLink>
      <RouterLink to="/post" class="link btn">Post</RouterLink>
      <RouterLink to="/tv" class="link btn">Tv</RouterLink>
    </ul>
  </nav>
  <div class="container">
    <RouterView />
  </div>
</template>

<nav class="navbar">
  
</nav>

<style scoped>
.navbar {
  background-color: #001f4d; 
  padding: 15px 30px; 
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3); 
}

.menu {
  display: flex;
  justify-content: space-between;
}

.link {
  color: #ffffff;
  padding: 10px 15px; 
  border-radius: 5px; 
  text-decoration: none;
  transition: background-color 0.3s ease; 
}

.link:hover {
  background-color: #003366;
}

</style>