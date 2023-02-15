<template>
    <div class="modal">

        <div class="form-top">
            <h1>Cadastrar Empresa</h1>
            <button @click="closeForm"><img src="/img/close.svg" alt="fechar"></button>
        </div>
        <Message :msg="msg" v-show="msg" />
        <div class="form">
            <form id="cadastro-form" @submit="postEmpresa">
                <div class="input-container">
                    <label for="nome">Nome</label>
                    <input type="text" id="nome" name="nome" v-model="nome">
                </div>
                <div class="input-container">
                    <label for="cnpj">CNPJ</label>
                    <input type="text" id="cnpj" name="cnpj" v-model="cnpj">
                </div>
                <div class="input-container">
                    <label for="email">Email</label>
                    <input type="email" id="email" name="email" v-model="email">
                </div>

                <div class="input-container-btn">
                    <div class="input-container-submit">
                        <button type="reset" class="reset-btn"><img src="/img/Trash.svg"></button>
                        <div class="input-container-flex">
                            <input type="reset" class="cancel-btn" value="Cancelar">
                            <input type="submit" class="submit-btn" value="Cadastrar">
                        </div>
                    </div>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Message from "./Message.vue"

export default {
    name: 'Form',
    props: { showForm: Boolean },
    emits: ['aoFecharAviso'],
    components: {
        Message
    },
    data() {
        return {
            nome: null,
            cnpj: null,
            email: null,
            msg: null
        }
    },
    methods: {
        async getEmpresas() {
            const req = await fetch('https://homolog.planetasec.com.br/prova/front/api/clients');
            const data = await req.json();
            console.log(data)
        },

        async postEmpresa(e) {
            e.preventDefault();
            const data = {
                name: this.nome,
                cnpj: this.cnpj,
                email: this.email
            }
            const dataJson = JSON.stringify(data);
            const req = await fetch('https://homolog.planetasec.com.br/prova/front/api/clients', {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });
            const res = await req.json();

            this.msg = `Empresa ${res.name} cadastrada com sucesso`;
            // console.log(res);

            setTimeout(() => this.msg = "", 3000);

            this.nome = ""
            this.cnpj = ""
            this.email = ""
        },
        closeForm() {
            this.$emit('aoFecharAviso')
        }
    },
    mounted() {
        this.getEmpresas()
    }
}

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

.modal {
    width: 319px;
    height: 330px;
    border-radius: 4px;
    background-color: #FFFFFF;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    border: none;
    border-radius: 15px;
    margin: auto;


}

.form {
    padding: 0 1.5rem 1.5rem 1.5rem;
    color: #630A37;
}

.form label {
    font-family: 'Roboto';
    font-weight: 400;
    font-size: 12px;
}

.form-top {
    display: flex;
    justify-content: space-between;
    color: rgba(0, 0, 0, 0.3);
    padding: 0.5rem 1rem;
    border-bottom: 1px solid #DDDDDD;
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
    border: 1px solid #DDDDDD;
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
    border: 1px solid #C7C9CC;
    border-radius: 4px;
    padding: 8px 12px;
    background-color: #FFFFFF;
}

.cancel-btn {
    color: #797979;
    font-weight: 500;
    font-size: 14px;
    border: 1px solid #C7C9CC;
    border-radius: 4px;
    padding: 8px 12px;
    background-color: #FFFFFF;
}

.submit-btn {
    background-color: #630A37;
    color: #FFFFFF;
    font-weight: 500;
    font-size: 14px;
    border-radius: 4px;
    padding: 8px 12px;
    border: none;
}
</style>