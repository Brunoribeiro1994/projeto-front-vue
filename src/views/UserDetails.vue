<template>
    <div class="p-4">
      <h1 class="text-2xl font-bold mb-4">Detalhes do Usuário</h1>
      <div v-if="user" class="border p-4">
        <p><strong>Nome:</strong> {{ user.name }}</p>
        <p><strong>Email:</strong> {{ user.email }}</p>
        <p><strong>Telefone:</strong> {{ user.phone }}</p>
        <p><strong>Website:</strong> {{ user.website }}</p>
        <p><strong>Empresa:</strong> {{ user.company.name }}</p>
        <p><strong>Endereço:</strong> {{ user.address.street }}, {{ user.address.city }}</p>
      </div>
      <router-link to="/" class="text-blue-500">Voltar para a lista de usuários</router-link>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  
  export default {
    setup() {
      const user = ref(null);
      const route = useRoute();
  
      onMounted(async () => {
        const response = await axios.get(`https://jsonplaceholder.typicode.com/users/${route.params.id}`);
        user.value = response.data;
      });
  
      return { user };
    },
  };
  </script>
  
  <style scoped>
  /* Estilos específicos para o componente */
  </style>
  