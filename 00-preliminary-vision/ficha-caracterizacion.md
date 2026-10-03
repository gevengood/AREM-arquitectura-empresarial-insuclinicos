# Ficha de Caracterización del Cliente

**Nombre del Equipo:** Insuclínicos Ltda.
**Fecha:** 14 de agosto de 2026
**Nombre del Cliente:** Santiago Martínez
**Rol/Organización:** Representante legal / Insuclínicos Ltda.

## I. Información General del Negocio

- **Nombre de la empresa o entidad:** Insuclínicos Ltda.
- **Sector económico:** Fabricación y comercialización de prendas e insumos médicos desechables en tela quirúrgica.
- **Número de empleados / usuarios / clientes:** 6 trabajadores / clientes corporativos tipo clínicas, consultorios odontológicos, spas y organizaciones que requieren prendas e insumos para procedimientos médicos, estéticos y ambientes controlados, aproximadamente 40 clínicas /empresas donde usan el producto.
- **Ubicación principal (física o digital):** Calle 164 # 19-15, Interior 2, Oficina 107, Bogotá. Sede única: en las mismas instalaciones se desarrollan las actividades administrativas, productivas, de almacenamiento y despacho.
- **Tecnologías principales actuales:**
  - WhatsApp y correo electrónico (comunicación comercial y coordinación interna).
  - Excel (cotizaciones, pedidos, inventario, registros de producción y control administrativo/contable interno).
  - Documentos físicos y remisiones manuales (despacho y algunos registros de producción).
  - Plataforma de facturación electrónica (emisión de facturas a clientes; el control contable interno se sigue apoyando en Excel).

**Misión:** Proveer prendas e insumos médicos desechables en tela quirúrgica de alta calidad para clínicas, consultorios, spas y organizaciones, garantizando protección, cumplimiento y un servicio cercano a nuestros clientes.

**Visión:** Consolidarnos como un proveedor eficiente y tecnológicamente integrado de insumos desechables, optimizando la trazabilidad de nuestros inventarios y procesos de producción para asegurar entregas oportunas y operaciones sin interrupciones.

## II. Objetivos Estratégicos

1. **OE-01 — Aumentar la capacidad y eficiencia de producción:** fabricar una mayor cantidad de productos aprovechando mejor los recursos disponibles y disminuyendo tiempos improductivos.
   *Indicadores:* tiempo promedio de producción, unidades producidas por jornada, cumplimiento de órdenes, porcentaje de desperdicio de material.
2. **OE-02 — Mejorar el control de inventarios y materias primas:** conocer con mayor precisión las cantidades disponibles de tela quirúrgica, insumos y producto terminado para evitar faltantes que retrasen la producción.
   *Indicadores:* diferencias entre inventario físico y registrado, número de faltantes de material, cumplimiento de órdenes sin interrupciones por falta de insumos.
3. **OE-03 — Mejorar la organización y digitalización de la información:** reducir la dependencia de registros manuales y mejorar la comunicación de información entre ventas, producción, inventario, despacho y facturación.
   *Indicadores:* reducción de errores de registro, disminución de información duplicada, trazabilidad de pedidos, tiempo requerido para consultar información.

## III. Problemas o necesidades identificadas

- **Problema #1 — Alta intervención manual en producción:** actividades productivas dependen considerablemente del trabajo manual de los operarios, generando variaciones en tiempos, capacidad limitada y dependencia del personal.
- **Problema #2 — Control y circulación fragmentada de la información:** la información necesaria para ejecutar un pedido pasa por distintas personas y medios (Excel, WhatsApp, correo, papel) sin estar centralizada, generando registros duplicados, desactualización y demoras en la comunicación.
- **Problema #3 — Control reactivo de materiales e inventario:** la disponibilidad de tela quirúrgica e insumos se registra manualmente en Excel por una sola persona; las diferencias entre existencias reales y registradas pueden ocasionar retrasos, compras urgentes o incumplimiento de pedidos.

## IV. Procesos clave del negocio

