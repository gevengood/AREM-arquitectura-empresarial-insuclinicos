# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller 3 - Arquitectura Actual del Sistema con el Modelo C4

## 👥 Integrantes del equipo
* David Santiago Buendia Londoño (Santiagoob7)
* Jorge Steven Doncel (gevengood)

## 🧠 Descripción general del trabajo
El objetivo de este taller fue representar la arquitectura actual (AS-IS) de Insuclínicos Ltda., enfocándonos en el macro-proceso de Gestión y Cumplimiento de Pedido. Utilizando las vistas de Contexto (C1) y Contenedores (C2) del modelo C4, se documentó cómo interactúan los actores internos y externos con el ecosistema de información de la empresa, evidenciando la fragmentación de los datos y la alta dependencia de herramientas ofimáticas aisladas.

## 🔧 Proceso de desarrollo
El modelado se desarrolló en draw.io. Inicialmente, surgió el reto de aplicar el modelo C4 a una empresa que no cuenta con un software dedicado (backend/frontend tradicional), sino con una gestión basada en archivos locales. Se tomó la decisión arquitectónica de representar el "Ecosistema de Gestión Operativa" como el sistema central en el C1, y luego desglosarlo en el C2 tratando los archivos de MS Excel como los "contenedores" lógicos de la información. Esto permitió mapear con precisión técnica los cuellos de botella del flujo de datos, como las transcripciones manuales.

## 🧩 Análisis del modelo propuesto
* **Estructura del modelo:** El modelo separa claramente las interfaces de comunicación externa (WhatsApp, Facturación Electrónica) de la lógica interna. En el C2, se evidencia la ausencia de una base de datos relacional centralizada.
* **Representación de necesidades:** El diagrama refleja fielmente el Problema #2 y #3 identificados en la Ficha de Caracterización (control fragmentado y reactivo), al mostrar que la actualización entre el Libro de Pedidos y el Libro de Inventarios depende exclusivamente de "Lectura cruzada y actualización manual".
* **Supuestos:** Se asume que el Ecosistema de Gestión Operativa actual reside íntegramente en equipos locales sin sincronización en la nube, lo cual justifica el alto riesgo de pérdida de trazabilidad.

## 📈 Diagrama final entregado

* [Ver Vista de Contexto (C1)](./c1-contexto-final.drawio)
* [Ver Vista de Contenedores (C2)](./c2-contenedores-final.drawio)

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
| :--- | :--- | :--- | :--- |
| Cliente | Actor | Entidad externa que solicita insumos médicos. | Externo |
| Ventas / Administración | Actor | Encargados de recibir el pedido por canales informales y registrar la cotización. | Insuclínicos |
| Producción / Almacén | Actor | Área técnica que verifica la disponibilidad de tela y ejecuta la confección. | Insuclínicos |
| Libro de Pedidos | Contenedor (Excel) | Archivo ofimático local que funciona como registro transaccional comercial. | Administración |
| Libro de Inventario | Contenedor (Excel) | Archivo ofimático que actúa como base de datos estática para la materia prima. | Almacén |
| Facturación Electrónica | Sistema Externo | Plataforma de terceros usada para emitir comprobantes fiscales. | Proveedor TI |

## 🔍 Investigación complementaria

**Tema investigado:** Aplicación de patrones de arquitectura C4 en sistemas legados y ofimáticos (Shadow IT).

**Resumen:**
En muchas pymes latinoamericanas, la arquitectura empresarial no inicia con sistemas monolíticos o microservicios formales, sino con "Shadow IT": soluciones construidas empíricamente por los usuarios utilizando hojas de cálculo y canales de mensajería (WhatsApp). Investigar cómo el modelo C4 se adapta a estos escenarios demuestra que el concepto de "contenedor" es flexible. Un contenedor en C4 no tiene que ser obligatoriamente un contenedor Docker o un servicio web Node.js/Python; puede ser cualquier almacén de datos o bloque de ejecución lógica, incluyendo un archivo estructurado de MS Excel que procese macros o funciones. 
Modelar el "Shadow IT" bajo estándares como C4 (tal como hicimos con Insuclínicos) es el primer paso crítico para justificar técnicamente una migración futura hacia infraestructuras en la nube o bases de datos relacionales robustas, mitigando los riesgos de concurrencia y seguridad de la información.

## 📚 Referencias
* [1] Brown, Simon. *The C4 model for visualising software architecture*. https://c4model.com/
* [2] The Open Group. *ArchiMate® 3.2 Specification*. https://pubs.opengroup.org/architecture/archimate3-doc/
* [3] draw.io / JGraph. Documentación oficial de formas y librerías C4. https://www.diagrams.net/
