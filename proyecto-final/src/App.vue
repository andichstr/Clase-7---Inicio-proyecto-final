<template>
    <div id="app">
        <Titulo/>
        <Carrito :productos="this.carrito" @restar-del-carrito="restarDelCarrito"/>
        <div class="row">
            <div class="col centrado" v-for="(item) in productos" :key="item.id">
                <Producto :producto="item" @agregar-al-carrito="agregarAlCarrito" @cambiar-fav="cambiarFavorito"/>
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
                    cantidad: 5,
                },
                {
                    id: 2,
                    nombre: 'Hamburguesa Completa',
                    precio: 950,
                    imagen: "hamburguesa.jpg",
                    favorito: true,
                    cantidad: 8,
                },
                {
                    id: 3,
                    nombre: "Picada Especial",
                    precio: 1980,
                    imagen: "picada.jpg",
                    favorito: false,
                    cantidad: 3,
                }
            ],
            carrito:[],
        }
    },
    methods:{
        agregarAlCarrito(p) {
            let a = this.productos.indexOf(p);
            if (this.productos[a].cantidad > 0){
                this.productos[a].cantidad -= 1;
                let result = this.carrito.find((prod) => {
                return prod.id == p.id;
                });
                if (result) {
                    result.cantidad += 1;
                } else {
                    result = { ...p };
                    result.cantidad = 1;
                    this.carrito.push(result);
                }
            } else {
                console.log("No hay mas stock");
            }
        },
        restarDelCarrito(p){
            let result = this.productos.find((prod) => {
                return prod.id == p.id;
            });
            p.cantidad -= 1;
            result.cantidad +=1;
            const i = this.carrito.indexOf(p);
            if (p.cantidad == 0) {
                this.carrito.splice(i, 1);
            };
        },
        cambiarFavorito(id){
            let result = this.productos.find((prod) => {
                return prod.id == id;
            });
            if (result) {
                result.favorito = !result.favorito;
            }
        },
    },
}
</script>

<style>

.centrado{
    text-align: center;
}

</style>
