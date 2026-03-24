# Python para la Investigación Científica
## Temario Completo de Python para Inteligencia Artificial

## MÓDULO 1: FUNDAMENTOS DE PYTHON

### 1.1 Introducción a Python
- ¿Qué es Python?
- Instalación y configuración del entorno
- Interpretador de Python
- Primeros pasos: "Hello World"
- Comentarios en código

### 1.2 Variables y Tipos de Datos Primitivos
- Concepto de variable
- Nomenclatura de variables (PEP 8)
- Tipos primitivos:
  - **String** (cadenas de texto)
    - Creación y manipulación
    - Métodos de strings (upper, lower, split, replace)
    - Indexación y slicing
    - Formato de strings (%, .format(), f-strings)
  - **Integers** (números enteros)
    - Operaciones básicas
    - Conversión de tipos
  - **Float** (números decimales)
    - Precisión y redondeo
    - Operaciones aritméticas
  - **Boolean** (valores lógicos)
    - True y False
    - Valores truthy y falsy
  - **Complex** (números complejos)
    - Componentes real e imaginaria
    - Operaciones complejas

### 1.3 Operadores
- **Aritméticos**: +, -, *, /, //, %, **
- **Comparación**: ==, !=, <, >, <=, >=
- **Lógicos**: and, or, not
- **Asignación**: =, +=, -=, *=, /=
- **Identidad**: is, is not
- **Pertenencia**: in, not in
- Jerarquía de operadores (precedencia)

### 1.4 Entrada y Salida
- `print()` - mostrar información en consola
- `input()` - recibir datos del usuario
- Formateo de salida
- Manejo de excepciones en entrada/salida

---

## MÓDULO 2: ESTRUCTURAS DE DATOS COLECTORAS

### 2.1 Listas
- Definición y características
- Creación de listas
- Indexación (positiva y negativa)
- Slicing (rebanadas)
- Métodos de listas:
  - `append()`, `extend()`, `insert()`
  - `remove()`, `pop()`, `clear()`
  - `sort()`, `reverse()`, `copy()`
  - `count()`, `index()`
- Iteración sobre listas
- List comprehensions (comprensiones de lista)

### 2.2 Tuplas
- Definición e inmutabilidad
- Creación de tuplas
- Desempaquetado de tuplas
- Métodos disponibles
- Cuándo usar tuplas vs listas
- Tuplas como claves de diccionarios

### 2.3 Diccionarios
- Definición y estructura (key: value)
- Creación de diccionarios
- Acceso a valores
- Métodos de diccionarios:
  - `keys()`, `values()`, `items()`
  - `get()`, `pop()`, `update()`
  - `clear()`, `copy()`
- Iteración sobre diccionarios
- Dict comprehensions
- Diccionarios anidados
- Diccionarios como base de datos

### 2.4 Conjuntos (Sets)
- Definición y características
- Creación de conjuntos
- Métodos de conjuntos:
  - `add()`, `remove()`, `discard()`, `clear()`
  - `union()` (|), `intersection()` (&)
  - `difference()` (-), `symmetric_difference()` (^)
  - `issubset()`, `issuperset()`, `isdisjoint()`
- Utilidad de conjuntos

### 2.5 Arreglos y Vectores (Introducción)
- Diferencia entre listas y arreglos
- Vectores: fila y columna
- Matrices
- Introducción a NumPy

---

## MÓDULO 3: CONTROL DE FLUJO

### 3.1 Condicionales
- Estructura if-else
- Estructura if-elif-else
- Operadores de comparación
- Expresiones booleanas
- Condicionales anidados
- Operador ternario

### 3.2 Conectores Lógicos
- **AND (y)**: condición1 and condición2
- **OR (o)**: condición1 or condición2
- **NOT (no)**: not condición
- Tablas de verdad
- Cortocircuito (short-circuit evaluation)

### 3.3 Bucles
- **Bucle for**:
  - Iteración sobre secuencias
  - Función `range()`
  - Enumeración con `enumerate()`
  - `zip()` para iterar múltiples secuencias
- **Bucle while**:
  - Condiciones de continuidad
  - Condiciones de salida
- **Control de bucles**:
  - `break` - salir del bucle
  - `continue` - siguiente iteración
  - `pass` - hacer nada
- **Bucles anidados**

### 3.4 Manejo de Excepciones
- Estructura try-except-else-finally
- Tipos comunes de excepciones:
  - `ZeroDivisionError`
  - `NameError`
  - `TypeError`
  - `ValueError`
  - `IndexError`
  - `KeyError`
- Excepciones personalizadas
- Lanzar excepciones (`raise`)

---

## MÓDULO 4: FUNCIONES

### 4.1 Definición y Sintaxis
- Estructura basic de una función
- Parámetros y argumentos
- `return` - retornar valores
- Docstrings (documentación de funciones)

