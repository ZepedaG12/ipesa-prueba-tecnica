# IPESA Ensacado - Prueba Tecnica

Proyecto P5 para prueba tecnica de candidatos Desarrollador.

## Objetivo

Crear un programa iRite simplificado para Rice Lake 1280:

- una sola pantalla,
- peso objetivo configurable,
- visualizacion de peso actual,
- boton de inicio,
- salida digital activa durante llenado,
- salida apagada al alcanzar el set point.

## Estructura

- `prueba/main.src`: archivo principal de la prueba tecnica.
- `SPEC.md`: alcance, flujo y criterios de aceptacion.
- `project.ini`: configuracion base del proyecto.
- `desarrollo/`: submodulo con el repo de referencia `IPESAH/santa-ana-tanque`.

## Validacion pendiente

El archivo `prueba/main.src` fue revisado contra documentacion iRite en Context7
`/fr4nkastro/frank-docs` y contra patrones del repo de referencia. Falta cargarlo o
compilarlo en el entorno Rice Lake 1280 para validar IDs reales de widgets y mapeo de I/O.
# ipesa-prueba-tecnica
