# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller 3 - Arquitectura Actual del Sistema con el Modelo C4

## 👥 Integrantes del equipo
* David Santiago Buendia Londoño (Santiagoob7)
* Jorge Steven Doncel (gevengood)

## 🧠 Descripción general del trabajo
El objetivo de este taller fue representar la arquitectura actual (AS-IS) de Insuclínicos Ltda., enfocándonos en el macro-proceso de Gestión y Cumplimiento de Pedido. Utilizando las vistas de Contexto (C1) y Contenedores (C2) del modelo C4, se documentó cómo interactúan los actores internos y externos con el ecosistema de información de la empresa, evidenciando la fragmentación de los datos, los cuellos de botella por digitación manual y la alta dependencia de herramientas ofimáticas locales ("Shadow IT").

## 🔧 Proceso de desarrollo
El modelado se desarrolló en draw.io utilizando la librería estándar de formas C4. A diferencia de un sistema de software tradicional basado en microservicios o arquitecturas web multicapa, Insuclínicos opera mediante un ecosistema híbrido de hojas de cálculo y registros físicos:
1. **Vista de Contexto (C1):** Se delimitó el "Ecosistema de Gestión Operativa" como el sistema central de la empresa. Se incorporaron los actores humanos clave (Clientes, Proveedor de Tela SMS, Ventas/Administración, Producción/Almacén y Despacho) y los sistemas externos (WhatsApp / Correo y la plataforma SaaS Siigo S.A.S. para facturación electrónica ante la DIAN). Las relaciones se ajustaron rigurosamente a la realidad operativa: los clientes se comunican por WhatsApp/correo, Ventas atiende desde smartphones personales y digita manualmente los datos en las hojas de cálculo, y luego transcribe los pedidos despachados al portal de Siigo.
2. **Vista de Contenedores (C2):** Se desglosó el ecosistema identificando las instancias físicas y lógicas donde residen los datos: el Libro de Pedidos (disco local C:\ en el PC de Administración), el Libro de Inventario (alojado en el PC de Administración y compartido vía SMB hacia el PC de Almacén) y los Registros de Calidad y Despacho (planillas físicas en papel dentro de la planta). Asimismo, se especificaron los protocolos y tecnologías de transporte en cada relación (digitación manual, SMB sobre LAN, HTTPS web).

## 🧩 Análisis del modelo propuesto
* **Estructura del modelo:** El modelo C1 y C2 separa con exactitud las interfaces de comunicación externa no estructuradas (WhatsApp en dispositivos BYOD) del almacenamiento ofimático interno y del portal fiscal de facturación.
* **Representación de necesidades:** Refleja la problemática operativa de Insuclínicos: al no existir una base de datos centralizada, la sincronización entre pedidos e inventario depende de "lectura cruzada humana", lo que genera desfases de stock y retrasos en planta.
* **Supuestos adoptados:**
  - El software de facturación electrónica utilizado por la empresa corresponde a **Siigo S.A.S.**, proveedor tecnológico autorizado por la DIAN (Resolución 000165 de 2023), accedido vía web HTTPS.
  - La red local opera bajo un grupo de trabajo Windows estándar sin Directorio Activo (Active Directory) ni servidor dedicado de archivos (NAS).

---

## ⚠️ Debilidades de la Arquitectura Actual (AS-IS)

Del análisis detallado de las vistas C1 y C2 se desprenden cuatro debilidades arquitectónicas críticas:

