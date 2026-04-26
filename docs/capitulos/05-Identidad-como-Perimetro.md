# Capítulo 05: Identidad como Perímetro (IAM Forense)

## El Fin del Firewall y el Inicio de la Atribución

> *"En la nube, no existe el 'adentro' ni el 'afuera'. Solo existe el 'quién'. Si no puedo identificar al sujeto de la acción con certeza matemática, no puedo atribuir responsabilidad. Y sin atribución, no hay ley; solo hay impunidad anónima."*

Entramos al dominio de la ingeniería dura. Pero antes de auditar servidores, debemos auditar **Sujetos**.
En la arquitectura moderna (Zero Trust), el firewall perimetral ha muerto. La identidad es el nuevo perímetro.

El atacante ya no "rompe" la entrada; el atacante "inicia sesión" (*Log In*).
Por tanto, la gestión de identidad (IAM) deja de ser una tarea de soporte técnico ("resetear passwords") y se convierte en la disciplina forense fundamental: **La Cadena de Custodia de la Acción**.

---

## 5.0. El Objeto Real de la Auditoría Técnica

Antes de auditar una sola línea de configuración, el Fiscal Digital debe establecer la jerarquía de la evidencia. Rechazamos la auditoría plana y establecemos tres niveles de realidad probatoria:

1.  **Nivel 1: Auditoría Declarativa (La Promesa).**

    * *Fuente:* Políticas, Manuales, Diagramas.
    * *Valor Probatorio sobre el Hecho Técnico:* **Nulo.**
    * *Definición:* Lo que la organización *dice* que hace. Jurídicamente sirve para establecer el "Estándar de Cuidado" (intención), pero es inútil para verificar la ejecución real o eximir de responsabilidad operativa.

2.  **Nivel 2: Auditoría Configurativa (La Capacidad).**

    * *Fuente:* JSON, YAML, Reglas de Firewall, GPOs.
    * *Valor Probatorio:* **Medio-Alto.**
    * *Definición:* Lo que el sistema *está obligado* a permitir o denegar. Define las leyes de la física del entorno.

3.  **Nivel 3: Auditoría Comportamental (La Ejecución).**

    * *Fuente:* Logs de Acceso, Tráfico, Cambios de Estado.
    * *Valor Probatorio:* **Absoluto (condicionado).**
    * *Definición:* Lo que *realmente ocurrió*. Este valor es absoluto únicamente si se cumple la cadena de custodia criptográfica (ver Cap. 02).

**Sentencia Doctrinal:**
Si la Política (Nivel 1) dice "Prohibido el acceso remoto" y el Log (Nivel 3) muestra una conexión SSH exitosa, la Política no es un control; es **perjurio documental**. El Fiscal Digital audita la configuración y el comportamiento.

---

## 5.1. Identidad: De la Autenticación a la No-Repudiación

El objetivo de la IAM (*Identity and Access Management*) no es permitir el acceso; es garantizar el **No Repudio**.

Si un usuario comparte su contraseña, destruye la capacidad del sistema para distinguir entre el empleado legítimo y el atacante. **En entornos financieros, una identidad no atribuible convierte cualquier transacción en potencialmente impugnable.** Un sistema sin trazabilidad de identidad convierte cualquier incidente en un litigio perdido por incapacidad probatoria.

**El Hallazgo Forense:**
Cualquier sistema administrativo que permita la autenticación de un solo factor es inseguro por diseño. La contraseña es un "secreto compartido". El MFA (*Multi-Factor Authentication*) es la prueba de posesión.
**Doctrina Legal:** La ausencia de MFA en cuentas privilegiadas elimina la capacidad probatoria en caso de litigio. No hay perito que pueda defender una contraseña compartida.

**Excepción de Entornos Críticos (OT/Legacy):**
En entornos industriales (SCADA) o sistemas legacy donde el MFA no es técnicamente viable, la excepción debe estar **formalmente documentada**, aprobada por el Directorio y compensada con controles equivalentes (ej. segmentación física de red o vigilancia biométrica). Sin esta documentación, la ausencia de MFA es negligencia, no limitación técnica.

