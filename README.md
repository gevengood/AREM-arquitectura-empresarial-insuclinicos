# Arquitectura Empresarial — Insuclínicos Ltda.

## Descripción

Este repositorio contiene el análisis de Arquitectura Empresarial de **Insuclínicos Ltda.**, empresa dedicada a la fabricación y comercialización de prendas e insumos médicos desechables en tela quirúrgica.

El proyecto documenta el estado actual (**AS-IS**) de la organización, con énfasis en la relación entre gestión comercial, pedidos, inventario, compras, producción, control de calidad, despacho, facturación y cartera.

La problemática principal identificada es la fragmentación de la información operativa entre Excel, WhatsApp, correo electrónico, registros internos y documentos físicos, lo que dificulta la trazabilidad de los pedidos, el control de inventario y la generación oportuna de indicadores.

---

## Objetivo del proyecto

Analizar la arquitectura empresarial AS-IS de Insuclínicos Ltda., centrada en el macro-proceso de Gestión y Cumplimiento de Pedido, y proponer conceptualmente una arquitectura objetivo que mejore la trazabilidad de pedidos, el control de inventario y la integración de información entre las áreas de la empresa.

> **Nota de alcance:** Este es un ejercicio académico del curso AREM (Arquitectura Empresarial) — Universidad de La Sabana. No constituye una implementación real ni un compromiso contractual con Insuclínicos Ltda. El único artefacto técnico funcional previsto en el semestre es un **Proof of Concept (POC)** acotado a un componente puntual de la arquitectura propuesta, a entregar al cierre del semestre. El resto del análisis (diagnóstico, visión, modelos) es documental y conceptual.

---

## Alcance — Corte 1 (AS-IS Completo)

Este repositorio consolida todos los entregables correspondientes al **Corte 1** según el marco metodológico TOGAF ADM adaptado al curso:

1. **Preliminary & Architecture Vision:** Contexto, ficha de caracterización, visión de arquitectura y registro metodológico.
2. **Business Architecture (BPMN):** Modelado de proceso de negocio AS-IS del cliente enfocado en producción y cumplimiento de pedidos.
3. **Information Systems Architecture (Datos y Contexto):** Modelo de datos AS-IS (ERD) y Diagrama de Contexto de negocio del cliente.

---

## Estructura del repositorio

```text
.
├── README.md
├── 00-preliminary-vision/
│   ├── ficha-caracterizacion.md
│   ├── vision.md
│   ├── notas.md
│   └── referencias.md
├── 01-bpmn/
│   ├── modelo-final.drawio
│   ├── informe.md
│   └── referencias.md
└── 02-modelo-informacion/
    ├── modelo-final-er.drawio
    ├── diagrama-contexto-final.drawio
    ├── informe.md
    └── referencias.md
```

---

## Entregables y Documentos

### 1. Preliminary & Architecture Vision (`00-preliminary-vision/`)
| Documento | Contenido |
|---|---|
| [Ficha de caracterización](00-preliminary-vision/ficha-caracterizacion.md) | Contexto de la empresa, objetivos estratégicos, problemas, procesos, restricciones y contacto |
| [Visión de arquitectura](00-preliminary-vision/vision.md) | Mapa conceptual de alto nivel, beneficios esperados trazados a los objetivos estratégicos, alcance y justificación |
| [Notas de trabajo](00-preliminary-vision/notas.md) | Registro de trabajo colaborativo, decisiones de modelado y compromisos del equipo |
| [Referencias de la visión](00-preliminary-vision/referencias.md) | Fuentes bibliográficas y fuentes primarias consultadas |

### 2. Business Architecture — BPMN (`01-bpmn/`)
| Entregable | Contenido |
|---|---|
| [Modelo BPMN del cliente (`modelo-final.drawio`)](01-bpmn/modelo-final.drawio) | Diagrama BPMN 2.0 editable con carriles funcionales, compuertas lógicas y eventos de excepción |
| [Informe técnico BPMN](01-bpmn/informe.md) | Descripción metodológica de 5 pasos, análisis del proceso de producción y decisiones de diseño |
| [Referencias BPMN](01-bpmn/referencias.md) | Estándares OMG BPMN 2.0 y referencias de soporte |

### 3. Information Systems Architecture — Datos y Contexto (`02-modelo-informacion/`)
| Entregable | Contenido |
|---|---|
| [Modelo Entidad-Relación (`modelo-final-er.drawio`)](02-modelo-informacion/modelo-final-er.drawio) | Modelo ER lógico editable con 8 entidades, atributos, claves primarias y relaciones de negocio |
| [Diagrama de Contexto (`diagrama-contexto-final.drawio`)](02-modelo-informacion/diagrama-contexto-final.drawio) | Diagrama de contexto editable mostrando actores externos, herramientas internas y flujos de información |
| [Informe técnico de Información](02-modelo-informacion/informe.md) | Explicación del modelo ERD, metodología de 4 pasos y flujos del diagrama de contexto |
| [Referencias de Información](02-modelo-informacion/referencias.md) | Literatura de bases de datos relacionales y referencias de soporte |

---

## Cliente

* **Insuclínicos Ltda.**
* Empresa dedicada a la fabricación y comercialización de prendas e insumos desechables elaborados principalmente en tela quirúrgica, dirigidos a clínicas, consultorios, spas y organizaciones que requieren protección en procedimientos médicos y estéticos.
* **Contacto:** Santiago Martínez — Representante legal.

---

## Equipo

* **Jorge Steven Doncel Bejarano** — [gevengood](https://github.com/gevengood)
* **David Santiago Buendia Londoño** — [Santiagoob7](https://github.com/Santiagoob7)

---

## Confidencialidad

La información se utiliza exclusivamente con fines académicos, previa autorización del cliente. Los datos personales, financieros, comerciales y sensibles de Insuclínicos Ltda., sus empleados, clientes y proveedores se omiten o se anonimizan.
