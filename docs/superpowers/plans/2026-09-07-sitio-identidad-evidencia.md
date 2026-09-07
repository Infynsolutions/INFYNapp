# Sitio INFYN — identidad nueva: plan de implementación

> **Para quien ejecute:** usar `superpowers:subagent-driven-development` o
> `superpowers:executing-plans`. Los pasos van con checkbox (`- [ ]`).

**Goal:** rehacer el contenido del sitio para que venda la identidad nueva — primero
medimos la evidencia, después construimos — y sumar `/auditoria` como la página del método.

**Arquitectura:** HTML + CSS puro, sin build. El sistema de diseño (hoy inline en
`index.html`) se extrae a `sistema.css` y lo comparten `index.html` y `auditoria.html`;
así la página nueva no puede derivar como derivaron `/diagnostico` y `/ejemplos`. El
markup reusa los componentes que ya existen (`.paso`, `.bento`/`.celda`, `.columnas`,
`.lamina`, `.hero-datos`): casi todo el trabajo es copy, no CSS nuevo.

**Stack:** HTML5, CSS3 (custom properties), SVG inline, Vercel estático.

**Spec:** `docs/superpowers/specs/2026-09-07-sitio-identidad-evidencia-design.md`

**Worktree:** `/Users/sofia/Projects/INFYN-sitio-evidencia`, rama `sitio/identidad-evidencia`.

---

## Mapa de archivos

| Archivo | Responsabilidad |
|---|---|
| `sistema.css` | **Nuevo.** Tokens, tipografía, componentes compartidos. Sale de `index.html` sin cambios de valor |
| `index.html` | Nuevo contenido, 12 bloques. Linkea `sistema.css` |
| `auditoria.html` | **Nuevo.** La página del método. Linkea `sistema.css` |
| `brand.md` | Se le suma la sección de nombres (escalera) y la regla de cifras propias |
| `diagnostico.html`, `ejemplos.html` | **No se tocan.** Backlog |

## Verificación (vale para todas las tareas)

```bash
cd /Users/sofia/Projects/INFYN-sitio-evidencia && python3 -m http.server 8765
```
Abrir `http://localhost:8765/index.html`. **Nunca `file://`** — rompe el logo y los
`cleanUrls`. Revisar a 1440px, 1024px, 860px y 390px de ancho.

Reglas que se chequean en cada commit:
- Ningún `rgba(` con verde escrito a mano dentro de un SVG nuevo: `currentColor` o `var()`.
- `strong` toma color de `var(--fuerte)`; si un bloque nuevo va sobre verde, se agrega al
  selector de `--fuerte`.
- Ningún par color/fondo nuevo por debajo de 4,5:1.
- Ningún precio en ninguna página. Ninguna cifra que no sea de un cliente de INFYN.

---

### Task 1: Extraer el sistema de diseño a `sistema.css`

**Files:**
- Create: `sistema.css`
- Modify: `index.html` (bloque `<style>` completo → `<link>`)

- [ ] **Step 1: Cortar el CSS a un archivo propio**

```bash
cd /Users/sofia/Projects/INFYN-sitio-evidencia
python3 - <<'PY'
s = open('index.html', encoding='utf-8').read()
ini = s.index('<style>') + len('<style>')
fin = s.index('</style>')
open('sistema.css', 'w', encoding='utf-8').write(s[ini:fin].strip() + '\n')
nuevo = s[:s.index('<style>')] + '<link rel="stylesheet" href="/sistema.css">' + s[fin + len('</style>'):]
open('index.html', 'w', encoding='utf-8').write(nuevo)
PY
```

- [ ] **Step 2: Verificar que no cambió nada visualmente**

