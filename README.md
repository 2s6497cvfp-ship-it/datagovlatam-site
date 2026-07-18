# datagovlatam.com — Landing del ecosistema DGL

Landing de marca única del ecosistema **Data Governance Latam**: consultoría ([datagovernancelatam.com](https://www.datagovernancelatam.com)), talento ([dgltalent.com](https://www.dgltalent.com)) y formación ([dgl.academy](https://www.dgl.academy)).

## Stack

HTML/CSS/JS vanilla, un solo archivo (`index.html`), sin dependencias ni build. Fuentes desde Google Fonts (pendiente self-hosting, ver handoff).

## Estructura

- `index.html` — la landing completa
- `docs/handoff-dev.md` — tokens de diseño, specs y checklist de producción
- `CNAME` — dominio para GitHub Pages

## Desarrollo local

Abrir `index.html` en el navegador. No requiere servidor.

## Deploy (GitHub Pages)

1. Settings → Pages → Source: `main` / root
2. DNS del dominio: registros `A` hacia GitHub Pages (`185.199.108.153` y siguientes) y `CNAME` de `www` → `<usuario>.github.io`
3. Activar **Enforce HTTPS**

## Antes de publicar

Revisar el checklist de producción en `docs/handoff-dev.md` — en especial: self-hostear fuentes, servir logo y fotos del equipo desde este dominio, y **no instalar trackers de terceros** (el footer declara "sin cookies de tracking").

---

© Data Governance Latam SA™ · Tu Privacy Partner™
