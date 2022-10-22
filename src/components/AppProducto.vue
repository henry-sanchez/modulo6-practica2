<template>
    <div class="container">
        <div class="row">
            <h3>{{producto.nombre}}</h3>
        </div>
        <div class="row">
            <div class="col-12 col-sm-6 col-md-4 ">
                <img :src="producto.imagen"
                    alt="" width="250">
            </div>
            <div class="col-12 col-sm-6  col-md-8">
                <h6>{{producto.descripcion}}</h6>
                <div class="p-3 mb-2 text-white" :style="`${configuracionPagina.precioEstilos}`">
                    Precio: {{producto.precio}} BOB
                </div>
                <h5>Color</h5>
                <div>
                    <div
                        v-for="(value, key) in producto.colores"
                        :key="key"
                        class="color-box clic"
                        :style="`background: ${value}`"
                        @click="pedido.color = value"
                    ></div>
                </div>
                <h5>Cantidad</h5>
                <div class="quantity">
                    <button @click="modificarCantidad(-1, producto.id)">-</button> <div>{{pedido.cantidad}}</div> <button @click="modificarCantidad(1, producto.id)">+</button>
                </div>
                <div class="buy-box">
                    <button @click="comprar" type="button" class="btn btn-primary" :disabled="pedido.cantidad === 0">Comprar</button>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'appProducto',
    data() {
        return {
            pedido: this.resetData(),
        }
    },
    watch: {
        producto (newItem, oldItem)  {
            if (newItem.id != oldItem.id) {
                this.pedido = this.resetData();
            }
        }
    },
    props: ["producto", "configuracionPagina"],
    methods: {
        resetData () {
            return {
                id: null,
                cantidad: 0,
                color: null,
            };
        },
        modificarCantidad(value, idProducto) {
            if (this.pedido.cantidad === 0 && +value === -1) return;
            this.pedido.cantidad += +value;
            this.pedido.id = idProducto;
        },
        comprar() {
            if (!this.pedido.color) {
                alert('Primero debe elegir un color!');
                return;
            }
            const mensaje = `Datos de producto comprado:\n
            Id producto: ${this.pedido.id}\n
            Cantidad: ${this.pedido.cantidad}\n
            Color: ${this.pedido.color}`;
            alert(mensaje);
        }
    },
    computed: {
    },
}
</script>

<style>

</style>