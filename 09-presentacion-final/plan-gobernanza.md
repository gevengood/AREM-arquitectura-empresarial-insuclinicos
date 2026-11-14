# Plan de Gobernanza de la Implementación

## Cliente
**Insuclínicos Ltda.** — Fabricación y comercialización de prendas e insumos médicos quirúrgicos desechables en tela no tejida SMS (Bogotá D.C., Colombia).

## Integrantes del equipo (Grupo 8)
- **Jorge Steven Doncel Bejarano** (`@gevengood` · [jorgedobe@unisabana.edu.co](mailto:jorgedobe@unisabana.edu.co))
- **David Santiago Buendia Londoño** (`@Santiagoob7` · [davidbulo@unisabana.edu.co](mailto:davidbulo@unisabana.edu.co))

## Propósito de este documento

Define el marco de supervisión que garantiza que la ejecución de las 12 semanas del Plan de Implementación ([`plan-implementacion.md`](plan-implementacion.md)) respete los principios, estándares y arquitectura objetivo TO-BE del Taller 7. El gobierno en Insuclínicos opera a escala PyME (6 trabajadores): un comité ligero liderado por el Representante Legal verifica cada fase contra criterios medibles y canaliza cualquier desviación de presupuesto o alcance mediante registro formal de excepción (ADR) antes de aplicarla.

---

## Principios Arquitectónicos

En la Visión del Taller 0 ([`../00-preliminary-vision/vision.md`](../00-preliminary-vision/vision.md)) y la Ficha de Caracterización ([`../00-preliminary-vision/ficha-caracterizacion.md`](../00-preliminary-vision/ficha-caracterizacion.md)) se formularon criterios rectores preliminares sobre aprovechamiento de equipos existentes, gradualidad sin detener la planta y trazabilidad centrada en pedidos (dejando en ese corte inicial fuera de alcance el reemplazo completo de Excel por un ERP). Con la evidencia recopilada de los Talleres 1 a 8, esos criterios iniciales se **confirman, reescriben, amplían o retiran** en cuatro reglas operativas verificables:

| Principio | Declaración | Implicación (qué descarta) | Justificación en el proyecto (evidencia de los talleres) | Estado frente al Taller 0 (confirmado / reescrito / nuevo) |
|---|---|---|---|---|
| **P1 · Sobriedad Tecnológica y Reúso (Adoptar antes que Desarrollar)** | Toda solución tecnológica para Insuclínicos debe reutilizar los PCs de oficina actuales, adoptar software SaaS/PaaS configurable y operar por debajo del techo presupuestal anual de `$3.000.000 COP/año`, sin interrumpir la producción física. | **Descarta y prohíbe** contratar desarrollo de software a medida desde cero (`>$15M COP`), adquirir servidores físicos locales, licenciar suites *enterprise* (ej. SAP B1 `>$30M`) o intervenir maquinaria industrial de corte/tendido en este ciclo. | Restricciones explícitas de la Ficha (Taller 0), análisis de hardware heredado (Taller 4) y Matriz Ponderada de 8 pasos donde la Opción B fue descartada por costo 5× superior y plazo de 16–24 semanas (Taller 7). | **Reescrito** *(evoluciona desde la restricción de presupuesto y aprovechamiento de equipos de la Visión Taller 0)* |
| **P2 · Fuente Única de Verdad y Trazabilidad Sanitaria Obligatoria** | Los datos maestros de clientes, pedidos, existencias SMS, órdenes de producción y remisiones residen en una única base de datos relacional transaccional que exige asociar el lote de tela quirúrgica antes de cerrar cualquier despacho. | **Prohíbe** mantener libros paralelos de Excel compartidos en LAN para pedidos o inventarios, despachar prendas sin descuento transaccional de stock o emitir remisiones manuales sin vínculo al `lote_sms_invima` (descartando también hojas en OneDrive). | Silos de Excel y doble digitación en C2 (Taller 3), bloqueos diarios de "Solo lectura" en LAN (Taller 4), entidad asociativa `CONSUMO_MATERIA_PRIMA` (Taller 2), exigencia INVIMA Dec. 4725/2005 y Res. 4816/2008 (Taller 6) y criterio eliminatorio `C1 < 3` en Taller 7. | **Reescrito y confirmado** *(formaliza la trazabilidad de punta a punta del OE-03 y OE-02 del Taller 0 con rigor sanitario)* |
| **P3 · Seguridad por Diseño Pragmática y Protección de Datos** | Todo canal comercial, equipo de usuario y repositorio de datos incorpora desde el día cero cuentas nominales por rol (RBAC), cifrado en tránsito/reposo, copias de seguridad 3-2-1 automatizadas y autorización previa de tratamiento de datos (Ley 1581). | **Prohíbe** operar con cuentas genéricas compartidas en Windows, carpetas de red SMB abiertas sin control, extracción masiva de bases a USB personales o captura comercial por WhatsApp sin aviso automático de privacidad ni canal ARCO. | Punto único de falla en disco duro local sin backups (`T5` Taller 4 y 5), vulnerabilidades STRIDE `T1`–`T6` (Taller 5) y 13 brechas ⚠️ Parcial en Ley 1581 / ISO 27001 A.5.15, A.8.13, A.8.15 y A.8.24 (Taller 6). | **Nuevo** *(emergió de los hallazgos críticos de Talleres 5 y 6, ausente como regla explícita en el Taller 0)* |

