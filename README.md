# Zully Ramos Hernández — Sitio Web de Contacto

Landing page profesional para la M.A.C. y Lic. en Contaduría Zully Tzetziangari Ramos Hernández, Perito Contable oficial de la JFCA/STPS.

**URL en producción:** https://perito.zullyramos.com.mx

---

## Stack técnico

| Componente | Tecnología |
|---|---|
| Frontend | HTML5 + CSS3 + Vanilla JS (un solo archivo) |
| Hosting | Vercel (deploy automático desde GitHub) |
| Formulario | Web3Forms (API gratuita, 250 envíos/mes) |
| Foto e imagen OG | Cloudinary (transformaciones vía URL) |
| Fuentes | Google Fonts — Cormorant Garamond + Inter |

---

## Estructura del proyecto

```
zully-ramos-web/
├── index.html           # Toda la página (HTML + CSS + JS inline)
├── README.md
├── PRD.md
├── LECCIONES_APRENDIDAS.md
├── TROUBLESHOOTING.md
└── graphify-out/        # Grafo de arquitectura (generado, no se versiona)
```

---

## Secciones de la página

1. **Hero** — Foto, nombre, badge JFCA, estadísticas, CTAs
2. **Servicios** — 4 cards (Peritajes contables destacado)
3. **Especialización Pericial** — 6 bloques de trayectoria JFCA
4. **Experiencia** — Timeline de puestos (IMSS, DID)
5. **Formación** — Maestría + Licenciatura + competencias
6. **Contacto** — Datos + formulario + WhatsApp flotante

---

## Formulario de contacto

Usa [Web3Forms](https://web3forms.com). El access key está en el `<head>` del HTML:

```html
<input type="hidden" name="access_key" value="3b8a307f-...">
```

Los mensajes llegan a **perito@zullyramos.com.mx**. El plan gratuito permite 250 envíos/mes. Para aumentar el límite: https://web3forms.com/pricing

---

## Foto de perfil (Cloudinary)

La foto **no se versiona en el repo**: vive en Cloudinary y se referencia en 3 lugares de `index.html`.

- **Cloud name:** `siu0xbwv`
- **Public ID actual:** `WhatsApp_Image_2026-09-29_at_18.09.14`

| Uso | Línea | Transformación |
|---|---|---|
| Hero | `<img class="hero-image">` | `f_auto,q_auto,c_fill,g_face,ar_3:4,w_740` |
| `og:image` | `<head>` | `w_1200,h_630,c_fill,g_face` + 3 capas `l_text:` |
| `twitter:image` | `<head>` | idéntica a `og:image` |

El recorte lo hace Cloudinary por URL, no el CSS: `g_face` centra el rostro automáticamente y `ar_3:4` da el retrato vertical que espera el marco del hero. Por eso el `object-position` es `center top` y no un porcentaje afinado a mano — la foto ya llega encuadrada.

**Para cambiar la foto:** subir la nueva imagen a Cloudinary y reemplazar el public ID en las 3 referencias. No hace falta recortarla antes: las transformaciones se encargan. Después, limpiar el caché de OG (ver `TROUBLESHOOTING.md`, problema 4).

---

## Grafo de arquitectura (Graphify)

La documentación viva de arquitectura se genera con [Graphify](https://github.com/Graphify-Labs/graphify). El grafo vive en `graphify-out/` y **no se versiona** (se regenera).

```bash
graphify update .                      # regenerar el grafo
graphify query "donde esta la foto"    # consultar
graphify affected "hero-image"         # que se rompe si toco esto
graphify explain "hero-image"          # explicacion en lenguaje llano
```

Un hook `post-commit` regenera el grafo en cada commit. Si se clona el repo de nuevo hay que reinstalarlo (los hooks no viajan en git):

```bash
cat > .git/hooks/post-commit <<'HOOK'
#!/bin/sh
export PATH="$HOME/.local/bin:$PATH"
command -v graphify >/dev/null 2>&1 && graphify update . >/dev/null 2>&1 &
HOOK
chmod +x .git/hooks/post-commit
```

**Convención:** consultar el grafo antes de refactors o de preguntar "¿cómo funciona X?", antes de abrir archivos a mano.

---

## Despliegue

El proyecto usa **Vercel + GitHub** con deploy continuo:

1. Cualquier push a `main` desencadena un deploy automático
2. Vercel detecta el proyecto como sitio estático
3. No requiere build steps ni dependencias

Para hacer cambios:
```bash
# Editar index.html, luego:
git add index.html
git commit -m "descripción del cambio"
git push
```

El deploy tarda ~30 segundos.

---

## Dominio

- **Dominio:** zullyramos.com.mx
- **Subdominio activo:** perito.zullyramos.com.mx
- **DNS:** Registro CNAME apuntando a `cname.vercel-dns.com`
- **SSL:** Automático vía Vercel

---

## Contacto del cliente

- **Cliente:** Zully Tzetziangari Ramos Hernández
- **Email profesional:** perito@zullyramos.com.mx
- **WhatsApp:** 55 2727 5299
- **Ubicación:** San Juan del Río, Querétaro
