# Proyecto SafeClaim: Perfiles de Riesgo y Detección de Fraude

Este repositorio contiene el análisis exploratorio de datos (EDA) para el proyecto "SafeClaim", enfocado en la detección de fraude en reclamos de seguros de vehículos.

## Integrantes

* Elsie Castro  
* Angélica Macías  
* Daniel Menoscal  
* Emily Rola  

---

## 1. Contexto del Proyecto

El fraude en los reclamos de seguros de autos representa un desafío significativo para la industria, generando pérdidas económicas debido a la dificultad en su detección y verificación [8].

El objetivo de este análisis es:

* **Segmentar el Riesgo:** Distinguir distintos perfiles de clientes (por edad, zona, historial, etc.) para determinar estrategias de prevención [13].
* **Identificar Patrones de Fraude:** Analizar variables como el tipo de vehículo y el deducible para encontrar factores asociados al fraude [16].

---

## 2. Metodología y Preparación de Datos

El análisis se realizó utilizando un dataset de **15,420 registros y 34 columnas** [54], empleando librerías como Pandas, Matplotlib y Seaborn.

### Calidad de Datos

Se identificaron dos problemas principales en el dataset:

* **Valores Nulos:** Se encontraron 323 valores faltantes en `AccidentArea` y 215 en `MaritalStatus` [66, 69].
* **Desbalance de Datos:** La variable objetivo `FraudFound_P` está altamente desbalanceada. Solo un **6%** de los reclamos (923 casos) fueron identificados como fraude [185], mientras que la gran mayoría (14,497 casos) son legítimos [26].

### Limpieza e Imputación

Para conservar la integridad del dataset y no eliminar registros, se decidió imputar los valores nulos utilizando la **moda** (el valor más frecuente) de cada columna:

* **AccidentArea:** Los valores nulos se reemplazaron por "Urban" [88].
* **MaritalStatus:** Los valores nulos se reemplazaron por "Married" [88].

Las gráficas comparativas (antes y después) confirman que esta imputación no alteró significativamente la distribución original de los datos [124].

### Variables Seleccionadas

El análisis se centró en las siguientes variables clave:  
`age`, `sex`, `brand`, `PolicyType`, `MaritalStatus`, `PastNumberOfClaims` y `FraudFound_P` [35-37].

---

## 3. Hallazgos Principales del Análisis

### Perfil Demográfico y de Contexto

* **Sexo:** Existe una presencia mucho mayor de asegurados hombres que de mujeres [243].  
* **Edad:** La mayor densidad de asegurados se encuentra en el rango de 30 a 50 años [241].  
* **Área del Accidente:** La gran mayoría de los accidentes ocurren en zonas urbanas [187].  

### Análisis de Riesgo y Fraude

#### Hallazgo 1: La Edad no es un factor determinante en el Riesgo

A pesar de la creencia común, el análisis del boxplot muestra que la edad, por sí sola, **no presenta una diferencia significativa** entre los grupos de alto y bajo riesgo.  
Las distribuciones de edad en ambos grupos son casi idénticas [251, 252].

![Gráfico de Edad vs Riesgo](https://i.imgur.com/0VHOcdA.png)

#### Hallazgo 2: La Categoría del Vehículo es clave en el Fraude

Se creó un segmento de "Alto Riesgo" si el cliente cumplía al menos uno de estos criterios [265–271]:

* Tener más de 2 reclamos previos.  
* Ser menor de 25 años.  
* Tener un `DriverRating` menor o igual a 2.  

Al cruzar la variable objetivo de fraude (`FraudFound_P`) con la categoría del vehículo, se observa que los vehículos tipo **Sedan** no solo son los más comunes, sino que también concentran más casos de fraude en términos absolutos [348].

![Gráfico de Fraude por Vehículo](https://i.imgur.com/FQisUXv.png)

#### Otros Hallazgos

* **Riesgo por Tipo de Póliza:** Las pólizas tipo "Sedan" (Collision, Liability y All Perils) concentran la mayor cantidad de asegurados clasificados como de alto riesgo [295].
* **Fraude por Deducible:** La mayor frecuencia de fraude se observa en el deducible de **400**, debido a que es el valor más común en el dataset [328, 329].

---

## 4. Conclusiones

* El perfil de alto riesgo se concentra principalmente en **conductores jóvenes** y aquellos con **múltiples reclamos previos** [362].
* Los vehículos tipo **Sedán** presentan la mayor concentración de alto riesgo y la mayor cantidad de casos de fraude [363].  
* La mayoría de los accidentes ocurren en **zonas urbanas** [365].  
* No se encontró una relación clara entre el monto del deducible y la probabilidad de fraude [364].  

---

## 5. Recomendaciones

Basado en los hallazgos, se recomienda:

* **Enfocar controles y auditorías** en clientes jóvenes y propietarios de vehículos Sedán [367].  
* **Ajustar las primas** y políticas de suscripción basándose en el nivel de riesgo segmentado [368].  
* **Fortalecer la prevención** y monitoreo en **zonas urbanas** [370].  
* **Revisar los procesos de auditoría** para los deducibles más comunes (400) [369].  
