# Informe de análisis de seguridad
## Posible actividad sospechosa de autenticación

**Tipo de actividad:** Análisis de registros de autenticación  
**Entorno:** Laboratorio educativo con datos ficticios  
**Fecha de los eventos:** 28 de octubre de 2026  
**Analista:** Guillermo Miller  
**Estado:** Investigación inicial — pendiente de validación

> **Nota:** Este informe corresponde a un ejercicio de laboratorio con datos sintéticos. No describe un incidente real ni experiencia profesional.

### 1. Resumen ejecutivo

Se identificó actividad de autenticación sospechosa desde la dirección IP `203.0.113.45`, con diez intentos fallidos dirigidos a tres cuentas diferentes en un intervalo de 2 minutos y 5 segundos.

Posteriormente, a las 09:17:14, se registró un inicio de sesión exitoso de la cuenta `aramos` desde la misma dirección IP.

El patrón podría ser compatible con un intento de *password spraying*. Sin embargo, la técnica utilizada y la legitimidad del acceso exitoso no pueden confirmarse con los registros disponibles.

### 2. Evidencia observada

- **Origen investigado:** `203.0.113.45`.
- **Equipo afectado:** `SRV-01`.
- **Cuentas con intentos fallidos:** `mlopez`, `aramos` y `admin`.
- **Cantidad de intentos fallidos desde el origen investigado:** 10.
- **Primer intento fallido:** 09:14:03.
- **Último intento fallido:** 09:16:08.
- **Inicio de sesión exitoso posterior:** cuenta `aramos`, a las 09:17:14.
- **Intervalo entre el último fallo y ese éxito:** 1 minuto y 6 segundos.

### 3. Análisis

La repetición de fallos desde un mismo origen contra varias cuentas constituye un indicador de actividad que requiere investigación.

El inicio exitoso posterior de `aramos` desde ese origen incrementa la prioridad de revisión, porque podría representar un acceso legítimo o un posible acceso no autorizado.

Los registros disponibles no permiten determinar la identidad de quien realizó los intentos, las contraseñas utilizadas ni si hubo compromiso de una cuenta.

### 4. Evaluación inicial

- **Hipótesis principal:** posible *password spraying* o actividad automatizada de autenticación.
- **Confianza:** moderada respecto de la existencia de un patrón sospechoso; insuficiente para confirmar la técnica o un compromiso.
- **Severidad:** pendiente de validación. Se recomienda priorizar la revisión del acceso exitoso de `aramos` antes de asignar una clasificación definitiva.

### 5. Acciones recomendadas

1. Revisar los registros adicionales de autenticación asociados a `aramos`.
2. Verificar, mediante el contexto autorizado de la cuenta, si el acceso desde `203.0.113.45` era esperado.
3. Examinar la actividad posterior al inicio de sesión exitoso.
4. Correlacionar los eventos con otros registros disponibles, como los del sistema operativo, firewall o SIEM.
5. Si se confirma actividad no autorizada, seguir el procedimiento de respuesta a incidentes de la organización.

### 6. Limitaciones

Este análisis se basa únicamente en un conjunto de registros ficticios de práctica. No se dispone de información sobre reputación de IP, contexto habitual de los usuarios, contraseñas probadas ni acciones posteriores a la autenticación.

Las direcciones IP pertenecen a rangos reservados para documentación y ejemplos; no deben interpretarse como fuentes reales de actividad maliciosa.

### 7. Conclusión

Los registros presentan un patrón de autenticación sospechoso que justifica una investigación adicional. El inicio exitoso de `aramos` desde el origen investigado es el evento prioritario para validar. No se puede afirmar que una cuenta haya sido comprometida con la evidencia actual.
