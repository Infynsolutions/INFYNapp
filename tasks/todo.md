# Sesión 2026-09-07 — Rediseño editorial del sitio

## Hecho
- [x] Cambiar la dirección visual de dark-first/SaaS a editorial/institucional (crema base + bloques verde macizo)
- [x] Nueva paleta: verde petróleo `#17403A`, medio `#21544C`, hoja `#2E6B5D`, salvia `#86B0A2`, crema `#E7E0CE`, hueso `#F2EFE7`
- [x] Eliminar aurora glow, grid de fondo, sombras difusas y verde neón `#2ED47A`
- [x] Tipografía: Inter 400–600 (saca Bricolage Grotesque) + Instrument Serif itálica como acento en la frase de cierre de cada bloque
- [x] Negritas de cuerpo en weight 600, con color por variable `--fuerte` según el fondo del bloque
- [x] Hero: saca el canvas animado y los badges flotantes; queda columna editorial + arco medido + barra de 3 datos
- [x] Ciro: mockup restilado en crema/verde mate, sin emojis, donut reemplazado por el panel "Lectura de Ciro"
- [x] Resultados: bento de 4 celdas con esquina cuarto de círculo
- [x] Capa de gráficos SVG: arco medido (hero), arco de ticks (quote), tres arcos concéntricos (método), sparkline / barras / línea de tiempo / onda (bento)
- [x] Logo: de `<img>` a `mask-image`, recortado al símbolo y en color de paleta
- [x] Contraste: `tinta-suave` de `#7A877F` a `#586764` (2,8:1 → 4,5:1). Todos los pares en uso pasan WCAG AA
- [x] Mobile: la lámina de escritorio se oculta bajo 860px, queda el teléfono
- [x] `brand.md` y `CLAUDE.md` reescritos con la dirección nueva
- [x] Verificado desktop 1440 y mobile 390, sin errores de consola, cero clases CSS huérfanas

## Pendiente
- [ ] **Deploy a producción** — el sitio en vivo (infynsolutions.com) sigue con el diseño anterior
- [ ] **`/diagnostico` y `/ejemplos` siguen con la estética vieja** (aurora + neón). Se nota el salto al navegar desde el CTA. 27KB y 65KB de HTML, es una sesión aparte
- [ ] Fotos reales: la sección Ciro y el bento aguantan el patrón media columna foto / media bloque de color, pero no hay assets de INFYN en el repo

## Review
Rediseño completo de `index.html`: 2511 → 1264 líneas, en tres pasadas con validación visual de Sofia entre cada una. Primera: cambio de dirección (paleta, tipografía, estructura). Segunda: serif itálica de acento, negritas de cuerpo y capa de gráficos, pedidos con referencias visuales. Tercera: el verde base al petróleo de la referencia.

Lo que hizo que saliera rápido fue preguntar tres decisiones antes de escribir una línea (base cromática, qué hacer con los elementos tech, sistema tipográfico) en vez de proponer una versión y rehacerla. Las tres pasadas siguientes fueron ajustes sobre esa base, no replanteos.

Dos bugs que solo aparecieron mirando: la negrita del hero en tinta oscura sobre verde (ilegible) y el SVG de fondo flotando en medio del texto porque `.celda > *` le pisó el `position`. Ninguno de los dos lo habría detectado leyendo el CSS. Lecciones en `tasks/lessons.md`.

---

# INFYN — Tareas en curso y review de sesiones

## Sesión 2026-05-11 — Rediseño completo (cerrada)

### Hecho
- [x] Audit UX/UI inicial del sitio (10 hallazgos críticos detectados)
- [x] Repositioning: "agencia que implementa y se queda" (hero, problema, modelo)
- [x] Modelo de 4 pasos → 3 capas (Diagnóstico → Sistema → Operación continua)
- [x] Pulso renombrado (era Argos) y posicionado como diferencial central
- [x] Pulso reemplaza al chart genérico en el hero
- [x] Chat de Pulso reescrito con preguntas estratégicas de director
- [x] Bloque problema reescrito con dolores del cliente (sin anti-positioning)
- [x] Tipografía: Bricolage Grotesque 800 (headlines) + Instrument Serif italic (.acento)
- [x] Hero asimétrico 1.2/0.8 + headline más grande + beam de luz diagonal
- [x] Verde acento reducido (eyebrows, hero-tag, paso-tiempo a neutro)
- [x] Corner marks `+` verde como signature decoración en secciones dark
- [x] Resultados con casos por industria anonimizados (+30% / −70% / 6 sem)
- [x] CTA con incentivo "diagnóstico se descuenta del proyecto"
- [x] Ambient chart de fondo detrás del Pulso card en hero (data 24/7)
- [x] Deploy a Vercel — live en infyn-web.vercel.app

### Review
La web pasó de SaaS dark genérica (Inter + chart + cards verdes simétricas) a editorial-tech distintiva (Bricolage 800 + acento serif italic + Pulso protagonista + corner marks + beam diagonal).

