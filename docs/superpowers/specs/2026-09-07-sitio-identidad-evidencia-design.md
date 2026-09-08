# Sitio INFYN — identidad nueva: la evidencia primero

**Fecha:** 2026-09-07 · **Estado:** spec, pendiente de aprobación de Sofia
**Repo:** `INFYN` · rama `sitio/identidad-evidencia` · worktree `../INFYN-sitio-evidencia`

---

## 1. El problema

La piel del sitio ya es la nueva (rediseño editorial de hoy: crema `#E7E0CE`, petróleo
`#17403A`, Inter 400–600 + Instrument Serif itálica). **El contenido todavía es el viejo.**

La home vende *"agencia que implementa y se queda"* → tres capas → Ciro → resultados.
La identidad que quedó escrita esta semana es otra: el activo central de INFYN es el
**método de auditoría de la evidencia** — cuatro ejes, doce controles, un catálogo de
18 controles con hallazgo real, cinco corridas propias que encontraron algo las cinco
veces. Nada de eso está en el sitio.

## 2. La decisión de posicionamiento

**Dos puertas, un solo pasillo.** El visitante llega por una de dos situaciones, pero
las dos desembocan en la misma secuencia.

> Primero medimos con qué decidís. Después construimos lo que falta.

La auditoría es **el paso inicial, no el final del negocio**: el sistema a medida sigue
siendo el destino y la suscripción sigue siendo el modelo. Lo que cambia es qué se pone
adelante: una **radiografía con evidencia** en vez de una conversación de descubrimiento
sin nada medido. No se regala nada — la radiografía se cobra como todo lo demás, y por
eso tiene que llegar con un hallazgo adentro.

La formulación que sostiene el posicionamiento sin traicionar el *"no somos consultora"*:

> No hacemos un informe y nos vamos. Medimos la evidencia con la que decidís, te decimos
> qué podés afirmar y qué no, y después construimos lo que falta. La auditoría no es el
> producto: es el gate técnico que decide si se puede construir algo encima.

## 3. Nombres

`Audit File` es de Antonio Sánchez De Boeck y no se usa. En `Referencias/` del vault se
mantiene como cita de **su** método; en las notas de INFYN se renombra.

| Escalón | Nombre nuevo | Antes | Duración |
|---|---|---|---|
| 0 | **Radiografía** | (igual) | 3 a 5 días · dos archivos |
| 0+ | **Primera pasada** | Auditoría Express | medio día |
| 1 | **Estado de Evidencia** | Audit File | 2 semanas |
| 2 | **Mapa de criterio** | (igual) | 2 a 3 semanas |
| 3 | **Copensador** | (igual) | fee + suscripción |
| 4 | **Estado mensual** | Auditoría recurrente | dentro de la suscripción |

*Estado de Evidencia* calca la forma de "estado de resultados": una foto formal con fecha
de corte, que se re-emite por período. Por eso el escalón 4 es **Estado mensual** y no
necesita nombre nuevo — es el mismo documento, otra vez.

Descartados por colisión con vocabulario propio ya en uso: *Expediente* (es el estado
compartido del pipeline `/cliente-*`) y *Acta* (es el Acta de Entrega).

## 4. Alcance

**Entra:** `index.html` rehecha entera + `auditoria.html` nueva.
**No entra:** `/diagnostico` y `/ejemplos` (quedan con la estética y el discurso viejos;
el CTA deja de apuntarles) · fotos reales (no hay assets en el repo) · backend.

## 5. Estructura de la home

