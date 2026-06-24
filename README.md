# Proyecto MLOps - Clasificación de Apertura de Notificaciones
## Objetivo
Desarrollar un pipeline de Machine Learning para predecir si un usuario abrirá una notificación push utilizando técnicas de clasificación supervisada.

## Tecnologías utilizadas
```text
Python 3.12
Poetry
Pandas
NumPy
Scikit-Learn
MLflow
DVC
```
## Estructura del proyecto
```text
MLOPS/
│
├── .dvc/
├── .dvcignore
│
├── data/
│   ├── raw/
│   │   ├── open_rate_dataset.csv
│   │   └── open_rate_dataset.csv.dvc
│   │
│   └── Contruir_DataSet.py
│
├── mlruns/
│
├── dvc.yaml
├── dvc.lock
│
├── data_preparation.py
├── train_models.py
│
├── pyproject.toml
├── poetry.lock
├── README.md
└── TEAM.md
```

## Instalación
### Clonar el repositorio:
git clone https://github.com/jjgomezreyes/MLOPS.git MLOPS
cd MLOPS

### Instalar dependencias:
poetry install

### Generación del dataset
poetry run python data_preparation.py

### El archivo generado quedará en:
data/raw/open_rate_dataset.csv

### Entrenamiento de modelos
poetry run python train_models.py

## Durante la ejecución se entrenan dos modelos:
Logistic Regression
Random Forest

## Seguimiento de experimentos con MLflow
### Iniciar MLflow:
poetry run mlflow ui

Abrir en navegador:
http://127.0.0.1:5000

### Desde la interfaz es posible:
Visualizar ejecuciones.
Comparar métricas.
Analizar parámetros.
Consultar artefactos generados.

## Modelo seleccionado
Se evaluaron dos algoritmos de clasificación:
- Logistic Regression
- Random Forest

```text
===== RESULTADOS =====
LogisticRegression
accuracy: 0.6150
precision: 0.5882
f1: 0.6091

RandomForest
accuracy: 0.6350
precision: 0.6038
recall: 0.6737
f1: 0.6368

MEJOR MODELO: RandomForest
F1 = 0.6368
======================
```

Los experimentos fueron registrados en MLflow para facilitar la comparación de métricas.

El modelo Random Forest obtuvo los mejores resultados en Accuracy, Precision, Recall y F1-Score, superando consistentemente a Logistic Regression. F1-Score es la métrica utilizada como criterio principal de selección.

Por esta razón se seleccionó Random Forest como modelo final para el problema de predicción de apertura de notificaciones, ya que ofrece una mayor capacidad predictiva y mejor equilibrio entre falsos positivos y falsos negativos.

## Versionamiento de datos con DVC
El dataset utilizado para el entrenamiento es gestionado mediante DVC (Data Version Control), permitiendo reproducibilidad y control de versiones de los datos.

### Generar dataset
```bash
poetry run python data/Contruir_DataSet.py
```

### Registrar dataset en DVC
```bash
poetry run dvc add data/raw/open_rate_dataset.csv
```

### Verificar estado
```bash
poetry run dvc status
```

### Recuperar dataset
```bash
poetry run dvc pull
```

El archivo:
```text
data/raw/open_rate_dataset.csv.dvc
```

almacena los metadatos necesarios para reproducir la versión exacta del dataset utilizada en los experimentos.

## Reproducibilidad del proyecto
### 1. Clonar repositorio
```bash
git clone https://github.com/jjgomezreyes/MLOPS.git
cd MLOPS
```

### 2. Instalar dependencias
```bash
poetry install
```

### 3. Recuperar o generar datos
```bash
poetry run dvc pull
```

o regenerar:
```bash
poetry run dvc repro
```

### 4. Entrenar modelos
```bash
poetry run python train_models.py
```

### 5. Visualizar experimentos
```bash
poetry run mlflow ui
```

Abrir:
```text
http://127.0.0.1:5000
```
