# Tarija Tech Week — Taller Intensivo UX/AI

## Taller
**Taller Intensivo UX/AI: De la Idea al Prototipo Digital en 50 Minutos**  
Duración operativa: **30 min**

## Idea central
**Problem → UX Contract → Build → Red Team → Controlled Iteration**

Este repositorio contiene el material técnico y de contingencia del workshop. La demostración está diseñada para seguir teniendo valor incluso si falla internet y para mostrar una agenda local que puede actualizarse de forma controlada.

## Estructura

```text
.
├── README.md
├── ux-contract/
│   ├── ux-contract.md          # canonical v1.1-frozen
│   └── ux-contract.yaml        # legacy/reference temporal
├── data/
│   ├── agenda-baseline.json
│   ├── agenda-current.json
│   ├── provenance.json
│   └── agenda-demo.json        # legado; no es la fuente activa del build
├── prompts/
│   ├── 01-discovery.md
│   ├── 02-build.md
│   ├── 03-ai-ux-red-team.md
│   └── 04-controlled-iteration.md
├── evals/
│   └── acceptance-tests.md
├── demo/
│   ├── before/
│   └── after/
├── fallback/
│   ├── offline/
│   │   └── index.html
│   └── recordings/
├── slides/
└── docs/
    └── speaker-runbook.md
```

## Fuentes de verdad
- `ux-contract/ux-contract.md` — contrato funcional y de UX canónico, **v1.1-frozen**.
- `data/agenda-baseline.json` — snapshot inmutable de referencia.
- `data/agenda-current.json` — única agenda que usa el motor de recomendaciones.
- `data/provenance.json` — procedencia, versión y ajustes locales de la agenda activa.
- `evals/acceptance-tests.md` — pruebas verificables del producto.

`ux-contract/ux-contract.yaml` se conserva temporalmente como referencia legacy y **ya no es la fuente canónica**.

`data/agenda-demo.json` queda temporalmente como archivo legado del primer kit y **no debe usarse como fuente activa** en nuevas generaciones.

## Responsive
TTW Session Scout es **mobile-first y responsive**, no mobile-only.

Viewports de referencia:
- mobile: `375 px`;
- tablet: `768 px`;
- laptop/desktop: `1280 px`.

Se mantiene el mismo producto, modelo de datos, lógica y capacidades esenciales en todos los tamaños. El layout puede adaptarse al espacio disponible. Ninguna acción esencial debe depender de hover.

## Agenda dinámica
La arquitectura contempla un flujo secundario para actualizar horarios sin convertir una extracción automática en verdad:

```text
.md / .pdf
   ↓
parse / extract
   ↓
normalize
   ↓
diff + conflict detection
   ↓
human preview
   ↓
confirm / cancel
   ↓
agenda-current + provenance
```

### Reglas
- Markdown es el formato preferido.
- PDF se trata como extracción best-effort.
- Un dato ambiguo debe quedar visible como `UNKNOWN` o warning.
- Ninguna importación altera `agenda-current` sin confirmación humana.
- `agenda-baseline` nunca se sobrescribe.
- Se permiten ajustes locales de retraso (+5, +10, +15 o personalizado) manteniendo trazabilidad.
- Salas válidas para este evento: `Main Stage`, `Sala IA`, `Sala Blockchain`.

## Prompts
- `prompts/01-discovery.md` — revisión de ambigüedades antes de construir.
- `prompts/02-build.md` — generación alineada al contrato, responsive y agenda dinámica.
- `prompts/03-ai-ux-red-team.md` — evaluación adversarial contra contrato, datos, responsive y provenance.
- `prompts/04-controlled-iteration.md` — corrección mínima de fallos prioritarios sin regresiones.

## Contingencia
- `fallback/offline/index.html` — demo local sin dependencias remotas.
- `docs/speaker-runbook.md` — guion de 30 minutos y plan A/B/C.

## Fuente de datos
Agenda oficial Tarija Tech Week 2026:  
https://tarijatechweek.com/agenda/

Snapshot base: **02/10/2026**.  
Archivo fuente entregado para el workshop: `agenda_tarija_tech_week_2026.md`.

> El dataset es un subconjunto educativo de la agenda. Ante cualquier diferencia, manda la agenda oficial en línea.

## Regla del taller
**No evaluar “qué tan bonita quedó la app”; evaluar evidencia de cumplimiento.**

## Estado del workshop
El UX Contract **v1.1-frozen** está congelado para la primera generación real. Incluye comportamiento mobile-first responsive para 375 / 768 / 1280 px. Las carpetas `demo/before`, `demo/after`, `fallback/recordings` y `slides` se completarán después de validar la primera generación real y sus fallos.
