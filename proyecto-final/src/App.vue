<template>
    <div id="app">
        <Titulo/>
        <Carrito ref="miCarrito"/>
        <div class="row">
            <div class="col centrado" v-for="(item) in productos" :key="item.id">
                <Producto :id="item.id" :nombre="item.nombre" :precio="item.precio" :imagen="item.imagen" :favorito="item.favorito" @agregar-al-carrito="AgregarAlCarrito"/>
            </div>
        </div>
    </div>
</template>

<script>
import Producto from './components/Producto.vue'
import Carrito from './components/Carrito.vue'
import Titulo from './components/Titulo.vue';

export default {
    name: 'App',
    components: { Producto, Carrito, Titulo },
    data() {
        return {
            productos:[
                {
                    id: 1,
                    nombre: "Milanesa Napolitana",
                    precio: 990,
                    imagen: "mila-napo.png",
                    favorito: false,
                },
                {
                    id: 2,
                    nombre: 'Hamburguesa Completa',
                    precio: 950,
                    imagen: "hamburguesa.jpg",
                    favorito: true,
                },
                {
                    id: 3,
                    nombre: "Picada Especial",
                    precio: 1980,
                    imagen: "picada.jpg",
                    favorito: false,
                }
            ]}
        },
    methods:{
        AgregarAlCarrito(id) {
            let result = this.productos.find((prod) => {
                return prod.id == id;
            });
            if (result) {
                this.$refs.miCarrito.AgregarProducto(result);
            }
        },
    }
}
</script>

<style>

.centrado{
    text-align: center;
}

</style>
