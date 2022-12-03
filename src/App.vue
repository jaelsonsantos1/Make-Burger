<template>
  <NavBar :logo="logo_src" :alt="app_name" />
  <router-view />
  <Footer />
</template>

<script>
import NavBar from "./components/Nav.vue"
import Footer from "./components/Footer.vue"

export default {
  components: {
    NavBar,
    Footer
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Make Hamburger"
    }
  }
}
</script>

<style>
  * {
    font-family: Arial, Helvetica, sans-serif;
    padding: 0;
    margin: 0;
    box-sizing: border-box;

  }

  .main-container {
    margin: 50px;
    /* height: 100vh; */
  }

  h1 {
    color: #D84346;
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
  }
</style>