# <Nombre de la máquina>

| | |
|---|---|
| **Plataforma** | VulnHub / HackTheBox / laboratorio propio |
| **Sistema** | <SO y versión> |
| **Dificultad** | fácil / media / difícil |
| **Fecha** | AAAA-MM-DD |
| **Tiempo** | <minutos> |

**Técnicas:** T####.### · T####.###
**Flags:** usuario `<flag-usuario>` · root `<flag-root>`

## Resumen

Dos o tres frases: por dónde se entra, qué falla y hasta dónde se llega.

## Reconocimiento

```bash
nmap -sC -sV -p- <IP-objetivo>
```

Qué devuelve y qué conclusión saco de cada puerto.

## Enumeración

Qué se prueba, en qué orden y por qué. Cada hallazgo con su evidencia.

## Acceso inicial

El fallo concreto, el comando exacto y la prueba de que funcionó.

## Post-explotación

Qué se encuentra dentro, con qué usuario y qué permite.

## Escalada de privilegios

La vía, el comando y la prueba del acceso como administrador.

## Detección

| Técnica | Qué genera | Alerta que lo cazaría |
|---|---|---|
| T#### | <evento o comportamiento> | <regla o fuente de log> |

Qué habría hecho falta para verlo en un SOC y qué señales deja.

## Lecciones

1. …
2. …

## Referencias

- Enlace oficial de la máquina
- Herramientas usadas
