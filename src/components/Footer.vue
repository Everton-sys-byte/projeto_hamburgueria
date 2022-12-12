<template>
    <div class="footer">
        <p>Make your burger &copy; 2022</p>
    </div>
</template>

<script>
    export default {
        name: 'Footer',
    }
</script>


<style scoped>
    .footer {
        position: absolute;
        height: 200px;
        background: #222;
        border-top: 4px solid #111;
        color: #FCBA03;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        bottom: 0;
    }

</style>