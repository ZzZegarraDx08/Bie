# Análisis: canal de clips de GTA 6 con agentes de IA

Fuente: 7 capturas compartidas el 2026-11-18. Son **tres documentos distintos** que describen el mismo negocio con distinto nivel de cautela:

| # | Documento | Qué es | Tono |
|---|-----------|--------|------|
| A | "the grok bot gta 6 prompt" (1 imagen) | Prompt maestro de un pipeline 100 % automático: buscar, editar y publicar a diario | Agresivo: "estoy fuera, decide tú y sigue" |
| B | "GTA 6 Clipping: Setup + Launch Prompt" (@E1Farhan, 1 imagen, "page 1/2") | Prompt de estratega: cuentas, campañas pagadas de clipping, tracker de pagos | Conservador: solo material con permiso, no inventar |
| C | "make money from gta 6 with ai agents" (5 imágenes, prompts 1–9) | Guía paso a paso: setup → outliers → miniaturas → clips → episodio → verticales → video propio → revisión → publicar | Intermedio: "publica solo lo que yo apruebe" |

> Nota: B dice "page 1/2". Falta la página 2.

---

## 1. El pipeline unificado (lo que los tres comparten)

```
pull → score → download → edit → vertical → critic → publish → report
```

1. **Setup** (A, C1): instalar `ffmpeg`, `yt-dlp`, `faster-whisper`, `scenedetect`/`opencv`. Conectar YouTube, Instagram, Apify y upload-post (TikTok), vía Composio. Las claves **nunca** en el chat ni en archivos.
2. **Memoria persistente** (A, C1): `STATUS.md` (qué corrió, qué está en cola, qué falló) y `RULES.md` (la barra de estilo medida). Se leen al empezar cada ejecución porque el ordenador se reinicia.
3. **Estudio de referencia** (A `<study>`, C2–C3): bajar ~10 episodios de canales de clips reales y medir duración de clip, cortes por minuto, duración de intro, plano más largo, posición del handle, estilo de subtítulos, nivel de música. Las **medianas** van a `RULES.md`. Detectar *outliers* (vídeos que superan de largo la media de su canal) → `outliers.csv` → patrones de títulos/miniaturas → `THUMBNAILS.md`.
4. **Búsqueda de clips** (A `<sources>`, C4): top de las últimas 24 h en Twitch, Kick y YouTube Live (C añade TikTok). Actor de Apify `omkar-cloud/twitch-clips-scraper`, Twitch Helix de respaldo. **Ranking por velocidad** = vistas ÷ horas de antigüedad.
5. **Episodio largo** (A `<edit>`, C5): sin intro; 10–20 min, 15–30 clips de 5–25 s; abre con uno de los 3 mejores y guarda un payoff para el final; alternar intensidad; etiqueta de contexto de una línea por clip; handle arriba-izquierda, logo abajo-derecha; −14 LUFS; mid-rolls solo entre clips.
6. **Verticales** (A `<vertical>`, C6): 3–5 al día, 15–40 s, 1080×1920; facecam arriba / gameplay abajo (40/60); primer fotograma = payoff; subtítulos palabra por palabra en la costura, nada en el 15 % inferior.
7. **Revisión "gauntlet"** (A `<critic_loop>`, C8): un agente **nuevo** que no ha visto tus notas juzga cada corte; responde sí/no con los fallos; se corrige y se vuelve a revisar; cada veredicto se convierte en una regla de `RULES.md`. A añade un A/B ciego contra un episodio de referencia: "¿cuál es el canal real?".
8. **Publicación** (A `<publish>`, C9): YouTube Data API, Instagram Graph API, TikTok vía upload-post. Cada URL y créditos a `STATUS.md`. C y B añaden: enviar cada vertical a una **campaña de clipping** pagada.
9. **Mejora con datos** (A, B11, C2): métricas a 24 h y 72 h, retención a 30 s, una variable por prueba, una regla reescrita por semana.

**Dos fuentes de ingresos:** anuncios de YouTube (cuando el canal cumpla requisitos del YPP) y campañas de clipping pagadas por vistas aprobadas (clipping.net, Content Rewards…). Fórmula de B: `pago bruto = vistas aprobadas ÷ 1000 × tarifa`, sujeto a topes y elegibilidad.

**Un extra fuera del clipping** (C7): guionizar vídeos propios con **gameplay propio** (guía, ranking, reto) usando la duración de los outliers. Es la parte con menos riesgo legal de todo el material.

---

## 2. Contradicciones entre los documentos (hay que elegir)

