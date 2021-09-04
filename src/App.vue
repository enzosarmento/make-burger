<template>
  <Navbar :logo="logo" :alt="alt"/>
  <Banner :burger="burger"/>
  <router-view/>
  <Footer/>
</template>

<script>

import Navbar from './components/Navbar.vue'
import Banner from './components/Banner.vue'
import Footer from './components/Footer.vue'

export default {
  components: {
    Navbar,
    Banner,
    Footer
  },
  data() {
    return {
      logo: 'img/logo.png',
      alt: 'Logo',
      burger: 'img/burger.jpg'
    }
  }
}
</script>


<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;

    font-family: Helvetica, sans-serif;
  }

  .container {
    margin: 3rem 4rem 0 4rem;
    height: 100vh;
  }

  h1 {
    text-align: center;
    color: #222;
    font-size: 2.625rem;
  }
</style>
