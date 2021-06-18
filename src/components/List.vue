<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        Empleados
      </div>
      <div class="card-body">
        <table class="table">
          <thead>
            <tr>
              <th>ID</th>
              <th>Nombre</th>
              <th>Correo</th>
              <th>Acciones</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="empleado in empleados" :key="empleado.id">
              <td scope="row">{{ empleado.id }}</td>
              <td>{{ empleado.nombre }}</td>
              <td>{{ empleado.correo }}</td>
              <td>
                <div class="btn-group" role="group" aria-label="">
                  <router-link
                    :to="{ name: 'Edit', params: { id: empleado.id } }"
                    class="btn btn-info"
                    >Editar</router-link
                  >
                  <button
                    type="button"
                    v-on:click="deleteUser(empleado.id)"
                    class="btn btn-danger"
                  >
                    Borrar
                  </button>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      empleados: [],
    };
  },
  created: function() {
    this.fetchUsers();
  },
  methods: {
    async fetchUsers() {
      try {
        const response = await fetch("http://localhost/empleados/index.php");
        const data = await response.json();

        this.empleados = data;
      } catch (error) {
        console.error(error);
      }
    },
    async deleteUser(id) {
      try {
        await fetch(`http://localhost/empleados/index.php?borrar=${id}`);
        this.fetchUsers();
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
