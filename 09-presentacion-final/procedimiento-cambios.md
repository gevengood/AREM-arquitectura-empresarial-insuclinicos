# Procedimiento de Actualización y Revisión de la Arquitectura

## Cliente
**Insuclínicos Ltda.** — Fabricación y comercialización de prendas e insumos médicos quirúrgicos desechables en tela no tejida SMS (Bogotá D.C., Colombia).

## Integrantes del equipo (Grupo 8)
- **Jorge Steven Doncel Bejarano** (`@gevengood` · [jorgedobe@unisabana.edu.co](mailto:jorgedobe@unisabana.edu.co))
- **David Santiago Buendia Londoño** (`@Santiagoob7` · [davidbulo@unisabana.edu.co](mailto:davidbulo@unisabana.edu.co))

## Propósito de este documento

Establece cómo Insuclínicos Ltda. mantiene actualizada, coherente y documentada su arquitectura **después** de finalizar las 12 semanas del Plan de Implementación ([`plan-implementacion.md`](plan-implementacion.md)). Define los eventos concretos que obligan a revisar el modelo TO-BE, el flujo ágil para evaluar cambios, la periodicidad de revisión integral y el **registro oficial de Decisiones Arquitectónicas (ADR)** tomadas durante el proyecto.

---

## Disparadores de cambio

La arquitectura no se revisa por simple intuición, sino cuando ocurre cualquiera de los siguientes eventos concretos en el entorno operativo, comercial o regulatorio de Insuclínicos Ltda.:

| Disparador | Ejemplo concreto para este cliente |
|---|---|
| **Nueva regulación** | Cambios del **INVIMA** al Decreto 4725/2005 o Resolución 4816/2008 (ej. exigencia de código UDI en etiquetas de ropa quirúrgica Clase I), nuevo anexo técnico de facturación electrónica de la **DIAN** (sucesor Res. 000165/2023) o nuevas directrices de la SIC sobre **Ley 1581**. |
| **Cambio de proveedor tecnológico** | Aumento de tarifa del hosting/CRM-ERP Cloud por encima del umbral de **`$4.000.000 COP/año`** (fijado en Taller 7, Paso 8), degradación del SLA de disponibilidad, o cambio de operador tecnológico para Facturación Electrónica DIAN. |
| **Incidente de seguridad** | Compromiso de credenciales de oficina, infección por *ransomware*, fuga sospechada de la cartera de ~40 clínicas o fallo verificado durante las pruebas semestrales de restauración del backup **3-2-1**. |
| **Crecimiento inesperado de demanda** | Superar los **20 trabajadores** o **200 clínicas activas** (umbral de reevaluación del Taller 7, Paso 8), apertura de una segunda sede/bodega fuera de la actual en Bogotá o necesidad de automatización física en tendido de tela. |
| **Otro — Falla operativa o de conectividad** | Caídas del enlace de internet local que superen el respaldo 4G/5G (`>4 h/mes` de afectación), desfase repetido entre inventario físico SMS y PostgreSQL en >2 cierres mensuales, o reclamos de clientes por tiempos de atención (`OE-03`). |

---

## Proceso de cambio

Para evitar burocracia desproporcionada en una empresa de 6 trabajadores sin sacrificar control arquitectónico, todo cambio estructural sigue 4 pasos con tiempo máximo definido:

1. **Solicitud (Quién propone):** Cualquier colaborador de ventas, almacén, producción o el asesor técnico registra la necesidad ante el **Comité Ligero de Arquitectura** (ver [`plan-gobernanza.md`](plan-gobernanza.md)) usando una nueva tabla ADR en estado **`Propuesta`** dentro de este documento.
2. **Evaluación de impacto (Quién evalúa y contra qué criterios):** El Responsable Técnico y el Líder Funcional evalúan en conjunto la propuesta contrastándola contra:
   - Los **3 Objetivos Estratégicos** de la Ficha del Taller 0 (`OE-01` producción, `OE-02` inventarios SMS, `OE-03` organización/trazabilidad).
   - Los **3 Principios Arquitectónicos** (`P1` Sobriedad `<= $3M COP/año`, `P2` Fuente Única y Trazabilidad INVIMA, `P3` Seguridad Pragmática).
   - Los riesgos afectados en [`matriz-riesgos.xlsx`](matriz-riesgos.xlsx) (incluyendo los riesgos `R9` de negocio y `R10` de hardware aceptado).
