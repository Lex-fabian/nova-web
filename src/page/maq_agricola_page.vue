<template>
  <div>
    <header class="encabezado" style="height:56px;">
      <nav class="contenedor-navegacion">
        <div class="contenedor-logo" style="height:32px;align-items:center;display:flex;margin-top:6px;">
          <img src="../assets/icono_savreh.png" alt="Icono Savreh" class="logo" style="height:32px;max-width:90px;margin-right:1.2rem;" />
        </div>

        <ul class="enlaces-navegacion solo-escritorio" style="height:32px;align-items:center;">
          <li><a href="/" class="enlace-menu" @click="navegarAInicio">Inicio</a></li>
          <li class="dropdown-item">
            <a href="#" class="enlace-menu">Tienda <span class="dropdown-arrow">▼</span></a>
            <ul class="dropdown-submenu">
              <li><a href="/#maquinaria" class="submenu-link" @click="navegarAMaquinaria">Maquinaria Industrial</a></li>
              <li><a href="/#panaderia" class="submenu-link" @click="navegarAPanaderia">Panadería</a></li>
            </ul>
          </li>
          <li><a href="/#sobre-nosotros" class="enlace-menu" @click="navegarASobre">Sobre Nosotros</a></li>
          <li><a href="/#contacto" class="enlace-menu" @click="navegarAContacto">Contáctanos</a></li>
          <li style="position:relative;">
            <button class="boton-buscar" @click="toggleBuscador" :aria-expanded="buscadorAbierto" aria-label="Buscar productos" style="background:transparent;border:none;color:#fff;cursor:pointer;padding:0.4rem 0.8rem;border-radius:8px;transition:background 0.2s;">
              <svg width="20" height="20" fill="none" stroke="currentColor" viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"></circle><path d="m21 21-4.35-4.35"></path></svg>
            </button>
            <transition name="fade">
              <input v-if="buscadorAbierto" ref="inputBuscar" type="text" placeholder="Buscar productos..." class="input-buscar" style="position:absolute;top:100%;right:0;background:#fff;border:2px solid #061a48;border-radius:10px;padding:0.5rem 1rem;font-size:0.9rem;width:220px;margin-top:0.5rem;z-index:1001;" @blur="cerrarBuscador" />
            </transition>
          </li>
        </ul>
 
        <button class="boton-menu-movil solo-movil" @click="menuMovilAbierto = !menuMovilAbierto" aria-label="Toggle navigation menu" style="background:transparent;border:none;color:#fff;font-size:1.5rem;cursor:pointer;padding:0.5rem;">☰</button>
      </nav>
  
      <div class="menu-movil solo-movil" v-show="menuMovilAbierto" style="background:rgba(6,26,72,0.98);padding:1rem 2rem;border-top:1px solid rgba(255,255,255,0.1);">
        <ul style="list-style:none;padding:0;margin:0;">
          <li style="margin-bottom:0.5rem;"><a href="/" @click="navegarAInicio; menuMovilAbierto = false" style="color:#fff;text-decoration:none;font-size:1.1rem;">Inicio</a></li>
          <li style="margin-bottom:0.5rem;"><a href="/#maquinaria" @click="navegarAMaquinaria; menuMovilAbierto = false" style="color:#fff;text-decoration:none;font-size:1.1rem;">Maquinaria Industrial</a></li>
          <li style="margin-bottom:0.5rem;"><a href="/#panaderia" @click="navegarAPanaderia; menuMovilAbierto = false" style="color:#fff;text-decoration:none;font-size:1.1rem;">Panadería</a></li>
          <li style="margin-bottom:0.5rem;"><a href="/#sobre-nosotros" @click="navegarASobre; menuMovilAbierto = false" style="color:#fff;text-decoration:none;font-size:1.1rem;">Sobre Nosotros</a></li>
          <li><a href="/#contacto" @click="navegarAContacto; menuMovilAbierto = false" style="color:#fff;text-decoration:none;font-size:1.1rem;">Contáctanos</a></li>
        </ul>
      </div>
    </header>

    <div class="pagina-maquinaria" style="margin-top:56px;">
      <h1 style="text-align:center;margin-top:2rem;color:#031641">Maquinaria Agrícola</h1>
      <div class="grid-tienda">
        <template v-if="seleccionado !== null">
          <div style="margin-bottom:2.5rem;">
            <div class="producto-tienda seleccionado">
              <div class="producto-ampliado">
                <div class="ampliado-imagen">
                  <img :src="productos[seleccionado].img" :alt="productos[seleccionado].nombre" />
                </div>
                <div class="ampliado-datos">
                  <h2 class="titulo-producto">{{ productos[seleccionado].nombre }}</h2>
                  <p class="descripcion">{{ productos[seleccionado].desc }}</p>
                  <div class="botones-pagina">
                    <button type="button" class="boton-ficha" @click="abrirFicha(productos[seleccionado].nombre)">Ficha técnica</button>
                    <button type="button" class="boton-contactar" @click="contactarWhatsApp">Contactar</button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="grid-tienda-secundaria">
            <div v-for="(prod, idx) in productos" :key="prod.nombre" v-if="idx !== seleccionado" class="producto-tienda" @click="seleccionarProducto(idx)">
              <img :src="prod.img" :alt="prod.nombre" />
              <h2 class="titulo-producto">{{ prod.nombre }}</h2>
              <p class="descripcion">{{ prod.desc }}</p>
              <div class="botones-pagina">
                <button type="button" class="boton-ficha" @click.stop="abrirFicha(prod.nombre)">Ficha técnica</button>
                <button type="button" class="boton-contactar" @click.stop="contactarWhatsApp">Contactar</button>
              </div>
            </div>
          </div>
        </template>
        <template v-else>
          <div class="grid-tienda-secundaria">
            <div v-for="(prod, idx) in productos" :key="prod.nombre" class="producto-tienda" @click="seleccionarProducto(idx)">
              <img :src="prod.img" :alt="prod.nombre" />
              <h2 class="titulo-producto">{{ prod.nombre }}</h2>
              <p class="descripcion">{{ prod.desc }}</p>
              <div class="botones-pagina">
                <button type="button" class="boton-ficha" @click.stop="abrirFicha(prod.nombre)">Ficha técnica</button>
                <button type="button" class="boton-contactar" @click.stop="contactarWhatsApp">Contactar</button>
              </div>
            </div>
          </div>
        </template>
      </div>
      
      <!-- Modal para mostrar ficha técnica -->
      <div v-if="mostrarFicha" class="overlay-ficha">
        <div class="contenedor-ficha">
          <button class="cerrar-ficha" @click="mostrarFicha = false">&times;</button>
          <iframe class="iframe-ficha" :src="fichaUrl" frameborder="0"></iframe>
        </div>
      </div>

      <!-- Botón WhatsApp flotante -->
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
    </div>
  </div>
