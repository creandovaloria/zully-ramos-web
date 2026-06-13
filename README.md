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
| Imagen OG | Cloudinary (transformaciones vía URL) |
| Fuentes | Google Fonts — Cormorant Garamond + Inter |

---

## Estructura del proyecto

```
zully-ramos-web/
├── index.html           # Toda la página (HTML + CSS + JS inline)
├── README.md
├── PRD.md
├── LECCIONES_APRENDIDAS.md
└── TROUBLESHOOTING.md
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

## Imagen OG (redes sociales)

La imagen de vista previa al compartir el link se genera dinámicamente con Cloudinary:

- **Recorte:** 1200×630 con detección automática de cara (`g_face`)
- **Texto superpuesto:** "Perito Contable" + nombre + "Solicitar consulta"
- **URL base:** `https://res.cloudinary.com/dldccvnyj/image/upload/...`

Para cambiar la foto: subir la nueva imagen a Cloudinary y actualizar el public ID en las URLs de `og:image` y `twitter:image` dentro del `<head>`.

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
