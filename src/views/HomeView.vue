<template>
  <div class="home">
    <form class="filtro" @submit.prevent="getEmpresas">
      <input type="text" placeholder="Buscar empresa..." v-model="filtro" />
    </form>

    <Form v-if="showForm" :showForm="showForm" @aoFecharAviso="closeForm" @aoDeletar="deleteEmpresa"
      @aoSubmeterForm="salvarEmpresa" :empresa="empresaSelecionada" />
    <button class="add-empresa" @click="adicionarEmpresa($event)">
      Adicionar Empresa
    </button>
    <Lista @onClick="openForm" :empresas="empresas" />

  </div>
</template>

<script>
import Form from "../components/Form.vue";
import Lista from "@/components/Lista.vue";
import axios from 'axios'
export default {
  name: "HomeView",
  components: {
    Form,
    Lista,
  },
  data() {
    return {
      filtro: "",
      empresas: [],
      showForm: false,
      empresaSelecionada: null,
    };
  },
  mounted() {
    this.getEmpresas();
  },
  watch: {
    filtro: function (novoFiltro) {
      if (novoFiltro === '') {
        this.getEmpresas();
      }
    }
  },

  methods: {

    async getEmpresas() {
      let url = "https://homolog.planetasec.com.br/prova/front/api/clients";
      if (this.filtro) {
        url += '?text=' + this.filtro
      }

      const res = await axios.get(url);
      this.empresas = res.data;
    },


    async deleteEmpresa(id) {
      const res = await axios.delete(
        `https://homolog.planetasec.com.br/prova/front/api/clients/${id}`
      );
      this.closeForm();
    },

    openForm(empresa) {
      this.showForm = true;
      this.empresaSelecionada = empresa;
    },
    adicionarEmpresa(e) {
      e.preventDefault();
      this.showForm = true;
    },
    closeForm() {
      this.showForm = false;
      this.empresaSelecionada = null;
      this.getEmpresas();
    },
    async salvarEmpresa(empresa) {
      if (this.empresaSelecionada) {
        const res = await axios.put(
          `https://homolog.planetasec.com.br/prova/front/api/clients/${this.empresaSelecionada.id}`,
          empresa
        );
        this.msg = `Empresa ${res.data.name} cadastrada com sucesso`;
      } else {
        const res = await axios.post(
          "https://homolog.planetasec.com.br/prova/front/api/clients",
          empresa
        );
        this.msg = `Empresa ${res.data.name} cadastrada com sucesso`;
      }
      this.closeForm();
    },
  },
};
</script>

<style scoped>
.home {
  background-color: #f7f7f7;
  text-align: center;
  /* width: 100%;*/
  height: 100vh;
  padding: 2rem;
  margin: 0 auto;
}

.filtro {
  text-align: right;
  margin: 0 auto;
  width: 95%;
}

.filtro input {
  width: 281px;
  height: 28px;
  border: 1px solid #DDDDDD;
  border-radius: 4px;
  background: url("/public/img/search.svg") no-repeat;
  background-color: #FFFFFF;
  background-position: right;
  background-position-x: 16rem;
  padding: 0.888rem;
}

.filtro input::placeholder {
  font-weight: 400;
  font-size: 14px;
}

.add-empresa {
  width: 95%;
  height: 3.5rem;
  margin: 0.75rem auto;
  border: 1px solid #dddddd;
  border-radius: 35px 4px 4px 35px;
  color: #969696;
  font-family: "Jost";
  font-weight: 500;
  font-size: 14px;
  letter-spacing: 1.25px;
  background: url("/public/img/NoteGray.svg") no-repeat;
  background-position: left;
  background-position-x: 0.5rem;
  transition: 15ms;
}

.add-empresa:hover {
  border: 2px solid #630A37;
  color: #630A37;
}

@media (max-width: 768px) {
  .filtro {
    text-align: center;
  }
}
</style>
