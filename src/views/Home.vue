<template>
  <div>
    <Banner />
    <main>
      <div>
        <h1>Monte o seu Hamburguer:</h1>
        <Form />
      </div>
    </main>
  </div>
</template>

<script>
  import Banner from '../components/Banner.vue';
  import Form from '../components/Form.vue';

  export default {
    name: "Home",
    components: {
      Banner,
      Form
    }
  }
</script>