# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller 4 - Mapa de Infraestructura y Diagnóstico Técnico

## 👥 Integrantes del equipo
* David Santiago Buendia Londoño (Santiagoob7)
* Jorge Steven Doncel (gevengood)

## 🧠 Descripción general del trabajo
El objetivo de este taller fue levantar el mapa de infraestructura actual (AS-IS) de Insuclínicos Ltda., enfocado en el macro-proceso de Gestión y Cumplimiento de Pedido. A través de este ejercicio, se realizó un diagnóstico técnico para identificar puntos únicos de falla, cuellos de botella y límites de escalabilidad en un entorno operado casi en su totalidad mediante herramientas ofimáticas locales ("Shadow IT") y transporte manual de información.

## 🔧 Proceso de desarrollo
El modelado se realizó en draw.io utilizando formas geométricas estándar para infraestructura, prescindiendo del modelo C4 estricto para reflejar adecuadamente la naturaleza física de la red. 
Primero, agrupamos los elementos en tres zonas lógicas: Nube Pública, Red Local (LAN) y Planta de Producción. Luego, diagramamos los equipos de cómputo y el almacenamiento local. Finalmente, aplicamos la metodología de diagnóstico marcando con advertencias (⚠️) los nodos críticos que carecen de redundancia, evidenciando que el principal cuello de botella no es de red, sino de concurrencia en la lectura y escritura de archivos locales.

## 🧩 Análisis del modelo propuesto
* **Estructura del modelo:** El mapa divide la infraestructura en servicios de terceros (nube), la oficina central (hardware físico) y la planta de producción (donde la transmisión de datos es analógica/física).
* **Representación de necesidades:** El diagrama demuestra el alto nivel de riesgo operativo del cliente. Al marcar el disco duro local que aloja los archivos de Excel como instancia única, se justifica la necesidad técnica de implementar una base de datos centralizada a futuro.
* **Supuestos:** Se asume que los PC de Ventas y Almacén están en la misma red física pero no cuentan con un servidor de archivos dedicado (NAS) ni políticas de copias de seguridad automatizadas.

## 📈 Diagrama final entregado
* [Ver Mapa de Infraestructura Final (AS-IS)](./mapa-final.drawio)

## 📋 Tabla de Diagnóstico Técnico

| Componente | Riesgo diagnosticado | Categoría | Impacto si ocurre | Prioridad |
| :--- | :--- | :--- | :--- | :--- |
| Disco Duro Local (Archivos Excel) | Punto único de falla (hardware) | Disponibilidad | Pérdida total de la información de inventario y pedidos. | Alta |
| Archivos de Excel | Concurrencia limitada / Cuello de botella | Rendimiento | Bloqueos de edición entre Ventas y Almacén; retrasos operativos. | Alta |
| PC Ventas / PC Almacén | Hardware sin redundancia | Disponibilidad | Inaccesibilidad temporal a los datos si el equipo físico falla. | Media |
| Transporte manual a Planta | Límite de escalabilidad | Escalabilidad | Retrasos en la línea si el volumen de pedidos supera la capacidad manual de comunicación. | Media |

## 🔍 Investigación complementaria

**Tema investigado:** Gestión de riesgos en arquitecturas de "Shadow IT" (TI en la sombra) para Pymes.

**Resumen:**
El concepto de "Shadow IT" se refiere a los sistemas, dispositivos y software utilizados dentro de una organización sin la aprobación explícita o gestión del departamento de TI. En Pymes como Insuclínicos, el uso intensivo de hojas de cálculo alojadas localmente y redes de mensajería personales (WhatsApp) forma una infraestructura ofimática que soporta procesos críticos, pero carece de estándares de seguridad, redundancia (alta disponibilidad) y escalabilidad.

La literatura técnica sobre migración a la nube subraya que el mayor riesgo de estas arquitecturas es el acoplamiento físico a hardware de grado de consumidor (puntos únicos de falla). Modernizar este esquema no requiere necesariamente un ERP robusto de inmediato; el primer paso arquitectónico recomendado es desacoplar el almacenamiento de datos del hardware local mediante bases de datos relacionales ligeras o repositorios centralizados en la nube (PaaS), permitiendo concurrencia segura y mitigando el riesgo de pérdida total de datos.

## 📚 Referencias
* [1] Gartner. "Shadow IT: Mitigating Security Risks". 2023. 
* [2] AWS Architecture Center. "Reliability Pillar - AWS Well-Architected Framework" (Conceptos de redundancia y eliminación de puntos únicos de falla). https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/
