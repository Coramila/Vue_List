<template>
  <Navbar :logo="logo_src" :alt="app_name" />

  <router-view />
</template>

<script>
import Navbar from './components/Navbar.vue';

export default {
  components: {
    Navbar
  },
  data() {
    return {
      logo_src: "/img/logoopea.svg",
      app_name: "Cadastro Empresas"
    }
  }


}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Jost:wght@400;500&display=swap');

* {
  font-family: 'Jost';
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

button:hover {
  cursor: pointer;
}
</style>
