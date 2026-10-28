# La Beta Escalada — Landing Page

Landing page de **[La Beta Escalada](https://www.instagram.com/labeta.escalada/)**, muro de escalada deportiva en Montevideo, Uruguay (Chaná 2240).

Sitio de una sola página con toda la información esencial para el visitante: hero con llamado a la acción, ubicación y horarios, reglas de convivencia del muro, y contacto por Instagram.

## Estructura del proyecto

```
.
├── index.html      # Página completa (markup + estilos + lógica)
├── support.js      # Runtime del componente x-dc (dc-runtime, generado — no editar a mano)
├── assets/         # Logo y recursos de marca
└── uploads/        # Imágenes usadas en el sitio (fotos, íconos, infografías)
```

Todo el contenido vive en **[index.html](index.html)**: es un único componente `<x-dc>` con su HTML, sus estilos (`<style>` dentro del `<helmet>`) y su lógica en un bloque `<script type="text/x-dc">` al final del archivo, que renderiza los datos dinámicos (horarios, íconos animados, etc.) mediante `sc-for` y `{{ }}`. Este formato es interpretado en el navegador por `support.js`.

## Secciones

- **Hero** — imagen de portada, logo, título ("Escalada y Psicomotricidad") y accesos rápidos (Instagram, cómo llegar, rating de Google).
- **Actividades** (`#actividades`) — dos cards: Muro libre (naranja `#E8611C`, @labeta.escalada) y Escalada Psicomotriz® (turquesa `#2BB3B1`, @escaladapsicomotora).
- **Dónde y cuándo** (`#labeta-info`) — mapa embebido, dirección y horarios (`#horarios`), con el mismo código de colores que las cards.
- **Reglas y Convivencia** (`#reglas-convivencia`) — infografía con las normas de uso y convivencia del muro.
- **Footer** — datos de contacto y link a Instagram.

## Cómo verlo localmente

Al ser un sitio estático, alcanza con abrir `index.html` en el navegador o servirlo con cualquier servidor estático, por ejemplo:

```bash
npx serve .
```

## Despliegue

El sitio es 100% estático (HTML + JS + imágenes), por lo que puede alojarse en cualquier hosting estático (GitHub Pages, Netlify, Vercel, etc.) sin pasos de build.

## Edición de contenido

- **Horarios**: se editan en el array `horarios` dentro del `<script type="text/x-dc">` al final de `index.html`. Cada día tiene una lista `items` armada con `muro("20 – 23 h")` o `psico("Psicomotriz · Infancias", "17 y 18 h")`. Si cambian, actualizar también las cards de Actividades y el footer.
- **Imágenes**: se agregan a `uploads/` (o `assets/` para elementos de marca) y se referencian con rutas relativas.
- **SEO / metadata**: título, descripción, canonical, Open Graph y JSON-LD (`SportsActivityLocation`) están en el `<head>` estático de `index.html` — **no** moverlos al `<helmet>`, porque ahí solo se inyectan con JS y WhatsApp/Facebook no los leen. Si cambian horarios o cantidad de opiniones, actualizarlos también en el JSON-LD, en la meta description y en el texto de la sección "Dónde y cuándo" y el footer.
- **Sitemap**: al hacer cambios de contenido, actualizar `<lastmod>` en `sitemap.xml`.
