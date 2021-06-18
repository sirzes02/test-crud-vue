<template>
  <nav class="navbar navbar-expand navbar-light bg-light mb-5">
    <div class="nav navbar-nav">
      <router-link class="nav-link" to="/create">Crear</router-link>
      <router-link class="nav-link" to="/">Empleados</router-link>
    </div>
  </nav>
  <router-view />
</template>