Cambio más importante: **Pulso pasó de mockup decorativo a diferencial central**. Esto cambia toda la narrativa — vendemos un co-pensador estratégico, no un dashboard. El chat en el hero comunica esto desde el primer segundo, sin que el visitante tenga que leer copy.

Cambio más sutil pero crítico: **el bloque problema sin anti-positioning**. Sofia notó que comparar contra competencia rompe conexión emocional. Los dolores del cliente (dependencia del dueño / datos en mil lugares / decisiones con miedo) mapean 1:1 a la solución y crean narrativa cerrada.

Cambio de mayor impacto visual: **la tipografía híbrida**. Sans heavy para autoridad + serif italic para signature editorial. Es lo que separa a INFYN del resto del mercado argentino (casi nadie usa serifs editoriales en agencias tech).

## Sesión 2026-05-22 — Git sync + Vercel fix (cerrada)

### Hecho
- [x] Commit y push de `index.html` + `.gitignore` al repo
- [x] Resolución de conflicto de merge (remote tenía copy actualizado: Ciro, headline reducido)
- [x] Fix cuenta Vercel: re-login como `sofiafbravo`, link a `sofiafbravos-projects/infyn-web`
- [x] Deploy exitoso a producción (infynsolutions.com)
- [x] Diagnóstico de `/ejemplos` → 404 por falta de cleanUrls
- [x] Agregado `vercel.json` con `cleanUrls: true`
- [x] Re-deploy y verificación: `/ejemplos` resuelve con 200

### Review
Sesión de mantenimiento/ops. El cambio más importante fue el `vercel.json` con `cleanUrls` — sin eso, el link del nav a `/ejemplos` daba 404 para todos los visitantes. También quedó fija la cuenta de Vercel para próximas sesiones.

## Sesión 2026-06-02 — Refinamiento del hero (cerrada)

### Hecho
- [x] Diagnóstico del hero actual (columna izq top-heavy, `.hero-sub` perdido en markup pero CSS huérfano, tarjeta compitiendo con titular)
- [x] Decisión de dirección: refinar y completar (no reinventar) — recomendado y aprobado
- [x] Subline recuperado en tono INFYN ("Convertimos el caos en sistema…") con max-width y ritmo
- [x] Barra fina de prueba al pie del fold (48–72hs · sin costo · 2–6 semanas) con punto verde acento por ítem
- [x] Ritmo vertical reequilibrado (headline → subline → CTAs → barra)
- [x] Headline un toque más grande (clamp tope 76→82px) para dominar el fold
- [x] Verificado desktop + mobile (390px) con screenshots
- [x] Deploy a producción (infynsolutions.com), READY, verificado en vivo

### Review
Sesión de refinamiento puntual del hero. El problema no era estético sino estructural: la columna izquierda quedaba vacía debajo de los botones y el subline se había perdido en un merge previo (el CSS lo seguía estilando). Se resolvió completando el bloque en vez de reinventarlo, respetando toda la intención acumulada (Bricolage+Instrument, aurora, corner marks, tarjeta Ciro, decisión de reducir verde). El acento verde volvió solo en los puntos de la barra de prueba — escasez intencional, no decoración. Gotcha capturado: revisar en local con server, no `file://` (logo roto / 404 falsos).

## Sesión 2026-06-02 — Ciro: re-scope de producto + design doc (cerrada)

### Hecho
- [x] Office-hours (YC product diagnostic) sobre Ciro a partir de `Diagnostico_Ciro.txt`
- [x] Re-scope: Ciro es el producto (sistema Ventas+Stock+Dashboard + asesor IA), no la capa de chat de Argos
- [x] Segmento fijado en ropa/calzado; Café Aruba descartado como primer usuario (gastronomía no calza)
- [x] Wedge elegido: el sistema armado, multi-tenant+RLS desde día uno (arquitectura completa, features angostas)
- [x] Ingesta definida: import de Excel flexible (mapeo asistido + cuarentena de filas) = camino crítico
- [x] Design doc escrito, revisado adversarialmente (9/14 issues) y **aprobado** (`~/.gstack/projects/sofiafbravo-infyn/sofia-main-design-20260602-092429.md`, supersede al de mayo)
- [x] Bitácora del producto creada en Obsidian (`Proyectos/INFYN/Ciro.md`)

### Pendiente (eng-review interrumpida en decisión 1)
- [ ] **Cerrar decisión 1:** modelo de datos de variantes (propuesto Product + ProductVariant, stock a nivel variante)
- [ ] **Cerrar decisión 2:** RPC atómico venta→StockMovement (propuesto plpgsql `registrar_venta()` vía supabase.rpc, tenant de auth.uid())
- [ ] **Cerrar decisión 3:** contrato de tool-calling de Ciro (funciones acotadas, tenant server-side, nunca SQL libre)
- [ ] **The assignment (antes de codear):** conseguir el Excel de ventas REAL de un dueño de ropa/calzado y ver si el import lo puede interpretar
- [ ] Reconciliar pricing ($12/$25 vs $35) para el producto Ciro
- [ ] **Bloqueantes duros:** crédito Anthropic API (el M1 quedó sin crédito) + upgrade Supabase Pro
- [ ] Abandonar/limpiar el backend viejo de Argos (`backend/` FastAPI) — stack nuevo es Next.js + Supabase

