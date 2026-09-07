# INFYN — Lecciones de proyecto

Lista de aprendizajes acumulados sesión a sesión. Revisar al inicio de cada sesión nueva.

---

## Marketing y copy

### Regla: No anti-positioning de competencia en la web pública
- **Por qué:** Sofia rechazó la versión con cards "Consultores que no ejecutan / Software factories que se van / Sistemas genéricos que no calzan". Quiere foco en dolores del cliente, no comparación con otros proveedores. El cliente PyME quiere sentirse entendido, no escuchar del mercado.
- **Cuándo aplica:** Toda copy de cara al cliente (web, landings, ads). El anti-positioning queda reservado para conversaciones uno-a-uno y materiales internos.

### Regla: Pulso vende preguntas estratégicas, no operativas
- **Por qué:** Las preguntas tipo "¿cómo cerré febrero comparado con enero?" hacen ver a Pulso como un dashboard más. Las preguntas tipo "¿conviene invertir $500K en una segunda sucursal?" o "¿cuál es mi cliente más rentable?" comunican co-pensador estratégico — categoría nueva. Es lo que un dueño piensa a las 11 PM y nadie le responde.
- **Cuándo aplica:** Cualquier mockup o copy de Pulso debe mostrar preguntas de director/dueño, no de empleado operativo.

### Regla: Positioning de INFYN = "agencia que implementa y se queda"
- **Por qué:** El gap real del mercado argentino (consultoras no ejecutan, software factories se van, SaaS genéricos no calzan) define la categoría que ocupa INFYN. Esto es la base de toda la comunicación, no solo una frase de pitch.
- **Cuándo aplica:** Siempre que se decida copy, mensajes, ads o materiales nuevos. El modelo de 3 capas (diagnóstico → sistema a medida → operación continua/retainer) es la IP del negocio.

---

## Diseño visual

### Regla: Tipografía B2B tech = peso primero, elegancia después
- **Por qué:** Probamos Instrument Serif sola (peso 400 regular) y se sintió "liviana, casi invitación de boda" para una agencia que vende IA + retainer + autoridad técnica. La fragilidad transmite lo opuesto al posicionamiento. Solución que funcionó: Bricolage Grotesque 800 (sans display con peso) para headline base + Instrument Serif italic solo en `.acento` (signature editorial).
- **Cuándo aplica:** Cualquier headline o título principal en cualquier landing/material. Mantener el contraste sans heavy + serif italic como signature.

### Regla: Si algo se siente "genérico", comparar contra referencias del sector
- **Por qué:** Cuando Sofia dijo "siento que falta más impacto, es una web genérica", la solución no era una intuición de diseñador — era investigar 6 sitios del sector (Linear, Vercel, Anthropic, Resend, Stripe, Cursor) y mapear gaps específicos (tipografía sin personalidad, headline no domina el fold, aurora muy sutil, hero simétrico predecible, verde overused).
- **Cuándo aplica:** Antes de proponer cambios visuales subjetivos. La comparación contra referencias da insights concretos en vez de opiniones.

### Regla: Verde acento de marca con criterio de escasez
- **Por qué:** El verde acento (`#2ED47A`) aparecía en ~8 lugares (eyebrows, .acento, botones, paso-num, paso-tiempo, hero-tag, live-dots, cards). Cuando todo es verde, nada es verde. Reducirlo a 3-4 lugares clave (botón primario, .acento italic, aurora background, live signals) hace que cada aparición se sienta intencional.
- **Cuándo aplica:** Al sumar elementos nuevos, preguntarse: "¿este lugar NECESITA verde acento o sirve con neutro?". Default a neutro, verde solo cuando es decisión consciente.


### Regla: la estética del sitio es editorial/institucional, no tech (2026-09-07)
- **Por qué:** Sofia pidió que la web aplicara a PyMEs tradicionales. La estética anterior (dark-first `#060D09`, neón `#2ED47A`, aurora glow, chart animado, emojis, mockup de app) leía como producto SaaS. La dirección nueva es crema `#E7E0CE` de base + bloques macizos verde petróleo `#17403A` + acento salvia, tipografía neutra 400–600, filetes en vez de cards, cero sombras.
- **Cuándo aplica:** Todo material visual de INFYN — web, landings, propuestas, PDFs. Antes de agregar un efecto, preguntarse si un estudio contable lo pondría en su pared.