**Criterio preliminar del borrador del Taller 0 que se retira, y por qué:**

| Principio / criterio retirado | Qué evidencia lo contradijo |
|---|---|
| *Conservar los archivos Excel operativos como plataforma central indefinida limitando la intervención tecnológica a un prototipo aislado (alcance inicial en `00-preliminary-vision/vision.md`)* | La evidencia técnica de los **Talleres 3, 4 y 5** demostró que Excel sobre LAN genera bloqueos diarios, carece de auditoría contra alteración (`T2`) y repudio (`T3`), y representa un SPOF crítico (`T5`). El **Taller 6** evidenció además que sin base relacional es inviable cumplir Tecnovigilancia INVIMA, y en el **Taller 7** la Opción C (*Excel en OneDrive*) reprobó el criterio eliminatorio `C1` (`2 < 3`). Por tanto, se retira la idea de mantener Excel en producción y se reemplaza por un CRM/ERP cloud ligero (`WP2`). |

---

## Estándares Tecnológicos

Cada estándar elegido se traza hacia arriba en la escalera de gobierno (**Estándar → Principio → Objetivo de negocio en Taller 0**) y admite excepciones únicamente mediante aprobación de una **ADR** documentada en [`procedimiento-cambios.md`](procedimiento-cambios.md).

| Categoría | Estándar definido | Por qué (traza a Principios y Objetivos) |
|---|---|---|
| **Plataforma / Base de Datos (Lenguaje / Framework)** | **Odoo Community Cloud o Dolibarr Cloud** (stack web modular estándar) sobre **PostgreSQL gestionado con integridad ACID y cifrado AES-256**; acceso exclusivamente vía navegador web moderno (PCs Windows actuales + Tablet Android/Web). | Evita desarrollar ni mantener código propio (`P1 · Sobriedad`), provee control nativo de lotes sanitarios, concurrencia multiusuario y bitácora inmutable `audit_log` (`P2` / `OE-01, OE-02, OE-03`), y soporta RBAC por rol (`P3`). |
| **Tipo de comunicación e integración** | **HTTPS con TLS 1.3** para todas las sesiones cliente-servidor; **exportación estructurada en CSV estándar** (o API REST si el operador tecnológico la habilita sin sobrecosto) hacia la plataforma de Facturación Electrónica DIAN; **Wi-Fi WPA3** interno entre planta y router; **WhatsApp Business** con respuesta automática Ley 1581 (sin adjuntar bases completas). | Elimina el acceso directo a carpetas compartidas SMB (`T6` / `P3`), suprime integraciones API costosas hechas a mano cuando DIAN permite carga estructurada (`P1` / `GAP-02`) y evita transcripción manual conservando el canal ágil con clientes (`OE-03`). |
| **Infraestructura y continuidad** | **Nube gestionada SaaS/PaaS (Multi-AZ)** con **bóveda de respaldo automático diario bajo regla 3-2-1 (`RPO <= 24 h`, retención 30 días)** + enlace de internet principal con contingencia **móvil 4G/5G** en oficina, reutilizando los PCs existentes endurecidos con cuentas nominales, bloqueo de pantalla (5 min) y puertos USB restringidos. | Erradica el Punto Único de Falla del disco duro local (`GAP-03` / `T5` / `P3`) reutilizando el hardware de oficina y manteniéndose en `~$2.2M COP/año` (`P1`). |

