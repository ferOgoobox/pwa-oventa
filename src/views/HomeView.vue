<script setup lang="ts">

  import { ref, onMounted } from 'vue';

  const products = ref([])


  const getData = () => {
    fetch('https://dummyjson.com/products')
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(data => {
      products.value = data.products
      localStorage.setItem('products', JSON.stringify(data.products))
      console.log(data);
    })
    .catch(error => {
      console.error('catch',error);
      if (!navigator.onLine) {

      products.value = JSON.parse(localStorage.getItem("products"))
      console.log(products);
      }
    });
  }
</script>

<template>
   <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
  </div>
  <h2>OVENTA</h2>
  <button @click="getData()">Obtener productos</button>
  <button @click="products = []">Limpiar</button>

  <ul v-for="product in products" :key="product.id">
    <li >{{ product.title }}</li>
  </ul>

</template>

<style scoped>
</style>
