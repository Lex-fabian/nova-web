<template>
  <div>
    <section class="tarjeta tarjeta--maquinaria">
      <div class="tarjeta__inner">
        <figure class="tarjeta__media">
          <img src="../assets/TS-754.png" alt="TS-754" class="tarjeta__imagen" loading="lazy" />
        </figure>
        <div class="tarjeta__body">
          <h2 class="tarjeta__title">MAQUINARIA INDUSTRIAL</h2>
          <p class="productos-vendidos">Más de 5,000 ventas</p>
          <button type="button" class="boton-primario" @click="$emit('open-maquinaria')">Más información</button>
        </div>
      </div>
    </section>

    <section class="tarjeta tarjeta--panaderia">
      <div class="tarjeta__inner">
        <figure class="tarjeta__media">
          <img src="../assets/batidora1.png" alt="Batidora Panadería" class="tarjeta__imagen" loading="lazy" />
        </figure>
        <div class="tarjeta__body">
          <h2 class="tarjeta__title tarjeta__title--pan">PANADERÍA</h2>
          <p class="productos-vendidos productos-vendidos--pan">Más de 13,000 ventas</p>
          <button type="button" class="boton-primario boton-primario--pan">Más información</button>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
// Este componente emite 'open-maquinaria' cuando se requiere mostrar más info
</script>

<style scoped>
/* Tarjeta base */
.tarjeta {
  width: 100%;
  max-width: 1100px;
  margin: 2rem auto;
  border-radius: 18px;
  overflow: hidden;
  box-sizing: border-box;
}
.tarjeta__inner {
  display: flex;
  gap: 2rem;
  align-items: center;
  padding: 1.75rem;
  background: linear-gradient(135deg, #ffffff 0%, #fafbff 50%, #f8fafc 100%);
  box-shadow: 0 8px 40px rgba(37,99,235,0.08);
  border: 1px solid rgba(37,99,235,0.06);
}
.tarjeta__media { flex: 0 0 420px; display:flex; align-items:center; justify-content:center; }
.tarjeta__imagen { width:100%; max-width:420px; height:auto; object-fit:contain; border-radius:12px; }
.tarjeta__body { flex:1; display:flex; flex-direction:column; gap:1rem; align-items:flex-start; justify-content:center; }
.tarjeta__title { font-size:1.6rem; color:#061a48; font-weight:700; margin:0; }
.productos-vendidos { background: rgba(255,255,255,0.9); padding:0.4rem 0.8rem; border-radius:20px; color:#374151; border:1px solid rgba(15,23,42,0.04); }

/* Variantes */
.tarjeta--panaderia .tarjeta__inner { background: linear-gradient(180deg, #fffefc 0%, #fff7f0 100%); }
.tarjeta__title--pan { color:#6b4423; text-shadow:0 1px 3px rgba(139,116,95,0.08); }
.productos-vendidos--pan { color:#8b5a2b; }

/* Botones */
.boton-primario { background: linear-gradient(135deg,#2563eb 0%,#1e4fd6 100%); color:#fff; padding:0.9rem 1.6rem; border-radius:10px; border:none; font-weight:700; cursor:pointer; box-shadow:0 8px 24px rgba(37,99,235,0.12); transition:transform .18s ease, box-shadow .18s ease; }
.boton-primario:hover { transform:translateY(-3px); box-shadow:0 12px 36px rgba(37,99,235,0.18); }
.boton-primario--pan { background: linear-gradient(135deg,#8b5a2b 0%,#7a4d24 100%); }

@media (max-width: 900px) {
  .tarjeta__inner { flex-direction: column; padding:1rem; }
  .tarjeta__media { flex: none; width:100%; }
  .tarjeta__imagen { max-width:90vw; }
  .tarjeta__body { align-items:center; text-align:center; }
  .tarjeta__title { font-size:1.5rem; }
}
</style>