---

## Mecanismo de gobierno

Al ser una microempresa de 6 empleados sin departamento de TI interno, se adopta un **Comité Ligero de Arquitectura** de tres roles reales:

| Rol | Responsabilidad | Persona / equipo sugerido |
|---|---|---|
| **Patrocinador y Dueño de Datos / Presupuesto (DPO)** | Aprueba el presupuesto anual (`<= $3M COP/año`), autoriza cambios y excepciones en ADR, firma las políticas de Ley 1581 y valida los hitos visibles de cierre de fase. | **Santiago Martínez** (Representante Legal, Insuclínicos Ltda.) |
| **Líder Funcional de Operación y Trazabilidad Sanitaria** | Verifica que los flujos del sistema correspondan al proceso real en almacén y confección, audita el registro obligatorio de lotes SMS y valida el simulacro de *recall* INVIMA. | **Jefe de Producción / Encargado de Almacén** (Insuclínicos Ltda.) |
| **Responsable Técnico y de Seguridad (Arquitecto / Implementador)** | Configura el CRM/ERP Cloud, backups 3-2-1, permisos RBAC y cuentas nominales; audita el cumplimiento técnico contra los diagramas TO-BE y redacta las propuestas de ADR. | **Consultor / Proveedor Técnico Cloud** *(acompañado por el equipo consultor durante el cierre académico)* |

## Cadencia de seguimiento

- **Durante la transición (`12 semanas` del roadmap):** sesión ejecutiva breve de **30 minutos cada 15 días** (Semanas 2, 4, 6, 8, 10 y 12) para revisar avance de los `Work Packages`, cierre de riesgos de [`matriz-riesgos.xlsx`](matriz-riesgos.xlsx) y comprobación del resultado visible por el negocio.
- **En operación regular (pos-semana 12):** revisión **trimestral de indicadores (`M1`, `M2`, `M3`) y costo cloud**, además de una **revisión arquitectónica anual completa** (octubre de 2027, según disparador del Taller 7 Paso 8).

## Criterio de conformidad

Ninguna fase del roadmap (`WP1`, `WP2-A`, `WP2-B`, `WP3`) se declara cerrada por simple opinión ni porcentaje de avance técnico. Para aprobar su cierre, el comité verifica objetivamente **tres condiciones contra el diseño TO-BE del Taller 7**:
1. **Correspondencia estructural TO-BE:** los módulos, tablas y nodos desplegados coinciden con los definidos en [`../07-opportunities-solutions/to-be-aplicaciones-final.drawio`](../07-opportunities-solutions/to-be-aplicaciones-final.drawio) y [`../07-opportunities-solutions/to-be-tecnologia-final.drawio`](../07-opportunities-solutions/to-be-tecnologia-final.drawio), retirando los activos Excel/papel asignados a esa fase.
2. **Verificación práctica de controles de seguridad y norma:** las amenazas STRIDE asignadas (`T1`–`T6`) y requisitos legales (aviso Ley 1581, RBAC nominal, bitácora `audit_log`, respaldo restaurable, lote INVIMA obligatorio) pasan una prueba en vivo registrada en el acta quincenal.
3. **Firma del resultado visible:** el actor fuera de TI designado en [`plan-implementacion.md`](plan-implementacion.md) confirma que comprobó el resultado operativo de la fase.

## Escalamiento