1. **Transcripción Manual y Cuello de Botella Humano:** No existe ninguna integración automatizada por API entre los canales de entrada (WhatsApp/Correo), los libros de Excel y el portal de facturación de Siigo S.A.S. Cada pedido debe ser transcrito manualmente dos veces por el personal de Ventas/Administración, incrementando la tasa de error en referencias de prendas y ralentizando la facturación.
2. **Punto Único de Falla (SPOF) en Hardware de Consumo:** Tanto el Libro de Pedidos como el Libro de Inventario residen físicamente en el disco duro local (unidad C:\) del equipo de Ventas/Administración. Un fallo mecánico del disco, una fluctuación de voltaje o un ataque por ransomware paralizaría de inmediato las cotizaciones, el inventario y las órdenes de producción.
3. **Bloqueo por Concurrencia sobre Protocolo SMB:** El PC de Almacén accede al Libro de Inventarios a través de una carpeta compartida de Windows (SMB). Microsoft Excel bloquea el archivo en modo "solo lectura" cuando un segundo usuario intenta abrirlo concurrentemente, forzando a los operarios a esperar que Administración cierre el documento para registrar ingresos o egresos de rollos de tela SMS.
4. **Desconexión y Ruptura de Trazabilidad Sanitaria (INVIMA):** La trazabilidad entre el lote del rollo de tela quirúrgica (materia prima) y la remisión final despachada al cliente se lleva en planillas físicas de papel en la planta. La ausencia de un identificador digital unificado dificulta responder oportunamente ante eventuales alertas sanitarias o auditorías de tecnovigilancia (Decreto 4725 de 2005).

---

## 🔄 Comparación con el Caso Base (RedExpress)

| Criterio Arquitectónico | Caso Base: RedExpress | Arquitectura AS-IS: Insuclínicos Ltda. |
| :--- | :--- | :--- |
| **Estilo Arquitectónico** | Microservicios distribuidos desacoplados y orientados a eventos. | "Shadow IT" ofimático local basado en hojas de cálculo y registros físicos. |
| **Persistencia de Datos** | Bases de datos relacionales (PostgreSQL/MySQL) y NoSQL escalables en la nube. | Archivos planos `.xlsx` en el sistema de archivos local (disco C:\) de un PC de escritorio. |
| **Mecanismo de Integración** | APIs REST, colas de mensajería (RabbitMQ/Kafka) y webhooks automatizados. | Transcripción manual por teclado, inspección visual humana y carpetas compartidas SMB. |
| **Concurrencia y Consistencia** | Control de transacciones ACID y concurrencia gestionada por motores de BD. | Bloqueo rudimentario a nivel de archivo de Windows; riesgo severo de sobreescritura. |
| **Escalabilidad y Despliegue** | Contenedores Docker orquestados, despliegue continuo en nube pública. | Estaciones de trabajo físicas (Windows 11) de oficina, sin capacidad de escalamiento elástico. |

---

## 📈 Diagramas finales entregados

* [Ver Vista de Contexto (C1)](./c1-contexto-final.drawio)
* [Ver Vista de Contenedores (C2)](./c2-contenedores-final.drawio)

---

## 📋 Tabla de actores, entidades y componentes

| Nombre del elemento | Tipo C4 | Descripción | Responsable |
| :--- | :--- | :--- | :--- |
| **Cliente** | Person (Actor Externo) | Clínicas, hospitales, odontólogos y centros estéticos que solicitan prendas quirúrgicas desechables en tela SMS. | Externo |
| **Proveedor de Tela SMS** | Person (Actor Externo) | Proveedor nacional de insumos que suministra rollos de tela no tejida SMS quirúrgica bajo cotizaciones formales. | Externo |
| **Ventas / Administración** | Person (Actor Interno) | Recibe pedidos por WhatsApp, cotiza, registra órdenes en Excel y transcribe datos a la plataforma de facturación. | Insuclínicos |
| **Producción / Almacén** | Person (Actor Interno) | Verifica stock de rollos de tela SMS en Excel, ejecuta el trazo, corte y confección de prendas en planta. | Insuclínicos |
| **Despacho** | Person (Actor Interno) | Verifica producto terminado, diligencia remisiones manuales de entrega y coordina transportadoras locales. | Insuclínicos |
| **WhatsApp / Correo** | External System | Servicios externos de comunicación móvil y mensajería en smartphones personales (BYOD) del equipo comercial. | Meta / Proveedor Mail |
| **Ecosistema de Gestión Operativa** | Software System | Conjunto desarticulado de hojas de cálculo MS Excel y registros físicos en papel que soportan la operación diaria. | Insuclínicos |
| **Libro de Pedidos y Cotizaciones** | Container (Excel) | Archivo `.xlsx` en disco local C:\ del PC Administración con histórico de pedidos, clientes y precios pactados. | Ventas / Administración |
| **Libro de Control de Inventario** | Container (Excel) | Archivo `.xlsx` en carpeta compartida de Windows (SMB) con cálculo de stock teórico de tela SMS y retazos. | Almacén / Producción |
| **Registros de Calidad y Despacho** | Container Físico (Papel) | Planillas físicas de corte, registro de no conformidades y remisiones manuscritas de entrega (Soporte Físico - No es software). | Planta / Despacho |
| **Plataforma Facturación (Siigo S.A.S.)** | External System | Software contable SaaS en la nube autorizado por la DIAN para emisión reglamentaria de facturas electrónicas con CUFE. | Siigo S.A.S. / DIAN |

