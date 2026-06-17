## Introducción y Contexto

El presente proyecto tiene como fin abarcar el sector minero argentino y su inserción en el comercio internacional.

El problema central que aborda este trabajo radica en la dificultad para interpretar de forma integrada la compleja estructura de la matriz minera nacional, donde coexisten minerales metalíferos de alto valor unitario, minerales no metalíferos y rocas de aplicación de gran volumen, y cómo esta diversidad impacta en las proyecciones económicas a mediano plazo.

Tradicionalmente, el análisis de este sector se ha limitado a estadísticas descriptivas lineales que miran el pasado, perdiendo la oportunidad de identificar patrones ocultos de competitividad y simular escenarios futuros.

En el contexto geopolítico actual, la minería, impulsada por la transición energética global y la alta demanda de elementos estratégicos como el litio y el cobre, está adquiriendo un rol crítico para la economía argentina como fuente de divisas. Por lo tanto, se vuelve sumamente relevante diseñar e implementar modelos avanzados de Aprendizaje Automático que permitan clasificar de manera automatizada el perfil comercial de los recursos mineros y predecir con precisión el flujo monetario de las exportaciones bajo diferentes escenarios productivos, optimizando la toma de decisiones estratégicas mediante sistemas predictivos.

---

# Objetivos

## Objetivo General

Desarrollar e implementar un enfoque mixto de aprendizaje automático (no supervisado y supervisado) sobre datasets históricos del comercio minero global para estructurar de manera óptima la matriz de recursos de la Argentina, con el fin de predecir el flujo monetario de las exportaciones para los próximos 2 a 3 años y simular escenarios económicos basados en la variación de parámetros de extracción y precios internacionales.

## Objetivos Específicos

1. Segmentar y caracterizar la matriz minera mediante algoritmos de agrupamiento (_clustering_) para clasificar automáticamente los diferentes minerales y países exportadores en perfiles económicos homogéneos.
    
2. Proyectar el flujo monetario por sectores mediante modelos de regresión para predecir las exportaciones futuras de la Argentina a mediano plazo.
    
3. Desarrollar un simulador de escenarios (_What-If_) que permita modificar parámetros clave y evaluar su impacto sobre el ingreso de divisas.
    
4. Generar un marco de visualización avanzada para representar espacialmente el posicionamiento competitivo de la Argentina en el mercado internacional.
    

---

# Definición del Problema de Aprendizaje Automático

Para abordar el problema planteado de manera integral, el proyecto se divide en dos etapas:

## Etapa de Aprendizaje No Supervisado (Clustering)

No se busca predecir una etiqueta conocida, sino descubrir la estructura oculta de los datos para clasificar minerales industriales, metales y rocas en perfiles comerciales basados en características comunes de mercado.

## Etapa de Aprendizaje Supervisado (Regresión)

Se trata estrictamente de un problema de regresión. La variable objetivo a predecir, el valor FOB de las exportaciones en millones de USD, es una variable continua y numérica a lo largo del tiempo.

---

# Modelos y Métodos a Utilizar

## 1. Preprocesamiento y Reducción de Dimensionalidad

### StandardScaler (Estandarización)

Los datasets combinan variables con escalas masivamente dispares. Este paso permite normalizar la media a cero y el desvío estándar a uno, evitando sesgos en los modelos.

### PCA (Análisis de Componentes Principales)

Se utilizará para reducir la dimensionalidad de los datasets de comercio mundial, remover la multicolinealidad y facilitar la visualización de grupos en gráficos bidimensionales y tridimensionales.

## 2. Modelos de Clustering

### K-Means

Se utilizará para particionar el conjunto de datos en una cantidad de clústeres prefijada, determinada mediante el Método del Codo o el coeficiente de Silhouette.

### DBSCAN

Se considerará como alternativa basada en densidad para identificar agrupaciones de formas arbitrarias y aislar valores atípicos (_outliers_) del mercado internacional.

## 3. Modelos de Regresión

### Random Forest Regressor y Gradient Boosting

Ideales para capturar relaciones no lineales complejas entre el volumen extraído, las fluctuaciones de precios internacionales y el flujo monetario resultante.

### Prophet o ARIMA

Permiten modelar la tendencia histórica de largo plazo y la posible estacionalidad de los flujos comerciales mineros.

---

# Origen de los Datasets

1. Exportaciones minerales mundiales por país.
    
2. Comercio minero mundial por sector y grupo.
    
3. Participación por país exportador en las exportaciones minerales mundiales.
    
4. Exportaciones de minerales de Argentina (SIACAM).
    

---

# Análisis de los Datasets

## Dataset 1: Exportaciones Mineras por País

**Variables:**

- `year`
    
