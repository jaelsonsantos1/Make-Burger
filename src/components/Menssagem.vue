<template>
    <div class="msg-container">
        <p>{{ msg }}</p>
    </div>
</template>

<script>
export default {
    name: 'Menssagem',
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .msg-container {
        color: #004045;
        background: #CCE5FF;
        border: 2px solid #88DAFF;
        border-radius: 5px;
        padding: 10px;
        max-width: 400px;
        margin: 30px auto;
    }
</style>