3. **Dictamen y registro (Quién aprueba y en cuánto tiempo):** El **Representante Legal (Santiago Martínez)** aprueba (`Aceptada`) o rechaza (`Rechazada` / `Reemplazada`) la ADR en un plazo máximo de **5 días hábiles** desde su propuesta (alimentando la métrica **`M3`** de gobernanza). Si un incidente de seguridad o fallo de facturación DIAN bloquea los despachos, el dictamen de emergencia se emite en **menos de 24 horas** y se formaliza la ADR al día hábil siguiente.
4. **Actualización documental:** Una vez aprobada la ADR, se actualizan únicamente las vistas impactadas (diagramas C2/TO-BE o vistas ArchiMate finales) y nunca se borra una ADR anterior: si una nueva decisión sustituye a otra previa, la anterior cambia su estado a **`Reemplazada por ADR #X`**.

---

## Registro de decisiones (ADR)

A continuación se documentan las **2 decisiones arquitectónicas críticas** ya adoptadas por el equipo y validadas con los criterios del negocio durante el proyecto (Talleres 7 y 8):

| Campo | ADR #1 |
|---|---|
| **Título** | Adopción de CRM/ERP ligero en la nube (Odoo / Dolibarr sobre PostgreSQL) en lugar de Excel en OneDrive o desarrollo a la medida |
| **Estado** | Aceptada |
| **Fecha de propuesta** | 28/09/2026 |
| **Fecha de dictamen** | 03/10/2026 |
| **Contexto** | Insuclínicos Ltda. operaba sus pedidos e inventarios de tela quirúrgica SMS en dos libros locales de Excel desconectados sobre red local LAN (Talleres 3 y 4) y disco duro único sin backups ni bitácora (Taller 5 `T2`, `T3`, `T5`), perdiendo `~6 horas/semana` y sufriendo `2–3` bloqueos diarios de "Solo lectura". |
| **Problema** | Sin base transaccional concurrente ni integridad referencial entre materia prima y despacho, persistían los descuadres de stock, la vulnerabilidad a pérdida total de información y la imposibilidad de garantizar trazabilidad rápida ante auditorías INVIMA antes del pico de cierre de año. |
| **Decisión** | Adoptar **Opción A — CRM/ERP ligero SaaS/PaaS (Odoo Community / Dolibarr Cloud con PostgreSQL Gestionada)** para los 6 usuarios (`~$2.200.000 COP/año`), priorizada mediante la matriz de decisión ponderada de 8 pasos del Taller 7 (`4.40 / 5.00`). |
| **Alternativas consideradas** | **(a) Opción B — Desarrollo web a la medida (Node.js/React/PostgreSQL) [`2.40 / 5.00`]:** descartada porque supera en más de 5 veces el presupuesto máximo (`>$15M COP` vs tope `$3M COP/año`) y tarda `16–24 semanas`, incumpliendo la ventana operativa y generando deuda de mantenimiento de código.<br>**(b) Opción C — Mantener Excel migrado a OneDrive / SharePoint [`3.65 / 5.00`]:** descartada porque reprueba el criterio eliminatorio obligatorio `C1 = 2 < 3` — permite borrar filas o fórmulas accidentalmente (`T2`), no provee bitácora transaccional inmutable por campo (`T3`) ni garantiza trazabilidad obligatoria de lotes SMS.<br>**(c) Suite empresarial (SAP Business One):** descartada en exploración temprana por costo prohibitivo (`>$30M COP`). |
| **Consecuencias** | **(+)** Fuente única de verdad con concurrencia multiusuario sin bloqueos, bitácora inmutable de inventario/precios, cumplimiento sanitario INVIMA y backups cloud dentro del presupuesto (`~$2.2M/año`).<br>**(−)** Introduce dependencia permanente de acceso a internet en la sede de Bogotá, un costo anual recurrente superior al de OneDrive (`$2.2M` vs `~$900k COP/año`) y obliga a los 6 empleados a adaptar sus hábitos de hojas libres a formularios estructurados durante 5–6 semanas.<br>**Trade-off aceptado:** Se sacrifica menor costo base de almacenamiento y familiaridad inmediata con Excel a cambio de integridad transaccional relacional, auditoría contra repudio y cumplimiento sanitario INVIMA. |

