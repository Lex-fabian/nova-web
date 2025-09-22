<script setup>
import { ref, onMounted, watch, onUnmounted } from 'vue'
import Contactanos from './components/contactanos.vue'
import './style.css'
import './style-mobil.css'

const isMenuOpen = ref(false)
const isShopSubmenuOpen = ref(false)

const products = ref([
  { id: 1, name: 'Producto 1', price: '€19.99', image: 'https://via.placeholder.com/250', description: 'Esta es una breve descripción del producto 1, destacando sus características principales.' },
  { id: 2, name: 'Producto 2', price: '€29.99', image: 'https://via.placeholder.com/250', description: 'Descripción detallada para el producto 2. Es excelente y de alta calidad.' },
  { id: 3, name: 'Producto 3', price: '€39.99', image: 'https://via.placeholder.com/250', description: 'El producto 3 ofrece una solución innovadora y duradera para sus necesidades.' },
  { id: 4, name: 'Producto 4', price: '€49.99', image: 'https://via.placeholder.com/250', description: 'No te pierdas el producto 4, la mejor opción en el mercado actual.' },
])

const testimonials = ref([
  { id: 1, text: '¡Excelente servicio y productos de alta calidad! Totalmente recomendado.', author: 'Ana Pérez', image: 'https://i.pravatar.cc/100?u=ana' },
  { id: 2, text: 'La maquinaria que compré superó mis expectativas. El soporte técnico es inmejorable.', author: 'Carlos Gómez', image: 'https://i.pravatar.cc/100?u=carlos' },
  { id: 3, text: 'Muy satisfecho con la compra. La entrega fue rápida y el personal muy amable.', author: 'Lucía Fernández', image: 'https://i.pravatar.cc/100?u=lucia' }
])

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value
  if (!isMenuOpen.value) {
    isShopSubmenuOpen.value = false
  }
}

function toggleShopSubmenu() {
  isShopSubmenuOpen.value = !isShopSubmenuOpen.value
}

watch(isMenuOpen, (isOpen) => {
  if (isOpen) {
    document.body.classList.add('no-scroll');
  } else {
    document.body.classList.remove('no-scroll');
  }
})

onUnmounted(() => {
  document.body.classList.remove('no-scroll');
})

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible');
        observer.unobserve(entry.target);
      }
    });
  }, {
    threshold: 0.1
  });

  document.querySelectorAll('.animate-on-scroll').forEach((el) => {
    observer.observe(el);
  });

  const header = document.querySelector('header');
  window.addEventListener('scroll', () => {
    if (window.scrollY > 50) {
      header.classList.add('scrolled');
    } else {
      header.classList.remove('scrolled');
    }
  });

  // Disable right-click context menu
  document.addEventListener('contextmenu', (e) => e.preventDefault());
  
  // Disable common keyboard shortcuts
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
  <div class="overlay-menu" :class="{ 'is-active': isMenuOpen }" @click="toggleMenu"></div>
  <header>
    <nav>
      <img src="./assets/logo-nova.png" alt="Nova Logo" class="logo" />
      <button class="menu-hamburguesa" @click="toggleMenu" :class="{ 'is-active': isMenuOpen }">
        <span></span>
        <span></span>
        <span></span>
      </button>
      <ul class="enlaces-navegacion" :class="{ 'is-active': isMenuOpen }">
        <div class="menu-header">
          <img src="./assets/logo-nova.png" alt="Nova Logo" class="logo" />
          <span class="menu-title">Menú</span>
        </div>
        <li @click="toggleMenu"><a href="#">Inicio</a></li>
        <li class="elemento-con-dropdown" :class="{ 'submenu-abierto': isShopSubmenuOpen }">
          <a href="#" @click.prevent="toggleShopSubmenu">Tienda <span class="flecha-dropdown">&#9662;</span></a>
          <ul class="submenu-dropdown" :class="{ 'is-active': isShopSubmenuOpen }">
            <li @click="toggleMenu"><a href="#">Maquinaria Agrícola</a></li>
            <li @click="toggleMenu"><a href="#">Equipos de Energía Solar</a></li>
            <li @click="toggleMenu"><a href="#">Acabados</a></li>
            <li @click="toggleMenu"><a href="#">Maquinaria Industrial</a></li>
            <li @click="toggleMenu"><a href="#">Otros</a></li>
          </ul>
        </li>
        <li @click="toggleMenu"><a href="#contactanos">Contáctanos</a></li>
        <li @click="toggleMenu"><a href="#sobre-nosotros">Sobre Nosotros</a></li>
        <div class="menu-footer">
          <div class="social-links">
            <a href="#" target="_blank" class="social-link">
              <i class="fab fa-instagram"></i>
            </a>
            <a href="#" target="_blank" class="social-link">
              <i class="fab fa-facebook-f"></i>
            </a>
          </div>
          <div class="copyright">
            <p>&copy; 2024 SAVREH S.A.</p>
          </div>
        </div>
      </ul>
    </nav>
  </header>
  <div class="carrusel-container">
    <div class="carrusel-diapositivas">
      <img src="./assets/portada-nova.jpg" alt="Portada Nova" class="portada" />
      <img src="./assets/portada-dos-nova.png" alt="Portada Dos Nova" class="portada" />
      <img src="./assets/portada-nova.jpg" alt="Portada Nova" class="portada" />
    </div>
    <div class="hero-texto">
      <p>Soluciones Innovadoras para la Industria y el Agro.</p>
    </div>
  </div>
  <main>
    <div class="info-section animate-on-scroll fade-in-up" id="sobre-nosotros">
      <div class="info-texto">
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

    <div class="grilla-productos animate-on-scroll fade-in-up">
      <div v-for="(product, index) in products" :key="product.id" class="tarjeta-producto animate-on-scroll" :style="{ transitionDelay: `${index * 100}ms` }">
        <img :src="product.image" :alt="product.name" class="imagen-producto"/>
        <div class="producto-info">
          <h3>{{ product.name }}</h3>
          <p class="descripcion">{{ product.description }}</p>
          <p class="precio">{{ product.price }}</p>
          <button>Más información</button>
        </div>
      </div>
    </div>

    <div class="seccion-testimonios animate-on-scroll fade-in-up">
      <h2 class="animate-on-scroll">Lo que dicen nuestros clientes</h2>
      <div class="contenedor-testimonios">
        <div v-for="(testimonial, index) in testimonials" :key="testimonial.id" class="tarjeta-testimonio animate-on-scroll" :style="{ transitionDelay: `${index * 150}ms` }">
          <img :src="testimonial.image" :alt="testimonial.author" class="imagen-testimonio"/>
          <p class="texto-testimonio">"{{ testimonial.text }}"</p>
          <p class="autor-testimonio">- {{ testimonial.author }}</p>
        </div>
      </div>
    </div>

    <Contactanos />
  </main>
  <footer>
    <p>Copyright &copy; SAVREH powered by SAVREH</p>
  </footer>
  <a href="https://wa.link/dgy5gs" target="_blank" rel="noopener noreferrer" class="boton-flotante">
    <i class="fab fa-whatsapp"></i>
  </a>
</template>