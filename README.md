# Tarija Tech Week — Taller Intensivo UX/AI

## Taller
**Taller Intensivo UX/AI: De la Idea al Prototipo Digital en 50 Minutos**  
Duración operativa: **30 min**

## Idea central
**Problem → UX Contract → Build → Red Team → Controlled Iteration**

Este repositorio contiene el material técnico y de contingencia del workshop. La demostración está diseñada para seguir teniendo valor incluso si falla internet.

## Estructura

```text
.
├── README.md
├── ux-contract/
│   └── ux-contract.yaml
├── data/
│   └── agenda-demo.json
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

## Qué contiene
- `ux-contract/ux-contract.yaml` — fuente de verdad del prototipo.
- `data/agenda-demo.json` — subconjunto educativo de la agenda oficial.
- `prompts/01-discovery.md` — revisión de ambigüedades antes de construir.
- `prompts/02-build.md` — prompt principal de generación.
- `prompts/03-ai-ux-red-team.md` — evaluación adversarial contra el contrato.
- `prompts/04-controlled-iteration.md` — corrección mínima de fallos prioritarios.
- `evals/acceptance-tests.md` — pruebas verificables.
- `fallback/offline/index.html` — demo sin dependencias remotas.
- `docs/speaker-runbook.md` — guion de 30 minutos y plan de contingencia.

## Fuente de datos
Agenda oficial Tarija Tech Week 2026:  
https://tarijatechweek.com/agenda/

Snapshot usado para el kit: **02/10/2026**.

> El dataset es un subconjunto simplificado para demostración. Ante cualquier diferencia, manda la agenda oficial en línea.

## Regla del taller
**No evaluar “qué tan bonita quedó la app”; evaluar evidencia de cumplimiento.**

## Estado del workshop
Este repositorio está en preparación. Las carpetas `demo/before`, `demo/after`, `fallback/recordings` y `slides` se completarán después de validar la primera generación real y sus fallos.
