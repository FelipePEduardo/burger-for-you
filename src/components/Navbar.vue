<template>
  <header>
    <router-link to="/">
      <img :src="logo" :alt="alt" class="logo">
    </router-link>

    <div class="navigation">
      <router-link to="/">Home</router-link>

      <router-link to="/pedidos">About</router-link>
    </div>

  </header>
</template>

<script>
  export default {
    name: "Navbar",
    props: ['logo', 'alt']
  }
</script>

<style scoped>
  header {
    background: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;

    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .logo {
    max-width: 40px;
  }

  .navigation {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .navigation a {
    font-size: 14px;
    color: #FCBA03;
    text-decoration: none;
    transition: 0.2s;
  }

  .navigation a:hover {
    color: #fff;
  }
</style>
