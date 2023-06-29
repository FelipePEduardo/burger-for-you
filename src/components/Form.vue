<template>
  <div>
    <Message :msg="msg" v-show="msg"/>
    <div>
      <form @submit="createBurguer">
        <div class="input-container">
          <label for="name">Nome do cliente:</label>
          <input 
            type="text" 
            id="name" 
            placeholder="Digite o seu nome" 
            v-model="name"
          >
        </div>

        <div class="input-container">
          <label for="bread">Escolha o pão:</label>
          <select id="bread" v-model="bread">
            <option value="">Selecione o seu pão</option>
            <option v-for="bread in breads" :key="bread.id" :value="bread.type">{{ bread.type }}</option>
          </select>
        </div>

        <div class="input-container">
          <label for="meat">Escolha a carne do seu hamburguer:</label>
          <select id="meat" v-model="meat">
            <option value="">Selecione o tipo de carne</option>
            <option v-for="meat in meats" :key="meat.id" :value="meat.type">{{ meat.type }}</option>
          </select>
        </div>

        <div class="input-container optional-container">
          <label for="optional">Selecione os opcionais:</label>

          <div class="options-container">
            <div class="checkbox-container" v-for="item in optionalData" :key="item.id">
              <input type="checkbox" id="optional" v-model="optional" :value="item.type">
              <span>{{ item.type }}</span>
            </div>
          </div>
        </div>

        <button type="submit">Criar meu hamburguer</button>
      </form>
    </div>
  </div>
</template>

<script>
  import Message from './Message.vue'

  export default {
    name: "Form",
    components: {
      Message
    },
    data() {
      return {
        breads: null,
        meats: null,
        optionalData: null,
        name: null,
        bread: null,
        meat: null,
        optional: [],
        msg: null,
      }
    },
    methods: {
      async getIngredients() {  
        const res = await fetch('http://localhost:3000/ingredients')
        const data = await res.json()

        this.breads = data.breads
        this.meats = data.meats
        this.optionalData = data.optional
      },

      async createBurguer(e) {
        e.preventDefault()

        const formHamburguerData = {
          name: this.name,
          meat: this.meat,
          bread: this.bread,
          optional: Array.from(this.optional),
          status: "Solicitado",
        }

        const formHamburguerDataJSON = JSON.stringify(formHamburguerData)

        const res = await fetch('http://localhost:3000/burgers', {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: formHamburguerDataJSON
        })
        
        const data = await res.json()

        this.msg = `Pedido N° ${data.id} realizado com sucesso`

        setTimeout(() => this.msg = "", 3000)
        
        this.name = ''
        this.meat = ''
        this.bread = ''
        this.optional = ''
      }
    },
    mounted() {
      this.getIngredients()
    }
  }
</script>

<style scoped>
  form {
    max-width: 400px;
    width: 100%;
    margin: 0 auto;
  }

  .input-container {
    display: flex;
    flex-direction: column;

    margin-bottom: 20px;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
  }

  input[type=text], select {
    padding: 5px 10px;
    width: 300px;
  }

  .options-container {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }

  .checkbox-container {
    width: 100%;
    display: flex;
    align-items: flex-start;
    gap: 8px;
  }

  .checkbox-container span {
    font-weight: bold;
  }

  button {
    width: 100%;
    background: #222;
    border: 0;
    border-radius: 6px;

    color: #fcba03;
    font-weight: bold;

    padding: 15px;

    display: flex;
    align-items: cente;
    justify-content: center;

    cursor: pointer;
    transition: 0.1s;
  }

  button:hover {
    background: #111;
    color: white;
  }
</style>