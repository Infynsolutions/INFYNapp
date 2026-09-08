# INFYN — Sistema de diseño

Dirección: **editorial / institucional**. Verde profundo y crema, bloques planos,
tipografía neutra, mucho aire. Debe leer como una consultora seria para una PyME
tradicional, no como un producto SaaS.

---

## Colores

| Token          | Hex       | Uso                                                |
|----------------|-----------|----------------------------------------------------|
| Verde          | `#17403A` | Bloques macizos (hero, método, quote, footer, nav) |
| Verde medio    | `#21544C` | Hover de botones oscuros, items activos            |
| Verde hoja     | `#2E6B5D` | Estados, íconos de línea, barras de datos          |
| Salvia         | `#86B0A2` | Acento: labels, filetes, números, bloques bento    |
| Salvia claro   | `#ADCBC0` | Variación de salvia                                |
| Crema          | `#E7E0CE` | **Base del sitio** y texto sobre verde             |
| Crema hueso    | `#F2EFE7` | Bloques claros de respiro (Ciro, CTA)              |
| Tinta          | `#15221F` | Texto principal sobre crema                        |
| Tinta media    | `#4E5F5A` | Texto secundario                                   |
| Tinta suave    | `#586764` | Labels, metadatos                                  |

El verde base es **petróleo**, no oliva: tiene azul adentro. Ese matiz es lo que
lo hace leer serio en vez de "eco". Toda la escala (medio, hoja, salvia) está
calibrada sobre ese mismo matiz — si se cambia el base, se recalibran los cuatro.

**Prohibido:** verde neón (`#2ED47A`), negro puro, gradientes de color, sombras
difusas de colores, azules y naranjas de dashboard.

**Contraste:** todos los pares en uso pasan WCAG AA. Los críticos: crema sobre
verde 8,7:1 · salvia sobre verde 4,8:1 · verde sobre salvia 4,8:1 · tinta suave
sobre crema 4,5:1. Antes de tocar un color, verificar el par contra su fondo.

---

## Tipografía

**Inter** para todo + **Instrument Serif itálica** como acento.

| Uso                  | Weight | Detalle                                     |
|----------------------|--------|---------------------------------------------|
| Titular hero         | 500    | `clamp(40px,5.2vw,72px)`, tracking `-0.035em` |
| Títulos de sección   | 500    | `clamp(30px,4vw,50px)`, tracking `-0.025em` |
| Números grandes      | 500    | tracking `-0.045em`, `font-feature: tnum`   |
| Cuerpo               | 400    | 15,5–18px, line-height 1.62–1.72            |
| Labels / eyebrows    | 600    | 11px, uppercase, tracking `0.14–0.16em`     |

Nunca weight 700/800: el peso extra es lo que hace que un sitio lea como startup.
La jerarquía se construye con tamaño y aire, no con negrita.

### Acento serif (`.serif`)

Instrument Serif itálica, 400, en la **frase que cierra la idea** — nunca en un
párrafo entero. Una sola por bloque de texto. Va a `1.06em` porque su altura x
es menor que la de Inter y sin ese ajuste parece hundida.

Color: `--verde-hoja` sobre crema, `--salvia` sobre verde.

| Bloque      | Grotesk                          | Serif itálica                  |
|-------------|----------------------------------|--------------------------------|
| Hero        | Tu negocio merece un sistema a medida | *sin que estés pendiente.* |
| Problema    | Tu negocio crece. Pero el caos también. El problema no es la venta. | *Es la falta de sistema.* |
| Método      | Tres capas.                      | *Sin huecos entre ellas.*      |
| Ciro        | Ciro.                            | *Tu co-pensador estratégico 24/7.* |
| Resultados  | Números reales.                  | *Casos reales.*                |
| Quote       | Tu negocio no necesita más ventas. | *Necesita orden.*            |
| CTA         | Si tu negocio depende de vos para funcionar, | *no está listo para crecer.* |

### Negrita de cuerpo (`strong`)

Weight 600 sobre párrafos de color atenuado: la negrita levanta el dato que
importa sin subir de peso el sistema. Una o dos por párrafo, nunca más.

El color sale de `--fuerte`, que cada bloque define según su fondo:

