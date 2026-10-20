# Wazuh → n8n → TheHive

Flujo de trabajo para que una alerta de Wazuh no se quede en un panel: se enriquece, se decide y
abre (o no) un caso en TheHive, con el aviso en el chat del equipo.

```
[Agentes Wazuh] → [Manager + reglas propias] → [integración custom-n8n]
                                                        ↓ webhook
                                               [n8n: validar + enriquecer]
                                                        ↓
                                  [TheHive: caso]  +  [Aviso al equipo]
```

## Componentes

- **Wazuh (manager + agentes)** — recolección y correlación; las reglas propias son las que deciden
  qué merece atención y con qué nivel.
- **Integración `custom-n8n`** — script en el manager que envía las alertas de nivel ≥ 7 al webhook
  de n8n. Formato JSON.
- **n8n** — normaliza, enriquece (activo, usuario, técnica) y decide si abre caso.
- **TheHive** — caso con la alerta y los indicadores.
- **Chat del equipo** — aviso con el enlace al caso.

## Documentos

- [arquitectura.md](arquitectura.md) — decisiones, flujo paso a paso y puntos frágiles.
- [reglas/](reglas/) — cómo se escribe una regla propia con MITRE y cómo se prueba.
- [playbooks/triaje-alerta.md](playbooks/triaje-alerta.md) — qué hace el analista en los primeros minutos.

## Estado

Documentado desde el diseño. Las reglas concretas de detección son de laboratorio y viven fuera de
este repositorio hasta que estén validadas con eventos reales.
