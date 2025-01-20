# Clasificación de imágenes de infraestructura con redes neuronales

Este repositorio contiene implementaciones de dos modelos para la clasificación de imágenes de infraestructura (decks, pavements y walls) en dos categorías: cracked (con fisuras) y non-cracked (sin fisuras). Los modelos incluidos son:

1. **Red Neuronal Convolucional Personalizada (ConvNet)**.
2. **Modelo Preentrenado ResNet18 para Transfer Learning**.

El objetivo principal es identificar el estado de diferentes superficies para aplicaciones de mantenimiento y evaluación estructural.

---

## Estructura del Proyecto

El proyecto tiene la siguiente estructura:

```
archive/                 # Directorio con las carpetas de datos (imágenes organizadas por clase)
scripts/
  train_convnet.py      # Script para entrenar el modelo ConvNet personalizado
  train_resnet18.py     # Script para entrenar el modelo ResNet18 preentrenado
  test.py               # Script para evaluar ambos modelos en el conjunto de prueba
models/                 # Carpeta para guardar los pesos de los modelos
README.md               # Documentación del proyecto
requirements.txt        # Dependencias necesarias
```

---

## Requisitos

### Dependencias

Asegúrate de tener Python 3.8+ instalado. Las dependencias necesarias están listadas en el archivo `requirements.txt`. Puedes instalarlas ejecutando:

```bash
pip install -r requirements.txt
```

### Estructura de Datos

El directorio `archive` debe contener las siguientes carpetas con imágenes organizadas por clase:

```
archive/
├── decks/
│   ├── cracked/
│   └── non-cracked/
├── pavements/
│   ├── cracked/
│   └── non-cracked/
└── walls/
    ├── cracked/
    └── non-cracked/
```

Cada carpeta contiene las imágenes correspondientes a su clase.

---

## Entrenamiento

### ConvNet Personalizado

Este modelo implementa una arquitectura convolucional personalizada con las siguientes características:
- Dos capas convolucionales con batch normalization y max pooling.
- Una capa fully connected con dropout para evitar sobreajuste.

#### Comando para entrenar:

```bash
python scripts/train_convnet.py
```

Los pesos del mejor modelo se guardan en `models/best_model_convnet.pth`.

### ResNet18 Preentrenado

Se utiliza ResNet18 preentrenado en ImageNet y se ajusta la capa fully connected para clasificar las 6 clases del dataset.

#### Comando para entrenar:

```bash
python scripts/train_resnet18.py
```

Los pesos del mejor modelo se guardan en `models/best_model_resnet18.pth`.

---

## Evaluación

El script `test.py` permite evaluar ambos modelos en el conjunto de prueba. Calcula las siguientes métricas:

- Pérdida de prueba.
- Precisión.
- F1-Score.
- Matriz de confusión.

#### Comando para evaluar:

```bash
python scripts/test.py
```

---

## Configuración de los Modelos

### ConvNet Personalizado

El modelo es una red convolucional definida en PyTorch con los siguientes hiperparámetros:

- **Dropout**: 0.2 (configurable).
- **Tasa de aprendizaje**: 0.001.
- **Peso de regularización**: 0.0001.
- **Batch size**: 64.
- **Número de épocas**: 10.

Puedes ajustar los hiperparámetros modificando el diccionario `params` dentro del script `train_convnet.py`.

### ResNet18 Preentrenado

El modelo ResNet18 utiliza los pesos preentrenados de ImageNet y ajusta su capa fully connected para adaptarse a 6 clases. Los hiperparámetros son similares a los del modelo ConvNet y pueden configurarse en el script `train_resnet18.py`.

---

## Visualización de Resultados

Ambos modelos generan:

1. Métricas de rendimiento por época:
   - Pérdida de entrenamiento y validación.
   - Precisión y F1-Score.

2. Matriz de confusión para interpretar los resultados del conjunto de prueba.
