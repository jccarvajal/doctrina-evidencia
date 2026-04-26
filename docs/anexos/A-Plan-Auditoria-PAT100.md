# ANEXO A: Plan Anual de Auditoría Continua sobre Población Total (PAT-100)

> **CLASIFICACIÓN DEL DOCUMENTO:** MARCO OPERATIVO / ESTRATÉGICO
>
> **OBJETIVO:** PRIORIZACIÓN DE DESPLIEGUE DE AUDITORÍA CONTINUA
>
> **ALCANCE:** SISTEMAS CRÍTICOS Y REPOSITORIOS DE EVIDENCIA
>
> **REFERENCIA:** DOCTRINA DE LA EVIDENCIA (FISCALÍA DIGITAL)

---

## 1. El Fin del Muestreo Estadístico

La auditoría tradicional prioriza qué muestras tomar basándose en la limitación humana para revisar grandes volúmenes de papel. El **Plan de Auditoría Continua** prioriza en qué dominios se desplegarán las reglas de validación sobre la población total. 

El nivel de riesgo no define el "tamaño de la muestra", sino el **orden cronológico** en el que se automatiza el control. Si existe la capacidad técnica de evaluar un registro mediante código, existe la capacidad de evaluarlos todos. El muestreo en bases de datos es negligencia por diseño.

---

## 2. Cobertura Técnica y Población Total

En el entorno digital, el estándar de diseño de control exige la cobertura total del universo auditable. Aceptar porcentajes intermedios es aceptar puntos ciegos sistémicos. El Plan Anual no busca revisar el 75% de los servidores; busca desplegar una regla de auditoría continua que abarque el 100% de la población.

| Dominio de Control | Universo Auditable | Cobertura Exigida | Método de Evidencia (Artefacto) |
| :--- | :--- | :--- | :--- |
| **Identidad Privilegiada (IAM)** | 100% de las cuentas admin | **100%** | Extracción API del Proveedor de Identidad (IdP) |
| **Infraestructura y Configuración** | 100% de los nodos/servidores | **100%** | Escaneo de Repositorio (Infraestructura como Código) |
| **Datos Críticos (Nivel L3)** | 100% de las transacciones | **100%** | Reglas de Auditoría Continua (Logs/SIEM) |
| **Resiliencia Operativa** | 100% de los respaldos | **100%** | Logs automáticos y Test de Restauración con timestamp |

---

## 3. Axioma de Cobertura y Presunción de Falla

El Plan Anual establece la siguiente regla innegociable para los equipos de auditoría y tecnología:

> **Cualquier cobertura inferior al 100% en un entorno digitalizado y centralizado se presumirá automáticamente como "Falla de Diseño de Control", independientemente del resultado arrojado por una muestra parcial.**

Si un sistema no permite la extracción total de sus registros para ser validados mediante rutinas de auditoría continua, el sistema en sí mismo constituye un riesgo de caja negra y debe ser reportado como un hallazgo estructural, no operativo.

---

## 4. Resultado y Entregables del Plan

El Plan Anual de Auditoría bajo este modelo no produce un calendario de "visitas a terreno" ni entrevistas de validación. El plan se convierte en un *roadmap* de ingeniería de control y debe producir:

1.  **Priorización de Dominios:** La secuencia en la que se integrarán los sistemas al motor de auditoría continua.
2.  **Requerimiento de Artefactos:** La especificación técnica de las APIs, logs o repositorios que las áreas de TI deben exponer al equipo de auditoría.
3.  **Scripts de Validación (Reglas):** El código (SQL, Python, Rego) que se ejecutará contra la población total para cada dominio priorizado.
4.  **Dashboard Forense de Estado de Control:** El paso de un informe estático en PDF a una visualización de estado continuo basada en evidencia inmutable.