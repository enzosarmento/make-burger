<template>
  <div class="banner">
    <h2>Make Your Buger</h2>
    <img :src="burger" alt="">
  </div>
</template>

<script>

export default {
  name: 'Banner',
  props: ['burger']
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