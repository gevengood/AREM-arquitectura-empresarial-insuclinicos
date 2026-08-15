# Business Architecture AS-IS

## Mapa de procesos

```mermaid
flowchart LR
    subgraph estrategicos["Procesos estratégicos"]
        direccion["Direccionamiento y administración"]
    end

    subgraph misionales["Procesos misionales"]
        ventas["Gestión comercial\ny cotizaciones"]
        pedidos["Gestión de pedidos"]
        abastecimiento["Inventario y abastecimiento"]
        produccion["Planeación y producción"]
        calidad["Control de calidad"]
        despacho["Despacho y entrega"]
        facturacion["Facturación y cartera"]
    end

    subgraph apoyo["Procesos de apoyo"]
        proveedores["Gestión de proveedores"]
        registros["Gestión de registros\ny comunicación interna"]
    end

    direccion --> ventas
    ventas --> pedidos
    pedidos --> abastecimiento
    abastecimiento --> produccion
    produccion --> calidad
    calidad --> despacho
    despacho --> facturacion
    proveedores --> abastecimiento
    registros --> ventas
    registros --> abastecimiento
    registros --> produccion
    registros --> calidad
    registros --> despacho
    registros --> facturacion
```

## Cadena de valor AS-IS

```mermaid
flowchart LR
    cliente1["Solicitud del cliente"] --> cotizacion["Cotización"]
    cotizacion --> confirmacion["Confirmación del pedido"]
    confirmacion --> inventario["Verificación de inventario"]
    inventario --> decision1{"¿Hay material suficiente?"}
    decision1 -->|Sí| plan["Planeación de producción"]
    decision1 -->|No| compra["Compra de materiales"]
    compra --> ingreso["Ingreso y registro de material"]
    ingreso --> plan
    plan --> fabricar["Producción"]
    fabricar --> calidad["Control de calidad"]
    calidad --> decision2{"¿Producto aprobado?"}
    decision2 -->|No| reproceso["Reproceso / no conforme"]
    reproceso --> calidad
    decision2 -->|Sí| almacenamiento["Almacenamiento de producto terminado"]
    almacenamiento --> despacho["Despacho y remisión"]
    despacho --> factura["Facturación electrónica"]
    factura --> cartera["Cartera y pago"]
```

## Catálogo de capacidades

| Dominio | Capacidad | Descripción AS-IS | Procesos relacionados |
|---|---|---|---|
| Comercial | Gestionar solicitudes y cotizaciones | Recibir requerimientos por canales de comunicación y elaborar ofertas | Gestión comercial |
| Comercial | Gestionar pedidos | Confirmar referencias, cantidades y fechas requeridas | Gestión de pedidos |
| Abastecimiento | Controlar inventario | Registrar y consultar manualmente existencias de materias primas, insumos y producto terminado | Inventario y almacenamiento |
| Abastecimiento | Gestionar compras | Solicitar y recibir materiales faltantes mediante comunicación con proveedores | Compras |
| Producción | Planear producción | Organizar fabricación a partir del pedido confirmado | Planeación de producción |
| Producción | Fabricar prendas e insumos | Preparar materiales, cortar, confeccionar o ensamblar productos | Producción |
| Calidad | Controlar conformidad | Inspeccionar productos y decidir aprobación, reproceso o no conformidad | Control de calidad |
| Logística | Gestionar despacho | Preparar el pedido, generar remisión y entregar al cliente | Despacho |
| Financiero-administrativo | Facturar y gestionar cartera | Emitir facturas electrónicas y gestionar cuentas por cobrar | Facturación y cartera |
| Gobierno | Administrar operación | Coordinar, validar información y tomar decisiones operativas | Direccionamiento y administración |

## 4.4 Mapa de actores e interacciones

```mermaid
flowchart TB
    cliente["Cliente"]
    ventas["Ventas / Administración"]
    inventario["Inventario / Almacén"]
    compras["Compras / Administración"]
    produccion["Producción"]
    calidad["Calidad / Producción"]
    despacho["Despacho / Almacén"]
    facturacion["Facturación / Administración"]
    proveedor["Proveedor"]

    cliente -->|Solicitud| ventas
    ventas -->|Cotización y confirmación| cliente
    ventas -->|Pedido confirmado| inventario
    inventario -->|Disponibilidad| ventas
    inventario -->|Faltantes| compras
    compras -->|Orden o solicitud de compra| proveedor
    proveedor -->|Materias primas e insumos| inventario
    ventas -->|Pedido y especificaciones| produccion
    inventario -->|Material disponible| produccion
    produccion -->|Producto fabricado| calidad
    calidad -->|Producto aprobado o reproceso| produccion
    calidad -->|Producto liberado| despacho
    despacho -->|Confirmación de entrega| facturacion
    facturacion -->|Factura| cliente
    cliente -->|Pago| facturacion
```

