# 🛒 E-Commerce Lakehouse & Customer Intelligence

![Python](https://img.shields.io/badge/Python-14354C?style=for-the-badge&logo=python&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache_Spark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=tableau&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white)

Una plataforma analítica de e-commerce moderna construida sobre **Databricks** y **PySpark**, implementando una arquitectura **Medallion Lakehouse (Bronce, Plata, Oro)** y un Data Warehouse dimensional para Business Intelligence.

Este proyecto procesa más de 100,000 registros transaccionales (basado en el dataset público de Olist), aplicando ingeniería de datos rigurosa para transformar datos crudos en métricas de negocio accionables.

---

## 🏗️ Arquitectura de Datos (Medallion)

```mermaid
flowchart TD
    subgraph Data Sources
        Olist[Olist Dataset<br/>Kaggle CSVs]
    end

    subgraph Databricks [Databricks Lakehouse]
        Bronze[(Bronze Layer<br/>Raw Data)]
        Silver[(Silver Layer<br/>Cleansed & Integrated)]
        Gold[(Gold Layer<br/>Star Schema / DWH)]
    end

    subgraph BI [Business Intelligence]
        Tableau[Tableau<br/>Executive Dashboard]
    end

    Olist -- Ingesta a Unity Catalog --> Bronze
    Bronze -- PySpark<br/>Limpieza, Casteo y Deduplicación --> Silver
    Silver -- PySpark<br/>Joins y Modelado Dimensional --> Gold
    Gold -- Exportación Analítica --> Tableau

    style Bronze fill:#cd7f32,stroke:#333,stroke-width:1px,color:#fff
    style Silver fill:#c0c0c0,stroke:#333,stroke-width:1px,color:#000
    style Gold fill:#ffd700,stroke:#333,stroke-width:1px,color:#000
    style Tableau fill:#e97627,stroke:#333,stroke-width:1px,color:#fff
    style Databricks fill:#f8f8f8,stroke:#e25a1c,stroke-width:2px,stroke-dasharray: 5 5
```

El pipeline de datos está orquestado en 3 capas progresivas utilizando **Delta Lake**:

1. **🥉 Capa Bronce (Raw):** Ingesta inmutable de datos transaccionales crudos (Orders, Items, Products, Customers) preservando el esquema original.
2. **🥈 Capa Plata (Cleansed & Integrated):** Limpieza de datos, *type casting*, manejo de valores nulos, deduplicación e integración de entidades mediante uniones optimizadas en Spark.
3. **🥇 Capa Oro (Data Warehouse):** Modelado dimensional (*Star Schema*) optimizado para consultas analíticas. Generación de llaves subrogadas y métricas de negocio pre-calculadas.

## 📊 Calidad de Datos (Data Quality)

Se implementaron controles automatizados con PySpark antes de exponer la información a la capa analítica, logrando:
* **Registros procesados:** 112,650
* **Integridad referencial (Llaves nulas):** 0
* **Consistencia de negocio (Precios inválidos):** 0
* ✅ **Tasa de registros válidos:** 100.00%

---

## 📈 Análisis y Business Intelligence (Frontend Analítico)

> **[En desarrollo]** Esta capa consumirá el modelo dimensional (Capa Oro) para responder preguntas críticas del negocio.

* **Herramienta:** Tableau
* **KPIs Core:** Ingresos totales, ticket promedio, volumen de ventas por categoría.
* **Dashboard Interactivo:** *(El enlace a Tableau Public se añadirá pronto)*
* **Vista previa:** *(Imagen del dashboard se añadirá pronto)*

---

## 💻 Tecnologías Utilizadas
* **Procesamiento Distribuido:** Apache Spark, PySpark
* **Infraestructura & Almacenamiento:** Databricks, Delta Lake, Unity Catalog
* **Lenguajes:** Python, SQL
* **Modelado:** Dimensional Modeling (Star Schema)