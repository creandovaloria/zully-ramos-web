# Lecciones Aprendidas — Sitio Web Perito Zully Ramos

**Proyecto:** perito.zullyramos.com.mx  
**Fecha:** Junio 2026

---

## 1. Cloudinary: gravity `g_face` es obligatorio para retratos

**Qué pasó:** La foto original es un retrato vertical (768×1365). Al recortar a 1200×630 usando `g_north` (desde arriba), la imagen mostraba el techo de la oficina, no el rostro.

**Solución:** Usar `g_face` como parámetro de gravity. Cloudinary tiene detección de caras integrada que centra automáticamente el recorte en el rostro detectado.

**Regla para futuros proyectos:** Para cualquier foto de perfil o retrato que requiera recorte a formato paisaje para OG image, siempre usar `g_face`. Solo recurrir a `g_north`, `g_center`, etc. cuando no haya una cara en la imagen.

---

## 2. Cloudinary OG image = solución elegante sin backend

**Contexto:** Necesitábamos una imagen OG 1200×630 con headline ("Perito Contable"), nombre y CTA superpuestos, sin crear un archivo de imagen separado ni un servicio de generación de imágenes.

**Solución:** Encadenar transformaciones Cloudinary en la URL:
```
/w_1200,h_630,c_fill,g_face/
l_text:Arial_54_bold:Perito%20Contable,co_white,g_south_west,x_44,y_195/
l_text:Arial_36:Nombre,co_rgb:e8f5f3,g_south_west,x_44,y_125/
l_text:Arial_24_bold:CTA,co_rgb:a8e6df,g_south_west,x_44,y_60/
```

**Ventaja:** La imagen se genera on-demand, sin archivos adicionales en el repo, y se actualiza automáticamente si cambia la foto base en Cloudinary.

**Para futuros proyectos:** Esta técnica es reutilizable para cualquier landing page profesional donde se quiera una OG image con texto sin generación de imágenes programática.

---

## 3. Web3Forms vs Resend en sitios estáticos

**Decisión:** Para este proyecto (HTML estático en Vercel) se usó Web3Forms en lugar de Resend.

**Por qué:** Resend requiere un endpoint de servidor (API route en Next.js o similar). En HTML puro no hay servidor disponible. Web3Forms recibe el `<form>` directamente desde el navegador del visitante y reenvía el email sin necesidad de backend.

**Cuándo usar cada uno:**
- HTML estático → Web3Forms (o Formspree)
- Next.js / cualquier framework con API routes → Resend

---

## 4. La descripción OG tiene un límite real de ~125 caracteres

**Qué pasó:** La primera descripción tenía 161 caracteres. Las plataformas móviles la truncaban y el inspector de metadatos la marcaba como advertencia.

**Regla:** Siempre redactar `og:description` y `twitter:description` por debajo de 120 caracteres. Contar incluyendo espacios, tildes y caracteres especiales.

---

## 5. Verificar metadatos con opengraph.xyz antes de entregar

**Flujo recomendado para futuros proyectos:**
1. Hacer deploy a Vercel
2. Esperar 2 min para que el CDN propague
3. Revisar en https://www.opengraph.xyz
4. Corregir cualquier warning antes de dar por terminado el proyecto

Ahorra rework y da confianza al cliente al ver la preview correcta desde el inicio.

---

## 6. Separar subdominio por servicio desde el inicio

**Decisión:** Usar `perito.zullyramos.com.mx` en lugar de la raíz `zullyramos.com.mx`.

**Por qué:** El dominio raíz queda libre para un sitio institucional futuro. El subdominio es más específico y deja la arquitectura abierta para escalar (ej: `consultas.zullyramos.com.mx`, `auditorias.zullyramos.com.mx`).

**Lección:** Para clientes con un solo dominio y múltiples servicios potenciales, siempre proponer subdominios en lugar de ocupar la raíz con el primer proyecto.
