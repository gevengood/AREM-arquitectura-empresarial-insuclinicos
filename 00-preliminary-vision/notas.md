# 🗒️ Registro de Trabajo en Clase - Taller 0

## 📆 Fecha de la sesión
14 de agosto de 2026.

## 👥 Integrantes presentes
- Jorge Steven Doncel Bejarano  
- David Santiago Buendia Londoño

## 🧠 Actividades realizadas en clase

- Se revisó la guía paso a paso del Taller 0 y el ejemplo oficial del curso (Fundación Salud Viva) para entender el nivel de detalle esperado en la Ficha de Caracterización y en el Documento de Visión.
- Se contrastó la Ficha de Caracterización del cliente real (Insuclínicos Ltda.) contra la plantilla oficial, identificando campos incompletos: correo electrónico del contacto y número aproximado de clientes/usuarios.
- Se decidió acotar el alcance del proyecto a un único macro-proceso crítico —Gestión y Cumplimiento de Pedido— por ser el que cruza ventas, inventario, producción, despacho y facturación, en lugar de modelar todas las áreas por separado.
- Se identificó, a partir del levantamiento de información con el cliente, que el subproceso de producción (desde la orden hasta el producto terminado) es el mejor candidato para el modelado BPMN detallado, con dos puntos de decisión clave: disponibilidad de materia prima y aprobación de calidad.
- Se construyó el mapa conceptual de alto nivel (negocio, datos, aplicaciones, tecnología) para el Documento de Visión, evitando entrar en el nivel de detalle de un BPMN o C4.
- Herramientas usadas: Markdown/GitHub para la documentación, Mermaid para el diagrama conceptual.

## 🧩 Boceto inicial del modelo

Flujo general identificado con el cliente para el macro-proceso de Gestión y Cumplimiento de Pedido:

*Solicitud del cliente → cotización → confirmación del pedido → revisión de inventario → planeación de producción → compra de materiales si es necesario → preparación y tendido de tela → corte → confección/ensamble → control de calidad → almacenamiento de producto terminado → despacho → facturación → cartera/pago.*

El subproceso de producción (candidato a modelo BPMN detallado) parte de: recepción de la orden → verificación de materia prima (decisión: ¿hay material?) → programación de producción → tendido de tela → corte → confección → inspección de calidad (decisión: ¿cumple especificaciones?) → registro y almacenamiento → liberación del pedido.

## 🔁 Tareas definidas para complementar el taller

| Tarea asignada | Responsable | Fecha estimada |
|----------------|-------------|----------------|
| Confirmar correo electrónico del contacto y número aproximado de clientes activos | Jorge | 15/08 |
| Completar y subir Ficha de Caracterización a `entrega/ficha-caracterizacion.md` | Jorge | 16/08 |
| Redactar y subir Documento de Visión a `entrega/vision.md` | Santiago | 16/08 |
| Consolidar referencias en `entrega/referencias.md` | Santiago | 16/08 |
| Validar ambos documentos con el cliente (Santiago Martínez) antes del cierre del Corte 1 | Todo el equipo | 17/08 |

---

*Este documento resume el trabajo colaborativo realizado durante la sesión del Taller 0 en el curso AREM - Universidad de La Sabana.*
