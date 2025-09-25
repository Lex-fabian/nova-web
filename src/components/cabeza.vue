<template>
<header class="encabezado">
  <nav class="contenedor-navegacion">
    <div class="contenedor-logo">
      <button type="button" class="logo-link" @click.prevent="scrollToInicio" aria-label="Ir al inicio">
        <img src="../assets/icono_savreh.png" alt="Icono Savreh" class="logo" />
        <span class="logo-text">SAVREH</span>
      </button>
    </div>
    <ul class="enlaces-navegacion solo-escritorio">
      <li class="dropdown-item" ref="dropdownTienda">
        <button type="button" class="enlace-menu dropdown-toggle" @click.stop="tiendaAbierto = !tiendaAbierto" :aria-expanded="tiendaAbierto" aria-haspopup="true">
          Tienda <span class="dropdown-arrow">▼</span>
        </button>
        <ul class="dropdown-submenu" v-show="tiendaAbierto" :class="{ show: tiendaAbierto }">
          <li><a href="#maquinaria" class="submenu-link" @click.prevent="scrollToMaquinaria; tiendaAbierto = false">Maquinaria Industrial</a></li>
          <li><a href="#panaderia" class="submenu-link" @click.prevent="scrollToPanaderia; tiendaAbierto = false">Panadería</a></li>
        </ul>
      </li>
      <li><a href="#sobre-nosotros" class="enlace-menu" @click.prevent="scrollToSobreNosotros">Sobre Nosotros</a></li>
      <li><a href="#contacto" class="enlace-menu" @click.prevent="scrollToContacto">Contáctanos</a></li>
      <li class="buscador-wrapper">
        <button type="button" class="boton-buscar" @click="toggleBuscador" :aria-expanded="buscadorAbierto" aria-label="Buscar productos">
          <svg width="20" height="20" viewBox="0 0 24 24" aria-hidden="true"><circle cx="11" cy="11" r="8"/></svg>
        </button>
        <transition name="fade">
          <input v-if="buscadorAbierto" ref="inputBuscar" type="text" placeholder="Buscar productos..." class="input-buscar" @blur="cerrarBuscador" />
        </transition>
      </li>
    </ul>
    <button type="button" class="boton-menu-movil solo-movil" @click="menuMovilAbierto = !menuMovilAbierto" :aria-expanded="menuMovilAbierto" aria-controls="menu-movil" aria-label="Abrir menú">☰</button>
  </nav>
    <div id="menu-movil" class="menu-movil solo-movil" v-show="menuMovilAbierto">
    <ul class="menu-movil-list">
      <li><a href="#maquinaria" @click.prevent="scrollToMaquinaria; menuMovilAbierto = false">Maquinaria Industrial</a></li>
      <li><a href="#panaderia" @click.prevent="scrollToPanaderia; menuMovilAbierto = false">Panadería</a></li>
      <li><a href="#sobre-nosotros" @click.prevent="scrollToSobreNosotros; menuMovilAbierto = false">Sobre Nosotros</a></li>
      <li><a href="#contacto" @click.prevent="scrollToContacto; menuMovilAbierto = false">Contáctanos</a></li>
    </ul>
  </div>
</header>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'

const menuMovilAbierto = ref(false)
const buscadorAbierto = ref(false)
const tiendaAbierto = ref(false)
const inputBuscar = ref(null)

function toggleBuscador() {
  buscadorAbierto.value = !buscadorAbierto.value
  if (buscadorAbierto.value) {
    // esperar a que el input se pinte y luego enfocar
    nextTick(() => {
      try { inputBuscar.value && inputBuscar.value.focus() } catch (e) { /* noop */ }
    })
  }
}

function cerrarBuscador(event) {
  // si el blur ocurre y el nuevo foco no es el botón de búsqueda, cerramos
  const related = event?.relatedTarget
  if (!related || !(related instanceof Element) || !related.closest('.boton-buscar')) {
    buscadorAbierto.value = false
  }
}

function scrollToInicio() { window.scrollTo({ top: 0, behavior: 'smooth' }) }
function scrollToMaquinaria() { const maquinaria = document.querySelector('.tarjeta-maquinaria-industrial'); if (maquinaria) maquinaria.scrollIntoView({ behavior: 'smooth' }) }
function scrollToPanaderia() { const panaderia = document.querySelector('.tarjeta-panaderia'); if (panaderia) panaderia.scrollIntoView({ behavior: 'smooth' }) }
function scrollToSobreNosotros() { const sobre = document.getElementById('sobre-nosotros'); if (sobre) sobre.scrollIntoView({ behavior: 'smooth' }) }
function scrollToContacto() { const contacto = document.getElementById('contacto'); if (contacto) contacto.scrollIntoView({ behavior: 'smooth' }) }

