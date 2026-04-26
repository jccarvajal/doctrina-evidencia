# Capítulo 10: Auditoría de Comportamiento: La Verdad del Log

## De la Permisibilidad Formal a la Legitimidad Operativa

> *"El permiso define lo autorizado; el comportamiento define lo legítimo. Un sistema puede estar correctamente configurado y, aun así, permitir conductas incompatibles con la función del negocio. En la Doctrina de la Evidencia, el comportamiento no es un dato complementario; es la evidencia primaria que constituye o cuestiona la verdad operativa del sistema."*

En los capítulos anteriores aseguramos la Identidad (Cap 5) y la Configuración (Cap 9). Sin embargo, existe un espacio crítico de impunidad: **El abuso del permiso legítimo.**

Para el Fiscal Digital, el cumplimiento de la regla estática ("El usuario tiene acceso") es irrelevante si la ejecución dinámica viola la lógica del negocio.
Pasamos de auditar **Controles** a auditar **Coherencia**.

---

## 10.1. Permiso Válido ≠ Conducta Válida

El error conceptual más común en auditoría es asumir que *"Si el sistema lo permitió, entonces es legítimo"*. Esto es falso.
Un permiso es una habilitación técnica; la legitimidad es una evaluación funcional.

**El Caso de la Incoherencia:**
Un analista financiero tiene permiso de lectura *root* sobre la base de datos histórica (porque "así se configuró").

* *Acción:* Descarga la totalidad de los registros contables de los últimos 10 años un domingo a las 3 AM.
* *Resultado Técnico:* El sistema no bloquea la acción. El permiso existe.
* *Dictamen Forense:* La acción es **funcionalmente incoherente**. No existe justificación operativa para una descarga masiva fuera de horario. La desviación no es técnica; es de propósito.

---

## 10.2. La Línea Base Conductual (Baseline Operativo)

No se puede auditar lo anómalo si no se ha definido lo habitual.
La auditoría de comportamiento exige construir una **Línea Base Operativa** por función, no por persona.

**Definición del Patrón de Rol:**
El sistema debe modelar qué es comportamiento "típico" para un rol específico (ej. Cajero, SysAdmin):

* ¿Cuáles son sus horarios de operación?
* ¿Qué volumen de datos manipula usualmente?
* ¿Desde qué ubicaciones geográficas accede?

Cuando la conducta rompe la lógica del rol, surge un indicio de **incoherencia funcional**. Y la incoherencia es materia de hallazgo, independientemente del permiso.

---

## 10.3. La Desviación como Indicio Técnico

En la auditoría forense moderna, la desviación estadística no es un error de sistema; es **causa probable**.
Aquí radica un cambio doctrinal fundamental: **El log de comportamiento no se usa para "confirmar" una sospecha externa; se usa para cuestionar la presunción de legitimidad técnica.**

**Tipos de Desviación Crítica:**

1.  **Desviación de Volumen:** Incrementos abruptos e injustificados en la cantidad de datos exportados (Exfiltración).
2.  **Desviación de Contexto:** Uso de herramientas administrativas por usuarios de negocio.
3.  **Inviabilidad Espacio-Temporal:** Accesos sucesivos desde ubicaciones físicamente imposibles (*Impossible Travel*).

---

## 10.4. Incoherencia de Rol y Obligación de Justificación

Cuando un usuario actúa dentro de sus permisos pero fuera de la lógica de su función, se activa una **Presunción Técnica de Compromiso**.

**La Regla de la Justificación Documentada:**
Toda acción que se desvíe sustancialmente del Baseline requiere una explicación formal (Ticket de Cambio, Orden de Trabajo).
Si no existe documento que respalde la anomalía, la conducta pasa de ser "posible" a ser **"administrativamente cuestionable"**.
La auditoría no necesita probar intención maliciosa (dolo); solo necesita probar **incoherencia no justificada**. Esto traslada la responsabilidad de la explicación al usuario dentro del proceso de control interno.

---

## 10.5. La Acción Aislada vs. El Patrón Persistente

Un evento único puede ser un error operativo. Un patrón repetido es diseño.

**Auditoría de Recurrencia:**
La auditoría de comportamiento no se centra solo en el evento aislado, sino en la persistencia temporal:

* Accesos repetidos fuera de horario laboral ("Testing the waters").
* Transferencias fraccionadas sistemáticas para evitar umbrales de alerta ("Salami Slicing").

Cuando la desviación se vuelve hábito, ya no estamos ante error o negligencia. Estamos ante un **riesgo estructural de abuso sistemático**.

---

## Conclusión del Capítulo

La auditoría tradicional valida que los controles existan. La auditoría conductual valida que la operación sea coherente.
Un sistema puede tener todos los controles técnicos en verde (Identidad, Logs, WORM) y aun así permitir el desfalco si nadie audita la consistencia entre el rol declarado y la acción ejecutada.

> El permiso habilita la capacidad técnica; la desviación conductual revela la intención operativa. Un permiso válido ejecutado de forma incoherente es, por defecto, una anomalía que requiere justificación forense.