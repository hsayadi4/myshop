<template>
    <div class="register">
      <h1>Inscription</h1>
      <form @submit.prevent="register">
        <label>Nom :</label>
        <input type="text" v-model="name" required />
  
        <label>Email :</label>
        <input type="email" v-model="email" required />
  
        <label>Mot de passe :</label>
        <input type="password" v-model="password" required />
  
        <button type="submit">S'inscrire</button>
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        name: '',
        email: '',
        password: '',
      };
    },
    methods: {
      register() {
        axios.post('http://localhost:3000/register', {
          name: this.name,
          email: this.email,
          password: this.password,
        })
          .then(response => {
            console.log("Inscription réussie :", response.data);
            // Redirige l'utilisateur vers la page de connexion
          })
          .catch(error => {
            console.error("Erreur d'inscription :", error);
          });
      },
    },
  };
  </script>
  
  <style scoped>
  /* Ajoute ton style ici */
  </style>
  