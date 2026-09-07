# INFYN — Contexto del proyecto

## Qué es

Consultora estratégica para PyMEs latinoamericanas.  
Ayuda a negocios que crecen en caos a ordenarse con procesos, estructura y visión.

**Propuesta:** Convertimos complejidad en sistema.  
**Posicionamiento:** No somos una agencia ni una tech company. Somos una consultora moderna que también implementa.

---

## Archivos del proyecto

| Archivo       | Descripción                                      |
|---------------|--------------------------------------------------|
| `index.html`  | Sitio web completo (HTML + CSS inline, sin build) |
| `brand.md`    | Sistema de diseño: colores, tipografía, aurora CSS |

---

## Stack

- HTML + CSS puro en un solo archivo (`index.html`)
- Sin frameworks, sin build tools, sin dependencias
- Tipografía: **Inter** via Google Fonts
- Sin JavaScript (por ahora)

---

## Sistema de diseño

Dirección: **editorial / institucional** (rediseño 2026-09-07). Ver `brand.md`.

### Colores

```
Verde        : #12281F   ← bloques macizos (hero, método, quote, nav, footer)
Verde medio  : #1E4034   ← hover, items activos
Verde hoja   : #2C5C48   ← íconos de línea, barras de datos
Salvia       : #7DA68B   ← acento (labels, filetes, celdas bento)
Crema        : #E7E0CE   ← base del sitio
Crema hueso  : #F2EFE7   ← bloques claros de respiro
Tinta        : #14201B   ← texto sobre crema
```

Prohibido: verde neón `#2ED47A`, negro puro, gradientes, sombras de color.

### Tipografía

Inter, sola. Títulos `font-weight: 500` (nunca 700/800), cuerpo `400`,
labels `600` en uppercase con `letter-spacing: 0.14em`. La jerarquía se hace
con tamaño y aire, no con negrita.

### Recursos de marca

- `.grain` — textura de papel (ruido SVG, `mix-blend-mode: overlay`), solo sobre verde
- Arco — círculos concéntricos de 1px en salvia (hero y quote)
- Esquina cuarto de círculo — `border-radius` de 150px en un solo vértice de las celdas bento
- Filetes de 1px en vez de cards con fondo
- Sin sombras, sin animaciones de entrada, `border-radius` 2–3px en el resto

### Layouts por sección

| Sección    | Fondo             | Composición                                     |
|------------|-------------------|-------------------------------------------------|
| Nav        | `--verde`         | Barra fija sólida, CTA crema                    |
| Hero       | `--verde` + grain | Columna izquierda + arco + barra de 3 datos     |
| Problema   | `--crema`         | Statement + 3 columnas con filetes              |
| Método     | `--verde` + grain | 3 filas 01/02/03 con filetes                    |
| Ciro       | `--crema-hueso`   | Lámina de escritorio + teléfono                 |
| Resultados | `--crema`         | Bento de 4 celdas                               |
| Quote      | `--verde` + grain | Frase centrada + arco                           |
| CTA        | `--crema-hueso`   | Centrado, botón oscuro                          |
| Footer     | `--verde`         | Logo · nav · copy                               |

---

## Tono de comunicación

Directo. Claro. Sin humo.

❌ "Transformamos tu negocio con soluciones innovadoras"  
✅ "Tu negocio no necesita más ventas. Necesita orden."

**Palabras clave:** orden, sistema, procesos, estructura, resultados medibles, implementación real.

---

## Reglas de diseño

- Estructura > estética
- Todo legible en 3 segundos
- Mucho aire entre elementos
- No agregar decoración sin función
- No usar diseño "startup hype" ni estética cripto

---

## Negocio

**Servicios:**
1. Diagnóstico operacional (48–72 hs)
2. Diseño del sistema (1 semana)
3. Implementación real (2–6 semanas)
4. Seguimiento y métricas (30 días)

**Dolores del cliente:**
- Dependencia del dueño
- Falta de procesos
- Decisiones sin datos

**Mercado:** PyMEs de Argentina, Chile y México.

**CTA principal:** "Agendar diagnóstico" (primera conversación sin costo).
