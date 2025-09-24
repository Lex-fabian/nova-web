<template>
  <div class="pagina-maquinaria">
    <div class="contenedor-pagina">
      <div class="columna-izquierda">
        <img :src="imagen" :alt="titulo" />
      </div>
      <div class="columna-derecha">
        <h1>{{ titulo }}</h1>
        <p class="descripcion">Descripción breve del producto. Aquí puedes añadir más información técnica y comercial.</p>
        <div class="botones-pagina">
          <button type="button" class="boton-ficha" @click="mostrarFicha = true">Ficha técnica</button>
          <button type="button" class="boton-contactar">Contactar</button>
        </div>
      </div>
    </div>
    <div v-if="mostrarFicha" class="overlay-ficha">
      <div class="contenedor-ficha">
        <button class="cerrar-ficha" @click="mostrarFicha = false">&times;</button>
        <div class="pdf-actions">
          <a class="accion enlace-descarga" :href="pdfUrl" download target="_blank">Descargar PDF</a>
        </div>
        <iframe class="iframe-ficha" :src="pdfUrl" frameborder="0"></iframe>
        <div class="pdf-fallback">
          Si no puedes ver el PDF, <a :href="pdfUrl" target="_blank">haz clic aquí para abrirlo</a>.
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import '../style/maq_agricola_style.css'
import { ref } from 'vue'
const { titulo, imagen } = defineProps({
  titulo: { type: String, default: 'TS-754' },
  imagen: { type: String, default: '/src/assets/TS-754-IMAGEN1.png' }
})

const mostrarFicha = ref(false)
const pdfUrl = '/src/pdf/ficha_tecnica_maquina_agricola/TRACTOR 754 SINQR.pdf'
</script>
