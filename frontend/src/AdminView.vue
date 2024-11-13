<template>
    <div class="admin">
      <h1>Gestion des produits</h1>
      <div v-if="products.length">
        <div v-for="product in products" :key="product.id" class="product-card">
          <h3>{{ product.name }}</h3>
          <button @click="deleteProduct(product.id)">Supprimer</button>
        </div>
      </div>
      <h2>Ajouter un produit</h2>
      <form @submit.prevent="addProduct">
        <label>Nom :</label>
        <input type="text" v-model="newProduct.name" required />
  
        <label>Prix :</label>
        <input type="number" v-model="newProduct.price" required />
  
        <label>Description :</label>
        <textarea v-model="newProduct.description"></textarea>
  
        <button type="submit">Ajouter le produit</button>
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        products: [],
        newProduct: {
          name: '',
          price: 0,
          description: '',
        },
      };
    },
    mounted() {
      this.fetchProducts();
    },
    methods: {
      fetchProducts() {
        axios.get('http://localhost:3000/get')
          .then(response => {
            this.products = response.data;
          })
          .catch(error => {
            console.error("Erreur de récupération des produits :", error);
          });
      },
      deleteProduct(id) {
        axios.delete(`http://localhost:3000/delete/${id}`)
          .then(() => {
            this.fetchProducts();
          })
          .catch(error => {
            console.error("Erreur de suppression du produit :", error);
          });
      },
      addProduct() {
        axios.post('http://localhost:3000/post', this.newProduct)
          .then(() => {
            this.fetchProducts();
            this.newProduct = { name: '', price: 0, description: '' };
          })
          .catch(error => {
            console.error("Erreur d'ajout du produit :", error);
          });
      },
    },
  };
  </script>
  
  <style scoped>
  /* Ajoute ton style ici */
  </style>
  