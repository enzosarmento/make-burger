<template>
  <div class="container">
    <h1>Monte o seu hamburger:</h1>
    <Form/>
  </div>
</template>

<script>
import Form from '../components/Form.vue'


export default {
  name: 'Home',
  props: ['burger'],
  components: {
    Form
  }
}
</script>

<style scoped>

  .banner {
    position: relative;
  }

  .banner img {
    width: 100%;
    height: 50rem;

    object-fit: cover;
  }

  .banner h2 {
    color: #FFF;
    font-size: 4rem;
    padding: 1.75rem;
    background-color: #222;

    position: absolute;
    top: 23rem;
    
  }
</style>