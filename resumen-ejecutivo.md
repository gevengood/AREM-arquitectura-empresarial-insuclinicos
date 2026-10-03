# Resumen Ejecutivo — Propuesta de Mejora Operativa y Tecnológica para Insuclínicos Ltda.

**Cliente:** Insuclínicos Ltda. (Representante legal: Santiago Martínez)  
**Equipo Consultor (Grupo 8):** Jorge Steven Doncel Bejarano · David Santiago Buendia Londoño  
**Universidad de La Sabana — Arquitectura Empresarial (2026)**

---

## 1. El Problema Hoy (En lenguaje de negocio)

Insuclínicos Ltda. fabrica y comercializa ropa e insumos médicos quirúrgicos desechables en tela SMS para cerca de **40 clínicas, spas y centros estéticos** en Bogotá con un equipo de **6 trabajadores**. Hoy la operación enfrenta cuatro cuellos de botella críticos:

1. **Pedidos e inventario desconectados:** Las cotizaciones y pedidos se llevan en un archivo de Excel y el inventario de tela quirúrgica en otro. Esto consume **~6 horas semanales** de conciliación manual y provoca compromisos de entrega sobre inventario que no está disponible.
2. **Bloqueos diarios y doble digitación:** Cuando el área comercial y el almacén abren los archivos de Excel al mismo tiempo en la red local, el archivo se bloquea en modo *"Solo lectura"*. Además, cada venta debe volverse a digitar manualmente en el portal de Facturación Electrónica de la DIAN, y las órdenes de producción se llevan en papel físico hasta la planta.
3. **Riesgo de pérdida total de la información:** Toda la operación vive en el disco duro de un computador de oficina sin copias de seguridad automáticas en la nube y con sesiones de usuario compartidas. Un daño físico del computador o un virus detendría la empresa por completo.
4. **Exposición ante el INVIMA y la Ley de Protección de Datos:** Hoy no queda registrado en sistema qué lote de rollo de tela quirúrgica SMS se utilizó para fabricar las prendas entregadas en cada remisión (exigencia sanitaria del **Decreto 4725 de 2005** y **Resolución 4816 de 2008**), ni se solicita autorización formal de tratamiento de datos personales (**Ley 1581 de 2012**) al atender clientes por WhatsApp.

---

## 2. Nuestra Propuesta (Qué cambia y por qué)

En lugar de adquirir software costoso o desarrollar un sistema desde cero que tardaría meses, proponemos una transformación práctica en **tres paquetes de trabajo** dentro del presupuesto de una PyME (`~ $2.200.000 COP/año`), que reemplaza los archivos sueltos de Excel por un **sistema web ligero y centralizado en la nube (CRM/ERP como Odoo o Dolibarr Cloud)**:

- **Un solo lugar para clientes, pedidos e inventario:** Cuando Ventas aprueba un pedido, el sistema descuenta o reserva automáticamente la tela quirúrgica y las prendas en bodega, sin bloqueos de archivo.
- **Trazabilidad sanitaria INVIMA de punta a punta:** Desde una **Tablet en la planta de producción**, los operarios consultan las órdenes pendientes sin usar papel y registran el número de lote del rollo SMS empleado, el cual queda impreso automáticamente en la remisión digital del cliente.
- **Facturación sin volver a digitar:** El pedido aprobado se exporta en formato listo para cargar en la plataforma de Facturación Electrónica DIAN.
- **Información protegida y respaldada todos los días:** Cada uno de los 6 empleados ingresa con su propio usuario según su rol, y la base de datos realiza copias de seguridad automáticas diarias en la nube.

---

## 3. Plan de Implementación en 3 Fases (12 Semanas)

| Fase / Paquete de Trabajo | Duración | Qué se entrega al negocio | Beneficio inmediato |
|---|---|---|---|
| **Fase 1 (`WP1` — Quick Win): Continuidad, Seguridad Base y Ley 1581** | **Semanas 1 a 2** | • Copias de seguridad automáticas diarias en la nube (Regla 3-2-1).<br>• Usuarios individuales con contraseña en los equipos de oficina.<br>• Mensaje automático de aviso de privacidad (Ley 1581) en WhatsApp Business. | Elimina en 15 días el riesgo de perder toda la información de la empresa y blinda legalmente el canal comercial de WhatsApp. |
| **Fase 2 (`WP2` — Núcleo): Sistema Centralizado CRM/ERP en la Nube y Facturación** | **Semanas 3 a 8** | • Puesta en marcha del CRM/ERP web con base de datos centralizada.<br>• Migración del catálogo de productos y de las ~40 clínicas.<br>• Exportador directo hacia Facturación Electrónica DIAN. | Elimina los bloqueos de Excel, ahorra ~6 horas semanales de reprocesos administrativos y evita pérdidas inexplicables de insumos. |
| **Fase 3 (`WP3` — Planta): Digitalización de Producción y Lotes INVIMA** | **Semanas 9 a 12** | • Tablet conectada por Wi-Fi seguro en la planta de corte y confección.<br>• Registro obligatorio del lote de tela SMS en cada orden y remisión digital. | Cero papel hacia la planta, visibilidad en vivo del estado de cada pedido y cumplimiento ante visitas de tecnovigilancia del INVIMA. |

---

## 4. Evolución de las Capacidades de Insuclínicos Ltda.

| Capacidad del Negocio | Estado Hoy (1 a 5) | Estado con la Propuesta (1 a 5) | Qué gana Insuclínicos Ltda. |
|---|:---:|:---:|---|
| **Gestionar pedidos y cotizaciones comerciales** | 2 / 5 | **4 / 5** | Cotizaciones rápidas con validación real de existencias y cumplimiento de Habeas Data. |
| **Controlar inventarios e insumos quirúrgicos** | 1 / 5 | **4 / 5** | Existencias exactas de rollos SMS en tiempo real, sin archivos bloqueados y con historial de quién hizo cada ajuste. |
| **Planificar y ejecutar la producción quirúrgica** | 2 / 5 | **4 / 5** | Órdenes digitales en pantalla desde la planta sin depender de hojas impresas. |
| **Asegurar la calidad y trazabilidad sanitaria** | 1 / 5 | **4 / 5** | Capacidad de rastrear en minutos qué lote de tela se entregó a cada clínica ante el INVIMA. |
| **Facturar y recaudar ventas** | 3 / 5 | **4 / 5** | Emisión ágil de facturas electrónicas sin transcripción manual. |
| **Asegurar la continuidad y seguridad de la información** | 1 / 5 | **4 / 5** | Negocio protegido contra daños de computadores, robo de datos o *ransomware*. |

---

> 📂 Para consultar las matrices detalladas, presupuestos comparativos y diagramas técnicos de esta propuesta, diríjase a [`07-opportunities-solutions/mejora-arquitectura.md`](07-opportunities-solutions/mejora-arquitectura.md) y [`07-opportunities-solutions/matriz-brechas.xlsx`](07-opportunities-solutions/matriz-brechas.xlsx).
