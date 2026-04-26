# Capítulo 07: Segregación de Funciones: La Matemática del Fraude

## El Fin de la Acción Unilateral

> *"El fraude perfecto no requiere un hacker externo; requiere un empleado interno con funciones incompatibles. Si la misma identidad puede iniciar, aprobar y ocultar una transacción, la organización no tiene un proceso de control; tiene una invitación estructural a la impunidad. La seguridad no se trata de confiar en las personas, sino de impedir matemáticamente que actúen solas."*

Ya hemos limitado el privilegio (Cap 06). Ahora debemos impedir la acción solitaria.
La Segregación de Funciones (SoD) no es una "buena práctica" burocrática; es la **Ingeniería de la Colusión Forzada**.

El objetivo forense de la SoD es la **Atribución No Ambigua**.

* Si una sola persona completa un ciclo crítico, la atribución es impugnable ("fue un error", "fue el script").
* Si el proceso exige dos personas (o persona + sistema), el fraude requiere colusión.
* Y la colusión deja, por definición, una huella probatoria exponencialmente mayor (comunicaciones, acuerdos, rastros duales).

---

## 7.1. La Combinación Tóxica: Capacidad vs. Ejecución

El riesgo no reside en el permiso individual, sino en la **intersección**.
Tener permiso para "Crear Proveedor" es necesario. Tener permiso para "Pagar Factura" es necesario. Tener ambos es una **Combinación Tóxica**.

**Sentencia de Auditoría:**
Cualquier usuario que posea una combinación tóxica activa tiene la capacidad técnica de cometer fraude y borrar su rastro.
Para el Fiscal Digital, la existencia del permiso combinado es el hallazgo. No es necesario probar que se usó; el hecho de que el sistema lo permita invalida la integridad del control financiero. **La capacidad de acción unilateral anula la presunción de fiabilidad del sistema.**

---

## 7.2. El Desarrollador en Producción: La Muralla China Digital

En la era DevOps, el mantra *"You build it, you run it"* se ha pervertido como *"El desarrollador tiene acceso root a Producción"*. Esto es inaceptable.

**El Conflicto del Creador:**
Si quien escribe el código tiene permiso de escritura en el entorno productivo, puede introducir lógica fraudulenta, desplegarla y borrar la evidencia, todo sin supervisión.

**La Regla del Pipeline como Árbitro:**
El desarrollador nunca toca Producción.

1.  El Dev hace `commit` al repositorio.
2.  Un pipeline automatizado (CI/CD) ejecuta pruebas de seguridad.
3.  Una cuenta de servicio (no humana) despliega el código.

Si existe una "puerta trasera" técnica que permita a un humano saltarse el Pipeline y editar archivos en vivo, **la segregación ha muerto**. El Pipeline es la única garantía de integridad del código.

---

## 7.3. Autorización Multi-Parte (Two-Man Rule)

Tomada de la doctrina nuclear: ninguna persona sola puede girar la llave.
En acciones irreversibles (ej. desencriptar bases de datos, transferencias > $1M, borrado de backups), la acción unilateral debe estar **técnicamente prohibida**.

**Implementación Forense:**
El sistema debe exigir criptográficamente dos aprobaciones concurrentes (MFA de Admin A + MFA de Admin B).

* *Valor Probatorio:* Si la acción ocurre, el sistema genera automáticamente **evidencia de colusión**.
* *Valor Disuasivo:* Obliga al atacante interno a reclutar un cómplice, elevando el riesgo de detección humana.

---

## 7.4. La Matriz de SoD y la Higiene del RBAC

No se puede auditar lo que no se define. La organización debe tener una **Matriz de Segregación de Funciones** que actúe como la "Constitución" de los permisos.

**El Problema del "Privilege Creep" (Acumulación Biográfica):**
Los roles RBAC (*Role-Based Access Control*) deben diseñarse por **función atómica**, no por la biografía del empleado.
Si "Juan" pasa de Contabilidad a Ventas y conserva sus permisos anteriores, acumula conflictos de interés. Al clonar el perfil de Juan para un empleado nuevo, clonamos la vulnerabilidad.

**Auditoría de la Brecha (Gap Analysis):**
El Fiscal Digital cruza la Matriz Teórica (lo que dice el papel) con la Configuración Real del RBAC (lo que permite el sistema).
Si la Matriz prohíbe que "Dev" toque "Prod", pero el grupo `Developers` tiene permisos de `Write` en AWS, la Matriz es papel mojado. **Una SoD que no se verifica en la configuración es una SoD inexistente.**

---

## Conclusión del Capítulo

La Segregación de Funciones es la matemática de la atribución no ambigua.
Un sistema que permite la acción unilateral en procesos críticos no solo habilita el fraude: habilita la defensa legal del defraudador ("no pueden probar que fui solo yo").

Mantener combinaciones tóxicas conocidas o permitir acceso de desarrolladores a producción tras una advertencia formal, constituye una decisión de operar bajo un esquema de **atribución impugnable**.

En caso de incidente, la organización no podrá sostener la validez de sus propios controles ante un tribunal; solo podrá alegar confianza ciega. Y la confianza no es evidencia.