### 4.2 Tipos de Parámetros
- Parámetros posicionales
- Parámetros con valores por defecto
- Parámetros nombrados (keyword arguments)
- `*args` - argumentos variables
- `**kwargs` - argumentos nombrados variables

### 4.3 Tipos de Funciones
- **Funciones estándar**: definidas con `def`
- **Funciones Lambda** (anónimas):
  - Sintaxis: `lambda x: expresión`
  - Casos de uso con `map()`, `filter()`, `sort()`
- **Funciones Matemáticas**:
  - Sin parámetros, con parámetros, con retorno
  - Funciones polinómicas
  - Funciones trigonométricas

### 4.4 Funciones Recursivas
- Definición de recursión
- Caso base y caso recursivo
- Profundidad máxima de recursión
- Ejemplos: factorial, fibonacci
- Ventajas y desventajas

### 4.5 Funciones de Orden Superior
- Funciones que reciben funciones
- Funciones que retornan funciones
- `map()`, `filter()`, `reduce()`
- Decoradores (introducción)

### 4.6 Scope (Alcance) de Variables
- Scope local
- Scope global
- Scope no local (`nonlocal`)
- Variables globales

---

## MÓDULO 5: PROGRAMACIÓN ORIENTADA A OBJETOS (POO)

### 5.1 Conceptos Básicos
- Clases y objetos
- Atributos y métodos
- Instancias de clases
- Constructor (`__init__`)

### 5.2 Encapsulación
- Atributos públicos y privados
- Métodos getters y setters
- Propiedades (`@property`)

### 5.3 Herencia
- Herencia simple
- Herencia múltiple
- Método `super()`
- Sobrescritura de métodos

### 5.4 Polimorfismo
- Métodos con el mismo nombre
- Sobrecarga de operadores
- Duck typing

### 5.5 Métodos Especiales
- `__str__()`, `__repr__()`
- `__eq__()`, `__lt__()`, `__gt__()`
- `__add__()`, `__sub__()`, `__mul__()`
- `__len__()`, `__getitem__()`

---

## MÓDULO 6: BIBLIOTECAS ESTÁNDAR

### 6.1 Módulos y Paquetes
- Importación de módulos
- `import módulo`
- `from módulo import función`
- `import módulo as alias`

### 6.2 Módulos Útiles
- **math**: operaciones matemáticas
- **random**: generación de números aleatorios
- **datetime**: manejo de fechas y horas
- **os**: operaciones del sistema operativo
- **sys**: parámetros del sistema
- **json**: manejo de archivos JSON
- **csv**: lectura/escritura de CSV

### 6.3 Archivos
- Lectura de archivos: `open()`, `read()`
- Escritura de archivos: `write()`
- Context managers: `with`
- Manejo de diferentes formatos:
  - Texto plano
  - JSON
  - CSV
  - Excel

---

## MÓDULO 7: NUMPY (NUMERICAL PYTHON)

### 7.1 Arrays de NumPy
- Creación de arrays
- Tipos de datos (`dtype`)
- Dimensiones y forma (`shape`, `ndim`)
- Indexación y slicing de arrays

### 7.2 Operaciones con Arrays
- Operaciones matemáticas elemento a elemento
- Operaciones con escalares
- Funciones universales (`ufunc`)
- Álgebra lineal

### 7.3 Reshape y Transpose
- `reshape()` - cambiar forma
- `transpose()` - transpuesta (`.T`)
- `flatten()` - aplanar arrays
- `concatenate()` - unir arrays

### 7.4 Operaciones Estadísticas
- `sum()`, `mean()`, `std()`, `var()`
- `min()`, `max()`
- `argmin()`, `argmax()`
- Cálculos por eje

### 7.5 Generación de Datos
- `np.zeros()`, `np.ones()`, `np.full()`
- `np.arange()`, `np.linspace()`
- `np.random.rand()`, `np.random.randint()`
- `np.random.normal()`

---

## MÓDULO 8: PANDAS (ANÁLISIS DE DATOS)

### 8.1 Series
- Creación de Series
- Acceso a datos
- Operaciones con Series
- Métodos útiles

### 8.2 DataFrames
- Creación de DataFrames
- Acceso a filas, columnas y elementos
- Métodos de exploración:
  - `head()`, `tail()`, `info()`, `describe()`
  - `shape`, `columns`, `index`

### 8.3 Limpieza de Datos
- Valores faltantes (`NaN`)
- `isnull()`, `dropna()`, `fillna()`
- Eliminación de duplicados
- Cambio de tipos de datos

### 8.4 Manipulación de DataFrames
- Selección de columnas
- Filtrado de filas
- `loc[]` y `iloc[]`
- `apply()` con funciones lambda
- Concatenación y merge

