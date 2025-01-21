# Clasificación de imágenes de infraestructura con redes neuronales

Este repositorio contiene implementaciones de dos modelos para la clasificación de imágenes de infraestructura (decks, pavements y walls) en dos categorías: cracked (con fisuras) y non-cracked (sin fisuras). Los modelos incluidos son:

1. **Red Neuronal Convolucional Personalizada (ConvNet)**.
2. **Modelo Preentrenado EfficientNet-B0 para Transfer Learning**.

El objetivo principal es identificar el estado de diferentes superficies para aplicaciones de mantenimiento y evaluación estructural.

---

## Estructura del Proyecto

El proyecto tiene la siguiente estructura:

```
archive/                 # Directorio con las carpetas de datos (imágenes organizadas por clase)
scripts/
  train_convnet.py      # Script para entrenar el modelo ConvNet personalizado
  train_efficientnet.py # Script para entrenar el modelo EfficientNet-B0 preentrenado
  test.py               # Script para evaluar ambos modelos en el conjunto de prueba
models/                 # Carpeta para guardar los pesos de los modelos
README.md               # Documentación del proyecto
requirements.txt        # Dependencias necesarias
```

---

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
- Dos capas convolucionales con Batch Normalization y Max Pooling.
- Una capa fully connected con Dropout para evitar sobreajuste.

#### Comando para entrenar:

```bash
python scripts/train_convnet.py
```

Los pesos del mejor modelo se guardan en `models/best_model_convnet.pth`.

### EfficientNet-B0 Preentrenado

Se utiliza EfficientNet-B0 preentrenado en ImageNet y se ajusta la capa classifier para clasificar las 6 clases del dataset. Además, las capas convolucionales iniciales se congelan para aprovechar los pesos preentrenados.

#### Comando para entrenar:

```bash
python scripts/train_efficientnet.py
```

Los pesos del mejor modelo se guardan en `models/best_model_efficientnet.pth`.

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

### EfficientNet-B0 Preentrenado

El modelo EfficientNet-B0 utiliza los pesos preentrenados de ImageNet y ajusta su capa classifier para adaptarse a las 6 clases. Los hiperparámetros son:

- **Tasa de aprendizaje**: 0.001.
- **Peso de regularización**: 0.0001.
- **Batch size**: 64.
- **Número de épocas**: 10.

Estos parámetros pueden configurarse en el script `train_efficientnet.py`.

---

## Visualización de Resultados

Ambos modelos generan:

1. Métricas de rendimiento por época:
   - Pérdida de entrenamiento y validación.
   - Precisión y F1-Score.

2. Matriz de confusión para interpretar los resultados del conjunto de prueba.
