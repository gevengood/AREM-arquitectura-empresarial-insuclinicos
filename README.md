# Arquitectura Empresarial — Insuclínicos Ltda.

## Descripción

Este repositorio contiene el análisis de Arquitectura Empresarial de **Insuclínicos Ltda.**, empresa dedicada a la fabricación y comercialización de prendas e insumos médicos desechables.

El proyecto documenta el estado actual (**AS-IS**) de la organización, con énfasis en la relación entre gestión comercial, pedidos, inventario, compras, producción, control de calidad, despacho, facturación y cartera.

La problemática principal identificada es la fragmentación de la información operativa entre Excel, WhatsApp, correo electrónico, registros internos y documentos físicos, lo que dificulta la trazabilidad de los pedidos, el control de inventario y la generación oportuna de indicadores.

## Objetivo del proyecto

Analizar la arquitectura empresarial AS-IS de Insuclínicos Ltda. y proponer progresivamente una arquitectura objetivo que mejore la trazabilidad de pedidos, el control de inventario y la integración de información entre las áreas de la empresa.

## Alcance del Corte 1

El Corte 1 comprende:

- Ficha de caracterización del cliente.
- Architecture Vision.
- Business Architecture AS-IS.
- Arquitectura de Datos AS-IS.
- Modelos de procesos, actores, capacidades, entidades y flujos de información.

> La implementación de aplicaciones, infraestructura tecnológica y soluciones detalladas corresponde a los cortes posteriores.

## Estructura del repositorio

```text
.
├── README.md
└── docs/
    ├── 01-ficha-caracterizacion.md
    ├── 02-vision-arquitectura.md
    ├── 03-business-architecture-asis.md
    ├── 04-data-architecture-asis.md
    └── 05-referencias.md
```

## Documentos

| Documento | Contenido |
|---|---|
| [Ficha de caracterización](docs/01-ficha-caracterizacion.md) | Contexto de la empresa, objetivos, problemas, procesos, restricciones y actores clave |
| [Visión de arquitectura](docs/02-vision-arquitectura.md) | Visión, motivadores, beneficios esperados, alcance y justificación |
| [Business Architecture AS-IS](docs/03-business-architecture-asis.md) | Procesos, capacidades, actores, interacciones y BPMN descriptivo |
| [Arquitectura de Datos AS-IS](docs/04-data-architecture-asis.md) | Entidades, modelo lógico, fuentes de información y flujos de datos |
| [Referencias](docs/05-referencias.md) | Fuentes utilizadas para el levantamiento y desarrollo del análisis |

## Cliente

**Insuclínicos Ltda.**  
Empresa dedicada a la fabricación y comercialización de prendas e insumos desechables elaborados principalmente en tela quirúrgica.

## Equipo

- [Jorge Steven Doncel Bejarano] — [gevengood]
- [Nombre completo] — [usuario GitHub]

## Confidencialidad

La información se utiliza exclusivamente con fines académicos. Los datos personales, financieros, comerciales y sensibles del cliente, sus empleados, clientes y proveedores se omiten o anonimizarán.
