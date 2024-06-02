<template>
  <div>
    <h2>Detalles del Producto</h2>
    <p>Nombre del Producto: {{ producto.nombre }}</p>
    <p>Precio Unitario: ${{ producto.precio }}</p>
    <p>Cantidad: <input type="number" v-model="cantidad"></p>
    <p>Precio Total: ${{ precioTotal }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      producto: {
        nombre: 'Camisa',  
        precio: 25.99      
      },
      cantidad: 1          // Cantidad inicial del producto
    };
  },
  computed: {
    // Propiedad computada para mostrar el precio total
    precioTotal() {
      return this.producto.precio * this.cantidad;
    }
  },
  watch: {
    // Vigila cambios en la cantidad
    cantidad(newCantidad) {
      // Actualiza el precio total cuando cambia la cantidad
      this.actualizarPrecioTotal(newCantidad);
    }
  },
  methods: {
    // Método para actualizar el precio total
    actualizarPrecioTotal(cantidad) {
      this.precioTotal = this.producto.precio * cantidad;
    }
  }
};
</script>
