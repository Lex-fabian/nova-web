<template>
<header class="encabezado">
  <nav class="contenedor-navegacion">
    <div class="contenedor-logo">
      <button type="button" class="logo-link" @click.prevent="emitIrInicio" aria-label="Ir al inicio">
        <img src="../assets/logo-nova.png" alt="Icono Savreh" class="logo" />
      </button>
    </div>
    <ul class="enlaces-navegacion solo-escritorio">
      <li class="tienda-wrapper"
          @mouseenter="onTiendaEnter"
          @mouseleave="onTiendaLeave"
      >
        <button
          class="enlace-menu enlace-tienda"
          aria-haspopup="true"
          :aria-expanded="tiendaAbierta"
          @click.prevent="onTiendaClick"
        >
          Tienda
          <span class="caret" :class="{ open: tiendaAbierta }" aria-hidden="true"></span>
        </button>

        <ul v-if="tiendaAbierta" class="submenu" role="menu">
          <li role="none">
            <button role="menuitem" class="submenu-item" @click="abrirMaquinariaAgricola">Maquinaria Agrícola</button>
          </li>
          <li role="none">
            <button role="menuitem" class="submenu-item" @click="abrirMaquinariaIndustrial">Maquinaria Industrial</button>
          </li>
          <li role="none">
            <button role="menuitem" class="submenu-item" @click="abrirPanaderia">Panadería</button>
          </li>
        </ul>
      </li>
      <li><a href="#sobre-nosotros" class="enlace-menu" @click.prevent="scrollToSobreNosotros">Sobre Nosotros</a></li>
      <li><a href="#contacto" class="enlace-menu" @click.prevent="scrollToContacto">Contáctanos</a></li>
      <li class="buscador-wrapper">
        <button type="button" class="boton-buscar" @click="toggleBuscador" :aria-expanded="buscadorAbierto" aria-label="Buscar productos">
          <svg width="20" height="20" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
            <circle cx="11" cy="11" r="6" stroke="currentColor" stroke-width="2" fill="none" />
            <line x1="20.5" y1="20.5" x2="15.5" y2="15.5" stroke="currentColor" stroke-width="2" stroke-linecap="round" />
          </svg>
        </button>
        <transition name="fade">
          <input v-if="buscadorAbierto" ref="inputBuscar" type="text" placeholder="Buscar productos..." class="input-buscar" @blur="cerrarBuscador" />
        </transition>
      </li>
    </ul>
    <button type="button" class="boton-menu-movil solo-movil" @click="menuMovilAbierto = !menuMovilAbierto" :aria-expanded="menuMovilAbierto" aria-controls="menu-movil" aria-label="Abrir menú">☰</button>
  </nav>

  <div v-if="menuMovilAbierto" class="menu-overlay" @click="menuMovilAbierto = false"></div>

  <div id="menu-movil" :class="['menu-movil','solo-movil',{ open: menuMovilAbierto }]" v-show="menuMovilAbierto">
    <div class="menu-header">
      <img src="../assets/logo-nova.png" alt="logo nova" class="menu-logo" />
      <div class="menu-title">menu</div>
    </div>
    <ul class="menu-movil-list">
      <li><a href="#maquinaria" @click.prevent="scrollToMaquinaria; menuMovilAbierto = false">Maquinaria Industrial</a></li>
      <li><a href="#panaderia" @click.prevent="scrollToPanaderia; menuMovilAbierto = false">Panadería</a></li>
      <li><a href="#tienda" @click.prevent="scrollToTienda; menuMovilAbierto = false">Tienda</a></li>
      <li><a href="#sobre-nosotros" @click.prevent="scrollToSobreNosotros; menuMovilAbierto = false">Sobre Nosotros</a></li>
      <li><a href="#contacto" @click.prevent="scrollToContacto; menuMovilAbierto = false">Contáctanos</a></li>
    </ul>
  </div>
</header>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'

const emit = defineEmits(['ir-inicio','abrir-maquinaria-agricola','abrir-maquinaria-industrial','abrir-panaderia'])
const menuMovilAbierto = ref(false)
const buscadorAbierto = ref(false)
const inputBuscar = ref(null)
const tiendaAbierta = ref(false)
const tiendaClicked = ref(false)

function toggleBuscador() {
  buscadorAbierto.value = !buscadorAbierto.value
  if (buscadorAbierto.value) {
    nextTick(() => {
      try { inputBuscar.value && inputBuscar.value.focus() } catch (e) {}
    })
  }
}

