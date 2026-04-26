# Capítulo 08: Logs, No Repudio y Cadena de Custodia Digital

## La Construcción de la Memoria Forense

> *"Un evento que ocurre en un servidor y no se replica en tiempo real a un repositorio inmutable, jurídicamente no sucedió. El log local es la propiedad privada del atacante; el log centralizado es la evidencia del fiscal. Una organización sin memoria inalterable opera en un estado de amnesia deliberada, diseñada para proteger la impunidad, no el activo."*

La ingeniería del rastro transforma el caos digital en historia verificable.
Sin identidad (Cap 05), no sabemos quién fue. Sin rastro inmutable, no podemos probar qué hizo.
Para el Fiscal Digital, el log no es una herramienta de *debugging* técnico; es una **declaración jurada automatizada**.

El crimen perfecto digital no consiste en no dejar huellas, sino en tener permisos para borrarlas. Por eso, la arquitectura de registro debe ser hostil a la modificación.

---

## 8.1. La Falacia del Log Local y la Regla de Exportación

El error arquitectónico más común y letal es almacenar los registros de auditoría únicamente en el servidor donde ocurre la actividad.

**El Escenario de Depredación:**

1.  El atacante compromete el servidor.
2.  Escala privilegios a `root`.
3.  Ejecuta su ataque.
4.  Antes de salir, ejecuta `rm -rf /var/log/*` o edita el historial.

**El Mandato de Shipping en Tiempo Real:**

Un log local tiene una vida útil de milisegundos antes de ser comprometido.
La regla de oro es la **Exportación Inmediata**. El servidor debe enviar sus logs a un colector externo (SIEM, Data Lake) en tiempo real. Si el atacante borra el disco local, la evidencia ya está segura en el búnker de auditoría. **El log local es efímero; el log centralizado es evidencia.**

---

## 8.2. El Ladrón de Tiempo (Ataques NTP)

La cronología es la columna vertebral de la reconstrucción forense. Pero el tiempo es manipulable.

**El Ataque Cronológico:**

Un atacante cambia la fecha del servidor al año 2015, ejecuta el robo y restaura la fecha.

* *Resultado:* El log queda enterrado en archivos "antiguos" que las políticas de retención eliminan automáticamente.

**Soberanía del Tiempo (Time Stamping):**

El protocolo NTP (*Network Time Protocol*) es un control de seguridad crítico.

1.  Los servidores no deben poder cambiar su hora arbitrariamente.
2.  La hora debe estar sincronizada con fuentes confiables (Stratum 0/1).
3.  Todos los logs deben registrarse en **UTC** (Tiempo Universal Coordinado) para permitir la correlación global.
Sin sincronización garantizada, la coartada del atacante es técnica: *"Ese log no coincide con mi horario laboral".*

---

## 8.3. Inmutabilidad Legal (WORM)

Volvemos al principio de Auditabilidad (Cap 02).
Para que un log sea admisible en un juicio o ante un regulador, debemos probar que no ha sido alterado, ni siquiera por el Administrador del Sistema.

**Tecnología WORM (Write Once, Read Many):**

El repositorio final de logs debe estar configurado en modo de **Retención Legal**.
Esto significa que, una vez escrito el dato, es tecnológicamente imposible sobrescribirlo o borrarlo hasta que expire el periodo de retención (ej. 5 años), incluso con credenciales de superusuario.

---

## 8.4. Principio de Custodia Externa

Este es el equivalente digital a la cadena de custodia física: **El investigado no puede custodiar la prueba.**

**Separación de Dominios Administrativos:**

El equipo que opera el sistema productivo (SysAdmins, DevOps) **no puede** tener credenciales de administración sobre el sistema de logs (SIEM/Log Server).
El dominio administrativo del repositorio de evidencia debe ser externo e independiente (ej. bajo control del CISO o Auditoría). Si el mismo administrador que gestiona el servidor de pagos gestiona el servidor de logs, existe un conflicto de interés estructural que invalida la prueba.

---

## 8.5. La Evidencia Negativa

En ciberseguridad, el silencio es a menudo más ruidoso que la alerta.
Los sistemas generan ruido constante (heartbeats, conexiones de fondo).

**El Hallazgo del Vacío:**

Si un servidor que genera 1GB de logs al día, repentinamente genera 0 bytes entre las 03:00 y las 04:00 AM, no es que el sistema esté "tranquilo"; es que el sistema ha sido **lobotomizado**.
La interrupción abrupta de la telemetría es, por defecto, un Indicador de Compromiso (IoC). El atacante ha deshabilitado el agente de monitoreo para operar a ciegas. El Fiscal Digital audita los huecos en la línea de tiempo como evidencia de manipulación.

---

## 8.6. Correlación: De Dato a Narrativa

Tener 50 terabytes de logs no es tener evidencia; es tener ruido.
El log bruto es ilegible para el humano. La evidencia surge de la **Correlación de Eventos**.

* *Dato A (Puerta):* Empleado entra al edificio a las 02:00 AM.
* *Dato B (Red):* Conexión VPN desde IP de China a las 02:05 AM usando credenciales del mismo empleado.

**La Imposibilidad Física:**

Por separado, son eventos operativos. Juntos, narran una **historia de compromiso de identidad**. Una persona no puede estar físicamente en la oficina y digitalmente en otro continente al mismo tiempo (Velocity Check).
Una organización que acumula logs pero no tiene reglas de correlación no tiene capacidad de detección; solo tiene capacidad de autopsia tardía.

---

## Conclusión del Capítulo

El rastro digital es la última línea de defensa de la verdad.
Si la organización permite logs locales, tiempos desincronizados o custodia compartida, está diseñando activamente su propia ceguera.

Operar sistemas críticos sin centralización de logs inmutables (WORM) y custodia segregada constituye una decisión de **no preservar la evidencia**.
Ante un litigio, la pérdida de logs no se interpretará como un fallo técnico ("se borraron"), sino como una **destrucción de pruebas** ("se permitieron borrar"). Y la destrucción de pruebas invierte la carga de la prueba en contra de la empresa.