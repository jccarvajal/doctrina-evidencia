# ANEXO B: Estándar de Admisibilidad de Evidencia (Checklist Forense)

> **CLASIFICACIÓN DEL DOCUMENTO:** ESTÁNDAR DE VERIFICACIÓN TÉCNICA
>
> **OBJETIVO:** ERRADICAR LA VALIDACIÓN BASADA EN LA INTENCIÓN Y EL PAPEL
>
> **ALCANCE:** TODA LA INFRAESTRUCTURA TECNOLÓGICA Y PROCESOS DE AUDITORÍA
>
> **REFERENCIA:** DOCTRINA DE LA EVIDENCIA (FISCALÍA DIGITAL)

---

## 1. Principio de Evidencia Técnica Primaria

La auditoría técnica se basa exclusivamente en evidencia objetiva, inmutable y reproducible. Las declaraciones verbales, las políticas en formato PDF firmadas o las actas de reunión **no constituyen evidencia suficiente de operación del control**. 

La Muerte del Papel es un axioma procedimental: el documento normativo prueba el diseño del control; **solo el artefacto del sistema prueba su ejecución**.

---

## 2. Atributos de la Evidencia Admisible

Para que un artefacto sea considerado válido en un proceso de Fiscalía Digital, debe cumplir obligatoriamente con los siguientes tres atributos técnicos:

1.  **Origen Sistémico Directo:** La evidencia debe ser extraída mediante consulta (API, SQL, CLI) directamente del sistema evaluado o de su repositorio centralizado. No se aceptan transcripciones manuales ni planillas construidas por el auditado.
2.  **Inmutabilidad o Control de Alteración:** Los registros deben provenir de un entorno donde el administrador del sistema evaluado carezca de privilegios de alteración o borrado silencioso (ej. repositorios *append-only*, versionado estricto, o almacenamiento WORM).
3.  **Trazabilidad Temporal:** Todo evento debe contener una marca de tiempo (timestamp) generada por el servidor y sincronizada mediante NTP (Network Time Protocol) corporativo.

---

## 3. Catálogo de Artefactos Exigibles (Checklist)

En cualquier proceso de revisión, el responsable del sistema deberá proveer los siguientes artefactos técnicos. 

### 3.1. Dominio de Identidad y Accesos (IAM)
* **[ ] Matriz de Roles Efectiva:** Exportación de sistema (JSON/CSV) de los usuarios activos y sus privilegios reales en producción.
* **[ ] Trazas de Aprovisionamiento:** Registro sistémico de los últimos 90 días que demuestre qué cuenta administrativa creó, modificó o eliminó accesos.
* **[ ] Evidencia de Autenticación Fuerte:** Configuración exportada del Proveedor de Identidad (IdP) que demuestre la exigencia forzada e ineludible de MFA.

### 3.2. Dominio de Configuración y Despliegue
* **[ ] Repositorio de Infraestructura (IaC):** Acceso de solo lectura al historial de commits donde se definen las configuraciones de los servidores.
* **[ ] Reglas Preventivas Activas:** Archivos de configuración de *Compliance as Code* que impiden despliegues no autorizados.
* **[ ] Reporte de Desviación (Drift):** Alertas del sistema que comparen el estado deseado en el código versus el estado real productivo.

### 3.3. Dominio de Auditoría y Resiliencia
* **[ ] Trazas de Superusuario (Root/Admin):** Registro detallado e inmodificable de la ejecución de comandos por parte de cuentas con privilegios elevados.
* **[ ] Integridad de Logs:** Evidencia de protección contra alteración (repositorios *append-only*, versionado estricto o almacenamiento WORM) sobre los repositorios de auditoría.
* **[ ] Artefacto de Restauración:** Log automático del sistema de respaldo que certifique el éxito de la prueba de recuperación con estampa de tiempo.

---

## 4. La Presunción de Falla (Inexistencia por Indemostrabilidad)

La auditoría técnica no acepta el beneficio de la duda. Se establece el siguiente axioma procedimental para toda revisión:

> **La ausencia de evidencia técnica verificable se presumirá como evidencia de incumplimiento del control.**

Si el auditado afirma que un control se ejecuta, pero no puede proveer el log sistémico inmutable o la configuración exportada que lo demuestre, el hallazgo declarará formalmente que el control no existe en la realidad operativa. La incapacidad de demostrar trazabilidad constituye un riesgo inaceptable de impunidad técnica.