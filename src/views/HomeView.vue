<template>
  <div class="home">
    <button @click="adicionarEmpresa($event)">Adicionar Empresa</button>
    <Form v-if="showForm" :showForm="showForm" @aoFecharAviso="closeForm" />
  </div>
</template>

<script>

import Form from '../components/Form.vue'
export default {
  name: "HomeView",
  components: {
    Form,
  },
  data(props) {
    return {
      showForm: false,
    }
  },
  methods: {
    adicionarEmpresa(e) {
      e.preventDefault();
      console.log("FUI CLICADO")
      this.showForm = true
    },
    closeForm() {
      this.showform = false
      console.log('FUI FECHADO' + this.showform)
    }
  }
}

</script>

<style scoped>
.home {
  background-color: #F7F7F7;
  width: 100vw;
  height: 100vh;
}
</style>
