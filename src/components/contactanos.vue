<template>
  <section class="seccion-contacto" id="contactanos">
    <div class="contenedor-contacto">
      <div class="info-contacto animate-on-scroll">
        <h2>Contáctanos</h2>
        <p>Estamos aquí para ayudarte. Rellena el formulario o utiliza nuestros datos de contacto directos.</p>
        <ul class="lista-detalles-contacto">
          <li>
            <span class="icono-contacto">&#x1F4CD;</span>
            <span>Panamericana Sur Km 1 1/2, Riobamba, Ecuador</span>
          </li>
          <li>
            <span class="icono-contacto">&#x1F4DE;</span>
            <a href="tel:+593987654321">+593 98 765 4321</a>
          </li>
          <li>
            <span class="icono-contacto">&#x2709;</span>
            <a href="mailto:info@savreh.com">info@savreh.com</a>
          </li>
          <li>
            <span class="icono-contacto"><i class="fab fa-facebook-f"></i></span>
            <a href="https://www.facebook.com/profile.php?id=61550893650426&sk=about" target="_blank">Facebook</a>
          </li>
          <li>
            <span class="icono-contacto"><i class="fab fa-instagram"></i></span>
            <a href="https://www.instagram.com/savreh.ec/" target="_blank">Instagram</a>
          </li>
          <li class="tiktok-mobile">
            <span class="icono-contacto"><i class="fab fa-tiktok"></i></span>
            <a href="https://www.tiktok.com/@savreh.ec" target="_blank">TikTok</a>
          </li>
        </ul>
        <div class="mapa-contacto">
          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3989.433119125346!2d-78.60938689999999!3d-0.7636209!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x91d4592bb8475eab%3A0x6dcd271287e48d3c!2sSavreh%20S.A.%20Bodega!5e0!3m2!1sen!2sec!4v1721342654315!5m2!1sen!2sec"
            loading="lazy"
            referrerpolicy="no-referrer-when-downgrade">
          </iframe>
        </div>
      </div>
      <div class="formulario-contacto animate-on-scroll" style="transition-delay: 200ms">
        <form @submit.prevent>
          <h3>Envíanos un mensaje</h3>
          <div class="grupo-formulario">
            <label for="nombre">Nombre</label>
            <input type="text" id="nombre" name="nombre" required>
          </div>
          <div class="grupo-formulario">
            <label for="email">Email</label>
            <input type="email" id="email" name="email" required>
          </div>
          <div class="grupo-formulario">
            <label for="asunto">Asunto</label>
            <input type="text" id="asunto" name="asunto" required>
          </div>
          <div class="grupo-formulario">
            <label for="mensaje">Mensaje</label>
            <textarea id="mensaje" name="mensaje" rows="5" required></textarea>
          </div>
          <button type="submit" class="boton-enviar">Enviar Mensaje</button>
        </form>
      </div>
    </div>
  </section>
</template>

<style scoped>
.lista-detalles-contacto li a {
  color: inherit;
  text-decoration: none;
  transition: color 0.3s ease;
}
.lista-detalles-contacto li a:hover {
  color: #42b883;
}
.tiktok-mobile {
  display: none;
}
@media (max-width: 768px) {
  .tiktok-mobile {
    display: list-item !important;
  }
}
</style>