# Reflexión Individual

## Nombre del Estudiante
**David Santiago Buendia Londoño** (`@Santiagoob7` · Código `306487` · [davidbulo@unisabana.edu.co](mailto:davidbulo@unisabana.edu.co))

## Rol en el equipo
Co-arquitecto y responsable principal de la formulación de la **Visión Preliminar (Taller 0)**, la arquitectura de sistemas actuales (**C4 C1 y C2 — Taller 3**), el mapa y diagnóstico técnico de **Infraestructura (Taller 4)**, la evaluación de amenazas (**STRIDE — Taller 5**), la integración vertical de 5 capas (**Taller 8**) y la consolidación de la matriz de riesgos, gobernanza y presentación ejecutiva (**Taller 9**).

## Aprendizajes Clave

- **Aprendí a modelar entornos *Shadow IT* sin forzar patrones corporativos artificiales:** al aplicar C4 (Taller 3), Infraestructura (Taller 4) y STRIDE (Taller 5) sobre Insuclínicos Ltda., comprobé que un "contenedor" o un "punto único de falla" en una PyME de 6 personas no es un clúster Kubernetes ni una API REST, sino dos libros locales de Excel compartidos por LAN, sesiones de Windows sin usuario propio y carpetas SMB abiertas.
- **Comprendí el valor de la integración vertical para detectar brechas ocultas:** en el Taller 8, al conectar los hilos *end-to-end* desde Negocio hasta Seguridad y Normatividad, resultó evidente que la causa raíz de varios problemas (descuadres de tela SMS, bloqueos de lectura/escritura y falta de rastro sanitario INVIMA) convergía exactamente sobre el mismo nodo físico del disco duro local y la desconexión con la planta.
- **Aprendí que priorizar riesgos en un roadmap requiere cruzar Nivel con Esfuerzo:** al construir la matriz de 7 dominios y el plan de implementación en el Taller 9 entendí por qué un riesgo crítico (`Nivel 9`, silos de Excel) no se resuelve el día 1, mientras un riesgo de menor esfuerzo (`WP1`, backup 3-2-1, cuentas nominales y aviso Ley 1581) genera protección real e inmediata sin detener la producción.

## Retos Superados

- **Tuve dificultades con representar amenazas STRIDE y diagramas multicapa sin generar grafos confusos**, pero logré superarlo estructurando el DFD alrededor del límite de confianza real de la red local (Taller 5), organizando el tablero integrado por hilos de negocio diferenciados por color (Taller 8) y aplicando la notación de capas y *Plateaus* de ArchiMate (Taller 9).
- **Traducir hallazgos técnicos a decisiones ejecutivas acotadas al negocio:** al inicio resultaba tentador proponer controles complejos o compra de servidores locales; trabajar sobre las restricciones de Insuclínicos (`<= $3M COP/año` y reúso de PCs) me enseñó a diseñar controles pragmáticos y aceptar explícitamente riesgos menores (`R10` hardware sin espejo local) cuando mitigarlos cuesta más que el impacto.

## Áreas por Mejorar

- Me gustaría reforzar mis conocimientos en **automatización práctica de infraestructura y pruebas reales de recuperación ante desastres (DRP/Backup 3-2-1)** en entornos nube gestionados para microempresas.
- Reconozco que debo mejorar la **síntesis ejecutiva para audiencias no técnicas**, cuidando que las explicaciones en comité prioricen el impacto operativo y financiero para el cliente antes que los detalles técnicos de infraestructura o esquemas de datos.

## Contribución Personal

Mi mayor aporte al Grupo 8 fue diseñar la línea técnica de arquitectura de aplicaciones, infraestructura, seguridad e integración: redacté el Documento de Visión inicial, modelé el ecosistema *Shadow IT* en C4 y el mapa de 3 zonas donde identificamos el SPOF crítico, estructuré el análisis de amenazas STRIDE (`T1`–`T6`), construí el tablero integrado de 5 capas del Taller 8 y consolidé el paquete final de riesgos, vistas ArchiMate y presentación ejecutiva del Taller 9.

---

_Esta reflexión individual hace parte de la entrega final del curso AREM - Arquitectura Empresarial - Universidad de La Sabana._