Levantar el server y comparar contra producción (https://infynsolutions.com) en la misma
pantalla. Esperado: idéntico. Si el logo desaparece, el `<link>` quedó con ruta relativa —
tiene que ser `/sistema.css`.

- [ ] **Step 3: Commit**

```bash
git add sistema.css index.html
git commit -m "refactor(sitio): el sistema de diseño sale a sistema.css"
```

---

### Task 2: Nav, `<head>` y hero nuevos

**Files:** Modify `index.html` (nav + `<section class="hero">`), `sistema.css` (componente nuevo)

- [ ] **Step 1: `<head>`**

```html
<title>INFYN — Primero medimos con qué decidís</title>
<meta name="description" content="Auditamos la base de datos con la que tu PyME toma decisiones: qué podés afirmar con ella y qué no. Después construimos el sistema.">
```

- [ ] **Step 2: Nav**

Links: `Método` → `/auditoria` · `Cómo se avanza` → `#escalera` · `La prueba` → `#prueba` ·
`Contacto` → `#contacto`. El `.nav-cta` dice **Pedir la radiografía** y va a `#contacto`.

- [ ] **Step 3: Copy del hero** (reusa `.hero-tag`, `.hero-headline`, `.hero-sub`, `.hero-actions`, `.hero-datos`)

```html
<div class="hero-tag">Auditoría de datos · Sistemas a medida</div>
<h1 class="hero-headline">
  Primero medimos con qué decidís.<br>
  <em class="serif">Después construimos lo que falta.</em>
</h1>
<p class="hero-sub">
  Auditamos la base con la que tu negocio toma decisiones y te decimos
  <strong>qué podés afirmar con ella y qué no</strong>. Recién después se construye encima.
</p>
<div class="hero-actions">
  <a href="#contacto" class="btn btn-claro">Pedir la radiografía</a>
  <a href="/auditoria" class="btn btn-linea">Ver el método</a>
</div>
<ul class="hero-datos">
  <li><span class="dato-num">2</span><span class="dato-label">archivos, y ya se puede medir</span></li>
  <li><span class="dato-num">3 a 5</span><span class="dato-label">días la radiografía completa</span></li>
  <li><span class="dato-num">5 de 5</span><span class="dato-label">auditorías nuestras encontraron algo</span></li>
</ul>
```

- [ ] **Step 4: La lámina de score en el hero**

Reemplaza a `.hero-arco`. Cuatro arcos chicos, uno por eje, con su puntaje, más una línea
de hallazgo abajo. CSS nuevo en `sistema.css`:

```css
/* ─── Lámina de score: el entregable de la radiografía, en el hero ─── */
.score-lamina {
  background: var(--crema); color: var(--tinta);
  border-radius: 3px; padding: 26px 28px 22px;
  display: flex; flex-direction: column; gap: 20px;
}
.score-ejes { display: grid; grid-template-columns: repeat(4, 1fr); gap: 18px; }
.score-eje { display: flex; flex-direction: column; align-items: center; gap: 9px; }
.score-eje svg { width: 62px; height: 62px; color: var(--verde-hoja); }
.score-eje-num { font-size: 19px; font-weight: 500; letter-spacing: -0.03em; }
.score-eje-label {
  font-size: 9.5px; font-weight: 600; text-transform: uppercase;
  letter-spacing: 0.13em; color: var(--tinta-suave); text-align: center;
}
.score-hallazgo {
  border-top: 1px solid var(--linea); padding-top: 16px;
  font-size: 13px; line-height: 1.55; color: var(--tinta-media);
}
.score-hallazgo strong { font-weight: 600; color: var(--tinta); }
@media (max-width: 860px) { .score-ejes { grid-template-columns: repeat(2, 1fr); } }
```

Cada arco es un SVG de trazo circular con `stroke="currentColor"` — **nunca** el hex
escrito. Valores de muestra: Aprovechamiento 71 · Cobertura 64 · Frescura 88 · Veracidad 42.
El hallazgo: `<strong>Veracidad 42.</strong> El transaccional y el mayor no cierran en 4 de los últimos 6 meses.`

- [ ] **Step 5: Verificar y commitear**

Chequear el fold a 1440px y a 390px: el titular, la barra de datos y la lámina tienen que
entrar sin scroll en desktop.

```bash
git add index.html sistema.css
git commit -m "feat(sitio): hero nuevo — primero medimos, después construimos"
```

---

### Task 3: Bloque "Las dos puertas"

**Files:** Modify `index.html` (sección nueva después del hero), `sistema.css`

- [ ] **Step 1: Markup** (reusa `.celda`, `.c-verde`, `.c-hueso`, `.celda-titulo`)

Sección `<section class="puertas">` sobre `--crema`, con eyebrow **Por dónde entrás**,
título `Dos situaciones.<br><em class="serif acento-verde">Un solo camino.</em>` y dos
tarjetas en grilla de 2:

**Puerta A** (`.c-verde`) — *Ya tenés un sistema.*
> Y no sabés si podés confiar en lo que te dice. El tablero cierra, pero cuando alguien
> pregunta de dónde sale un número, la respuesta es *"lo calcula el sistema"*.

**Puerta B** (`.c-hueso`) — *Todavía no tenés sistema.*
> La operación vive en Excel, en un cuaderno y en la cabeza de tres personas. Lo informal
> no se tira: **casi siempre es donde está la plata.**

- [ ] **Step 2: El cierre del bloque**

Debajo de las dos tarjetas, centrado, con filete arriba:
> Las dos puertas dan al mismo pasillo. **Nadie construye sobre una base que no midió.**

- [ ] **Step 3: CSS**

```css
.puertas { background: var(--crema); padding: 110px 40px; }
.puertas-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; margin-top: 54px; }
.puerta-cierre {
  margin-top: 42px; padding-top: 28px; border-top: 1px solid var(--linea);
  text-align: center; font-size: 17px; line-height: 1.6; color: var(--tinta-media);
}
@media (max-width: 860px) {
  .puertas { padding: 84px 24px; }
  .puertas-grid { grid-template-columns: 1fr; }
}
```

- [ ] **Step 4: Commit**

```bash
git add index.html sistema.css
git commit -m "feat(sitio): las dos puertas — dos situaciones, un camino"
```

---

### Task 4: Bloque "El problema", reescrito

**Files:** Modify `index.html` (`<section class="problema">`)

- [ ] **Step 1: Statement**

```html
<p class="problema-statement">
  No es que no tengas datos.
  <em class="serif acento-verde">Es que nadie te dijo nunca cuánto valen los que tenés.</em>
</p>
```

- [ ] **Step 2: Las tres columnas** (reusa `.columnas` / `.columna`)

1. **El dato que no se carga** — Un campo vacío no es un error del sistema. Es una decisión
   que nadie tomó, **repetida medio millón de veces**. No se arregla con desarrollo: se
   arregla decidiendo que se pide el dato.
2. **El conteo que miente** — Contar celdas vacías da 87,2 %. El número real era **95,7 %**.
   La diferencia es clasificar cada vacío —estructural, omisión o foco— con una razón de
   negocio escrita al lado. Eso no lo hace una herramienta.
3. **La decisión tardía** — El costo no aparece en ningún reporte. Es la decisión que
   tomaste tarde **porque el dato llegó tarde**, y nadie la anotó en ningún lado.

- [ ] **Step 3: Verificar y commitear**

```bash
git add index.html
git commit -m "feat(sitio): el problema — cuánto valen los datos que ya tenés"
```

---

### Task 5: Bloque "Los cuatro ejes"

**Files:** Modify `index.html` (`<section class="metodo">`, id `#metodo`)

- [ ] **Step 1: Header**

Eyebrow **El método**. Título `Cuatro ejes.<br><em class="serif acento-salvia">Doce controles.</em>`
Bajada: *La misma medición, en el mismo orden, en todos los clientes. El puntaje no aprueba
ni reprueba:* **dice cuántas horas hay que poner y dónde.**

- [ ] **Step 2: Los cuatro `.paso`**

`.paso-num` = 01…04 · `.paso-titulo` = nombre del eje + la pregunta · `.paso-texto` = cómo
se mide · `.paso-tiempo` = el ejemplo real.

| # | Eje · la pregunta | Cómo se mide | Ejemplo (`.paso-tiempo`) |
|---|---|---|---|
| 01 | **Aprovechamiento** — ¿Cuánto de lo que tu sistema pide se está cargando de verdad? | Censo columna por columna, separando el vacío por diseño del vacío por omisión **antes** de puntuar | Un campo de garantía con 0 filas |
| 02 | **Cobertura** — De todo lo que pasó en el negocio, ¿cuánto quedó registrado? | Maestro contra movimiento, períodos completos, transacciones atribuibles a un tercero. La misma medición puede ser falla o decisión tomada a conciencia: **eso se cierra preguntando** | 62 ventas sin cobro asociado |
| 03 | **Frescura** — ¿Cuánto tarda un hecho en aparecer? ¿Y qué aparece antes de pasar? | Rezago entre el hecho y el registro, homogeneidad del corte entre fuentes, registros anticipados | El rezago negativo: lo que se registra antes de ocurrir |
| 04 | **Veracidad** — Si te señalo un número de tu balance, ¿podés justificarlo hasta el asiento? | Cierre de la partida doble, tie-out mes a mes, unicidad efectiva de las claves. Y lo físico antes que lo contable: **si dice 100 unidades, tiene que haber 100 unidades** | IVA liquidado al 21 % durante años |

- [ ] **Step 3: Link al método completo**

Debajo del último paso: `<a class="celda-link" href="/auditoria">Ver el método completo</a>`

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat(sitio): los cuatro ejes en lenguaje de dueño"
```

---

### Task 6: Bloque "La escalera"

**Files:** Modify `index.html` (sección nueva `#escalera`), `sistema.css`

- [ ] **Step 1: Header**

Eyebrow **Cómo se avanza**. Título `Un escalón por vez.<br><em class="serif acento-verde">Nadie los saltea.</em>`

- [ ] **Step 2: Los seis escalones**

| # | Nombre | Duración | Qué sale |
|---|---|---|---|
| 01 | Radiografía | 3 a 5 días | Puntaje de los cuatro ejes, un hallazgo con nombre y las tres preguntas que hoy tu base no contesta. Hace falta el mayor contable y el plan de cuentas: nada más |
| 02 | Primera pasada | medio día | Los hallazgos que aparecen sobre la base real, ordenados por plata, cada uno con su consulta y su número. Y una sección de **lo que sí funciona** |
| 03 | Estado de Evidencia | 2 semanas | Los cuatro ejes completos, el universo auditado declarado con fecha de corte, y **la lista escrita de lo que hoy no podés afirmar** |
| 04 | Mapa de criterio | 2 a 3 semanas | Los indicadores que tu base sí sostiene, con umbral y acción. Y el mapa de dónde dos áreas miran distinto el mismo dato |
| 05 | El sistema | 2 a 6 semanas | Recién acá se construye. Sobre una base medida y con el criterio pactado por escrito |
| 06 | Estado mensual | cada mes | El mismo estado, re-emitido. Lo que se reporta es qué limitaciones se levantaron desde la corrida anterior |

- [ ] **Step 3: La nota de precio**

Al pie del bloque, con filete arriba:
> Cada plan se arma sobre tu negocio. **El alcance y el precio salen de la primera
> conversación**, no de una lista de precios.

- [ ] **Step 4: CSS**

```css
.escalera { background: var(--crema-hueso); padding: 120px 40px; }
.escalon {
  display: grid; grid-template-columns: 62px 1fr 150px;
  gap: 34px; align-items: start;
  padding: 30px 0; border-top: 1px solid var(--linea);
}
.escalon:last-of-type { border-bottom: 1px solid var(--linea); }
.escalon-num {
  font-size: 13px; font-weight: 600; color: var(--verde-hoja);
  letter-spacing: 0.08em; padding-top: 4px;
}
.escalon-nombre { font-size: 21px; font-weight: 500; letter-spacing: -0.02em; }
.escalon-texto { margin-top: 9px; font-size: 15px; line-height: 1.62; color: var(--tinta-media); max-width: 62ch; }
.escalon-tiempo {
  font-size: 11px; font-weight: 600; text-transform: uppercase;
  letter-spacing: 0.14em; color: var(--tinta-suave); text-align: right; padding-top: 7px;
}
.escalera-nota {
  margin-top: 40px; padding-top: 26px; border-top: 1px solid var(--linea);
  font-size: 15px; line-height: 1.62; color: var(--tinta-media); max-width: 68ch;
}
@media (max-width: 860px) {
  .escalera { padding: 84px 24px; }
  .escalon { grid-template-columns: 46px 1fr; gap: 18px; }
  .escalon-tiempo { grid-column: 2; text-align: left; padding-top: 10px; }
}
```

- [ ] **Step 5: Commit**

```bash
git add index.html sistema.css
git commit -m "feat(sitio): la escalera — seis escalones, sin precios"
```

---

### Task 7: Bloque "La prueba"

**Files:** Modify `index.html` (`<section class="resultados">`, id `#prueba`)

- [ ] **Step 1: Header**

Eyebrow **La prueba**. Título `Cinco auditorías nuestras.<br><em class="serif acento-verde">Las cinco encontraron algo.</em>`

- [ ] **Step 2: El bento** (reusa `.bento` / `.celda` / `.celda-num` / `.celda-label` / `.celda-texto`)

| Celda | Clase | Número | Label | Texto |
|---|---|---|---|---|
| 1 | `.celda-ancha .c-verde` | `$569.379.492` | mal imputados | Encontrados en **una hora y media** de consultas de solo lectura sobre una base de 98 tablas. Concesionaria de utilitarios |
| 2 | `.c-salvia` | `21 %` | en vez de 10,5 % | IVA de vehículos liquidado al doble durante años. El sistema lo permitía y nadie lo miraba |
| 3 | `.c-hueso` | `USD 60.000` | por año | Kilos que no se rendían y cobranzas sin saldo. Cafetería de especialidad |
| 4 | `.c-hoja` | `4` | sucursales, un mismo error | Códigos de artículo corruptos y saldos de caja sin cargar, en un sistema que parecía sano. Cadena de neumáticos |

- [ ] **Step 3: El pie del bloque**

`.celda-frase` o párrafo con filete:
> **No garantizamos el hallazgo. Garantizamos la medición.**

- [ ] **Step 4: Chequear la regla de cifras**

Ninguna cifra de este bloque puede venir del material de Sánchez De Boeck. Las cuatro son
de clientes de INFYN, sin nombre. Verificar contra el spec §7.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat(sitio): la prueba — cuatro hallazgos propios, clientes anonimizados"
```

---

### Task 8: Bloque "El final del camino" (sistema + Ciro)

**Files:** Modify `index.html` (`<section class="producto">`)

Los mockups (`.lamina`, `.app`, `.telefono`) **se conservan tal cual**. Cambia el encuadre:
Ciro deja de ser el diferencial de entrada y pasa a ser el destino.

- [ ] **Step 1: Header**

Eyebrow **El destino**. Título `El sistema es el final del camino.<br><em class="serif acento-verde">No el punto de partida.</em>`
Bajada: *Cuando la base está medida y el criterio está escrito, se construye: el sistema que
ordena la operación y* **Ciro, que responde sobre esa base.**

- [ ] **Step 2: La nota de Ciro** (`.nota-ciro`)

> Ciro no adivina. Cuando el dato no alcanza para responder, **lo dice** — y dice qué falta
> para poder responder.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat(sitio): Ciro pasa a ser el destino, no la entrada"
```

---

### Task 9: "Lo que no prometemos", quote, CTA y footer

**Files:** Modify `index.html`, `sistema.css`

- [ ] **Step 1: "Lo que no prometemos"** (sección nueva sobre `--crema`, reusa `.columnas`)

Eyebrow **Los límites**. Título `Lo que no prometemos.` Cuatro columnas:

1. **Un KPI que tu base no sostiene** — Ni en la reunión de venta. Si el dato no está, lo que
   se entrega es qué hay que cargar para que esté.
2. **El hallazgo** — Se garantiza la medición. En cinco corridas propias no hubo una sin
   hallazgo, pero eso es historia, no promesa.
3. **Un veredicto** — El puntaje no aprueba ni reprueba: **asigna horas**. Dice dónde
   trabajar primero y cuánto mueve la aguja cada arreglo.
4. **Que no tengamos sesgo** — Si auditamos un sistema que construimos nosotros, **se dice
   en la primera línea del informe**. Conocer el esquema es una ventaja y también un sesgo.

- [ ] **Step 2: Quote** (`.quote`)

```html
<p class="quote-texto">El problema no fue la decisión.<br><span>Fue enterarte tarde.</span></p>
```

- [ ] **Step 3: CTA** (`.cta`, id `#contacto`)

```html
<h2 class="cta-titulo">
  Contame la última decisión que tomaste tarde
  <span>porque te enteraste tarde.</span>
</h2>
<p class="cta-sub">
  Con eso arrancamos. Dos archivos y, entre tres y cinco días después, tenés el puntaje de
  tu base y un hallazgo con nombre. <strong>El alcance y el precio se arman sobre tu caso.</strong>
</p>
<a href="mailto:info@infynsolutions.com" class="btn btn-oscuro">Escribir a INFYN</a>
```

- [ ] **Step 4: Footer**

Sumar `Método` → `/auditoria` a `.footer-nav`. Sacar los links a `/diagnostico` y
`/ejemplos` si los tiene: quedaron con el discurso viejo.

- [ ] **Step 5: Commit**

```bash
git add index.html sistema.css
git commit -m "feat(sitio): límites, quote y CTA con la pregunta gate"
```

---

### Task 10: `auditoria.html` — la página del método

**Files:** Create `auditoria.html`

Misma estructura de `<head>` que `index.html` (fuentes + `<link rel="stylesheet" href="/sistema.css">`),
mismo nav y footer.

- [ ] **Step 1: `<head>` y hero**

```html
<title>El método — INFYN</title>
<meta name="description" content="Cuatro ejes, doce controles: cómo medimos la base de datos con la que tu negocio decide, qué entregamos y qué no prometemos.">
```

Hero (`.hero`): eyebrow **El método** · titular `Medimos la evidencia<br><em class="serif">con la que decidís.</em>`
· bajada: *Cuatro ejes, doce controles, el mismo orden en todos los clientes.* **Arranca con
dos archivos que tu contador ya tiene:** *el mayor y el plan de cuentas.*

- [ ] **Step 2: Los cuatro ejes en profundidad**

Un bloque por eje (alternando `--crema` y `--crema-hueso`), cada uno con cuatro partes:
**Qué mide** · **La pregunta que contesta** · **Un hallazgo real** · **Qué no puede decir**.

Los hallazgos reales por eje son los del Task 5 (campo de garantía con 0 filas · 62 ventas
sin cobro · rezago negativo · IVA al 21 %). Los "qué no puede decir":

- Aprovechamiento: *no dice si el campo vacío importa. Eso se decide con el negocio, campo por campo.*
- Cobertura: *no distingue sola la falla de la decisión tomada a conciencia. Se cierra preguntando.*
- Frescura: *no explica por qué hay rezago. Dice dónde y cuánto.*
- Veracidad: *sin un contador que lea el mayor, se acota a lo que se prueba sin salir del dato: stock físico, saldos reconocidos, unicidad de claves.*

- [ ] **Step 3: Las seis etapas**

Reusar `.paso` sobre `.metodo` (verde). Etapa · qué se hace · **el gate que hay que pasar**:

| Etapa | Qué se hace | El gate |
|---|---|---|
| 0 · Calificar | Tres preguntas al dueño: la decisión tardía y su costo, qué mira primero al abrir el día, de dónde saca la información | Sin decisión tardía cuantificada, no hay proyecto |
| 1 · Censar el origen | Todas las fuentes, formales e informales, cada una con su fecha de corte. Lo informal no se descarta: se normaliza o se declara fuera de alcance | El archivo real en mano, no su descripción |
| 2 · Auditar la evidencia | Los cuatro ejes, en orden: veracidad primero, después frescura, aprovechamiento y cobertura | Ninguna limitación al alcance sin escribir |
| 3 · Cargar el criterio | El formulario por puesto: qué mira cada área, con qué umbral y qué hace cuando se pasa | No se promete un indicador que la base no sostiene |
| 4 · Construir | Recién acá se escribe código, sobre lo que la auditoría priorizó | La tabla de prioridades, ordenada por cuánto mueve la aguja |
| 5 · Validar y entregar | Datos reales, referentes por área, acta de entrega | Nada se entrega contra datos de demo |

- [ ] **Step 4: Los entregables del Estado de Evidencia**

Lista de seis, con el quinto destacado (`.celda` `.c-verde` o filete propio):

1. La declaración del universo auditado — tablas, registros, fecha de corte, qué queda afuera y por qué.
2. Un informe por eje, con la evidencia de cada control.
3. La lámina resumen con los cuatro puntajes.
4. El puntaje global y qué significa en horas de trabajo.
5. **La lista escrita de lo que hoy no podés afirmar con tu base.** ← *La parte cara de esto
   no es el puntaje: es esta lista.*
6. La tabla de prioridades, ordenada por cuánto mueve la aguja cada arreglo.

- [ ] **Step 5: El conflicto declarado**

Bloque propio, sobre `--crema-hueso`, título `Auditamos sistemas que construimos nosotros.`
Texto: *Cuando pasa, se dice en la primera línea del informe. Tiene una ventaja —nadie conoce
el esquema como quien lo escribió— y tiene un sesgo. Si preferís, el eje de veracidad lo
valida tu contador.*

- [ ] **Step 6: FAQ** (las objeciones, textuales del material comercial)

- *"Mi contador ya audita."* → Tu contador audita los estados. Nosotros auditamos el dato con
  el que los arma. Son dos cosas distintas y la segunda casi nunca se hizo.
- *"¿Y si el puntaje me da mal?"* → El puntaje no aprueba ni reprueba: te dice cuántas horas
  hay que poner y dónde. Y si da mal, te ahorraste el proyecto que iba a fracasar.
- *"Es caro para un informe."* → No estás pagando el informe. Estás pagando la lista escrita
  de lo que hoy no podés afirmar con tus datos, y qué arreglar primero.
- *"Esto lo hago yo con IA."* → Corré el conteo de vacíos y te va a dar 87 %. El número real
  era 95,7. La diferencia es clasificar cada vacío con una razón de negocio al lado.
- *"Ahora no es el momento."* → Mientras tanto la fuga corre. Se puede empezar por la
  radiografía, que son dos archivos.

CSS del acordeón: usar `<details>`/`<summary>` nativos, sin JS.

```css
.faq details { border-top: 1px solid var(--linea); padding: 22px 0; }
.faq details:last-of-type { border-bottom: 1px solid var(--linea); }
.faq summary { cursor: pointer; font-size: 17px; font-weight: 500; list-style: none; }
.faq summary::-webkit-details-marker { display: none; }
.faq summary::after { content: '+'; float: right; color: var(--verde-hoja); font-weight: 400; }
.faq details[open] summary::after { content: '–'; }
.faq p { margin-top: 14px; font-size: 15px; line-height: 1.65; color: var(--tinta-media); max-width: 68ch; }
```

- [ ] **Step 7: CTA y footer** — los mismos de `index.html`.

- [ ] **Step 8: Verificar `cleanUrls`**

`http://localhost:8765/auditoria.html` tiene que renderizar completo. En producción la ruta
es `/auditoria` gracias a `vercel.json` — **ese archivo no se toca**.

- [ ] **Step 9: Commit**

```bash
git add auditoria.html sistema.css
git commit -m "feat(sitio): /auditoria — el método, las etapas y los límites"
```

---

### Task 11: Pasada de verificación

**Files:** los tres (`index.html`, `auditoria.html`, `sistema.css`)

- [ ] **Step 1: Cifras y nombres**

```bash
cd /Users/sofia/Projects/INFYN-sitio-evidencia
grep -n "55,8\|72,9\|42,8\|25,7\|Audit File\|sin costo\|gratis\|USD 1\.\|USD 2\." index.html auditoria.html
```
Esperado: **cero resultados.** Son las cifras de Sánchez De Boeck, el nombre viejo del
entregable y precios. Si aparece algo, se saca.

- [ ] **Step 2: SVG con color escrito a mano**

```bash
grep -n "rgba(23,64\|#17403A\|#2E6B5D\|#86B0A2" index.html auditoria.html
```
Esperado: cero. Todo color va por `var()` o `currentColor` desde `sistema.css`.

- [ ] **Step 3: Contraste**

Verificar los pares nuevos con un chequeador WCAG: `.escalon-tiempo` (tinta-suave sobre
crema-hueso), `.score-eje-label` (tinta-suave sobre crema), `.puerta-cierre` (tinta-media
sobre crema). Mínimo 4,5:1. En el rediseño de hoy apareció un par a 2,8:1 que estaba
fallando desde antes — se chequea siempre.

- [ ] **Step 4: Mobile**

390px: que no haya scroll horizontal, que el hero entre, que la escalera se lea en dos
columnas y que el bento pase a una sola.

- [ ] **Step 5: Links**

Que `Método`, `Cómo se avanza`, `La prueba` y `Contacto` lleguen a destino en las dos
páginas, y que ningún link apunte a `/diagnostico` ni a `/ejemplos`.

- [ ] **Step 6: Commit**

```bash
git add -A index.html auditoria.html sistema.css
git commit -m "fix(sitio): pasada de verificación — contraste, mobile y cifras propias"
```

---

### Task 12: `brand.md` y el nombre en el vault

**Files:** Modify `brand.md`; modificar las notas de INFYN en `/Users/sofia/Projects/segundo-cerebro`

- [ ] **Step 1: `brand.md`**

Sumar dos secciones: **Nombres de la escalera** (la tabla del spec §3, con la nota de que
*Audit File* es de Sánchez De Boeck y no se usa) y **Regla de cifras** (en el sitio van solo
cifras de clientes de INFYN, anonimizados).

- [ ] **Step 2: Renombrar en el vault**

```bash
cd /Users/sofia/Projects/segundo-cerebro
grep -rln "Audit File" --include="*.md" "Proyectos/" "Lecciones técnicas/"
```

En esos archivos, `Audit File` → `Estado de Evidencia`, **salvo** cuando la frase describe
el método de Sánchez De Boeck (ahí se aclara *"su Audit File"*). `Referencias/`, `Inbox/` y
`Bitácora/` **no se tocan**: son cita o registro histórico.

- [ ] **Step 3: Commit en los dos repos**

```bash
cd /Users/sofia/Projects/INFYN-sitio-evidencia
git add brand.md && git commit -m "docs(brand): nombres de la escalera y regla de cifras propias"

cd /Users/sofia/Projects/segundo-cerebro
git add "Proyectos/" "Lecciones técnicas/"
git commit -m "INFYN: el entregable se llama Estado de Evidencia (Audit File es de SdB)"
```

---

### Task 13: Merge y deploy

- [ ] **Step 1: Merge a main**

```bash
cd /Users/sofia/Projects/INFYN
git fetch --quiet && git merge --no-ff sitio/identidad-evidencia
```
`git fetch` primero, siempre: al repo `INFYNapp` pushea más gente y el remoto avanza solo.

- [ ] **Step 2: Deploy**

```bash
cd /Users/sofia/Projects/INFYN
vercel whoami   # tiene que decir sofiafbravo
vercel deploy --prod
```
`.vercelignore` tiene que seguir existiendo: es lo que evita que `marunails/` e `inventario/`
—código de cliente— se publiquen en infynsolutions.com.

- [ ] **Step 3: Verificar en producción**

Abrir https://infynsolutions.com y https://infynsolutions.com/auditoria en el browser real.
Chequear el fold, el bento y el mobile. El `/auditoria` sin `.html` es la prueba de que
`cleanUrls` sigue en pie.

- [ ] **Step 4: Limpiar el worktree**

Solo después de verificar en producción, y auditando antes:

```bash
cd /Users/sofia/Projects/INFYN
git fetch --quiet
git cherry -v origin/main sitio/identidad-evidencia   # todo tiene que dar "-"
git -C ../INFYN-sitio-evidencia status --short -uall  # tiene que dar vacío
git worktree remove ../INFYN-sitio-evidencia
git branch -d sitio/identidad-evidencia
```