---

## 5.2. Cuentas de Servicio: Los Fantasmas con Privilegios de Dios

El mayor riesgo en la nube no son los humanos; son las **Cuentas de Servicio** (Non-Human Identities). Aplicaciones y bots que operan 24/7, a menudo con privilegios excesivos (*Over-privileged*).

**El Escenario de Terror:**
Un desarrollador crea una cuenta de servicio para una migración. Le da permisos de `Admin`. La migración termina. La cuenta queda activa. Las credenciales (API Keys) quedan *hardcoded* en el código fuente.

**La Regla de Rotación Forzada:**
Las identidades no humanas deben tener un ciclo de vida de credencial más corto que las humanas. Si una API Key tiene 3 años de antigüedad, es una vulnerabilidad crítica. El Fiscal Digital exige rotación automatizada. Una llave estática es una llave robada en potencia.

---

## 5.3. El Usuario Zombi (Off-boarding Fallido)

No hay amenaza más triste y evitable que el ex-empleado descontento que conserva acceso. Esto ocurre por la desconexión entre RRHH y TI.

* **RRHH:** Despide al empleado el viernes.
* **TI:** Recibe el ticket el lunes.
* **La Ventana de Venganza:** 65 horas de acceso no supervisado.

**Auditoría de Latencia de Revocación:**
Cruzamos la base de datos de nómina (fecha de despido) con los logs de actividad (último login).
Si encontramos un `Last_Login > Termination_Date`, tenemos evidencia de **falla en el proceso de baja**. El sistema permitió acceso a un actor externo sin vínculo contractual.

---

## 5.4. Break-Glass: La Gestión de la Emergencia

En crisis, se necesitan superpoderes. Las cuentas "Break-Glass" son usuarios de emergencia con privilegios absolutos.
El problema es cuando se usan para la rutina por comodidad operativa.

**Protocolo de Uso Forense:**

1.  La cuenta debe estar en una bóveda digital (PAM).
2.  Su extracción debe disparar alertas masivas a la 2ª y 3ª Línea.
3.  Toda acción debe ser grabada (video/log verboso).
4.  La contraseña debe rotar automáticamente al devolverse.

**Doctrina de Presunción:**
Toda cuenta Break-Glass utilizada fuera de un incidente formalmente declarado (Ticket de Crisis) constituye una **presunción de bypass deliberado de controles**. No es administración ágil; es administración no autorizada.

---

## 5.5. El Tablero de Control Forense (KPIs de Identidad)

El Fiscal Digital no acepta adjetivos ("el sistema es seguro"); exige sustantivos y números. La salud de la identidad se mide con métricas de tolerancia cero:

| Métrica Forense | Umbral Aceptable | Significado del Fallo |
| :--- | :--- | :--- |
| **% Admins sin MFA** | **0%** | Negligencia grave. Incapacidad de atribución. |
| **% Cuentas Genéricas Activas** | **0%** | Disolución estructural de responsabilidad. El "usuario compartido" impide el No Repudio. |
| **Edad de Credenciales de Servicio** | **< Política** | Llaves expuestas o hardcodeadas. |
| **Latencia de Revocación** | **< 24 horas** | Acceso no contractual (Riesgo legal alto). |
| **Privilegios Permanentes ("Standing")** | **0 (Tendencia a JIT)** | Superficie de ataque innecesaria. El privilegio debe ser efímero (Just-in-Time). |

---

## Conclusión del Capítulo

La identidad es el hilo conductor de la responsabilidad.
Pero hay una línea roja que el Directorio debe conocer.

Una vez informado formalmente este estado de debilidad en identidad (existencia de cuentas genéricas, falta de MFA, revocación tardía), la mantención de estas condiciones deja de ser un problema técnico de "deuda". Se convierte en una **decisión de gobierno**.

Mantener la opacidad en la identidad es una aceptación documentada de operar bajo un esquema de impunidad. Si ocurre un incidente, la organización no podrá alegar ignorancia técnica, solo complicidad por omisión.