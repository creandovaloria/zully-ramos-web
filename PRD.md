# PRD — Sitio Web de Contacto: Perito Contable Zully Ramos

**Versión:** 1.0  
**Fecha:** Junio 2026  
**Responsable:** Arturo Barrios / Creando Valor IA  
**Cliente:** M.A.C. y Lic. Zully Tzetziangari Ramos Hernández  

---

## 1. Problema

Zully Ramos es una perito contable con más de 20 años de trayectoria y presencia en la lista oficial JFCA/STPS. No contaba con presencia digital profesional: clientes potenciales no podían encontrarla ni verificar sus credenciales fácilmente. La adquisición de clientes dependía 100% de referencias personales.

---

## 2. Objetivo

Crear una landing page de contacto que:
- Proyecte credibilidad profesional ante abogados, empresas y particulares
- Destaque la especialización pericial como principal servicio
- Genere solicitudes de consulta directas vía formulario y WhatsApp
- Sea fácil de mantener por un equipo no técnico

---

## 3. Usuarios objetivo

| Segmento | Necesidad |
|---|---|
| Abogados litigantes | Encontrar un perito confiable para procesos laborales ante JFCA |
| Empresas demandadas | Contratar peritaje contable de defensa en juicios laborales |
| Particulares en litigio | Obtener un dictamen pericial independiente |

---

## 4. Alcance (en scope)

- [x] Landing page de una sola página (single-page)
- [x] Hero con foto profesional y badge de credencial JFCA
- [x] Sección de servicios con peritajes como card destacada
- [x] Sección de especialización pericial con bullets del CV
- [x] Timeline de experiencia profesional
- [x] Sección de formación académica y competencias
- [x] Formulario de contacto funcional (Web3Forms → perito@zullyramos.com.mx)
- [x] Botón de WhatsApp flotante
- [x] Metadatos Open Graph y Twitter Card optimizados
- [x] Imagen OG 1200×630 con headline y CTA via Cloudinary
- [x] Subdominio perito.zullyramos.com.mx en Vercel
- [x] Deploy continuo desde GitHub

---

## 5. Fuera de alcance (v1.0)

- Blog o sección de artículos
- Sistema de agendamiento de citas
- Pasarela de pagos
- Panel de administración de contenido (CMS)
- Versión en inglés
- Analytics avanzados (solo los que provee Vercel por defecto)

---

## 6. Decisiones técnicas

### ¿Por qué HTML estático y no Next.js?
La página no requiere lógica de servidor ni SSR. Un archivo HTML único elimina dependencias, tiempos de build y superficie de error. Vercel lo sirve como CDN sin configuración adicional.

### ¿Por qué Web3Forms y no Resend?
Resend requiere un endpoint de servidor. En un sitio estático, Web3Forms procesa el formulario desde el navegador sin backend. Plan gratuito (250 envíos/mes) suficiente para el volumen esperado. La cuenta de Resend ya existente se reserva para proyectos Next.js.

### ¿Por qué Cloudinary para la imagen OG?
La foto original es retrato (768×1365). Las redes sociales esperan 1200×630 (ratio 1.91:1). Cloudinary permite transformar la imagen vía URL sin necesidad de editar y re-subir un archivo. La detección de cara (`g_face`) garantiza que el recorte siempre centre el rostro automáticamente.

### ¿Por qué subdominio perito.* y no la raíz?
El dominio raíz `zullyramos.com.mx` queda libre para un posible sitio principal futuro. El subdominio `perito.*` es semánticamente claro y específico para este servicio.

---

## 7. Criterios de aceptación

- [x] La página carga en menos de 3 segundos en conexión móvil
- [x] El formulario envía correctamente y llega a perito@zullyramos.com.mx
- [x] El botón de WhatsApp abre conversación con mensaje predeterminado
- [x] La imagen OG muestra la cara de Zully en proporción 1.91:1 al compartir el link
- [x] El inspector de metadatos reporta 0 errores críticos
- [x] El sitio es responsive en móvil, tablet y desktop

---

## 8. Métricas de éxito (sugeridas para seguimiento)

| Métrica | Meta inicial |
|---|---|
| Solicitudes de contacto por formulario | ≥ 2 / mes |
| Clics en WhatsApp flotante | ≥ 5 / mes |
| Posición en Google: "perito contable Querétaro" | Top 10 en 6 meses |
