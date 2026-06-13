# Troubleshooting — Sitio Web Perito Zully Ramos

---

## Problema 1: La imagen OG muestra el techo en lugar de la cara

**Síntoma:** Al compartir el link en WhatsApp o revisarlo en opengraph.xyz, la preview muestra el techo de una oficina en lugar del rostro de Zully.

**Causa:** La foto original es retrato vertical (768×1365). El gravity `g_north` recorta desde la parte superior de la imagen — donde está el techo, no la cara.

**Solución:**
En la URL de Cloudinary, cambiar `g_north` por `g_face`:

```
# Incorrecto
w_1200,h_630,c_fill,g_north/...

# Correcto
w_1200,h_630,c_fill,g_face/...
```

`g_face` usa el detector de caras de Cloudinary para centrar el recorte en el rostro detectado automáticamente.

**Archivos afectados:** `index.html` — líneas con `og:image` y `twitter:image` en el `<head>`.

---

## Problema 2: El formulario no envía (access key pendiente)

**Síntoma:** Al hacer clic en "Enviar mensaje", el botón queda en estado "Enviando…" indefinidamente o cambia a rojo.

**Causa más común:** El access key de Web3Forms no está configurado o es incorrecto.

**Solución:**
1. Ir a https://web3forms.com y verificar el access key del formulario "Contacto Perito Zully Ramos"
2. En `index.html`, buscar la línea:
   ```html
   <input type="hidden" name="access_key" value="...">
   ```
3. Confirmar que el value coincide con el key de la cuenta
4. Verificar que el email destino (`perito@zullyramos.com.mx`) esté confirmado en Web3Forms

**Access key actual:** `3b8a307f-3d1e-48c2-b3e4-11fafc2bf678`

---

## Problema 3: Cambios en el código no se reflejan en el sitio

**Síntoma:** Se editó `index.html` pero el sitio en perito.zullyramos.com.mx sigue mostrando la versión anterior.

**Causas posibles y soluciones:**

| Causa | Solución |
|---|---|
| No se hizo `git push` | Correr `git push` desde la carpeta del proyecto |
| Vercel aún está desplegando | Esperar 1-2 min y revisar el dashboard de Vercel |
| Caché del navegador | Hacer Ctrl+Shift+R (hard refresh) o probar en modo incógnito |
| El CDN tiene caché | Esperar ~5 min para propagación completa |

**Verificar el deploy:** Ir a https://vercel.com → proyecto `zully-ramos-web` → pestaña "Deployments" para ver si el último commit está desplegado.

---

## Problema 4: La imagen OG no se actualiza en WhatsApp después de cambiarla

**Síntoma:** Se actualizó la imagen pero WhatsApp sigue mostrando la versión anterior.

**Causa:** WhatsApp cachea agresivamente las vistas previas de links.

**Solución:** WhatsApp no tiene forma de forzar refresco de caché desde el exterior. Las opciones son:
1. Esperar ~24-72 horas a que el caché expire naturalmente
2. Agregar un query string a la URL de la imagen OG para forzar una URL diferente (ej: `?v=2`), aunque esto no siempre funciona en WhatsApp
3. Para Facebook/LinkedIn, usar el [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/) para limpiar el caché manualmente

---

## Problema 5: El dominio no apunta al sitio de Vercel

**Síntoma:** `perito.zullyramos.com.mx` da error de DNS o carga una página en blanco.

**Verificación:**
```bash
dig perito.zullyramos.com.mx CNAME
```
Debe responder con `cname.vercel-dns.com`.

**Solución:** En el panel DNS del registrador del dominio, verificar que existe el registro:
```
Tipo:   CNAME
Nombre: perito
Valor:  cname.vercel-dns.com
TTL:    3600 (o el valor por defecto)
```
Si el registro existe pero no responde, esperar hasta 48 horas para propagación de DNS.
