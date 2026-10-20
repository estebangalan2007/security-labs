# Reglas propias con MITRE ATT&CK

## Anatomía

```xml
<rule id="100xxx" level="9">
  <if_sid>PADRE</if_sid>
  <match>patron-a-detectar</match>
  <description>Qué se detecta, en una frase</description>
  <mitre>
    <id>T####.###</id>
  </mitre>
  <group>categoria,mitre_t####.###,soc_analysis,</group>
</rule>
```

- **`if_sid`** — la regla padre. La hija solo se evalúa si el padre ya encajó con **ese mismo
  evento**, y además su `match` debe aparecer en la misma línea. Elegir el padre es elegir el juego
  de datos: si es de otra familia (por ejemplo, una regla de sshd para un evento de PowerShell), la
  regla no dispara nunca.
- **`level`** — de 0 a 15. Por debajo del umbral de la integración, la alerta no sale del manager.
- **`mitre`** — solo el `id`; táctica y técnica se resuelven al consumir la alerta.
- **`group`** — permite buscar y filtrar después (`mitre_t####.###`).

## Cómo se prueba (obligatorio)

```bash
printf '%s\n' '<evento de prueba en el formato que llega del agente>' | \
  sudo /var/ossec/bin/wazuh-logtest
```

La salida tiene tres fases: pre-decodificación, decodificación y búsqueda de regla. **Si la fase 3
no devuelve una regla con su nivel, no hay alerta.** Se comprueba con dos eventos: el malicioso y
uno de control que sí deba disparar.

## Lista de comprobación

- [ ] El padre corresponde al decodificador que recibe el evento (comprobado en la definición).
- [ ] El evento malicioso dispara y devuelve el nivel esperado.
- [ ] El evento de control dispara con su propia regla.
- [ ] El nivel supera el umbral de la integración.
- [ ] La regla tiene descripción clara y técnica MITRE.
- [ ] Se ha guardado la captura de la fase 3 como evidencia.
