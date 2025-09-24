<template>
	<header class="encabezado" style="height:56px;">
		<nav class="contenedor-navegacion">
					<div class="contenedor-logo" style="height:32px;align-items:center;display:flex;margin-top:6px;">
						<img src="./assets/icono_savreh.png" alt="Icono Savreh" class="logo" style="height:32px;max-width:90px;margin-right:1.2rem;" />
					</div>
				<ul class="enlaces-navegacion solo-escritorio" style="height:32px;align-items:center;">
					<li><a href="#" class="enlace-menu" @click.prevent="scrollToInicio">Inicio</a></li>
					<li class="dropdown-item">
						<a href="#" class="enlace-menu">Tienda <span class="dropdown-arrow">▼</span></a>
						<ul class="dropdown-submenu">
							<li><a href="#" class="submenu-link" @click.prevent="mostrarMaquinariaAgricola = true">Maquinaria Agrícola</a></li>
							<li><a href="#" class="submenu-link">Maquinaria Industrial</a></li>
							<li><a href="#" class="submenu-link">Equipos de Energía Solar</a></li>
							<li><a href="#" class="submenu-link">Acabados</a></li>
							<li><a href="#" class="submenu-link">Otros</a></li>
						</ul>
					</li>
					<li><a href="#contacto" class="enlace-menu" @click.prevent="scrollToContacto">Contáctanos</a></li>
					<li><a href="#" class="enlace-menu" @click.prevent="scrollToSobreNosotros">Sobre Nosotros</a></li>
				</ul>
		</nav>
		</header>
		<div class="contenedor-carrusel">
			<div class="diapositivas-carrusel">
				<img v-for="(img, idx) in portadas" :key="img.src" :src="img.src" :alt="img.alt" class="portada" :style="{ opacity: indicePortada === idx ? 1 : 0, zIndex: indicePortada === idx ? 2 : 1, transition: 'opacity 0.7s' }" />
				<button class="carousel-control carousel-prev" @click="anteriorPortada" aria-label="Anterior">&#10094;</button>
				<button class="carousel-control carousel-next" @click="siguientePortada" aria-label="Siguiente">&#10095;</button>
				<div class="carousel-indicators">
					<span v-for="(img, idx) in portadas" :key="'indicador-' + idx" :class="['carousel-indicator', { active: indicePortada === idx }]" @click="indicePortada = idx"></span>
				</div>
			</div>
			<div class="hero-text">
				Soluciones Innovadoras para la Industria y el Agro
			</div>
		</div>
		<div class="fila-portada-extra">
					<div class="texto-portada-extra">
						<div class="info-ts754" style="align-items:center;text-align:center;">
							<h2>MAQUINARIA INDUSTRIAL</h2>
							<p class="productos-vendidos">Más de 20,000 ventas</p>
							<button class="boton-mas-info" @click="mostrarMaquinaria = true">Más información</button>
						</div>
					</div>
					<div class="imagen-portada-extra">
						<img src="./assets/TS-754.png" alt="TS-754" class="portada-extra" style="max-width:340px;max-height:340px;display:block;margin:0 auto;" loading="lazy" />
					</div>
			</div>
					<div class="fila-portada-extra">
						<div class="imagen-portada-extra">
							<img src="./assets/batidora1.png" alt="Batidora Panadería" class="portada-extra" style="max-width:340px;max-height:340px;display:block;margin:0 auto;" loading="lazy" />
						</div>
						<div class="texto-portada-extra">
							<div class="info-ts754" style="align-items:center;text-align:center;">
								<h2>PANADERÍA</h2>
								<p class="productos-vendidos">Más de 13,000 ventas</p>
								<button class="boton-mas-info">Más información</button>
							</div>
						</div>
					</div>
			<MaqAgriPage v-if="mostrarMaquinariaAgricola" :titulo="'Maquinaria Agrícola TS-754'" :imagen="'/src/assets/TS-754-IMAGEN1.png'" @close="mostrarMaquinariaAgricola = false" />
			<MaqAgriPage v-if="mostrarMaquinaria" :titulo="'Maquinaria Industrial TS-754'" :imagen="'/src/assets/TS-754-IMAGEN1.png'" @close="mostrarMaquinaria = false" />

			<!-- Sección Testimonios Clientes -->
			<section class="seccion-testimonios">
				<h2 style="text-align:center;color:#2563eb;margin-bottom:2rem;">Lo que dicen nuestros clientes</h2>
				<div class="testimonios-cards" style="display:flex;gap:2rem;justify-content:center;flex-wrap:wrap;">
					<div class="testimonio-card" style="background:#fff;border-radius:14px;box-shadow:0 2px 12px rgba(37,99,235,0.07);padding:1.5rem 1.2rem;max-width:320px;flex:1 1 220px;">
						<p style="font-size:1.08rem;color:#2c3e50;margin-bottom:1rem;">“Excelente atención y productos de calidad. Mi empresa ha mejorado mucho gracias a Savreh.”</p>
						<span style="color:#2563eb;font-weight:600;">Juan Pérez, Agroindustrias JP</span>
					</div>
					<div class="testimonio-card" style="background:#fff;border-radius:14px;box-shadow:0 2px 12px rgba(37,99,235,0.07);padding:1.5rem 1.2rem;max-width:320px;flex:1 1 220px;">
						<p style="font-size:1.08rem;color:#2c3e50;margin-bottom:1rem;">“La maquinaria industrial que adquirimos superó nuestras expectativas. Recomendados.”</p>
						<span style="color:#2563eb;font-weight:600;">María Gómez, Soluciones Industriales</span>
					</div>
					<div class="testimonio-card" style="background:#fff;border-radius:14px;box-shadow:0 2px 12px rgba(37,99,235,0.07);padding:1.5rem 1.2rem;max-width:320px;flex:1 1 220px;">
						<p style="font-size:1.08rem;color:#2c3e50;margin-bottom:1rem;">“Muy satisfecho con el servicio y la asesoría. Los equipos solares funcionan perfecto.”</p>
						<span style="color:#2563eb;font-weight:600;">Carlos Ruiz, EcoEnergia</span>
					</div>
				</div>
			</section>

			<!-- Sección Sobre Nosotros -->
			<section id="sobre-nosotros" class="sobre-nosotros-section">
				<div class="sobre-nosotros-content">
					<h2>Sobre Nosotros</h2>
					<div class="sobre-nosotros-cards">
						<div class="sobre-nosotros-card">
							<h3>Misión</h3>
							<p>Brindar soluciones innovadoras y de calidad para la industria y el agro, contribuyendo al desarrollo sostenible y la satisfacción de nuestros clientes.</p>
						</div>
						<div class="sobre-nosotros-card">
							<h3>Visión</h3>
							<p>Ser líderes en el mercado nacional e internacional, reconocidos por nuestra excelencia, responsabilidad y compromiso con el progreso tecnológico.</p>
						</div>
						<div class="sobre-nosotros-card">
							<h3>Objetivo</h3>
							<p>Impulsar el crecimiento de nuestros clientes mediante productos y servicios que generen valor, confianza y resultados sostenibles.</p>
						</div>
					</div>
				</div>
			</section>

			<!-- Sección Contáctanos -->
			<section id="contacto" class="contact-section">
				<div class="contact-info">
					<h2>Contáctanos</h2>
					<p>¿Tienes dudas, necesitas una cotización o quieres saber más sobre nuestros productos? Escríbenos y te responderemos lo antes posible.</p>
					<div class="contact-details">
						<div class="contact-item"><i class="fab fa-facebook"></i> <a href="https://www.facebook.com/p/Savreh-SA-61563909317105/" target="_blank">Facebook</a></div>
						<div class="contact-item"><i class="fab fa-instagram"></i> <a href="https://www.instagram.com/savreh.ec/" target="_blank">Instagram</a></div>
						<div class="contact-item"><i class="fab fa-tiktok"></i> <a href="https://www.tiktok.com/@savreh.ec" target="_blank">TikTok</a></div>
					</div>
				</div>
				<form class="contact-form">
					<input type="text" placeholder="Nombre" required />
					<input type="email" placeholder="Correo electrónico" required />
					<textarea placeholder="Mensaje" required></textarea>
					<button type="submit" class="send-button">Enviar mensaje</button>
				</form>
			</section>


			<!-- Pie de página -->
			<footer class="footer-copyright">
				&copy; Copyright Savreh
			</footer>

