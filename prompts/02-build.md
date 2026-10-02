# Prompt 02 — Build / Spec-Driven Prototype

Construye un prototipo funcional mobile-first llamado **TTW Session Scout** usando como fuente de verdad los archivos:

- `ux-contract.yaml`
- `data/agenda-demo.json`

## Regla principal
El prototipo debe cumplir el contrato; no debes reinterpretarlo como una invitación a agregar features.

## Flujo máximo
1. Elegir uno o más intereses + disponibilidad.
2. Ver hasta 3 recomendaciones.
3. Guardar una opción localmente.

## Restricciones obligatorias
- Sin login.
- Sin backend.
- Sin APIs externas.
- No hagas web search.
- No inventes sesiones, speakers, horarios, salas ni ratings.
- Usa exclusivamente `agenda-demo.json`.
- Debe existir recuperación cuando no haya resultados.
- Debe funcionar con teclado.
- Focus visible.
- No depender solo del color.
- Respetar `prefers-reduced-motion`.
- Favoritos únicamente con `localStorage`.
- Mostrar una nota breve: “Demo educativa; la agenda oficial en línea manda”.
- No uses imágenes remotas ni fuentes externas para que exista una versión offline reproducible.

## Recomendación
Cada tarjeta debe explicar en una frase por qué apareció, basada solo en:
- intereses seleccionados;
- horario;
- duración disponible.

No infieras calidad, popularidad o reputación del speaker.

## Antes de construir
Devuelve una lista de:
- requisitos que implementarás;
- requisitos que NO implementarás;
- acceptance tests que usarás para verificar el resultado.

Después construye.
