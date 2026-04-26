# Capítulo 9: Auditoría de Configuración: La Ley del Sistema

## De la Intención Documental a la Realidad Material

> *"El sistema no obedece intenciones; obedece parámetros. Para el Fiscal Digital, lo que está escrito en el manual de seguridad es irrelevante si contradice la realidad binaria del servidor. En la Doctrina de la Evidencia, la configuración no es un detalle técnico; es la materialización de una decisión administrativa. Cada puerto abierto es un acto de gobierno ejecutado."*

El error fundamental de la auditoría tradicional es auditar la promesa (el documento) en lugar de la realidad (el parámetro).
El auditor pregunta: *"¿La política prohíbe el acceso administrativo remoto?"*.
El CISO responde: *"Sí, está firmado en la política ISO 27001"*.

Al Fiscal Digital no le importa el PDF. Le importa el valor del registro en el controlador de dominio. Si el sistema permite la conexión, **la organización ha autorizado materialmente el riesgo**, independientemente de lo que diga su literatura interna.

Este capítulo establece que la configuración técnica es la única política vigente. Todo lo demás es ficción corporativa.

---

## 9.1. La Disociación Normativa (Papel vs. Silicio)

Existe una brecha estructural de gobierno:

1.  **La Norma Declarada:** La intención del Directorio (Políticas).
2.  **La Norma Ejecutada:** La realidad configurada por el Administrador.

**El Principio de Supremacía Técnica:**
Cuando existe una discrepancia entre el documento y el parámetro, **el parámetro prevalece como verdad jurídica**.
Si la política prohíbe la exfiltración de datos, pero la configuración del USB permite la escritura, el acto de exfiltración no fue una "violación al sistema", fue una acción habilitada por el diseño del sistema.
La auditoría de configuración tiene como único fin cerrar esta brecha: alinear la física del sistema con la voluntad del gobierno.

---

## 9.2. Defaults de Fábrica: La Omisión del Deber de Cuidado

La presencia de configuraciones por defecto (parámetros de fábrica) no es un olvido técnico; es una **Abdicación de Diseño**.
Dejar un sistema en estado *Default* significa que nadie tomó la decisión consciente de adaptarlo a la necesidad y riesgo de la organización.

**Doctrina de la Debida Diligencia:**
Mantener credenciales, protocolos o servicios predeterminados constituye una **omisión verificable del deber de cuidado**.
El auditor no reporta "falta de hardening"; reporta que la organización decidió no ejercer su facultad de configuración, aceptando pasivamente la vulnerabilidad del fabricante. Es negligencia por inacción.

---

## 9.3. Configuration Drift (La Entropía de la Autorización)

Un sistema seguro el Día 1 no necesariamente es seguro el Día 100.
Los cambios operativos no documentados ("abre esto un momento", "apaga aquello para probar") erosionan la postura de seguridad.

**La Erosión de la Voluntad Administrativa:**
Este fenómeno, el *Drift*, no es solo desorden técnico; es la pérdida del control de gobierno sobre el activo.
Si la organización no puede detectar cuándo un parámetro crítico ha sido modificado, significa que **la administración ha perdido el mando sobre la infraestructura**. El *Drift* convierte el diseño original en una sugerencia histórica.

---

## 9.4. Infraestructura como Código (IaC): Trazabilidad de la Decisión

La modernización técnica (Terraform, Ansible) tiene un efecto secundario crítico para la auditoría: transforma la configuración en evidencia forense.

**El Repositorio como Cadena de Custodia:**
Cuando la infraestructura se define como código, cada cambio deja un rastro inmutable:

1.  **Autoría:** ¿Quién escribió el cambio en el código? (El *Commit*).
2.  **Autorización:** ¿Quién aprobó el cambio? (El *Pull Request*).
3.  **Integridad:** ¿Coincide el código con lo que corre en producción?

IaC no es una herramienta de despliegue rápido; es un mecanismo de **Trazabilidad Decisional**.
El auditor ya no revisa pantallas; audita el flujo de aprobación del código. Si el cambio no pasó por el flujo de aprobación, es un acto ilegítimo, un sabotaje o un error no autorizado.

---

## Conclusión del Capítulo

La política de seguridad vive en el archivo de configuración, no en la intranet.
Cualquier auditoría que se limite a revisar la documentación escrita sin contrastarla con la realidad paramétrica es un ejercicio de fe, no de verificación.

> La configuración traza la frontera de lo posible. Si el código permite una acción, esa acción es una realidad operativa aceptada por diseño. El sistema no tiene culpa; solo tiene parámetros.