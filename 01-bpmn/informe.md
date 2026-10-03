# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller 1 - Modelado de Proceso del Cliente con BPMN

## 👥 Integrantes del equipo
- Jorge Steven Doncel Bejarano ([gevengood](https://github.com/gevengood))
- David Santiago Buendia Londoño ([Santiagoob7](https://github.com/Santiagoob7))

## 🧠 Descripción general del trabajo

El objetivo de este taller fue modelar en notación BPMN un proceso real de Insuclínicos Ltda., aplicando la misma metodología de 5 pasos usada en clase con el caso base de la Clínica Salud Viva, pero sobre un proceso distinto al de agendamiento de citas. Se seleccionó el **subproceso de Producción**, desde la recepción de la orden de producción confirmada hasta la liberación del pedido para despacho, porque es el punto donde confluyen los tres problemas identificados en la Ficha de Caracterización del Taller 0: la alta intervención manual en producción, el control reactivo de materiales e inventario, y la fragmentación de la información entre áreas.

## 🔧 Proceso de desarrollo

Se aplicaron los 5 pasos de la guía metodológica del curso:

1. **Identificar actores:** se determinaron cuatro roles/áreas que participan en el proceso: Producción, Almacén/Inventario, Calidad y Despacho/Administración. A diferencia del caso base de clase (dos lanes: Paciente y Sistema de Citas), este proceso requirió cuatro carriles porque involucra más áreas de la operación real de la empresa.
2. **Definir inicio y fin:** el proceso inicia cuando se recibe una orden de producción ya confirmada comercialmente. Se identificaron dos desenlaces posibles: el pedido queda **despachado y facturado**, o la producción queda **en espera por abastecimiento** si no hay materia prima suficiente.
3. **Listar actividades:** se inventariaron las tareas de cada área a partir del levantamiento de información con el cliente (recibir orden, verificar materia prima, programar producción, tender tela, cortar, confeccionar, inspeccionar calidad, registrar y almacenar, liberar pedido).
4. **Insertar gateways:** se identificaron los dos puntos de decisión reales del proceso: **¿hay material suficiente?** (Almacén) y **¿cumple especificaciones?** (Calidad), ambos mencionados explícitamente por el cliente como fuentes de retraso o reproceso.
5. **Conectar y validar:** se trazaron los flujos de secuencia, se etiquetaron las salidas de cada gateway ("Sí"/"No") y se verificó contra la checklist del curso que no quedaran actividades sueltas ni caminos sin evento de fin.

Se usó draw.io para digitalizar el modelo, manteniendo la misma paleta de colores y estilos de notación que el ejemplo de clase (`ejemplo-agendamiento-citas.drawio`), para conservar consistencia visual entre los dos diagramas del curso.

## 🧩 Análisis del modelo propuesto

El modelo se estructura en cuatro carriles horizontales dentro de un único pool ("Producción de Prendas Desechables — Insuclínicos Ltda."), siguiendo el mismo patrón del caso base pero escalado a un proceso con más actores. Representa fielmente las necesidades del cliente porque:

- Refleja los dos puntos de fricción que el cliente señaló como problemas reales (Problema #1 y #3 de la Ficha): la ruta "No" del primer gateway lleva a un evento de fin de tipo interrupción ("Producción en Espera por Abastecimiento"), en lugar de simplemente terminar el diagrama, dejando explícito que un faltante de materia prima detiene el flujo.
- Incluye un ciclo de reproceso (flujo punteado desde "Enviar a Reproceso" de vuelta a "Confeccionar/Ensamblar Producto") para representar que un producto no conforme no sale del sistema, sino que reingresa a producción — un comportamiento que el cliente mencionó explícitamente en el levantamiento de información.
- Separa "Almacén/Inventario" de "Producción" como carriles distintos, aunque ambas funciones puedan ser ejercidas por las mismas personas en una empresa de 6 empleados; esto se hizo deliberadamente para modelar el **rol funcional**, no la persona, siguiendo la recomendación de BPMN de representar responsabilidades y no organigramas.

**Supuestos tomados:**
- Se asume que la orden de producción ya fue confirmada comercialmente antes del evento de inicio (la etapa de cotización/venta se modeló en el Taller 0 como parte del macro-proceso de Order Fulfillment, no se repite aquí).
- Se asume un único ciclo de reproceso por inspección de calidad; no se modelan reprocesos múltiples ni tiempos de espera cuantificados, dado que el cliente no proporcionó esos datos con precisión.
- La tarea "Generar Solicitud de Compra" se representa como un punto de interrupción del flujo (evento de fin), no como un subproceso completo de compras, porque ese subproceso está fuera del alcance definido en el Taller 0.

## 📈 Diagrama final entregado

Ver archivo [`modelo-final.drawio`](modelo-final.drawio) — ábralo en [draw.io](https://app.diagrams.net/) para visualizar el modelo completo con las cuatro lanes, los dos gateways y los dos eventos de fin.

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Producción | Lane / Actor | Ejecuta la recepción de la orden, programación, tendido, corte y confección | Encargado de producción / operarios |
| Almacén / Inventario | Lane / Actor | Verifica materia prima, gestiona compras urgentes y registra producto terminado | Encargado de almacén |
| Calidad | Lane / Actor | Inspecciona el producto confeccionado y decide aprobación o reproceso | Responsable de calidad |
| Despacho / Administración | Lane / Actor | Libera el pedido aprobado para su entrega y facturación | Encargado de despacho |
| ¿Hay material suficiente? | Gateway exclusivo (XOR) | Punto de decisión sobre disponibilidad de tela quirúrgica e insumos | Almacén |
| ¿Cumple especificaciones? | Gateway exclusivo (XOR) | Punto de decisión sobre aprobación de calidad del producto | Calidad |

## 🔍 Investigación complementaria

### Tema investigado
Buenas prácticas de modelado BPMN 2.0 para procesos de manufactura con puntos de control de calidad y gestión de excepciones (faltantes de material, reprocesos).

### Resumen
La especificación oficial de BPMN 2.0 (OMG) recomienda representar los puntos de excepción del proceso —como la falta de insumos o el rechazo de calidad— con eventos de fin diferenciados o eventos de error, en lugar de dejar el flujo sin resolver; esto se aplicó en el modelo usando un evento de fin distinto ("Producción en Espera por Abastecimiento") para la rama negativa del primer gateway, en vez de simplemente cerrar el diagrama. Asimismo, la literatura de gestión de procesos de manufactura recomienda modelar los reprocesos como ciclos explícitos que regresan a la actividad de origen, práctica que se siguió en el ciclo de reproceso de calidad.

También se investigó la diferencia entre modelar por **rol funcional** (lo que se hizo aquí) frente a modelar por **persona**, que es un error común en empresas pequeñas donde una sola persona cubre varias funciones. Mantener los carriles por función, y no por individuo, permite que el modelo siga siendo válido incluso si Insuclínicos cambia de personal o redistribuye funciones internamente, lo cual es relevante dado que la empresa cuenta con solo 6 trabajadores que desempeñan funciones cruzadas.

## 📚 Referencias
- [1] Object Management Group (OMG). *Business Process Model and Notation (BPMN), Version 2.0.2*. 2013. [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)
- [2] Insuclínicos Ltda. Levantamiento de información primaria con el cliente (Santiago Martínez), agosto de 2026. Documento interno: `Preguntas-Arq.-Empresarial.md`.
- [3] Universidad de La Sabana. *Guía Paso a Paso: Cómo Modelar un Proceso en BPMN*. Material del curso AREM, 2026.

---

_Este documento hace parte de la entrega del Taller 1 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