function onDocClick(e) {
  const target = e.target
  if (!(target instanceof Element)) return
  if (!target.closest('.boton-menu-movil') && !target.closest('.menu-movil')) menuMovilAbierto.value = false
  if (!target.closest('.boton-buscar') && !target.closest('.input-buscar')) buscadorAbierto.value = false
  // cerrar submenu de Tienda si se clickea fuera
  if (!target.closest('.dropdown-item') && tiendaAbierto.value) tiendaAbierto.value = false
}

function onKeydown(e) {
  if (e.key === 'Escape') {
    if (menuMovilAbierto.value) menuMovilAbierto.value = false
    if (buscadorAbierto.value) buscadorAbierto.value = false
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
  background: rgba(6, 26, 72, 0.98);
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
.logo-text { color: #fff; margin-left: 0.4rem; font-weight: 700; letter-spacing: 1.6px; font-size: 0.95rem; line-height: 1; font-family: 'Lato', sans-serif; display: inline-block; }

.enlaces-navegacion { display: flex; align-items: center; gap: 1.25rem; list-style: none; margin: 0; padding: 0; }
.enlaces-navegacion li { position: relative; }
.enlace-menu { color: #fff; text-decoration: none; font-weight: 300; font-size: 1rem; padding: 0.35rem 0.5rem; letter-spacing: 0.6px; line-height: 1; }
.enlace-menu:focus, .enlace-menu:hover { color: #fff; background: rgba(255,255,255,0.035); border-radius: 6px; }

.dropdown-item { display: inline-block; }
.dropdown-submenu { position: absolute; top: calc(100% + 8px); left: 0; background: #fff; color: #0f172a; border-radius: 10px; padding: 0.2rem 0.2rem; min-width: 220px; box-shadow: 0 8px 24px rgba(2,6,23,0.12); backdrop-filter: blur(4px); list-style: none; opacity: 0; pointer-events: none; transform-origin: top left; transition: opacity 160ms ease, transform 160ms ease; }
.dropdown-submenu li { padding: 0; }
.dropdown-submenu.show, .dropdown-submenu[style*="display: block"], .dropdown-submenu[style*="display:block"] { opacity: 1; pointer-events: auto; transform: translateY(0); }
.dropdown-submenu .submenu-link { display: block; padding: 0.6rem 0.9rem; color: #0f172a; text-decoration: none; font-weight: 400; letter-spacing: 0.2px; transition: background 160ms ease, color 160ms ease; border-radius: 8px; }
.dropdown-submenu .submenu-link:hover { background: rgba(37,99,235,0.06); color: var(--primary, #2563eb); }
.dropdown-submenu .submenu-link:hover { background: rgba(255,255,255,0.06); color: #fff; }
.dropdown-item:hover .dropdown-submenu, .dropdown-item:focus-within .dropdown-submenu { display: block; transform-origin: top left; animation: popDown 160ms ease forwards; }

@keyframes popDown {
  from { opacity: 0; transform: translateY(-6px) scale(0.99); }
  to { opacity: 1; transform: translateY(0) scale(1); }
}

.buscador-wrapper { display: flex; align-items: center; position: relative; }
.boton-buscar { background: transparent; border: none; color: #fff; cursor: pointer; padding: 0.35rem; border-radius: 6px; }
.boton-buscar svg { width: 20px; height: 20px; fill: #fff; stroke: none; }
.input-buscar { position: absolute; top: 64px; right: 1.25rem; background: #fff; border: 1px solid rgba(6,26,72,0.08); border-radius: 8px; padding: 0.5rem 0.75rem; font-size: 0.95rem; width: 240px; box-shadow: 0 8px 30px rgba(2,6,23,0.12); font-family: inherit; }

.boton-menu-movil { display: none; background: transparent; border: none; color: #fff; font-size: 1.25rem; }
.menu-movil { display: none; }
.menu-movil-list { list-style: none; margin: 0; padding: 0.75rem 1rem; display: flex; flex-direction: column; gap: 0.5rem; }
.menu-movil-list a { color: #fff; text-decoration: none; padding: 0.6rem 0.75rem; display: block; border-radius: 6px; font-weight: 300; letter-spacing: 0.25px; }
.menu-movil-list a:hover { background: rgba(255,255,255,0.03); }

@media (max-width: 900px) {
  .enlaces-navegacion { display: none; }
  .boton-menu-movil { display: inline-flex; }
  .menu-movil.solo-movil[style] { display: block; }
  .menu-movil { background: rgba(6,26,72,0.99); box-shadow: 0 8px 24px rgba(2,6,23,0.25); }
  .input-buscar { right: 1rem; top: 64px; width: calc(100% - 2rem); left: 1rem; }
  .contenedor-navegacion { padding: 0 0.75rem; }
  .logo-text { font-size: 0.9rem; letter-spacing: 1.2px; }
}

</style>
