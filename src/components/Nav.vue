<template>
    <div id="nav">
        <router-link to="/" id="logo-url">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>
        <div id="links">
            <router-link to="/">Home</router-link>
            <a href="#monte-hamburguer">Montar pedido</a>
            <router-link to="/pedidos">Pedidos</router-link>
        </div>
    </div>
</template>

<script>
export default {
    name: "NavBar",
    props: ["logo", "alt"]
}
</script>

<style scoped>
    #nav {
        background-color: #171919;
        border-bottom: 4px solid #080606;
        padding: 15px 50px;
        display: flex;
        justify-content:space-between;
        align-items: center;
    }

    #logo {
        width: 40px;
        height: 40px;
    }

    #links a {
        color: #EFA335;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
    }
    
    #links a:hover {
        color: lavender;
    }
</style>