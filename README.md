# NLP Training Starter

Framework modular y configurable para entrenar modelos de NLP con PyTorch Lightning y Hydra, diseñado como base para desarrollar diversos proyectos de procesamiento de lenguaje natural.

## Descripción

Este proyecto proporciona una estructura base sólida para entrenar modelos de procesamiento de lenguaje natural (NLP) utilizando PyTorch Lightning y Transformers. Está diseñado para servir como punto de partida para desarrollar diversos proyectos de NLP, permitiéndote enfocarte en tu caso de uso específico sin tener que configurar toda la infraestructura de entrenamiento desde cero.

## Características

- Arquitectura modular y extensible
- Integración completa con modelos de HuggingFace Transformers
- Sistema de configuración flexible mediante Hydra
- Logging y seguimiento de experimentos con TensorBoard
- Dockerizado para facilitar portabilidad y reproducibilidad
- Estructura preparada para fine-tuning de modelos preentrenados
- Scripts para entrenamiento y predicción listos para usar

## Requisitos

- Python 3.8+
- PyTorch 2.0+
- Docker (opcional)

## Instalación

### Opción 1: Instalación local

```bash
# Clonar el repositorio
git clone <url-del-repositorio>
cd nlp-training-starter

# Crear entorno virtual
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate

# Instalar dependencias
pip install -r requirements.txt
```

### Opción 2: Usando Docker

```bash
# Clonar el repositorio
git clone <url-del-repositorio>
cd nlp-training-starter

# Ejecutar con docker-compose
docker-compose up
```

## Estructura del Proyecto

```
.
├── conf/                       # Configuraciones con Hydra
│   ├── config.yaml             # Configuración principal
│   ├── model/                  # Configuraciones de modelos
│   └── training/               # Configuraciones de entrenamiento
├── data/                       # Datos de entrenamiento
│   └── *.csv                   # Datasets (reemplazar con tus datos)
├── src/                        # Código fuente
│   ├── model.py                # Definición del modelo
│   ├── predict.py              # Script para predicción
│   └── train.py                # Script para entrenamiento
├── outputs/                    # Modelos guardados (generado al entrenar)
├── logs/                       # Logs de entrenamiento (generado al entrenar)
├── docker-compose.yml          # Configuración de Docker
├── requirements.txt            # Dependencias del proyecto
└── README.md                   # Este archivo
```

## Comenzando un Nuevo Proyecto

Para utilizar este framework como base para tu proyecto de NLP:

1. **Adaptar el modelo**: Modifica `src/model.py` para implementar la arquitectura específica para tu tarea de NLP (clasificación, NER, generación de texto, etc.).

2. **Preparar tus datos**: Coloca tus datasets en el directorio `data/` y ajusta el formato según sea necesario.

3. **Configuración**: Edita los archivos en `conf/` para especificar parámetros del modelo y entrenamiento adecuados para tu caso de uso.

4. **Personalizar el pipeline**: Modifica `src/train.py` para adaptar el procesamiento de datos a tu tarea específica.

## Uso

### Entrenamiento del Modelo

```bash
# Entrenamiento con configuración predeterminada
python src/train.py

# Entrenamiento con una configuración específica de modelo
python src/train.py model=tu_modelo_personalizado

# Entrenamiento con una configuración específica de entrenamiento
python src/train.py training=tu_configuracion

# Modificar parámetros específicos
python src/train.py training.epochs=5 training.batch_size=32
```

### Predicción con el Modelo Entrenado

```bash
# Modo interactivo
python src/predict.py

# Predicción para un texto específico
python src/predict.py --text "Texto de ejemplo"

# Usar un modelo específico
python src/predict.py --model_path "./outputs/tu_modelo"
```

## Configuración con Hydra

El proyecto utiliza Hydra para la gestión de configuraciones, lo que permite:

- Cambiar configuraciones sin modificar el código
- Combinar diferentes archivos de configuración
- Sobrescribir parámetros específicos desde la línea de comandos
- Mantener múltiples configuraciones para diferentes experimentos

### Principales Archivos de Configuración

- `conf/config.yaml`: Configuración global del proyecto
- `conf/model/*.yaml`: Configuraciones para diferentes arquitecturas de modelos
- `conf/training/*.yaml`: Configuraciones para diferentes regímenes de entrenamiento

## Personalización

### Implementar Nuevas Tareas de NLP

1. **Clasificación de Texto**: Adaptar las clases de modelos y datasets para tu tarea específica
2. **Named Entity Recognition (NER)**: Adaptar la clase del modelo para usar `AutoModelForTokenClassification`
3. **Question Answering**: Implementar con `AutoModelForQuestionAnswering`
4. **Generación de Texto**: Usar `AutoModelForCausalLM` o `AutoModelForSeq2SeqLM`

### Cambiar Modelos Preentrenados

Edita `conf/model/*.yaml` para usar cualquier modelo de HuggingFace:

```yaml
model:
  name: "bert-base-multilingual-cased"  # O cualquier otro modelo
  type: "classification"  # Ajustar según tu tarea (sequence, token-classification, etc.)
  # Otros parámetros específicos para tu tarea
```

## Contribuciones

Las contribuciones son bienvenidas. Por favor, siga estos pasos:

1. Fork del repositorio
2. Cree una rama para su funcionalidad (`git checkout -b feature/nueva-caracteristica`)
3. Haga commit de sus cambios (`git commit -am 'Añadir nueva característica'`)
4. Push a la rama (`git push origin feature/nueva-caracteristica`)
5. Cree un Pull Request

## Licencia

[MIT](LICENSE)

## Contacto

Para preguntas y soporte, por favor abra un issue en este repositorio.
