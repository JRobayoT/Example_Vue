<template>
    <div>
      <h2>Formulario de Producto</h2>
      <form @submit.prevent="agregarProducto">
        <label for="name">Nombre del Producto:</label>
        <input type="text" id="name" v-model="nombreProducto" required>
  
        <label for="available">Disponible:</label>
        <input type="number" id="available" v-model.number="disponible" required>
  
        <label for="price">Precio:</label>
        <input type="number" id="price" v-model.number="precio" required>
  
        <button type="submit">Agregar Producto</button>
      </form>
  
      <h2>Tabla de Productos</h2>
      <table>
        <thead>
          <tr>
            <th>Nombre del Producto</th>
            <th>Disponible</th>
            <th>Precio</th>
            <th>Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(producto, index) in productos" :key="index">
            <td>{{ producto.nombre }}</td>
            <td>
              <input type="number" v-model.number="producto.disponible">
              <span v-if="producto.disponible > 0">Unidades</span>
              <span v-else>Sin Unidades</span>
            </td>
            <td>{{ producto.precio }}</td>
            <td>
              <button @click="eliminarProducto(index)">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        nombreProducto: '',
        disponible: 0,
        precio: 0,
        productos: []
      };
    },
    methods: {
      agregarProducto() {
        this.productos.push({
          nombre: this.nombreProducto,
          disponible: this.disponible,
          precio: this.precio
        });
        // Limpiar los campos del formulario después de agregar un producto
        this.nombreProducto = '';
        this.disponible = 0;
        this.precio = 0;
      },
      eliminarProducto(index) {
        this.productos.splice(index, 1);
      }
    }
  };
  </script>
  
  <style scoped>
  table {
    width: 100%;
    border-collapse: collapse;
  }
  
  th, td {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
  }
  
  th {
    background-color: #f2f2f2;
  }
  </style>
  