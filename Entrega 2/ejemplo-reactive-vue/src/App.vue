<template>
    <div>
      <p>Contador: {{ contador }}</p>
      <button @click="incrementar">Incrementar</button>
    </div>
  </template>
  
  <script setup>
    import { reactive } from 'vue';
  
    // Definimos el estado del componente como un objeto reactiva
    const state = reactive({
      contador: 0
    });
  
    // Función para incrementar el contador
    function incrementar() {
      state.contador++;
    }
  </script>
  