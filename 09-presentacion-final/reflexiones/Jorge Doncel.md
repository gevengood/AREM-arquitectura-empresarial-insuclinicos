# Reflexión Individual

## Nombre del Estudiante
**Jorge Steven Doncel Bejarano** (`@gevengood` · Código `282296` · [jorgedobe@unisabana.edu.co](mailto:jorgedobe@unisabana.edu.co))

## Rol en el equipo
Co-arquitecto y responsable principal del levantamiento del cliente (**Ficha de Caracterización — Taller 0**), el modelado de procesos (**BPMN — Taller 1**), el modelo conceptual de información (**ER y Diagrama de Contexto — Taller 2**), la auditoría legal y sanitaria (**Normatividad — Taller 6**) y la consolidación de decisiones estratégicas de la arquitectura objetivo (**Opportunities & Solutions — Taller 7**).

## Aprendizajes Clave

- **Aprendí a separar roles funcionales de personas concretas en empresas pequeñas:** al modelar el subproceso de producción de Insuclínicos Ltda. en BPMN (Taller 1), entendí que aunque 6 trabajadores cumplan funciones cruzadas entre bodega, corte y despacho, los carriles deben representar responsabilidades del proceso (`Producción`, `Almacén`, `Calidad`, `Despacho`) y no nombres propios, para que el diseño siga vigente si cambia el personal.
- **Comprendí cómo la regulación sectorial moldea directamente el modelo de datos:** en los Talleres 2 y 6 descubrí que la exigencia sanitaria del **INVIMA (Decreto 4725 de 2005 y Resolución 4816 de 2008)** sobre tecnovigilancia de dispositivos médicos Clase I no es solo un texto legal; obligó a introducir la entidad asociativa `CONSUMO_MATERIA_PRIMA` y el campo `lote_sms_invima` como condición eliminatoria en la toma de decisiones del Taller 7 (`C1 < 3`).
- **Practiqué la toma de decisiones estructurada con Trade-offs explícitos:** aplicar los 8 pasos con pesos validados y análisis de sensibilidad en el Taller 7 me mostró que una herramienta más barata y rápida (como mantener Excel en OneDrive) puede quedar descartada técnicamente si viola restricciones críticas de integridad y trazabilidad del negocio.

## Retos Superados

- **Tuve dificultades con delimitar el alcance de un macro-proceso sin intentar resolver toda la empresa a la vez**, pero logré superarlo acotando desde la Ficha del Taller 0 el flujo crítico *Gestión y Cumplimiento de Pedido* y manteniendo fuera de alcance procesos administrativos secundarios como nómina o automatización mecánica del tendido de tela.
- **Evitar el sesgo de anclaje al usar asistentes de IA en el Taller 7:** cuando contrastamos la matriz ponderada, recalculamos manualmente los escenarios de sensibilidad y detectamos errores aritméticos en el umbral sugerido por la herramienta y una sobrevaloración de seguridad para Excel en OneDrive; eso reforzó mi criterio de validar siempre los cálculos y evidencias frente a nuestros talleres previos (`STRIDE` y `checklist-cliente.xlsx`).

## Áreas por Mejorar

- Me gustaría profundizar en técnicas prácticas de parametri­zación real y migración de datos maestros sobre **ERP ligeros de código abierto (Odoo / Dolibarr)** para estimar con aún mayor precisión los esfuerzos de transición en PyMEs manufactureras.
- Reconozco que debo mejorar la formalización temprana de **principios arquitectónicos verificables desde la Visión inicial (Taller 0)**, de modo que desde la primera entrega queden explícitas las reglas que permiten decir «no» antes de llegar al cierre en Gobernanza (Taller 9).

## Contribución Personal

Mi mayor aporte al Grupo 8 fue estructurar la columna vertebral funcional, de datos y normativa del proyecto: liderar la caracterización real con Santiago Martínez, construir los modelos BPMN y Entidad-Relación que dieron origen a las entidades de trazabilidad, levantar la auditoría de 15 criterios frente a Ley 1581, INVIMA, DIAN e ISO 27001, y dirigir la evaluación multicriterio del Taller 7 que consolidó el repositorio en el Corte 2.

---

_Esta reflexión individual hace parte de la entrega final del curso AREM - Arquitectura Empresarial - Universidad de La Sabana._
