# Alacena Mágica · Landing page

Sitio web de presentación de **Alacena Mágica**, un asistente de cocina que genera recetas a partir de los ingredientes que ya tienes en la nevera.

La app todavía no está publicada. Este sitio funciona como carta de presentación y como lista de espera previa al lanzamiento.

## Contenido del sitio

| Página | Archivo | Descripción |
|---|---|---|
| Inicio | `index.html` | Landing principal: problema, demo interactiva, funciones, cómo funciona, opiniones, galería y llamada a la acción con formulario de lista de espera. |
| Soporte | `soporte.html` | Preguntas frecuentes y datos de contacto. |
| Cancelar suscripción | `cancelar-suscripcion.html` | Formulario para solicitar la baja de cuenta y la eliminación de datos. |
| Gracias | `gracias.html` | Confirmación tras enviar el formulario de cancelación. |
| Política de privacidad | `privacidad.html` | Tratamiento de datos personales. |
| Términos y condiciones | `terminos.html` | Condiciones de uso del servicio. |

## Tecnologías

Es un sitio **estático**: HTML, CSS y JavaScript puro, sin frameworks, sin dependencias y sin proceso de compilación.

- Los estilos (`<style>`) y los scripts (`<script>`) están **dentro de cada archivo HTML**; no hay archivos `.css` ni `.js` separados.
- Tipografías: [Fraunces](https://fonts.google.com/specimen/Fraunces) y [Outfit](https://fonts.google.com/specimen/Outfit), cargadas desde Google Fonts (requiere conexión a internet).
- No usa analítica, cookies de seguimiento ni servicios de terceros aparte de Google Fonts.

## Estructura del proyecto

```
.
├── index.html
├── soporte.html
├── cancelar-suscripcion.html
├── gracias.html
├── privacidad.html
├── terminos.html
└── assets/
    ├── images/      # Fotografías, capturas y botones de tiendas
    │   └── recetas/ # Imágenes de las recetas de la demo
    └── logos/       # Logotipos, isotipo, patrón e iconos (SVG/PNG)
```

## Ver el sitio en tu computadora

No hace falta instalar nada. Opciones:

1. **Doble clic en `index.html`** para abrirlo en el navegador.
2. O, para simular un servidor real (recomendado), desde la carpeta del proyecto:

   ```bash
   python3 -m http.server 8000
   ```

   y abre <http://localhost:8000>.

## Publicar el sitio

Como es un sitio estático, funciona en cualquier hosting. Sube **todo el contenido de la carpeta** (los HTML y la carpeta `assets/`) respetando la estructura. El archivo de entrada es `index.html`.

### Opción A · GitHub Pages (gratis)

1. En el repositorio, ve a **Settings → Pages**.
2. En *Build and deployment*, elige **Deploy from a branch**, rama `main` y carpeta `/ (root)`.
3. Guarda. En unos minutos tendrás una URL del tipo `https://usuario.github.io/repositorio/`.

### Opción B · Netlify o Vercel (gratis)

Arrastra la carpeta del proyecto a [app.netlify.com/drop](https://app.netlify.com/drop), o conecta el repositorio. No hay comando de build ni carpeta de salida especial: se publica la raíz.

### Opción C · Hosting tradicional

Sube los archivos por FTP/cPanel a la carpeta pública (`public_html`, `www` o similar).

### Dominio propio

El sitio está configurado para `https://www.alacenamagica.com` (meta `og:url` en `index.html`). Si usas GitHub Pages, añade el dominio en *Settings → Pages → Custom domain* y crea los registros DNS que indica GitHub. Si cambia el dominio, actualiza ese valor.

## Cómo editar el contenido

| Qué quieres cambiar | Dónde |
|---|---|
| Textos de cualquier página | Directamente en el HTML correspondiente. |
| Correo de contacto | Aparece en `soporte.html`, `privacidad.html`, `terminos.html`, `gracias.html` y `cancelar-suscripcion.html` (también en el atributo `data-fallback-email` del formulario de cancelación). Usa buscar y reemplazar en todo el proyecto. |
| Enlaces a App Store y Google Play | Botones con `aria-label="Descargar en App Store"` / `"Descargar en Google Play"`. En `index.html` (zona de llamada a la acción) y en `cancelar-suscripcion.html`, `gracias.html`, `privacidad.html`, `soporte.html` y `terminos.html` apuntan a `#`. Sustituye por las URL reales al publicar la app. El pie de `index.html` los dirige a `index.html#cta`. |
| Enlace de redes sociales | `soporte.html`, tarjeta "Redes sociales" (`Síguenos →`, ahora apunta a `#`). |
| Cifras y testimonios | `index.html`, sección `#opiniones`. Los números se definen con atributos `data-count` y `data-suffix`. |
| Contador de la lista de espera | `index.html`, texto "personas ya están en la lista" (junto al formulario final). |
| Logotipos e imágenes | Carpeta `assets/`. Mantén el mismo nombre de archivo para no tener que tocar el HTML. |
| Año del copyright | Automático (se calcula con JavaScript). |

## Formularios

### Lista de espera (`index.html`)

El formulario de correo del final de la página **valida el email y muestra el mensaje de confirmación, pero todavía no guarda ni envía el correo a ningún sitio**. Para recoger registros reales hay que conectarlo a un servicio (por ejemplo Formspree, Netlify Forms, Mailchimp, Brevo o un backend propio). El código del formulario está en `index.html`, bloque `/* ── Formulario CTA final ── */`.

### Cancelación de cuenta (`cancelar-suscripcion.html`)

El formulario tiene el atributo `data-endpoint=""` vacío. Comportamiento actual:

- **Sin endpoint:** al enviar, se abre el programa de correo del usuario con un mensaje prellenado dirigido al correo de contacto (`data-fallback-email`).
- **Con endpoint:** si se añade una URL en `data-endpoint`, el formulario envía los datos por POST y, si todo va bien, redirige a `gracias.html`. Si falla, vuelve al método del correo.

## Imágenes

Las imágenes están optimizadas en formato WebP. Si agregas o reemplazas alguna, conviene comprimirla antes (por ejemplo con [Squoosh](https://squoosh.app)) y no subir fotos de más de 1600 px de ancho: se ven igual y el sitio carga mucho más rápido.

## Soporte

Para dudas sobre el funcionamiento o el despliegue de este sitio, escribe al correo de contacto indicado en `soporte.html`.

---

© Alacena Mágica. Todos los derechos reservados.
