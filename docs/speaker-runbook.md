# Runbook de speaker — Taller UX/AI 30 min

## Objetivo pedagógico
Que el público salga pudiendo repetir este patrón:

**Problem → UX Contract → Build → Red Team → Controlled Iteration**

La herramienta puede cambiar. El método debe sobrevivir.

## Regla de scope
No agregar features durante el workshop.

La demostración es exitosa si el público entiende que:
1. generar no es validar;
2. un requisito debe poder comprobarse;
3. la IA acelera tanto los aciertos como los errores;
4. el criterio humano se desplaza hacia especificar, verificar y decidir.

---

## Cronómetro

### 00:00–02:00 — Hook
Pregunta:

> “Si una IA me genera una app funcional en dos minutos, ¿cómo sabemos que construyó la app correcta?”

Mostrar una pantalla/prototipo rápido.

Frase:
> “El prompt produce una salida. El contrato nos permite discutir si esa salida es aceptable.”

### 02:00–05:00 — Problema
Caso: un asistente a TTW quiere decidir qué sesión aprovechar con poco tiempo.

Mostrar:
- usuario;
- JTBD;
- 3 constraints;
- 3 acceptance tests.

No explicar todo el YAML.

### 05:00–08:00 — UX Contract
Mostrar el archivo completo solo 10–15 segundos.

Enfatizar:
- estados;
- restricciones;
- éxito;
- acceptance tests.

Pregunta al público:
> “¿Qué estado suele olvidar un prototipo hecho con prisa?”

Buscar: vacío, error, offline, loading.

### 08:00–14:00 — Build
Usar `Prompt 02`.

Mientras genera:
- explicar por qué no permitimos APIs externas;
- mostrar el dataset;
- preguntar qué creen que la IA omitirá.

**Timeout operativo:** si no hay preview utilizable al minuto 90, pasar a la grabación/backup sin disculparse extensamente.

Transición:
> “No vamos a evaluar a la IA por si terminó de renderizar a tiempo. Vamos a evaluar el producto contra el contrato.”

### 14:00–20:00 — Human Red Team
Pedir al público que intente romperlo.

Probar mínimo:
- no results;
- volver y cambiar filtros;
- 375 px;
- teclado.

Registrar 1–2 fallos.

### 20:00–24:00 — AI UX Red Team
Usar `Prompt 03`.

Comparar:
- lo que encontró el público;
- lo que encontró el evaluator.

Idea:
> “La IA puede ayudar a verificar IA, pero la fuente de verdad debe seguir siendo un criterio explícito.”

### 24:00–27:00 — Controlled Iteration
Usar `Prompt 04`.

Corregir únicamente los 2 fallos principales.

Frase:
> “Iterar no significa volver a pedir ‘hazlo mejor’. Significa cambiar evidencia.”

### 27:00–29:00 — Transferencia
Mostrar repo/QR con:
- UX Contract;
- dataset;
- prompts;
- acceptance tests;
- demo offline.

Desafío al público:
> “Cambien el dataset y el problema, pero mantengan el método.”

### 29:00–30:00 — Cierre
Versión recomendada:

> “Construir rápido puede impresionar. Construir bien puede transformar. Las herramientas van a seguir cambiando; el criterio con el que decidimos qué construir y la excelencia con la que lo hacemos siguen siendo nuestra responsabilidad.”

---

# Contingencia

## Plan A — Internet estable
Build en vivo + prueba + iteración.

## Plan B — Internet lento
Abrir una generación ya preparada y ejecutar solo la iteración en vivo.

## Plan C — Sin internet
Abrir `fallback/offline/index.html`, hacer human red team y enseñar los clips del proceso.

## Disparadores
- >90 s sin preview: backup.
- Login/permiso bloqueado: backup.
- La herramienta cambia UI: no perder tiempo explicando; backup.
- Proyector falla: tener PDF exportado y demo local.

---

# Grabaciones que deben existir ANTES del taller

## Clip A — First build
Duración: 60–90 s.
Contenido: cargar contrato/dataset → prompt → preview.

## Clip B — Failure discovery
Duración: 45–60 s.
Contenido: provocar estado vacío + mostrar otro fallo.

## Clip C — Controlled iteration
Duración: 60–90 s.
Contenido: aplicar corrección → re-test.

### Ajustes
- 1080p.
- cursor visible.
- zoom UI 125–150% si hace falta.
- notificaciones desactivadas.
- no depender de audio del clip.
- guardar localmente, no solo en nube.

---

# Checklist físico
- laptop cargada;
- cargador;
- adaptador HDMI/USB-C;
- mouse;
- hotspot;
- videos locales;
- PDF local;
- carpeta del repo clonada/local;
- `index.html` probado sin Wi-Fi;
- pestañas ya autenticadas;
- modo “No molestar”;
- fuente del navegador aumentada;
- QR probado desde otro teléfono.
