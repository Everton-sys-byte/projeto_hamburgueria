<template>

  <!-- todos os componentes que se repetem (Nav, Footer) ficam aqui em App.vue-->
  <Navbar :logo="logo_source" :alt="app_name"/>

  <!-- a view é impressa nesta tag <router-view>, que são os componentes que estão dentro do direitório views -->
  <router-view/>

  <!-- todos os componentes que se repetem (Nav, Footer) ficam aqui em App.vue-->
  <Footer/>
</template>

<script>
  import Navbar from '@/components/Navbar.vue';
  import Footer from '@/components/Footer.vue';

  export default {
    components: {
      Navbar,
      Footer,
    },

    data() {
      return {
        logo_source: '/img/logo.png',
        app_name: 'Hamburgueria',
      }
    }


  }
</script>

<style>

*{
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  font-family: Helvetica;
}

.main-container {
  margin: 50px;
  min-height: 500px;
}

h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}

</style>
