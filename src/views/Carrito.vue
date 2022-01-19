<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="card bg-warning">
          <div class="card-body">
            <!-- Button trigger modal -->
            <button
              type="button"
              class="btn btn-primary"
              data-bs-toggle="modal"
              data-bs-target="#exampleModal"
            >
              Nuevo Producto
            </button>

            <!-- Modal -->
            <div
              class="modal fade"
              id="exampleModal"
              tabindex="-1"
              aria-labelledby="exampleModalLabel"
              aria-hidden="true"
            >
              <div class="modal-dialog">
                <div class="modal-content">
                  <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">
                      Nuevo Producto
                    </h5>
                    <button
                      type="button"
                      class="btn-close"
                      data-bs-dismiss="modal"
                      aria-label="Close"
                    ></button>
                  </div>
                  <div class="modal-body">
                    <label for="">Ingrese Nombre Producto:</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="producto.nombre"
                    />
                    <br />
                    <label for="">Ingrese Cantidad:</label>
                    <input
                      type="number"
                      class="form-control"
                      v-model="producto.cantidad"
                    />
                    <br />
                    <label for="">Ingrese Precio:</label>
                    <input
                      type="number"
                      step="0.01"
                      class="form-control"
                      v-model="producto.precio"
                    />
                  </div>
                  <div class="modal-footer">
                    <button
                      type="button"
                      class="btn btn-secondary"
                      data-bs-dismiss="modal"
                    >
                      Cerrar
                    </button>
                    <button
                      type="button"
                      class="btn btn-primary"
                      @click="guardarProducto()"
                    >
                      Guardar Producto
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-md-7">
        <div class="card">
          <div class="card-body">
            <h2>Lista de Productos</h2>

            <table class="table table-striped table-hover">
              <thead>
                <tr>
                  <th>ID</th>
                  <th>NOMBRE</th>
                  <th>PRECIO</th>
                  <th>CANTIDAD</th>
                  <th>ACCIONES</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="prod in lista_productos" :key="prod.id">
                  <td>{{ prod.id }}</td>
                  <td>{{ prod.nombre }}</td>
                  <td>{{ prod.precio }}</td>
                  <td>{{ prod.cantidad }}</td>
                  <td></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
      <div class="col-md-5">
        <div class="card bg-danger">
          <div class="card-body">
            <h2>Carrito</h2>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      lista_productos: [],
      producto: {
        nombre: "",
        precio: 0,
        cantidad: 0,
        detalle: "",
      },
    };
  },
  mounted() {
    // 1
    this.listarProductos();
  },
  methods: {
    async listarProductos() {
      const { data } = await axios.get("http://127.0.0.1:8000/api/producto");
      this.lista_productos = data;
    },
    async guardarProducto() {
      await axios.post("http://127.0.0.1:8000/api/producto", this.producto);
      this.listarProductos();
    },
    modificarProducto() {},
    eliminarProducto() {},
  },
};
</script>

<style>
</style>