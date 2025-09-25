<template>
  <section class="nosotros" id="sobre-nosotros" aria-labelledby="nosotros-title">
    <div class="wrap">
      <div class="content">
        <h2 id="nosotros-title">Sobre Nosotros</h2>
        <p class="intro">Somos especialistas en maquinaria industrial y agrícola. Nuestra meta es ofrecer soluciones confiables que impulsen el crecimiento de nuestros clientes.</p>

        <div class="cards">
          <article class="card">
            <h3>Misión</h3>
            <p>Brindar soluciones innovadoras y de calidad para la industria y el agro, contribuyendo al desarrollo sostenible y la satisfacción de nuestros clientes.</p>
          </article>

          <article class="card">
            <h3>Visión</h3>
            <p>Ser la empresa líder en el mercado nacional e internacional de maquinaria industrial y agrícola, reconocida por nuestra excelencia y compromiso.</p>
          </article>

          <article class="card">
            <h3>Valores</h3>
            <p>Impulsar el crecimiento de nuestros clientes mediante productos y servicios que generen valor, confianza y resultados sostenibles.</p>
          </article>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// componente de presentación
</script>

<style scoped>
.nosotros { min-height: calc(100vh - 64px); display:flex; align-items:center; background: linear-gradient(180deg,#f8fafc 0%, #ffffff 100%); padding:2rem 1rem }
.wrap { width:100%; max-width:1100px; margin:0 auto }
.content { text-align:center }
.nosotros h2 { color:var(--primary,#2563eb); font-size:2.25rem; margin-bottom:0.5rem }
.intro { color:#334155; font-size:1.05rem; margin-bottom:1.25rem }
.cards { display:grid; grid-template-columns: repeat(3,1fr); gap:1rem; align-items:stretch }
.card { background:#fff; padding:1.5rem; border-radius:14px; box-shadow:0 14px 40px rgba(2,6,23,0.06); text-align:left }
.card h3 { margin-top:0; color:#061a48; font-size:1.1rem }
.card p { color:#334155; line-height:1.6 }

@media (max-width:980px) {
  .cards { grid-template-columns: 1fr; }
  .content { padding:0 1rem }
}
</style>
