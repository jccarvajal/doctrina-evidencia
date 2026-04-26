# Capítulo 11: Red Teaming y Prueba Hostil de Controles

## De la Hipótesis de Control a la Resistencia Material

> *"Un control que no ha sido atacado es una hipótesis. Un control que resistió una agresión es un hecho probado. La auditoría tradicional revisa el diseño documental; la auditoría adversaria somete ese diseño a estrés real para validar si la organización es capaz de detectar, resistir y, sobre todo, registrar la actividad hostil."*

Hasta este punto, hemos diseñado controles (Bloque 2) y auditado su consistencia (Bloque 3). Pero existe una diferencia abismal entre un control "bien configurado" y un control "eficaz".

El Fiscal Digital no valida intenciones ("El firewall está activo"). Valida resultados ("El firewall detuvo y registró el intento de exfiltración").
La **Prueba Hostil** no busca vulnerabilidades de software (eso es gestión de parches); busca **silencios en la capacidad de detección**.

---

## 11.1. Vulnerabilidad Técnica vs. Fragilidad de Proceso (Pentest vs. Red Team)

Es vital distinguir dos ejercicios que a menudo se confunden:

1.  **Pentest (Penetration Testing):** Busca agujeros técnicos (falta de parches, errores de código). Es una auditoría de *software*.
2.  **Red Teaming (Simulación de Adversario):** Busca agujeros de proceso y detección. Es una auditoría de *defensa*.

**El Objetivo de Auditoría:**
Al Fiscal Digital le interesa el Red Teaming.
No queremos saber si el servidor es vulnerable (eso se arregla con un update). Queremos saber si, cuando el atacante explota esa vulnerabilidad, **el sistema de vigilancia se da cuenta**.
Si el Red Team logra entrar, elevar privilegios y salir sin que se genere una alerta de seguridad, la prueba ha revelado una **ceguera funcional**.

---

## 11.2. La Prueba del Silencio: El Hallazgo Crítico

Muchas organizaciones configuran sus defensas para bloquear ataques en silencio.

* *Acción:* Intento de acceso no autorizado.
* *Respuesta del Sistema:* Bloqueo técnico.
* *Registro:* Ninguno (para "ahorrar espacio" o por mala configuración).

**Doctrina:**
En auditoría forense, un bloqueo sin registro es un evento inexistente.
La prueba hostil verifica que cada intento de violación de política genere un registro inmutable. **El silencio es un hallazgo de auditoría de nivel crítico.** Un sistema que se defiende pero no testifica carece de valor probatorio para la reconstrucción de los hechos.

---

## 11.3. Estrés de la Cadena de Custodia (Ataque a la Evidencia)

La prueba más importante de este capítulo es el intento deliberado de destruir la evidencia (validación del Cap 8).
El Red Team debe intentar activamente:

* Borrar los logs locales.
* Modificar la hora del servidor (NTP) para romper la línea temporal.
* Interrumpir la comunicación con el servidor central de logs (WORM).

**Veredicto de Resistencia:**

* **Falla Catastrófica:** Si el atacante logra borrar sus huellas, la cadena de custodia queda jurídicamente comprometida. El sistema pierde su capacidad de defensa legal.
* **Éxito de Diseño:** Si el intento falla y, además, genera una alerta de "Integridad Comprometida", la arquitectura es robusta.

---

## 11.4. La Ventana de Impunidad (Tiempo de Detección)

No basta con detectar; hay que detectar antes de que el daño sea irreversible.
La prueba hostil mide cronómetros, no solo éxitos/fracasos.

**Métrica de Eficacia:**
Si el Red Team exfiltra la base de datos a las 10:00 AM y la alerta llega a las 18:00 PM, el atacante tuvo 8 horas de **impunidad operativa**.
Para el Fiscal Digital, un tiempo de detección excesivo equivale a la inexistencia del control. La latencia destruye la capacidad de respuesta y permite la destrucción de evidencia secundaria.

---

## Conclusión del Capítulo

La prueba hostil transforma la fe en evidencia empírica.
Validar controles mediante entrevistas o revisión de configuraciones es insuficiente. Solo la agresión simulada revela la verdad de la postura defensiva.

> Un control no probado bajo estrés es solo una intención administrativa. La eficacia material del control solo se demuestra cuando este detecta, resiste y documenta un intento activo de subversión.