### 8.5 Análisis Exploratorio
- Estadísticas descriptivas
- Correlaciones
- Agrupación (`groupby()`)
- Pivot tables

### 8.6 Lectura y Escritura
- CSV: `read_csv()`, `to_csv()`
- Excel: `read_excel()`, `to_excel()`
- JSON: `read_json()`, `to_json()`
- SQL: `read_sql()`

---

## MÓDULO 9: MATPLOTLIB Y VISUALIZACIÓN

### 9.1 Conceptos Básicos
- Figuras y ejes
- Estructura de plots
- `plt.show()`, `plt.savefig()`

### 9.2 Tipos de Gráficos
- **Líneas**: `plot()`
- **Puntos/Dispersión**: `scatter()`
- **Barras**: `bar()`, `barh()`
- **Histogramas**: `hist()`
- **Cajas**: `boxplot()`
- **Pastel**: `pie()`
- **Heatmaps**: `imshow()`

### 9.3 Personalizacion
- Títulos y etiquetas (`title()`, `xlabel()`, `ylabel()`)
- Leyendas (`legend()`)
- Colores y estilos
- Tamaño de figura (`figsize`)
- Subplots (`subplot()`)

### 9.4 Gráficos 3D
- Importación de `Axes3D`
- Gráficos de superficie
- Gráficos de dispersión 3D

### 9.5 Seaborn (Visualización Estadística)
- Estilo de gráficos
- `pairplot()`, `heatmap()`
- Integración con Pandas

---

## MÓDULO 10: CÁLCULO DIFERENCIAL E INTEGRACIÓN

### 10.1 Derivadas
- Concepto de derivada
- Derivada numérica
- Aplicaciones: tasas de cambio

### 10.2 Funciones Matemáticas
- Función lineal: $f(x) = mx + b$
- Función cuadrática: $f(x) = ax^2 + bx + c$
- Función cúbica: $f(x) = ax^3 + bx^2 + cx + d$
- Funciones trigonométricas
- Función exponencial

### 10.3 Optimización
- Descenso del gradiente
- Función Rosenbrock
- Algoritmos de optimización
- Learning rate (tasa de aprendizaje)

### 10.4 Matrices y Álgebra Lineal
- Operaciones con matrices
- Multiplicación de matrices
- Inversa y determinante
- Valores y vectores propios

---

## MÓDULO 11: MACHINE LEARNING BASICS

### 11.1 Conceptos Fundamentales
- Qué es Machine Learning
- Tipos de aprendizaje:
  - Supervisado
  - No supervisado
  - Por refuerzo
- Train-test split
- Validación cruzada

### 11.2 Regresión Lineal
- Ecuación de regresión lineal
- Método de mínimos cuadrados
- Cálculo manual vs sklearn
- Interpretación de coeficientes
- Predicción de nuevos valores

### 11.3 Regresión Múltiple
- Múltiples características
- Normalización de datos
- Multicolinealidad

### 11.4 Evaluación de Modelos
- **Métricas de Regresión**:
  - MSE (Error Cuadrático Medio)
  - RMSE (Raíz del ECM)
  - MAE (Error Absoluto Medio)
  - R² (Coeficiente de determinación)
- Matriz de confusión
- Curva ROC

### 11.5 Clasificación
- Regresión Logística
- Clasificación binaria
- Clasificación multiclase
- Probabilidades de predicción

---

## MÓDULO 12: FUNCIONES DE ACTIVACIÓN

### 12.1 Sigmoid
- Definición matemática: $\sigma(x) = \frac{1}{1 + e^{-x}}$
- Rango de salida: [0, 1]
- Casos de uso: clasificación binaria

### 12.2 Tanh (Tangente Hiperbólica)
- Definición: $tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}$
- Rango de salida: [-1, 1]
- Ventajas sobre Sigmoid

### 12.3 ReLU (Rectified Linear Unit)
- Definición: $ReLU(x) = max(0, x)$
- Características
- Variantes: Leaky ReLU, ELU

### 12.4 Softmax
- Para salidas multiclase
- Conversión a probabilidades

### 12.5 Otras Funciones
- Softplus
- Softsign
- Comparación y selección

---

## MÓDULO 13: REDES NEURONALES INTRODUCCIÓN

### 13.1 Conceptos Básicos
- Neurona artificial
- Pesos y sesgos
- Forward propagation
- Backward propagation

### 13.2 Arquitectura
- Capas de entrada, ocultas y salida
- Unidades por capa
- Conexiones

### 13.3 Entrenamiento
- Epochs e iteraciones
- Batch size
- Learning rate
- Funciones de pérdida

### 13.4 Frameworks
- Introducción a TensorFlow/Keras
- Introducción a PyTorch

---

## MÓDULO 14: DATASETS Y CASOS DE ESTUDIO

