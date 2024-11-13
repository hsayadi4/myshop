<template>
    <div class="home">
      <h1>Bienvenue dans notre boutique !</h1>
      <div v-if="products.length">
        <div v-for="product in products" :key="product.id" class="product-card">
          <h3>{{ product.name }}</h3>
          <p>{{ product.description }}</p>
          <p>Prix : {{ product.price }}€</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        products: [],
      };
    },
    mounted() {
      axios.get('http://localhost:3000/get')
        .then(response => {
          this.products = response.data;
        })
        .catch(error => {
          console.error("Erreur de récupération des produits :", error);
        });
    },
  };
  </script>
  
  <style scoped>
  /* Ajoute ton style ici */
  </style>
  