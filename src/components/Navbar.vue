<template>
    <nav>
        <router-link to="/" class="logo-url">
            <img :src="logo" :alt="alt" class="logo">
        </router-link>

        <router-link to="/">Home</router-link> 
        <router-link to="/pedidos">Pedidos</router-link>
    </nav>
</template>

<script>

    export default {
        name: 'Navbar',
        props: {
            logo: String,
            alt: String,
        }
    }

</script>

<style scoped>
    nav {
        padding: 15px 50px;
        background: #222;
        border-bottom: 4px solid #111;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }

    .logo-url {
        margin: auto;
        margin-left: 0;
    }

    .logo {
        width: 40px;
        height: 40px;
    }

    nav a {
        color: #FCBA03;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
    }

    nav a:hover {
        color: #FFF
    }

</style>