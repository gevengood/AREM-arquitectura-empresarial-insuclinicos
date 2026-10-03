# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller 2 - Modelo de Información y Diagrama de Contexto

## 👥 Integrantes del equipo
- Jorge Steven Doncel Bejarano — Código: 282296 / Correo: [jorgedobe@unisabana.edu.co](mailto:jorgedobe@unisabana.edu.co)
- David Santiago Buendia Londoño — Código: 306487 / Correo: [davidbulo@unisabana.edu.co](mailto:davidbulo@unisabana.edu.co)

## 🧠 Descripción general del trabajo

El objetivo del Taller 2 fue modelar las entidades de información del cliente y los flujos de información entre sus actores y sistemas, mediante un modelo entidad-relación (ERD) y un diagrama de contexto de negocio. La Parte 1 del taller se desarrolló en clase sobre el dominio de la Clínica Salud Viva; esta entrega corresponde a la Parte 2 y adapta ambas metodologías al dominio real de **Insuclínicos Ltda.**

El alcance se centra en la Gestión y Cumplimiento de Pedido, especialmente en su relación con producción, inventario y despacho. Se eligió este dominio porque la empresa registra pedidos, materias primas y actividades de producción de manera fragmentada entre Excel, WhatsApp, correo electrónico y documentos físicos, lo que limita la trazabilidad y dificulta conocer el estado real de un pedido.

## 🔧 Proceso de desarrollo

### Modelo entidad-relación

Se aplicó la metodología de cuatro pasos propuesta en la guía del curso:

1. **Identificar entidades:** se seleccionaron ocho entidades esenciales para representar el dominio sin sobredimensionar el modelo: Cliente, Pedido, DetallePedido, Producto, OrdenProduccion, MateriaPrima, ConsumoMateriaPrima y Despacho.
2. **Definir atributos:** cada entidad tiene una clave primaria (PK) y atributos descriptivos mínimos. Por ejemplo, `id_pedido` identifica el pedido, mientras que fecha, estado y fecha requerida permiten hacer seguimiento a su cumplimiento.
3. **Trazar relaciones:** las relaciones se nombraron con verbos de negocio: Cliente *realiza* Pedido; Pedido *contiene* DetallePedido; Pedido *origina* OrdenProduccion; OrdenProduccion *registra* ConsumoMateriaPrima; y Pedido *se entrega mediante* Despacho.
4. **Asignar cardinalidad:** se indicaron cardinalidades 1:N o N:1 en ambos extremos. La relación potencialmente N:N entre OrdenProduccion y MateriaPrima se resolvió mediante la entidad asociativa **ConsumoMateriaPrima**.

### Diagrama de contexto

También se siguieron los cuatro pasos de la guía: se identificaron los actores externos (Cliente y Proveedor), se trazó el límite organizacional de Insuclínicos, se ubicaron dentro sus herramientas internas actuales (Excel Operativo, WhatsApp/Correo y Documentos Físicos/Remisiones), y se diferenció la Plataforma de Facturación Electrónica como sistema externo. Finalmente, se etiquetó cada flujo con la información intercambiada, evitando flechas genéricas sin significado.

## 📈 Diagramas finales entregados

- [Modelo Entidad-Relación (`modelo-final-er.drawio`)](modelo-final-er.drawio)
- [Diagrama de Contexto (`diagrama-contexto-final.drawio`)](diagrama-contexto-final.drawio)

