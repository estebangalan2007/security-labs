# Arquitectura del flujo

## 1. Qué dispara

Solo las alertas que superan un umbral de nivel salen del manager. Por debajo, se quedan en el
registro: el objetivo es que lo que llegue al analista sea accionable.

```xml
<!-- /var/ossec/integrations/custom-n8n -->
<nivel_minimo>7</nivel_minimo>
<webhook>http://<n8n>/webhook/<ruta></webhook>
<formato>json</formato>
```

## 2. Qué hace n8n

1. **Valida** el JSON recibido (si no trae regla, nivel y agente, se descarta).
2. **Enriquece**: nombre del activo, técnica MITRE y grupo de la regla, hora local.
3. **Deduplica**: si hay un caso abierto con la misma regla y el mismo activo en la última hora, se
   añade como observación en vez de abrir otro.
4. **Decide** por nivel: alto → caso en TheHive; medio → observación; bajo → sólo registro.
5. **Notifica** al chat con el enlace al caso.

## 3. Puntos frágiles (lo que hay que vigilar)

- **Reglas mal colgadas**: una regla con un `if_sid` que no corresponde nunca dispara y el flujo
  queda vacío sin dar error. Se detecta probando cada regla con `wazuh-logtest`.
- **Webhook caído**: la integración falla en silencio si n8n no responde. Conviene un chequeo diario
  de que llegan eventos.
- **Duplicados**: sin deduplicación, una ráfaga llena TheHive de casos iguales.
- **Datos personales**: la alerta puede traer usuarios y rutas; el caso debe limitarse a lo necesario.

## 4. Métricas que merece la pena medir

| Métrica | Para qué |
|---|---|
| Alertas por regla y semana | detectar reglas ruidosas o muertas |
| Tiempo hasta el caso | salud del flujo |
| Casos cerrados como falso positivo | calidad de las reglas |
| Reglas que nunca han disparado | detección ciega |
