# Analisis de Datos utilizando un modelo local (Ollama y SQLite3)

Este proyecto consiste en la extracción de reseñas desde una base de datos local mediante SQLite3, 
el cual clasifica estas reseñas mediante Ollama según ciertos criterios descritos en el archivo,
para guardar estos resultados y generar reportes analíticos

## Requisitos

* Python 3.13

* Ollama instalado en el sistema (descargar desde ollama.com)

* Modelo para Ollama (en este caso qwen2.5:1.5b)

* Instalar uv "uv_build>=0.12.21,<0.13.0"


## Instalación

Instala las dependencias necesarias:
   ```bash
   uv sync
   ```
## Modelo Utilizado y Cómo Levantarlo

Utilice el modelo **qwen2.5:1.5b** con Ollama

Este es un modelo liviano de la familia Qwen2.5 (que usa 1.5 mil millones de parámetros), ideal para inferencia rápida con uso de datos estructurados

## Ejecución
* Asegúrate de tener el archivo de base de datos el mismo directorio que el notebook.   

* Inicia Ollama en tu sistema local mientras ejecuta el codigo.   

* Abre Jupyter Notebook o JupyterLab y ejecuta todas las celdas en orden secuencial.

## Decisiones Relevantes

* Salida Estructurada, se definió un esquema con campos restringidos para la categoria_problema y area_mejora, garantizando que el modelo devuelva únicamente las opciones válidas y tener un output mas estable.   

* Temperatura en 0.0, se fijó la temperatura en cero para forzar respuestas deterministas y reducir al mínimo las alucinaciones en la clasificación.   

* Manejo de la Base de Datos, se exportaron primero los resultados filtrados mediante una consulta SQL a un archivo .txt local llamado resultados_reviews.txt para aislar la etapa de extracción de la clasificación, este archivo se genera al ejecutar las celdas de la parte 1.

* Se creó una tabla llamada clasification en SQLite para hacer joins analíticos, esta tabla se genera automaticamente al correr las celdas de la parte 3


## Mejoras futuras
* Procesamiento por lotes: Clasificar las reseñas en lotes para reducir la sensibilidad y el tiempo total de la ejecución del bucle

* Evaluación del Modelo: Realizar pruebas comparativas con algún dataset pequeño etiquetado manualmente para validar la precisión del modelo de 1.5B, comparandolo a modelos más grandes