# MÓDULO 8: PANDAS (ANÁLISIS DE DATOS)
## Manipulación y Análisis de Datos Tabulares

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Crear y manipular Series y DataFrames de pandas
2. Realizar operaciones de limpieza y preprocesamiento de datos
3. Filtrar, seleccionar y transformar datos eficientemente
4. Realizar análisis exploratorio de datos (EDA)
5. Agrupar y agregar datos para análisis estadístico
6. Leer y escribir datos en diferentes formatos (CSV, Excel, JSON, SQL)

---

## 8.1 Series

### Concepto: ¿Qué es una Serie en pandas?

Una **Serie** es una estructura de datos unidimensional etiquetada que puede contener cualquier tipo de datos. Es similar a una columna en una hoja de cálculo o a un array de NumPy con índices.

### Creación de Series

```python
import pandas as pd
import numpy as np

def demostracion_series():
    """
    Demuestra la creación y manipulación de Series en pandas.
    """
    
    print("SERIES EN PANDAS - DATOS UNIDIMENSIONALES")
    print("=" * 70)
    
    # 1. Creación de Series desde diferentes fuentes
    print("1. CREACIÓN DE SERIES:")
    
    # Desde una lista
    temperaturas = pd.Series([22.5, 23.1, 21.8, 24.3, 22.9])
    print(f"\n  Desde lista (índices automáticos):\n{temperaturas}")
    
    # Con índices personalizados
    temperaturas_nombres = pd.Series(
        [22.5, 23.1, 21.8, 24.3, 22.9],
        index=['Lunes', 'Martes', 'Miércoles', 'Jueves', 'Viernes']
    )
    print(f"\n  Con índices personalizados:\n{temperaturas_nombres}")
    
    # Desde un diccionario (las claves se convierten en índices)
    ph_muestras = pd.Series({
        'Muestra A': 7.2,
        'Muestra B': 6.8,
        'Muestra C': 7.5,
        'Muestra D': 7.0
    })
    print(f"\n  Desde diccionario:\n{ph_muestras}")
    
    # Desde un array de NumPy
    concentraciones = pd.Series(
        np.array([0.1, 0.2, 0.3, 0.4, 0.5]),
        index=['Dilución 1', 'Dilución 2', 'Dilución 3', 'Dilución 4', 'Dilución 5']
    )
    print(f"\n  Desde array NumPy:\n{concentraciones}")
    
    # 2. Atributos de una Serie
    print("\n2. ATRIBUTOS DE UNA SERIE:")
    
    serie_ejemplo = pd.Series([10, 20, 30, 40, 50], index=['A', 'B', 'C', 'D', 'E'])
    print(f"  Serie ejemplo:\n{serie_ejemplo}")
    print(f"\n  Atributos:")
    print(f"    Índices: {serie_ejemplo.index}")
    print(f"    Valores: {serie_ejemplo.values}")
    print(f"    dtype: {serie_ejemplo.dtype}")
    print(f"    shape: {serie_ejemplo.shape}")
    print(f"    size: {serie_ejemplo.size}")
    print(f"    name: {serie_ejemplo.name}")
    
    # Asignar nombre a la Serie
    serie_ejemplo.name = "Mediciones"
    print(f"    name (después): {serie_ejemplo.name}")
    
    # 3. Acceso a datos
    print("\n3. ACCESO A DATOS:")
    
    serie_datos = pd.Series([100, 200, 300, 400, 500], index=['a', 'b', 'c', 'd', 'e'])
    print(f"  Serie: {serie_datos}")
    
    # Por índice de posición
    print(f"  Por posición [0]: {serie_datos[0]}")
    print(f"  Por posición [-1]: {serie_datos[-1]}")
    print(f"  Por posición [1:4]:\n{serie_datos[1:4]}")
    
    # Por etiqueta de índice
    print(f"  Por etiqueta ['b']: {serie_datos['b']}")
    print(f"  Por etiqueta ['c':'e']:\n{serie_datos['c':'e']}")
    
    # Por lista de etiquetas
    print(f"  Por lista [['a', 'c', 'e']]:\n{serie_datos[['a', 'c', 'e']]}")
    
    # 4. Operaciones con Series
    print("\n4. OPERACIONES CON SERIES:")
    
    # Datos científicos de ejemplo
    absorbancia = pd.Series([0.12, 0.25, 0.38, 0.42, 0.31], 
                           index=['M1', 'M2', 'M3', 'M4', 'M5'])
    print(f"  Absorbancia original:\n{absorbancia}")
    
    # Operaciones escalares
    print(f"\n  Absorbancia × 2:\n{absorbancia * 2}")
    print(f"\n  Absorbancia + 0.1:\n{absorbancia + 0.1}")
    
    # Operaciones entre Series
    absorbancia2 = pd.Series([0.10, 0.22, 0.35, 0.40, 0.28], 
                            index=['M1', 'M2', 'M3', 'M4', 'M5'])
    print(f"\n  Diferencia entre mediciones:\n{absorbancia - absorbancia2}")
    
    # Funciones matemáticas
    print(f"\n  Logaritmo natural:\n{np.log(absorbancia)}")
    print(f"\n  Exponencial:\n{np.exp(absorbancia)}")
    
    # 5. Métodos estadísticos
    print("\n5. MÉTODOS ESTADÍSTICOS:")
    
    datos_estadisticos = pd.Series([23.5, 24.1, 22.8, 25.3, 23.9, 24.5, 22.1])
    print(f"  Datos: {datos_estadisticos.values}")
    
    print(f"  Media: {datos_estadisticos.mean():.2f}")
    print(f"  Mediana: {datos_estadisticos.median():.2f}")
    print(f"  Desviación estándar: {datos_estadisticos.std():.2f}")
    print(f"  Varianza: {datos_estadisticos.var():.2f}")
    print(f"  Mínimo: {datos_estadisticos.min():.2f}")
    print(f"  Máximo: {datos_estadisticos.max():.2f}")
    print(f"  Suma: {datos_estadisticos.sum():.2f}")
    print(f"  Cuantil 25%: {datos_estadisticos.quantile(0.25):.2f}")
    print(f"  Cuantil 75%: {datos_estadisticos.quantile(0.75):.2f}")
    
    # 6. Métodos útiles
    print("\n6. MÉTODOS ÚTILES:")
    
    serie_con_nulos = pd.Series([1, 2, None, 4, None, 6])
    print(f"  Serie con nulos:\n{serie_con_nulos}")
    
    print(f"  ¿Tiene nulos? {serie_con_nulos.isnull().any()}")
    print(f"  Número de nulos: {serie_con_nulos.isnull().sum()}")
    print(f"  Sin nulos:\n{serie_con_nulos.dropna()}")
    print(f"  Rellenar nulos con 0:\n{serie_con_nulos.fillna(0)}")
    
    # Ordenamiento
    serie_desordenada = pd.Series([5, 2, 8, 1, 9], index=['E', 'B', 'D', 'A', 'C'])
    print(f"\n  Serie desordenada:\n{serie_desordenada}")
    print(f"  Ordenada por valor:\n{serie_desordenada.sort_values()}")
    print(f"  Ordenada por índice:\n{serie_desordenada.sort_index()}")
    
    # Conteo de valores únicos
    serie_repetidos = pd.Series(['A', 'B', 'A', 'C', 'B', 'A', 'D'])
    print(f"\n  Serie con valores repetidos:\n{serie_repetidos}")
    print(f"  Valores únicos: {serie_repetidos.unique()}")
    print(f"  Conteo de valores:\n{serie_repetidos.value_counts()}")
    
    # 7. Aplicación de funciones
    print("\n7. APLICACIÓN DE FUNCIONES:")
    
    def clasificar_temperatura(temp):
        """Clasifica temperaturas en categorías."""
        if temp < 22:
            return 'Fría'
        elif temp < 25:
            return 'Templada'
        else:
            return 'Caliente'
    
    temps = pd.Series([21.5, 23.1, 24.8, 20.9, 25.5])
    categorias = temps.apply(clasificar_temperatura)
    print(f"  Temperaturas: {temps.values}")
    print(f"  Categorías: {categorias.values}")
    
    # Función lambda
    temps_fahrenheit = temps.apply(lambda x: x * 9/5 + 32)
    print(f"  Temperaturas en Fahrenheit: {temps_fahrenheit.values}")

# Ejecutar demostración
demostracion_series()
```

