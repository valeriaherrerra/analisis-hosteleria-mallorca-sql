# Análisis de Datos para la Identificación de Oportunidades Comerciales B2B en la Hostelería de Mallorca

## Descripción del Proyecto
Este proyecto de inteligencia de negocio y analítica de datos surge como una solución estratégica real para identificar clientes potenciales de alto valor en el sector de la hostelería de Palma de Mallorca (Casco Antiguo, Paseo del Borne, Santa Catalina y Vía Alemania/Blanquerna).

El objetivo principal es optimizar la prospección comercial B2B detectando aquellos restaurantes que cuentan con una excelente reputación en su cocina general (calificaciones Google entre 4.3 y 4.9 estrellas) pero cuyas reseñas revelan una debilidad latente o insatisfacción en su menú de postres (menciones de repostería industrial, tarta de queso seca o desactualizada). De este modo, el equipo comercial puede presentarse ofreciendo una solución directa a una pérdida de facturación identificada.

## Stack Tecnológico Utilizado
* **Extracción de Datos (Web Scraping):** Captura automatizada en la nube a través de herramientas de extracción de Google Places.
* **Procesamiento de Datos & Almacenamiento:** **Google BigQuery** (Servidores localizados en la región de Madrid, Europa) para el modelado de la base de datos relacional.
* **Análisis de Datos:** Consultas condicionales avanzadas empleando cláusulas de filtrado e instrucciones de unificación en SQL.
* **Visualización de Datos:** Google Sheets para el análisis descriptivo y resúmenes estadísticos por zonas.

##  Estructura del Repositorio
* `dataset_restaurantes_palma.csv`: Archivo de datos unificado y limpio con las columnas de nombre, zona, calificación general y comentarios extraídos.
* `README.md`: Documentación técnica y desglose metodológico del proyecto.

## Código SQL de la Consulta Unificada (BigQuery)
A continuación se detalla la consulta avanzada utilizada en Google BigQuery para filtrar las quejas de postres y unificar las tres principales áreas gastronómicas de Palma de Mallorca en una única vista comercial:

```sql
-- 1. Filtrado de Oportunidades en Santa Catalina
SELECT nombre, 'Santa Catalina' AS zona, nota_general, resena_texto
FROM analisis_mallorca.santa_catalina
WHERE resena_texto LIKE '%tarta de queso%'
   OR resena_texto LIKE '%postre%'
   OR resena_texto LIKE '%tiramisu%'
   OR resena_texto LIKE '%brownie%'

UNION ALL

-- 2. Filtrado de Oportunidades en Casco Antiguo / Borne
SELECT nombre, 'Casco Antiguo / Borne' AS zona, nota_general, resena_texto
FROM analisis_mallorca.casco_antiguo
WHERE resena_texto LIKE '%tarta de queso%'
   OR resena_texto LIKE '%postre%'
   OR resena_texto LIKE '%tiramisu%'
   OR resena_texto LIKE '%brownie%'

UNION ALL

-- 3. Filtrado de Oportunidades en Blanquerna / Vía Alemania
SELECT nombre, 'Blanquerna / Via Alemania' AS zona, nota_general, resena_texto
FROM analisis_mallorca.blanquerna_alemania
WHERE resena_texto LIKE '%tarta de queso%'
   OR resena_texto LIKE '%postre%'
   OR resena_texto LIKE '%tiramisu%'
   OR resena_texto LIKE '%brownie%'

-- Consolidación y ordenación del mercado de Palma de mayor a menor reputación
ORDER BY nota_general DESC;
```

## Conclusiones Principales del Estudio Comercial
A través de este modelo analítico, se lograron centralizar un total de **23 oportunidades comerciales de alto valor** distribuidas estratégicamente de la siguiente manera:
1. **Casco Antiguo / Borne:** 11 restaurantes identificados (Liderados por *Breogán Cocina Gallega* con 4.9 estrellas).
2. **Santa Catalina:** 7 restaurantes identificados (Liderados por *Sumaq Peruano* con 4.8 estrellas).
3. **Blanquerna / Vía Alemania:** 5 restaurantes identificados (Liderados por *Urbe Blanquerna* con 4.8 estrellas).

*Estrategia de Ventas:* El análisis demuestra que Santa Catalina y el Casco Antiguo manejan los estándares de reputación más exigentes (puntuaciones medias de 4.61 y 4.59 respectivamente), lo que los convierte en los clientes ideales para una propuesta B2B premium.
