<template>
  <div class="background"></div>
  <div class="modal">
    <div class="form-top">
      <h1>Cadastrar Empresa</h1>
      <button @click="closeForm">
        <img src="/img/close.svg" alt="fechar" />
      </button>
    </div>
    <Message :msg="msg" v-show="msg" />
    <div class="form">
      <form id="cadastro-form" @submit="postEmpresa">
        <div class="input-container">
          <label for="nome">Nome</label>
          <input type="text" id="nome" name="nome" v-model="nome" required />
        </div>
        <div class="input-container">
          <label for="cnpj">CNPJ</label>
          <input type="text" id="cnpj" name="cnpj" v-model="cnpj" minlength="14" maxlength="14" required />
        </div>
        <div class="input-container">
          <label for="email">Email</label>
          <input type="email" id="email" name="email" v-model="email" required />
        </div>

        <div class="input-container-btn">
          <div class="input-container-submit">
            <button type="reset" class="reset-btn" @click="deletar" :disabled="!empresa">
              <img src="/img/Trash.svg" />
            </button>
            <div class="input-container-flex">
              <input type="button" @click="closeForm" class="cancel-btn" value="Cancelar" />
              <input type="submit" class="submit-btn" value="Cadastrar" />
            </div>
          </div>
        </div>
      </form>
    </div>
</div>
</template>

<script>
import Message from "./Message.vue";

export default {
  name: "Form",
  props: { showForm: Boolean, empresa: Object, msg: String },
  emits: ["aoFecharAviso", "aoDeletar", "aoSubmeterForm"],
  components: {
    Message,
  },
  data() {
    return {
      nome: this.empresa ? this.empresa.name : null,
      cnpj: this.empresa ? this.empresa.cnpj : null,
      email: this.empresa ? this.empresa.email : null,
      msg: null,
    };
  },
  methods: {
    async getEmpresas() {
      const req = await fetch(
        "https://homolog.planetasec.com.br/prova/front/api/clients"
      );
      const data = await req.json();
    },
    postEmpresa(e) {
      e.preventDefault();
      this.$emit("aoSubmeterForm", {
        name: this.nome,
        cnpj: this.cnpj,
        email: this.email,
      });

      this.nome = "";
      this.cnpj = "";
      this.email = "";
    },
    closeForm() {
      this.nome = "";
      this.cnpj = "";
      this.email = "";
      this.$emit("aoFecharAviso");
    },
    deletar() {
      this.$emit("aoDeletar", this.empresa.id);
    },
  },
  mounted() {
    this.getEmpresas();
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");

.background {
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.8);
}

.modal {
  position: absolute;
  width: 319px;
  height: 330px;
  border-radius: 4px;
  background-color: #ffffff;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  border: none;
  border-radius: 15px;
  left: 50%;
  transform: translateX(-50%);
}

.form {
  padding: 0 1.5rem 1.5rem 1.5rem;
  color: #630a37;
}

.form label {
  font-family: "Roboto";
  font-weight: 400;
  font-size: 12px;
  text-align: left;
}

.form-top {
  display: flex;
  justify-content: space-between;
  color: rgba(0, 0, 0, 0.3);
  padding: 0.5rem 1rem;
  border-bottom: 1px solid #dddddd;
  align-items: center;
}

.form-top h1 {
  font-weight: 400;
  font-size: 16px;
}

.form-top button {
  background-color: #ffffff;
  border: none;
}

.input-container {
  display: flex;
  flex-direction: column;
  padding-top: 1rem;
}

.input-container input {
  padding: 1rem;
  height: 1.875rem;
  box-sizing: border-box;
  height: 36px;
  left: 0px;
  right: 0px;
  top: 16px;
  border: 1px solid #dddddd;
  border-radius: 2px;
}

.input-container-submit {
  display: flex;
  justify-content: space-between;
  margin-top: 2rem;
  align-items: center;
}

.input-container-flex {
  display: flex;
  gap: 1rem;
}

.reset-btn {
  text-align: center;
  color: #797979;
  font-weight: 500;
  font-size: 14px;
  border: 1px solid #c7c9cc;
  border-radius: 4px;
  padding: 8px 12px;
  background-color: #ffffff;
  cursor: pointer;
  transition: 15ms;
}

.reset-btn:hover {
  border-color: #630a37;
}

.cancel-btn {
  color: #797979;
  font-weight: 500;
  font-size: 14px;
  border: 1px solid #c7c9cc;
  border-radius: 4px;
  padding: 8px 12px;
  background-color: #ffffff;
  cursor: pointer;
  transition: 15ms;
}

.cancel-btn:hover {
  border-color: #630a37;
}

.submit-btn {
  background-color: #630a37;
  color: #ffffff;
  font-weight: 500;
  font-size: 14px;
  border-radius: 4px;
  padding: 8px 12px;
  border: none;
  cursor: pointer;
  transition: 15ms;
}

.submit-btn:hover {
  opacity: 0.8;
}
</style>