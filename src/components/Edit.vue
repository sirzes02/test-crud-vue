<template>
  <div class="container">
    <div class="card">
      <div class="card-header">Editar empleado</div>
      <div class="card-body">
        <form v-on:submit.prevent="updateUser">
          <div class="form-group">
            <label for="name">Nombre:</label>
            <input
              type="text"
              class="form-control"
              name="name"
              id="name"
              aria-describedby="helpId"
              placeholder="Name"
              v-model="empleado.nombre"
              required
            />
            <small id="helpId" class="form-text text-muted"
              >Escribe el nombre del empleado</small
            >
          </div>
          <div class="form-group">
            <label for="name">Correo:</label>
            <input
              type="email"
              class="form-control"
              name="email"
              id="email"
              aria-describedby="helpId"
              placeholder="Email"
              v-model="empleado.correo"
              required
            />
            <small id="helpId" class="form-text text-muted"
              >Escribe el correo del empleado</small
            >
          </div>
          <div class="btn-group" role="group" aria-label="">
            <button type="submit" class="btn btn-success">Modificar</button>
            <router-link :to="{ name: 'List' }" class="btn btn-warning"
              >Cancelar</router-link
            >
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      empleado: {},
    };
  },
  created: function() {
    this.fetchUser();
  },
  methods: {
    async fetchUser() {
      try {
        const response = await fetch(
          `http://localhost/empleados/index.php?consultar=${this.$route.params.id}`
        );
        const data = await response.json();
        this.empleado = data[0];
      } catch (error) {
        console.error(error);
      }
    },
    async updateUser() {
      const dataToSend = {
        id: this.$route.params.id,
        nombre: this.empleado.nombre,
        correo: this.empleado.correo,
      };

      try {
        await fetch(
          `http://localhost/empleados/index.php?actualizar=${dataToSend.id}`,
          {
            method: "POST",
            body: JSON.stringify(dataToSend),
          }
        );

        window.location.href = "../list";
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
