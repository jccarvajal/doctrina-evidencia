# ANEXO D: Responsabilidad Legal y Transferencia de Riesgo

> **CLASIFICACIÓN DEL DOCUMENTO:** MARCO DE GOBIERNO DE AUDITORÍA
>
> **OBJETIVO:** PROTEGER LA FUNCIÓN DEL AUDITOR Y LIMITAR LA RESPONSABILIDAD TÉCNICA ANTE LA NEGLIGENCIA ADMINISTRATIVA
>
> **ALCANCE:** COMITÉ DE DIRECTORIO, ALTA ADMINISTRACIÓN, ÁREAS DE TI Y AUDITORÍA
>
> **REFERENCIA:** DOCTRINA DE LA EVIDENCIA (FISCALÍA DIGITAL)

---

## 1. Alcance y Límites de la Certificación del Auditor

El Fiscal Digital (ejerciendo la función de auditoría técnica) evalúa y certifica la existencia, el diseño y la efectividad operativa de la **arquitectura de evidencia** corporativa. No certifica la moralidad del personal, las intenciones de la gerencia, ni garantiza la invulnerabilidad absoluta de los sistemas frente a amenazas de día cero (zero-day).

* **Mandato del Auditor:** Su responsabilidad es detectar, exponer y reportar la brecha demostrable entre la política de control declarada y la configuración real ejecutada, basándose estrictamente en evidencia técnica admisible.
* **Exclusión de Responsabilidad:** El auditor **NO** es responsable de la ejecución de los parches, la reestructuración de la red, la modificación del código, ni la mitigación operativa del hallazgo. La corrección de la vulnerabilidad es obligación exclusiva e indelegable de la Administración (Dueño del Sistema / Dueño del Proceso).

---

## 2. Principio de Indemostrabilidad

Como se establece en el marco probatorio (Anexo B), la auditoría técnica no admite la presunción de cumplimiento. 

Si la Alta Administración, la Gerencia de TI o el Dueño del Proceso no pueden proveer la evidencia sistémica exigida (por ejemplo, porque los logs no se configuran, se borran prematuramente o el sistema opera como una caja negra), el control en cuestión se declara formalmente como **"Inexistente por Indemostrabilidad"**.

Este estado de indemostrabilidad constituye, por sí mismo, un **riesgo residual crítico**. La auditoría no asumirá ni respaldará bajo ninguna circunstancia la efectividad de un control que no puede ser probado mediante artefactos inmutables.

---

## 3. Mecanismo de Transferencia de Riesgo (Protocolo de Liberación)

La tecnología expone el riesgo, pero el gobierno corporativo decide qué hacer con él. Cuando la Alta Administración decide no solucionar un hallazgo crítico, rechazar la implementación de un control técnico por "razones de negocio", o postergar indefinidamente la regularización de un sistema indemostrable, se activa el protocolo de transferencia:

1.  **Cambio de Naturaleza:** El riesgo detectado deja de ser un "problema técnico de TI" o un "hallazgo de auditoría" y se tipifica automáticamente como una **Decisión Ejecutiva**.
2.  **Formalización (Aceptación de Riesgo):** Dicha decisión ejecutiva debe ser documentada, justificada y firmada formalmente en un acta del Comité de Riesgos o Sesión de Directorio, identificando explícitamente al directivo que asume operar bajo dicho nivel de exposición.
3.  **Liberación de Responsabilidad Fiduciaria:** La emisión de esta acta traslada la responsabilidad primaria a la administración, liberando al equipo de Auditoría, al CISO y a las áreas operativas de cualquier responsabilidad legal, civil o fiduciaria derivada de la explotación futura, fuga de datos o colapso operativo provocado por la vulnerabilidad conscientemente aceptada.

El riesgo que no se mitiga con ingeniería, se asume con patrimonio y responsabilidad ejecutiva directa.