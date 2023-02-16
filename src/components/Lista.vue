<template>
  <ul>
    <li v-for="empresa in empresas" :key="empresa.id" class="item" @click="() => onClick(empresa)">
      <div class="card-container">
        <div class="card-info">
          <p>{{ empresa.name }}</p>
          <div class="card-detalhe">
            <p>CNPJ: {{ empresa.cnpj }}</p>
            <p class="hífen"> - </p>
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
  props: { empresas: Array },
  methods: {
    onClick(empresa) {
      this.$emit("onClick", empresa);
    },
  },
};
</script>

<style scoped>
.item {
  cursor: pointer;
}

.card-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 95%;
  height: 3.5rem;
  margin: 0 auto 0.75rem auto;
  border: 1px solid #ffffff;
  border-radius: 35px 4px 4px 35px;
  background: url("/public/img/Note.svg") no-repeat;
  background-color: #FFFFFF;
  background-position: left;
  background-position-x: 0.5rem;
}

.card-info {
  margin-left: 4.5rem;
  text-align: left;
  font-weight: 400;
  font-size: 16px;
  color: #616161;
  line-height: 20px;
}

.hífen {
  padding: 0 0.375rem;
}

.card-detalhe {
  display: flex;
}

li {
  list-style: none;
}

.card-btn {
  display: flex;
  gap: 1rem;
}
</style>