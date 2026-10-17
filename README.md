# Pre-entrega-9
Construccion de un Pipeline de Preprocesamiento Robusto

Pipeline de Preprocesamiento y Clasificación con el Dataset Iris

Este proyecto implementa un flujo de trabajo de Machine Learning robusto y reproducible utilizando Scikit-Learn. A partir de una versión modificada del dataset Iris (a la cual se le introdujeron valores nulos y variables categóricas de forma artificial), se diseñó un ColumnTransformer integrado en un Pipeline final para la limpieza de datos, el entrenamiento de un modelo de Regresión Logística y su posterior persistencia.

🛠️ Arquitectura del Pipeline

El flujo de datos está automatizado y encapsulado para evitar el Data Leakage (fuga de datos) durante las fases de entrenamiento y validación.

1. Preprocesamiento por Tipo de Columna (ColumnTransformer)

• Variables Numéricas:
	• Imputación: Relleno de valores faltantes (NaN) mediante la mediana de cada columna (SimpleImputer).
	• Escalado: Transformación de características utilizando StandardScaler (media 0 y varianza 1).
• Variables Categóricas:
	• Imputación: Relleno de valores faltantes mediante la estrategia del valor más frecuente (moda).
	• Codificación: Conversión de texto a variables binarias mediante OneHotEncoder (configurado para ignorar categorías desconocidas en producción).

2. Modelo Estimador

• Se integró una Regresión Logística (LogisticRegression) como clasificador final para predecir las tres especies de la flor Iris (setosa, versicolor, virginica).

📊 Validación y Métricas

El dataset se dividió utilizando una partición estándar de 80% para entrenamiento y 20% para prueba (train_test_split).
El modelo alcanza un alto rendimiento en el conjunto de test. Las métricas evaluadas de forma automatizada por el script son:
• Exactitud Global (Accuracy): Mide el porcentaje total de aciertos.
• Precisión, Sensibilidad (Recall) y F1-Score: Desglosadas por cada una de las tres clases de flores para garantizar un análisis de error balanceado.

💾 Persistencia del Modelo (Despliegue)

Para permitir el uso del modelo en entornos de producción sin necesidad de volver a entrenarlo, se incluyó un módulo de persistencia con la librería joblib:
• Exportación: El pipeline completo (que guarda internamente los criterios de imputación, las medias de escalado y los pesos del modelo) se exporta al archivo pipeline_iris_logistica.joblib.
• Importación y Uso: Se incluye un bloque de código que demuestra cómo cargar el archivo .joblib para procesar y predecir instantáneamente nuevas muestras de datos (incluso si contienen valores nulos).