### Regla: el verde base es petróleo, no oliva — y la escala se recalibra entera
- **Por qué:** `#12281F` (oliva oscuro) leía "eco"; `#17403A` tiene azul adentro y lee institucional. Al mover el base hay que recalibrar medio/hoja/salvia sobre el mismo matiz o la jerarquía se aplana (el verde medio queda igual al base).
- **Cuándo aplica:** Cualquier cambio de color de marca. Y verificar contraste después: al hacerlo se descubrió que `tinta-suave` a 11px daba 2,8:1 y fallaba WCAG AA desde antes.

### Regla: los SVG inline con colores hardcodeados no siguen a los tokens
- **Por qué:** El cambio de paleta dejó 419 `rgba()` con el verde viejo dentro de los gráficos SVG. Los tokens CSS cambiaron y los gráficos no.
- **Cuándo aplica:** Al generar SVG inline, o se usa `currentColor`/`var(--token)`, o se acepta que el cambio de paleta es un reemplazo global sobre el archivo.

### Regla: el color de `strong` sale de una variable por bloque, no de una lista de selectores
- **Por qué:** `strong { color: var(--tinta) }` dejó la negrita del hero en tinta oscura sobre fondo verde, ilegible. Listar selectores (`.sobre-verde strong, .paso-texto strong…`) se rompe con cada bloque nuevo. La solución: `strong { color: var(--fuerte, var(--tinta)) }` y cada bloque define `--fuerte` según su fondo.
- **Cuándo aplica:** Cualquier estilo que dependa del fondo del contenedor (negritas, links, bordes) en un sitio que alterna claro y oscuro.

### Regla: los gráficos no van detrás de párrafos
- **Por qué:** La onda de líneas arrancó como fondo de la celda `+30%` y competía con la lectura del texto. Movida a la celda que tenía aire, funciona como textura de marca.
- **Cuándo aplica:** Todo gráfico decorativo. Va en el espacio vacío de la composición, no debajo de contenido que hay que leer.

### Regla: serif de acento + grotesk necesita ajuste de tamaño
- **Por qué:** Instrument Serif itálica tiene menor altura x que Inter: al mismo `font-size` parece hundida dentro del titular. Va a `1.06em`.
- **Cuándo aplica:** Cualquier mezcla de dos familias en una misma línea de texto.

### Regla: los titulares llevan `<br>` explícitos
- **Por qué:** El quiebre automático dejó palabras huérfanas ("crecer." y "24/7." solas en una línea) y arruinó la composición en tres secciones distintas.
- **Cuándo aplica:** Todo titular de más de una línea. El ancho de columna sugiere, el `<br>` decide.

### Regla: un PNG monocromo con alpha se recolorea con `mask-image`, no se re-exporta
- **Por qué:** El logo es blanco puro y trae su propio wordmark debajo del símbolo, que duplicaba el "INFYN" en Inter. Con `mask-image` + `background: var(--crema)` toma el color exacto de la paleta, y con `mask-size`/`mask-position` se recorta solo el símbolo. Sin tocar el asset.
- **Cuándo aplica:** Logos e íconos monocromos que tienen que adaptarse a varios fondos.

### Regla: `.contenedor > *` pisa el `position` de los hijos decorativos
- **Por qué:** `.celda > * { position: relative; z-index: 1 }` (puesto para que el texto quede sobre el grano) anuló el `position: absolute` del SVG de fondo, que apareció flotando en el medio del texto.
- **Cuándo aplica:** Al usar el patrón "hijos por encima del fondo", acotar el selector al tipo de hijo real (`> div`) o excluir el decorativo.

---

## Workflow

