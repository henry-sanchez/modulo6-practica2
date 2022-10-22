<template>
  <app-menu :menu="configuracionPagina"></app-menu>
  <app-producto v-if="producto.id" :producto="producto" :configuracionPagina="configuracionPagina"></app-producto>
  <app-tarjeta-producto :productos="productos" @selected="itemSeleccionado($event)"></app-tarjeta-producto>
  <app-pie-pagina :colorFooter="configuracionPagina.footerColor"/>
</template>

<script>
import AppMenu from '@/components/AppMenu.vue';
import AppProducto from '@/components/AppProducto.vue';
import AppTarjetaProducto from '@/components/AppTarjetaProducto.vue';
import AppPiePagina from '@/components/AppPiePagina';
export default {
  name: 'app',
  data() {
    return {
      producto: {
          id: null,
          imagen: null,
          nombre: null,
          descripcion: null,
          precio: null,
          colores: []
      },
      productos: [],
      configuracionPagina: {
          marca: "MegaDron",
          menuColor: "lightblue",
          footerColor: "slategrey",
          precioEstilos: "background: orangered; color: white; font-weight: bold",
          menus: [
              {
                  etiqueta: "Inicio",
                  url: "?"
              },
              {
                  etiqueta: "Tienda",
                  url: "?"
              }
          ]
      },
    }
  },
  methods: {
    itemSeleccionado(item) {
      this.producto = item;
    }
  },
  computed: {
  },
  async mounted() {
    try {
      const productos = await axios.get(`${process.env.VUE_APP_API_BACKEND}/productos`);
      if (productos.status === 200) {
        this.productos = productos.data;
      } else {
        console.log('No se pudo obtener datos de productos');
      }
    } catch (error) {
      console.error('Error en consumo de API: ', error.message);
    }
  },
  components: {
    AppMenu,
    AppProducto,
    AppTarjetaProducto,
    AppPiePagina,
  }
}
</script>

<style>

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}

.abs-center {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}
</style>
