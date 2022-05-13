<template>
    <div class="container">
        <img :src="getLogoUrl()" :alt="logo.nombre" class="logo">
        <h1>Carta de comida</h1>
    </div>
</template>

<script>
export default {
    data() {
        return {
            logo: {
                nombre: "logo.png",
            }
        }
    },
    methods: {
        getLogoUrl(){
            return require(`@/assets/images/${this.logo.nombre}`);
        }
    }
}
</script>

<style scoped>

    h1 {
        color: #008ea7d7;
        text-decoration: underline;
    }

    .logo{
        height: auto;
        width: auto;
    }
    .container{
        text-align: center;
    }

</style>