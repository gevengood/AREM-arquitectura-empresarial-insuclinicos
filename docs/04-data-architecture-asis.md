# Arquitectura de Datos AS-IS

## Principios de lectura del modelo

El modelo de datos representa las entidades de negocio identificadas durante el levantamiento. No implica que hoy exista una base de datos integrada: en el estado AS-IS la información se encuentra distribuida en Excel, mensajes, correo, documentos físicos, registros internos, remisiones y plataforma de facturación electrónica.

## Catálogo de entidades

| Entidad | Descripción | Fuente o soporte AS-IS | Responsable principal |
|---|---|---|---|
| Cliente | Organización o persona que solicita, compra y recibe productos | Excel, WhatsApp, correo, registros administrativos | Ventas / Administración |
| Producto / Referencia | Prenda o insumo comercializado, con especificaciones y precio | Excel y archivos internos | Ventas / Producción |
| Cotización | Oferta comercial preparada para un cliente | Excel, correo y WhatsApp | Ventas / Administración |
| Pedido | Solicitud confirmada con referencias, cantidades y fecha requerida | Excel, registros administrativos, WhatsApp y correo | Ventas / Administración |
| Detalle de pedido | Líneas de producto, cantidades y especificaciones de cada pedido | Excel o registros administrativos | Ventas / Producción |
| Orden de producción | Requerimiento interno para fabricar un pedido o parte de este | Excel, registros internos y comunicación directa | Producción |
| Materia prima / Insumo | Material requerido para fabricar productos | Excel, documentos y registros de inventario | Inventario / Producción |
| Inventario | Existencias disponibles de materias primas, insumos y producto terminado | Principalmente Excel y registros manuales | Responsable de inventario |
| Movimiento de inventario | Entrada, consumo, ajuste o salida de un material o producto | Excel y registros manuales | Responsable de inventario |
| Proveedor | Entidad que suministra materiales e insumos | Excel y documentos administrativos | Compras / Administración |
| Compra | Solicitud o adquisición de materias primas e insumos | Facturas y registros administrativos | Compras / Administración |
| Registro de producción | Evidencia del avance o resultado de fabricación | Papel, Excel y registros de producción | Producción |
| Control de calidad | Resultado de inspección, liberación, reproceso o no conformidad | Registros internos | Calidad / Producción |
| Producto terminado | Producto fabricado y aprobado para almacenamiento o despacho | Inventario y registros de producción | Almacén / Producción |
| Despacho / Remisión | Registro de preparación y entrega de productos al cliente | Remisiones y registros administrativos | Despacho / Almacén |
| Factura | Documento electrónico emitido al cliente por el pedido entregado | Plataforma de facturación electrónica | Facturación / Administración |
| Pago / Cartera | Cuenta por cobrar, pago recibido y estado de recaudo | Plataforma de facturación y Excel | Administración / Cartera |
| Empleado / Responsable | Persona que realiza o valida actividades operativas | Documentación administrativa | Gerencia / Administración |

## Modelo lógico de datos AS-IS (SANTIAGO, PASAR ESTO A DRAW.IO)

