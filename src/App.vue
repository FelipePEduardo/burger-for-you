<template>
  <div class="wrapper">
    <Navbar :logo="logo_src" :alt="app_name"/>
    <router-view />

    <Footer />
  </div>
</template>

<script>
  import Navbar from './components/Navbar.vue';
  import Footer from './components/Footer.vue';

  export default {
    components: {
      Navbar,
      Footer
    },
    data() {
      return {
        logo_src: '/src/assets/logo.png',
        app_name: 'Make Your Burguer'
      }
    }
  }
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;

    font-family: Helvetica;
  }

  body {
    background: #e0e0e0;
  }

  .wrapper {
    min-height: 100vh;

    display: grid;
    grid-template-rows: 78px auto 200px;
  }

  main > div {
    max-width: 400px;
    width: 100%;
    margin: 50px auto 50px;
  }

  h1 {
    text-align: center;
    color: #222;
    margin-bottom: 30px;
  }
</style>