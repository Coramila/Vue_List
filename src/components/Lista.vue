<template>
    <ul>
        <li v-for="empresa in empresas" :key="empresa.id">
            <div class="card-container">
                <div class="card-info">
                    <p>{{ empresa.name }}</p>
                    <div class="card-detalhe">
                        <p>CNPJ: {{ empresa.cnpj }} - </p>
                        <p>Email: {{ empresa.email }}</p>
                    </div>
                </div>
            </div>
        </li>
    </ul>
</template>

<script>
export default {
    name: "Lista",
    data() {
        return {
            empresas: null
        }
    },
    methods: {
        async getEmpresas() {
            const req = await fetch("https://homolog.planetasec.com.br/prova/front/api/clients");
            const data = await req.json();
            this.empresas = data;
            console.log(this.empresas)
        }
    },
    mounted() {
        this.getEmpresas();
    },
}
</script>

<style scoped>
.card-container {
    display: flex;
    align-items: center;
    width: 95%;
    height: 3.5rem;
    margin: 0.75rem auto;
    border: 1px solid #FFFFFF;
    border-radius: 35px 4px 4px 35px;
    background-color: #FFFFFF;
    background: url("/public/img/Note.svg") no-repeat;
    background-position: left;
    background-position-x: 0.5rem;
}

.card-info {
    margin-left: 4.5rem;
    text-align: left;
}

.card-detalhe {
    display: flex;
}

li {
    list-style: none;
}
</style>