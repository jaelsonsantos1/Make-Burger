<template>
  <Banner />
  <div class="main-container">
    <h1 id="monte-hamburguer">Monte seu burger!</h1>
    <BannerForm />
  </div>
</template>

<script>
import Banner from "../components/banner.vue"
import BannerForm from "../components/burguerForm.vue"

export default {
  name: 'Home',
  components: {
      Banner,
      BannerForm
  }
}
</script>


<style scoped>
  .main-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>