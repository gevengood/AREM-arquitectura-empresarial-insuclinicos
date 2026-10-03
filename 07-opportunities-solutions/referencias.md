# Referencias Bibliográficas e Investigación Complementaria del Taller

Este archivo contiene las fuentes académicas, normativas y técnicas consultadas para el diseño de la arquitectura objetivo (TO-BE), el análisis de brechas (*Gap Analysis*) y la matriz de decisión ponderada de **Insuclínicos Ltda.** en el **Taller 7**.

## Taller
**Taller 7 — Opportunities & Solutions (Arquitectura Objetivo TO-BE y Análisis de Brechas)**

---

## Síntesis de Investigación Complementaria (Patrones de Solución para PyMEs Manufactureras del Sector Salud)

Para fundamentar la transición de **Insuclínicos Ltda.** desde hojas de cálculo aisladas (*Shadow IT*) hacia una arquitectura centralizada, se investigaron tres patrones de referencia aplicables a pequeñas empresas manufactureras de insumos médicos en Colombia:

1. **Adopción de ERP/CRM Ligero en la Nube (SaaS/PaaS) frente a Hojas de Cálculo en PyMEs Manufactureras:**
   La literatura sobre transformación digital en micro y pequeñas empresas demuestra que el uso de hojas de cálculo compartidas en red local colapsa cuando concurren procesos de ventas, abastecimiento de materia prima y órdenes de producción, debido a la ausencia de integridad referencial ACID y bloqueos de archivo. El patrón recomendado para empresas de menos de 20 empleados es la adopción modular de un **ERP/CRM ligero de código abierto o SaaS gestionado** (como *Odoo* o *Dolibarr* sobre PostgreSQL), habilitando inicialmente solo el núcleo comercial y de inventarios (*Quick-to-Value*) antes de digitalizar el piso de planta.
2. **Patrón de Trazabilidad de Lotes hacia Adelante y hacia Atrás (*Forward & Backward Lot Traceability*) para Dispositivos Médicos:**
   Bajo el **Decreto 4725 de 2005** y la **Resolución 4816 de 2008** (Programa Nacional de Tecnovigilancia del INVIMA), todo fabricante de ropa e insumos quirúrgicos desechables (Clasificación de Riesgo I / IIa) debe poder reconstruir la cadena `Lote de Materia Prima (Rollo SMS del proveedor) → Orden de Producción Interna → Lote de Producto Terminado → Remisión / Factura de la Clínica`. En sistemas ERP ligeros, este patrón se implementa exigiendo el número de lote como clave foránea obligatoria al consumir inventario en planta y estampándolo automáticamente en el documento PDF de despacho.
3. **Estrategia de Respaldo 3-2-1 e Inmutabilidad Cloud frente a Fallos de Hardware y Ransomware:**
   Conforme a **ISO/IEC 27001:2022 (Control A.8.13)** y las guías del NIST para PyMEs, eliminar el Punto Único de Falla (SPOF) de un computador de oficina requiere externalizar la base de datos a una instancia cloud gestionada con copias automáticas diarias en un segundo contenedor de almacenamiento de objetos inmutable (*Object Lock*), garantizando un punto de recuperación ($RPO \le 24\text{ h}$) sin intervención humana.

---

## Referencias utilizadas (Formato APA 7.ª Edición)

1. **The Open Group.** (2022). *The TOGAF® Standard, 10th Edition — Phase E: Opportunities & Solutions and Gap Analysis*. The Open Group. https://pubs.opengroup.org/togaf-standard/adm-phases/chap09.html
2. **The Open Group.** (2022). *ArchiMate® 3.2 Specification — Chapter 13: Implementation and Migration Elements (Plateau, Gap, Work Package)*. The Open Group. https://pubs.opengroup.org/architecture/archimate32-doc/chap13.html
3. **Brown, S.** (2022). *The C4 Model for Visualizing Software Architecture: System Context and Container Views*. C4Model.com. https://c4model.com/
4. **Ministerio de la Protección Social de Colombia.** (2005). *Decreto 4725 de 2005: Por el cual se reglamenta el régimen de registros sanitarios, permiso de comercialización y vigilancia sanitaria de los dispositivos médicos para uso humano*. Diario Oficial No. 46.134. https://www.minsalud.gov.co/sites/rid/Lists/BibliotecaDigital/RIDE/DE/DIJ/Decreto-4725-de-2005.pdf
5. **Ministerio de la Protección Social de Colombia & INVIMA.** (2008). *Resolución 4816 de 2008: Por la cual se reglamenta el Programa Nacional de Tecnovigilancia*. Diario Oficial No. 47.201. https://www.invima.gov.co/
6. **Congreso de la República de Colombia.** (2012). *Ley Estatutaria 1581 de 2012: Por la cual se dictan disposiciones generales para la protección de datos personales*. Diario Oficial No. 48.587. http://www.secretariasenado.gov.co/senado/basedoc/ley_1581_2012.html
7. **International Organization for Standardization [ISO].** (2022). *ISO/IEC 27001:2022 Information security, cybersecurity and privacy protection — Information security management systems — Requirements*. ISO. https://www.iso.org/standard/27001
8. **Shostack, A.** (2014). *Threat Modeling: Designing for Security* (STRIDE Methodology). Wiley. ISBN: 978-1-118-80999-0.
9. **Odoo S.A.** (2025). *Odoo Inventory & Manufacturing Documentation: Lot and Serial Number Traceability*. https://www.odoo.com/documentation/17.0/applications/inventory_and_mrp/inventory/product_management/product_tracking/lots.html
10. **Vega, C. A.** (2026). *Guía Paso a Paso: Opportunities & Solutions y Guías de Notación ArchiMate — Curso de Arquitectura Empresarial (AREM)*. Universidad de La Sabana. https://github.com/CesarAVegaF312/AREM-Taller_7_Opportunities_Solutions
11. **Entregables previos del Grupo 8 (Insuclínicos Ltda.):**
    - *Talleres 0, 1 y 2 (Visión Preliminar, BPMN y Modelo Conceptual de Datos)*: Repositorio Corte 1 (`AREM-arquitectura-empresarial-insuclinicos`).
    - *Taller 3 (Arquitectura de Aplicaciones C4 AS-IS)*: `AREM-Taller_3_Arquitectura_C4`.
    - *Taller 4 (Mapa de Infraestructura y Riesgos AS-IS)*: `AREM-Taller_4_Infraestructura`.
    - *Taller 5 (Evaluación de Seguridad con STRIDE)*: `Taller-5-Evaluaci-n-de-Seguridad-con-STRIDE`.
    - *Taller 6 (Auditoría de Cumplimiento y Normatividad)*: `taller-06-normatividad`.
12. **Fuente asistida por IA:** *Asistente de IA (Copiloto metodológico usado bajo el protocolo de verificación y recálculo de la sección 2.2 de la guía), octubre de 2026*.

---

_Este archivo forma parte de la entrega académica del Taller 7 del curso Arquitectura Empresarial (AREM) - Universidad de La Sabana._