</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import MaqAgriPage from './page/maq_agricola_page.vue'
import './style.css'
import './style-mobil.css'

import portadaNova from './assets/portada-nova.jpg'
import portada2 from './assets/portada2.png'
import portada3 from './assets/portada3.png'
const portadas = [
	{ src: portadaNova, alt: 'Portada Nova' },
	{ src: portada2, alt: 'Portada 2' },
	{ src: portada3, alt: 'Portada 3' }
]
const indicePortada = ref(0)
let intervaloCarrusel = null

const mostrarMaquinaria = ref(false)
const mostrarMaquinariaAgricola = ref(false)

function siguientePortada() {
	indicePortada.value = (indicePortada.value + 1) % portadas.length
}
function anteriorPortada() {
	indicePortada.value = (indicePortada.value - 1 + portadas.length) % portadas.length
}

function scrollToInicio() {
	window.scrollTo({ top: 0, behavior: 'smooth' })
	mostrarMaquinariaAgricola.value = false
}
function scrollToContacto() {
	const contacto = document.getElementById('contacto')
	if (contacto) {
		contacto.scrollIntoView({ behavior: 'smooth' })
	}
}
function scrollToSobreNosotros() {
	const sobre = document.getElementById('sobre-nosotros')
	if (sobre) {
		sobre.scrollIntoView({ behavior: 'smooth' })
	}
}

onMounted(() => {
	intervaloCarrusel = setInterval(siguientePortada, 4000)
})
onUnmounted(() => {
	clearInterval(intervaloCarrusel)
})
</script>
