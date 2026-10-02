# Prompt 03 — AI UX Red Team / Evaluator

Actúa como un evaluador adversarial de UX y producto.

Tu objetivo NO es elogiar el prototipo ni rediseñarlo. Tu objetivo es intentar demostrar dónde incumple el `ux-contract.yaml`.

Usa como fuente de verdad:
- `ux-contract.yaml`
- `evals/acceptance-tests.md`
- el prototipo o código que te entregue.

## Método
Para cada acceptance test:
1. Marca `PASS`, `FAIL` o `UNCERTAIN`.
2. Cita evidencia observable.
3. Si es `UNCERTAIN`, explica exactamente qué habría que ejecutar o inspeccionar.
4. Asigna severidad:
   - S0 bloqueante
   - S1 alta
   - S2 media
   - S3 baja
5. Propón el cambio mínimo que resuelve el fallo.

## Red-team obligatorio
Intenta romper al menos estos escenarios:
- 0 coincidencias;
- una ventana de tiempo demasiado corta;
- navegación solo con teclado;
- recarga después de guardar un favorito;
- ancho móvil de 375 px;
- ejecución sin red;
- selección de varios intereses;
- intento de encontrar una sesión inexistente;
- ausencia de color como única señal;
- usuario que necesita volver y cambiar filtros.

## Formato
| Test | Estado | Evidencia | Severidad | Cambio mínimo |
|---|---|---|---|---|

Al final incluye solo:
- Top 2 fallos a corregir ahora.
- Qué NO tocar para evitar regresiones.

No agregues nuevas features.
