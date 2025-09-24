<template>
  <div class="pagina-maquinaria">
    <h1 style="text-align:center;margin-top:2rem;color:#031641">Maquinaria Agrícola</h1>
    <div class="grid-tienda">
      <template v-if="seleccionado !== null">
        <div style="margin-bottom:2.5rem;">
          <div class="producto-tienda seleccionado">
            <div class="producto-ampliado">
              <div class="ampliado-imagen">
                <img :src="productos[seleccionado].img" :alt="productos[seleccionado].nombre" />
              </div>
              <div class="ampliado-datos">
                <h2 class="titulo-producto">{{ productos[seleccionado].nombre }}</h2>
                <p class="descripcion">{{ productos[seleccionado].desc }}</p>
                <div class="botones-pagina">
                  <button type="button" class="boton-ficha" @click="abrirFicha(productos[seleccionado].nombre)">Ficha técnica</button>
                  <button type="button" class="boton-contactar">Contactar</button>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="grid-tienda-secundaria">
          <div v-for="(prod, idx) in productos" :key="prod.nombre" v-if="idx !== seleccionado" class="producto-tienda" @click="seleccionarProducto(idx)">
            <img :src="prod.img" :alt="prod.nombre" />
            <h2 class="titulo-producto">{{ prod.nombre }}</h2>
            <p class="descripcion">{{ prod.desc }}</p>
            <div class="botones-pagina">
              <button type="button" class="boton-ficha" @click.stop="abrirFicha(prod.nombre)">Ficha técnica</button>
              <button type="button" class="boton-contactar">Contactar</button>
            </div>
          </div>
        </div>
      </template>
      <template v-else>
        <div class="grid-tienda-secundaria">
          <div v-for="(prod, idx) in productos" :key="prod.nombre" class="producto-tienda" @click="seleccionarProducto(idx)">
            <img :src="prod.img" :alt="prod.nombre" />
            <h2 class="titulo-producto">{{ prod.nombre }}</h2>
            <p class="descripcion">{{ prod.desc }}</p>
            <div class="botones-pagina">
              <button type="button" class="boton-ficha" @click.stop="abrirFicha(prod.nombre)">Ficha técnica</button>
              <button type="button" class="boton-contactar">Contactar</button>
            </div>
          </div>
        </div>
      </template>
    </div>
    <div v-if="mostrarFicha" class="overlay-ficha">
      <div class="contenedor-ficha">
        <button class="cerrar-ficha" @click="mostrarFicha = false">&times;</button>
        <iframe class="iframe-ficha" :src="fichaUrl" frameborder="0"></iframe>
      </div>
    </div>
  </div>
</template>

<script>
import '../style/maq_agricola_style.css'
import TS754Img from '../assets/TS-754.png';
import TS254SImg from '../assets/TS-254S.png';
import TS254PImg from '../assets/TS-254P.png';
import TS454Img from '../assets/TS-454.png';
import TS1104Img from '../assets/TS-1104.png';
import TS1604Img from '../assets/TS-1604.png';
export default {
  name: 'MaqAgricolaPage',
  data() {
    return {
      productos: [
        {
          nombre: 'TA-754',
          img: TS754Img,
          desc: 'Tractor robusto y confiable para grandes extensiones agrícolas. Alto rendimiento y durabilidad.'
        },
        {
          nombre: 'TS-254S',
          img: TS254SImg,
          desc: 'Tractor compacto, eficiente y versátil para labores agrícolas. Motor potente y bajo consumo.'
        },
        {
          nombre: 'TS-254P',
          img: TS254PImg,
          desc: 'Tractor versátil y eficiente, ideal para pequeñas y medianas parcelas. Bajo mantenimiento y gran maniobrabilidad.'
        },
        {
          nombre: 'TS454',
          img: TS454Img,
          desc: 'Tractor potente y moderno, diseñado para trabajos exigentes en el campo. Gran capacidad y tecnología avanzada.'
        },
        {
          nombre: 'TS-1104',
          img: TS1104Img,
          desc: 'Tractor de alta potencia y tecnología avanzada, ideal para grandes extensiones y trabajos exigentes.'
        },
        {
          nombre: 'TS-1604',
          img: TS1604Img,
          desc: 'Tractor de última generación, máxima potencia y eficiencia para los retos más grandes del campo.'
        }
      ],
      seleccionado: null,
      mostrarFicha: false,
      fichaUrl: ''
    }
  },
  methods: {
    seleccionarProducto(i) {
      this.seleccionado = i;
      this.$nextTick(() => {
        const ampliado = document.querySelector('.producto-tienda.seleccionado');
        if (ampliado) {
          ampliado.scrollIntoView({ behavior: 'smooth', block: 'center' });
        }
      });
    },
    abrirFicha(producto) {
      if (producto === 'TA-754') {
        this.fichaUrl = '/pdf/ficha_tecnica_maquina_agricola/TRACTOR 754.pdf';
      } else if (producto === 'TS-254S') {
        this.fichaUrl = '/pdf/ficha_tecnica_maquina_agricola/TRACTOR 254S.pdf';
      } else if (producto === 'TS-254P') {
        this.fichaUrl = '/pdf/ficha_tecnica_maquina_agricola/TRACTOR 254P.pdf';
      } else if (producto === 'TS454') {
        this.fichaUrl = '/pdf/ficha_tecnica_maquina_agricola/TRACTOR 454.pdf';
      } else if (producto === 'TS-1104') {
        this.fichaUrl = '/pdf/ficha_tecnica_maquina_agricola/TRACTOR 1104.pdf';
      } else {
        this.fichaUrl = '';
      }
      this.mostrarFicha = true;
    }
  }
}
</script>
