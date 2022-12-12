<template>

  <!-- todos os componentes que se repetem (Nav, Footer) ficam aqui em App.vue-->
  <Navbar/>
  <!-- a view é impressa nesta tag <router-view>, que são os componentes que estão dentro do direitório views -->
  <router-view/>
  <Footer/>
</template>

<script>
  import Navbar from '@/components/Navbar.vue';
  import Footer from '@/components/Footer.vue';

  export default {
    components: {
      Navbar,
      Footer,
    }
  }
</script>

<style>

</style>