| Campo | ADR #2 |
|---|---|
| **Título** | Digitalización de trazabilidad INVIMA en planta vía Tablet Web + integración DIAN mediante exportador CSV (sin automatización industrial ni API directa inmediata) |
| **Estado** | Aceptada |
| **Fecha de propuesta** | 26/10/2026 |
| **Fecha de dictamen** | 02/11/2026 |
| **Contexto** | Los Talleres 1, 3 y 4 mostraron dos quiebres físicos en el flujo end-to-end: las órdenes hacia corte/confección y los lotes de tela SMS se registran en papel suelto en planta (`GAP-05`, `GAP-09`), y los pedidos aprobados se redigitan manualmente desde Excel en el portal externo de Facturación Electrónica DIAN (`GAP-02`). En el Taller 8 se consolidaron estas integraciones en los Hilos 1 y 2. |
| **Problema** | Exigir transcripción manual en papel al cierre del turno produce olvidos del código de lote SMS (exposición ante Decreto 4725/2005 INVIMA), pero adquirir maquinaria automatizada con lectores RFID industriales y programar conectores API REST a medida con el proveedor DIAN excedería el presupuesto PyME y detendría la confección. |
| **Decisión** | Implementar en `WP3` una **Tablet Web conectada por Wi-Fi WPA3 en planta** sobre el módulo de producción del CRM/ERP con campo obligatorio `lote_sms_invima` para liberar la **Remisión Digital PDF**, y habilitar en `WP2-B` un **exportador CSV estandarizado** desde el módulo comercial hacia la plataforma externa de facturación DIAN. |
| **Alternativas consideradas** | **(a) Continuar con planillas en papel en planta y transcribir lotes al final del día desde un PC de oficina:** descartada porque mantiene doble trabajo, omisiones de lote en días de alto pedido y retraso al responder alertas de tecnovigilancia.<br>**(b) Implementar lectores RFID / sensores en mesas de tendido e integración API bidireccional a medida con DIAN:** descartada por sobrecosto financiero (viola `P1` y tope `$3M COP/año`) y alta complejidad técnica innecesaria para un equipo de 6 trabajadores y ~40 clientes. |
| **Consecuencias** | **(+)** Suprime el papel en planta, reduce la doble digitación contable sin intervenir el software del proveedor DIAN y permite reconstruir un *recall* sanitario de lotes en menos de 2 minutos.<br>**(−)** Requiere asegurar señal Wi-Fi WPA3 estable en el área de corte/confección, proteger físicamente la Tablet en entorno textil y mantener una acción manual controlada de carga del archivo CSV en el portal DIAN (expuesta a cambios de formato del proveedor).<br>**Trade-off aceptado:** Se sacrifica automatización 100% sin intervención humana en carga fiscal y en captura física de rollos a cambio de despliegue rápido en 4 semanas, cero desarrollo a medida y respeto estricto al presupuesto PyME. |

*(Para registrar futuras decisiones posteriores a la entrega, agregue nuevas tablas con este mismo esquema manteniendo numeración secuencial `ADR #3`, `ADR #4`, etc.)*

---

## Revisión periódica completa

Además de los disparadores puntuales, el Comité Ligero de Arquitectura ejecuta una **revisión arquitectónica integral cada 6 meses (semestral)** y una **reevaluación formal obligatoria en octubre de 2027** (a los 12 meses de la decisión `ADR #1`), evaluando:
1. Estado de las métricas **`M1` (adopción fuera de Excel), `M2` (cumplimiento del checklist de 15 ítems) y `M3` (agilidad del comité)** en [`plan-gobernanza.md`](plan-gobernanza.md).
2. Costo total anual real de licenciamiento y nube frente al umbral de `$4.000.000 COP/año`.
3. Vigencia de los riesgos aceptados (**`R10`** hardware PCs cliente) y resultados de las dos pruebas semestrales de restauración de backups 3-2-1.
4. Alineación del volumen de negocio frente al disparador de escala (**20 empleados o 200 clínicas activas**).

---

_Este documento hace parte de la entrega final del Taller 9 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
