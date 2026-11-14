# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller 4 - Mapa de Infraestructura y Diagnóstico Técnico

## 👥 Integrantes del equipo
* David Santiago Buendia Londoño (Santiagoob7)
* Jorge Steven Doncel (gevengood)

## 🧠 Descripción general del trabajo
El objetivo de este taller fue levantar el mapa de infraestructura tecnológica y física actual (AS-IS) de Insuclínicos Ltda., enfocado en el macro-proceso crítico de **Gestión y Cumplimiento de Pedido**. A través de este ejercicio, se realizó un diagnóstico técnico exhaustivo para identificar puntos únicos de falla (SPOF), cuellos de botella de concurrencia y límites de escalabilidad en un entorno empresarial operado casi en su totalidad mediante herramientas ofimáticas locales ("Shadow IT"), dispositivos móviles personales y transporte manual de información.

## 🔧 Proceso de desarrollo
El modelado se realizó en draw.io utilizando diagramación física de red e infraestructura:
1. **Delimitación de Zonas:** Se estructuró la topología en tres zonas operativas:
   - **Nube Pública / Servicios Externos:** Servidores de Meta (WhatsApp Business) y la plataforma de facturación electrónica validada ante la DIAN (**Siigo S.A.S.**).
   - **Conectividad y Dispositivos de Acceso:** Incorporación de los **Smartphones personales (BYOD)** del personal comercial y el **Router / Módem ISP de la oficina** (enlace FTTH que conecta la red LAN y los móviles a Internet).
   - **Red Local (LAN) Oficina:** Modelado del **PC de Ventas / Administración**, situando explícitamente el **Disco Duro Local C:\** dentro de su chasis físico para evidenciar que alberga los archivos maestros de Excel (`Libro_Pedidos.xlsx` y `Libro_Inventario.xlsx`), y el **PC de Almacén**, el cual se conecta mediante un recurso compartido de red de Windows (protocolo SMB).
   - **Planta de Producción:** Zona de manufactura donde residen los **Registros Físicos en Papel** (planillas de corte y remisiones manuscritas).
2. **Diagnóstico Técnico de Riesgos:** Se identificaron y categorizaron los riesgos de disponibilidad, rendimiento y escalabilidad, destacando que el PC de Administración constituye el verdadero Punto Único de Falla (SPOF) de toda la compañía al no disponer de almacenamiento en red dedicado (NAS) ni respaldos automatizados.

---