### 14.1 Dataset Iris
- Características
- Exploración
- Clasificación con Logistic Regression
- Visualización de límites de decisión

### 14.2 Dataset Custom
- Creación de datasets basados en ingreso-horas
- Análisis exploratorio
- Modelado
- Evaluación

### 14.3 Fuentes de Datos
- UCI Machine Learning Repository
- Kaggle
- Generación sintética con sklearn

---

## MÓDULO 15: BUENAS PRÁCTICAS

### 15.1 Estilo de Código
- PEP 8 - Guía de estilo Python
- Nomenclatura de variables
- Longitud de líneas
- Imports

### 15.2 Documentación
- Docstrings
- Comentarios efectivos
- Type hints

### 15.3 Testing
- Unit tests
- Testing frameworks
- Integración continua

### 15.4 Debugging
- Debugging con pdb
- Logging
- Mensajes de error claros

### 15.5 Rendimiento
- Profiling de código
- Optimización
- Memory management

---

## APÉNDICES

### A. Atajos de Teclado VS Code
### B. Recursos Adicionales
### C. Ejercicios Prácticos
### D. Glosario de Términos
### E. Bibliografía y Referencias

## Introducción

Python se ha consolidado como uno de los lenguajes de programación más utilizados en el ámbito de la investigación científica. Su sintaxis clara, su naturaleza de código abierto y un ecosistema de bibliotecas especializadas lo convierten en una herramienta fundamental para científicos, ingenieros y analistas de datos.

## Ventajas de Python en el Entorno Científico

- **Curva de aprendizaje accesible**: sintaxis legible que permite concentrarse en los problemas científicos más que en la complejidad del lenguaje.
- **Reproducibilidad**: los scripts y notebooks facilitan la documentación y replicación de experimentos.
- **Comunidad activa**: desarrollo continuo de herramientas y soporte en áreas especializadas.
- **Integración**: capacidad de interactuar con código en C, C++, Fortran y R.
- **Multiplataforma**: funciona en sistemas Windows, macOS y Linux sin modificaciones sustanciales.

## Ecosistema de Bibliotecas Esenciales

### Cálculo Numérico y Álgebra Lineal

- **NumPy**: proporciona arreglos multidimensionales eficientes y funciones matemáticas de alto rendimiento. Es la base para la mayoría de las bibliotecas científicas en Python.
- **SciPy**: construida sobre NumPy, ofrece módulos para optimización, integración, interpolación, procesamiento de señales, álgebra lineal y estadística.

### Visualización de Datos

- **Matplotlib**: biblioteca fundamental para generar gráficos estáticos, animados e interactivos con un control detallado sobre cada elemento.
- **Seaborn**: basada en Matplotlib, simplifica la creación de visualizaciones estadísticas complejas.
- **Plotly**: ideal para gráficos interactivos y dashboards, con soporte para visualizaciones en 3D.

### Análisis y Manipulación de Datos

- **Pandas**: estructura de datos en forma de DataFrames que permite manipular, limpiar y transformar conjuntos de datos tabulares con facilidad.
- **Xarray**: diseñada para trabajar con datos multidimensionales etiquetados, común en ciencias de la tierra y física.

### Aprendizaje Automático

- **Scikit-learn**: ofrece implementaciones consistentes y bien documentadas de algoritmos de clasificación, regresión, agrupamiento y reducción de dimensionalidad.
- **TensorFlow y PyTorch**: frameworks dominantes para aprendizaje profundo, con soporte para GPU y amplias comunidades de investigación.

### Computación Científica Avanzada

- **SymPy**: permite realizar álgebra simbólica, derivación, integración y resolución de ecuaciones de forma analítica.
- **Jupyter Notebook / JupyterLab**: entorno interactivo que combina código, visualizaciones, ecuaciones y texto explicativo en un mismo documento.

## Ejemplo Práctico

A continuación se muestra un ejemplo mínimo que integra varias de las bibliotecas mencionadas:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression

# Generar datos sintéticos
np.random.seed(42)
x = np.linspace(0, 10, 100)
y = 2.5 * x + np.random.normal(0, 2, 100)

# Crear DataFrame
df = pd.DataFrame({'x': x, 'y': y})

# Ajustar modelo lineal
modelo = LinearRegression()
modelo.fit(df[['x']], df['y'])

# Visualizar resultados
plt.figure(figsize=(8, 5))
plt.scatter(df['x'], df['y'], alpha=0.6, label='Datos')
plt.plot(df['x'], modelo.predict(df[['x']]), color='red', label='Ajuste lineal')
plt.xlabel('Variable independiente (x)')
plt.ylabel('Variable dependiente (y)')
plt.title('Regresión lineal con Python')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()

print(f"Pendiente estimada: {modelo.coef_[0]:.3f}")
print(f"Intersección estimada: {modelo.intercept_:.3f}")