| # | Bloque | Contenido |
|---|---|---|
| 1 | Nav | Método · Servicios · Casos · Contacto |
| 2 | Hero | *Primero medimos con qué decidís.* / **Después construimos lo que falta.** Visual: lámina de los cuatro ejes con puntaje → el sistema. Barra al pie del fold: dos archivos · 3 a 5 días · un hallazgo con nombre |
| 3 | Las dos puertas | A — *"Ya tenés un sistema y no sabés si podés confiar en lo que te dice."* B — *"Todavía no tenés sistema: la operación vive en Excel y en la cabeza de tres personas."* Cierre: **las dos puertas dan al mismo pasillo** |
| 4 | El problema | *No es que no tengas datos.* / **Es que nadie te dijo nunca cuánto valen los que tenés.** Ancla: 87,2 % contra 95,7 % sobre el mismo dato |
| 5 | Los cuatro ejes | Aprovechamiento · Cobertura · Frescura · Veracidad, cada uno con su pregunta en lenguaje de dueño (ver §6) + gráfico SVG plano |
| 6 | La escalera | Los seis escalones de §3 con duración y entregable. Se lee que auditar es el escalón 1 |
| 7 | La prueba | Cuatro hallazgos reales anonimizados con su cifra (ver §7) |
| 8 | El final del camino | El sistema a medida + Ciro. *Ciro responde sobre la base que ya medimos* |
| 9 | Lo que no prometemos | Las cuatro reglas de §8. Es el bloque que compra confianza |
| 10 | Quote | *El problema no fue la decisión. Fue enterarte tarde.* |
| 11 | CTA | La pregunta gate + botón a la Radiografía. Sin precio: *el alcance se arma sobre tu negocio* |
| 12 | Footer | (se conserva) |

## 6. Los cuatro ejes, en lenguaje de dueño

| Eje | La pregunta que le hacemos al dueño |
|---|---|
| **Aprovechamiento** | ¿Cuánto de lo que tu sistema pide se está cargando de verdad? |
| **Cobertura** | De todo lo que pasó en el negocio, ¿cuánto quedó registrado? |
| **Frescura** | ¿Cuánto tarda un hecho en aparecer en el sistema? ¿Y qué aparece antes de pasar? |
| **Veracidad** | Si te señalo un número de tu balance, ¿podés justificarlo hasta el asiento? |

## 7. La prueba

Cuatro tarjetas, cliente anonimizado y cifra real:

1. **Concesionaria de utilitarios** — IVA de vehículos liquidado al 21 % en vez de 10,5 %,
   durante años.
2. **Concesionaria de utilitarios** — $569.379.492 mal imputados, encontrados en una hora
   y media de consultas de solo lectura sobre una base de 98 tablas.
3. **Cafetería de especialidad** — ~USD 60.000 al año entre kilos que no se rendían y
   cobranzas sin saldo.
4. **Cadena de neumáticos, cuatro sucursales** — códigos de artículo corruptos y saldos de
   caja sin cargar, en un sistema que parecía sano.

Pie del bloque: *cinco auditorías corridas sobre bases propias; las cinco encontraron algo
material.*

> **Regla dura de contenido:** en el sitio van **solo cifras propias de INFYN**. Los números
> del material de Sánchez De Boeck (el 55,8 % de venta anónima, los $72,9 M del contrafáctico
> del shopping, los márgenes 42,8 / 25,7) son suyos y **no se publican como casos nuestros**.
> Misma razón por la que se cambia *Audit File*. Por eso también se descarta su frase
> *"un informe no tiene que ser una autopsia"* y el bloque 10 lleva una línea propia.

## 8. Lo que no prometemos

- No prometemos un KPI que tu base no sostiene. Ni en la reunión.
- No garantizamos el hallazgo. Garantizamos la medición.
- El score no aprueba ni reprueba: **asigna horas**.
- Si auditamos un sistema que construimos nosotros, se dice en la primera línea del informe.

## 9. `/auditoria` — la página del método

1. Hero del método + el input mínimo (dos archivos: mayor contable y plan de cuentas).
2. Los cuatro ejes en profundidad: qué mide · qué contesta · un hallazgo real · **qué no
   puede decir**.
3. Las seis etapas con su gate, en versión cliente.
4. Los seis entregables del Estado de Evidencia, con el #5 destacado: *"la parte cara no es
   el puntaje, es la lista escrita de lo que hoy no podés afirmar"*.
5. El conflicto declarado (auditamos lo que construimos) como argumento, no como nota al pie.
6. Las objeciones como FAQ.
7. CTA a la Radiografía.

