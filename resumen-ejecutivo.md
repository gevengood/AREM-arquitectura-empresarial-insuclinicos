# Resumen Ejecutivo del Proyecto Arquitectónico

## Nombre del Cliente
**Insuclínicos Ltda.** — Fabricación y comercialización de prendas e insumos médicos quirúrgicos desechables en tela no tejida SMS (Bogotá D.C., Colombia · Representante Legal: Santiago Martínez · 6 trabajadores · ~40 clínicas, consultorios odontológicos y spas).

## Objetivo General del Proyecto
Diagnosticar la arquitectura empresarial actual (AS-IS) de **Insuclínicos Ltda.** en su macro-proceso crítico de *Gestión y Cumplimiento de Pedido*, identificar riesgos técnicos, operativos, de seguridad y regulatorios, y definir una arquitectura objetivo (TO-BE) implementable de forma gradual y dentro del presupuesto PyME (`<= $3.000.000 COP/año`), que elimine los silos de Excel, proteja la continuidad de la información y garantice la trazabilidad sanitaria exigida por el INVIMA sin detener la producción.

## Vistas Arquitectónicas Cubiertas

| Vista | Alcance de la Solución |
|---|---|
| **Procesos de Negocio** | Modelado BPMN AS-IS del subproceso de Producción (4 roles funcionales, gateways de inventario y calidad, ciclo de reproceso) y flujo TO-BE integrado de ventas a remisión sin papel (`01-bpmn/`, `07-opportunities-solutions/`). |
| **Información / Datos** | Modelo Entidad-Relación de 8 entidades nucleares (`CLIENTE`, `PEDIDO`, `DETALLE_PEDIDO`, `PRODUCTO`, `ORDEN_PRODUCCION`, `CONSUMO_MATERIA_PRIMA`, `MATERIA_PRIMA`, `DESPACHO`) extendido en TO-BE con `lote_sms_invima`, consentimiento Ley 1581 y `BITACORA_AUDITORIA` (`02-modelo-informacion/`, `08-integracion-vistas/`). |
| **Aplicaciones / Sistemas** | Contexto C1 y Contenedores C2 AS-IS sobre ecosistema *Shadow IT* (2 Excels desconectados + WhatsApp + papel + portal DIAN) y diseño TO-BE basado en **CRM/ERP Ligero Cloud (Odoo/Dolibarr sobre PostgreSQL)** + exportador CSV DIAN + Tablet Web (`03-arquitectura-c4/`, `07-opportunities-solutions/`). |
| **Infraestructura** | Mapa físico AS-IS de 3 zonas (Nube externa, Red Local LAN, Planta) con identificación de SPOF en disco local, evolucionado a infraestructura Cloud gestionada Multi-AZ con bóveda de backup 3-2-1, enlace móvil 4G/5G de contingencia y Wi-Fi WPA3 en planta (`04-infraestructura/`, `07-opportunities-solutions/`). |
| **Seguridad** | Evaluación de 6 amenazas STRIDE (`T1`–`T6`: suplantación, alteración de fórmulas, repudio sin logs, fuga por USB/chat, ransomware/SPOF, permisos abiertos SMB) y controles integrados RBAC, bloqueo automático, cifrado TLS 1.3/AES-256 y bitácora inmutable (`05-seguridad-stride/`). |
| **Cumplimiento Normativo** | Auditoría de 15 criterios frente a **INVIMA** (Decreto 4725/2005 y Resolución 4816/2008 Tecnovigilancia), **Ley 1581 de 2012** (Habeas Data y derechos ARCO), **DIAN** (Resolución 000165/2023) e **ISO/IEC 27001:2022** (`06-normatividad/`). |
| **Integración y Gobernanza** | Tablero vertical integrado de 5 capas y 3 hilos *end-to-end*, matriz consolidada de riesgos en 7 dominios, vistas ArchiMate de Motivación y Migración, 3 principios rectores, 3 métricas de gobierno y 2 ADR registradas (`08-integracion-vistas/`, `09-presentacion-final/`). |

## Hallazgos Clave