```css
strong { font-weight: 600; color: var(--fuerte, var(--tinta)); }
.hero, .metodo, .quote, footer,
.c-verde, .c-hoja, .app-side { --fuerte: var(--crema); }
.c-salvia { --fuerte: var(--verde); }
```

Se hace con variable y no con una lista de selectores para que una negrita
nueva en un bloque oscuro no quede en tinta ilegible.

### Quiebres de línea

Los titulares llevan `<br>` explícitos. El quiebre automático deja palabras
huérfanas ("crecer." sola en una línea) y arruina la composición.

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

### 5. Gráficos

SVG plano, generado con geometría medida: sin relleno de color, sin blur, sin
animación. Cada uno dice algo del dato que acompaña.

| Gráfico       | Dónde                    | Qué es                                        |
|---------------|--------------------------|-----------------------------------------------|
| Arco medido   | Hero                     | Anillos + ticks radiales, como un instrumento |
| Arco de ticks | Quote                    | Círculo completo de ticks detrás de la frase   |
| Tres capas    | Método                   | 3 arcos concéntricos de largo creciente, uno por capa, con `01/02/03` al final de cada arco |
| Sparkline     | Bento `+30%`             | Línea de tendencia ascendente con área         |
| Barras        | Bento `−70%`             | Barras descendentes, la última destacada       |
| Línea de tiempo | Bento `6 semanas`      | 6 nodos, `S1`–`S6`                             |
| Onda          | Bento (celda con aire)   | Líneas verticales ascendentes ancladas a la base |

Reglas: trazos de 1–2,5px en salvia con opacidad entre 0,10 y 0,85; nunca
detrás de un párrafo (compite con la lectura) — van en el aire de la celda.

### 6. Filetes
Separadores de 1px (`rgba(21,34,31,0.14)` sobre crema, `rgba(231,224,206,0.16)`
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

## Nombres de la escalera

| Escalón | Nombre nuevo | Antes | Duración |
|---|---|---|---|
| 0 | **Radiografía** | (igual) | 3 a 5 días · dos archivos |
| 0+ | **Primera pasada** | Auditoría Express | medio día |
| 1 | **Estado de Evidencia** | Audit File | 2 semanas |
| 2 | **Mapa de criterio** | (igual) | 2 a 3 semanas |
| 3 | **Copensador** | (igual) | fee + suscripción |
| 4 | **Estado mensual** | Auditoría recurrente | dentro de la suscripción |

"Audit File" es el nombre del método de Antonio Sánchez De Boeck y no se usa
para nada propio de INFYN — nuestro entregable equivalente se llama "Estado de
Evidencia". *Estado de Evidencia* calca la forma de "estado de resultados":
una foto formal con fecha de corte, que se re-emite por período (por eso el
escalón 4 se llama "Estado mensual" — es el mismo documento, otra vez, no un
producto nuevo).

Nombres descartados por colisión con vocabulario ya en uso en el proceso
comercial de INFYN: *Expediente* (ya es el estado compartido del pipeline
`/cliente-*`) y *Acta* (ya es el Acta de Entrega).

---

## Regla de cifras

En el sitio (`index.html`, `auditoria.html` y cualquier página futura) solo
pueden aparecer cifras de hallazgos de **clientes reales de INFYN**, siempre
**anonimizados**: sin nombre de cliente, solo descripción genérica del rubro
("concesionaria de utilitarios", "cafetería de especialidad", "cadena de
neumáticos, 4 sucursales").

Ninguna cifra del material de Antonio Sánchez De Boeck (su método, sus casos,
sus números de ejemplo) puede publicarse como si fuera un caso de INFYN — esas
cifras son suyas, no nuestras.

**Nunca usar como propias** (son de SdB):
- 55,8% (venta anónima)
- $72,9M (contrafáctico de shopping)
- 42,8% / 25,7% (márgenes shopping / outlet)

**Aprobadas para el sitio** (verificadas como propias de INFYN):
- $569.379.492 mal imputados
- IVA al 21% en vez de 10,5%
- USD 60.000/año de fuga estimada
- 4 sucursales con error de artículos/caja

---

## Tono de comunicación

Directo. Claro. Sin humo.

❌ "Transformamos tu negocio con soluciones innovadoras"
✅ "Tu negocio no necesita más ventas. Necesita orden."

---

## Principio

> **Estructura > estética**
> Todo legible en 3 segundos. La seriedad se logra restando.