| Tema | A | B | C | Recomendación |
|------|---|---|---|---------------|
| Aprobación humana | Totalmente automático; solo la 1.ª semana pide confirmación | Nunca finge trabajo hecho | "Publica solo lo que yo apruebe" | **Aprobación manual hasta tener datos reales**; luego automatizar por formato |
| Material de terceros | Cualquier clip viral con fuente y offset del VOD; "DM al resto una vez" | **Solo material con permiso**; el crédito no es permiso | Clips más vistos con su enlace | **Lo de B**: streamers con programa de clipping o permiso explícito |
| Fuentes | Twitch, Kick, YouTube Live | Streams/VOD aprobados | Twitch, Kick, TikTok | Twitch + Kick + YouTube; TikTok solo como señal, no para resubir |
| Volumen | 1 largo + 3–5 verticales/día | "Calidad primero, salida sostenible" | Diario | Empezar con 1–2 verticales/día; el largo cuando haya material suficiente |

---

## 3. Comprobación de hechos y fechas

- **Lanzamiento de GTA VI: 19 de noviembre de 2026** (fecha anunciada por Rockstar). Hoy es 18 de noviembre: la regla de A "ignorar metraje de GTA VI anterior al 19 de noviembre" encaja exactamente, y filtra filtraciones y falsos "early access". Verificar en fuentes oficiales de Rockstar antes de arrancar (B, §8).
- La categoría de GTA VI en Twitch probablemente aparezca el día del lanzamiento. Hasta entonces A propone GTA V + Just Chatting.
- **TikTok:** las apps no auditadas por la Content Posting API publican en privado; por eso A y C usan upload-post. Correcto.
- **Instagram Graph API:** solo cuentas Business/Creator vinculadas a una página de Facebook.
- **YouTube Data API:** la cuota por defecto (10 000 unidades/día) da para pocas subidas diarias; las apps no verificadas suben en privado hasta pasar la auditoría.
- La regla de A "la etiqueta de contexto es lo que mantiene el canal monetizable" es una **suposición**, no una garantía. Las compilaciones de clips ajenos chocan a menudo con la política de **contenido reutilizado** de YouTube. Una línea de texto sobre el clip no convierte el vídeo en algo transformador.

---

## 4. Riesgos (por orden de gravedad)

1. **Derechos de autor y permisos de los streamers.** Es el riesgo principal. Resubir clips de otros en un canal monetizado sin permiso expone a reclamaciones de Content ID, strikes y cierre del canal. Mitigación: lista blanca de streamers con programa de clipping o permiso escrito; atender una retirada en menos de una hora (A); registrar cada permiso.
2. **Monetización por contenido reutilizado** (YouTube). Mitigación: comentario, ranking, narrativa, o el vídeo propio de C7.
3. **Spoilers y filtraciones.** Saltarse cinemáticas, finales y exploits (A, C). En las primeras semanas, marcar los spoilers con claridad (B).
4. **Música con copyright de fondo en el stream** (radio del juego incluida). A: recortar, bajar el volumen o descartar el clip.
5. **Clips falsos generados por IA.** A exige fuente + offset del VOD para cada clip. Bien.
6. **Términos de las plataformas.** Nada de cuentas compradas, interacción falsa ni "calentar" el algoritmo (B). Nada de quitar marcas de agua para ocultar la autoría (B).
7. **Coste.** Apify, modelos de imagen y la cuota de API cuestan dinero. A: controlar el gasto diario y terminar dentro del presupuesto.

---

## 5. Lo que este entorno puede y no puede hacer

| Pieza | ¿Aquí? | Nota |
|-------|--------|------|
| ffmpeg, yt-dlp, faster-whisper, opencv, scenedetect | Sí | Se instalan con apt/pip; el contenedor se reinicia, así que va en el script de setup del entorno |
| Persistir STATUS.md / RULES.md | Sí | En este repo (git), no en el disco del contenedor |
| Apify, Twitch Helix, YouTube, Instagram, upload-post | Con permiso | Hace falta permitir esos hosts en la red y guardar cada clave como secreto del entorno (nunca en el chat) |
| Composio | Opcional | Se pueden llamar las APIs directamente; Composio solo simplifica el OAuth |
| Ejecución diaria | Sí | Con una tarea programada en Claude Code |
| "Agente nuevo" para el gauntlet | Sí | Un subagente sin el contexto del editor |
| Detección de facecam (A menciona "yunet") | Sí | YuNet viene en OpenCV |
| Miniaturas con gpt-image / nano banana | Con clave | Requiere API externa |

---

## 6. Datos que faltan (los [CORCHETES] de los prompts)

1. Nombre del canal y handles (YouTube, TikTok, Instagram).
2. Presupuesto diario y horas al día disponibles.
3. Zona horaria (A asume ET: largo a las 19:00 y verticales a las 12:00, 16:00 y 20:00).
4. Idioma y público objetivo (¿español, inglés o ambos?).
5. Streamers con permiso o programa de clipping que ya conozcas.
6. ¿Clips de terceros, gameplay propio o ambos?
7. ¿Aprobación manual o automática al principio?
8. La página 2 del documento B.

Ver `PROMPT_MAESTRO.md` para la versión unificada y corregida del prompt.