## 10. Precio y qué se ofrece — decisiones tomadas

1. **Todo se cobra. No hay escalón gratis.** Decisión de Sofia del 2026-09-07: cierra la
   pendiente que la nota del servicio dejaba abierta (*"si la Radiografía va gratis o
   arranca paga"*) a favor de paga. La radiografía se cobra igual que el resto y por eso
   tiene que llegar con un hallazgo adentro, no con un puntaje solo.
2. **No se publica ningún precio, en ninguna página.** Ni bandas, ni "desde", ni "sin
   costo". El sitio muestra **duración y entregable**; el número sale de la conversación,
   porque el plan se arma sobre cada negocio. La página lo dice de frente —
   *el alcance y el precio se arman sobre tu caso* — para que se lea como criterio y no
   como evasiva.
3. **La entrada es la Radiografía o la Primera pasada.** Son las dos que ya están probadas
   (cinco corridas informales; una hora y media dio nueve hallazgos). El Estado de
   Evidencia y el Mapa de criterio se muestran **como el camino**, sin pedir compra, hasta
   que corra el Ejemplo 0 sobre Bestani. La nota del servicio lo pide textual: *"vender un
   servicio que nunca se corrió entero es cómo se rompe la relación con el primer cliente
   que lo compre."*
4. **El gate de entrada se mantiene** — la decisión tardía cuantificada. Ya no protege
   horas regaladas; ahora califica que haya negocio antes de cotizar.

## 11. Restricciones técnicas

- HTML + CSS puro, sin build ni dependencias. El sistema de diseño sale de `index.html` a
  un `sistema.css` compartido por `index.html` y `auditoria.html`: la página nueva no
  puede derivar como derivaron `/diagnostico` y `/ejemplos`, que copiaron el CSS y quedaron
  atrás. `vercel.json` con `cleanUrls: true` **no se toca** (es lo que hace andar `/auditoria`).
- Sistema visual de `brand.md` **sin tocar tokens**: crema base, bloques macizos petróleo,
  salvia de acento, Inter 400–600, nunca 700/800, serif itálica una frase por bloque.
- Los SVG nuevos usan `currentColor` / `var(--token)`. Nunca `rgba()` con el color escrito:
  es lo que dejó 419 ocurrencias que había que reemplazar a mano en el rediseño de hoy.
- `strong` toma color de `var(--fuerte)` definido **por bloque**, no de un selector listado.
- Cada par color/fondo nuevo se verifica contra WCAG AA antes de quedar.
- Se reusa la capa de gráficos SVG ya construida (arco medido, arco de ticks, arcos
  concéntricos, sparkline, barras, línea de tiempo, onda).
- Verificación: `python3 -m http.server` en local (no `file://`, rompe el logo y los
  `cleanUrls`), revisión visual desktop + mobile antes de cada pasada siguiente.

## 12. Fuera del sitio, pero parte del cambio

Renombrar `Audit File` → `Estado de Evidencia` en las notas de INFYN del vault
(`Auditoría de negocio — el servicio`, `Auditoría de la evidencia — método propio`,
`Metodología Copensador`, `Casos base del método`, `INFYN.md`, `Copensador.md`, las notas
de Bestani y las lecciones técnicas que lo citan). **`Referencias/` no se toca.**

## 13. Riesgos

| Riesgo | Mitigación |
|---|---|
| Publicar la escalera entera es vender algo que no se corrió completo | Solo Radiografía y Primera pasada tienen botón (§10.1) |
| Usar material de SdB como propio | Regla dura de §7; nombre propio en §3 |
| El sitio promete auditoría contable que INFYN no puede firmar | "Lo que no prometemos" (§8) y el eje 04 acotado a lo que se verifica sin contador |
| `/diagnostico` y `/ejemplos` quedan viejos y se nota el salto | El CTA deja de apuntarles; quedan en backlog explícito |
| Un sitio sin precios se lee como "no lo quieren decir" | Se dice de frente por qué: el plan se arma sobre cada negocio. Y la duración de cada escalón sí está publicada, que es lo que ordena la expectativa |
