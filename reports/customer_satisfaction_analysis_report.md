# Análisis de la Satisfacción del Cliente en el Marketplace Olist
## 1. Introducción

En el comercio electrónico, la satisfacción del cliente representa uno de los principales indicadores para evaluar la calidad del servicio ofrecido por una empresa. Factores como los tiempos de entrega, el cumplimiento de los plazos prometidos, el costo del envío o el valor de la compra pueden influir directamente en la experiencia del cliente y, en consecuencia, en la calificación que este otorga al finalizar una compra.

El objetivo de este proyecto es desarrollar un análisis exploratorio utilizando el Brazilian E-commerce Public Dataset by Olist, con el propósito de comprender qué variables presentan una mayor relación con la satisfacción del cliente.

A diferencia de otros análisis que trabajan sobre un único conjunto de datos, este proyecto requiere integrar múltiples tablas relacionadas mediante un modelo relacional, construir un dataset analítico y generar nuevas variables que permitan representar el comportamiento del proceso logístico y comercial de cada pedido.

## 2. Problema de negocio

En un marketplace participan múltiples vendedores, productos y clientes, por lo que identificar qué aspectos afectan la satisfacción del cliente resulta fundamental para mejorar la experiencia de compra.

Comprender estas relaciones permite responder preguntas como:

- ¿Los retrasos en la entrega afectan las calificaciones?
- ¿Los clientes que realizan compras de mayor valor son más exigentes?
- ¿Existen diferencias entre regiones?
- ¿Qué variables permiten explicar una buena o una mala experiencia de compra?

Responder estas preguntas puede ayudar a optimizar procesos logísticos, mejorar los niveles de servicio y aumentar la satisfacción del cliente.

## 3. Objetivo

Analizar la relación entre las características del proceso de compra y la satisfacción del cliente mediante la construcción de un dataset analítico y la aplicación de técnicas de análisis exploratorio de datos.

## 4. Hipótesis

Se plantea la siguiente hipótesis de trabajo:

Los retrasos en la entrega tienen un mayor impacto en la satisfacción del cliente que el valor económico de la compra.

A lo largo del proyecto esta hipótesis será evaluada mediante el análisis de las variables temporales, económicas y logísticas disponibles en el dataset.

## 5. Dataset

Para este proyecto se utilizó el Brazilian E-commerce Public Dataset by Olist, un conjunto de datos público que contiene información de compras realizadas entre los años 2016 y 2018.

El dataset se encuentra organizado mediante un modelo relacional compuesto por múltiples tablas que representan las distintas etapas del proceso de compra.

Entre ellas se encuentran:

- Customers
- Orders
- Order Items
- Order Payments
- Order Reviews
- Products
- Sellers
- Geolocation
- Product Category Translation

Cada una aporta información específica que posteriormente será integrada para construir un único dataset orientado al análisis.

## 6. Modelo de datos

El modelo relacional de Olist distribuye la información de una compra en diferentes tablas relacionadas mediante identificadores únicos.

Las tablas Orders y Order Items constituyen el núcleo del modelo, ya que permiten conectar la información correspondiente a clientes, productos, vendedores, pagos y reseñas.

Esta estructura facilita el análisis desde múltiples perspectivas, aunque requiere un proceso previo de integración y preparación de los datos.

#### Agregar Imagen modelo de datos relacional

## Metodología

El proyecto se desarrolló siguiendo una metodología de análisis exploratorio compuesta por las siguientes etapas:

- Carga de los datasets.
- Comprensión de la estructura de cada tabla.
- Análisis de relaciones entre datasets.
- Evaluación de la calidad de los datos.
- Selección de variables relevantes.
- Integración de las tablas.
- Preparación del dataset analítico.
- Creación de nuevas variables (Feature Engineering).
- Validación del dataset.
- Análisis exploratorio de datos (EDA).
- Obtención de conclusiones.

## 8. Data Preparation
### 8.1 Exploración inicial

Como primer paso se realizó una exploración individual de cada uno de los datasets mediante el análisis de su estructura, dimensiones, tipos de datos y relaciones.

