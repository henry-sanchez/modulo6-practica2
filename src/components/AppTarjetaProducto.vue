<template>
    <div class="container ">
        <div class="row">
            <h4>Productos relacionados</h4>
        </div>
        <div class="row">
            <div class="col" v-for="item in productos" :key="item.id">
                <div class="card" style="width: 18rem;" @click="emitirEvento(item)">
                    <div class="card-body">
                        <h5 class="card-title">{{item.nombre}}</h5>
                        <img :src="item.imagen" alt="" width="250">
                        <p class="card-text">{{item.descripcion}}</p>
                            <div class="producto-relacionado-precio">Precio: {{item.precio}} BOB</div>
                        <div>
                            <div>
                                <div class="color-box" v-for="value in item.colores" :key="value" :style="`background: ${value}`"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'appTarjetaProducto',
    data(){},
    props: ["productos"],
    methods: {
        emitirEvento(item) {
            this.$emit('selected', item)
        }
    },
    computed: {
    },
}
</script>

<style>

</style>