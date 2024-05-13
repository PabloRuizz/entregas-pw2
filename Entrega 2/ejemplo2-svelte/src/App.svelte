<script>
  // Importamos la función `writable` de Svelte
  import { writable } from 'svelte/store';

  // Creamos una declaración reactiva para almacenar la lista de tareas
  const tareas = writable([
    { id: 1, nombre: 'Hacer la compra', completada: false },
    { id: 2, nombre: 'Lavar el coche', completada: true },
    { id: 3, nombre: 'Estudiar para el examen', completada: false }
  ]);

  // Creamos una declaración reactiva para almacenar el filtro actual
  const filtro = writable('todas');

  // Declaración de la variable para almacenar el nombre de la nueva tarea
  let nuevaTarea = '';

  // Función para agregar una nueva tarea a la lista
  function agregarTarea() {
    // Verificamos que la nueva tarea no esté vacía
    if (nuevaTarea.trim() === '') return;

    // Generamos una nueva tarea con un ID único y el nombre proporcionado
    const nueva = {
      id: Date.now(),
      nombre: nuevaTarea,
      completada: false
    };

    // Actualizamos la lista de tareas añadiendo la nueva tarea al final
    tareas.update(t => [...t, nueva]);

    // Limpiamos el campo de entrada después de agregar la tarea
    nuevaTarea = '';
  }

  // Función para cambiar el estado de completado de una tarea
  function cambiarEstado(id) {
    // Buscamos la tarea con el ID proporcionado y cambiamos su estado de completado
    tareas.update(t => t.map(tarea => tarea.id === id ? { ...tarea, completada: !tarea.completada } : tarea));
  }

  // Función para eliminar una tarea de la lista
  function eliminarTarea(id) {
    // Filtramos la lista de tareas para eliminar la tarea con el ID proporcionado
    tareas.update(t => t.filter(tarea => tarea.id !== id));
  }

  // Función para cambiar el filtro de tareas
  function cambiarFiltro(nuevoFiltro) {
    filtro.set(nuevoFiltro);
  }
</script>

<!-- Estructura visual del componente -->
<div>
  <h1>Lista de Tareas</h1>
  
  <!-- Formulario para agregar nuevas tareas -->
  <form on:submit|preventDefault="{agregarTarea}">
    <input type="text" bind:value="{nuevaTarea}" placeholder="Agregar nueva tarea">
    <button type="submit">Agregar</button>
  </form>

  <!-- Filtro para mostrar tareas completadas, no completadas o todas -->
  <div>
    <button on:click="{() => cambiarFiltro('todas')}">Todas</button>
    <button on:click="{() => cambiarFiltro('completadas')}">Completadas</button>
    <button on:click="{() => cambiarFiltro('pendientes')}">Pendientes</button>
  </div>

  <!-- Lista de tareas -->
  <ul>
    {#each $tareas.filter(tarea => $filtro === 'todas' || (tarea.completada && $filtro === 'completadas') || (!tarea.completada && $filtro === 'pendientes')) as tarea (tarea.id)}
      <li>
        <input type="checkbox" bind:checked="{tarea.completada}" on:change="{() => cambiarEstado(tarea.id)}">
        <span style="{tarea.completada ? 'text-decoration: line-through' : ''}">{tarea.nombre}</span>
        <button on:click="{() => eliminarTarea(tarea.id)}">Eliminar</button>
      </li>
    {/each}
  </ul>
</div>

<style>
  div {
    text-align: center;
    margin-top: 20px;
  }

  ul {
    list-style: none;
    padding: 0;
  }

  li {
    margin-top: 10px;
  }
</style>
