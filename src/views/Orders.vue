<template>
  <main>
    <h1 class="title">Gerenciar pedidos</h1>
    <Dashboard />
  </main>
</template>

<script>
  import Dashboard from '../components/Dashboard.vue';

  export default {
    name: "Requests",
    components: {
      Dashboard
    }
  }
</script>

<style scoped>
  h1 {
    margin-top: 50px;
  }
</style>