function cerrarBuscador(event) {
  const related = event?.relatedTarget
  if (!related || !(related instanceof Element) || !related.closest('.boton-buscar')) {
    buscadorAbierto.value = false
  }
}

function emitIrInicio() {
  emit('ir-inicio')
}

function scrollToMaquinaria() { const maquinaria = document.querySelector('.tarjeta-maquinaria-industrial'); if (maquinaria) maquinaria.scrollIntoView({ behavior: 'smooth' }) }
function scrollToPanaderia() { const panaderia = document.querySelector('.tarjeta-panaderia'); if (panaderia) panaderia.scrollIntoView({ behavior: 'smooth' }) }
function scrollToTienda() { tiendaAbierta.value = !tiendaAbierta.value }

function onTiendaEnter() {
  tiendaAbierta.value = true
}

function onTiendaLeave() {
  if (!tiendaClicked.value) {
    tiendaAbierta.value = false
  }
}

function onTiendaClick() {
  tiendaAbierta.value = !tiendaAbierta.value
  tiendaClicked.value = tiendaAbierta.value
}

function abrirMaquinariaAgricola() { tiendaAbierta.value = false; tiendaClicked.value = false; emit('abrir-maquinaria-agricola') }
function abrirMaquinariaIndustrial() { tiendaAbierta.value = false; tiendaClicked.value = false; emit('abrir-maquinaria-industrial') }
function abrirPanaderia() { tiendaAbierta.value = false; tiendaClicked.value = false; emit('abrir-panaderia') }

function scrollToSobreNosotros() { const sobre = document.getElementById('sobre-nosotros'); if (sobre) sobre.scrollIntoView({ behavior: 'smooth' }) }
function scrollToContacto() { const contacto = document.getElementById('contacto'); if (contacto) contacto.scrollIntoView({ behavior: 'smooth' }) }

function onDocClick(e) {
  const target = e.target
  if (!(target instanceof Element)) return
  if (!target.closest('.boton-menu-movil') && !target.closest('.menu-movil')) menuMovilAbierto.value = false
  if (!target.closest('.boton-buscar') && !target.closest('.input-buscar')) buscadorAbierto.value = false
  if (!target.closest('.tienda-wrapper')) { tiendaAbierta.value = false; tiendaClicked.value = false }
}

function onKeydown(e) {
  if (e.key === 'Escape') {
    if (menuMovilAbierto.value) menuMovilAbierto.value = false
    if (buscadorAbierto.value) buscadorAbierto.value = false
    if (tiendaAbierta.value) { tiendaAbierta.value = false; tiendaClicked.value = false }
  }
}

onMounted(() => {
  document.addEventListener('click', onDocClick)
  document.addEventListener('keydown', onKeydown)
})
onUnmounted(() => {
  document.removeEventListener('click', onDocClick)
  document.removeEventListener('keydown', onKeydown)
})
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@400;700&display=swap');

.encabezado {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  box-sizing: border-box;
  background: rgba(255, 255, 255, 0.98);
  z-index: 1000;
  display: flex;
  flex-direction: column;
  font-family: 'Montserrat', 'Helvetica Neue', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-weight: 500;
  line-height: 1;
}

.contenedor-navegacion {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 64px;
  padding: 0 1.25rem;
  gap: 0.75rem;
}

