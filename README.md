# Customer Satisfaction Analysis in Olist Marketplace

La satisfacción del cliente es uno de los principales indicadores de desempeño en plataformas de comercio electrónico. Comprender qué factores influyen en la experiencia de compra permite detectar oportunidades de mejora en los procesos logísticos y comerciales, además de facilitar la toma de decisiones basada en datos.

Se seleccionó el dataset Brazilian E-commerce Public Dataset by Olist porque representa un caso de negocio real y contiene información completa sobre el ciclo de una compra: clientes, pedidos, productos, pagos, vendedores y reseñas. Esta estructura relacional permite construir un análisis más completo que un EDA tradicional, integrando múltiples fuentes de datos para estudiar el comportamiento de los clientes.

## Descripción del proyecto

Este proyecto tiene como objetivo analizar los factores que influyen en la satisfacción de los clientes dentro del marketplace brasileño Olist mediante un proceso de Análisis Exploratorio de Datos (EDA).

A partir de la integración de múltiples conjuntos de datos se construyó un único dataset analítico que reúne información sobre pedidos, clientes, pagos, productos y reseñas. Sobre esta base se busca comprender cómo distintas variables del proceso de compra y entrega pueden afectar la calificación otorgada por los clientes.

### Objetivo

Analizar la relación entre el proceso de compra y la satisfacción del cliente, identificando qué variables presentan una mayor influencia sobre la calificación final de cada pedido.

### Hipótesis

Se plantea que los retrasos en la entrega tienen un mayor impacto en la satisfacción del cliente que el valor económico de la compra, provocando una disminución en las calificaciones cuando los pedidos son entregados fuera del plazo esperado.

### Dataset

Se utilizó el Brazilian E-commerce Public Dataset by Olist, un conjunto de datos públicos que contiene información de un marketplace brasileño entre 2016 y 2018.

El proyecto integra información proveniente de distintos datasets relacionados con:

- Clientes
- Pedidos
- Productos
- Pagos
- Reseñas
- Vendedores 

![Data Base](data_base.jpg)

### Metodologia 

El desarrollo del proyecto siguió un flujo completo de análisis de datos, desde la comprensión de las fuentes de información hasta la obtención de conclusiones orientadas al negocio.

Las principales etapas fueron:

- Exploración y comprensión de los datasets.
- Evaluación de la calidad de los datos.
- Selección de variables relevantes para el análisis.
- Integración de múltiples tablas mediante claves relacionales.
- Limpieza y transformación de los datos.
- Creación de nuevas variables mediante Feature Engineering.
- Construcción y validación del dataset analítico.
- Análisis Exploratorio de Datos (EDA).
- Análisis de la relación entre las variables y la satisfacción del cliente.
- Obtención de hallazgos y conclusiones de negocio.

### Dataset Analítico

Para responder la hipótesis se construyó un dataset integrado utilizando información de los siguientes conjuntos de datos

| Dataset        | Variables principales                            |
| -------------- | ------------------------------------------------ |
| Customers      | Ubicación del cliente                            |
| Orders         | Estado del pedido y fechas del proceso de compra |
| Order Items    | Precio, cantidad de productos y costo de envío   |
| Order Payments | Valor total y cuotas del pago                    |
| Order Reviews  | Calificación del cliente                         |
| Products       | Categoría del producto                           |
| Sellers        | Ubicación del vendedor                           |


### Variables creadas

Como parte del proceso de Feature Engineering se generaron nuevas variables orientadas al análisis del proceso logístico.

| Variable                | Descripción                                                |
| ----------------------- | ---------------------------------------------------------- |
| delivery_time_days      | Tiempo total de entrega del pedido                         |
| approval_time_hours     | Tiempo transcurrido hasta la aprobación del pago           |
| estimated_delivery_days | Tiempo estimado de entrega                                 |
| delivery_delay_days     | Diferencia entre la entrega real y la fecha estimada       |
| late_delivery           | Indica si el pedido fue entregado fuera del plazo previsto |

### Herramientas utilizadas
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

## Análisis realizado

Una vez construido el dataset analítico se desarrolló un análisis exploratorio orientado a comprender qué factores presentan una mayor asociación con la satisfacción del cliente.

El análisis se dividió en dos etapas:

### Análisis univariado

Se estudió el comportamiento individual de las principales variables mediante estadísticas descriptivas y visualizaciones, permitiendo analizar su distribución, detectar valores atípicos y comprender las características generales del dataset.

Entre las variables exploradas se encuentran:

- Calificación de los clientes
- Tiempo de entrega
- Tiempo estimado de entrega
- Retrasos
- Valor de la compra
- Costo de envío
- Cantidad de productos
- Cantidad de pagos

### Análisis relacional

Posteriormente se evaluó la relación entre la variable objetivo (**review_score**) y distintas variables del proceso de compra para identificar cuáles presentan una mayor asociación con la satisfacción del cliente.

Se analizaron las siguientes relaciones:

- Tiempo de entrega vs. satisfacción.
- Cumplimiento del plazo de entrega vs. satisfacción.
- Valor de la compra vs. satisfacción.
- Costo de envío vs. satisfacción.
- Cantidad de productos vs. satisfacción.
- Cantidad de pagos vs. satisfacción.

## Principales resultados

El análisis permitió identificar diferencias importantes entre los distintos factores estudiados.

Los principales hallazgos fueron:

- El tiempo de entrega presenta una clara asociación con la satisfacción del cliente.
- El cumplimiento del plazo prometido resultó ser el factor con mayor relación con las calificaciones otorgadas.
- El valor económico de la compra mostró una influencia limitada sobre las reseñas.
- El costo de envío presentó únicamente una asociación débil con la satisfacción.
- La cantidad de productos y el número de pagos no evidenciaron una relación significativa con las calificaciones.

En conjunto, los resultados respaldan la hipótesis planteada al inicio del proyecto, indicando que el desempeño logístico influye considerablemente más en la satisfacción del cliente que el valor económico de la compra.

## Dashboard Interactivo

Como complemento del análisis exploratorio, se desarrolló un dashboard interactivo en Power BI con el objetivo de resumir los principales hallazgos del proyecto de forma visual e intuitiva.

El dashboard presenta los indicadores más relevantes relacionados con la satisfacción del cliente, incluyendo métricas generales, la distribución de las calificaciones y las principales variables analizadas durante el EDA, como el tiempo de entrega, el porcentaje de pedidos con retraso, el precio promedio y el costo de envío. De esta manera, permite identificar rápidamente los factores que muestran una mayor asociación con las reseñas de los clientes y facilita la interpretación de los resultados obtenidos.

## Vista del Dashboard

![Dashboard de Power BI](olist-customer-satisfaction-analysis.jpg)

## Conclusiones

El proyecto permitió construir un dataset analítico a partir de múltiples fuentes de información y analizar los principales factores asociados a la satisfacción del cliente en el marketplace de Olist.

Los resultados muestran que las variables relacionadas con la logística, especialmente el tiempo de entrega y el cumplimiento del plazo prometido, presentan una asociación considerablemente mayor con las calificaciones otorgadas por los clientes que variables económicas como el valor de la compra o el costo de envío.

Estos hallazgos evidencian la importancia de optimizar el desempeño logístico para mejorar la experiencia de compra y demuestran cómo un proceso completo de preparación, integración y análisis de datos puede generar información útil para la toma de decisiones.