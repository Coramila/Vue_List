<template>
    <div class="message-container">
        <p>{{ msg }}</p>
    </div>
</template>

<script>
export default {
    name: "Message",
    props: {
        msg: String
    }
}
</script>

<style scoped>
.message-container {
    color: #004085;
    /* background-color: #cce5ff;
    border: 2px solid #b8daff;
    border-radius: 5px;
    padding: 0.625rem; */
    max-width: 25rem;
    font-size: 12px;
    position: absolute;
    padding-left: 1.5rem;
    /* margin: 1.875rem auto;
    text-align: center; */
}
</style>