### Review
Sesión de definición de producto, sin código. El cambio de fondo: Ciro deja de ser "la capa de chat sobre Argos" y pasa a ser **el producto integral** (sistema + IA). La corrección más valiosa fue de segmento: el reflejo de elegir Café Aruba como primer cliente chocaba con el diagnóstico (ropa/calzado, variantes, temporada) — un café es otra operación. Sofia defendió con argumento construir la arquitectura multi-tenant completa desde el día uno (su stack default, costo marginal casi cero). Quedó claro que el riesgo del producto no es la IA ni la arquitectura, sino que el import de Excel sobreviva al Excel real de un comercio.

## Sesión 2026-06-21 — Copensador (tier Custom): spec + plan técnico (cerrada, sin código)

### Hecho
- [x] Autenticado NotebookLM (MCP) + registrado notebook "Auditoría Continua + IA Generativa (Sánchez De Boeck)"
- [x] Extraído el blueprint técnico del Compensador Estratégico del notebook (entrenamiento, XMLA/MCP, Power BI semántico, Claude Project)
- [x] Brainstorming: definido el Copensador como **producto del tier Custom** (≠ Ciro, que es el copiloto operativo del tier Estándar)
- [x] Sofia aportó su propio doc (`Plan_Copensador_Custom.docx`) — arquitectura en capas ya pensada
- [x] **Spec consolidado y aprobado** → `docs/superpowers/specs/2026-06-21-copensador-custom-design.md` (su doc + 5 fixes de review: SQL guardado, fase de validación, política doble moneda, centro `__global`, MODELO.md auto-generado)
- [x] **Plan de implementación escrito** (15 tasks TDD) → `docs/superpowers/plans/2026-06-21-copensador-custom.md` — pero apuntando al repo/stack EQUIVOCADO (INFYN/backend = copia de Argos, Python)
- [x] Corrección clave de Sofia: cada cliente Custom es **repo + base separados** (Café Aruba, Blue Motors), no tenants de Argos. Argos = multi-tenant para emprendedores chicos (Ciro)
- [x] Decisiones cerradas: stack **TS/Next.js** (largo plazo: matchea stack default, cero infra nueva por cliente, paquete TS futuro), reuso **plantilla ahora → paquete después**
- [x] Aterrizado a Café Aruba real: distribuidora de café por ruta; mapeadas las 3 lentes a sus tablas (`movements`, `cash_transactions`, `stock_purchases`, `client_balances`, etc.)

### Pendiente (retomar mañana)
- [ ] **Cerrar decisión keystone:** eje conformado para Café Aruba — vendedor/ruta (recomendado, único presente en las 3 lentes) vs zona vs producto. Sofia frenó antes de elegir.
- [ ] **Reescribir el plan de implementación** apuntando a `Cafe Aruba/` en TS/Next.js, sin `tenant_id`, con vistas sobre las tablas reales (el SQL es agnóstico al lenguaje y se reusa; solo se reescribe la capa del agente)
- [ ] Definir política de tipo de cambio (MEP) para Café Aruba (flujos point-in-time, patrimonial revaluado a cierre)
- [ ] Agregar `@anthropic-ai/sdk` + driver Postgres read-only (`postgres`/`pg`) a Café Aruba
- [ ] Crear rol `copensador_ro` en la Supabase de Café Aruba (solo lectura, solo schema analytics)
- [ ] Más adelante: superficie de entrega UI (vista "Copensador" con render de las 3 lentes + mapa)

### Review
Sesión 100% de diseño, sin código. El valor: separar dos productos que se confundían — **Ciro** (operativo, tier Estándar, Argos multi-tenant) y **Copensador** (estratégico, tier Custom, repos/bases por cliente). El spec quedó sólido (capas Kimball: dims conformadas → vistas de dominio → mart integrado → capa semántica → agente read-only). El plan se escribió dos veces sobre supuestos equivocados de repo/stack porque no verifiqué DÓNDE vive el código antes de planear — corregido cuando Sofia aclaró la separación de proyectos. Quedó listo para reescribir el plan mañana contra Café Aruba real, faltando solo elegir el eje keystone.

## Backlog (próximas sesiones)

- [ ] WhatsApp como escalón blando además de "agendar diagnóstico"
- [ ] Animaciones de scroll-trigger: entrada con stagger en secciones
- [ ] Sumar Café Aruba como caso con nombre (cuando haya permiso del cliente)
- [ ] Posible landing dedicada a Pulso/Ciro si se quiere llevarlo como producto comprable
- [ ] Considerar segunda línea de data en el ambient chart para más densidad
- [ ] Auditar si el footer necesita información de contacto/email visible
