# Runbook — actividad sospechosa en un equipo Windows

| | |
|---|---|
| **Regla** | propia, grupo `soc_analysis` |
| **Nivel** | 7-10 según la regla que dispare |
| **Técnicas** | T1059.001 · T1562.001 · T1071.001 · T1082 · T1021.002 |
| **Fuente** | agente Windows · canal de eventos de PowerShell y Sysmon |

## Disparador

Una regla propia de la familia `soc_analysis` supera el umbral y llega al flujo: PowerShell con
argumentos ofuscados, intento de desactivar el antivirus, exfiltración por web o DNS, descubrimiento
del sistema, movimiento lateral por SMB o sesión remota.

## Triaje (primeros 5 minutos)

1. Confirmar que el evento es real: la regla ha disparado **con su fase 3 y su nivel**.
2. Identificar activo, usuario y hora; comprobar si es una tarea de mantenimiento conocida.
3. Mirar eventos relacionados ±10 minutos (procesos padre, conexiones, inicios de sesión).
4. Clasificar: benigno, sospechoso o malicioso.

## Contención

- Aislar el equipo de la red si hay indicios de ejecución real.
- Bloquear la cuenta comprometida.
- Preservar evidencia: línea de comandos, hashes de los binarios, conexiones activas.

## Escalado

Abrir caso en TheHive con la alerta, el activo y la línea de comandos. Avisar al responsable del
activo con el resumen en una frase.

## Cierre

- Acción tomada y verificación de que el proceso o la conexión ya no están.
- ¿La regla generó falsos positivos? Ajustar patrón o umbral.
- Documentar en el caso y dejar la captura de `wazuh-logtest` como prueba de que la detección sigue
  viva.
