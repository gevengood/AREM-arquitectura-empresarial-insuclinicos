# 📚 Referencias Bibliográficas del Taller

Este archivo contiene las fuentes primarias, normativas y metodológicas consultadas para el desarrollo del Taller 8 (integración multi-vista AS-IS y TO-BE aplicada a **Insuclínicos Ltda.** y caso base **FarmApp**).

## 🔖 Taller
Taller 8 — Integración de Vistas de Arquitectura

---

## 📚 Referencias utilizadas

### Estándares de Arquitectura Empresarial y Trazabilidad
1. **ISO/IEC/IEEE.** (2022). *ISO/IEC/IEEE 42010:2022 — Software, systems and enterprise — Architecture description* (Conceptos de vistas, puntos de vista, correspondencias y verificación de consistencia entre vistas). International Organization for Standardization. [https://www.iso.org/standard/74393.html](https://www.iso.org/standard/74393.html) *(Fecha de verificación: noviembre de 2026)*.
2. **The Open Group.** (2022). *ArchiMate® 3.2 Specification — Cross-Layer Dependencies and Layered Viewpoint*. The Open Group. [https://pubs.opengroup.org/architecture/archimate32-doc/](https://pubs.opengroup.org/architecture/archimate32-doc/) *(Fecha de verificación: noviembre de 2026)*.
3. **The Open Group.** (2022). *The TOGAF® Standard, 10th Edition — Architecture Views, Viewpoints, and Stakeholders*. The Open Group. [https://www.opengroup.org/togaf](https://www.opengroup.org/togaf) *(Fecha de verificación: noviembre de 2026)*.
4. **Brown, Simon.** (2022). *The C4 Model for Visualising Software Architecture*. [https://c4model.com/](https://c4model.com/) *(Base para la trazabilidad de contenedores AS-IS y TO-BE en la capa de aplicaciones)*.

### Normatividad Sanitaria, Protección de Datos y Seguridad (Conexión Capa 5)
5. **Ministerio de la Protección Social & INVIMA.** (2005). *Decreto 4725 de 2005: Por el cual se reglamenta el régimen de registros sanitarios, permiso de comercialización y vigilancia sanitaria de los dispositivos médicos para uso humano*. Diario Oficial No. 46.134. [https://www.minsalud.gov.co/sites/rid/Lists/BibliotecaDigital/RIDE/DE/DIJ/Decreto-4725-de-2005.pdf](https://www.minsalud.gov.co/sites/rid/Lists/BibliotecaDigital/RIDE/DE/DIJ/Decreto-4725-de-2005.pdf) *(Justifica la obligatoriedad del campo `lote_sms_invima` desde la orden de producción hasta la remisión)*.
6. **Ministerio de la Protección Social & INVIMA.** (2008). *Resolución 4816 de 2008: Por la cual se reglamenta el Programa Nacional de Tecnovigilancia*. Diario Oficial No. 47.185. [https://www.invima.gov.co/](https://www.invima.gov.co/) *(Exige trazabilidad bidireccional ante alertas sanitarias o retiros de producto)*.
7. **Congreso de la República de Colombia.** (2012). *Ley Estatutaria 1581 de 2012: Por la cual se dictan disposiciones generales para la protección de datos personales*. Diario Oficial No. 48.587. [http://www.secretariasenado.gov.co/senado/basedoc/ley_1581_2012.html](http://www.secretariasenado.gov.co/senado/basedoc/ley_1581_2012.html) *(Condiciona el canal de WhatsApp Business y la entidad `CLIENTE`)*.
8. **Dirección de Impuestos y Aduanas Nacionales (DIAN).** (2023). *Resolución 000165 de 2023: Sistema de facturación electrónica y anexo técnico*. [https://www.dian.gov.co/](https://www.dian.gov.co/) *(Regula la interfaz del Exportador / Conector de Facturación)*.
9. **International Organization for Standardization (ISO).** (2022). *ISO/IEC 27001:2022 — Information security, cybersecurity and privacy protection (Controles A.5.15, A.8.2, A.8.13, A.8.15, A.8.24)*. [https://www.iso.org/standard/27001](https://www.iso.org/standard/27001).
10. **International Organization for Standardization (ISO).** (2016). *ISO 13485:2016 — Medical devices — Quality management systems (Numeral 7.5.9 Identificación y Trazabilidad)*. [https://www.iso.org/standard/59752.html](https://www.iso.org/standard/59752.html).

### Material Académico y Documentación Interna del Proyecto
11. **Vega Fernández, César Augusto.** (2026). *Taller 8: Integración de Vistas de Arquitectura — Guía paso a paso, visualización interactiva de FarmApp y plantillas*. Curso Arquitectura Empresarial (AREM), Universidad de La Sabana. [https://github.com/CesarAVegaF312/AREM-Taller_8_Integracion_Vistas](https://github.com/CesarAVegaF312/AREM-Taller_8_Integracion_Vistas).
12. **Grupo 8 — Insuclínicos Ltda.** (2026). *Repositorio consolidado del proyecto (`00-preliminary-vision` a `07-opportunities-solutions`)*. Universidad de La Sabana.

### Uso de Inteligencia Artificial
- **Fuente asistida por IA:** Asistente de IA (noviembre de 2026). Utilizado para verificar consistencia nominal de elementos entre las Fases 00–07, estructurar las coordenadas sin solapamientos de los tableros en draw.io y apoyar la redacción de la narrativa de coherencia y la investigación sobre ISO/IEC/IEEE 42010 y ArchiMate en PyMEs. Todas las conexiones, nombres de entidades y decisiones del cliente fueron contrastadas manualmente contra los entregables reales del repositorio.

---

*Este archivo forma parte de la entrega académica del Taller 8 del curso AREM — Universidad de La Sabana.*
