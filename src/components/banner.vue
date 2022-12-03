<template>
    <div id="main-banner">
        <h1>JS Burguer 🍟</h1>
    </div>
</template>

<script>
export default {
    name: "Banner"
}
</script>

<style scoped>
    #main-banner {
        background-image: url("C:\Users\jaels\OneDrive\Documentos\Programação\Vue.js\REF\make_burger\public\img\burger.jpg");
        background-position: 0 -250px;
        background-repeat: no-repeat;
        background-size: cover;

        height: 100vh;
        display: flex;
        justify-content: flex-start;
        align-items: center;  
    }

    #main-banner h1 {
        color: #fff;
        background-color: rgb(35, 34, 34);
        font-size: 3em;
        text-align: center;
        padding: 20px 40px;
    }
</style>