Esta etapa permitió comprender el modelo de datos y definir qué información sería necesaria para responder la hipótesis planteada.

### 8.2 Evaluación de la calidad de los datos

Posteriormente se evaluó la calidad de cada uno de los datasets revisando:

- valores faltantes
- registros duplicados
- tipos de datos
- consistencia de variables categóricas
- distribución de variables numéricas

En términos generales, los datos presentaron un buen nivel de calidad. Los principales inconvenientes detectados estuvieron relacionados con fechas almacenadas como texto y valores faltantes asociados al propio proceso de negocio.

### 8.3 Selección de variables

A partir del análisis inicial se descartaron aquellas variables que no aportaban información relevante para responder la hipótesis del proyecto.

Se conservaron únicamente variables relacionadas con:

- clientes
- pedidos
- pagos
- productos
- vendedores
- reseñas

Esta selección permitió reducir la complejidad del modelo y construir un dataset orientado específicamente al problema de negocio.

### 8.4 Integración del dataset

Debido a que la información se encontraba distribuida en múltiples tablas, fue necesario integrar los distintos datasets utilizando sus claves de relación.

Durante este proceso se detectó que algunas tablas presentaban relaciones uno a muchos respecto de la tabla Orders.

Para evitar la duplicación de registros, las tablas Order Items y Order Payments fueron agregadas previamente a nivel de pedido, obteniendo métricas como:

- cantidad de productos
- cantidad de vendedores
- valor total de la compra
- costo total del envío
- cantidad de pagos
- monto total abonado

De esta forma se garantizó que cada pedido estuviera representado por una única fila dentro del dataset analítico.

### 8.5 Tratamiento de múltiples reseñas

Durante la integración también se identificó que algunos pedidos poseían más de una reseña asociada.

Para mantener una única observación por pedido, las fechas de respuesta fueron convertidas al tipo datetime y posteriormente se conservó únicamente la reseña más reciente para cada orden, utilizando la fecha de respuesta como criterio de selección.

Esta decisión permitió evitar duplicaciones sin perder la información más actual registrada por el cliente.

### 8.6 Transformación de variables

Como parte de la preparación de los datos se realizó la conversión de todas las variables temporales al tipo datetime, facilitando el cálculo de diferencias entre fechas y la generación de nuevas métricas.

Además, se verificó la consistencia cronológica de las fechas correspondientes al proceso de compra, aprobación, envío y entrega.

### 8.7 Feature Engineering

Con el dataset integrado se generaron nuevas variables derivadas orientadas a describir el comportamiento logístico de cada pedido.

Las principales variables creadas fueron:

| Variable                | Descripción                                                |
| ----------------------- | ---------------------------------------------------------- |
| delivery_time_days      | Tiempo total entre la compra y la entrega.                 |
| approval_time_hours     | Tiempo hasta la aprobación del pedido.                     |
| estimated_delivery_days | Tiempo estimado informado al cliente.                      |
| delivery_delay_days     | Diferencia entre la fecha estimada y la entrega real.      |
| late_delivery           | Indicador de pedidos entregados fuera del plazo prometido. |

Estas variables constituyen la base sobre la cual se desarrollará el análisis exploratorio.

### 8.8 Validación del dataset analítico

Finalmente se realizó una revisión del dataset resultante para verificar la consistencia de las nuevas variables creadas.

Durante esta etapa se identificaron algunos valores extremos relacionados con tiempos de entrega y fechas estimadas. Tras analizar estos casos individualmente, se comprobó que mantenían una secuencia cronológica consistente, por lo que fueron considerados valores atípicos válidos y se conservaron para el análisis.

Asimismo, se verificó que el dataset final contuviera una única fila por pedido, garantizando la integridad necesaria para las etapas posteriores.

## 9. Análisis de la relación entre las variables y la satisfacción del cliente

Hasta este punto del proyecto se analizó de forma individual el comportamiento de las principales variables del conjunto de datos, permitiendo comprender su distribución, identificar valores atípicos y detectar posibles patrones generales. Sin embargo, este enfoque descriptivo no resulta suficiente para responder la hipótesis planteada al inicio del análisis.

