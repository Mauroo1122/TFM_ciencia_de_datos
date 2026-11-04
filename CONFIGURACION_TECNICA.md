# Configuración técnica

Entorno de ejecución, versiones de las librerías e hiperparámetros de las cinco técnicas comparadas, tal como figuran en los notebooks.

## Entorno

Miniconda, entorno `tesis_env`, Python 3.10.19. Todo el procesamiento se ejecutó localmente, incluido el modelo de lenguaje, que operó mediante Ollama sin llamadas a servicios externos.

Dos componentes forman parte de la definición de los resultados: la versión de gensim, porque C_npmi se estima con su implementación y sus parámetros por defecto (entre ellos, la ventana deslizante de diez tokens), y el modelo de lematización de spaCy, que determina el vocabulario de LDA y de K-Means sobre TF-IDF.

| Componente | Función | Versión |
|---|---|---|
| gensim | C_npmi y entrenamiento de Word2Vec | 4.4.0 |
| scikit-learn | TF-IDF, CountVectorizer, LDA, K-Means, SVD truncada | 1.7.2 |
| spacy | Lematización | 3.8.2 |
| es_core_news_sm | Modelo de lematización para el español | 3.8.0 |
| nltk | Palabras funcionales del español | 3.9.2 |
| bertopic | BERTopic | 0.17.4 |
| sentence-transformers | Embeddings de oración (`paraphrase-multilingual-MiniLM-L12-v2`) | 5.2.0 |
| umap-learn | Reducción de dimensionalidad en BERTopic y Figura 4.3 | 0.5.11 |
| hdbscan | Agrupamiento por densidad en BERTopic | 0.8.41 |
| ollama | Ejecución local del modelo de lenguaje | 0.6.1 |
| llama3.1 | 8.000 millones de parámetros, cuantizado a 4 bits | `llama3.1:latest` (46e0c10c039e) |
| lingua-language-detector | Detección de idioma | 2.1.1 |
| numpy | Operaciones numéricas | 2.2.5 |
| pandas | Manipulación de datos | 2.3.3 |
| scipy | Pruebas de Wilcoxon y de Mann-Whitney | 1.15.3 |
| matplotlib | Figuras | 3.10.7 |
| seaborn | Figuras exploratorias | 0.13.2 |

## Hiperparámetros

En todas las técnicas, «semillas» significa 42 en la corrida de referencia y 42 y 0 a 8 en el conjunto de diez semillas. La lista de exclusión es la de `DICCIONARIO_EXCLUSION.md` (449 entradas).

### LDA

| Componente | Parámetro | Valor |
|---|---|---|
| CountVectorizer | stop_words | lista de exclusión |
| | min_df / max_df | 10 / 0,6 |
| | ngram_range | (1, 2) |
| LatentDirichletAllocation | n_components | 6 |
| | max_iter | 100 en la corrida de referencia; 50 en las diez semillas y en el barrido de K |
| | learning_method | `'online'` |
| | random_state | semillas |
| | n_jobs | −1 |

### K-Means sobre TF-IDF

| Componente | Parámetro | Valor |
|---|---|---|
| TfidfVectorizer | stop_words | lista de exclusión |
| | min_df / max_df | 10 / 0,6 |
| | ngram_range | (1, 2) |
| | sublinear_tf | True |
| TruncatedSVD | n_components | 100 |
| | random_state | semillas (se recalcula con cada semilla) |
| Normalizer | — | normalización euclídea de la matriz reducida |
| KMeans (modelo final) | n_clusters | 6 |
| | init / max_iter / n_init | `'k-means++'` / 300 / 10 |
| | random_state | semillas |
| KMeans (barrido de K) | max_iter / n_init | 100 / 5 |
| | algorithm | `'elkan'` en la corrida de referencia |

### K-Means sobre Word2Vec

| Componente | Parámetro | Valor |
|---|---|---|
| Word2Vec | vector_size / window / min_count | 100 / 5 / 5 |
| | sg | 1 (skip-gram) |
| | epochs | 10 |
| | workers | 1 |
| | seed | semillas (se reentrena con cada semilla) |
| Vector por documento | — | promedio de los vectores de sus tokens presentes en el vocabulario y no excluidos |
| | documentos sin tokens | quedan sin vector y no se agrupan |
| KMeans | n_clusters / n_init | 6 / 30 |
| | random_state | semillas |

### BERTopic

| Componente | Parámetro | Valor |
|---|---|---|
| BERTopic | language | `'spanish'` (`paraphrase-multilingual-MiniLM-L12-v2`) |
| | min_topic_size | 80 en la corrida reportada; 15 en la exploratoria |
| | nr_topics | `'auto'` en la exploratoria; `reduce_topics(nr_topics=7)` en la reportada (seis tópicos más el ruido) |
| | calculate_probabilities | True en la corrida de referencia; False en las diez semillas |
| | representation_model | KeyBERTInspired durante el ajuste |
| UMAP | n_neighbors / n_components / min_dist | 15 / 5 / 0,0 |
| | metric | `'cosine'` |
| | random_state | semillas (única fuente de variación entre semillas) |
| HDBSCAN | tamaño mínimo de grupo | min_topic_size |
| CountVectorizer (ajuste) | preprocessor / stop_words | remoción de tildes / lista de exclusión |
| | min_df / ngram_range | 3 / (1, 2) |
| `update_topics` (palabras reportadas) | vectorizer_model | remoción de tildes y minúsculas; mismos stop_words, min_df y ngram_range |
| | representation_model | None (c-TF-IDF) |

### Modelo de lenguaje

| Parámetro | Valor |
|---|---|
| Modelo | llama3.1, ejecutado localmente con Ollama |
| Muestra | 200 reseñas por parque (2.000), semilla 42 |
| Réplicas | una ejecución |
| Reseñas para el descubrimiento | 500 de la muestra |
| Categorías solicitadas | 6 |
| Temperatura | 0,3 en el descubrimiento; 0,1 en la clasificación |
| num_predict | 800 en el descubrimiento; 120 en la clasificación |
| Truncado del texto | 200 caracteres en el descubrimiento; 400 en la clasificación |
| Reintentos | 3, con una pausa de 1 segundo |
| Reseñas no enviadas | menos de 5 caracteres |
| Palabras por categoría | 10, derivadas a posteriori por peso TF-IDF sobre el texto lematizado |
