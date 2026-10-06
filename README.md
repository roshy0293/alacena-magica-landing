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

## Pendientes antes del lanzamiento

- [ ] Conectar el formulario de la lista de espera a un servicio que guarde los correos.
- [ ] Sustituir los `#` de los botones de App Store / Google Play por las URL reales cuando la app esté publicada.
- [ ] Añadir el enlace real de redes sociales en `soporte.html`.
- [ ] Revisar el contenido de `#opiniones`: las cifras (500+ recetas, 80 % menos desperdicio, 3 h/semana), los testimonios (María, Carlos) y el contador "1.247 personas" son valores de ejemplo hasta que la app tenga usuarios reales. Deben sustituirse por datos reales o confirmarse con el cliente antes de promocionar el sitio.
- [ ] Confirmar que el correo de contacto es el definitivo.
- [ ] Revisar con el cliente los textos legales (`privacidad.html`, `terminos.html`), que describen funcionalidades de la app como el uso de la cámara.
- [ ] En `index.html`, cambiar `og:image` a una URL absoluta (por ejemplo `https://www.alacenamagica.com/assets/images/frittata-alacena-magica.webp`) para que la vista previa al compartir en redes funcione.
- [ ] Opcional: añadir `robots.txt` y `sitemap.xml`.

## Rendimiento

El proyecto pesa unos 27 MB, la mayor parte en imágenes. Las cinco imágenes de `assets/images/recetas/` pesan entre 1 y 3,5 MB cada una, y unos 16 archivos de `assets/` (cerca de 11 MB) no se usan en ninguna página. Para una carga más rápida conviene comprimir las imágenes grandes (por ejemplo con [Squoosh](https://squoosh.app)) y eliminar los archivos que no se referencian.

## Soporte

Para dudas sobre el funcionamiento o el despliegue de este sitio, escribe al correo de contacto indicado en `soporte.html`.

---

© Alacena Mágica. Todos los derechos reservados.
