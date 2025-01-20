# Clasificación de Imágenes de Infraestructura con Redes Convolucionales

Este proyecto implementa una red neuronal convolucional (CNN) para clasificar imágenes de estructuras de infraestructura (decks, pavements, y walls) en dos categorías: cracked (con fisuras) y non-cracked (sin fisuras). El objetivo es identificar el estado de diferentes superficies para aplicaciones de mantenimiento y evaluación estructural.

---

## Estructura del Proyecto

El proyecto tiene la siguiente estructura:

```
archive/                 # Directorio con las carpetas de datos (imágenes organizadas por clase)
scripts/
  train.py              # Script principal para entrenar y validar el modelo
  test.py               # Script para evaluar el modelo en el conjunto de prueba
models/                 # Carpeta para guardar los pesos del modelo
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

El entrenamiento del modelo puede realizarse ejecutando el script `train.py`. Este script incluye la configuración de early stopping y guarda los mejores pesos del modelo basado en la pérdida de validación.

### Comando para entrenar:

```bash
python scripts/train.py
```

Los pesos del mejor modelo se guardan en `models/best_model.pth`.

---

## Evaluación

El script `test.py` permite evaluar el modelo entrenado en el conjunto de prueba. Calcula las siguientes métricas:

- Pérdida de prueba
- Precisión
- F1-Score
- Matriz de confusión

### Comando para evaluar:

```bash
python scripts/test.py
```

---

## Configuración del Modelo

El modelo es una red convolucional definida en PyTorch. Los principales hiperparámetros incluyen:

- **Dropout**: 0.2 (configurable)
- **Tasa de aprendizaje**: 0.001
- **Peso de regularización**: 0.0001
- **Batch size**: 64
- **Número de épocas**: 10

Puedes ajustar los hiperparámetros modificando el diccionario `params` dentro de los scripts.

---

## Visualización de Resultados

El script genera:

1. Métricas de rendimiento por época:
   - Pérdida de entrenamiento y validación
   - Precisión y F1-Score

2. Matriz de confusión para interpretar los resultados del conjunto de prueba.

---

## Contribución

Si deseas contribuir a este proyecto, puedes:

1. Hacer un fork del repositorio.
2. Crear una rama para tus cambios:
   ```bash
   git checkout -b feature/nueva-caracteristica
   ```
3. Realizar un pull request con una descripción detallada de tus cambios.

---

## Licencia

Este proyecto está bajo la licencia MIT. Consulta el archivo `LICENSE` para más detalles.

---

## Autor

Este proyecto fue desarrollado como parte de un sistema de clasificación automática para la detección de fisuras en infraestructura. Si tienes dudas, no dudes en contactarme.

