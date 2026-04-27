# 💧 Water Quality India — Spark + Keras
### Predicción del Índice de Calidad del Agua (WQI) de la India mediante Redes Neuronales

**Autor:** Santiago Beltrán López  
**Materia:** Procesamiento de Datos  
---

## 📌 Descripción

Este proyecto implementa un flujo completo de procesamiento y análisis de datos de calidad del agua en estados de la India. Se utiliza **Apache PySpark** para el procesamiento distribuido y **Keras (TensorFlow)** para entrenar un modelo de red neuronal que predice el **Water Quality Index (WQI)**.

El cuaderno cubre desde la ingesta del dataset hasta la visualización geoespacial y la evaluación del modelo predictivo.

---

## 🗂️ Estructura del Repositorio

```
water-quality-india-spark-keras/
│
├── Clean_ML_Water_Beltran.ipynb   # Cuaderno principal con todo el flujo
├── Indian_States.shp              # Shapefile para visualización geoespacial
├── Indian_States.shx              # Archivo índice del shapefile
├── Indian_States.dbf              # Atributos del shapefile
├── README.md                      # Este archivo
└── data/
    └── water_quality_india.csv    # Dataset original
```

---

## 🔧 Tecnologías Utilizadas

| Herramienta | Versión | Uso |
|---|---|---|
| Python | 3.9+ | Lenguaje base |
| Apache PySpark | 3.x | Procesamiento distribuido |
| Keras / TensorFlow | 2.x | Modelo de red neuronal |
| GeoPandas | 0.x | Visualización geoespacial |
| Matplotlib / PyLab | — | Gráficas y visualización |
| Pandas | — | Manipulación de datos |
| Scikit-learn | — | Métricas de evaluación |
| Findspark | — | Integración Spark–Jupyter |

---

## 📊 Flujo del Proyecto

```
1. Inicialización de SparkSession
        ↓
2. Carga del dataset (CSV) desde HDFS/local
        ↓
3. Limpieza de datos (nulos, tipos, columnas)
        ↓
4. Cálculo de rangos de calidad por parámetro
   (qrPH, qrDO, qrCOND, qrBOD, qrNN, qrFecal)
        ↓
5. Cálculo del WQI ponderado
        ↓
6. Categorización de calidad del agua
        ↓
7. Visualización (gráficas + mapa geoespacial)
        ↓
8. Entrenamiento del modelo Keras (Red Neuronal)
        ↓
9. Evaluación y métricas (MSE, RMSE, MAE, R²)
```

---

## 🧠 Modelo de Red Neuronal

El modelo implementado es una red neuronal secuencial construida con Keras:

- **Entrada:** 6 features (qrPH, qrDO, qrCOND, qrBOD, qrNN, qrFecal)
- **Capas ocultas:** 3 capas densas de 350 neuronas con activación **ReLU**
- **Salida:** 1 neurona lineal (regresión del WQI)
- **Optimizador:** Adam (lr = 0.001)
- **Función de pérdida:** Mean Squared Error (MSE)
- **Épocas:** 200 | **Batch size:** 81

---

## 📈 Resultados del Modelo

| Métrica | Entrenamiento | Prueba |
|---------|:---:|:---:|
| MSE | 0.0007 | 0.0082 |
| RMSE | 0.0255 | 0.0905 |
| MAE | 0.0166 | 0.0415 |
| R² | 1.0000 | 1.0000 |

El modelo obtuvo un **R² = 1.0** tanto en entrenamiento como en prueba, explicando el 100% de la varianza del WQI. El error bajo se debe a que las variables de entrada son rangos de calidad derivados de los mismos parámetros fisicoquímicos que componen el WQI, lo que hace que la red aprenda con alta precisión la función de ponderación.

---

## 🗺️ Parámetros del WQI

El Índice de Calidad del Agua (WQI) se calcula con la siguiente ponderación:

| Parámetro | Peso |
|---|:---:|
| pH | 0.165 |
| Oxígeno Disuelto (DO) | 0.281 |
| Conductividad (COND) | 0.234 |
| Demanda Bioquímica de O₂ (BOD) | 0.009 |
| Nitratos/Nitrógeno (NN) | 0.028 |
| Coliformes Fecales (FC) | 0.281 |

### Categorías de Calidad

| Rango WQI | Categoría |
|---|---|
| < 25 | Excelente (Agua Potable) |
| 25 – 50 | Buena |
| 50 – 75 | Media |
| 75 – 100 | Mala |
| > 100 | Muy Mala |

---

## ⚙️ Instalación y Ejecución

### Requisitos previos
- Java 8+ instalado (necesario para Spark)
- Python 3.9+
- Jupyter Notebook o JupyterLab

### Instalación de dependencias

```bash
pip install findspark pyspark tensorflow keras geopandas matplotlib pandas scikit-learn
```

### Ejecución

1. Clona el repositorio:
```bash
git clone https://github.com/SBL/water-quality-india-spark-keras.git
cd water-quality-india-spark-keras
```

2. Abre el cuaderno:
```bash
jupyter notebook Clean_ML_Water_Beltran.ipynb
```

3. Ejecuta todas las celdas en orden: `Kernel → Restart & Run All`

---

## 📚 Referencias

- Tyagi, S., Sharma, B., Singh, P., & Dobhal, R. (2013). *Water Quality Assessment in Terms of Water Quality Index*. American Journal of Water Resources, 1(3), 34–38.
- Chollet, F. (2021). *Deep Learning with Python* (2nd ed.). Manning Publications.
- Apache Spark Documentation. https://spark.apache.org/docs/latest/
- GeoPandas Documentation. https://geopandas.org/en/stable/
- Zaharia, M., et al. (2016). *Apache Spark: A unified engine for big data processing*. Communications of the ACM, 59(11), 56–65.

---

*Proyecto académico — Procesamiento de Datos · 2026*
