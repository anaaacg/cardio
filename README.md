# Predicción de Enfermedad Cardiovascular mediante Modelos de Clasificación Supervisada

## Descripción del proyecto

Este proyecto tiene como objetivo desarrollar y evaluar modelos de clasificación supervisada para predecir la presencia de enfermedad cardiovascular en pacientes, utilizando variables clínicas, antropométricas y de estilo de vida.

El trabajo se basa en el **Cardiovascular Disease Dataset**, disponible en Kaggle, el cual contiene información de pacientes como edad, género, altura, peso, presión arterial, colesterol, glucosa, tabaquismo, consumo de alcohol, actividad física y la variable objetivo `cardio`.

La variable `cardio` es binaria:

| Valor | Interpretación                        |
| ----- | ------------------------------------- |
| 0     | No presenta enfermedad cardiovascular |
| 1     | Presenta enfermedad cardiovascular    |

El proyecto incluye adquisición de datos, análisis exploratorio, limpieza, feature engineering, entrenamiento de modelos, optimización, validación cruzada y evaluación final.

---

## Objetivo general

Desarrollar y evaluar modelos de clasificación supervisada para predecir la presencia de enfermedad cardiovascular en pacientes, utilizando variables clínicas, antropométricas y de estilo de vida.

---

## Objetivos específicos

* Comprender la estructura del dataset y la naturaleza de sus variables.
* Realizar un análisis exploratorio de datos para identificar distribuciones, patrones, relaciones y anomalías.
* Aplicar técnicas de limpieza y preparación de datos.
* Crear nuevas variables mediante feature engineering.
* Entrenar diferentes modelos de clasificación supervisada.
* Evaluar los modelos mediante métricas como accuracy, precision, recall, F1-score, ROC-AUC y matriz de confusión.
* Comparar los modelos y seleccionar el más adecuado según su rendimiento.
* Analizar la importancia de reducir falsos negativos en un contexto relacionado con salud.

---

## Dataset utilizado

Fuente original:

[Cardiovascular Disease Dataset - Kaggle](https://www.kaggle.com/datasets/sulianova/cardiovascular-disease-dataset)

El dataset original contiene:

* 70.000 registros
* 13 columnas
* Variable objetivo: `cardio`

Después del proceso de limpieza, el dataset final limpio quedó compuesto por:

* 65.307 registros
* Archivo generado: `cardio_clean.csv`

---

## Estructura del proyecto

```text
PROYECTO_FINAL_2/
│
├── Analisis_exploratorio_EDA.ipynb
├── Limpieza.ipynb
├── Feature_engineering.ipynb
├── modelado_supervisado.ipynb
│
├── cardio_train.csv
├── cardio_clean.csv
├── cardio_features_full.csv
├── cardio_features_reduced.csv
├── cardio_features_reduced2.csv
├── cardio_features_reduced3.csv
├── cardio_features_v4.csv

---

## Descripción de archivos principales

| Archivo                           | Descripción                                                                                       |
| --------------------------------- | ------------------------------------------------------------------------------------------------- |
| `cardio_train.csv`                | Dataset original descargado desde Kaggle.                                                         |
| `Analisis_exploratorio_EDA.ipynb` | Notebook con análisis exploratorio, estadísticas descriptivas y visualizaciones iniciales.        |
| `Limpieza.ipynb`                  | Notebook con eliminación de inconsistencias, duplicados y valores fisiológicamente no plausibles. |
| `cardio_clean.csv`                | Dataset limpio resultante del preprocesamiento.                                                   |
| `Feature_engineering.ipynb`       | Notebook con creación de nuevas variables e interacciones.                                        |
| `cardio_features_full.csv`        | Dataset final utilizado para el modelado supervisado.                                             |
| `modelado_supervisado.ipynb`      | Notebook con entrenamiento, comparación, optimización y evaluación de modelos.                    |
| `Rubrica.md`                      | Rúbrica o guía del proyecto.                                                                      |

---

## Proceso realizado

### 1. Adquisición de datos

El archivo `cardio_train.csv` fue descargado manualmente desde Kaggle y cargado en Python mediante la librería `pandas`.

No se utilizaron técnicas de web scraping ni APIs, ya que el dataset estaba disponible directamente en formato CSV.

---

### 2. Análisis Exploratorio de Datos, EDA

Durante el EDA se analizaron:

* Estadísticas descriptivas.
* Distribución de la variable objetivo `cardio`.
* Distribución de variables numéricas como edad, altura, peso y presión arterial.
* Variables categóricas, ordinales y binarias como género, colesterol, glucosa, tabaquismo, alcohol y actividad física.
* Relaciones entre variables clínicas y la presencia de enfermedad cardiovascular.
* Matriz de correlación del dataset original.

El análisis permitió identificar patrones relevantes y detectar inconsistencias en variables como presión arterial, altura y peso.

---

### 3. Limpieza y preprocesamiento

Durante esta etapa se realizaron las siguientes acciones:

* Verificación de valores nulos.
* Eliminación de la columna `id`, por no aportar información predictiva.
* Conversión de `age` de días a años mediante `age_years`.
* Eliminación de duplicados exactos.
* Filtrado de valores fisiológicamente no plausibles.
* Aplicación de rangos válidos para altura, peso, presión arterial e IMC temporal.

Rangos utilizados:

| Variable         | Rango aplicado            |
| ---------------- | ------------------------- |
| `height`         | 130 a 210 cm              |
| `weight`         | 35 a 180 kg               |
| `ap_hi`          | 80 a 220 mmHg             |
| `ap_lo`          | 40 a 130 mmHg             |
| IMC temporal     | 12 a 60                   |
| Presión arterial | `ap_hi` mayor que `ap_lo` |

---

### 4. Feature Engineering

Se crearon nuevas variables para representar mejor factores asociados al riesgo cardiovascular.

Algunas variables generadas fueron:

| Variable                       | Descripción                                      |
| ------------------------------ | ------------------------------------------------ |
| `bmi`                          | Índice de masa corporal.                         |
| `bmi_category`                 | Categoría del IMC.                               |
| `obesity`                      | Indicador de obesidad.                           |
| `bp_category`                  | Categoría de presión arterial.                   |
| `hypertension`                 | Indicador de hipertensión.                       |
| `metabolic_risk`               | Indicador de riesgo metabólico.                  |
| `lifestyle_risk`               | Indicador de riesgo por estilo de vida.          |
| `risk_score`                   | Puntaje general de riesgo cardiovascular.        |
| `pulse_pressure`               | Diferencia entre presión sistólica y diastólica. |
| `mean_arterial_pressure`       | Presión arterial media.                          |
| `age_pressure`                 | Interacción entre edad y presión sistólica.      |
| `cholesterol_gluc_interaction` | Interacción entre colesterol y glucosa.          |
| `age_bmi_interaction`          | Interacción entre edad e IMC.                    |
| `bp_ratio`                     | Relación entre presión sistólica y diastólica.   |

Se probaron distintas versiones del dataset, pero para el modelado final se utilizó `cardio_features_full.csv`, ya que presentó mejores métricas.

---

## Modelos entrenados

Se entrenaron los siguientes modelos de clasificación supervisada:

* Regresión Logística
* Random Forest
* Support Vector Machine, SVM
* K-Nearest Neighbors, KNN
* Naive Bayes
* Árbol de Decisión

El dataset fue dividido en:

* 80% entrenamiento
* 20% prueba

La división se realizó manteniendo la proporción de clases.

---

## Resultados iniciales

| Modelo              | Accuracy | Precision | Recall | F1-score | ROC-AUC |
| ------------------- | -------: | --------: | -----: | -------: | ------: |
| Logistic Regression |   0.7267 |    0.7496 | 0.6919 |   0.7196 |  0.7922 |
| SVM                 |   0.7281 |    0.7617 | 0.6748 |   0.7156 |  0.7858 |
| Naive Bayes         |   0.7079 |    0.7217 | 0.6898 |   0.7054 |  0.7673 |
| Random Forest       |   0.6860 |    0.6912 | 0.6878 |   0.6895 |  0.7366 |
| KNN                 |   0.6859 |    0.6930 | 0.6828 |   0.6879 |  0.7330 |
| Decision Tree       |   0.6152 |    0.6221 | 0.6138 |   0.6179 |  0.6146 |

Aunque SVM obtuvo el mayor accuracy inicial, la Regresión Logística presentó el mejor ROC-AUC y mejor interpretabilidad, por lo que fue seleccionada para la optimización final.

---

## Modelo final

La Regresión Logística fue optimizada mediante `GridSearchCV` con validación cruzada de 5 folds.

Además, se evaluó un ajuste del umbral de clasificación para priorizar el recall, debido a que en un contexto de salud es importante reducir falsos negativos.

| Modelo final                           | Threshold | Accuracy | Precision | Recall | F1-score | ROC-AUC |
| -------------------------------------- | --------: | -------: | --------: | -----: | -------: | ------: |
| Logistic Regression optimizada         |      0.50 |   0.7275 |    0.7508 | 0.6920 |   0.7202 |  0.7921 |
| Logistic Regression priorizando recall |      0.45 |   0.7218 |    0.7116 | 0.7585 |   0.7343 |  0.7921 |

El modelo con umbral 0.45 permitió mejorar el recall, reduciendo falsos negativos, aunque con una ligera disminución del accuracy.

---

## Prueba estadística

Se aplicó una prueba chi-cuadrado para evaluar la asociación entre la categoría de presión arterial `bp_category` y la presencia de enfermedad cardiovascular `cardio`.

Hipótesis:

* H₀: No existe asociación entre la categoría de presión arterial y la presencia de enfermedad cardiovascular.
* H₁: Existe asociación entre la categoría de presión arterial y la presencia de enfermedad cardiovascular.

Resultado:

* Chi-cuadrado: 9162.3938
* Grados de libertad: 3
* Valor p: menor a 0.05

Por tanto, se rechazó la hipótesis nula y se concluyó que existe asociación estadísticamente significativa entre la categoría de presión arterial y la presencia de enfermedad cardiovascular.

---

## Conclusiones

El proyecto permitió comprobar que las variables clínicas, antropométricas y de estilo de vida contienen información útil para identificar patrones asociados con enfermedad cardiovascular.

Los resultados muestran que el modelo tiene una capacidad predictiva aceptable, con un ROC-AUC cercano a 0.79. Sin embargo, no debe considerarse una herramienta de diagnóstico médico, sino una aproximación académica y exploratoria.

La Regresión Logística fue seleccionada como modelo final debido a su equilibrio entre desempeño, interpretabilidad y capacidad de separación entre clases.

---

## Tecnologías utilizadas

* Python
* pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Visual Studio Code
* Jupyter Notebook

---

## Instalación y ejecución

1. Clonar el repositorio:

```bash
git clone <URL_DEL_REPOSITORIO>
```

2. Entrar al proyecto:

```bash
cd PROYECTO_FINAL_2
```

3. Crear un entorno virtual:

```bash
python -m venv venv
```

4. Activar el entorno virtual:

En Windows:

```bash
venv\Scripts\activate
```

En Linux o macOS:

```bash
source venv/bin/activate
```

5. Instalar dependencias:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

6. Ejecutar los notebooks en el siguiente orden:

```text
1. Analisis_exploratorio_EDA.ipynb
2. Limpieza.ipynb
3. Feature_engineering.ipynb
4. modelado_supervisado.ipynb
```

---

## Referencias

* Sulianova. (2019). *Cardiovascular Disease Dataset*. Kaggle.
  https://www.kaggle.com/datasets/sulianova/cardiovascular-disease-dataset

* Centers for Disease Control and Prevention. *Adult BMI Categories*.
  https://www.cdc.gov/bmi/adult-calculator/bmi-categories.html

* National Heart, Lung, and Blood Institute. *Calculate Your BMI*.
  https://www.nhlbi.nih.gov/health/educational/lose_wt/BMI/bmicalc.htm

* American Heart Association. *Understanding Blood Pressure Readings*.
  https://www.heart.org/en/health-topics/high-blood-pressure/understanding-blood-pressure-readings

---

## Nota importante

Este proyecto tiene fines académicos y exploratorios. Los modelos desarrollados no deben ser utilizados como herramienta de diagnóstico médico real.

