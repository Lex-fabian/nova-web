<template>
	<Cabeza
    @ir-inicio="scrollToInicio"
    @abrir-maquinaria-agricola="handleAbrirMaquinariaAgricola"
    @abrir-maquinaria-industrial="handleAbrirMaquinariaIndustrial"
    @abrir-panaderia="handleAbrirPanaderia"
  />

	<main style="margin-top:64px; margin-bottom:64px; background: #f3f4f6;">
		<Portada />

		<Maquinas @open-maquinaria="mostrarMaquinaria = true" />

		<MaqAgriPage
			v-if="mostrarMaquinariaAgricola"
			titulo="Maquinaria Agrícola TS-754"
			imagen="/src/assets/TS-754-IMAGEN1.png"
			@close="mostrarMaquinariaAgricola = false"
		/>

		<MaqAgriPage
			v-if="mostrarMaquinaria"
			titulo="Maquinaria Industrial TS-754"
			imagen="/src/assets/TS-754-IMAGEN1.png"
			@close="mostrarMaquinaria = false"
		/>

		<Comentario />

		<Nosotros />

		<a
			href="https://wa.link/hj2t5j"
			class="whatsapp-flotante"
			target="_blank"
			rel="noopener"
			aria-label="Contactar por WhatsApp"
		>
			<svg viewBox="0 0 24 24" aria-hidden="true">
				<path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.890-5.335 11.893-11.893A11.821 11.821 0 0020.885 3.488"/>
			</svg>
		</a>

		<Contactanos />
		<Pie @ir-inicio="scrollToInicio" />
	</main>
</template>

<script setup>
import { ref, nextTick } from 'vue'
import Cabeza from './components/cabeza.vue'
import MaqAgriPage from './page/maq_agricola_page.vue'
import Maquinas from './components/maquinas.vue'
import Portada from './components/portada.vue'
import Comentario from './components/comentario.vue'
import Nosotros from './components/nosotros.vue'
import Contactanos from './components/contactanos.vue'
import Pie from './components/pie.vue'

const mostrarMaquinaria = ref(false)
const mostrarMaquinariaAgricola = ref(false)

const formulario = ref({ nombre: '', email: '', mensaje: '' })

function scrollToInicio() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function scrollToMaquinaria() {
  const maquinaria = document.querySelector('.tarjeta-maquinaria-industrial')
  if (maquinaria) maquinaria.scrollIntoView({ behavior: 'smooth' })
}

function scrollToPanaderia() {
  const panaderia = document.querySelector('.tarjeta-panaderia')
  if (panaderia) panaderia.scrollIntoView({ behavior: 'smooth' })
}

function scrollToSobreNosotros() {
  const sobreNosotros = document.getElementById('sobre-nosotros')
  if (sobreNosotros) sobreNosotros.scrollIntoView({ behavior: 'smooth' })
}

function scrollToContacto() {
  const contacto = document.getElementById('contacto')
  if (contacto) contacto.scrollIntoView({ behavior: 'smooth' })
}

function enviarFormulario() {
  alert('Mensaje enviado. Nos contactaremos contigo pronto.')
  formulario.value = { nombre: '', email: '', mensaje: '' }
}

function handleAbrirMaquinariaAgricola() {
  mostrarMaquinariaAgricola.value = true
  mostrarMaquinaria.value = false
  nextTick(() => {
    const el = document.querySelector('.tarjeta-maquinaria-agricola')
    if (el) el.scrollIntoView({ behavior: 'smooth' })
  })
}

function handleAbrirMaquinariaIndustrial() {
  mostrarMaquinaria.value = true
  mostrarMaquinariaAgricola.value = false
  nextTick(() => {
    const el = document.querySelector('.tarjeta-maquinaria-industrial')
    if (el) el.scrollIntoView({ behavior: 'smooth' })
  })
}

function handleAbrirPanaderia() {
  mostrarMaquinaria.value = false
  mostrarMaquinariaAgricola.value = false
  nextTick(() => {
    const el = document.querySelector('.tarjeta-panaderia')
    if (el) el.scrollIntoView({ behavior: 'smooth' })
  })
}
</script>

<style scoped>
.whatsapp-flotante {
	position: fixed;
	right: 18px;
	bottom: 8px;
	width: 46px;
	height: 46px;
	background: #25D366; 
	color: #fff;
	border-radius: 50%;
	display: inline-grid;
	place-items: center;
	z-index: 9999;
	text-decoration: none;
}

.whatsapp-flotante svg { width: 28px; height: 28px; display: block; }

@media (max-width: 520px) {
	.whatsapp-flotante { right: 12px; bottom: 6px; width: 48px; height: 48px; } /* ajustado para móvil */
}
</style>