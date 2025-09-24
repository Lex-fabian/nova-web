import './style/web/contactanosweb.css'
import './style/movil/contactanosmobil.css'
<script setup>
import { ref, onMounted, watch, onUnmounted } from 'vue'
import './style.css'
import './style-mobil.css'

const menuAbierto = ref(false)
const submenuTiendaAbierto = ref(false)

const productos = ref([
  { id: 1, nombre: 'Producto 1', precio: '€19.99', imagen: 'https://via.placeholder.com/250', descripcion: 'Esta es una breve descripción del producto 1, destacando sus características principales.' },
  { id: 2, nombre: 'Producto 2', precio: '€29.99', imagen: 'https://via.placeholder.com/250', descripcion: 'Descripción detallada para el producto 2. Es excelente y de alta calidad.' },
  { id: 3, nombre: 'Producto 3', precio: '€39.99', imagen: 'https://via.placeholder.com/250', descripcion: 'El producto 3 ofrece una solución innovadora y duradera para sus necesidades.' },
  { id: 4, nombre: 'Producto 4', precio: '€49.99', imagen: 'https://via.placeholder.com/250', descripcion: 'No te pierdas el producto 4, la mejor opción en el mercado actual.' },
])

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

function siguientePortada() {
  indicePortada.value = (indicePortada.value + 1) % portadas.length
}
function anteriorPortada() {
  indicePortada.value = (indicePortada.value - 1 + portadas.length) % portadas.length
}

onMounted(() => {
  intervaloCarrusel = setInterval(siguientePortada, 4000)
})
onUnmounted(() => {
  clearInterval(intervaloCarrusel)
})

const testimonios = ref([
  { id: 1, texto: '¡Excelente servicio y productos de alta calidad! Totalmente recomendado.', autor: 'Ana Pérez', imagen: 'https://i.pravatar.cc/100?u=ana' },
  { id: 2, texto: 'La maquinaria que compré superó mis expectativas. El soporte técnico es inmejorable.', autor: 'Carlos Gómez', imagen: 'https://i.pravatar.cc/100?u=carlos' },
  { id: 3, texto: 'Muy satisfecho con la compra. La entrega fue rápida y el personal muy amable.', autor: 'Lucía Fernández', imagen: 'https://i.pravatar.cc/100?u=lucia' }
])

function alternarMenu() {
  menuAbierto.value = !menuAbierto.value
  if (!menuAbierto.value) {
    submenuTiendaAbierto.value = false
  }
}

function alternarSubmenuTienda() {
  submenuTiendaAbierto.value = !submenuTiendaAbierto.value
}

watch(menuAbierto, (abierto) => {
  if (abierto) {
    document.body.classList.add('no-scroll');
  } else {
    document.body.classList.remove('no-scroll');
  }
})

onUnmounted(() => {
  document.body.classList.remove('no-scroll');
})

onMounted(() => {
  const observador = new IntersectionObserver((entradas) => {
    entradas.forEach(entrada => {
      if (entrada.isIntersecting) {
        entrada.target.classList.add('is-visible');
        observador.unobserve(entrada.target);
      }
    });
  }, {
    threshold: 0.1
  });

  document.querySelectorAll('.animar-al-desplazar').forEach((el) => {
    observador.observe(el);
  });

  const encabezado = document.querySelector('header');
  window.addEventListener('scroll', () => {
    if (window.scrollY > 50) {
      encabezado.classList.add('desplazado');
    } else {
      encabezado.classList.remove('desplazado');
    }
  });

  document.addEventListener('contextmenu', (e) => e.preventDefault());
  document.addEventListener('keydown', (e) => {
    if (e.ctrlKey && (e.key === 'c' || e.key === 'a' || e.key === 's' || e.key === 'u')) {
      e.preventDefault();
    }
    if (e.key === 'F12') {
      e.preventDefault();
    }
  });
})
</script>

