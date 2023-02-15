<template>
    <nav>
        <router-link to="/"><img :src="logo" :alt="alt" id="logo"></router-link>
        <div class="user">
            <p>Nome de Usuário</p>
            <img src="/img/icon-user.svg" alt="Ícone Usuário">
        </div>
    </nav>
</template>

<script>
export default {
    name: "Navbar",
    props: ["logo", "alt"]
}
</script>

<style scoped>
nav {
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #FFFFFF;
    box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);
}

.user {
    display: flex;
    gap: 0.813rem;
    align-items: center;
}
</style>