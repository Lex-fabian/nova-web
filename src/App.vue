<template>
	<header class="encabezado" style="height:56px;">
		<nav class="contenedor-navegacion">
			<div class="contenedor-logo" style="height:32px;align-items:center;display:flex;margin-top:6px;">
				<img src="./assets/icono_savreh.png" alt="Icono Savreh" class="logo" style="height:32px;max-width:90px;margin-right:1.2rem;" />
			</div>
			<!-- Menú escritorio -->
			<ul class="enlaces-navegacion solo-escritorio" style="height:32px;align-items:center;">
				<li><a href="#" class="enlace-menu" @click.prevent="scrollToInicio">Inicio</a></li>
				<li class="dropdown-item">
					<a href="#" class="enlace-menu">Tienda <span class="dropdown-arrow">▼</span></a>
					<ul class="dropdown-submenu">
						<li><a href="#maquinaria" class="submenu-link" @click.prevent="scrollToMaquinaria">Maquinaria Industrial</a></li>
						<li><a href="#panaderia" class="submenu-link" @click.prevent="scrollToPanaderia">Panadería</a></li>
					</ul>
				</li>
				<li><a href="#sobre-nosotros" class="enlace-menu" @click.prevent="scrollToSobreNosotros">Sobre Nosotros</a></li>
				<li><a href="#contacto" class="enlace-menu" @click.prevent="scrollToContacto">Contáctanos</a></li>
				<li style="position:relative;">
					<button class="boton-buscar" @click="toggleBuscador" :aria-expanded="buscadorAbierto" aria-label="Buscar productos" style="background:transparent;border:none;color:#fff;cursor:pointer;padding:0.4rem 0.8rem;border-radius:8px;transition:background 0.2s;">
						<svg width="20" height="20" fill="none" stroke="currentColor" viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"></circle><path d="m21 21-4.35-4.35"></path></svg>
					</button>
					<transition name="fade">
						<input v-if="buscadorAbierto" ref="inputBuscar" type="text" placeholder="Buscar productos..." class="input-buscar" style="position:absolute;top:100%;right:0;background:#fff;border:2px solid #2563eb;border-radius:10px;padding:0.5rem 1rem;font-size:0.9rem;width:220px;margin-top:0.5rem;z-index:1001;" @blur="cerrarBuscador" />
					</transition>
				</li>
			</ul>
			
			<!-- Botón menú móvil -->
			<button class="boton-menu-movil solo-movil" @click="menuMovilAbierto = !menuMovilAbierto" aria-label="Toggle navigation menu" style="background:transparent;border:none;color:#fff;font-size:1.5rem;cursor:pointer;padding:0.5rem;">☰</button>
		</nav>
		
		<!-- Menú móvil -->
		<div class="menu-movil solo-movil" v-show="menuMovilAbierto" style="background:rgba(6,26,72,0.98);padding:1rem 2rem;border-top:1px solid rgba(255,255,255,0.1);">
			<ul style="list-style:none;padding:0;margin:0;">
				<li style="margin-bottom:0.5rem;"><a href="#" @click.prevent="scrollToInicio; menuMovilAbierto = false" style="color:#fff;text-decoration:none;font-size:1.1rem;">Inicio</a></li>
				<li style="margin-bottom:0.5rem;"><a href="#maquinaria" @click.prevent="scrollToMaquinaria; menuMovilAbierto = false" style="color:#fff;text-decoration:none;font-size:1.1rem;">Maquinaria Industrial</a></li>
				<li style="margin-bottom:0.5rem;"><a href="#panaderia" @click.prevent="scrollToPanaderia; menuMovilAbierto = false" style="color:#fff;text-decoration:none;font-size:1.1rem;">Panadería</a></li>
				<li style="margin-bottom:0.5rem;"><a href="#sobre-nosotros" @click.prevent="scrollToSobreNosotros; menuMovilAbierto = false" style="color:#fff;text-decoration:none;font-size:1.1rem;">Sobre Nosotros</a></li>
				<li><a href="#contacto" @click.prevent="scrollToContacto; menuMovilAbierto = false" style="color:#fff;text-decoration:none;font-size:1.1rem;">Contáctanos</a></li>
			</ul>
		</div>
	</header>

	<main style="margin-top:56px;">
		<div class="tarjeta-carrusel" @mouseenter="pausarCarrusel" @mouseleave="reanudarCarrusel">
			<div class="diapositivas-carrusel">
				<img v-for="(img, idx) in portadas" :key="img.src" :src="img.src" :alt="img.alt" class="portada" :style="{ opacity: indicePortada === idx ? 1 : 0, zIndex: indicePortada === idx ? 2 : 1, transition: 'opacity 0.7s' }" loading="lazy" />
				<div :class="['texto-carrusel', { oculto: textoOculto }]">
					Soluciones Innovadoras para la Industria y el Agro
				</div>
				<button class="carousel-control carousel-prev" @click="anteriorPortada" aria-label="Imagen anterior" title="Imagen anterior">&#10094;</button>
				<button class="carousel-control carousel-next" @click="siguientePortada" aria-label="Imagen siguiente" title="Imagen siguiente">&#10095;</button>
				<div class="carousel-indicators" role="tablist" aria-label="Indicadores de carrusel">
					<span v-for="(img, idx) in portadas" :key="'indicador-' + idx" :class="['carousel-indicator', { active: indicePortada === idx } ]" @click="indicePortada = idx" :aria-label="`Ir a imagen ${idx + 1}`" role="tab" :aria-selected="indicePortada === idx"></span>
				</div>
			</div>
		</div>
		
		<div class="tarjeta-maquinaria-industrial">
			<div class="fila-tarjeta">
				<div class="imagen-portada-extra">
					<img src="./assets/TS-754.png" alt="TS-754" class="portada-extra" style="max-width:440px;max-height:440px;display:block;margin:0 auto;" loading="lazy" />
				</div>
				<div class="texto-portada-extra">
					<div class="info-ts754">
						<h2>MAQUINARIA INDUSTRIAL</h2>
						<p class="productos-vendidos">Más de 5,000 ventas</p>
						<button class="boton-panaderia" @click="mostrarMaquinaria = true">Más información</button>
					</div>
				</div>
			</div>
		</div>

		<div class="tarjeta-panaderia">
			<div class="fila-tarjeta">
				<div class="imagen-portada-extra">
					<img src="./assets/batidora1.png" alt="Batidora Panadería" class="portada-extra" style="max-width:440px;max-height:440px;display:block;margin:0 auto;" loading="lazy" />
				</div>
				<div class="texto-portada-extra">
					<div class="info-ts754">
						<h2>PANADERÍA</h2>
						<p class="productos-vendidos">Más de 13,000 ventas</p>
						<button class="boton-panaderia">Más información</button>
					</div>
				</div>
			</div>
		</div>

		<MaqAgriPage v-if="mostrarMaquinariaAgricola" :titulo="'Maquinaria Agrícola TS-754'" :imagen="'/src/assets/TS-754-IMAGEN1.png'" @close="mostrarMaquinariaAgricola = false" />
		<MaqAgriPage v-if="mostrarMaquinaria" :titulo="'Maquinaria Industrial TS-754'" :imagen="'/src/assets/TS-754-IMAGEN1.png'" @close="mostrarMaquinaria = false" />

		<!-- Sección Testimonios Clientes -->
		<section class="tarjeta-testimonios">
			<h2 style="text-align:center;color:#2563eb;margin-bottom:2rem;">Lo que dicen nuestros clientes</h2>
			<div class="testimonios-cards" style="display:flex;gap:2rem;justify-content:center;flex-wrap:wrap;">
				<div class="testimonio-card" style="background:#fff;border-radius:14px;box-shadow:0 2px 12px rgba(37,99,235,0.07);padding:1.5rem 1.2rem;max-width:320px;flex:1 1 220px;">
					<div class="testimonio-perfil" style="display:flex;align-items:center;margin-bottom:1rem;">
						<div class="avatar" style="width:50px;height:50px;border-radius:50%;background:#2563eb;display:flex;align-items:center;justify-content:center;color:#fff;font-weight:600;font-size:1.1rem;margin-right:1rem;">JP</div>
						<div>
							<div style="color:#2563eb;font-weight:600;font-size:1rem;">Juan Pérez</div>
							<div style="color:#6b7280;font-size:0.85rem;">Agroindustrias JP</div>
						</div>
					</div>
					<p style="font-size:1.08rem;color:#2c3e50;margin-bottom:0;">"Excelente atención y productos de calidad. Mi empresa ha mejorado mucho gracias a Savreh."</p>
				</div>
				<div class="testimonio-card" style="background:#fff;border-radius:14px;box-shadow:0 2px 12px rgba(37,99,235,0.07);padding:1.5rem 1.2rem;max-width:320px;flex:1 1 220px;">
					<div class="testimonio-perfil" style="display:flex;align-items:center;margin-bottom:1rem;">
						<div class="avatar" style="width:50px;height:50px;border-radius:50%;background:#059669;display:flex;align-items:center;justify-content:center;color:#fff;font-weight:600;font-size:1.1rem;margin-right:1rem;">MG</div>
						<div>
							<div style="color:#2563eb;font-weight:600;font-size:1rem;">María Gómez</div>
							<div style="color:#6b7280;font-size:0.85rem;">Soluciones Industriales</div>
						</div>
					</div>
					<p style="font-size:1.08rem;color:#2c3e50;margin-bottom:0;">"La maquinaria industrial que adquirimos superó nuestras expectativas. Recomendados."</p>
				</div>
				<div class="testimonio-card" style="background:#fff;border-radius:14px;box-shadow:0 2px 12px rgba(37,99,235,0.07);padding:1.5rem 1.2rem;max-width:320px;flex:1 1 220px;">
					<div class="testimonio-perfil" style="display:flex;align-items:center;margin-bottom:1rem;">
						<div class="avatar" style="width:50px;height:50px;border-radius:50%;background:#dc2626;display:flex;align-items:center;justify-content:center;color:#fff;font-weight:600;font-size:1.1rem;margin-right:1rem;">CR</div>
						<div>
							<div style="color:#2563eb;font-weight:600;font-size:1rem;">Carlos Ruiz</div>
							<div style="color:#6b7280;font-size:0.85rem;">EcoEnergia</div>
						</div>
					</div>
					<p style="font-size:1.08rem;color:#2c3e50;margin-bottom:0;">"Muy satisfecho con el servicio y la asesoría. Los equipos solares funcionan perfecto."</p>
				</div>
			</div>
		</section>

		<!-- Sección Sobre Nosotros -->
		<section id="sobre-nosotros" class="tarjeta-nosotros">
			<div class="sobre-nosotros-content">
				<h2>Sobre Nosotros</h2>
				<div class="sobre-nosotros-cards">
					<div class="sobre-nosotros-card">
						<h3>Misión</h3>
						<p>Brindar soluciones innovadoras y de calidad para la industria y el agro, contribuyendo al desarrollo sostenible y la satisfacción de nuestros clientes.</p>
					</div>
					<div class="sobre-nosotros-card">
						<h3>Visión</h3>
						<p>Ser la empresa líder en el mercado nacional e internacional de maquinaria industrial y agrícola, reconocida por nuestra excelencia y compromiso.</p>
					</div>
					<div class="sobre-nosotros-card">
						<h3>Valores</h3>
						<p>Impulsar el crecimiento de nuestros clientes mediante productos y servicios que generen valor, confianza y resultados sostenibles.</p>
					</div>
				</div>
			</div>
		</section>

		<!-- Sección Contáctanos -->
		<section id="contacto" class="tarjeta-contacto">
			<div class="info-contacto">
				<h2>Contáctanos</h2>
				<p>¿Tienes alguna pregunta o necesitas más información sobre nuestros productos?</p>
				<div class="redes-contacto">
					<a class="item-contacto" href="https://www.facebook.com/p/Savreh-SA-61563909317105/" target="_blank" rel="noopener" aria-label="Visitar Facebook de Savreh">Facebook</a>
					<a class="item-contacto" href="https://www.instagram.com/savreh.ec/" target="_blank" rel="noopener" aria-label="Visitar Instagram de Savreh">Instagram</a>
					<a class="item-contacto" href="https://www.tiktok.com/@savreh.ec" target="_blank" rel="noopener" aria-label="Visitar TikTok de Savreh">TikTok</a>
					<a class="item-contacto item-whatsapp" href="https://wa.link/hj2t5j" target="_blank" rel="noopener" aria-label="Contactar por WhatsApp">
						<svg width="20" height="20" fill="currentColor" viewBox="0 0 24 24">
							<path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.890-5.335 11.893-11.893A11.821 11.821 0 0020.885 3.488"/>
						</svg>
						WhatsApp
					</a>
				</div>
			</div>
			<form class="formulario-contacto" @submit.prevent="enviarFormulario">
				<input type="text" placeholder="Nombre" v-model="formulario.nombre" required />
				<input type="email" placeholder="Email" v-model="formulario.email" required />
				<textarea placeholder="Mensaje" v-model="formulario.mensaje" required></textarea>
				<button type="submit" class="boton-enviar">Enviar Mensaje</button>
			</form>
		</section>

		<!-- Botón flotante de WhatsApp -->
		<a 
			href="https://wa.link/hj2t5j" 
			class="whatsapp-flotante" 
			target="_blank" 
			rel="noopener"
			aria-label="Contactar por WhatsApp"
		>
			<svg width="30" height="30" fill="currentColor" viewBox="0 0 24 24">
				<path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.890-5.335 11.893-11.893A11.821 11.821 0 0020.885 3.488"/>
			</svg>
		</a>

		<!-- Pie de página -->
		<footer class="footer-copyright">
			&copy; Copyright Savreh
		</footer>
	</main>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import MaqAgriPage from './page/maq_agricola_page.vue'