```mermaid
erDiagram
    CLIENTE ||--o{ COTIZACION : recibe
    CLIENTE ||--o{ PEDIDO : realiza
    COTIZACION ||--o| PEDIDO : se_convierte_en
    PEDIDO ||--|{ DETALLE_PEDIDO : contiene
    PRODUCTO ||--o{ DETALLE_PEDIDO : corresponde_a
    PEDIDO ||--o{ ORDEN_PRODUCCION : origina
    ORDEN_PRODUCCION ||--o{ REGISTRO_PRODUCCION : registra
    ORDEN_PRODUCCION ||--o{ CONSUMO_MATERIAL : requiere
    MATERIA_PRIMA ||--o{ CONSUMO_MATERIAL : es_consumida
    MATERIA_PRIMA ||--o{ MOVIMIENTO_INVENTARIO : registra
    PRODUCTO ||--o{ MOVIMIENTO_INVENTARIO : registra
    PROVEEDOR ||--o{ COMPRA : suministra
    COMPRA ||--|{ DETALLE_COMPRA : contiene
    MATERIA_PRIMA ||--o{ DETALLE_COMPRA : es_adquirida
    COMPRA ||--o{ MOVIMIENTO_INVENTARIO : genera_entrada
    ORDEN_PRODUCCION ||--o{ CONTROL_CALIDAD : es_inspeccionada
    CONTROL_CALIDAD ||--o{ PRODUCTO_TERMINADO : libera
    PRODUCTO ||--o{ PRODUCTO_TERMINADO : materializa
    PEDIDO ||--o{ DESPACHO : se_entrega_en
    PRODUCTO_TERMINADO ||--o{ DESPACHO : se_despacha_en
    DESPACHO ||--o| FACTURA : soporta
    CLIENTE ||--o{ FACTURA : recibe
    FACTURA ||--o{ PAGO_CARTERA : registra

    CLIENTE {
        string id_cliente PK
        string nombre
        string contacto
        string canal_contacto
    }
    COTIZACION {
        string id_cotizacion PK
        date fecha
        string estado
        decimal valor
    }
    PEDIDO {
        string id_pedido PK
        date fecha_confirmacion
        date fecha_requerida
        string estado
    }
    DETALLE_PEDIDO {
        string id_detalle_pedido PK
        int cantidad
        string especificacion
    }
    PRODUCTO {
        string id_producto PK
        string referencia
        string descripcion
        decimal precio_referencia
    }
    ORDEN_PRODUCCION {
        string id_orden_produccion PK
        date fecha_programada
        string estado
    }
    MATERIA_PRIMA {
        string id_material PK
        string nombre
        string unidad_medida
    }
    CONSUMO_MATERIAL {
        string id_consumo PK
        decimal cantidad_consumida
        date fecha
    }
    INVENTARIO {
        string id_inventario PK
        decimal existencia_registrada
        string ubicacion
    }
    MOVIMIENTO_INVENTARIO {
        string id_movimiento PK
        string tipo
        decimal cantidad
        date fecha
    }
    PROVEEDOR {
        string id_proveedor PK
        string nombre
        string contacto
    }
    COMPRA {
        string id_compra PK
        date fecha
        string estado
    }
    DETALLE_COMPRA {
        string id_detalle_compra PK
        decimal cantidad
    }
    REGISTRO_PRODUCCION {
        string id_registro_produccion PK
        date fecha
        decimal cantidad_producida
        string observacion
    }
    CONTROL_CALIDAD {
        string id_control_calidad PK
        date fecha
        string resultado
        string observacion
    }
    PRODUCTO_TERMINADO {
        string id_producto_terminado PK
        decimal cantidad_disponible
        string estado
    }
    DESPACHO {
        string id_despacho PK
        date fecha
        string remision
        string estado
    }
    FACTURA {
        string id_factura PK
        date fecha
        decimal valor
        string estado
    }
    PAGO_CARTERA {
        string id_pago PK
        date fecha
        decimal valor
        string estado_cartera
    }
```

## Flujo de información AS-IS (SANTIAGO, PASAR ESTO A DRAW.IO)

```mermaid
flowchart LR
    ventas["Ventas / Administración"]
    inv["Inventario / Almacén"]
    compras["Compras / Administración"]
    prod["Producción"]
    calidad["Calidad"]
    despacho["Despacho"]
    fact["Facturación / Cartera"]

    ventas -->|Cliente, cotización, pedido, referencias, cantidades y fecha| prod
    ventas -->|Pedido confirmado| inv
    inv -->|Disponibilidad de materiales| prod
    prod -->|Consulta y consumo de materiales| inv
    inv -->|Faltantes de materiales| compras
    compras -->|Compra, recepción y datos de proveedor| inv
    prod -->|Producto fabricado y registro de producción| calidad
    calidad -->|Resultado, aprobación o reproceso| prod
    calidad -->|Producto aprobado| despacho
    despacho -->|Remisión y confirmación de entrega| fact
    fact -->|Factura y estado de cartera| ventas
```

## Matriz de información por proceso

| Proceso | Crea o actualiza | Consulta o utiliza | Soporte AS-IS |
|---|---|---|---|
| Ventas/cotización | Cliente, cotización, pedido, detalle de pedido | Productos, referencias, precios, estado de pedido | WhatsApp, correo, Excel |
| Inventario | Inventario, movimientos, entradas y consumos | Pedido, orden de producción, materias primas, compras | Excel y registros manuales |
| Compras | Compra, proveedor, detalle de compra | Faltantes, inventario, materias primas | Teléfono, WhatsApp, correo, facturas y registros administrativos |
| Producción | Orden de producción, registro de producción, consumo de materiales | Pedido, detalle de pedido, inventario, especificaciones | Registros internos, papel y Excel |
| Calidad | Control de calidad, reproceso o no conformidad | Registro de producción, producto, especificaciones | Registros internos |
| Despacho | Despacho, remisión | Producto terminado, pedido, aprobación de calidad | Remisiones y registros administrativos |
| Facturación/cartera | Factura, cuenta por cobrar, pago | Pedido entregado, despacho, datos de cliente | Plataforma de facturación electrónica y Excel |

## Problemas de datos AS-IS

- La información se crea y almacena en múltiples medios que no se encuentran integrados automáticamente.
- Excel se utiliza como soporte transversal para inventario, pedidos, organización administrativa y control interno.
- La actualización de inventario depende de una persona y de registros manuales de entrada y consumo.
- La orden de producción se comunica directamente al personal de producción después de organizar el pedido en Excel.
- No existe evidencia de un identificador único integrado que conecte de manera automática pedido, orden de producción, consumo de inventario, control de calidad, despacho y factura.
- La consulta del estado de una orden puede requerir revisar varios archivos, mensajes o registros de áreas distintas.
- La generación de indicadores depende de consolidación manual de datos.

---
