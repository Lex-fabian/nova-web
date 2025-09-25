<template>
  <section class="contactanos" id="contacto" aria-labelledby="contacto-title">
    <div class="container">
      <div class="inner">
        <div class="left">
          <h2 id="contacto-title">Contáctanos</h2>
          <p class="lead">¿Tienes alguna pregunta o necesitas más información sobre nuestros productos?</p>
          <div class="redes">
            <a class="red" href="https://www.facebook.com/p/Savreh-SA-61563909317105/" target="_blank" rel="noopener">Facebook</a>
            <a class="red" href="https://www.instagram.com/savreh.ec/" target="_blank" rel="noopener">Instagram</a>
            <a class="red" href="https://www.tiktok.com/@savreh.ec" target="_blank" rel="noopener">TikTok</a>
            <a class="red red--whatsapp" href="https://wa.link/hj2t5j" target="_blank" rel="noopener">WhatsApp</a>
          </div>
        </div>

        <form class="contact-form" @submit.prevent="submitForm" novalidate>
          <div class="fields">
            <input type="text" placeholder="Nombre" v-model="form.nombre" required />
            <input type="email" placeholder="Email" v-model="form.email" required />
            <textarea placeholder="Mensaje" v-model="form.mensaje" required></textarea>
          </div>
          <div class="actions">
            <button type="submit" class="btn">Enviar Mensaje</button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { reactive } from 'vue'
const form = reactive({ nombre: '', email: '', mensaje: '' })
function submitForm() {
  alert('Mensaje enviado. Nos contactaremos pronto.')
  form.nombre = ''
  form.email = ''
  form.mensaje = ''
}
</script>

<style scoped>
.contactanos {
  min-height: calc(100vh - 64px);
  display: flex;
  align-items: center;
  background: linear-gradient(180deg, #ffffff 0%, #f7fbff 100%);
  padding: 2rem 1rem;
}
.container { max-width:1100px; margin:0 auto; width:100%; }
.inner { display: grid; grid-template-columns: 1fr 460px; gap:2rem; align-items: center; }
.left h2 { color: var(--primary,#2563eb); margin:0 0 0.75rem 0; font-size:2rem }
.lead { color:#334155; font-size:1.05rem; margin-bottom:1rem }
.redes { display:flex; gap:0.6rem; flex-wrap:wrap }
.red { display:inline-flex; align-items:center; gap:0.5rem; padding:0.6rem 1rem; background:#fff; border-radius:8px; border:1px solid rgba(2,6,23,0.04); color:#0f172a; text-decoration:none; font-weight:600 }
.red--whatsapp { background:#25D366; color:#fff; border-color:rgba(0,0,0,0.06) }
.contact-form { background:#fff; padding:1.5rem; border-radius:12px; box-shadow:0 12px 40px rgba(2,6,23,0.06); display:flex; flex-direction:column; }
.fields { display:flex; flex-direction:column; gap:0.9rem; }
.contact-form input, .contact-form textarea { padding:0.95rem; border-radius:10px; border:1px solid rgba(2,6,23,0.08); font-size:1rem }
.contact-form textarea { min-height:180px; resize:vertical }
.actions { display:flex; justify-content:flex-end; margin-top:0.5rem }
.btn { background: linear-gradient(135deg,#2563eb 0%,#1e4fd6 100%); color:#fff; padding:0.9rem 1.2rem; border-radius:10px; border:none; font-weight:800; cursor:pointer }

@media (max-width:980px) {
  .inner { grid-template-columns: 1fr; }
  .contactanos { padding:1.5rem 1rem; }
  .left { order: 2; text-align:center }
  .contact-form { order: 1 }
  .actions { justify-content:center }
}
</style>
