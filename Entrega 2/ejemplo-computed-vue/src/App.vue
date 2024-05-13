<template>
  <div>
    <p>Contador: {{ contador }}</p>
    <button @click="incrementar">Incrementar</button>
  </div>
</template>

<script setup>
  import { ref } from 'vue';

  // Definimos el contador como una referencia reactiva con valor inicial de 0
  const contador = ref(0);

  // Función para incrementar el contador
  function incrementar() {
    contador.value++;
  }
</script>
