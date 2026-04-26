# ANEXO C: Formato de Hallazgo Irrefutable

> **CLASIFICACIÓN DEL DOCUMENTO:** ARTEFACTO FORENSE
>
> **OBJETIVO:** ESTANDARIZAR LA REDACCIÓN DE HALLAZGOS ELIMINANDO LA INTERPRETACIÓN SUBJETIVA
>
> **ALCANCE:** TODOS LOS INFORMES DE AUDITORÍA TÉCNICA Y GRC
>
> **REFERENCIA:** DOCTRINA DE LA EVIDENCIA (FISCALÍA DIGITAL)

---

## 1. Principio de Irrefutabilidad

En la auditoría tradicional, un hallazgo es el inicio de una negociación con el auditado. En la Fiscalía Digital, un hallazgo es una **demostración técnica reproducible** de una falla de control. 

Un hallazgo no se debate; se demuestra. Si el auditado puede "interpretar", "matizar" o "contextualizar" el hallazgo para diluir su gravedad, el hallazgo está mal redactado. Debe ser binario, estar anclado a un artefacto inmutable y ser reproducible por cualquier tercero independiente.

---

## 2. Anatomía del Hallazgo Forense

Todo hallazgo reportado a la Alta Administración o al Comité de Directorio debe contener obligatoriamente los siguientes seis elementos. La ausencia de uno solo de ellos **debilita irreversiblemente la fuerza probatoria del hallazgo**.

1.  **Criterio (La Norma Fija):** La regla de negocio, política corporativa o restricción de ingeniería que define el estado esperado ("El Deber Ser").
2.  **Condición (La Realidad Observada):** El hecho técnico irrefutable que demuestra la desviación de la norma ("El Ser").
3.  **Evidencia Técnica (El Artefacto):** La fuente primaria inmutable de donde se extrajo la condición (Ej: Nombre de la tabla, ID del log, hash del commit).
4.  **Reproducibilidad (El Código):** La instrucción exacta (SQL, script, comando CLI) que cualquier auditor puede copiar, pegar y ejecutar para obtener el mismo resultado y confirmar la falla.
5.  **Impacto Técnico y de Negocio:** La consecuencia materializada o la exposición directa generada por la vulnerabilidad.
6.  **Asignación de Responsabilidad de Control:** La identificación nominal del dueño del riesgo (Data Owner / System Owner) responsable por la falla del diseño preventivo.

---

## 3. Plantilla de Aplicación (Ejemplo Estándar)

A continuación, se presenta el formato oficial de redacción de un hallazgo irrefutable, utilizando como ejemplo una violación de Segregación de Funciones (SoD).

**[ID_HALLAZGO_001]: Violación de Segregación de Funciones (SoD) en Entorno Productivo (Pagos)**

* **1. Criterio:** La Política de Seguridad Financiera v2.1 (Cap. 4) y la Matriz de Riesgos prohíben estrictamente que una misma identidad digital cree un proveedor y apruebe un pago hacia ese mismo proveedor.
* **2. Condición:** El control preventivo a nivel de aplicación falló o es inexistente. Se identificaron 14 transacciones donde el usuario creador y el usuario aprobador son la misma cuenta de Active Directory.
* **3. Evidencia Técnica:** Registros inmutables extraídos del SIEM corporativo (Índice: `erp_prod_audit_logs`, Fuente: `ERP_audit_trail`).
* **4. Reproducibilidad:**
    ```sql
    SELECT 
        vendor_id, 
        payment_id, 
        created_by_user, 
        approved_by_user, 
        transaction_timestamp 
    FROM erp_prod.vendor_payments_log 
    WHERE created_by_user = approved_by_user
    AND status = 'PROCESSED';
    ```
* **5. Impacto:** Exposición directa a fraude interno mediante manipulación del ciclo de pagos. Capacidad técnica demostrada de exfiltración de capital sin detección preventiva.
* **6. Asignación de Responsabilidad de Control:** Diseño de control **INEFECTIVO**. La responsabilidad técnica recae en la Gerencia de Sistemas (System Owner) por no implementar la restricción a nivel de base de datos, y la responsabilidad operativa recae en la Gerencia de Finanzas (Process Owner) por operar bajo un diseño vulnerable.