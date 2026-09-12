# Taller 06: Reducción de Dimensiones

## 📋 Descripción

Se aplican y comparan cinco técnicas de reducción de dimensiones —**PCA, MDS Clásico, MDS Métrico, MDS No-métrico y UMAP**— sobre datos de acelerómetro y giroscopio de teléfono y smartwatch del [WISDM Smartphone and Smartwatch Activity and Biometrics Dataset](https://archive.ics.uci.edu/dataset/507/wisdm+smartphone+and+smartwatch+activity+and+biometrics+dataset).

Para 3 voluntarios seleccionados aleatoriamente (de 50 disponibles, códigos 1600–1650, sin el 1614), y para cada uno de los 4 casos (`phone-accel`, `phone-gyro`, `watch-accel`, `watch-gyro`):

- Se construye una matriz con las 30 columnas `xyzbins` (`X0..X9`, `Y0..Y9`, `Z0..Z9`) y se usa `ACTIVITY` como ground truth.
- Se proyectan los datos a 2 dimensiones con cada una de las 5 técnicas, coloreando por actividad.
- Se repite el análisis uniendo los 3 voluntarios en una sola matriz por caso.

El notebook cierra con una discusión sobre qué actividades se diferencian mejor, cuáles se superponen, y una comparación cualitativa entre las 5 técnicas.

## 📁 Estructura del repositorio

```
.
├── main.ipynb   # Notebook principal
├── README.md
└── wisdm-dataset/                              # Dataset
    └── arff_files/
        ├── phone/{accel,gyro}/
        └── watch/{accel,gyro}/
```

## 🗂️ Dataset

El dataset **ya está incluido en este repositorio**, dentro de `wisdm-dataset/arff_files/`, con la estructura mostrada arriba. No es necesario descargarlo ni descomprimirlo aparte: basta con clonar el repositorio y ejecutar el notebook.

Fuente original: [WISDM Smartphone and Smartwatch Activity and Biometrics Dataset (UCI)](https://archive.ics.uci.edu/dataset/507/wisdm+smartphone+and+smartwatch+activity+and+biometrics+dataset).

## ⚙️ Requisitos

```bash
pip install pandas numpy scipy scikit-learn matplotlib seaborn umap-learn
```

Probado con Python 3.11.

## ▶️ Cómo ejecutar

1. Clone este repositorio (el dataset ya viene incluido, no requiere pasos adicionales).
2. Abra `main.ipynb` en Jupyter Notebook / JupyterLab / VS Code.
3. Ejecute las celdas en orden (`Run All`).

> **Nota:** el notebook usa los hiperparámetros por defecto de `scikit-learn` y `umap-learn` (sin ajustes para acelerar el cómputo), por lo que la ejecución completa —especialmente los casos combinados, con hasta ~2000 muestras— puede tardar varios minutos.

## 🖼️ Resultados visuales

**Reducción de dimensiones individual**
<img width="2514" height="474" alt="phone-accel" src="https://github.com/user-attachments/assets/7dbe3b62-3628-43d9-9ccd-045426c66461" />

<img width="2514" height="474" alt="2" src="https://github.com/user-attachments/assets/52163827-59c2-49a7-978c-3ce5b8c4c81e" />

<img width="2514" height="474" alt="3" src="https://github.com/user-attachments/assets/48a5ff7e-cba2-47ff-9c92-202cb52d663d" />

<img width="2514" height="474" alt="4" src="https://github.com/user-attachments/assets/951482d2-1d52-410a-8630-8d82e47bb56f" />

<img width="2514" height="474" alt="5" src="https://github.com/user-attachments/assets/93464bf3-095c-4df5-ac5b-4b0fc77ffa94" />

<img width="2514" height="474" alt="6" src="https://github.com/user-attachments/assets/489fe91f-cf10-4ef7-bd64-dbc0639a6629" />

<img width="2514" height="474" alt="7" src="https://github.com/user-attachments/assets/1955ed22-c728-4a61-8afc-ebabca335ee2" />

<img width="2514" height="474" alt="8" src="https://github.com/user-attachments/assets/44f989e4-d6a6-4e32-ae3b-064686f8a3ea" />

<img width="2514" height="474" alt="9" src="https://github.com/user-attachments/assets/507d098c-6825-4c16-a805-77bc3aa8df3e" />

<img width="2514" height="474" alt="10" src="https://github.com/user-attachments/assets/585358da-0df4-49b6-b8b0-00c0bd51097c" />

<img width="2514" height="474" alt="11" src="https://github.com/user-attachments/assets/0f6ae8a4-ef65-4c31-9979-a8691b665db5" />

<img width="2514" height="474" alt="12" src="https://github.com/user-attachments/assets/ca82215f-7259-4eee-bcd5-c64ab877acb9" />

**Reducción de dimensiones combinado**

<img width="2514" height="474" alt="21" src="https://github.com/user-attachments/assets/1c68ea62-1764-4d35-8f1b-a3cb49b4e8ca" />

<img width="2514" height="474" alt="22" src="https://github.com/user-attachments/assets/63144746-a244-45a6-a88c-aeabb332ee3a" />


<img width="2514" height="474" alt="23" src="https://github.com/user-attachments/assets/dd8b5f6b-4c59-442c-81f1-6ed8f5315b2f" />


<img width="2514" height="474" alt="24" src="https://github.com/user-attachments/assets/23f74990-0f7b-420e-84ff-6a1d2377d091" />

## 📊 Resultados principales

- Las actividades con movimientos amplios y repetitivos (**caminar, trotar, subir/bajar escaleras**) tienden a separarse mejor en 2D, especialmente con datos de acelerómetro.
- Las actividades estáticas o de movimiento fino (**sentado, de pie, escribir, comer**) se superponen considerablemente, ya que producen señales de baja variabilidad muy similares entre sí.
- **UMAP** produce las agrupaciones locales más compactas y visualmente separadas; **PCA** y **MDS Clásico** son más útiles para interpretar la estructura global; **MDS No-métrico** mostró más dificultad para separar las clases en este dataset, incluso con múltiples inicializaciones.

Ver la sección de Discusión al final del notebook para el análisis completo.
