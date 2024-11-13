<template>
    <div class="login">
      <h1>Connexion</h1>
      <form @submit.prevent="login">
        <label>Email :</label>
        <input type="email" v-model="email" required />
  
        <label>Mot de passe :</label>
        <input type="password" v-model="password" required />
  
        <button type="submit">Se connecter</button>
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        email: '',
        password: '',
      };
    },
    methods: {
      login() {
        axios.post('http://localhost:3000/login', {
          email: this.email,
          password: this.password,
        })
          .then(response => {
            console.log("Connexion réussie :", response.data);
            // Redirige l'utilisateur vers la page d'accueil ou admin selon le rôle
          })
          .catch(error => {
            console.error("Erreur de connexion :", error);
          });
      },
    },
  };
  </script>
  
  <style scoped>
  /* Ajoute ton style ici */
  </style>
  