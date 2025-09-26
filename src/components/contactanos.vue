<template>
  <section id="contacto" class="contacto-seccion" aria-labelledby="contacto-titulo">
    <div class="contacto-contenedor">
      <h2 id="contacto-titulo">Contáctanos</h2>

      <form class="contacto-form" @submit.prevent="enviar">
        <label>
          <span class="label-text">Nombre</span>
          <input v-model="form.nombre" type="text" required />
        </label>

        <label>
          <span class="label-text">Email</span>
          <input v-model="form.email" type="email" required />
        </label>

        <label>
          <span class="label-text">Mensaje</span>
          <textarea v-model="form.mensaje" rows="5" required></textarea>
        </label>

        <div class="acciones">
          <button type="submit" class="btn-enviar">Enviar</button>
        </div>
      </form>

      <div class="social-row" aria-hidden="false">
        <a href="#" class="social" aria-label="Facebook" target="_blank" rel="noopener">
          <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor" aria-hidden="true"><path d="M22 12a10 10 0 10-11.5 9.9v-7H8.5v-2.9h2V9.2c0-2 1.2-3.1 3-3.1.9 0 1.8.16 1.8.16v2h-1c-1 0-1.3.62-1.3 1.25v1.56h2.2l-.35 2.9H14v7A10 10 0 0022 12z"/></svg>
          <span class="social-label">Facebook</span>
        </a>
        <a href="#" class="social" aria-label="Instagram" target="_blank" rel="noopener">
          <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor" aria-hidden="true"><path d="M7 2h10a5 5 0 015 5v10a5 5 0 01-5 5H7a5 5 0 01-5-5V7a5 5 0 015-5zm5 5.5a4.5 4.5 0 100 9 4.5 4.5 0 000-9zm6.5-.9a1.1 1.1 0 11-2.2 0 1.1 1.1 0 012.2 0zM12 9.5a2.5 2.5 0 110 5 2.5 2.5 0 010-5z"/></svg>
          <span class="social-label">Instagram</span>
        </a>
        <a href="#" class="social social-tiktok" aria-label="TikTok" target="_blank" rel="noopener">
          <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor" aria-hidden="true"><path d="M12 3v9.2a3.8 3.8 0 11-3.8-3.8V8.2a6 6 0 006 6V3h-2.2z"/></svg>
          <span class="social-label">TikTok</span>
        </a>
        <a href="https://wa.link/hj2t5j" class="social whatsapp-social" aria-label="WhatsApp" target="_blank" rel="noopener">
          <svg viewBox="0 0 24 24" width="18" height="18" fill="currentColor" aria-hidden="true"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347"/></svg>
          <span class="social-label">WhatsApp</span>
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
import { reactive } from 'vue'
const form = reactive({ nombre: '', email: '', mensaje: '' })

function enviar() {
  alert('Mensaje enviado. Gracias.')
  form.nombre = ''
  form.email = ''
  form.mensaje = ''
}
</script>

<style scoped>
.contacto-seccion {
  padding: 2.4rem 1rem;
  display: flex;
  justify-content: center;
  background: rgb(159, 156, 156);
}
.contacto-contenedor {
  width: 100%;
  max-width: 760px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.25rem;
  margin: 0 auto;
}
#contacto-titulo {
  font-size: 2.0rem;
  margin: 0;
  font-weight: 700;
  text-align: center;
  color: white !important;
}

.contacto-form {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  background: #082572;
  padding: 1.25rem;
  border-radius: 8px;
  box-shadow: 0 8px 24px rgba(243, 240, 240, 0.08);
}
.label-text {
  display: block;
  font-size: 1.05rem;
  margin-bottom: 0.35rem;
  color: #fcfcff;
  font-weight: 600;
}
.contacto-form input,
.contacto-form textarea {
  width: 100%;
  font-size: 1rem;
  padding: 0.7rem;
  border: 1px solid rgba(6,26,72,0.12);
  border-radius: 6px;
  outline: none;
  box-sizing: border-box;
}
.contacto-form textarea { resize: vertical; min-height: 120px; }

.acciones { display:flex; justify-content:center; }
.btn-enviar {
  background: #feffff;
  color: #082572;
  padding: 0.65rem 1rem;
  border-radius: 8px;
  border: none;
  font-size: 1rem;
  cursor: pointer;
}

.social-row {
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-top: 0.75rem;
  flex-wrap: wrap;
}
.social {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 8px 12px;
  background: #ffffff;
  color: #082572;
  border-radius: 8px;
  text-decoration: none;
  box-shadow: 0 4px 12px rgba(2,6,23,0.06);
  height: 44px;
}
.social svg { width:18px; height:18px; flex: 0 0 18px; }
.social-label { color: #082572; font-weight: 600; font-size: 0.95rem; line-height: 1; }

.whatsapp-social { background: #ffffff; color: #082572; }
.whatsapp-social .social-label { color: #082572; }

.social-tiktok { display: none; }

@media (max-width: 900px) {
  .social-tiktok { display: inline-flex; }
}

@media (max-width: 520px) {
  .contacto-contenedor { padding: 0 12px; }
  #contacto-titulo { font-size: 1.4rem; }
  .contacto-form { padding: 12px; }
  .label-text { font-size: 0.95rem; }
  .btn-enviar { width: 100%; }
  .social-row { gap: 8px; margin-top: 0.5rem; }
  .social { padding: 8px; height: 40px; }
  .social-label { font-size: 0.85rem; display: inline-block; }
}
</style>
