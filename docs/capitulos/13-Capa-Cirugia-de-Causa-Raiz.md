# Capítulo 13: CAPA: Cirugía de la Causa Raíz

## De la Corrección de Síntomas a la Solución Estructural

> *"Despedir al negligente es fácil; arreglar el proceso que permitió su negligencia es lo difícil. La mayoría de las organizaciones son expertas en 'parchar y seguir' (Corrección), pero mediocres en evitar la recurrencia (Acción Correctiva). En la Doctrina de la Evidencia, un incidente no se cierra cuando se restaura el servicio; se cierra cuando se ha extirpado quirúrgicamente la falla de diseño que lo hizo posible."*

El capítulo anterior (Sanción) cerró la responsabilidad individual. Este capítulo cierra la responsabilidad sistémica.
Si un usuario borró la base de datos, la sanción es para el usuario. Pero la pregunta del Auditor es: **¿Por qué el sistema permitió que un solo usuario tuviera la capacidad de borrar todo sin aprobación dual?**

El enfoque CAPA (*Corrective and Preventive Action*) transforma el incidente en una mejora de ingeniería.

---

## 13.1. Corrección vs. Acción Correctiva

Es vital distinguir dos conceptos que la gestión de TI suele confundir:

1.  **Corrección (Contención):** Es la acción inmediata para detener el sangrado.
    * *Ejemplo:* Restaurar el backup, cambiar la contraseña comprometida, reiniciar el servidor.
    * *Resultado:* El negocio sigue operando, pero el riesgo permanece latente.
2.  **Acción Correctiva (Remediación):** Es la modificación estructural para eliminar la causa.
    * *Ejemplo:* Implementar autenticación multifactor (MFA), rediseñar el flujo de permisos, segregación de funciones.
    * *Resultado:* El incidente no puede volver a ocurrir por la misma vía.

El Fiscal Digital no acepta un "Reinicio" como solución final. Eso es primeros auxilios, no cirugía.

---

## 13.2. Análisis de Causa Raíz (RCA): Los 5 Porqués

Para llegar a la Acción Correctiva, debemos ignorar la causa superficial ("el usuario hizo click") y encontrar la falla de gobierno.
Utilizamos la metodología de los **5 Porqués** aplicada a la auditoría:

* **Hecho:** Se fugó información confidencial.
    1.  *¿Por qué?* El usuario envió un Excel a su Gmail personal.
    2.  *¿Por qué pudo hacerlo?* El sistema de correo (DLP) no bloqueó el adjunto.
    3.  *¿Por qué no bloqueó?* La política de DLP estaba en modo "Monitoreo" y no "Bloqueo".
    4.  *¿Por qué estaba en modo Monitoreo?* Porque hace 6 meses se configuró así para una prueba y nadie la cambió (Drift del Cap 9).
    5.  *¿Por qué nadie la cambió?* **Causa Raíz:** No existe un proceso de revisión periódica de configuraciones críticas.

La solución no es "regañar al usuario"; es instituir la revisión de configuraciones.

---

## 13.3. El Plan de Remediación (La Cirugía)

Una vez identificada la causa raíz, se diseña el **Plan de Remediación**.
Este plan no es una intención; es un proyecto con:

* **Responsable:** Quién hará el cambio.
* **Fecha Límite:** Cuándo estará listo.
* **Evidencia de Cambio:** Cómo demostraremos que se hizo (Logs, Configuración, Código).

Si la causa raíz fue "Falta de Segregación de Funciones", la remediación es técnica (quitar permisos) y normativa (reescribir el procedimiento).

---

## 13.4. La No-Remediación como Acto de Gobierno

¿Qué pasa si la solución estructural es demasiado costosa o compleja para el negocio?
(Ejemplo: "No podemos cambiar el sistema legacy porque detiene la facturación").

**La Aceptación Formal del Riesgo Residual:**
La organización puede optar por no remediar, pero esa decisión constituye una **aceptación formal del riesgo de recurrencia**.
Si se decide no aplicar la CAPA propuesta, esa decisión debe quedar documentada en un **Acta de Aceptación de Riesgo**, firmada por el nivel jerárquico competente (Gerente General o Directorio).

* *Significado Jurídico:* "Entendemos la causa raíz, conocemos la probabilidad de recurrencia, y aceptamos conscientemente el impacto financiero/legal de que vuelva a suceder".

La no-remediación sin firma es negligencia. La no-remediación firmada es estrategia.

---

## 13.5. Verificación de Eficacia (La Prueba de Fuego)

El paso final de CAPA es validar que la "cirugía" fue exitosa.
Muchas empresas implementan un control y asumen que funciona.
El Auditor exige la **Prueba de Eficacia**:

* *Acción:* Intentar replicar el incidente original en un entorno controlado.
* *Éxito:* Si el sistema ahora bloquea o detecta la acción que antes permitió, la CAPA es efectiva.
* *Fracaso:* Si el incidente se puede repetir, la remediación fue cosmética.

Solo cuando la eficacia está probada empíricamente, se firma el cierre del hallazgo.

---

## Conclusión del Capítulo

Un incidente es una auditoría forzada y costosa. Desperdiciar esa lección aplicando solo parches superficiales es una ineficiencia de gobierno.
Una organización **estructuralmente robusta** es aquella que usa cada falla como un plano para blindar su arquitectura.

> Un problema resuelto sin atacar su causa raíz no es un problema solucionado; es un problema en espera. La inacción ante la causa raíz conocida es una decisión administrativa explícita de aceptar el riesgo de recurrencia.