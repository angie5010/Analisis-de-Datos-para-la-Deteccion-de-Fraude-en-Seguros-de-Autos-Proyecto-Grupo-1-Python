# Proyecto SafeClaim: Perfiles de Riesgo y Detección de Fraude

Este repositorio contiene el análisis exploratorio de datos (EDA) para el proyecto "SafeClaim", enfocado en la detección de fraude en reclamos de seguros de vehículos.

## Integrantes

* Elsie Castro
* Angélica Macías
* Daniel Menoscal
* Emily Rola

---

## 1. Contexto del Proyecto

[cite_start]El fraude en los reclamos de seguros de autos representa un desafío significativo para la industria, generando pérdidas económicas debido a la dificultad en su detección y verificación[cite: 8].

El objetivo de este análisis es:
* [cite_start]**Segmentar el Riesgo:** Distinguir distintos perfiles de clientes (por edad, zona, historial, etc.) para determinar estrategias de prevención[cite: 13].
* [cite_start]**Identificar Patrones de Fraude:** Analizar variables como el tipo de vehículo y el deducible para encontrar factores asociados al fraude[cite: 16].

---

## 2. Metodología y Preparación de Datos

[cite_start]El análisis se realizó utilizando un dataset de **15,420 registros y 34 columnas**[cite: 54], empleando librerías como Pandas, Matplotlib y Seaborn.

### Calidad de Datos

Se identificaron dos problemas principales en el dataset:

* [cite_start]**Valores Nulos:** Se encontraron 323 valores faltantes en `AccidentArea` y 215 en `MaritalStatus`[cite: 66, 69].
* **Desbalance de Datos:** La variable objetivo `FraudFound_P` está altamente desbalanceada. [cite_start]Solo un **6%** de los reclamos (923 casos) fueron identificados como fraude [cite: 185][cite_start], mientras que la gran mayoría (14,497 casos) son legítimos[cite: 26].

### Limpieza e Imputación

Para conservar la integridad del dataset y no eliminar registros, se decidió imputar los valores nulos utilizando la **moda** (el valor más frecuente) de cada columna:

* [cite_start]**AccidentArea:** Los valores nulos se reemplazaron por "Urban"[cite: 88].
* [cite_start]**MaritalStatus:** Los valores nulos se reemplazaron por "Married"[cite: 88].

[cite_start]Las gráficas comparativas (antes y después) confirman que esta imputación no alteró significativamente la distribución original de los datos[cite: 124].

### Variables Seleccionadas

El análisis se centró en las siguientes variables clave:
[cite_start]`age`, `sex`, `brand`, `PolicyType`, `MaritalStatus`, `PastNumberOfClaims` y `FraudFound_P` [cite: 35-37].

---

## 3. Hallazgos Principales del Análisis

### Perfil Demográfico y de Contexto
* [cite_start]**Sexo:** Existe una presencia mucho mayor de asegurados hombres que de mujeres[cite: 243].
* [cite_start]**Edad:** La mayor densidad de asegurados se encuentra en el rango de 30 a 50 años[cite: 241].
* [cite_start]**Área del Accidente:** La gran mayoría de los accidentes ocurren en zonas urbanas, lo cual es esperado debido a la alta densidad de tráfico[cite: 187].

### Análisis de Riesgo y Fraude

#### Hallazgo 1: La Edad no es un factor determinante en el Riesgo

A pesar de la creencia común, el análisis del boxplot muestra que la edad, por sí sola, **no presenta una diferencia significativa** entre los grupos de alto y bajo riesgo. [cite_start]Las distribuciones de edad en ambos grupos son casi idénticas[cite: 251, 252].

![Gráfico de Edad vs Riesgo](https://i.imgur.com/0VHOcdA.png)

#### Hallazgo 2: La Categoría del Vehículo es clave en el Fraude

[cite_start]Se creó un segmento de "Alto Riesgo" si el cliente cumplía al menos uno de estos criterios [cite: 265-271]:
* Tener más de 2 reclamos previos.
* Ser menor de 25 años.
* Tener un `DriverRating` (calificación de conductor) menor o igual a 2.

[cite_start]Al cruzar la variable objetivo de fraude (`FraudFound_P`) con la categoría del vehículo, se observa que los vehículos tipo **"Sedan"** no solo son los más comunes, sino que también son la categoría donde se comete más fraude en términos absolutos[cite: 348].

![Gráfico de Fraude por Vehículo](https://i.imgur.com/FQisUXv.png)

#### Otros Hallazgos
* [cite_start]**Riesgo por Tipo de Póliza:** Las pólizas tipo "Sedan" (Collision, Liability y All Perils) concentran la mayor cantidad de asegurados clasificados como de alto riesgo[cite: 295].
* **Fraude por Deducible:** La mayor frecuencia de fraude se observa en el deducible de **400**. [cite_start]Sin embargo, esto se debe a que es el valor más común en el dataset, no a que ese monto específico incentive el fraude[cite: 328, 329].

---

## 4. Conclusiones

* [cite_start]El perfil de alto riesgo se concentra principalmente en **conductores jóvenes** y aquellos con **múltiples reclamos previos**[cite: 362].
* [cite_start]Los vehículos tipo **Sedán** presentan la mayor concentración de alto riesgo y la mayor cantidad de casos de fraude[cite: 363].
* [cite_start]La mayoría de los accidentes ocurren en **zonas urbanas**[cite: 365].
* [cite_start]**No se encontró una relación clara** entre el monto del deducible y la probabilidad de fraude[cite: 364].

---

## 5. Recomendaciones

Basado en los hallazgos, se recomienda:

* [cite_start]**Enfocar controles y auditorías** en los perfiles de mayor riesgo: clientes jóvenes y propietarios de vehículos Sedán[cite: 367].
* [cite_start]**Ajustar las primas** y las políticas de suscripción basándose en el nivel de riesgo segmentado (historial de reclamos, tipo de auto)[cite: 368].
* [cite_start]**Fortalecer la prevención** de accidentes y la vigilancia de reclamos en **zonas urbanas**[cite: 370].
* [cite_start]**Revisar los procesos de auditoría** para los **deducibles más comunes (400)**, ya que es donde se acumula el mayor volumen de fraude[cite: 369].
