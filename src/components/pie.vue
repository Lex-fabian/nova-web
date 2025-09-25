<template>
  <footer class="site-footer">
    <div class="container">
      <div class="footer-grid">
        <div class="brand">
          <img src="../assets/logo-nova.png" alt="Savreh" class="brand-logo" />
          <p class="brand-desc">Soluciones industriales y agrícolas que impulsan tu negocio.</p>
        </div>
        <nav class="footer-nav" aria-label="Enlaces del pie">
          <a href="#maquinaria">Maquinaria</a>
          <a href="#panaderia">Panadería</a>
          <a href="#sobre-nosotros">Sobre Nosotros</a>
          <a href="#contacto">Contacto</a>
        </nav>
        <div class="footer-copy">&copy; {{ year }} Savreh</div>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { ref } from 'vue'
const year = ref(new Date().getFullYear())
</script>

<style scoped>
.site-footer { background: linear-gradient(180deg,#061a48 0%, #0a213f 100%); color:#fff; padding:2rem 1rem; }
.container { max-width:1100px; margin:0 auto; }
.footer-grid { display:flex; gap:1rem; align-items:center; justify-content:space-between; }
.brand-logo { height:44px; }
.brand-desc { color:rgba(255,255,255,0.85); margin-top:0.5rem; }
.footer-nav a { color:rgba(255,255,255,0.9); margin-right:0.75rem; text-decoration:none }
.footer-copy { color:rgba(255,255,255,0.7); }
@media (max-width:900px) {
  .footer-grid { flex-direction:column; text-align:center; gap:0.75rem }
}
</style>