---

## 🔍 Investigación complementaria

**Tema investigado:** Adopción de arquitecturas ofimáticas (Shadow IT) frente a requerimientos regulatorios y tributarios en Pymes manufactureras de Colombia.

**Resumen y conexión con decisiones del modelo:**
En el sector de confección y manufactura ligera de insumos médicos en Colombia, la adopción tecnológica frecuentemente difiere de los modelos teóricos de ingeniería de software. Según estudios del Departamento Nacional de Planeación (DNP) y la Cámara de Comercio de Bogotá (CCB, 2023), más del 70% de las micro y pequeñas empresas manufactureras operan su cadena de suministro sobre "Shadow IT", apoyándose en hojas de cálculo de Microsoft Excel y WhatsApp Business debido a restricciones presupuestales y a la baja complejidad inicial de sus catálogos.

Al modelar esta realidad bajo el estándar C4 (Brown, 2022), se valida que un "contenedor" no se limita a ejecutables binarios o microservicios Docker, sino que abarca cualquier almacén estructurado de datos o entorno lógico de ejecución. En Insuclínicos, representar las hojas de cálculo como contenedores individuales y delimitar claramente los registros físicos en papel permitió diagnosticar los puntos exactos de fricción regulatoria:
1. **Regulación Tributaria (DIAN):** La obligatoriedad de la factura electrónica bajo validación previa (Resolución DIAN 000165 de 2023) forzó a la empresa a adoptar un sistema externo SaaS (**Siigo S.A.S.**), creando una brecha de integración que hoy se resuelve mediante transcripción manual humana.
2. **Regulación Sanitaria (INVIMA):** La normativa de dispositivos médicos y prendas quirúrgicas (Decreto 4725 de 2005) exige estricta trazabilidad de materias primas. El modelo C2 evidencia cómo el almacenamiento de remisiones en papel rompe el hilo digital con el inventario de tela, impidiendo una respuesta ágil ante auditorías de tecnovigilancia.

Este diagnóstico visual fundamenta técnicamente la propuesta de evolución hacia una arquitectura centralizada con base de datos relacional y APIs REST para la fase TO-BE.

---

## 📚 Referencias
* [1] Brown, Simon. (2022). *The C4 model for visualising software architecture*. Software Architecture for Developers. https://c4model.com/
* [2] Dirección de Impuestos y Aduanas Nacionales — DIAN. (2023). *Resolución 000165 de 2023: Por la cual se desarrolla el sistema de facturación electrónica y se adopta el anexo técnico 1.9*. Diario Oficial de Colombia. https://www.dian.gov.co/
* [3] Cámara de Comercio de Bogotá — CCB. (2023). *Encuesta de Adopción Tecnológica y Madurez Digital en Micro y Pequeñas Empresas Manufactureras de Bogotá y la Región*. Dirección de Productividad y Competitividad. https://www.ccb.org.co/
* [4] Ministerio de Comercio, Industria y Turismo & DANE. (2023). *Encuesta de Tecnologías de la Información y las Comunicaciones en Empresas Manufactureras (EMyC)*. DANE Información Estratégica. https://www.dane.gov.co/
* [5] Ministerio de Salud y Protección Social. (2005). *Decreto 4725 de 2005: Régimen de registros sanitarios y vigilancia sanitaria de dispositivos médicos y prendas de uso médico*. Presidencia de la República de Colombia.
* [6] The Open Group. (2022). *ArchiMate® 3.2 Specification: A Formal Language for Enterprise Architecture*. https://pubs.opengroup.org/architecture/archimate3-doc/
