<template>
	<div class="tarjeta-carrusel" @mouseenter="pausarCarrusel" @mouseleave="reanudarCarrusel">
		<div class="diapositivas-carrusel" role="region" aria-roledescription="carrusel">
			<img
				v-for="(img, idx) in portadas"
				:key="img.src"
				:src="img.src"
				:alt="img.alt"
				class="portada"
				:class="{ active: indicePortada === idx }"
				loading="lazy"
			/>
			<div :class="['texto-carrusel', { oculto: textoOculto }]">
				Soluciones Innovadoras para la Industria y el Agro
			</div>
			<button class="carousel-control carousel-prev" @click="anteriorPortada" aria-label="Imagen anterior" title="Imagen anterior">&#10094;</button>
			<button class="carousel-control carousel-next" @click="siguientePortada" aria-label="Imagen siguiente" title="Imagen siguiente">&#10095;</button>
			<div class="carousel-indicators" role="tablist" aria-label="Indicadores de carrusel">
				<button v-for="(img, idx) in portadas" :key="'indicador-' + idx" type="button" class="carousel-indicator" :class="{ active: indicePortada === idx }" @click="indicePortada = idx" :aria-label="`Ir a imagen ${idx + 1}`" role="tab" :aria-selected="indicePortada === idx"></button>
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import portadaNova from '../assets/portada1.png'
import portada2 from '../assets/portada2.png'
import portada3 from '../assets/portada3.png'

const indicePortada = ref(0)
const textoOculto = ref(false)
const textoTimeout = ref(null)
// almacenamos el id del setInterval o null
const intervaloCarrusel = ref(null)

const portadas = [
	{ src: portadaNova, alt: 'Nova - Soluciones Industriales y Agrícolas' },
	{ src: portada2, alt: 'Portada 2' },
	{ src: portada3, alt: 'Portada 3' }
]

function siguientePortada() {
	indicePortada.value = (indicePortada.value + 1) % portadas.length
}

function anteriorPortada() {
	indicePortada.value = indicePortada.value === 0 ? portadas.length - 1 : indicePortada.value - 1
}

function pausarCarrusel() {
	if (intervaloCarrusel.value) {
		clearInterval(intervaloCarrusel.value)
		intervaloCarrusel.value = null
	}
}

function reanudarCarrusel() {
	if (!intervaloCarrusel.value) {
		intervaloCarrusel.value = setInterval(siguientePortada, 4000)
	}
}

function onKeydown(e) {
	if (e.key === 'ArrowLeft') anteriorPortada()
	if (e.key === 'ArrowRight') siguientePortada()
}

onMounted(() => {
	textoTimeout.value = setTimeout(() => {
		textoOculto.value = true
		textoTimeout.value = null
	}, 3000)

	intervaloCarrusel.value = setInterval(siguientePortada, 4000)
	document.addEventListener('keydown', onKeydown)
})

onUnmounted(() => {
	if (intervaloCarrusel.value !== null) {
		clearInterval(intervaloCarrusel.value)
		intervaloCarrusel.value = null
	}
	if (textoTimeout.value !== null) {
		clearTimeout(textoTimeout.value)
		textoTimeout.value = null
	}
	document.removeEventListener('keydown', onKeydown)
})
</script>

<style scoped>
.tarjeta-carrusel { margin-top: 2.5rem !important; margin-bottom: 1rem; }
.diapositivas-carrusel {
	width: 100vw;
	height: calc(100vh - 56px);
	display: flex;
	align-items: center;
	justify-content: center;
	position: relative;
	top: 0;
	left: 0;
	overflow: hidden;
}

.texto-carrusel {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	color: #ffffff;
	font-size: 2.8rem;
	font-weight: 600;
	text-align: center;
	text-shadow: 0 2px 8px rgba(0,0,0,0.7);
	z-index: 10;
	max-width: 85vw;
	line-height: 1.3;
	letter-spacing: 0;
	transition: opacity 0.5s ease-in-out;
}

.texto-carrusel.oculto {
	opacity: 0;
	pointer-events: none;
}

.portada {
	width: 100vw;
	height: calc(100vh - 64px);
	object-fit: cover;
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	opacity: 0;
	z-index: 1;
	pointer-events: none;
	transition: opacity 0.7s ease-in-out;
}
.portada.active {
	opacity: 1;
	z-index: 2;
	pointer-events: auto;
}

.carousel-control {
	position: absolute;
	top: 50%;
	transform: translateY(-50%);
	background: rgba(6, 26, 72, 0.6);
	color: #fff;
	border: 2px solid rgba(255,255,255,0.3);
	font-size: 2.2rem;
	padding: 0.4em 0.8em;
	border-radius: 50%;
	cursor: pointer;
	z-index: 15;
	transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
	backdrop-filter: blur(8px);
	width: 50px;
	height: 50px;
	display: flex;
	align-items: center;
	justify-content: center;
}
.carousel-control:hover {
	background: rgba(6, 26, 72, 0.8);
	border-color: #2563eb;
	transform: translateY(-50%) scale(1.1);
	box-shadow: 0 4px 20px rgba(37,99,235,0.3);
}
.carousel-control:focus {
	outline: 3px solid rgba(37,99,235,0.5);
	outline-offset: 2px;
}
.carousel-prev { left: 2vw; }
.carousel-next { right: 2vw; }

.carousel-indicators {
	position: absolute;
	bottom: 2.5vh;
	left: 50%;
	transform: translateX(-50%);
	display: flex;
	gap: 0.7em;
	z-index: 10;
}

.carousel-indicator {
	width: 13px;
	height: 13px;
	border-radius: 50%;
	background: rgba(255,255,255,0.5);
	cursor: pointer;
	transition: transform 0.2s ease, background 0.2s ease;
	border: 2px solid rgba(255,255,255,0.8);
	display: inline-block;
}
.carousel-indicator.active { background: #2563eb; border-color: #2563eb; transform: scale(1.2); box-shadow: 0 2px 8px rgba(37,99,235,0.4); }
.carousel-indicator:hover { transform: scale(1.1); }
</style>
