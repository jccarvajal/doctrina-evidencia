# ANEXO E: CUSTODIA DELEGADA Y SOBERANÍA PROBATORIA
**La Cadena de Custodia como Arquitectura de Independencia**

## 1. El Supuesto que Este Anexo Destruye

La Doctrina de la Evidencia descansa sobre un principio técnico: la única verdad jurídica es el artefacto inmutable. El Capítulo 08 estableció las condiciones de ese artefacto —logs WORM, sincronización temporal verificable, cadena de custodia ininterrumpida.

Ese principio asume, implícitamente, que la organización posee el control físico y lógico de la infraestructura donde reside la evidencia.

Ese supuesto es metodológicamente obsoleto. En la arquitectura operacional contemporánea, la organización delega de forma rutinaria la captura, almacenamiento y procesamiento de su realidad a terceros. El correo corporativo reside en plataformas SaaS; las identidades son provistas por servicios externos; las firmas digitales dependen de terceros de confianza; los algoritmos de riesgo corren en infraestructuras opacas.

Cuando la cadena de custodia depende de una arquitectura que no se controla, el problema deja de ser la simple preservación documental. El problema es la pérdida de control probatorio sobre la propia capacidad de reconstruir la realidad.

---

## 2. La Teoría Central: Soberanía Probatoria

La evidencia no existe para almacenar archivos criptográficamente íntegros. Existe para reconstruir hechos. La soberanía sobre los sistemas de información exige independencia probatoria suficiente para reconstruir los hechos sin depender materialmente de terceros.

*Principio de Soberanía Probatoria:*

Una organización posee soberanía probatoria cuando puede reconstruir de manera independiente los hechos relevantes para una decisión, auditoría, litigio o investigación, aun cuando los sistemas originales y sus custodios ya no existan.

La soberanía probatoria se pierde en el instante en que la validez, legibilidad o interpretación de una evidencia requiere que un juez, un regulador o un auditor confíen en la reputación, la continuidad comercial o la asistencia técnica de un tercero.

---

## 3. El Modelo de Degradación: Cuatro Dependencias Arquitectónicas

La soberanía probatoria no se pierde de forma abstracta; se degrada mediante dependencias estructurales específicas. Para diseñar controles efectivos, la arquitectura forense debe mapear cómo la delegación operacional se manifiesta en vulnerabilidades probatorias.

El siguiente marco clasifica las cuatro dependencias arquitectónicas fundamentales y su manifestación patológica:

| Dependencia Arquitectónica | Naturaleza de la Delegación | Manifestación Forense | Riesgo Materializado |
| :--- | :--- | :--- | :--- |
| **Dependencia de Custodia** | Un tercero almacena el registro original. | **Alteración Silenciosa** | Imposibilidad de demostrar integridad sin depender de la palabra del proveedor. |
| **Dependencia de Interpretación** | Un tercero procesa el dato para generar una conclusión. | **Opacidad Algorítmica** | Imposibilidad de explicar el proceso de transformación subyacente. |
| **Dependencia de Acceso** | Un tercero controla el formato, API o interfaz de lectura. | **Evidencia Rehén** | El registro existe, pero la organización no puede utilizarlo de forma autónoma. |
| **Dependencia Temporal** | Un tercero determina el ciclo de vida del dato o del servicio. | **Desaparición de Evidencia** | Expiración o purga del registro antes de que concluya el horizonte probatorio requerido. |

**Patologías Estructurales de la Evidencia Delegada**

Mientras que la *Alteración Silenciosa* y la *Desaparición de Evidencia* representan riesgos forenses extensamente documentados en la literatura clásica, la arquitectura de delegación contemporánea introduce dos patologías críticas que exigen nuevos enfoques de control:

*   **Evidencia Rehén (Falla de Acceso):** Existe una categoría de registro cuya integridad puede ser validada, pero cuya existencia es indisoluble del proveedor. Es la evidencia cuya extracción o lectura depende operacionalmente de formatos propietarios o consolas específicas de un tercero. Una exportación de logs que solo puede ser leída mediante el visualizador del proveedor original no es evidencia soberana; es una concesión temporal de lectura.
*   **Opacidad Algorítmica (Falla de Interpretación):** Frecuentemente, la evidencia depende de terceros no solo para su preservación, sino para su interpretación. Cuando un modelo propietario o algoritmo externo decide qué evento es relevante o calcula un nivel de riesgo, la organización delega el razonamiento. Si la organización posee el registro final pero no puede reproducir determinísticamente el proceso que generó esa conclusión, ha perdido su soberanía explicativa. Su valor probatorio disminuye drásticamente ante un escrutinio adversarial.

---

## 4. El Control Compensatorio: Anclaje Criptográfico

La única compensación arquitectónica viable para la evidencia generada bajo dependencias externas es el anclaje criptográfico inmediato, extrayendo el registro del dominio de confianza del proveedor en el instante mismo de su generación.

La implementación técnica exige:

1.  **Extracción en tiempo real:** Un pipeline que captura eventos mediante APIs de streaming en el momento exacto de ocurrencia.
2.  **Traducción a formato abierto:** Neutralización de la *evidencia rehén* mediante la transformación del registro a un esquema de datos abierto e independiente del proveedor.
3.  **Hash y sellado temporal:** Aplicación de un hash criptográfico estampado con un sello temporal emitido por una Autoridad de Tiempo ajena a ambas partes.
4.  **Almacenamiento WORM Soberano:** Escritura en infraestructura inmutable bajo control exclusivo de la organización, mitigando la *dependencia temporal* y de *custodia*.

---

## 5. Implicaciones para el PAT-100

El Anexo A define el PAT-100 como el estándar de auditoría sobre población total. En un modelo de custodia delegada, el PAT-100 requiere forzosamente reconciliación de ingesta.

No basta con auditar lo que el proveedor permite exportar; se debe auditar el diferencial entre lo generado y lo retenido. Una arquitectura de PAT-100 sin mecanismos de extracción soberana y neutralización de evidencia rehén es simplemente auditoría de muestreo delegada, disfrazada de auditoría continua.

---

## 6. Conclusión: La Evidencia como Fenómeno Arquitectónico

La cadena de custodia no es una propiedad estática del registro. Es una propiedad de la independencia que la organización conserva respecto de las dependencias que permiten reconstruir la realidad.

Bajo este marco, una organización puede acumular hashes, repositorios WORM, firmas digitales y sellos temporales, y aun así carecer de soberanía probatoria si depende de terceros para acceder a su evidencia, interpretarla o preservarla en el tiempo. Subcontratar la operación tecnológica es una decisión de eficiencia; subcontratar la capacidad de reconstruir la propia realidad operacional es una falla de gobernanza que inhabilita a la organización para defenderse.

La soberanía probatoria no se delega, se diseña.