## 🧩 Análisis del modelo propuesto
* **Estructura del modelo:** El mapa refleja con precisión la dependencia de enlaces de consumo hogareño/comercial básico (router provisto por el ISP, smartphones de los propios empleados bajo modelo BYOD sin MDM corporativo).
* **Representación de necesidades:** Se evidencia gráficamente por qué se presentan pérdidas de datos y demoras en planta: al abrir el archivo de inventario simultáneamente entre Administración y Almacén sobre SMB, Windows aplica bloqueos de concurrencia a nivel de archivo.
* **Supuestos adoptados:**
  - Los PC de Ventas y Almacén cuentan con Windows 11 en un grupo de trabajo local sin servidor de dominio Active Directory.
  - La conexión a Internet de la oficina depende de un único módem router provisto por el operador local de telecomunicaciones (sin enlace de contingencia 4G/5G).
  - Los archivos de Excel residen en la unidad `C:\Gestion_Insuclinicos\` del PC de Administración.

---

## 📈 Diagrama final entregado
* [Ver Mapa de Infraestructura Final (AS-IS)](./mapa-final.drawio)

---

## 📋 Tabla de Componentes de Infraestructura

| Nombre del Componente | Tipo de Elemento | Descripción Técnica | Zona / Ubicación | Responsable |
| :--- | :--- | :--- | :--- | :--- |
| **Servidores Meta (WhatsApp)** | Servicio Nube (SaaS) | Servidores de mensajería instantánea que gestionan el canal comercial de entrada con las clínicas. | Nube Pública | Meta Platforms |
| **Plataforma Facturación (Siigo)** | Servicio Nube (SaaS) | Portal web contable autorizado por la DIAN para validación y generación de facturas XML con CUFE. | Nube Pública | Siigo S.A.S. |
| **Smartphones Personales (BYOD)** | Dispositivo Móvil | Celulares personales del equipo de ventas utilizados para atención de clientes y recepción de cotizaciones. | Oficina / Remoto | Empleados / Ventas |
| **Router / Módem ISP de Oficina** | Hardware de Red | Equipo de borde provisto por el operador que brinda acceso a Internet FTTH y señal Wi-Fi/Ethernet a la LAN. | Oficina Insuclínicos | ISP / Administración |
| **PC Ventas / Administración** | Estación de Trabajo | Computador de escritorio (Windows 11) que procesa cotizaciones, pedidos y aloja el almacenamiento compartido. | Red Local (LAN) | Administración |
| **Disco Duro Local C:\ (SPOF)** | Almacenamiento Local | Disco mecánico/SSD interno del PC de Administración que almacena los libros Excel de pedidos e inventario. | PC Administración | Administración |
| **PC Almacén / Inventario** | Estación de Trabajo | Computador de oficina (Windows 11) utilizado por el encargado de almacén para consultar stock vía red local SMB. | Red Local (LAN) | Almacén |
| **Registros Físicos en Papel** | Soporte Físico | Carpetas archivadoras con planillas de corte, remisiones de despacho y registros manuales de calidad INVIMA. | Planta de Producción | Planta / Despacho |

---

## 📋 Tabla de Diagnóstico Técnico

| Componente | Riesgo Diagnosticado | Categoría | Impacto si Ocurre | Prioridad |
| :--- | :--- | :--- | :--- | :--- |
| **Disco Duro Local C:\ (PC Administración)** | Punto Único de Falla (SPOF físico) sin respaldo en nube | Disponibilidad | Pérdida definitiva de clientes, pedidos históricos e inventarios ante daño de hardware o ataque de ransomware. | **Alta** |
| **Carpeta Compartida Windows (SMB)** | Bloqueo por concurrencia en archivos `.xlsx` | Rendimiento | Almacén no puede actualizar stock mientras Administración edita precios; paradas en despacho y demoras operativas. | **Alta** |
| **Smartphones Personales (BYOD)** | Falta de control y retención de información comercial | Seguridad / Disponibilidad | Pérdida de contactos de clientes o fuga de cotizaciones ante pérdida/robo del terminal móvil del vendedor. | **Media** |
| **Router ISP Único** | Enlace de comunicaciones sin redundancia (No Failover) | Disponibilidad | La caída del servicio de Internet impide facturar en Siigo y sincronizar WhatsApp Web con las clínicas. | **Media** |
| **Transporte Físico de Papel a Planta** | Límite severo de escalabilidad y desconexión digital | Escalabilidad | Pérdida física de remisiones, errores de caligrafía y retrasos en el alistamiento de pedidos urgentes. | **Media** |

---

## 🔍 Investigación complementaria

**Tema investigado:** Gestión de riesgos de infraestructura, puntos únicos de falla (SPOF) y TI en la sombra (*Shadow IT*) en micro y pequeñas empresas manufactureras colombianas.

**Resumen y conexión con fuentes verificables:**
La arquitectura tecnológica de Insuclínicos ejemplifica el estado típico de madurez digital de las microempresas del sector manufactura en Bogotá. Según el *Diagnóstico de Adopción Tecnológica y Madurez Digital en Microempresas* publicado por la Cámara de Comercio de Bogotá (CCB, 2023), más del 68% de las microempresas de confección y suministros industriales centralizan sus registros contables y operativos en un único computador de escritorio de gama doméstica, prescindiendo de servidores dedicados de almacenamiento en red (NAS) o esquemas formales de respaldo debido a percepciones de sobrecosto.

Esta condición crea un acoplamiento crítico al hardware físico que el Instituto Nacional de Estándares y Tecnología de los Estados Unidos (NIST, 2021) en su *Small Business Cybersecurity Corner (SP 800-184 / Small Business Guide)* cataloga como la principal vulnerabilidad de continuidad operativa en pequeñas organizaciones: la falla del dispositivo anfitrión destruye simultáneamente los activos de datos y la capacidad operativa del negocio. 

Asimismo, los lineamientos del pilar de confiabilidad del *AWS Well-Architected Framework* (Amazon Web Services, 2023) señalan que la eliminación de SPOFs no exige necesariamente la migración hacia centros de datos de misión crítica de alto costo, sino la separación desacoplada entre la capa de cómputo y la capa de almacenamiento. Para Insuclínicos, la transición tecnológica no requiere un datacenter corporativo, sino reemplazar el recurso compartido SMB local por repositorios de datos centralizados en la nube (PaaS o bases de datos relacionales gestionadas) con replicación geográfica automática y esquemas de respaldo siguiendo la regla 3-2-1 recomendada por CISA (2023).

Adicionalmente, el Ministerio de las TIC de Colombia (MinTIC, 2023) a través de su *Guía de Digitalización Segura para Mipymes*, resalta que el uso de dispositivos personales de los empleados (BYOD) para la atención de clientes vía WhatsApp sin políticas de respaldo institucional expone a la empresa a la pérdida irreversible de su cartera comercial en caso de renuncia o cambio de dispositivo del trabajador.

---

## 📚 Referencias
* [1] Cámara de Comercio de Bogotá — CCB. (2023). *Diagnóstico de Adopción Tecnológica y Madurez Digital en Micro y Pequeñas Empresas Manufactureras de Bogotá y Cundinamarca*. Vicepresidencia de Fortalecimiento Empresarial. https://www.ccb.org.co/
* [2] National Institute of Standards and Technology — NIST. (2021). *Small Business Cybersecurity Corner: Planning and Managing Information Security for Small Businesses*. U.S. Department of Commerce. https://www.nist.gov/itl/smallbusinesscyber
* [3] Amazon Web Services — AWS. (2023). *Reliability Pillar: AWS Well-Architected Framework (Design Principles for Eliminating Single Points of Failure)*. AWS Architecture Center. https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/
* [4] Ministerio de Tecnologías de la Información y las Comunicaciones — MinTIC. (2023). *Guía de Ciberseguridad y Respaldo de Información para Micro, Pequeñas y Medianas Empresas en Colombia*. Estrategia Nacional de Seguridad Digital. https://www.mintic.gov.co/
* [5] Cybersecurity and Infrastructure Security Agency — CISA. (2023). *Data Backup Options and the 3-2-1 Rule for Small Business Resilience*. CISA Insights. https://www.cisa.gov/resources-tools/resources/data-backup-options