.contenedor-logo { display: flex; align-items: center; }
.logo-link { display: inline-flex; align-items: center; gap: 0.5rem; background: transparent; border: none; padding: 0; cursor: pointer; }
.logo { height: 38px; width: auto; max-width: 120px; }
.logo-text { color: #14143a; margin-left: 0.4rem; text-shadow: 20cap; font-weight: 900; letter-spacing: 1.6px; font-size: 0.95rem; line-height: 50; font-family: 'Lato', sans-serif; display: inline-block; }

.enlaces-navegacion { display: flex; align-items: center; gap: 1.25rem; list-style: none; margin: 0; padding: 0; }
.enlaces-navegacion li { position: relative; }

.enlace-menu {
  color: #040404 !important;
  text-decoration: none;
  font-weight: 300 !important;
  font-size: 1rem;
  padding: 0.35rem 0.5rem;
  letter-spacing: 0.6px;
  line-height: 1;
  transition: font-weight 0.15s;
}
.enlace-menu:focus, .enlace-menu:hover {
  color: #000000 !important;
  background: rgba(248, 244, 244, 0.035);
  border-radius: 6px;
}

.buscador-wrapper { display: flex; align-items: center; position: relative; }
.boton-buscar { background: transparent; border: none; color: #000; cursor: pointer; padding: 0.35rem; border-radius: 6px; }
.boton-buscar svg { width: 20px; height: 20px; stroke: currentColor; fill: none; }
.input-buscar { position: absolute; top: 64px; right: 1.25rem; background: #fff; border: 1px solid rgba(6,26,72,0.08); border-radius: 8px; padding: 0.5rem 0.75rem; font-size: 0.95rem; width: 240px; box-shadow: 0 8px 30px rgba(2,6,23,0.12); font-family: inherit; }

.boton-menu-movil {
  display: none;
  background: transparent;
  border: none;
  color: #fff;
  font-size: 1.25rem;
  padding: 0.35rem;
  border-radius: 6px;
}
.boton-menu-movil:hover { background: rgba(13,110,253,0.08); color: #0b5ed7; }
.menu-movil {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 280px;
  max-width: 85%;
  background: rgba(6,26,72,0.99);
  transform: translateX(-100%);
  transition: transform 300ms ease;
  z-index: 1100;
  padding-top: 64px;
  box-shadow: 8px 0 24px rgba(2,6,23,0.25);
}
.menu-movil.open {
  transform: translateX(0);
}
.menu-movil-list { list-style: none; margin: 0; padding: 1rem; display: flex; flex-direction: column; gap: 0.5rem; }
.menu-movil-list a { color: #fff; text-decoration: none; padding: 0.9rem 0.75rem; display: block; border-radius: 6px; font-weight: 400; }
.menu-movil-list a:hover { background: rgba(255,255,255,0.03); }


.menu-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.35);
  z-index: 1090;
}

/* Header dentro del menú móvil */
.menu-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 6px;
  padding: 18px 12px;
  background: transparent;
}
.menu-logo {
  width: 86px;
  height: auto;
  display: block;
}
.menu-title {
  color: #ffffff;
  font-weight: 700;
  text-transform: lowercase;
  letter-spacing: 1px;
}

/* Submenu (estilos para versión web) */
.submenu {
  position: absolute;
  top: 100%;
  left: 0;
  background: #ffffff;
  color: #111;
  border-radius: 8px;
  padding: 0.25rem 0;
  box-shadow: 0 10px 30px rgba(2,6,23,0.12);
  min-width: 190px;
  z-index: 1100;
  list-style: none;
  pointer-events: auto;
}
.submenu-item {
  display: block;
  width: 100%;
  text-align: left;
  padding: 0.6rem 0.9rem;
  background: transparent;
  border: none;
  cursor: pointer;
  font: inherit;
  color: inherit;
}
.submenu-item:hover,
.submenu-item:focus {
  background: rgba(6,26,72,0.06);
  outline: none;
  border-radius: 6px;
}

.boton-menu-movil {
  display: none;
  background: transparent;
  border: none;
  color: #fff;
  font-size: 1.25rem;
  padding: 0.35rem;
  border-radius: 6px;
}

/* Estilos del menu movil */
@media (max-width: 900px) {
  .submenu { display: none !important; }
  .enlaces-navegacion { display: none; }

  .boton-menu-movil { display: inline-flex; order: 1; color: #080808; background: transparent; }
  .boton-menu-movil:hover { background: rgba(255,255,255,0.06); color: #000000; }

  .contenedor-logo { order: 2; margin-left: auto; }

  .menu-movil {
    position: fixed;
    top: 0;
    left: 0;
    height: 100%;
    width: 280px;
    max-width: 85%;
    background: rgba(253, 254, 255, 0.99);
    transform: translateX(-100%);
    transition: transform 300ms ease;
    z-index: 1100;
    padding-top: 0; 
    box-shadow: 8px 0 24px rgba(2,6,23,0.25);
  }
  .menu-movil.open { transform: translateX(0); }
  .menu-movil-list { list-style: none; margin: 0; padding: 0.5rem 1rem; display: flex; flex-direction: column; gap: 0.5rem; }
  .menu-movil-list a { color: #060606; text-decoration: none; padding: 0.9rem 0.75rem; display: block; border-radius: 6px; font-weight: 400; }

  .input-buscar { right: 1rem; top: 64px; width: calc(100% - 2rem); left: 1rem; }
  .contenedor-navegacion { padding: 0 0.75rem; }
  .logo-text { font-size: 0.9rem; letter-spacing: 1.2px; }

  .menu-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.35);
    z-index: 1090;
  }
}
</style>