import portadaNova from './assets/portada-nova.jpg'
import portada2 from './assets/portada2.png'
import portada3 from './assets/portada3.png'

// Variables reactivas
const indicePortada = ref(0)
const textoOculto = ref(false)
const menuMovilAbierto = ref(false)
const buscadorAbierto = ref(false)
const inputBuscar = ref(null)
const intervaloCarrusel = ref(null)
const mostrarMaquinaria = ref(false)
const mostrarMaquinariaAgricola = ref(false)

const formulario = ref({
	nombre: '',
	email: '',
	mensaje: ''
})

const portadas = [
	{ src: portadaNova, alt: 'Nova - Soluciones Industriales y Agrícolas' },
	{ src: portada2, alt: 'Portada 2' },
	{ src: portada3, alt: 'Portada 3' }
]

// Métodos del carrusel
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

// Métodos de navegación
function scrollToInicio() {
	window.scrollTo({ top: 0, behavior: 'smooth' })
}

function scrollToMaquinaria() {
	const maquinaria = document.querySelector('.tarjeta-maquinaria-industrial')
	if (maquinaria) {
		maquinaria.scrollIntoView({ behavior: 'smooth' })
	}
}

function scrollToPanaderia() {
	const panaderia = document.querySelector('.tarjeta-panaderia')
	if (panaderia) {
		panaderia.scrollIntoView({ behavior: 'smooth' })
	}
}

