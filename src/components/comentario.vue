<template>
  <section class="comentarios" aria-label="Testimonios de clientes">
    <h2 class="comentarios__titulo">Lo que dicen nuestros clientes</h2>
    <div class="comentarios__grid">
      <article class="comentario-card">
        <div class="avatar">JP</div>
        <div class="contenido">
          <h3 class="nombre">Juan Pérez</h3>
          <p class="empresa">Agroindustrias JP</p>
          <p class="texto">"Excelente atención y productos de calidad. Mi empresa ha mejorado mucho gracias a Savreh."</p>
        </div>
      </article>

      <article class="comentario-card">
        <div class="avatar avatar--verde">MG</div>
        <div class="contenido">
          <h3 class="nombre">María Gómez</h3>
          <p class="empresa">Soluciones Industriales</p>
          <p class="texto">"La maquinaria industrial que adquirimos superó nuestras expectativas. Recomendados."</p>
        </div>
      </article>

      <article class="comentario-card">
        <div class="avatar avatar--rojo">CR</div>
        <div class="contenido">
          <h3 class="nombre">Carlos Ruiz</h3>
          <p class="empresa">EcoEnergia</p>
          <p class="texto">"Muy satisfecho con el servicio y la asesoría. Los equipos solares funcionan perfecto."</p>
        </div>
      </article>
    </div>
  </section>
</template>

<script setup>
// componente puro de presentación
</script>

<style scoped>
.comentarios { max-width:1100px; margin:2.5rem auto; padding:1.25rem; }
.comentarios__titulo { text-align:center; color:var(--primary,#2563eb); margin-bottom:1.5rem; font-size:1.9rem; }
.comentarios__grid { display:grid; grid-template-columns: repeat(3,1fr); gap:1.25rem; }
.comentario-card { background:#fff; border-radius:12px; padding:1.25rem; box-shadow:0 6px 20px rgba(37,99,235,0.06); display:flex; gap:1rem; align-items:flex-start; }
.avatar { width:56px; height:56px; border-radius:50%; display:flex; align-items:center; justify-content:center; font-weight:700; color:#fff; background:#2563eb; flex:0 0 56px; font-size:1.05rem; }
.avatar--verde { background:#059669 }
.avatar--rojo { background:#dc2626 }
.contenido .nombre { margin:0; color:#061a48; font-weight:700; }
.contenido .empresa { margin:0; color:#6b7280; font-size:0.9rem; }
.contenido .texto { margin-top:0.6rem; color:#334155; line-height:1.4; }

@media (max-width:900px) {
  .comentarios__grid { grid-template-columns: 1fr; }
  .comentario-card { align-items:center; }
}
</style>
