<template>
  <div class="grillaProducto">
        <img
            v-if="producto.favorito"
            src="@/assets/images/star.png"
            alt="favorito"
            class="favorito"
            @click="cambiarFav()"
        />
        <img
            v-if="!producto.favorito"
            src="@/assets/images/graystar2.png"
            alt="favorito"
            class="favorito"
            @click="cambiarFav()"
        />
        <img
            :alt="producto.nombre"
            :src="getImgUrl()"
            class="imgGrilla"
        />
        <h4>{{ producto.nombre }}</h4>
        <div>Stock: {{ producto.cantidad }}</div>
        <div>$ {{ producto.precio }}</div>
        <button
        class="botonAgregarCarrito"
        @click="AgregarAlCarrito()">
        Agregar
        </button>
  </div>
</template>

<script>
export default {
    props:{
        producto: {
            type: Object,
            required: true
        },
    },
    methods: {
        getImgUrl() {
            return require(`@/assets/images/${this.producto.imagen}`);
        },
        AgregarAlCarrito() {
            this.$emit("agregar-al-carrito", this.producto);
        },
        cambiarFav() {
            this.$emit("cambiar-fav", this.producto.id);
        }
    },

}
</script>

<style scoped>

.grillaProducto{
    position: relative;
    width: 300px;
    height: 300px;
    box-shadow: 0 0 10px rgba(45, 75, 100, 0.7);
    background-color: rgba(149, 184, 214, 0.7);
    color: black;
    padding: 5px;
    margin: auto;
    border-radius: 10px;
    cursor: pointer;
    text-align: center;
    z-index: 1;
}

.favorito {
    position: absolute;
    top: 5px;
    left: 5px;
    width: 40px;
}

.imgGrilla {
    max-width: 100%;
    height: 150px;
}

.grillaProducto:hover {
    box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.7);
}

.botonAgregarCarrito {
    background-color: #01d9ffd7;
    width: 100px;
    border-radius: 10px;
    margin-top: 10px;
    font-size: 1.1em;
    padding: 5px 0;
    border: 1px solid rgba(0, 0, 0, 0.5);
    cursor: pointer;
}

.botonAgregarCarrito:hover {
    background-color: #0aa19ad0;
}

</style>