*Nota: por el alcance del proyecto, nos enfocamos en modelar y analizar exclusivamente el macro-proceso más crítico que cruza las áreas afectadas.*

**Gestión y Cumplimiento de Pedido (Order Fulfillment):** abarca desde la recepción y confirmación comercial de la solicitud, pasando por la verificación de inventario y planeación de producción, hasta el control de calidad, despacho y facturación.

Flujo general: *Solicitud del cliente → cotización → confirmación del pedido → revisión de inventario → planeación de producción → compra de materiales si es necesario → preparación y tendido de tela → corte → confección/ensamble → control de calidad → almacenamiento de producto terminado → despacho → facturación → cartera/pago.*

| Proceso | Responsable | Objetivo | Entrada | Salida | Herramienta actual |
|---|---|---|---|---|---|
| Ventas/cotización | Ventas/Administración | Recibir requerimiento y definir oferta | Solicitud del cliente | Cotización/pedido | WhatsApp, correo, Excel |
| Inventario | Almacén/Producción | Verificar materiales disponibles | Pedido | Disponibilidad de materiales | Excel (registro manual) |
| Compras | Administración/Compras | Conseguir materiales faltantes | Necesidad de material | Materia prima disponible | Teléfono, WhatsApp, correo |
| Planeación | Producción | Organizar la fabricación | Pedido confirmado | Orden/plan de producción | Excel, comunicación manual |
| Tendido y corte | Producción | Preparar las piezas necesarias | Tela + especificaciones | Piezas cortadas | Equipos de producción |
| Confección | Producción | Fabricar la prenda | Piezas cortadas | Producto confeccionado | Máquinas/equipos |
| Calidad | Responsable de calidad/Producción | Verificar el producto | Producto fabricado | Producto aprobado o reproceso | Registros de calidad |
| Despacho | Almacén/Despachos | Preparar y entregar el pedido | Producto aprobado | Pedido despachado | Remisión/registros manuales |
| Facturación | Administración/Contabilidad | Registrar la venta | Pedido entregado | Factura/cuenta por cobrar | Plataforma de facturación electrónica + Excel |

**Subproceso recomendado para modelado BPMN detallado:** producción, desde la recepción de la orden hasta el producto terminado, incluyendo los puntos de decisión "¿hay material suficiente?" y "¿el producto cumple especificaciones?". El proceso de **tendido de tela** es candidato adicional para profundizar a nivel técnico si el proyecto se orienta a automatización industrial (operarios involucrados, tiempos, método de medición y extensión, errores frecuentes).

## V. Expectativas frente a la solución

- Recibir un diagnóstico estructurado de la operación actual (AS-IS) centrado en el cumplimiento de pedidos.
- Obtener un mapa general de procesos y un modelo BPMN detallado del proceso seleccionado.
- Identificar problemas, oportunidades de mejora y riesgos tecnológicos, junto con un análisis del flujo de información entre áreas.
- Obtener una propuesta de arquitectura y hoja de ruta progresiva (corto, mediano y largo plazo) que mejore la visibilidad del ciclo de vida del pedido sin reconstruir todo desde cero.

**Restricciones:**
- Presupuesto limitado para tecnología y automatización.
- La producción no puede detenerse durante la implementación.
- Se debe priorizar el aprovechamiento de equipos y herramientas actuales antes de grandes inversiones.
- Disponibilidad limitada del personal (6 trabajadores, varios con funciones cruzadas).
- Espacio físico de la planta.
- Confidencialidad de la información comercial, de clientes, proveedores y empleados.
- Requisitos sanitarios y de calidad aplicables a los productos.
- Implementación gradual para no afectar los pedidos existentes.

## VI. Persona de contacto

- **Nombre del contacto:** Santiago Martínez
- **Correo electrónico / teléfono:** [por confirmar] / 324 357 2958
- **Rol o vínculo con la solución:** Representante legal de Insuclínicos Ltda., encargado de validar la información y los modelos junto con el equipo de producción cuando aplique.

---
*Fuente de la información: levantamiento de requisitos con el cliente y validación de formato contra la ficha de ejemplo del curso.*
