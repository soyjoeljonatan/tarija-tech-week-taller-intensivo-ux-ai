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
| AT-01 | Recomendación básica | Seleccionar `AI` + disponibilidad 13:00 + 60 min | Aparecen hasta 3 sesiones reales del dataset; ninguna inventada | S0 |
| AT-02 | Máximo 3 pasos | Iniciar desde estado default y obtener recomendación | Decisión alcanzable en <= 3 pasos principales | S1 |
| AT-03 | No results recovery | Elegir combinación/ventana sin coincidencias | Mostrar estado vacío con acciones para cambiar filtros, ampliar tiempo o ver todas | S1 |
| AT-04 | Sin callejón sin salida | Abrir resultados y volver a editar preferencias | Siempre existe una ruta clara para cambiar la decisión | S1 |
| AT-05 | Explainability | Revisar cada recomendación | Cada tarjeta explica coincidencia temática/temporal sin ratings inventados | S1 |
| AT-06 | Integridad de datos | Comparar títulos, speakers, horas y salas con JSON | 0 campos de agenda fabricados | S0 |
| AT-07 | Keyboard | Usar Tab, Shift+Tab, Enter/Espacio | Todo control interactivo es accesible; focus visible | S1 |
| AT-08 | No color-only | Revisar selección, éxito y guardado | Estado comunicado también con texto/iconografía/estructura | S2 |
| AT-09 | Mobile 375 px | Abrir a 375 px de ancho | Sin scroll horizontal; CTA y contenido siguen utilizables | S1 |
| AT-10 | Guardado local | Guardar sesión, recargar la página | Favorito persiste con localStorage | S2 |
| AT-11 | Offline | Cargar versión local, desconectar red y repetir flujo | Flujo principal sigue operativo sin requests externas | S0 |
| AT-12 | Reduced motion | Activar `prefers-reduced-motion: reduce` | Animaciones prescindibles se reducen/eliminan | S2 |
| AT-13 | Datos frescos | Revisar pie o info | Se muestra aviso de demo y prioridad de la agenda oficial | S2 |
| AT-14 | Multi-interest | Elegir `AI` + `UX` | Ranking favorece coincidencias múltiples sin inventar score de calidad | S1 |
| AT-15 | Ventana temporal | Configurar hora/duración que excluye una sesión | No recomienda sesiones fuera de la ventana definida | S1 |

## Smoke test final
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
