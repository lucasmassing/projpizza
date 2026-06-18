<template>
  <div class="main-container">
    <Banner />
    <div class="main-container">
      <h1>Monte a sua pizza:</h1>
      <PizzaForm />
    </div>
  </div>
</template>

<script>
import Banner from '../components/Banner.vue'
import PizzaForm from '../components/PizzaForm.vue'

export default {
   name:"HomeView",
  components:{
    Banner,
    PizzaForm
  }
  
}
</script>

<style scoped>

</style>