function scrollToSobreNosotros() {
	const sobreNosotros = document.getElementById('sobre-nosotros')
	if (sobreNosotros) {
		sobreNosotros.scrollIntoView({ behavior: 'smooth' })
	}
}

function scrollToContacto() {
	const contacto = document.getElementById('contacto')
	if (contacto) {
		contacto.scrollIntoView({ behavior: 'smooth' })
	}
}

// Métodos del buscador
function toggleBuscador() {
	buscadorAbierto.value = !buscadorAbierto.value
	if (buscadorAbierto.value) {
		setTimeout(() => {
			inputBuscar.value?.focus()
		}, 100)
	}
}

function cerrarBuscador(event) {
	if (!event.relatedTarget || !event.relatedTarget.closest('.boton-buscar')) {
		buscadorAbierto.value = false
	}
}

// Método del formulario
function enviarFormulario() {
	alert('Mensaje enviado. Nos contactaremos contigo pronto.')
	formulario.value = { nombre: '', email: '', mensaje: '' }
}

// Lifecycle hooks
onMounted(() => {
	// Ocultar texto del carrusel después de 3 segundos
	setTimeout(() => {
		textoOculto.value = true
	}, 3000)

	// Iniciar carrusel automático
	intervaloCarrusel.value = setInterval(siguientePortada, 4000)

	// Listeners para cerrar menús al hacer clic fuera
	document.addEventListener('click', (e) => {
		if (!e.target.closest('.boton-menu-movil') && !e.target.closest('.menu-movil')) {
			menuMovilAbierto.value = false
		}
		if (!e.target.closest('.boton-buscar') && !e.target.closest('.input-buscar')) {
			buscadorAbierto.value = false
		}
	})

	// Navegación con teclado para el carrusel
	document.addEventListener('keydown', (e) => {
		if (e.key === 'ArrowLeft') {
			anteriorPortada()
		}
		if (e.key === 'ArrowRight') {
			siguientePortada()
		}
	})
})

onUnmounted(() => {
	if (intervaloCarrusel.value) {
		clearInterval(intervaloCarrusel.value)
	}
})
</script>