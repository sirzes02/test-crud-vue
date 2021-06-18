<template>
  <div class="container">
    <div class="card">
      <div class="card-header">Agregar nuevo empleado</div>
      <div class="card-body">
        <form v-on:submit.prevent="addUser">
          <div class="form-group">
            <label for="name">Nombre:</label>
            <input
              type="text"
              class="form-control"
              name="name"
              id="name"
              aria-describedby="helpId"
              placeholder="Nombre"
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
              placeholder="Correo"
              v-model="empleado.correo"
              required
            />
            <small id="helpId" class="form-text text-muted"
              >Escribe el correo del empleado</small
            >
          </div>
          <div class="btn-group" role="group" aria-label="">
            <button type="submit" class="btn btn-success">Agregar</button>
            <button type="reset" class="btn btn-danger">Borrar</button>
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
  methods: {
    async addUser() {
      const dataToSend = {
        nombre: this.empleado.nombre,
        correo: this.empleado.correo,
      };

      try {
        await fetch("http://localhost/empleados/index.php?insertar=1", {
          method: "POST",
          body: JSON.stringify(dataToSend),
        });

        window.location.href = "list";
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
