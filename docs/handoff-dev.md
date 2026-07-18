# Handoff de desarrollo — Landing datagovlatam.com

**Proyecto:** Landing del ecosistema DGL (Data Governance Latam)
**Archivo de referencia:** `datagovlatam-home-mockup.html` (mockup navegable, single-file, HTML/CSS/JS vanilla)
**Basado en:** Manual de Marca DGL v1.0 (Marzo 2026) + Manual de Marca Verticales v1.1 (Abril 2026)
**Fecha:** Julio 2026

El mockup es la fuente de verdad visual. Este documento resume los tokens, las especificaciones y lo que hay que cambiar para llevarlo a producción.

---

## 1. Design tokens

### Colores (CSS custom properties, según manual §03)

```css
:root{
  --cyan:       #00A3E0;  /* Acento principal: CTAs, links, highlights. Máx. 25% de la superficie */
  --cyan-dark:  #0077BB;  /* Extremo oscuro del gradiente de botones */
  --navy:       #00203F;  /* Nav scrolled, fondos de soporte */
  --navy-deep:  #001529;  /* Fondo principal de toda la página */
  --navy-mid:   #001a33;  /* Reservado, fondos intermedios */
  --white:      #FFFFFF;  /* Texto principal sobre fondo oscuro */
  --gold:       #C9A84C;  /* SOLO badges premium: "Informe insignia", "Próximamente" */
  --gray:       #53565A;  /* Gris metálico de soporte */
  --silver:     #B0B8C4;  /* Complemento del cyan en gradientes */

  /* Derivados usados en la landing */
  --glass-bg:     rgba(255,255,255,0.04);  /* Fondo de tarjetas glass */
  --glass-border: rgba(255,255,255,0.06);  /* Borde de tarjetas glass */
  --text-dim:     rgba(255,255,255,0.62);  /* Texto secundario */
  --text-faint:   rgba(255,255,255,0.40);  /* Captions y labels */
}
```

Reglas del manual: Navy dominante (~56%), Cyan solo como acento (~25%), Gold solo en destacados breves (~10%). Nunca Cyan como fondo principal, nunca Gold en textos largos.

### Tipografía (manual §04)

| Rol | Familia | Peso | Tamaño | Detalles |
|---|---|---|---|---|
| H1 hero | Montserrat | 800 | clamp(38px, 5.4vw, 64px) | line-height 1.08, tracking −0.02em |
| H2 sección | Montserrat | 800 | clamp(28px, 3.4vw, 40px) | line-height 1.15, tracking −0.015em |
| H3 card | Montserrat | 700 | 17–19px | — |
| Eyebrow | Montserrat | 600 | 11px | UPPERCASE, tracking 0.3em, color cyan, guión de 34px antes |
| Body | Open Sans | 300 | 17px | line-height 1.65 |
| Caption/label | Open Sans | 400 | 12–13.5px | color text-faint |
| CTAs y nav | Montserrat | 600–700 | 13–14px | — |

### Espaciado y layout

- Contenedor: max-width **1180px**, padding lateral **32px**
- Secciones: padding vertical **110px** desktop / **80px** ≤980px
- Separación título de sección → contenido: **64px** (`.sec-head`)
- Gap entre cards: **20px**
- Padding interno de cards: **36px 32px** (verticales: 42px 36px)
- Radios: cards **16px**, tarjetas grandes **20px**, mini-stats **14px**, botones/chips/pills **50px** (pill shape, según manual)

### Breakpoints

- **≤980px:** nav colapsa a hamburguesa, grids de 4/3 columnas pasan a 2/1, stats 2×2
- **≤600px:** todo a 1 columna, botón WhatsApp solo ícono

---

## 2. Componentes

### Botones (manual §05)

- **Primario:** gradient 120° cyan → cyan-dark, texto blanco Montserrat 700 14px, padding 15px 32px, radius 50px, sombra `0 8px 28px rgba(0,163,224,.28)`. Hover: translateY(−2px) + sombra más intensa. La flecha `→` se desplaza 4px a la derecha en hover.
- **Ghost:** transparente, borde `rgba(255,255,255,.22)`, hover borde y texto cyan.
- **Link-arrow:** texto cyan Montserrat 600 13.5px + flecha con el mismo micro-desplazamiento.

