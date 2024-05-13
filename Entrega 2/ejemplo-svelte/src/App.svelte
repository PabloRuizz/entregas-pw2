<script>
  // Importamos la función `writable` de Svelte para crear una declaración reactiva
  import { writable } from 'svelte/store';

  // Creamos una declaración reactiva llamada `contador`
  const contador = writable(0);

  // Función para incrementar el contador
  function incrementar() {
    // Actualizamos el valor del contador añadiendo 1
    contador.update(n => n + 1);
  }

  // Función para resetear el contador
  function resetear() {
    // Restablecemos el valor del contador a 0
    contador.set(0);
  }
</script>

<!-- Estructura visual del componente -->
<div>
  <h1>Contador: {$contador}</h1>
  <button on:click={incrementar}>Incrementar</button>
  <button on:click={resetear}>Resetear</button>
</div>

<style>
  /* Estilos opcionales */
  div {
    text-align: center;
    margin-top: 20px;
  }
</style>