- **Silos de Excel y bloqueos diarios de concurrencia:** La operación depende de `Libro de Pedidos y Cotizaciones.xlsx` y `Libro de Control de Inventario.xlsx` desconectados en LAN, provocando **2 a 3 bloqueos diarios** de *"Solo lectura"*, desfase de inventario de rollos SMS y **~6 horas semanales** perdidas en conciliación manual y redigitación hacia el portal de facturación DIAN.
- **Riesgo crítico de pérdida total (SPOF) e inseguridad operativa:** El 100 % de los datos reside en un único disco duro local sin respaldos automáticos 3-2-1 (`T5` Nivel `8`), con sesiones genéricas compartidas en Windows (`T1`), carpetas SMB abiertas (`T6`), fórmulas de precios/stock editables sin registro histórico de autoría (`T2`/`T3` Nivel `9`) y riesgo de extracción de la cartera de ~40 clínicas vía USB (`T4`).
- **Exposición regulatoria INVIMA y Ley 1581 (`2 / 15` criterios cumplidos en AS-IS):** Aunque Insuclínicos cumple con facturación electrónica DIAN y conservación contable, carece de vínculo sistematizado entre el lote del rollo SMS del proveedor y la remisión entregada a cada clínica (exigencia sanitaria de Tecnovigilancia INVIMA), y capta contactos por WhatsApp sin aviso ni registro de autorización de datos personales (Ley 1581).

## Recomendaciones Principales

- **Asegurar continuidad inmediata y cumplimiento Habeas Data (`WP1`):** Activar copias diarias automatizadas bajo regla **3-2-1** en nube cifrada, crear 6 perfiles nominales de usuario con bloqueo a los 5 min, cerrar carpetas SMB/puertos USB e implementar respuesta automática con aviso **Ley 1581** en WhatsApp Business y buzón ARCO (`contacto@insuclinicos.com`).
- **Adoptar CRM/ERP ligero en la nube con PostgreSQL y exportador CSV DIAN (`WP2-A` y `WP2-B`):** Seleccionado en la matriz ponderada de 8 pasos (`4.40 / 5.00`, `~$2.200.000 COP/año`, frente a `$15M+` de desarrollo a medida y descarte de OneDrive por no garantizar trazabilidad INVIMA `C1 < 3`). Unifica pedidos e inventario sin bloqueos, protege precios con RBAC/bitácora `audit_log` y suprime la doble digitación fiscal.
- **Digitalizar planta e integrar trazabilidad sanitaria INVIMA (`WP3`):** Desplegar una **Tablet Web** sobre Wi-Fi WPA3 en corte y confección que impida cerrar órdenes sin registrar `lote_sms_invima` e imprima el lote automáticamente en la **Remisión Digital PDF**, elevando las 6 capacidades clave del negocio de madurez `1–3` a `4 / 5`.

## Plan de Implementación (resumen)

El despliegue se secuencia en **4 fases ejecutables durante 12 semanas** cruzando prioridad de riesgo con esfuerzo real e incorporando gestión del cambio sobre los 6 empleados, de forma que la operación no se detenga:

| Fase | Qué se implementa | Duración estimada |
|---|---|---|
| **Quick win** (`WP1`) | Backups automáticos 3-2-1 en nube, 6 cuentas nominales Windows, cierre de SMB/USB y aviso automático Ley 1581 en WhatsApp Business + buzón ARCO. | Semanas 1–2 (14 días) |
| **Corto plazo** (`WP2-A`) | Aprovisionamiento Cloud de CRM/ERP y PostgreSQL Multi-AZ, saneamiento/deduplicación del catálogo de ~40 clínicas y saldos SMS, y mapeo del archivo CSV DIAN. | Semanas 3–4 (14 días) |
| **Mediano plazo** (`WP2-B`) | Despliegue en producción del CRM/ERP Cloud (Comercial, Inventario concurrente, RBAC, `audit_log`), exportador CSV hacia DIAN y marcha blanca paralela retirando Excel. | Semanas 5–8 (28 días) |
| **Largo plazo** (`WP3`) | Cobertura Wi-Fi WPA3 en planta, Tablet Web de confección/calidad con registro obligatorio de `lote_sms_invima` y generación automática de Remisión Digital PDF. | Semanas 9–12 (28 días) |

_Ver el detalle completo, con la relación de cada fase a los riesgos identificados en el curso y la gestión del cambio con las personas, en [`09-presentacion-final/plan-implementacion.md`](09-presentacion-final/plan-implementacion.md)._

## Reflexión Final

Este ejercicio permitió al Grupo 8 aplicar de manera práctica los principios y métodos de la arquitectura empresarial sobre una PyME manufacturera real del sector salud en Colombia (**Insuclínicos Ltda.**), demostrando que la transformación tecnológica no consiste en proponer herramientas costosas ni reescribir sistemas desde cero, sino en conectar los dolores operativos, la regulación sanitaria y fiscal, el control de riesgos de seguridad y la gestión del cambio humano en una hoja de ruta financieramente viable y gobernable en el tiempo.

---

_Este resumen ejecutivo forma parte de la entrega final del curso AREM - Arquitectura Empresarial - Universidad de La Sabana._
