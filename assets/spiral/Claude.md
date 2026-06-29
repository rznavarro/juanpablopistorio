# CLAUDE.md — Proyecto Juan Pablo Pistorio Realtor®
### Reglas del proyecto para Claude Code

---

## CONTEXTO DEL PROYECTO

Sitio web de lujo para Juan Pablo Pistorio, REALTOR® licenciado en Florida, especializado en inversiones inmobiliarias para inversores latinoamericanos. Cliente de Vortexia.

---

## STACK TÉCNICO — REGLA CRÍTICA

Este proyecto es **HTML + CSS + JavaScript vanilla**. NO es un proyecto React/Next.js.

- Un único archivo `index.html` (o estructura simple de archivos estáticos)
- CSS en `<style>` o archivo `.css` separado, sin frameworks (sin Tailwind, sin Bootstrap)
- JavaScript vanilla + librerías cargadas vía CDN
- GSAP 3.12.5 + ScrollTrigger (animaciones de scroll)
- Lenis 1.1.14 (smooth scroll)
- Sin npm, sin pnpm, sin build tools, sin bundlers
- Sin frameworks de componentes (NO React, NO Vue, NO Svelte)

**Siempre usar pnpm** si en algún punto del proyecto se requiere instalar algo vía npm — esto es una regla general del cliente para todos sus proyectos, aunque este proyecto específico no debería necesitar instalaciones.

---

## REGLA ESPECIAL — REACT BITS

El cliente toma inspiración visual y de animación de **React Bits** (reactbits.dev), una librería de componentes animados para React.

**IMPORTANTE:** React Bits se instala vía CLI (`npx shadcn@latest add @react-bits/...` o `npx jsrepo add ...`) y asume un proyecto React/Next.js con shadcn configurado. **Este proyecto NO tiene esa base, por lo tanto el CLI de React Bits NO se debe ejecutar ni asumir como funcional aquí.**

Cuando el cliente pegue código o un link de un componente de React Bits y pida implementarlo:

1. **NO intentes instalar React Bits ni correr su CLI.**
2. **NO sugieras migrar el proyecto a React** a menos que el cliente lo pida explícitamente.
3. **Sí debes traducir la lógica de animación** del componente React Bits a vanilla JS + GSAP, manteniendo el mismo resultado visual.
4. Identifica qué hace el componente original (ej: SplitText anima palabras con stagger, BlurText desenfoca y enfoca al hacer scroll, GradientText anima un gradiente de color en el texto) y recréalo usando:
   - GSAP + ScrollTrigger para el timing y trigger de scroll
   - CSS puro para estilos visuales (gradientes, blur, transforms)
   - Vanilla JS para cualquier lógica de estado simple

### Ejemplo de traducción esperada

Si el cliente dice: *"Quiero el efecto SplitText de React Bits en el hero"*

Correcto: Implementar el split de palabras con `SplitText` de GSAP (el plugin de GSAP, que es distinto pero compatible conceptualmente) o con una función manual que envuelva cada palabra en un `<span>`, animando con `gsap.from()` y `stagger`.

Incorrecto: Correr `npx shadcn@latest add @react-bits/SplitText-TS-TW` o sugerir crear un proyecto Next.js nuevo.

---

## SISTEMA DE DISEÑO

```css
--bg-primary: #080B12;
--bg-secondary: #0D1220;
--gold-primary: #C9A84C;
--gold-light: #E2C97E;
--text-primary: #F5F5F0;
--text-secondary: #9CA3AF;
--font-heading: 'Playfair Display', serif;
--font-body: 'Inter', sans-serif;
```

Estilo: **Dark Luxury Professional** — fondo negro azulado, acentos dorados, tipografía serif en títulos, sans-serif en cuerpo. Inspirado en webs de wealth management / banca privada, NO en sitios inmobiliarios genéricos.

---

## ANIMACIONES — LIBRERÍAS PERMITIDAS

- GSAP core
- GSAP ScrollTrigger
- GSAP SplitText (plugin oficial de GSAP, gratuito)
- GSAP ScrollSmoother
- Lenis (smooth scroll)

Todo vía CDN, nunca vía npm install para este proyecto.

```html
<script src="https://unpkg.com/lenis@1.1.14/dist/lenis.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.12.5/dist/SplitText.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.12.5/dist/ScrollSmoother.min.js"></script>
```

---

## ASSETS

Todas las imágenes y videos van en `/assets/` con rutas relativas. El cliente adjunta los archivos directamente — nunca generar placeholders ni asumir nombres de archivo distintos a los que el cliente indique.

---

## COPY

- Español neutro para mercado latino-USA (NO regionalismos argentinos como "reservá", "tomá")
- Tono serio, confiable, experto — no vendedor agresivo
- Nunca modificar el copy ya aprobado sin que el cliente lo pida explícitamente

---

## REGLA DE EJECUCIÓN

Antes de instalar cualquier dependencia o correr cualquier CLI, verificar primero si el proyecto realmente lo necesita dado que es vanilla HTML/CSS/JS. Si una solución vía CDN o código manual resuelve lo mismo sin agregar un build step, **siempre preferir esa opción**.