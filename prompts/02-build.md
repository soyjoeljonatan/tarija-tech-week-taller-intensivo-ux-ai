# Prompt 02 — Build / Spec-Driven Prototype

Construye un prototipo funcional mobile-first llamado **TTW Session Scout** usando como fuente de verdad los archivos:

- `ux-contract/ux-contract.yaml`
- `data/agenda-baseline.json`
- `data/agenda-current.json`
- `data/provenance.json`
- `evals/acceptance-tests.md`

## Regla principal
El prototipo debe cumplir el contrato; no debes reinterpretarlo como una invitación a agregar features.

## Flujo principal — máximo 3 pasos
1. Elegir uno o más intereses + disponibilidad.
2. Ver hasta 3 recomendaciones.
3. Guardar una opción localmente.

## Flujo secundario — mantenimiento de agenda
Debe existir una vía separada para:
1. cargar agenda `.md` o `.pdf`;
2. mostrar preview/diff y warnings;
3. confirmar o cancelar.

Este flujo secundario NO cuenta dentro de los 3 pasos de recomendación.

## Restricciones obligatorias
- Sin login.
- Sin backend.
- Sin web search.
- Sin telemetría.
- No inventes sesiones, speakers, horarios, salas, ratings ni descripciones.
- El motor de recomendación usa exclusivamente `agenda-current.json`.
- `agenda-baseline.json` es inmutable.
- Una importación jamás modifica `agenda-current` antes de confirmación humana.
- Markdown es el formato preferido de importación.
- PDF es best-effort: cualquier ambigüedad debe quedar visible como `UNKNOWN` o warning.
- Debe detectar al menos: end <= start, sala desconocida, posible duplicado y solapamiento dentro de la misma sala/fecha.
- Salas válidas: `Main Stage`, `Sala IA`, `Sala Blockchain`.
- Debe permitir un ajuste de retraso local (+5, +10, +15 o custom) sin modificar baseline.
- Debe existir recuperación cuando no haya resultados.
- Debe funcionar con teclado y focus visible.
- No depender solo del color.
- Respetar `prefers-reduced-motion`.
- Favoritos únicamente con `localStorage`.
- Agenda activa y provenance pueden persistirse localmente para la demo.
- Mostrar fuente/versión de la agenda activa y una nota: “Demo educativa; la agenda oficial en línea manda”.
- La versión offline no debe depender de imágenes, fuentes, scripts o APIs remotas.

## Recomendación
Cada tarjeta debe explicar en una frase por qué apareció, basada solo en:
- intereses seleccionados;
- horario;
- duración disponible.

No infieras calidad, popularidad o reputación del speaker.

## Importación
Antes de aplicar una actualización, mostrar un diff con categorías como:
- `added`
- `removed`
- `time_changed`
- `venue_changed`
- `speaker_changed`
- `ambiguous`

No conviertas una extracción incierta en un dato cierto.

## Antes de construir
Devuelve una lista breve de:
- requisitos que implementarás;
- requisitos que NO implementarás;
- acceptance tests que usarás para verificar el resultado;
- riesgos técnicos del parsing de PDF.

Después construye.