### Tarjetas glass (manual §05, exacto)

```css
background: rgba(255,255,255,0.04);
border: 1px solid rgba(255,255,255,0.06);
backdrop-filter: blur(8px);
/* línea superior cyan gradient que aparece en hover */
/* hover: translateY(-6px), borde rgba(0,163,224,.35), glow */
```

Extra del mockup: glow radial que sigue el cursor (`--mx`/`--my` vía `pointermove`).

### Iconografía

Sprite SVG inline (`<symbol>`) al inicio del `<body>`. Estilo: pictogramas planos, monocromo cyan, geometría sólida con esquinas redondeadas, grilla 24×24, `fill: currentColor`. Íconos: building, user, team, network, shield, briefcase, cap, chart, radar, doc, mail, check. Contenedor: 46×46px, radius 12px, fondo `rgba(0,163,224,.1)`, borde `rgba(0,163,224,.2)`.

### Badges

- **Gold premium** (`.badge-gold`, `.soon`): borde y texto gold, fondo `rgba(201,168,76,.08)`, UPPERCASE, radius 50px. Solo para "Informe insignia" y "Próximamente".
- **Pills de vertical** (`.eco-pill`): cyan, mismo patrón.

---

## 3. Mapa de secciones y ruteo

La landing es **derivadora de tráfico**: no tiene formularios ni backend. Todos los links externos llevan `target="_blank" rel="noopener"` y sufijo visual `↗`.

