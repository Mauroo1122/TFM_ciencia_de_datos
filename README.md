# Detección de tópicos en reseñas de parques de Montevideo

Código de la tesis *Comparación de cinco técnicas de detección de tópicos sobre reseñas de parques públicos de Montevideo* (Maestría en Ciencia de Datos, Universidad Católica del Uruguay).

## Datos

Los datos no se incluyen; se conservan en la Universidad Católica del Uruguay. Los notebooks esperan esta estructura:

```
<raíz>/
├── notebooks/
├── csv_parques/
├── df_generic_cleaned.pkl
└── Topic/
    ├── Dataframes/
    ├── Resultados/Topico/
    └── figuras/
```

## Notebooks

Se ejecutan en orden, desde la carpeta `notebooks/`.

| Notebook | Contenido |
|---|---|
| 01_limpieza_datos | Limpieza y anonimización del corpus |
| 02_EDA | Descripción del corpus · Figura 3.2 |
| 03_LDA | LDA |
| 04_kmeans_tfidf | K-Means sobre TF-IDF |
| 05_kmeans_word2vec | K-Means sobre Word2Vec |
| 06_BERTopic | BERTopic |
| 07_LLM | Llama 3.1 en modalidad zero-shot (requiere Ollama) |
| 08_metricas | Tablas 3.1, 3.2, 4.1 y 4.2 |
| 09_analisis_derivados | Tablas 4.3 a 4.5 · columnas de la Tabla 4.1 con corpus de referencia de tamaño común · robustez |
| 10_porcentajes_dos_decimales | Porcentajes reportados con dos decimales |
| 11_figuras | Figuras 3.1 y 4.1 a 4.5 · Tabla 4.5 |

Cada celda indica qué tabla, figura o sección de la tesis produce. La lista de exclusión está en `DICCIONARIO_EXCLUSION.md`.

## Entorno

Python 3.10.19. Las versiones de las librerías y los hiperparámetros de cada técnica están en `CONFIGURACION_TECNICA.md`.
