# Labs y SOC

Documentación de laboratorios de pentesting y de proyectos de detección y SOC.
Todo el contenido se ha ejecutado en **entornos propios de práctica** (VulnHub y laboratorio
local). No hay datos de clientes. En los writeups sí aparecen la IP y las credenciales de la
máquina del reto: son laboratorios públicos y retirados, y sin ellas el writeup no sirve.

## Por qué existe

Escribo cada laboratorio una vez y de ahí salen tres cosas: el histórico de git, esta web y las
piezas de contenido. Documentar es el principio de la cadena, no el final.

## Labs

| Máquina | Plataforma | Dificultad | Técnicas | Writeup |
|---|---|---|---|---|
| DarkHole 2 | VulnHub | media | T1213 · T1552.001 · T1078 · T1190 · T1505.003 · T1548.003 | [labs/darkhole2](labs/darkhole2/) |

## Proyectos SOC

- [wazuh-n8n-thehive](soc/wazuh-n8n-thehive/) — flujo de alerta: Wazuh → n8n → TheHive, con triaje y playbooks.

## Estructura

```
labs/<maquina>/        writeup, evidencia y scripts
soc/<proyecto>/        arquitectura, reglas y playbooks
plantillas/            writeup, informe de pentest, runbook de SOC
herramientas/          saneador de secretos
public/                lo que se publica en GitHub Pages
```

## Reglas del repositorio

1. **Nada de datos reales**: ni IPs, ni correos, ni hashes, ni credenciales, ni nombres de cliente.
2. El saneador (`herramientas/sanear.py`) corre en cada push y **bloquea** el commit si encuentra algo.
3. Cada lab lleva su apartado de **detección**: qué alerta lo habría cazado y con qué técnica.

## Uso

```bash
python3 herramientas/sanear.py --check .   # busca secretos
python3 herramientas/sanear.py --fix .     # los sustituye por marcadores
```

## Licencia

Código y scripts: MIT. Textos y writeups: CC BY-NC-SA 4.0.

> Todo el material es educativo y de laboratorio propio. No se publica ninguna técnica contra
> sistemas de terceros ni datos que no sean míos.