### Operaciones con Series

```python
import pandas as pd
import numpy as np

def operaciones_avanzadas_series():
    """
    Demuestra operaciones avanzadas con Series.
    """
    
    print("OPERACIONES AVANZADAS CON SERIES")
    print("=" * 70)
    
    # 1. Alineación automática por índice
    print("1. ALINEACIÓN AUTOMÁTICA POR ÍNDICE:")
    
    # Crear dos Series con índices parcialmente superpuestos
    serie1 = pd.Series([10, 20, 30], index=['A', 'B', 'C'])
    serie2 = pd.Series([40, 50, 60], index=['B', 'C', 'D'])
    
    print(f"  Serie 1:\n{serie1}")
    print(f"\n  Serie 2:\n{serie2}")
    
    # Suma con alineación automática
    suma = serie1 + serie2
    print(f"\n  Serie1 + Serie2 (con alineación):\n{suma}")
    print("  Nota: Los índices no coincidentes dan NaN")
    
    # 2. Operaciones con manejo de NaN
    print("\n2. MANEJO DE VALORES NULOS (NaN):")
    
    # Suma con fill_value
    suma_con_cero = serie1.add(serie2, fill_value=0)
    print(f"  Serie1 + Serie2 (rellenando con 0):\n{suma_con_cero}")
    
    # Operaciones con métodos que ignoran NaN
    print(f"\n  Suma ignorando NaN: {suma.sum(skipna=True)}")
    print(f"  Media ignorando NaN: {suma.mean(skipna=True)}")
    
    # 3. Operaciones vectorizadas complejas
    print("\n3. OPERACIONES VECTORIZADAS COMPLEJAS:")
    
    # Datos de un experimento: tiempo (s) y posición (m)
    tiempo = pd.Series(np.linspace(0, 10, 11), name='Tiempo')
    posicion = pd.Series(0.5 * 9.8 * tiempo**2, name='Posición')
    
    print(f"  Tiempo (s):\n{tiempo}")
    print(f"\n  Posición (m) = 0.5 * 9.8 * t²:\n{posicion}")
    
    # Calcular velocidad (derivada numérica)
    velocidad = posicion.diff() / tiempo.diff()
    velocidad.name = 'Velocidad'
    print(f"\n  Velocidad (m/s) = Δposición/Δt:\n{velocidad}")
    
    # Calcular aceleración (segunda derivada)
    aceleracion = velocidad.diff() / tiempo.diff()
    aceleracion.name = 'Aceleración'
    print(f"\n  Aceleración (m/s²) = Δvelocidad/Δt:\n{aceleracion}")
    
    # 4. Operaciones de ventana (rolling)
    print("\n4. OPERACIONES DE VENTANA (ROLLING):")
    
    # Datos con ruido
    np.random.seed(42)
    señal_ruidosa = pd.Series(
        np.sin(np.linspace(0, 4*np.pi, 50)) + np.random.normal(0, 0.2, 50),
        name='Señal ruidosa'
    )
    
    # Media móvil
    media_movil = señal_ruidosa.rolling(window=5).mean()
    media_movil.name = 'Media móvil (window=5)'
    
    print(f"  Señal original (primeros 10 valores):\n{señal_ruidosa.head(10)}")
    print(f"\n  Media móvil (primeros 10 valores):\n{media_movil.head(10)}")
    
    # Otras operaciones de ventana
    print(f"\n  Máximo móvil (window=3):\n{señal_ruidosa.rolling(window=3).max().head(10)}")
    print(f"\n  Suma móvil (window=4):\n{señal_ruidosa.rolling(window=4).sum().head(10)}")
    
    # 5. Operaciones acumulativas
    print("\n5. OPERACIONES ACUMULATIVAS:")
    
    crecimiento_bacteriano = pd.Series([100, 150, 225, 337, 506], 
                                      index=['Hora 0', 'Hora 1', 'Hora 2', 'Hora 3', 'Hora 4'])
    
    print(f"  Crecimiento bacteriano (UFC/mL):\n{crecimiento_bacteriano}")
    
    # Suma acumulativa
    suma_acum = crecimiento_bacteriano.cumsum()
    print(f"\n  Suma acumulativa:\n{suma_acum}")
    
    # Producto acumulativo
    producto_acum = crecimiento_bacteriano.cumprod()
    print(f"\n  Producto acumulativo:\n{producto_acum}")
    
    # Máximo acumulativo
    max_acum = crecimiento_bacteriano.cummax()
    print(f"\n  Máximo acumulativo:\n{max_acum}")
    
    # Mínimo acumulativo
    min_acum = crecimiento_bacteriano.cummin()
    print(f"\n  Mínimo acumulativo:\n{min_acum}")
    
    # 6. Operaciones de agrupación (groupby) en Series
    print("\n6. OPERACIONES DE AGRUPACIÓN:")
    
    # Serie con categorías
    datos_categorizados = pd.Series(
        [23.5, 24.1, 22.8, 25.3, 23.9, 24.5, 22.1, 25.8],
        index=pd.MultiIndex.from_tuples([
            ('Grupo A', 'Muestra 1'), ('Grupo A', 'Muestra 2'),
            ('Grupo A', 'Muestra 3'), ('Grupo A', 'Muestra 4'),
            ('Grupo B', 'Muestra 1'), ('Grupo B', 'Muestra 2'),
            ('Grupo B', 'Muestra 3'), ('Grupo B', 'Muestra 4')
        ])
    )
    
    print(f"  Datos con índice multi-nivel:\n{datos_categorizados}")
    
    # Agrupar por primer nivel del índice
    grupo_a = datos_categorizados.xs('Grupo A')
    grupo_b = datos_categorizados.xs('Grupo B')
    
    print(f"\n  Grupo A:\n{grupo_a}")
    print(f"  Media Grupo A: {grupo_a.mean():.2f}")
    
    print(f"\n  Grupo B:\n{grupo_b}")
    print(f"  Media Grupo B: {grupo_b.mean():.2f}")
    
    # 7. Operaciones de cadena (string) en Series
    print("\n7. OPERACIONES DE CADENA:")
    
    nombres_muestras = pd.Series([
        'Muestra_A_Control',
        'Muestra_B_Tratamiento',
        'Muestra_C_Control',
        'Muestra_D_Tratamiento',
        '