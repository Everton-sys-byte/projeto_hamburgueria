<template>
    <div class="banner">
        <h1>Make your burger</h1>
    </div>
</template>

<script>
    export default {
        name: 'Banner'
    }
</script>

<style scoped>
    .banner {
        background-image: url('../../public/img/burger.jpg');
        height: 550px;
        background-position: 0 -300px;
        background-size: cover;
        display: flex;
        align-items: center;
        flex-direction: start;
    }

    .banner h1 {
        color: #FFF;
        text-align: center;
        font-size: 60px;
        background-color: #222;
        padding: 20px 40px;
    }
</style>