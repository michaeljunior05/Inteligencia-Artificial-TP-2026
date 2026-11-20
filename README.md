# TP de Inteligencia Artificial 2026 — SQAC
Integrantes: Junior Jordan Flores Ramos, Marcial Alejandro Insaurralde, Luis Uriel Espindola.
Notebook principal: `natebook.ipynb`.

El proyecto reformula SQAC como una tarea de **clasificación binaria de pares pregunta–oración**: dado una pregunta y una oración candidata del contexto, el modelo predice si esa oración contiene la respuesta según la etiqueta construida a partir de `answer_start`.

## Contenido del notebook

El archivo integra estas etapas:

- **Etapa 1:** análisis exploratorio, particiones oficiales, generación de pares pregunta–oración y baseline TF-IDF con regresión logística.
- **Etapa 2:** análisis de errores, reducción de negativos en Train y experimentos con MLP sobre características TF-IDF.
- **Etapa 3:** clasificadores Naive Bayes como referencia y modelos neuronales sobre embeddings, incluidos embeddings preentrenados en español y arquitecturas pareadas.
- **Etapa 5:** comparación y selección del modelo, verificación en Dev, evaluación final en Test, inspección cualitativa y análisis ético/de sesgos.

La versión actual no contiene una sección de Etapa 4.

## Dataset y entorno

- **Dataset:** `PlanTL-GOB-ES/sqac`, cargado desde Hugging Face Datasets mediante `load_dataset`. Se utilizan las particiones oficiales Train, Validation/Dev y Test.
- **Entorno recomendado:** Google Colab. El notebook usa `google.colab.drive` para montar Google Drive y contiene funciones de descarga de archivos de Colab.
- **Framework:** TensorFlow/Keras. No usa PyTorch.
- **Otras librerías:** NumPy, pandas, scikit-learn, Matplotlib, Seaborn, Hugging Face Datasets y spaCy.
- **Dependencia fijada explícitamente:** spaCy `3.8.16`; el notebook instala el modelo de idioma `es_core_news_md`.

## Preparación y ejecución

1. Abrir `natebook.ipynb` en Google Colab y conectar Google Drive cuando lo solicite el notebook.
2. Ejecutar las celdas desde el inicio y en orden. La carga del dataset se realiza desde Hugging Face; no requiere descargar SQAC manualmente.
3. La celda inicial instala spaCy y descarga `es_core_news_md`. Se requiere acceso a Internet para esas descargas.
4. Ejecutar las etapas de desarrollo antes de la Etapa 5: varias celdas reutilizan datos, vectorizadores, modelos e historias generados anteriormente.
5. Antes de ejecutar la carga del modelo seleccionado en la Etapa 5, verificar que el archivo de pesos esté disponible en Google Drive en esta ruta exacta:

   `/content/drive/MyDrive/IA- TP/modelo_1_pesos.weights.h5`

   Enlace de Drive informado para el archivo: [Pesos del Modelo 1 de la Etapa 3](https://drive.google.com/file/d/1cRZTUdRPfmFwEo7AwH5YNgokuD7fl8T0/view?usp=drivesdk). Asegurarse de que la cuenta de Colab tenga acceso y que el archivo esté disponible con el nombre y la ruta indicados arriba.

   La celda de la Etapa 5 carga ese archivo con `modelo_pareado.load_weights(...)`; no lo crea. El archivo de pesos no está incluido en este repositorio, por lo que debe guardarse previamente en esa ubicación.
6. La Etapa 5 prepara y evalúa Test con el Modelo 1 pareado seleccionado, usando el umbral 0,50. Test está reservado para la evaluación final: realizarla una sola vez y no usar sus resultados para volver a elegir o ajustar el modelo.

El notebook contiene varios entrenamientos y su ejecución completa puede llevar tiempo. Si se inicia una sesión nueva de Colab, hay que volver a ejecutar las celdas necesarias en orden para reconstruir las variables y modelos.

## Archivos y resultados

- `natebook.ipynb`: notebook con el desarrollo y las celdas de análisis.
- La inspección de errores de la Etapa 2 puede exportar un CSV y ofrecer su descarga desde Colab.
- Los gráficos se muestran en las salidas de las celdas; el notebook no exporta automáticamente todos los gráficos como archivos independientes.
