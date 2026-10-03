# Acceptance Tests — TTW Session Scout

> Regla del taller: **una pantalla bonita no equivale a un requisito cumplido**.

## Escala
- PASS: evidencia observable de cumplimiento.
- FAIL: evidencia de incumplimiento.
- UNCERTAIN: no existe evidencia suficiente; debe probarse.
- S0: bloqueante
- S1: alta
- S2: media
- S3: baja

| ID | Test | Procedimiento | Resultado esperado | Severidad si falla |
|---|---|---|---|---|
| AT-01 | Recomendación básica | Seleccionar `AI` + disponibilidad 13:00 + 60 min | Aparecen hasta 3 sesiones reales de `agenda-current`; ninguna inventada | S0 |
| AT-02 | Máximo 3 pasos | Iniciar desde estado default y obtener recomendación | Decisión alcanzable en <= 3 pasos principales | S1 |
| AT-03 | No results recovery | Elegir combinación/ventana sin coincidencias | Mostrar estado vacío con acciones para cambiar filtros, ampliar tiempo o ver todas | S1 |
| AT-04 | Sin callejón sin salida | Abrir resultados y volver a editar preferencias | Siempre existe una ruta clara para cambiar la decisión | S1 |
| AT-05 | Explainability | Revisar cada recomendación | Cada tarjeta explica coincidencia temática/temporal sin ratings inventados | S1 |
| AT-06 | Integridad de datos | Comparar títulos, speakers, horas y salas con `agenda-current` | 0 campos de agenda fabricados | S0 |
| AT-07 | Keyboard | Usar Tab, Shift+Tab, Enter/Espacio | Todo control interactivo es accesible; focus visible | S1 |
| AT-08 | No color-only | Revisar selección, éxito, warnings y guardado | Estado comunicado también con texto/iconografía/estructura | S2 |
| AT-09 | Mobile 375 px | Abrir a 375 px de ancho y completar el flujo | Sin scroll horizontal inesperado; CTA, contenido y flujo completo utilizables | S1 |
| AT-10 | Guardado local | Guardar sesión, recargar la página | Favorito persiste con localStorage | S2 |
| AT-11 | Offline | Cargar versión local, desconectar red y repetir flujo | Flujo principal sigue operativo sin requests externas | S0 |
| AT-12 | Reduced motion | Activar `prefers-reduced-motion: reduce` | Animaciones prescindibles se reducen/eliminan | S2 |
| AT-13 | Datos frescos | Revisar pie o info | Se muestra procedencia/versión de la agenda activa y prioridad de la agenda oficial | S2 |
| AT-14 | Multi-interest | Elegir `AI` + `UX` | Ranking favorece coincidencias múltiples sin inventar score de calidad | S1 |
| AT-15 | Ventana temporal | Configurar hora/duración que excluye una sesión | No recomienda sesiones fuera de la ventana definida | S1 |
| AT-16 | Import Markdown | Cargar un `.md` con estructura reconocible y cambios respecto al baseline | El sistema extrae sesiones y muestra preview/diff antes de alterar `agenda-current` | S0 |
| AT-17 | Import PDF best-effort | Cargar un `.pdf` de agenda con al menos un campo difícil de extraer | Se muestran datos extraídos y cualquier ambigüedad se marca `UNKNOWN` o warning; no se inventa | S0 |
| AT-18 | Conflict detection | Importar dos sesiones que se solapan en misma fecha y sala, o un end <= start | Se muestra warning de conflicto antes de confirmar | S1 |
| AT-19 | Human confirmation | Importar una agenda válida y cerrar/cancelar el preview | `agenda-current` permanece sin cambios hasta confirmación explícita | S0 |
| AT-20 | Provenance | Confirmar una actualización y revisar información de fuente | La agenda activa muestra archivo/fuente, versión si existe, fecha de importación y `confirmedByHuman: true` | S1 |
| AT-21 | Venue validation | Importar una sesión con sala desconocida | Se marca como ambigua/inválida; no se normaliza silenciosamente a una sala existente | S1 |
| AT-22 | Delay offset | Aplicar +10 min a un rango de sesiones | Horas vigentes cambian en `agenda-current`, baseline queda intacto y provenance registra ajuste local | S1 |
| AT-23 | Failed import rollback | Provocar error de lectura/parsing durante importación | Se mantiene la agenda activa previa y existe opción de reintentar/cancelar | S0 |
| AT-24 | Baseline immutability | Confirmar una importación o delay y comparar con baseline | `agenda-baseline.json` no cambia | S0 |
| AT-25 | Tablet 768 px | Abrir a 768 px y completar el flujo principal | Sin overflow inesperado ni contenido crítico cortado; mismas capacidades esenciales que mobile | S1 |
| AT-26 | Laptop 1280 px | Abrir a 1280 px, completar flujo principal y navegar con teclado | Layout aprovecha el ancho sin cambiar la lógica; todo el flujo sigue utilizable con teclado | S1 |
| AT-27 | Sin hover obligatorio | Recorrer acciones esenciales en touch/teclado sin hover | Ninguna función esencial requiere hover ni existe solo en un viewport | S1 |

## Smoke test — flujo principal
1. Abrir.
2. Seleccionar `AI` + `UX`.
3. Elegir hora `13:00`.
4. Elegir `90 min`.
5. Generar recomendaciones.
6. Guardar una sesión.
7. Recargar.
8. Cambiar filtros.
9. Forzar un estado sin resultados.
10. Recuperarse sin reiniciar la aplicación.

## Smoke test — responsive
1. Completar flujo a 375 px.
2. Repetir a 768 px.
3. Repetir a 1280 px.
4. Verificar ausencia de overflow horizontal inesperado.
5. Verificar que ninguna acción esencial depende de hover.
6. En 1280 px, repetir el flujo solo con teclado.

## Smoke test — actualización de agenda
1. Revisar versión/fuente activa.
2. Cargar un `.md` modificado.
3. Ver diff sin aplicar.
4. Verificar que `agenda-current` todavía no cambió.
5. Provocar/detectar al menos un conflicto.
6. Corregir o aceptar conscientemente los datos permitidos.
7. Confirmar actualización.
8. Verificar provenance.
9. Ejecutar una recomendación con la agenda actualizada.
10. Comprobar que baseline permanece intacto.

## Regla de evaluación
La importación de archivos es una función secundaria del producto y no debe aumentar el flujo principal de recomendación por encima de 3 pasos.

El requisito responsive exige **usabilidad consistente**, no pixel-perfect idéntico entre viewports.
