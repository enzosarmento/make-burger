<template>
    <div id="nav">
        <nav>
            <route-link to="/">
                <img :src="logo" :alt="alt" id="logo">
            </route-link>
            <div id="menu">
                <router-link to="/">Fazer Pedido</router-link>
                <router-link to="/pedidos">Pedidos</router-link>
            </div>
        </nav>  
  </div>
</template>

<script>
export default {
    name: 'Navbar',
    props: ['logo', 'alt']
}
</script>

<style scoped>
    #nav {
        background-color: #222;
        border-bottom: 4px solid #111;
    }

    nav {
        margin: 0 4rem 2rem 4rem;
        padding-top: 1.5rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    #menu {
        display: flex;
        gap: 1rem;
    }

    #menu a {
        color: #FCBA03;
        text-decoration: none;
        transition: 0.5s;
    }

    #menu a:hover {
        color: #FFF;
    }


    #logo {
        max-width: 3rem;
    }
</style>