<template>
  <div class="superposicion-menu" :class="{ 'activo': menuAbierto }" @click="alternarMenu"></div>
  <encabezado>
    <navegacion-encabezado>
      <logo-encabezado>
        <img src="./assets/icono_savreh.png" alt="Icono Savreh" class="logo" width="90" height="30" />
      </logo-encabezado>

      <!-- Menú web solo escritorio -->
      <ul class="enlaces-navegacion-web solo-escritorio">
        <li><a href="#" class="enlace-menu">Inicio</a></li>
        <li class="elemento-con-desplegable" tabindex="0">
          <a href="#" class="enlace-menu">Tienda <span class="flecha-desplegable">&#9662;</span></a>
          <ul class="submenu-desplegable">
            <li><a href="#" class="enlace-submenu">Maquinaria Agrícola</a></li>
            <li><a href="#" class="enlace-submenu">Equipos de Energía Solar</a></li>
            <li><a href="#" class="enlace-submenu">Acabados</a></li>
            <li><a href="#" class="enlace-submenu">Maquinaria Industrial</a></li>
            <li><a href="#" class="enlace-submenu">Otros</a></li>
          </ul>
        </li>
        <li>
          <a href="#contactanos" class="enlace-menu">Contáctanos</a>
        </li>
        <li><a href="#sobre-nosotros" class="enlace-menu">Sobre Nosotros</a></li>
      </ul>
      <!-- Menú móvil solo móvil -->
      <!-- Menú hamburguesa móvil visual -->
      <button class="menu-hamburguesa solo-movil" @click="alternarMenu" :class="{ 'activo': menuAbierto }" aria-label="Abrir menú" tabindex="0">
        <span :style="{ transform: menuAbierto ? 'rotate(45deg) translate(6px, 6px)' : 'none', background: menuAbierto ? '#2563eb' : '#031641' }"></span>
        <span :style="{ opacity: menuAbierto ? 0 : 1, background: menuAbierto ? '#2563eb' : '#031641' }"></span>
        <span :style="{ transform: menuAbierto ? 'rotate(-45deg) translate(7px, -7px)' : 'none', background: menuAbierto ? '#2563eb' : '#031641' }"></span>
      </button>
      <ul class="enlaces-navegacion-movil solo-movil" :class="{ 'activo': menuAbierto }">
        <div class="encabezado-menu-movil">
          <img src="./assets/icono_savreh.png" alt="Icono Savreh" class="logo" width="70" height="24" />
          <span class="titulo-menu-movil">Menú</span>
        </div>
        <li @click="alternarMenu"><a href="#" class="enlace-menu-movil">Inicio</a></li>
        <li class="elemento-con-desplegable-movil" :class="{ 'submenu-abierto-movil': submenuTiendaAbierto }">
          <a href="#" @click.prevent="alternarSubmenuTienda" class="enlace-menu-movil">Tienda <span class="flecha-desplegable-movil">&#9662;</span></a>
          <ul class="submenu-desplegable-movil" :class="{ 'activo': submenuTiendaAbierto }">
            <li @click="alternarMenu"><a href="#" class="enlace-submenu-movil">Maquinaria Agrícola</a></li>
            <li @click="alternarMenu"><a href="#" class="enlace-submenu-movil">Equipos de Energía Solar</a></li>
            <li @click="alternarMenu"><a href="#" class="enlace-submenu-movil">Acabados</a></li>
            <li @click="alternarMenu"><a href="#" class="enlace-submenu-movil">Maquinaria Industrial</a></li>
            <li @click="alternarMenu"><a href="#" class="enlace-submenu-movil">Otros</a></li>
          </ul>
        </li>
        <li @click="alternarMenu"><a href="#contactanos" class="enlace-menu-movil">Contáctanos</a></li>
        <li @click="alternarMenu"><a href="#sobre-nosotros" class="enlace-menu-movil">Sobre Nosotros</a></li>
        <div class="pie-menu-movil">
          <div class="copyright">
            <p>&copy; 2024 SAVREH S.A.</p>
          </div>
        </div>
      </ul>
    </navegacion-encabezado>
  </encabezado>
  <div class="contenedor-carrusel">
    <div class="diapositivas-carrusel">
      <img
        v-for="(portada, idx) in portadas"
        :key="portada.src"
        :src="portada.src"
        :alt="portada.alt"
        class="portada"
        loading="lazy"
        :style="{ opacity: indicePortada === idx ? 1 : 0, zIndex: indicePortada === idx ? 2 : 1, transition: 'opacity 0.7s' }"
      />
      <button class="carrusel-control carrusel-anterior" @click="anteriorPortada" aria-label="Anterior">&#10094;</button>
      <button class="carrusel-control carrusel-siguiente" @click="siguientePortada" aria-label="Siguiente">&#10095;</button>
      <div class="carrusel-indicadores">
        <span
          v-for="(portada, idx) in portadas"
          :key="'indicador-' + idx"
          :class="['carrusel-indicador', { activo: indicePortada === idx }]"
          @click="indicePortada = idx"
        ></span>
      </div>
    </div>
    <div class="texto-hero">
      <p>Soluciones Innovadoras para la Industria y el Agro</p>
    </div>
  </div>

  <div class="fila-portada-extra">
    <div class="texto-portada-extra">
      <div class="info-ts754">
        <h2>Maquinaria Agrícola TS-754</h2>
        <p class="productos-vendidos">Más de 20,000 productos vendidos</p>
        <button class="boton-mas-info">Más información</button>
      </div>
    </div>
    <div class="imagen-portada-extra">
      <img src="./assets/TS-754-IMAGEN1.png" alt="Imagen TS-754" class="portada-extra" loading="lazy" />
    </div>
  </div>
  <div class="principal">
    <div class="seccion-info animar-al-desplazar aparecer-arriba" id="sobre-nosotros">
      <div class="texto-info">
        <h2>Sobre Nosotros</h2>
        <p>
          En SAVREH S.A. Trabajamos duro para ofrecerte los productos de mejor calidad.
        </p>
        <p>
          Desde 2003, SAVREH S.A. se especializa en la importación y distribución de equipos industrial. Ubicada en Lasso provincia de Cotopaxi, dispone de una amplia gama de implementos y maquinarias agrícolas, paneles de aluminio, calefones y lámpara solares. Todos los equipos importados por SAVREH poseen un amplio stock de repuestos, así como técnicos calificados, comprometidos en brindar un buen servicio. Nuestros productos cuentan con garantía y provienen de empresas con Certificación de Calidad ISO 9001.
        </p>
        <h3>MISIÓN</h3>
        <p>
          SAVREH S.A. fue creada en 2003, dedicada a la importación y distribución de maquinaria agrícola, paneles de aluminio, calefones, lámparas solares; con precios competitivos en el mercado. Nuestros proveedores cuentan con certificación ISO 9001, garantizando así la calidad de los equipos.
        </p>
        <h3>VISIÓN</h3>
        <p>
          Ser reconocida a nivel nacional como una empresa importadora, que busca satisfacer las necesidades de sus clientes, con un amplio stock de equipos y repuestos, con técnicas calificadas y comprometidos en brindar un buen servicio.
        </p>
        <h3>NUESTRO EQUIPO</h3>
        <p>
          Contamos con un equipo multidisciplinario de expertos profesionales que trabajan bajo los más exigentes parámetros de calidad, convirtiéndose en un apoyo estratégico para nuestros clientes. Somos especialistas en varios segmentos de negocios, tenemos un conocimiento detallado de las empresas y sus operaciones, lo que asegura apoyo y soporte técnico especializado no sólo a nuestros equipos sino a nuestros clientes.
        </p>
      </div>
    </div>
    <!-- Eliminada la grilla de productos y detalles -->
    <div class="seccion-testimonios animar-al-desplazar aparecer-arriba">
      <h2 class="animar-al-desplazar">Lo que dicen nuestros clientes</h2>
      <div class="contenedor-testimonios">
        <div v-for="(testimonio, indice) in testimonios" :key="testimonio.id" class="tarjeta-testimonio animar-al-desplazar" :style="{ transitionDelay: `${indice * 180}ms` }">
          <img :src="testimonio.imagen" :alt="testimonio.autor" class="imagen-testimonio" loading="lazy"/>
          <p class="texto-testimonio">"{{ testimonio.texto }}"</p>
          <p class="autor-testimonio">- {{ testimonio.autor }}</p>
        </div>
      </div>
    </div>
    <Contactanos />
    <!-- Sección Contáctanos -->
    <div class="seccion-contactanos animar-al-desplazar aparecer-arriba" id="contactanos">
      <div class="contactanos-info">
        <h2>Contáctanos</h2>
        <p>¿Tienes preguntas o necesitas asesoría personalizada? Nuestro equipo está listo para ayudarte.</p>
        <div class="contactanos-datos">
          <div class="contacto-item">
            <i class="fas fa-phone-alt"></i>
            <span>Teléfono: <a href="tel:+593999999999">+593 99 999 9999</a></span>
          </div>
          <div class="contacto-item">
            <i class="fas fa-envelope"></i>
            <span>Email: <a href="mailto:info@savreh.com">info@savreh.com</a></span>
          </div>
          <div class="contacto-item">
            <i class="fab fa-whatsapp"></i>
            <span>WhatsApp: <a href="https://wa.link/dgy5gs" target="_blank" rel="noopener">Contáctanos</a></span>
          </div>
        </div>
        <form class="formulario-contacto" @submit.prevent>
          <input type="text" placeholder="Nombre" required />
          <input type="email" placeholder="Correo electrónico" required />
          <textarea placeholder="Mensaje" rows="4" required></textarea>
          <button type="submit" class="boton-enviar">Enviar mensaje</button>
        </form>
      </div>
    </div>
  </div>
  <pie-pagina>
    <pie-social>
      <a href="#" target="_blank" class="enlace-social"><i class="fab fa-instagram"></i></a>
      <a href="#" target="_blank" class="enlace-social"><i class="fab fa-facebook-f"></i></a>
    </pie-social>
    <div class="copyright-pie">
      <p>Copyright &copy; SAVREH powered by SAVREH</p>
    </div>
  </pie-pagina>
  <a href="https://wa.link/dgy5gs" target="_blank" rel="noopener noreferrer" class="boton-flotante" aria-label="Contactar por WhatsApp">
    <i class="fab fa-whatsapp"></i>
  </a>
</template>