Una vez construido y validado el dataset analítico, el siguiente paso consiste en estudiar la relación entre la variable objetivo (review_score) y distintas características del proceso de compra. En particular, se analizarán variables relacionadas con la logística, el valor económico de la compra y la complejidad de las órdenes, con el propósito de identificar cuáles presentan una mayor asociación con la satisfacción del cliente.

A lo largo de esta sección se evaluarán tanto medidas descriptivas como representaciones gráficas que permitan comparar el comportamiento de cada variable según las distintas calificaciones otorgadas por los clientes.

### 9.1 Relación entre el tiempo de entrega y la satisfacción del cliente

El tiempo de entrega constituye uno de los principales indicadores de desempeño dentro del comercio electrónico y representa un aspecto fundamental de la experiencia de compra. Una entrega rápida puede generar una percepción positiva del servicio, mientras que tiempos excesivos pueden afectar negativamente la satisfacción del cliente.

En esta sección se analiza la relación entre el tiempo real de entrega (delivery_time_days) y la variable objetivo (review_score), con el objetivo de determinar si existen diferencias significativas entre los distintos niveles de calificación.

##### Conclusión

Los resultados muestran una asociación clara entre el tiempo de entrega y la satisfacción del cliente. En promedio, las órdenes con mejores calificaciones fueron entregadas en menos tiempo, mientras que aquellas con evaluaciones bajas registraron tiempos de entrega considerablemente superiores.

Aunque este análisis no permite establecer una relación causal, la evidencia sugiere que el tiempo de entrega constituye uno de los factores más relevantes asociados con la percepción del servicio.

### 9.2 Relación entre el cumplimiento del plazo de entrega y la satisfacción del cliente

Además del tiempo total de entrega, resulta importante analizar si los pedidos fueron entregados dentro del plazo prometido al cliente. Para ello se creó la variable delay_days, que representa la diferencia entre la fecha estimada y la fecha real de entrega.

El objetivo de este análisis es evaluar si el cumplimiento —o incumplimiento— del plazo informado al cliente presenta una asociación con las calificaciones registradas.

#### Conclusión

Los resultados muestran que, en promedio, la mayoría de los pedidos fueron entregados antes de la fecha estimada. Sin embargo, las órdenes con mejores calificaciones fueron entregadas con un mayor margen de anticipación respecto al plazo prometido.

Asimismo, al analizar únicamente las entregas con retraso, se observa una diferencia significativa entre los distintos niveles de satisfacción. Aproximadamente el 30,6% de las órdenes calificadas con una estrella fueron entregadas fuera del plazo previsto, mientras que este porcentaje desciende hasta 2,54% en las órdenes con cinco estrellas.

Estos resultados evidencian que el cumplimiento de los plazos de entrega constituye uno de los factores más estrechamente asociados con la satisfacción del cliente.

###9.3 Relación entre el valor de la compra y la satisfacción del cliente

Además de los aspectos logísticos, el valor económico de una compra podría influir en las expectativas del cliente y, en consecuencia, en la evaluación final de su experiencia.

En esta sección se analiza la relación entre el valor total de cada pedido (total_price) y la variable objetivo (review_score), con el propósito de identificar posibles diferencias entre los distintos niveles de satisfacción.

#### Conclusión

A diferencia de las variables relacionadas con la logística, el valor económico de la compra no presenta una asociación clara con las calificaciones otorgadas por los clientes.

Aunque las órdenes calificadas con una estrella muestran un importe promedio ligeramente superior, las diferencias observadas entre el resto de las categorías son reducidas y no permiten identificar una tendencia consistente. Esto sugiere que el valor de la compra, por sí solo, no constituye un factor determinante para explicar la satisfacción del cliente.

### 9.4 Relación entre el costo de envío y la satisfacción del cliente

El costo de envío representa otro componente importante dentro del proceso de compra y podría influir en la percepción del cliente sobre el servicio recibido.

En esta sección se analiza la relación entre el costo total de envío (total_freight) y la calificación otorgada por los clientes (review_score) para determinar si esta variable presenta algún grado de asociación con la satisfacción.

#### Conclusión

