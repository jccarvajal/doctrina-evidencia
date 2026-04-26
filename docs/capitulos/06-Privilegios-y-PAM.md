# Capítulo 06: Privilegios, PAM y el Fin del "Modo Dios"

## La Tiranía del Administrador Absoluto

> *"El poder absoluto no solo corrompe; anula la evidencia. Si un administrador posee privilegios permanentes ('root', 'Domain Admin') sin supervisión, tiene la capacidad técnica de alterar la realidad operativa y borrar sus huellas. En tal escenario, la organización no tiene control; tiene fe ciega en la bondad de un empleado. Y la fe no es una estrategia de gobierno."*

Hemos fijado la Identidad (Cap 05). Ahora debemos limitar la **Capacidad de Destrucción**.
El modelo tradicional de TI se basa en una vulnerabilidad estructural: entregar las "llaves del reino" a un humano las 24 horas del día.

Para el Fiscal Digital, el "Modo Dios" permanente no es una conveniencia operativa; es un **conflicto de interés técnico**. Un administrador con privilegio absoluto es, simultáneamente, el operador del sistema y el custodio de la evidencia de sus propios errores.

---

## 6.1. Privilegios Permanentes como Inhabilidad Probatoria Estructural

La mayoría de las empresas operan con "Standing Privileges" (Privilegios de Pie/Permanentes).

* *Escenario:* El DBA tiene la credencial `sa` (System Administrator). Puede entrar un domingo a las 3 AM, borrar una tabla financiera y luego purgar el log de transacciones.

**La Doctrina de la Cadena de Custodia:**
La existencia de privilegios permanentes no es solo una debilidad técnica; es una **inhabilidad probatoria estructural**.
Un sistema donde el mismo sujeto puede ejecutar la acción, modificar el registro y eliminar la evidencia es, por definición, un sistema incapaz de sostener una reconstrucción forense confiable. No se trata de riesgo de ataque. Se trata de imposibilidad de prueba.

---

## 6.2. JIT (Just-in-Time) como Requisito de Gobernanza

El privilegio permanente transforma la excepción en norma. En gobierno corporativo, la excepción sin trazabilidad es opacidad autorizada.

**El Mandato JIT:**
El privilegio no es una propiedad del usuario ("Soy Admin"); es un estado temporal otorgado para una función específica.
JIT no es una mejora operativa; es una **condición mínima para que la cadena de custodia exista**.
El Fiscal Digital exige **Cero Privilegios Permanentes**. Todo escalamiento debe ser efímero, justificado y revocado automáticamente (TTL).

---

## 6.3. La Bóveda PAM: Separación Digital de Poderes

No basta con rotar contraseñas. El sistema PAM (*Privileged Access Management*) no es una herramienta de seguridad; es una forma digital de **separación de poderes**.

**La Regla de la Ignorancia Técnica:**
El administrador no debe poseer simultáneamente el poder de actuar y el poder de borrar la evidencia de su actuación.

1.  El Admin se autentica en la Bóveda (con MFA).
2.  El PAM inyecta la credencial en el servidor destino.
3.  **El Admin nunca ve ni conoce la contraseña real.**

Al no conocer la contraseña, el administrador *está obligado* a pasar por el canal auditado. Si un administrador tiene un Excel con claves de servidores, la organización ha perdido la separación de poderes.

---

## 6.4. Movimiento Lateral como Amplificador de Responsabilidad

El privilegio mal gestionado permite que un compromiso local se convierta en una catástrofe sistémica.

**La Uniformidad como Negligencia Directiva:**
Es práctica común usar la misma contraseña de Administrador Local en todas las estaciones de trabajo.
La uniformidad de credenciales no solo amplifica el daño técnico; **amplifica la responsabilidad directiva**.
Cuando un diseño facilita el movimiento lateral masivo (Pass-the-Hash), el incidente deja de ser una contingencia y se convierte en una **consecuencia previsible**.

El Fiscal Digital exige LAPS (*Local Administrator Password Solution*) para aleatorizar cada credencial. Permitir la uniformidad es facilitar deliberadamente el trabajo del atacante.

---

## 6.5. Meta-Auditoría (Quis Custodiet Ipsos Custodes)

Centralizar todos los secretos en una Bóveda PAM crea el riesgo definitivo: ¿Quién controla al dueño del PAM?

**El Principio de Autovalidación:**
Si el administrador del PAM puede alterar sus propios logs, el sistema de control es autorreferencial.
Un sistema autorreferencial no es control; es autovalidación. Y la autovalidación **carece de valor probatorio** ante un tribunal o regulador.

**Controles de Meta-Auditoría:**

1.  **Aprobación Dual:** Ninguna configuración crítica del PAM puede ser alterada por una sola persona.
2.  **Exfiltración de Logs (WORM):** Los logs del PAM deben ser enviados en tiempo real a un SIEM externo de solo lectura.

---

## Conclusión del Capítulo

El privilegio absoluto es incompatible con la responsabilidad verificable.

Mantener un esquema de privilegios permanentes ("Standing Privileges") después de ser advertido del riesgo no es deuda técnica. Es una **decisión consciente de operar sin capacidad de reconstrucción forense**.

En tal escenario, el incidente no será un accidente imprevisible. Será la manifestación lógica de un diseño que priorizó conveniencia sobre verificabilidad. **Y la conveniencia no es defensa en juicio.**