### Regla: Pivots grandes se validan con preguntas concretas antes de tocar código
- **Por qué:** Al repositionar INFYN de "consultora pura" a "agencia híbrida con Pulso", se hicieron 4 preguntas concretas (servicio hero, role de Pulso, pricing público, casos) antes de implementar. Esto evitó rehacer trabajo y permitió a Sofia tomar decisiones de negocio en vez de aprobar implementaciones.
- **Cuándo aplica:** Cuando un cambio toca el posicionamiento o copy estructural. AskUserQuestion antes de Edit.

### Regla: Deployar siempre al terminar cambios visuales
- **Por qué:** Sofia valida en su browser real (Chrome, retina, su resolución). Los screenshots locales son aproximaciones — el feedback útil viene de ver en producción.
- **Cuándo aplica:** Siempre después de cambios al sitio. `vercel --prod` y avisar la URL.

### Regla: Verificar `vercel whoami` antes de deployar
- **Por qué:** El CLI puede quedar logueado con una cuenta incorrecta (contacto-9286 en vez de sofiafbravo). El proyecto `infyn-web` vive en `sofiafbravos-projects`. Si el `orgId` en `.vercel/project.json` no matchea la cuenta activa, el deploy falla o va al proyecto equivocado.
- **Cuándo aplica:** Al inicio de cualquier sesión que incluya deploy. Si `vercel whoami` no dice `sofiafbravo`, hacer `vercel logout` + `vercel login` + `vercel link --project infyn-web --scope sofiafbravos-projects --yes`.

### Regla: `cleanUrls: true` en vercel.json para rutas sin extensión
- **Por qué:** Sin esta config, Vercel sirve `ejemplos.html` en `/ejemplos.html` pero devuelve 404 en `/ejemplos`. El nav linkea a `/ejemplos`, así que sin `cleanUrls` la página es inaccesible desde el sitio.
- **Cuándo aplica:** Cualquier página nueva que se agregue al proyecto (diagnostico.html, ejemplos.html, etc.). El `vercel.json` ya tiene `cleanUrls: true` desde 2026-05-22, no volver a sacarlo.

### Regla: En conflictos de merge, si el remote es la verdad, usar `git checkout --theirs`
- **Por qué:** Al hacer pull con conflictos en `index.html` (20+ marcadores), resolver a mano es lento y propenso a errores. Si Sofia confirma que el remote es la versión correcta, `git checkout --theirs <archivo>` resuelve todo en un comando.
- **Cuándo aplica:** Cuando hay conflictos y el usuario dice "lo que vale es lo del github" o equivalente.

### Regla: El "cliente que ya tengo" no es por defecto el primer usuario — validar que calce con el segmento
- **Por qué:** Al definir Ciro (segmento ropa/calzado: variantes talle/color, estacionalidad), el reflejo fue elegir Café Aruba como primer cliente porque es el cliente pago que ya existe. Pero un café es otra operación (merma, costo de receta, ventas por franja horaria) y rompe el modelo de datos. La comodidad de "el cliente que tengo a mano" desvía el producto hacia el rubro equivocado.
- **Cuándo aplica:** Al elegir el primer usuario/piloto de un producto. Chequear que su operación calce con el modelo de datos y las preguntas core antes de adoptarlo como caso real. Si no calza, es un test mal calzado, no el primer usuario.

### Regla: Multi-tenant + RLS desde el día uno cuando es el stack default (arquitectura completa, features angostas)
- **Por qué:** Para un producto SaaS que se vende a escala, separar "arquitectura completa" de "alcance de features" evita re-trabajo. El multi-tenant + RLS es el stack default de Sofia (Supabase Variante A) → costo marginal casi cero hacerlo bien desde el inicio. La regla NO es "construí todo": es fundación completa + features mínimas. Confundir "buena arquitectura" con "todas las features" es lo que hunde meses antes de cobrar.
- **Cuándo aplica:** Producto SaaS greenfield propio que se vende a muchos. Invertir tiempo de diseño en los cimientos (aislamiento de tenant, RLS) sí; inflar el set de features no.