## BPMN descriptivo AS-IS — Gestión y cumplimiento de pedido

> El siguiente modelo se presenta en Mermaid como representación documentable del BPMN. En la versión gráfica final se recomienda dibujarlo en Bizagi Modeler, Draw.io o una herramienta BPMN con eventos, tareas, compuertas y carriles.

```mermaid
flowchart TB
    start((Inicio: solicitud del cliente))

    subgraph V["Carril: Ventas / Administración"]
        v1["Registrar solicitud en canal disponible\n(WhatsApp, correo o Excel)"]
        v2["Elaborar y enviar cotización"]
        g1{"¿Cliente confirma pedido?"}
        v3["Registrar pedido y comunicar requerimiento"]
    end

    subgraph I["Carril: Inventario / Almacén"]
        i1["Verificar disponibilidad de materias primas e insumos"]
        g2{"¿Material suficiente?"}
        i2["Registrar entrada de materiales"]
        i3["Entregar o disponer materiales para producción"]
        i4["Registrar producto terminado"]
    end

    subgraph C["Carril: Compras / Administración"]
        c1["Solicitar o gestionar compra de materiales faltantes"]
        c2["Coordinar recepción con proveedor"]
    end

    subgraph P["Carril: Producción"]
        p1["Recibir pedido y especificaciones"]
        p2["Programar producción"]
        p3["Fabricar producto\n(preparación, corte, confección o ensamble)"]
        p4["Registrar avance o resultado de producción"]
        p5["Realizar reproceso o clasificar no conformidad"]
    end

    subgraph Q["Carril: Calidad"]
        q1["Inspeccionar producto fabricado"]
        g3{"¿Cumple especificaciones?"}
        q2["Liberar producto aprobado"]
    end

    subgraph D["Carril: Despacho"]
        d1["Preparar pedido y remisión"]
        d2["Entregar o despachar pedido"]
    end

    subgraph F["Carril: Facturación / Cartera"]
        f1["Emitir factura electrónica"]
        f2["Registrar cuenta por cobrar"]
        f3["Registrar pago o realizar seguimiento de cartera"]
    end

    start --> v1 --> v2 --> g1
    g1 -->|No| end1((Fin: cotización no aceptada))
    g1 -->|Sí| v3 --> i1 --> g2
    g2 -->|No| c1 --> c2 --> i2 --> i3 --> p1
    g2 -->|Sí| i3 --> p1
    p1 --> p2 --> p3 --> p4 --> q1 --> g3
    g3 -->|No| p5 --> q1
    g3 -->|Sí| q2 --> i4 --> d1 --> d2 --> f1 --> f2 --> f3 --> end2((Fin: pedido facturado y en cartera/pagado))
```

## Hallazgos del proceso AS-IS

| Punto del proceso | Riesgo o dificultad AS-IS | Consecuencia potencial |
|---|---|---|
| Solicitud, cotización y pedido | Información distribuida entre WhatsApp, correo y Excel | Duplicidad, pérdida de contexto o demoras en la confirmación |
| Verificación de inventario | Actualización manual de existencias | Diferencias entre registro y realidad; faltantes no anticipados |
| Comunicación de órdenes a producción | Comunicación directa y dependencia de Excel | Riesgo de omisión, versión desactualizada o dificultad para rastrear prioridades |
| Compras | Activación reactiva ante faltantes | Compras urgentes y retrasos de producción |
| Registro de producción | Información en papel, Excel o registros internos | Visibilidad limitada del avance de la orden |
| Calidad | Registro interno separado del pedido | Dificultad para relacionar calidad, reproceso y cumplimiento de pedido |
| Despacho y facturación | Información operativa y administrativa no centralizada | Mayor esfuerzo para confirmar entrega, facturar y consultar estado de cartera |

---
