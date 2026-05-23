# IPESA - Ensacado Prueba Técnica

## 1. Resumen

- **Proyecto:** IPESA Ensacado - Prueba Técnica para candidatos Desarrollador
- **Tipo:** iRite monolítico (single `main.src`)
- **Equipo:** Rice Lake 1280
- **Comunicación:** TCP/IP (TCPC2)
- **Objetivo:** Sistema de ensacado simplificado como prueba técnica para candidatos

## 2. Alcance

### Included
- Interfaz gráfica de una sola pantalla
- Configuración de peso objetivo
- Botón de inicio/paro
- Visualización de peso en vivo
- Activación de salida al iniciar, desactivación al alcanzar setpoint

### Excluded
- Base de datos
- Múltiples pantallas
- Histórico de pesada
- Configuración de recetas
- Logging a archivo

## 3. Diseño UI

```
┌─────────────────────────────────────────────┐
│  ENSACADO - PRUEBA TÉCNICA                │
├─────────────────────────────────────────────┤
│                                             │
│  Peso Objetivo: [    50.0    ] kg          │
│                                             │
│  Peso Actual:      23.45 kg                │
│                                             │
│  Estado:            ESPERANDO             │
│                                             │
│  Salida:             OFF                  │
│                                             │
│  [  INICIAR  ]     [  DETENER  ]          │
│                                             │
└─────────────────────────────────────────────┘
```

## 4. Campos

| Campo | Tipo | Descripción |
|-------|------|-------------|
| `peso_objetivo` | Entry (decimal) | Set point en kg |
| `peso_actual` | Label (readonly) | Peso leído de bascula |
| `estado` | Label | ESPERANDO / LLENANDO / COMPLETADO |
| `salida` | Label | OFF / ON |
| `btn_iniciar` | Button | Activa llenado |
| `btn_detener` | Button | Para el proceso |

## 5. Flujo funcional

```
1. Operador ingresa peso objetivo (ej: 50.0 kg)
2. Operador presiona INICIAR
3. Estado cambia a "LLENANDO"
4. Salida se activa (ON)
5. Sistema monitorea peso_actual
6. Cuando peso_actual >= peso_objetivo → Salida OFF, Estado COMPLETADO
7. Presionar DETENER o esperar confirmación para reiniciar
```

## 6. Arquitectura

- ** Paradigma:** Monolito - todo en `main.src`
- ** Manejo de eventos:** `handler WidgetClicked` para botones, `handler UserEntry` para el peso objetivo, `handler Timer1Trip` para monitoreo continuo
- ** Sin base de datos**
- ** Peso:** lectura mediante `GetGross(scale, Primary, value)`
- ** Salida:** control mediante `SetDigout(slot, bit, value)`
- ** UI:** una pantalla Revolution preconfigurada; el SRC actualiza widgets con `SetLabelText` y abre captura numerica con `PromptUser` / `GetEntry`

## 7. Hardware

- **Báscula:** Rice Lake 1280
- **Comunicación:** TCP/IP vía TCPC2
- **Salida:** Digital output (DO) controlada por el programa

## 8. Criterios de aceptación

- [x] Interfaz muestra peso objetivo, peso actual, estado y salida
- [x] Botón INICIAR activa la salida y cambia estado a LLENANDO
- [x] Botón DETENER para el proceso y resetea estado
- [x] Cuando peso_actual >= peso_objetivo, salida se desactiva
- [x] Entrada de peso objetivo acepta valores decimales
- [x] Programa usa estructura iRite defendible: `program`, declaraciones, procedimientos, `handler ...`, `begin ... end main;`
- [x] Se eliminaron patrones no validados para iRite: `onInit`, `onClick`, `onEntry`, `onIdle`, `screen { ... }`, `label(...)`, `entry(...)`, `button(...)`
- [ ] Compilar/cargar en el entorno Rice Lake 1280 para validar los IDs reales de widgets y hardware
