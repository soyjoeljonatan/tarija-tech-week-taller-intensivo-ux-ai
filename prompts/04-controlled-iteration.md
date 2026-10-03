# Prompt 04 — Controlled Iteration

Tienes:
- `ux-contract/ux-contract.md`;
- `evals/acceptance-tests.md`;
- el prototipo actual;
- el reporte del AI UX Red Team.

Haz una iteración controlada.

## Objetivo
Corregir ÚNICAMENTE los 2 fallos de mayor prioridad identificados por el evaluator.

## Reglas
- No hagas un rediseño completo.
- No cambies la arquitectura si no es necesario.
- No agregues features.
- Conserva comportamientos que ya pasaron sus acceptance tests.
- Mantén el dataset intacto.
- No introduzcas dependencias externas.
- No rompas la paridad funcional entre 375 px, 768 px y 1280 px.
- Ninguna corrección debe introducir acciones esenciales dependientes de hover.

## Antes del cambio
Escribe:
1. test que falla;
2. causa;
3. cambio mínimo planeado;
4. posible regresión.

## Después del cambio
Reejecuta:
- los tests afectados;
- un smoke test del flujo principal;
- el viewport relacionado si el fallo es responsive.

Devuelve:
- tests corregidos;
- tests que siguen fallando;
- cambios realizados;
- deuda conocida que conscientemente no se resolvió.

La meta no es “hacerlo más bonito”; la meta es aumentar evidencia de que cumple el contrato.