### Regla: Para revisar en local idéntico a prod, levantar un server (no abrir con `file://`)
- **Por qué:** El logo usa ruta absoluta (`<img src="/Logo Infyn.png">`) y `vercel.json` tiene `cleanUrls`. Abriendo el `index.html` directo (protocolo `file://`) el logo se ve roto y las rutas absolutas/`/ejemplos` no resuelven — parece un bug del sitio cuando no lo es. Levantando `python3 -m http.server 8000` desde la carpeta del proyecto y abriendo `http://localhost:8000`, las rutas absolutas resuelven igual que en Vercel.
- **Cuándo aplica:** Cuando Sofia quiere ver cambios en local antes de deployar. Nunca diagnosticar "logo roto / 404" sobre un render `file://`.

### Regla: Verificar DÓNDE vive el código (repo + stack) antes de escribir un plan de implementación
- **Por qué:** En la sesión del Copensador escribí el plan dos veces sobre supuestos equivocados: primero apuntando a `INFYN/backend` (que resultó ser una copia vieja de Argos), asumiendo además multi-tenant y Python. La realidad: cada cliente Custom es un repo y una base separados, y el piloto (Café Aruba) es Next.js/TS, no Python. Planear sobre el repo equivocado tira a la basura el detalle del plan.
- **Cuándo aplica:** Antes de redactar cualquier plan de implementación. Confirmar 1) en qué carpeta/repo concreto vive el código objetivo, 2) su stack real (leer package.json / schema), 3) si es multi-tenant o single-tenant. No asumir que el repo del cwd es el destino.

### Regla: Multi-tenancy ≠ reuso entre clientes Custom — son cosas distintas
- **Por qué:** Argos es multi-tenant (un código, una base, muchos tenants) y sirve a emprendedores chicos (Ciro). Los proyectos Custom (Café Aruba, Blue Motors) son repos y bases separados. El reuso entre ellos NO se logra con multi-tenancy, sino con plantillas (SQL agnóstico al lenguaje + código del agente) que se copian/adaptan, y eventualmente un paquete compartido. Mezclar ambos conceptos lleva a meter clientes Custom como tenants de Argos, que es el modelo equivocado.
- **Cuándo aplica:** Al diseñar la reutilización de una capa (como el Copensador) entre varios proyectos cliente. Separar "un servicio multi-tenant" de "una plantilla/paquete que cada proyecto instancia". Default: plantilla ahora, paquete cuando aparezca el 2º caso real (YAGNI).

### Regla: Distinguir Ciro (operativo, tier Estándar) del Copensador (estratégico, tier Custom)
- **Por qué:** Comparten stack (Claude API + Supabase) pero son productos distintos. Ciro = copiloto operativo del día a día para el emprendedor chico, sobre Argos multi-tenant. Copensador = análisis estratégico profundo (cruce económico/financiero/patrimonial sobre dims conformadas) para la dirección de un negocio Custom, en su repo y base propios. No mezclar: el Copensador solo es viable cuando INFYN diseña/controla el esquema desde el modelado.
- **Cuándo aplica:** Cualquier decisión sobre dónde vive una capa de IA en el ecosistema INFYN. Preguntar primero: ¿es operativo o estratégico? ¿tier Estándar (Argos) o Custom (repo del cliente)?

### Regla: `python3 -m http.server` cachea — verificar con `?v=timestamp`
- **Por qué:** Tres screenshots seguidos mostraron el diseño viejo después de editar el archivo, y llevó a "arreglar" cosas que ya estaban bien.
- **Cuándo aplica:** Toda verificación visual sobre servidor local. Navegar a `index.html?v=$(date +%s)` en vez de recargar.

### Regla: los `*.png` están gitignored — el logo llega a prod por el deploy, no por git
- **Por qué:** `.gitignore` excluye `*.png`, así que `Logo Infyn.png` no está en el repo. En un worktree limpio el logo da 404 y parece un bug del rediseño. En producción funciona porque Vercel deploya desde la carpeta local.
- **Cuándo aplica:** Al trabajar en un worktree o clon nuevo, copiar los assets ignorados antes de verificar visualmente. Si alguna vez se deploya desde git, el logo degrada al wordmark de texto.