- `pais_exportador`
    
- `value`
    

**Cantidad de registros:** 6535.

**Utilidad:** Permite analizar el volumen histórico manejado por cada país en el mercado mundial.

## Dataset 2: Comercio Mundial por Sector

**Variables:**

- `year`
    
- `sector`
    
- `grupo`
    
- `value`
    

**Cantidad de registros:** 2666.

**Utilidad:** Proporciona el peso económico y la demanda de cada mineral a nivel mundial.

## Dataset 3: Participación por País Exportador

**Variables:**

- `year`
    
- `pais_exportador`
    
- `porcentaje_participacion`
    

**Cantidad de registros:** 6535.

**Utilidad:** Permite analizar el peso relativo de cada país dentro del comercio minero mundial.

## Dataset 4: Exportaciones de Minerales de Argentina (SIACAM)

**Variables:**

- `ANYO`
    
- `MES`
    
- `GRUPO`
    
- `SECTOR`
    
- `FOB`
    

**Utilidad:** Constituye el único dataset con información mensual y desagregada de las exportaciones mineras argentinas.

---

# Consideraciones sobre los Datasets

## Normalización de la Moneda

Los datasets mundiales expresan valores en millones de dólares, mientras que el dataset argentino utiliza dólares corrientes. Por ello, el valor FOB debe transformarse a millones de dólares.

## Normalización Temporal

Los primeros tres datasets están organizados por año, mientras que el dataset argentino posee registros mensuales. Se agruparon los datos por año, sector y grupo.

## Selección del Período de Entrenamiento

Se utilizaron registros comprendidos entre 1995 y 2024 para el entrenamiento de los modelos, reservando los datos de 2025 y 2026 para la validación y simulación.

---

# Etapa de Procesamiento de Datos

Durante esta etapa se realizaron las siguientes tareas:

- Conversión de tipos de datos y tratamiento de valores nulos.
    
- Detección y eliminación de registros duplicados.
    
- Análisis de variables categóricas y valores únicos.
    
- Estandarización y limpieza de variables categóricas.
    
- Estandarización de las variables `Sector` y `Grupo`.
    
- Agrupación por año y sector del dataset SIACAM.
    
- Eliminación del año 2026 y separación del año 2025 para validación.
    

---

# Etapa de Aprendizaje Automático

## Clustering de Minerales – Aprendizaje No Supervisado

Se construyó una matriz de características para el agrupamiento de minerales considerando también la participación de Argentina.

El Método del Codo indicó que la cantidad óptima de clústeres era:

**k = 3**

### Cluster 0

- 84 minerales.
    
- Bajo valor promedio.
    
- Menor volatilidad.
    
- Presencia estable.
    

### Clusters 1 y 2

- Compuestos por 1 y 2 minerales, respectivamente.
    
- Alto valor promedio.
    
- Alta volatilidad.
    
- Importancia estratégica en el mercado mundial.
    

Posteriormente se aplicó DBSCAN, identificando como valores atípicos:

- Cobre
    
- Hierro
    
- Litio
    
- Oro
    
- Plata
    

Finalmente, mediante PCA se observó que Argentina se encuentra agrupada dentro de una escala exportadora relativamente baja, aunque con una tendencia sostenida de crecimiento.

---

## Regresión y Simulador "What-If" – Aprendizaje Supervisado

Se construyeron variables basadas en retrasos temporales (_lags_) y se codificaron las variables categóricas.

Posteriormente se entrenó un modelo de Random Forest Regressor para predecir el valor FOB en función del sector y de los valores históricos.

El modelo obtuvo:

**R² = 0,929**

Este resultado evidencia una capacidad predictiva elevada. La importancia de las variables indica que el valor FOB del año inmediatamente anterior (`fob_lag_1`) es el predictor más influyente.

Como validación, se predijeron los valores correspondientes al año 2025 utilizando información histórica entre 1994 y 2024.

Los resultados presentaron:

- Errores inferiores al 7 % para minerales industriales y rocas de aplicación.
    
- Un error aproximado del 32 % en el sector metalífero.
    

Finalmente, se desarrolló una función capaz de predecir el valor FOB del año 2026 a partir de los dos años anteriores y de variaciones hipotéticas definidas por el usuario.

---

# Conclusiones del Proyecto

La combinación de técnicas de aprendizaje no supervisado y supervisado permitió caracterizar la estructura de la minería argentina y desarrollar modelos predictivos con elevada capacidad explicativa.

Asimismo, la incorporación de un simulador de escenarios proporciona una herramienta de apoyo para la toma de decisiones estratégicas, permitiendo evaluar el impacto potencial de distintos escenarios económicos y productivos sobre el ingreso de divisas provenientes del sector minero argentino.