</template><script>
import { ref, onMounted, onUnmounted } from 'vue'
import '../style/maq_agricola_style.css'
import '../style.css'  // Importar estilos del header
import TS754Img from '../assets/TS-754.png';
import TS254SImg from '../assets/TS-254S.png';
import TS254PImg from '../assets/TS-254P.png';
import TS454Img from '../assets/TS-454.png';
import TS1104Img from '../assets/TS-1104.png';
import TS1604Img from '../assets/TS-1604.png';

export default {
  name: 'MaqAgricolaPage',
  emits: ['close'],
  setup(props, { emit }) {
    // Variables reactivas para header
    const menuMovilAbierto = ref(false)
    const buscadorAbierto = ref(false)
    const inputBuscar = ref(null)
    
    // Variables reactivas para productos
    const seleccionado = ref(null)
    const mostrarFicha = ref(false)
    const fichaUrl = ref('')

    const productos = [
      {
        nombre: 'TA-754',
        img: TS754Img,
        desc: 'Tractor robusto y confiable para grandes extensiones agrícolas. Alto rendimiento y durabilidad.'
      },
      {
        nombre: 'TS-254S',
        img: TS254SImg,
        desc: 'Tractor compacto, eficiente y versátil para labores agrícolas. Motor potente y bajo consumo.'
      },
      {
        nombre: 'TS-254P',
        img: TS254PImg,
        desc: 'Tractor versátil y eficiente, ideal para pequeñas y medianas parcelas. Bajo mantenimiento y gran maniobrabilidad.'
      },
      {
        nombre: 'TS454',
        img: TS454Img,
        desc: 'Tractor potente y moderno, diseñado para trabajos exigentes en el campo. Gran capacidad y tecnología avanzada.'
      },
      {
        nombre: 'TS-1104',
        img: TS1104Img,
        desc: 'Tractor de alta potencia y tecnología avanzada, ideal para grandes extensiones y trabajos exigentes.'
      },
      {
        nombre: 'TS-1604',
        img: TS1604Img,
        desc: 'Tractor de última generación, máxima potencia y eficiencia para los retos más grandes del campo.'
      }
    ]

    const toggleBuscador = () => {
      buscadorAbierto.value = !buscadorAbierto.value
      if (buscadorAbierto.value) {
        setTimeout(() => {
          inputBuscar.value?.focus()
        }, 100)
      }
    }

    const cerrarBuscador = (event) => {
      if (!event.relatedTarget || !event.relatedTarget.closest('.boton-buscar')) {
        buscadorAbierto.value = false
      }
    }

    const seleccionarProducto = (i) => {
      seleccionado.value = i;
      setTimeout(() => {
        const ampliado = document.querySelector('.producto-tienda.seleccionado');
        if (ampliado) {
          ampliado.scrollIntoView({ behavior: 'smooth', block: 'center' });
        }
      }, 100);
    }

    const abrirFicha = (producto) => {
      if (producto === 'TA-754') {
        fichaUrl.value = '/pdf/ficha_tecnica_maquina_agricola/TRACTOR 754.pdf';
      } else if (producto === 'TS-254S') {
        fichaUrl.value = '/pdf/ficha_tecnica_maquina_agricola/TRACTOR 254S.pdf';
      } else if (producto === 'TS-254P') {
        fichaUrl.value = '/pdf/ficha_tecnica_maquina_agricola/TRACTOR 254P.pdf';
      } else if (producto === 'TS454') {
        fichaUrl.value = '/pdf/ficha_tecnica_maquina_agricola/TRACTOR 454.pdf';
      } else if (producto === 'TS-1104') {
        fichaUrl.value = '/pdf/ficha_tecnica_maquina_agricola/TRACTOR 1104.pdf';
      } else {
        fichaUrl.value = '';
      }
      mostrarFicha.value = true;
    }

    const contactarWhatsApp = () => {
      window.open('https://wa.link/hj2t5j', '_blank');
    }

    const navegarAInicio = (event) => {
      event.preventDefault();
      emit('close');
      setTimeout(() => {
        window.location.href = '/';
      }, 100);
    }

    const navegarASobre = (event) => {
      event.preventDefault();
      emit('close');
      setTimeout(() => {
        window.location.href = '/#sobre-nosotros';
      }, 100);
    }

    const navegarAContacto = (event) => {
      event.preventDefault();
      emit('close');
      setTimeout(() => {
        window.location.href = '/#contacto';
      }, 100);
    }

    const navegarAMaquinaria = (event) => {
      event.preventDefault();
      emit('close');
      setTimeout(() => {
        window.location.href = '/#maquinaria';
      }, 100);
    }

    const navegarAPanaderia = (event) => {
      event.preventDefault();
      emit('close');
      setTimeout(() => {
        window.location.href = '/#panaderia';
      }, 100);
    }

    onMounted(() => {
      document.addEventListener('click', (e) => {
        if (!e.target.closest('.boton-menu-movil') && !e.target.closest('.menu-movil')) {
          menuMovilAbierto.value = false
        }
        if (!e.target.closest('.boton-buscar') && !e.target.closest('.input-buscar')) {
          buscadorAbierto.value = false
        }
      })
    })

    return {
      menuMovilAbierto,
      buscadorAbierto,
      inputBuscar,
      toggleBuscador,
      cerrarBuscador,
      productos,
      seleccionado,
      mostrarFicha,
      fichaUrl,
      seleccionarProducto,
      abrirFicha,
      contactarWhatsApp,
      navegarAInicio,
      navegarASobre,
      navegarAContacto,
      navegarAMaquinaria,
      navegarAPanaderia
    }
  }
}
</script>