| Sección | Destino de sus CTAs |
|---|---|
| Nav | Consulting → datagovernancelatam.com · Talent → dgltalent.com · Academy → dgl.academy · resto anclas internas |
| Hero | "Coordinar una call" → datagovernancelatam.com/#contacto · chips por audiencia a cada vertical |
| Audiencias | Empresas → consulting · Profesionales → academy · RRHH → dgltalent.com · Comunidad → ancla #comunidad |
| Ecosistema | Cada tarjeta a su dominio |
| Research | Todo → dgltalent.com/recursos.html (informe insignia a #informes y #estudio-completo) · reportes "Próximamente" → ancla #newsletter |
| Comunidad | "Unirme a la comunidad" → dgltalent.com/postularme.html |
| Newsletter | Sin CTA (pre-lanzamiento, solo badge Próximamente) |
| CTA final | Consulta → datagovernancelatam.com/#contacto · WhatsApp → wa.me/5491133219958 con mensaje precargado |
| Footer | Links reales del sitio actual (data-privacy.html, prensa.html, etc.) |

---

## 4. Animaciones (specs)

Todas respetan `prefers-reduced-motion: reduce` (se desactivan, incluidos los canvas).

| Animación | Spec |
|---|---|
| Scroll reveal | IntersectionObserver, threshold 0.18 · opacity 0→1 + translateY 28px→0 · 0.7s cubic-bezier(.2,.8,.2,1) · stagger .08s entre elementos hermanos (clases d1–d4) |
| Red de nodos (hero y comunidad) | Canvas 2D · 55/40 nodos · líneas entre nodos a <160/130px con alpha proporcional a distancia · velocidad .22px/frame · respeta devicePixelRatio |
| Contadores | requestAnimationFrame, 1400ms, easing cubic-out, formato es-AR |
| Shimmer H1 | background-position del gradiente, 7s ease-in-out infinite |
| Marquee sectores | translateX −50%, 34s linear infinite, pausa en hover, mask de fade lateral |
| Flywheel | Anillo dasharray girando (60s) + 3 dots con animateMotion (14s, offsets −4.66s/−9.33s) |
| Nav | Fondo `rgba(0,32,63,.7)` + blur 30px al superar 40px de scroll (spec del manual §06) |
| Scrollspy | IntersectionObserver rootMargin −30%/−55%, subrayado cyan en link activo |
| Barra de progreso | 2px, top fixed, width = % de scroll |
| Orbes de fondo | blur 90px, float 14s, opacidad 2–10% |

---

## 5. Checklist de producción

### Assets (lo primero)

- [ ] **Fuentes self-hosteadas:** bajar Montserrat (300–900) y Open Sans (300–700) de Google Fonts, servir como WOFF2 con `font-display: swap` y `preload` de los pesos críticos (Montserrat 800, Open Sans 300). Eliminar el `<link>` a fonts.googleapis.com (independencia de terceros + coherente con el badge de privacidad).
- [ ] **Logo como archivo:** hoy va embebido en base64 (54KB PNG). Reemplazar por **SVG vectorial** del lockup DGL-OSC (pedir el original al equipo de marca) o, si no existe, WebP @2x (~15KB). Mínimo 120px de ancho según manual.
- [ ] **Favicon:** hoy base64. Generar set completo: favicon.ico, apple-touch-icon 180px, icon 192/512px para manifest. Usar el isotipo sin fondo (DGL-ISO).
- [ ] **Fotos del equipo:** hoy hotlinkeadas desde datagovernancelatam.com. Descargar, recortar cuadradas, exportar WebP 176px (@2x de los 88px renderizados), servir desde el propio dominio con `loading="lazy"` (ya está en el markup).
- [ ] **Imagen OG:** crear `og-image` 1200×630 (fondo navy-deep, logo, tagline) y agregar `og:image` — hoy no existe y LinkedIn es el canal principal.

### Performance

- [ ] Minificar HTML/CSS/JS (el archivo está sin minificar a propósito, para legibilidad).
- [ ] Los canvas de red corren con requestAnimationFrame continuo: pausarlos cuando no están en viewport (IntersectionObserver) y con `document.visibilitychange`.
- [ ] Verificar Lighthouse ≥90 en Performance y 100 en Accessibility/SEO/Best Practices.

### Privacidad y analytics

- [ ] El footer declara **"sin cookies de tracking de terceros"**. DGL no usa Google Analytics, así que el badge es verdadero por defecto — mantenerlo así. **No instalar GA ni ningún tracker de terceros en esta página.**
- [ ] Si se necesitan métricas de visitas, usar solo analytics sin cookies: Plausible, Fathom o Matomo self-hosted. No requieren banner de consentimiento y no contradicen el badge.
- [ ] Sin formularios propios: no hay datos personales que tratar en esta página. Mantenerlo así simplifica el compliance.

### SEO

- [ ] JSON-LD ya incluido (Organization con los 3 dominios como `sameAs` + FAQPage). Validar con Rich Results Test al publicar.
- [ ] Agregar `canonical`, `sitemap.xml` y `robots.txt`.
- [ ] `hreflang` si se suma la versión EN (planificada, no incluida).
- [ ] Verificar dominio en Search Console y dar de alta la property.

### QA

- [ ] Probar en Chrome, Safari, Firefox, Edge + iOS/Android reales (el blur y `backdrop-filter` varían en móviles de gama baja — hay fallback de color sólido implícito, verificar).
- [ ] Probar navegación completa por teclado (focus-visible ya implementado).
- [ ] Probar con `prefers-reduced-motion` activado.
- [ ] Verificar todos los links externos contra los sitios reales (tabla de ruteo, sección 3).
- [ ] Revisar contraste AA en textos `--text-faint` sobre navy (los tamaños pequeños están al límite; si falla, subir a rgba .5).

### Contenido pendiente (no bloquea el lanzamiento)

- [ ] Newsletter DGL Intelligence: cuando exista, restaurar CTA en la banda (el diseño del formulario está en el historial del mockup: input + botón primario, radius 50px).
- [ ] Reportes "Próximamente" (Estado de la Privacidad, Radar de IA, Índice de Madurez): al publicarse, quitar badge y apuntar el link a dgltalent.com/recursos.html.
- [ ] Logos de clientes con permiso de uso para reemplazar el marquee de sectores.
- [ ] Testimonios con nombre y empresa para la sección comunidad.

---

## 6. Estructura del archivo

```
<head>
  meta + OG + JSON-LD + favicon + fuentes
  <style> tokens → tipografía → componentes → secciones → polish → responsive
<body>
  #progress (barra scroll)
  sprite SVG de íconos
  header + .mobile-menu
  .hero (canvas #net)
  .stats-bar → .trust (marquee) → .press
  #audiencias → #ecosistema (+ flywheel) → #research
  #comunidad (canvas #net2) → #equipo → #newsletter → #faq → #contacto
  footer
  .wa-float
  <script> nav/progress → menu → reveal+counters → scrollspy → glow → network()
```

Cualquier duda sobre una decisión de diseño, la referencia es siempre: primero el Manual de Marca, después este documento, después el mockup.
