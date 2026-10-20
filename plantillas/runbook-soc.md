# Runbook — <nombre de la alerta>

| | |
|---|---|
| **Regla** | <id y descripción> |
| **Nivel** | <nivel Wazuh / severidad> |
| **Técnica** | T####.### |
| **Fuente** | <agente, decodificador, log> |

## Disparador

Qué evento hace saltar la alerta y con qué campos.

## Triaje (primeros 5 minutos)

1. Confirmar que el evento es real (no un falso positivo conocido).
2. Identificar activo, usuario y hora.
3. Ver si hay eventos relacionados ±10 minutos.
4. Clasificar: benigno / sospechoso / malicioso.

## Contención

- Aislar el activo
- Bloquear la cuenta o la IP
- Preservar evidencia antes de tocar nada

## Escalado

Cuándo abrir caso, a quién avisar y con qué información.

## Cierre

- Acción tomada y verificación
- Lección para la regla (¿falso positivo? ¿ajustar umbral?)
- Documentar en el caso
