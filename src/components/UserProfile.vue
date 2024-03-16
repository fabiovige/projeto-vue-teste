<template>
    <div v-if="user">
      <h1>{{ user.name }}</h1>
      <p>{{ user.bio }}</p>
      <p>{{ user.blog }}</p>
      <img :src="user.avatar_url" alt="User avatar" />
    </div>
    <div v-else>
      <p>Usuário não encontrado.</p>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'UserProfile',
    data() {
      return {
        user: null
      };
    },
    methods: {
      fetchUserData() {
        axios.get('https://api.github.com/users/fabiovige')
          .then(response => {
            this.user = response.data;
          })
          .catch(error => {
            console.error("Erro ao buscar dados do usuário:", error);
          });
      }
    },
    mounted() {
      this.fetchUserData();
    }
  };
  </script>
  