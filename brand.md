# INFYN — Sistema de diseño

Dirección: **editorial / institucional**. Verde profundo y crema, bloques planos,
tipografía neutra, mucho aire. Debe leer como una consultora seria para una PyME
tradicional, no como un producto SaaS.

---

## Colores

| Token          | Hex       | Uso                                                |
|----------------|-----------|----------------------------------------------------|
| Verde          | `#12281F` | Bloques macizos (hero, método, quote, footer, nav) |
| Verde medio    | `#1E4034` | Hover de botones oscuros, items activos            |
| Verde hoja     | `#2C5C48` | Estados, íconos de línea, barras de datos          |
| Salvia         | `#7DA68B` | Acento: labels, filetes, números, bloques bento    |
| Salvia claro   | `#A8C4B2` | Variación de salvia                                |
| Crema          | `#E7E0CE` | **Base del sitio** y texto sobre verde             |
| Crema hueso    | `#F2EFE7` | Bloques claros de respiro (Ciro, CTA)              |
| Tinta          | `#14201B` | Texto principal sobre crema                        |
| Tinta media    | `#4E5D55` | Texto secundario                                   |
| Tinta suave    | `#7A877F` | Labels, metadatos                                  |

**Prohibido:** verde neón (`#2ED47A`), negro puro, gradientes de color, sombras
difusas de colores, azules y naranjas de dashboard.

---

## Tipografía

**Inter, sola.** Sin serif, sin display, sin condensada.

| Uso                  | Weight | Detalle                                     |
|----------------------|--------|---------------------------------------------|
| Titular hero         | 500    | `clamp(40px,5.2vw,72px)`, tracking `-0.035em` |
| Títulos de sección   | 500    | `clamp(30px,4vw,50px)`, tracking `-0.025em` |
| Números grandes      | 500    | tracking `-0.045em`, `font-feature: tnum`   |
| Cuerpo               | 400    | 15,5–18px, line-height 1.62–1.72            |
| Labels / eyebrows    | 600    | 11px, uppercase, tracking `0.14–0.16em`     |

Nunca weight 700/800: el peso extra es lo que hace que un sitio lea como startup.
La jerarquía se construye con tamaño y aire, no con negrita.

---

## Recursos de marca

### 1. Bloque macizo
Secciones enteras en verde profundo plano, sin degradado ni glow. El contraste
entre bloque verde y base crema **es** la identidad.

### 2. Textura de papel (`.grain`)
Ruido SVG al 30% en `mix-blend-mode: overlay` sobre los bloques verdes. Da el
acabado impreso de las referencias. Solo sobre verde, nunca sobre crema.

```css
.grain::before {
  content: '';
  position: absolute; inset: 0;
  pointer-events: none;
  opacity: 0.30;
  mix-blend-mode: overlay;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='140' height='140'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='3'/%3E%3C/filter%3E%3Crect width='140' height='140' filter='url(%23n)' opacity='0.5'/%3E%3C/svg%3E");
}
.grain > * { position: relative; z-index: 1; }
```

### 3. Arco
Círculos concéntricos de 1px en salvia al 14–22% de opacidad, saliendo del
borde del bloque (hero) o centrados detrás del texto (quote). Geometría plana,
nunca relleno ni blur.

### 4. Esquina cuarto de círculo
`border-top-right-radius: 150px` / `border-bottom-left-radius: 150px` en las
celdas del bento. Un solo vértice por celda, alternando. En mobile baja a 90px.

### 5. Filetes
Separadores de 1px (`rgba(20,32,27,0.14)` sobre crema, `rgba(231,224,206,0.16)`
sobre verde) para columnas y pasos. Reemplazan a las cards con fondo.

---

## Geometría

- `border-radius`: 2px en botones e inputs, 3px en cards y láminas, 0 en el resto.
  La única curva grande es la esquina cuarto de círculo del bento.
- Sin `box-shadow` en ningún lado. La profundidad se hace con color y borde.
- Sin animaciones de entrada ni elementos flotantes.

---

## Layouts por sección

| Sección     | Fondo             | Composición                                   |
|-------------|-------------------|-----------------------------------------------|
| Nav         | `--verde`         | Barra fija sólida, CTA crema                  |
| Hero        | `--verde` + grain | Una columna a la izquierda + arco + barra de 3 datos al pie |
| Problema    | `--crema`         | Statement + 3 columnas separadas por filetes  |
| Método      | `--verde` + grain | 3 filas `01/02/03` con filetes horizontales   |
| Ciro        | `--crema-hueso`   | Lámina de escritorio + teléfono                |
| Resultados  | `--crema`         | Bento de 4 celdas (verde / hueso / salvia / hoja) |
| Quote       | `--verde` + grain | Frase centrada + arco                          |
| CTA         | `--crema-hueso`   | Centrado, botón oscuro                         |
| Footer      | `--verde`         | Logo · nav · copy                              |

---

## Logo

Símbolo infinito con flecha (`Logo Infyn.png`, blanco puro con alpha).

En el sitio no se usa como `<img>`: se enmascara (`mask-image`) sobre un fondo
`var(--crema)`, y el recorte deja solo el símbolo — el wordmark del PNG se
descarta y el nombre se compone con Inter, igual que el resto del sitio. Así el
logo toma siempre un color de la paleta y funciona sobre cualquier fondo con
solo cambiar el `background`.

Nota: los `*.png` están en `.gitignore`, así que el archivo del logo vive solo
en el checkout local y llega a producción por el deploy de Vercel desde la
carpeta, no por git. Si el archivo falta, el sitio degrada al wordmark de texto.

---

## Tono de comunicación

Directo. Claro. Sin humo.

❌ "Transformamos tu negocio con soluciones innovadoras"
✅ "Tu negocio no necesita más ventas. Necesita orden."

---

## Principio

> **Estructura > estética**
> Todo legible en 3 segundos. La seriedad se logra restando.
