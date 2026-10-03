<!--
Puerta de entrada del repositorio del proyecto con el cliente real (Insuclínicos Ltda.),
estructurada siguiendo la guía oficial AREM-Proyecto-Cliente de la Universidad de La Sabana.
-->

# Arquitectura Empresarial — Insuclínicos Ltda.

**Equipo:** Grupo 8 · **Jorge Steven Doncel Bejarano** ([`@gevengood`](https://github.com/gevengood)), **David Santiago Buendia Londoño** ([`@Santiagoob7`](https://github.com/Santiagoob7))  
**Curso:** Arquitectura Empresarial (AREM) — Universidad de La Sabana  
**Cliente Real:** Insuclínicos Ltda. (Bogotá D.C., Colombia · Contacto: Santiago Martínez — Representante Legal)

---

## 📌 En una frase

Unificamos la gestión de pedidos, el inventario de tela quirúrgica SMS, las órdenes de planta y la facturación de **Insuclínicos Ltda.** en una plataforma web ligera en la nube, para eliminar el caos de los archivos de Excel desconectados, proteger la información contra pérdidas y asegurar la trazabilidad sanitaria exigida por el INVIMA.

## 🩺 El problema

Hoy la operación diaria de Insuclínicos Ltda. (6 empleados atendiendo a ~40 clínicas y spas) depende de mensajes de WhatsApp, hojas de cálculo de Excel guardadas en computadores locales que no se conectan entre sí y órdenes de producción en papel. Esto provoca bloqueos diarios cuando dos personas intentan abrir el mismo archivo, pérdida de **~6 horas semanales** pasando datos a mano hacia la facturación electrónica, riesgo de perder toda la información si falla un disco duro, e imposibilidad de rastrear rápidamente qué lote de rollo quirúrgico se usó en cada entrega ante una auditoría del INVIMA.

## 💡 Lo que proponemos

- **Centralizar pedidos, clientes e inventario en un solo sistema web en la nube** (CRM/ERP ligero para PyMEs), de modo que al aprobar un pedido se reserve automáticamente el material disponible sin bloqueos de lectura/escritura ni doble digitación hacia la facturación electrónica.
- **Conectar digitalmente la planta de confección y garantizar la trazabilidad sanitaria INVIMA**, registrando desde una Tablet en planta el lote de tela quirúrgica SMS usado en cada orden e imprimiéndolo en la remisión digital de la clínica.
- **Blindar la continuidad y el cumplimiento legal desde el primer mes**, implementando copias de seguridad automáticas diarias en la nube, cuentas de usuario individuales por rol y aviso de privacidad de datos personales (Ley 1581) en el canal de WhatsApp Business.
- **Ejecutar un plan gradual en 3 fases (12 semanas)** dentro del presupuesto de la empresa (`~ $2.2M COP/año`), empezando por las mejoras rápidas de seguridad y respaldo en las primeras 2 semanas.

## 🗺️ Cómo se implementa

Ver el **[Resumen Ejecutivo (`resumen-ejecutivo.md`)](resumen-ejecutivo.md)** — ahí está el detalle de beneficios esperados, evolución de capacidades del negocio, fases de implementación y tiempos, en un solo documento pensado para la gerencia de Insuclínicos Ltda.

---

## 📂 Si quiere ver el detalle técnico completo

Todo el análisis que sustenta esta propuesta está documentado carpeta por carpeta (Fases `00` a `07` consolidadas de los Cortes 1 y 2), siguiendo la metodología del curso:

| Carpeta | Qué contiene | Entregables principales |
|---|---|---|
| **[`00-preliminary-vision/`](00-preliminary-vision/)** | Contexto del cliente, problemas, objetivos estratégicos y visión de la solución | [Ficha de caracterización](00-preliminary-vision/ficha-caracterizacion.md) · [Visión de arquitectura](00-preliminary-vision/vision.md) · [Notas](00-preliminary-vision/notas.md) · [Referencias](00-preliminary-vision/referencias.md) |
| **[`01-bpmn/`](01-bpmn/)** | Cómo funciona hoy el proceso de negocio de gestión y cumplimiento de pedidos | [Modelo BPMN (`modelo-final.drawio`)](01-bpmn/modelo-final.drawio) · [Informe BPMN](01-bpmn/informe.md) · [Referencias](01-bpmn/referencias.md) |
| **[`02-modelo-informacion/`](02-modelo-informacion/)** | Qué información maneja el negocio (entidades) y cómo fluye entre áreas | [Modelo ER (`modelo-final-er.drawio`)](02-modelo-informacion/modelo-final-er.drawio) · [Diagrama de Contexto (`diagrama-contexto-final.drawio`)](02-modelo-informacion/diagrama-contexto-final.drawio) · [Informe](02-modelo-informacion/informe.md) · [Referencias](02-modelo-informacion/referencias.md) |
| **[`03-arquitectura-c4/`](03-arquitectura-c4/)** | Los sistemas actuales (AS-IS) modelados en contexto (C1) y contenedores (C2) | [Contexto C1 (`c1-contexto-final.drawio`)](03-arquitectura-c4/c1-contexto-final.drawio) · [Contenedores C2 (`c2-contenedores-final.drawio`)](03-arquitectura-c4/c2-contenedores-final.drawio) · [Informe C4](03-arquitectura-c4/informe.md) · [Referencias](03-arquitectura-c4/referencias.md) |
| **[`04-infraestructura/`](04-infraestructura/)** | Dónde corre todo hoy (Nube, Red Local LAN, Planta) y qué riesgos técnicos tiene | [Mapa de Infraestructura (`mapa-final.drawio`)](04-infraestructura/mapa-final.drawio) · [Informe de Infraestructura](04-infraestructura/informe.md) · [Referencias](04-infraestructura/referencias.md) |
| **[`05-seguridad-stride/`](05-seguridad-stride/)** | Evaluación de amenazas de seguridad de la información con metodología STRIDE (`T1`–`T6`) | [Tabla STRIDE (`tabla-stride-cliente.xlsx`)](05-seguridad-stride/tabla-stride-cliente.xlsx) · [Informe de Seguridad](05-seguridad-stride/informe.md) · [Referencias](05-seguridad-stride/referencias.md) |
| **[`06-normatividad/`](06-normatividad/)** | Auditoría de cumplimiento legal y normativo (Ley 1581, INVIMA Dec. 4725, ISO 27001) | [Checklist Normativo (`checklist-cliente.xlsx`)](06-normatividad/checklist-cliente.xlsx) · [Informe de Normatividad](06-normatividad/informe.md) · [Referencias](06-normatividad/referencias.md) |
| **[`07-opportunities-solutions/`](07-opportunities-solutions/)** | La arquitectura objetivo (TO-BE), matriz de brechas, matriz de decisión ponderada y paquetes de trabajo | [Documento Mejora TO-BE (`mejora-arquitectura.md`)](07-opportunities-solutions/mejora-arquitectura.md) · [Informe (`informe.md`)](07-opportunities-solutions/informe.md) · [TO-BE Aplicaciones (`to-be-aplicaciones-final.drawio`)](07-opportunities-solutions/to-be-aplicaciones-final.drawio) · [TO-BE Tecnología (`to-be-tecnologia-final.drawio`)](07-opportunities-solutions/to-be-tecnologia-final.drawio) · [Matriz de Brechas (`matriz-brechas.xlsx`)](07-opportunities-solutions/matriz-brechas.xlsx) · [Referencias](07-opportunities-solutions/referencias.md) |

---

## 🌳 Árbol de Estructura del Repositorio

```text
AREM-arquitectura-empresarial-insuclinicos/
├── README.md                                  # ⭐ Puerta de entrada ejecutiva y técnica
├── resumen-ejecutivo.md                       # Síntesis de negocio, beneficios y fases de implementación
├── 00-preliminary-vision/
│   ├── ficha-caracterizacion.md
│   ├── vision.md
│   ├── notas.md
│   └── referencias.md
├── 01-bpmn/
│   ├── modelo-final.drawio
│   ├── informe.md
│   └── referencias.md
├── 02-modelo-informacion/
│   ├── modelo-final-er.drawio
│   ├── diagrama-contexto-final.drawio
│   ├── informe.md
│   └── referencias.md
├── 03-arquitectura-c4/
│   ├── c1-contexto-final.drawio
│   ├── c2-contenedores-final.drawio
│   ├── informe.md
│   └── referencias.md
├── 04-infraestructura/
│   ├── mapa-final.drawio
│   ├── informe.md
│   └── referencias.md
├── 05-seguridad-stride/
│   ├── tabla-stride-cliente.xlsx
│   ├── informe.md
│   └── referencias.md
├── 06-normatividad/
│   ├── checklist-cliente.xlsx
│   ├── informe.md
│   └── referencias.md
└── 07-opportunities-solutions/
    ├── to-be-aplicaciones-final.drawio
    ├── to-be-tecnologia-final.drawio
    ├── matriz-brechas.xlsx
    ├── mejora-arquitectura.md
    ├── informe.md
    └── referencias.md
```

---

## 🔗 Repositorios Individuales de Talleres (Trabajo en Clase + Cliente)

- **Taller 1 (BPMN):** [`gevengood/taller-01-bpmn`](https://github.com/gevengood/taller-01-bpmn)
- **Taller 2 (Modelo de Información):** [`gevengood/taller-02-modelo-informacion`](https://github.com/gevengood/taller-02-modelo-informacion)
- **Taller 3 (Arquitectura C4):** [`Santiagoob7/AREM-Taller_3_Arquitectura_C4`](https://github.com/Santiagoob7/AREM-Taller_3_Arquitectura_C4)
- **Taller 4 (Infraestructura):** [`Santiagoob7/AREM-Taller_4_Infraestructura`](https://github.com/Santiagoob7/AREM-Taller_4_Infraestructura)
- **Taller 5 (Seguridad STRIDE):** [`Santiagoob7/Taller-5-Evaluaci-n-de-Seguridad-con-STRIDE`](https://github.com/Santiagoob7/Taller-5-Evaluaci-n-de-Seguridad-con-STRIDE)
- **Taller 6 (Normatividad):** [`gevengood/taller-06-normatividad`](https://github.com/gevengood/taller-06-normatividad)
- **Taller 7 (Opportunities & Solutions):** [`gevengood/taller-07-opportunities-solutions`](https://github.com/gevengood/taller-07-opportunities-solutions)

---

## 👥 Contacto

- **Jorge Steven Doncel Bejarano** — [`@gevengood`](https://github.com/gevengood) · `jorjuchod@gmail.com`
- **David Santiago Buendia Londoño** — [`@Santiagoob7`](https://github.com/Santiagoob7)

> **Confidencialidad y alcance académico:** La información contenida en este repositorio se utiliza exclusivamente con fines académicos en el curso Arquitectura Empresarial de la Universidad de La Sabana, previa autorización del cliente, con anonimización de datos sensibles y comerciales.
