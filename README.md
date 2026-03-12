
# Comparación entre embeddings de turno y estados latentes dinámicos para la recuperación aproximada de vecinos en diálogos orientados a tareas

**Trabajo Final**  
Curso: *Algoritmos Recientes para Búsqueda de Proximidad en Altas Dimensiones*  
Doctorado en Ciencias de la Computación  
Universidad Nacional de San Luis (UNSL)

Docentes: **Edgar Chávez** y **Nora Reyes**

---

## Descripción

Este repositorio contiene el código y los experimentos desarrollados para el trabajo final del curso *Algoritmos Recientes para Búsqueda de Proximidad en Altas Dimensiones*.

El objetivo del trabajo es analizar el comportamiento de distintos **métodos de búsqueda aproximada de vecinos (ANN)** en espacios vectoriales generados a partir de diálogos orientados a tareas y explorar el uso de **representaciones dinámicas del estado conversacional**.

Los experimentos se realizan sobre el corpus **MultiWOZ 2.2**, generando embeddings semánticos para cada turno de diálogo y comparando distintas estrategias de indexación utilizando la librería **FAISS**.

---

## Resumen

En los sistemas de diálogo orientados a tareas, la representación del estado conversacional constituye un componente central para la toma de decisiones del agente. En enfoques actuales, cada turno del diálogo se representa mediante embeddings semánticos individuales. Sin embargo, los diálogos son procesos secuenciales en los que el significado de cada intervención depende del historial de la conversación, lo que motiva el estudio de representaciones que integren información acumulativa del diálogo mediante estados latentes dinámicos.

En este trabajo se comparan embeddings estáticos de turno con estados latentes dinámicos construidos a lo largo del diálogo. Utilizando el corpus **MultiWOZ 2.2**, se generaron embeddings mediante dos modelos basados en sentence transformers (**all-mpnet-base-v2** y **all-MiniLM-L6-v2**) y se evaluó su comportamiento en distintos índices de búsqueda aproximada implementados con **FAISS**.

Los experimentos analizan el compromiso entre precisión de recuperación y eficiencia computacional utilizando distintos métodos de búsqueda aproximada de vecinos. Asimismo, se estudia la evolución de los estados latentes dinámicos a lo largo del diálogo y su impacto en la estructura del espacio vectorial mediante técnicas de reducción de dimensionalidad.

Los resultados permiten explorar el potencial de los estados latentes dinámicos como consultas informativas para recuperar estados conversacionales similares en grandes colecciones de interacciones y facilitar la reutilización de estrategias de acción en agentes orientados a tareas.

---

## Dataset

Los experimentos utilizan el corpus **MultiWOZ 2.2**, un dataset ampliamente utilizado en investigación sobre sistemas de diálogo orientados a tareas.

Referencia:

Zang, X., Rastogi, A., Sunkara, S., Gupta, R., Zhang, J., & Chen, J. (2020).  
*MultiWOZ 2.2: A Dialogue Dataset with Additional Annotation Corrections and State Tracking Baselines.*

El dataset **no se incluye en este repositorio**.

Para reproducir los experimentos debe descargarse desde:

https://github.com/budzianowski/multiwoz

Una vez descargado, ubicar los archivos en el directorio:

data/multiwoz/

---

## Modelos de embeddings

Se utilizaron dos modelos de **Sentence Transformers**:

- all-mpnet-base-v2  
- all-MiniLM-L6-v2  

Estos modelos permiten generar representaciones semánticas densas para cada turno del diálogo.

---

## Representaciones analizadas

### Embeddings estáticos de turno

Cada turno del diálogo se representa mediante un embedding independiente generado a partir del texto del turno.

### Estados latentes dinámicos

Se construyen acumulando información de turnos anteriores según la siguiente actualización:

h_t = LayerNorm(h_{t-1} + e_t)

donde:

- e_t es el embedding del turno actual  
- h_t es el estado dinámico del diálogo  
- LayerNorm estabiliza la magnitud del vector  

---

## Métodos de búsqueda evaluados

Los experimentos utilizan **FAISS** con los siguientes índices:

- FlatL2 (búsqueda exacta)
- IVF
- HNSW
- IVFPQ

Las métricas evaluadas incluyen:

- Recall@5
- Tiempo promedio de consulta

---

## Visualización del espacio vectorial

Para explorar la estructura del espacio semántico se aplica **UMAP** para reducir la dimensionalidad de los embeddings y visualizar su distribución en un plano bidimensional.

---

# Estructura del repositorio

ANN-UNSL/

```
├── data/  
│   └── multiwoz/ (dataset no incluido)  
│
├── embeddings/  
│
├── notebooks/  
│   ├── 01_carga_datos_y_embeddings.ipynb  
│   ├── 02_indexacion_y_ann.ipynb  
│   └── 03_estados_latentes_dinamicos.ipynb  
│
├── figures/  
│
├── report/  
│   └── informe_final.pdf  
│
├── requirements.txt  
│
└── README.md  
```

---

## Descripción de las notebooks

### 01_carga_datos_y_embeddings.ipynb

- carga del dataset MultiWOZ
- generación de embeddings
- comparación entre modelos MPNet y MiniLM

### 02_indexacion_y_ann.ipynb

- construcción de índices FAISS
- evaluación de métodos ANN
- medición de recall y tiempos de consulta

### 03_estados_latentes_dinamicos.ipynb

- construcción de estados dinámicos del diálogo
- análisis de similitud entre representaciones
- visualización del espacio semántico mediante UMAP

---

# Reproducción de los experimentos

## 1. Clonar el repositorio

git clone https://github.com/<usuario>/ANN-UNSL.git  
cd ANN-UNSL

## 2. Crear entorno de Python

python -m venv venv  
source venv/bin/activate

En Windows:

venv\Scripts\activate

## 3. Instalar dependencias

pip install -r requirements.txt

---

## Dependencias principales

- Python 3.10+
- numpy
- pandas
- faiss
- sentence-transformers
- scikit-learn
- umap-learn
- matplotlib

---

## 4. Ejecutar las notebooks

1. notebooks/01_carga_datos_y_embeddings.ipynb  
2. notebooks/02_indexacion_y_ann.ipynb  
3. notebooks/03_estados_latentes_dinamicos.ipynb  

---

## Informe final

El informe del trabajo se encuentra en:

report/informe_final.pdf

---

## Autor

Juan Manuel Fernández  
Doctorado en Ciencias de la Computación  
Universidad Nacional de San Luis
