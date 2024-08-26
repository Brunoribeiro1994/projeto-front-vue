<template>
    <div class="p-4">
      <h1 class="text-2xl font-bold mb-4">Lista de Usuários</h1>
      <input v-model="query" placeholder="Enter search term" class="border p-2 mb-4"/>
      <button @click="search" class="bg-blue-500 text-white p-2">Buscar</button>
      <ul class="mt-4">
        <li v-for="user in users" :key="user.id" class="border p-2 my-2">
          <router-link :to="{ name: 'UserDetails', params: { id: user.id } }">
            {{ user.name }}
          </router-link>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        query: '',
        users: [],
      };
    },
    methods: {
      async search() {
        const response = await axios.get(`https://jsonplaceholder.typicode.com/users`);
        this.users = response.data.filter(user => 
          user.name.toLowerCase().includes(this.query.toLowerCase())
        );
      },
    },
    mounted() {
      // Carregar todos os usuários quando o componente for montado
      this.search();
    },
  };
  </script>
  
  <style scoped>
  /* Estilos específicos para o componente */
  </style>
  