Cuando una fase necesite desviarse del diseño aprobado —por ejemplo, sobrecosto cloud por encima de `$3.000.000 COP/año`, incompatibilidad del formato CSV con el proveedor DIAN, necesidad temporal de mantener un archivo paralelo en Excel o cambio de proveedor tecnológico— **se detiene la modificación no autorizada** y se sigue este flujo:
1. **Propuesta:** El Responsable Técnico o cualquier líder operativo documenta la solicitud como una **ADR en estado `Propuesta`** en [`procedimiento-cambios.md`](procedimiento-cambios.md), indicando qué principio o estándar afecta, alternativas y costo.
2. **Evaluación técnica y operativa:** El Líder Funcional evalúa el impacto en producción/INVIMA y el Responsable Técnico valida el impacto en seguridad (`STRIDE`) y TO-BE.
3. **Autorización o rechazo:** El **Representante Legal (Santiago Martínez)** dictamina la excepción (`Aceptada` o `Rechazada`) en máximo **5 días hábiles** (o `< 24 horas` si detiene despachos/seguridad). Sin aprobación escrita, el estándar y el TO-BE permanecen vigentes.

---

## Métricas de gobierno

Las tres métricas verifican el cumplimiento real de los principios y miden que el gobierno no frene la operación PyME. Todas usan fuentes verificables existentes hoy (sin líneas base inventadas):

| Métrica | Qué mide (principio) | Fórmula | Fuente que ya existe | Línea base | Umbral |
|---|---|---|---|---|---|
| **M1 · Adopción transaccional única y trazabilidad de lote** | Cumplimiento de **P2 (Fuente Única de Verdad y Trazabilidad Sanitaria)** | `(Pedidos y despachos semanales registrados en sistema central con lote SMS vinculado ÷ Total de pedidos despachados en la semana) × 100` | Inventario de contenedores C2 AS-IS ([`../03-arquitectura-c4/c2-contenedores-final.drawio`](../03-arquitectura-c4/c2-contenedores-final.drawio)), `Libro de Pedidos.xlsx` y talonarios físicos de remisión | **`0 %` integrado / `100 %` fragmentado** (`2` libros Excel aislados + remisiones manuales en papel; `0 %` vinculan lote SMS en base relacional en AS-IS) | `< 100 %` de pedidos fuera de Excel al cerrar `WP2-B` (Semana 8), o cualquier remisión emitida sin lote SMS tras cerrar `WP3` (Semana 12) activa revisión inmediata para clausurar hojas paralelas |
| **M2 · Cierre de controles normativos y seguridad base** | Cumplimiento de **P3 (Seguridad por Diseño y Protección de Datos)** | `(Criterios del checklist normativo y STRIDE verificados en estado ✅ Cumple ÷ 15 criterios totales evaluados) × 100` | Auditoría normativa de Insuclínicos ([`../06-normatividad/checklist-cliente.xlsx`](../06-normatividad/checklist-cliente.xlsx)) y matriz STRIDE ([`../05-seguridad-stride/tabla-stride-cliente.xlsx`](../05-seguridad-stride/tabla-stride-cliente.xlsx)) | **`13,3 %` (`2 de 15` criterios en ✅ Cumple** —solo DIAN y retención contable— y `13 ⚠️ Parcial` en Taller 6; `0 de 6` amenazas `T1`–`T6` cerradas) | Menor a **`53 %`** (`8/15`) al concluir `WP1`+`WP2-B` (debendo quedar cubiertos los 4 críticos de prioridad Alta), o menor a **`85 %`** (`13/15`) tras concluir `WP3` obliga a sesión correctiva del comité |
| **M3 · Tiempo de dictamen del comité** *(mide al propio comité)* | Agilidad del **gobierno** frente al principio **P1** (evitar burocracia que empuje de vuelta al *Shadow IT*) | `Días hábiles transcurridos entre la Fecha de propuesta y la Fecha de dictamen de cada ADR o solicitud de excepción` | Registro histórico de decisiones (tabla ADR) en [`procedimiento-cambios.md`](procedimiento-cambios.md) | **No tiene línea base previa** porque el registro formal de ADR comienza a operar con este plan; se mide desde la primera solicitud de cambio posterior al comité | **`> 5 días hábiles`** (una semana laboral): si el comité supera 5 días hábiles en dictaminar una excepción operativa, la gerencia debe simplificar la aprobación para evitar el retorno informal a Excel |

---

_Este documento hace parte de la entrega final del Taller 9 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