Los resultados muestran una ligera tendencia a que las órdenes con menores calificaciones presenten costos de envío superiores. Sin embargo, las diferencias observadas son considerablemente menores que las identificadas en las variables relacionadas con la logística.

En consecuencia, el costo de envío parece ejercer una influencia limitada sobre la satisfacción del cliente en comparación con el desempeño del proceso de entrega.

### 9.5 Relación entre la cantidad de productos y la satisfacción del cliente

La cantidad de productos incluidos en una orden puede incrementar la complejidad del proceso logístico y, potencialmente, afectar la experiencia del cliente.

En esta sección se analiza la relación entre la cantidad de productos por pedido (total_items) y la variable objetivo (review_score) con el fin de evaluar si existe alguna diferencia entre las distintas calificaciones.

#### Conclusión

La cantidad de productos por orden no presenta una asociación significativa con las calificaciones otorgadas por los clientes.

Si bien las órdenes con una estrella muestran un número promedio de artículos ligeramente superior, las diferencias entre las distintas categorías son pequeñas y no evidencian un patrón suficientemente consistente como para considerar esta variable un factor relevante en la satisfacción del cliente.

### 9.6 Relación entre la cantidad de pagos y la satisfacción del cliente

Otra característica analizada corresponde a la cantidad de pagos registrados por cada orden. En algunos casos, una compra puede realizarse mediante múltiples transacciones, lo que podría representar un proceso de compra más complejo.

En esta sección se estudia la relación entre la variable payments_count y las calificaciones otorgadas por los clientes.

#### Conclusión

La cantidad de pagos registrados por orden no muestra una asociación significativa con la satisfacción del cliente.

Las diferencias entre los distintos niveles de review_score son prácticamente inexistentes y no permiten identificar un patrón consistente que vincule esta variable con la experiencia de compra.

### 9.7 Resumen de los principales hallazgos

El análisis relacional permitió comparar el comportamiento de distintas variables respecto de la satisfacción del cliente e identificar cuáles presentan una mayor capacidad para explicar las diferencias observadas en las calificaciones.

En conjunto, los resultados muestran que las variables relacionadas con el desempeño logístico presentan asociaciones considerablemente más fuertes que aquellas vinculadas con el valor económico o la complejidad de las órdenes.

En particular, el tiempo de entrega y el cumplimiento del plazo prometido evidencian diferencias claras entre las distintas categorías de review_score, mientras que variables como el valor de la compra, el costo de envío, la cantidad de productos y el número de pagos presentan comportamientos mucho más homogéneos.

| Variable Analizada     | Hallazgo Principal                                                              | Asociación con **review_score** |
| ---------------------- | ------------------------------------------------------------------------------- | ----------------------------- |
| **Delivery Time**      | Menor tiempo de entrega → mejores calificaciones.                               | **Alta**                      |
| **Delivery Delay**     | Cumplir o superar el plazo prometido se asocia con mejores reseñas.             | **Muy alta**                  |
| **Purchase Value**     | No se observó una tendencia consistente.                                        | **Baja**                      |
| **Freight Cost**       | Los costos más altos presentan una ligera asociación con peores calificaciones. | **Baja**                      |
| **Number of Items**    | Las diferencias entre grupos son mínimas.                                       | **Muy baja**                  |
| **Number of Payments** | No se identificó una relación relevante.                                        | **muy baja**           |

## 10. Hallazgos de negocio

El análisis exploratorio permitió identificar distintos factores asociados con la satisfacción del cliente dentro del marketplace de Olist. Sin embargo, más allá de describir el comportamiento de los datos, resulta fundamental interpretar estos resultados desde una perspectiva orientada a la toma de decisiones.

En términos generales, la evidencia obtenida indica que las mayores oportunidades de mejora se encuentran en el desempeño logístico. Variables como el tiempo de entrega y el cumplimiento del plazo prometido presentan una asociación significativamente más fuerte con la satisfacción del cliente que aquellas relacionadas con el valor económico de la compra o con la complejidad de las órdenes.

Estos resultados permiten orientar futuras acciones hacia aquellos procesos con mayor potencial para mejorar la experiencia del cliente y fortalecer la calidad del servicio ofrecido.
