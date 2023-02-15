<template>
  <div class="home">
    <div class="filtro">
      <input type="text" placeholder="Buscar empresa...">
    </div>
    <Form v-if="showForm" :showForm="showForm" @aoFecharAviso="closeForm" :empresa="empresaSelecionada"/>
    <button class="add-empresa" @click="adicionarEmpresa($event)">Adicionar Empresa</button>
    <Lista @onClick="openForm"/>
  </div>
</template>

<script>

import Form from '../components/Form.vue'
import Lista from '@/components/Lista.vue';
export default {
  name: "HomeView",
  components: {
    Form,
    Lista,
  },
  data(props) {
    return {
      showForm: false,
      empresaSelecionada: null
    }
  },
  methods: {
    openForm (empresa) {
      this.showForm = true
      this.empresaSelecionada = empresa
    },
    adicionarEmpresa(e) {
      e.preventDefault();
      console.log("FUI CLICADO")
      this.showForm = true
    },
    closeForm() {
      this.showForm = false
      this.empresaSelecionada = null
      console.log('FUI FECHADO' + this.showform)
    }
  }
}

</script>

<style scoped>
.home {
  background-color: #F7F7F7;
  text-align: center;
  /* width: 100%;*/
  height: 100vh;
  padding: 2rem;
  margin: 0 auto;

}

.filtro {
  text-align: right;
  padding-right: 3rem;
  margin: 0 auto;

}

.add-empresa {
  width: 95%;
  height: 3.5rem;
  margin: 0.75rem auto;
  border: 1px solid #DDDDDD;
  border-radius: 35px 4px 4px 35px;
  color: #969696;
  font-family: 'Jost';
  font-weight: 500;
  font-size: 14px;
  letter-spacing: 1.25px;
  background: url("/public/img/NoteGray.svg") no-repeat;
  background-position: left;
  background-position-x: 0.5rem;
}
</style>
