# MÓDULO 7: NUMPY (NUMERICAL PYTHON)
## Computación Numérica Eficiente para Ciencia

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Crear y manipular arrays NumPy para datos científicos
2. Realizar operaciones matemáticas eficientes con arrays
3. Utilizar funciones universales (ufuncs) para cálculos vectorizados
4. Aplicar álgebra lineal para problemas científicos
5. Realizar operaciones estadísticas sobre arrays multidimensionales
6. Generar datos sintéticos para simulaciones científicas

---

## 7.1 Arrays de NumPy

### Concepto: ¿Por qué NumPy es Esencial para la Ciencia?

NumPy (Numerical Python) es la biblioteca fundamental para **computación científica en Python**. Proporciona:
- **Arrays multidimensionales** eficientes en memoria
- **Operaciones vectorizadas** (sin bucles explícitos)
- **Funciones matemáticas** optimizadas en C/Fortran
- **Interoperabilidad** con otras bibliotecas científicas

### Instalación y Configuración

```python
# Instalación de NumPy
# pip install numpy

# Verificación de instalación
import numpy as np

print("NUMPY PARA CIENCIA COMPUTACIONAL")
print("=" * 60)
print(f"NumPy versión: {np.__version__}")
print(f"Configuración: {np.show_config()}")
```

### Creación de Arrays

```python
import numpy as np

def demostracion_creacion_arrays():
    """
    Demuestra diferentes formas de crear arrays NumPy.
    """
    
    print("CREACIÓN DE ARRAYS NUMPY")
    print("=" * 70)
    
    # 1. Desde listas de Python (la forma más común)
    print("1. DESDE LISTAS DE PYTHON:")
    
    # Array 1D (vector)
    vector = np.array([1, 2, 3, 4, 5])
    print(f"  Vector 1D: {vector}")
    print(f"  Tipo: {vector.dtype}, Forma: {vector.shape}, Dimensiones: {vector.ndim}")
    
    # Array 2D (matriz)
    matriz = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
    print(f"\n  Matriz 2D:\n{matriz}")
    print(f"  Tipo: {matriz.dtype}, Forma: {matriz.shape}, Dimensiones: {matriz.ndim}")
    
    # Array 3D (tensor)
    tensor = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
    print(f"\n  Tensor 3D (shape {tensor.shape}):")
    print(tensor)
    
    # 2. Arrays con valores específicos
    print("\n2. ARRAYS CON VALORES ESPECÍFICOS:")
    
    # Ceros
    ceros_1d = np.zeros(5)
    ceros_2d = np.zeros((3, 4))
    print(f"  zeros(5): {ceros_1d}")
    print(f"  zeros((3,4)):\n{ceros_2d}")
    
    # Unos
    unos_1d = np.ones(5)
    unos_2d = np.ones((2, 3))
    print(f"\n  ones(5): {unos_1d}")
    print(f"  ones((2,3)):\n{unos_2d}")
    
    # Lleno con un valor específico
    lleno = np.full((3, 3), 7)
    print(f"\n  full((3,3), 7):\n{lleno}")
    
    # Matriz identidad
    identidad = np.eye(4)
    print(f"\n  eye(4) (matriz identidad):\n{identidad}")
    
    # 3. Arrays con patrones
    print("\n3. ARRAYS CON PATRONES:")
    
    # Rango (similar a range() pero devuelve array)
    rango = np.arange(0, 10, 2)  # start, stop, step
    print(f"  arange(0, 10, 2): {rango}")
    
    # Espaciado lineal
    lineal = np.linspace(0, 1, 5)  # start, stop, num_points
    print(f"  linspace(0, 1, 5): {lineal}")
    
    # Espaciado logarítmico
    logaritmico = np.logspace(0, 2, 5)  # 10^0 a 10^2, 5 puntos
    print(f"  logspace(0, 2, 5): {logaritmico}")
    
    # 4. Arrays aleatorios
    print("\n4. ARRAYS ALEATORIOS:")
    
    # Uniforme [0, 1)
    uniforme = np.random.rand(3, 3)
    print(f"  random.rand(3,3) (uniforme):\n{uniforme}")
    
    # Normal (Gaussiana)
    normal = np.random.randn(3, 3)  # μ=0, σ=1
    print(f"\n  random.randn(3,3) (normal estándar):\n{normal}")
    
    # Enteros aleatorios
    enteros = np.random.randint(0, 100, size=(3, 4))
    print(f"\n  random.randint(0, 100, (3,4)):\n{enteros}")
    
    # 5. Arrays con tipos de datos específicos
    print("\n5. TIPOS DE DATOS ESPECÍFICOS:")
    
    # Especificar dtype
    enteros_32 = np.array([1, 2, 3], dtype=np.int32)
    flotantes_64 = np.array([1.0, 2.0, 3.0], dtype=np.float64)
    complejos = np.array([1+2j, 3+4j], dtype=np.complex128)
    
    print(f"  int32: {enteros_32}, dtype: {enteros_32.dtype}")
    print(f"  float64: {flotantes_64}, dtype: {flotantes_64.dtype}")
    print(f"  complex128: {complejos}, dtype: {complejos.dtype}")
    
    # 6. Arrays desde datos existentes
    print("\n6. DESDE DATOS EXISTENTES:")
    
    # Copiar un array
    original = np.array([1, 2, 3])
    copia = np.copy(original)
    copia[0] = 99
    print(f"  Original: {original}, Copia modificada: {copia}")
    
    # Desde buffer (ejemplo: datos binarios)
    datos_bytes = bytes([1, 2, 3, 4, 5])
    desde_bytes = np.frombuffer(datos_bytes, dtype=np.uint8)
    print(f"  Desde bytes: {desde_bytes}")

# Ejecutar demostración
demostracion_creacion_arrays()
```

### Tipos de Datos (`dtype`)

```python
import numpy as np

def demostracion_tipos_datos():
    """
    Demuestra los diferentes tipos de datos en NumPy.
    """
    
    print("TIPOS DE DATOS (DTYPE) EN NUMPY")
    print("=" * 70)
    
    # Tipos de datos numéricos
    tipos_numericos = [
        (np.int8, "Entero de 8 bits con signo", [-128, 127]),
        (np.int16, "Entero de 16 bits con signo", [-32768, 32767]),
        (np.int32, "Entero de 32 bits con signo", [-2147483648, 2147483647]),
        (np.int64, "Entero de 64 bits con signo", [-9223372036854775808, 9223372036854775807]),
        (np.uint8, "Entero de 8 bits sin signo", [0, 255]),
        (np.uint16, "Entero de 16 bits sin signo", [0, 65535]),
        (np.uint32, "Entero de 32 bits sin signo", [0, 4294967295]),
        (np.uint64, "Entero de 64 bits sin signo", [0, 18446744073709551615]),
        (np.float16, "Flotante de 16 bits (media precisión)", "±65504"),
        (np.float32, "Flotante de 32 bits (precisión simple)", "±3.4e38"),
        (np.float64, "Flotante de 64 bits (precisión doble)", "±1.8e308"),
        (np.complex64, "Complejo de 64 bits", "2×float32"),
        (np.complex128, "Complejo de 128 bits", "2×float64"),
        (np.bool_, "Booleano", "[True, False]"),
    ]
    
    print("TIPOS NUMÉRICOS DISPONIBLES:")
    print("-" * 80)
    print(f"{'Tipo':<15} {'Descripción':<40} {'Rango/Valores':<30}")
    print("-" * 80)
    
    for tipo, descripcion, rango in tipos_numericos:
        print(f"{str(tipo):<15} {descripcion:<40} {str(rango):<30}")
    
    # Ejemplos prácticos
    print("\n" + "=" * 70)
    print("EJEMPLOS PRÁCTICOS DE USO DE DTYPES")
    print("=" * 70)
    
    # 1. Especificar dtype al crear arrays
    print("\n1. ESPECIFICAR DTYPE AL CREAR:")
    
    # Para imágenes (valores 0-255)
    imagen = np.array([0, 128, 255], dtype=np.uint8)
    print(f"  Imagen (uint8): {imagen}, dtype: {imagen.dtype}")
    
    # Para datos científicos de alta precisión
    datos_cientificos = np.array([3.141592653589793], dtype=np.float64)
    print(f"  Datos científicos (float64): {datos_cientificos}, dtype: {datos_cientificos.dtype}")
    
    # Para datos categóricos (booleanos)
    resultados = np.array([True, False, True], dtype=np.bool_)
    print(f"  Resultados (bool): {resultados}, dtype: {resultados.dtype}")
    
    # 2. Conversión entre tipos
    print("\n2. CONVERSIÓN ENTRE TIPOS:")
    
    enteros = np.array([1, 2, 3, 4, 5], dtype=np.int32)
    print(f"  Original (int32): {enteros}, dtype: {enteros.dtype}")
    
    # Conversión a float
    flotantes = enteros.astype(np.float64)
    print(f"  Convertido a float64: {flotantes}, dtype: {flotantes.dtype}")
    
    # Conversión a booleano (0=False, ≠0=True)
    booleanos = enteros.astype(np.bool_)
    print(f"  Convertido a bool: {booleanos}, dtype: {booleanos.dtype}")
    
    # 3. Verificación y manipulación de dtypes
    print("\n3. VERIFICACIÓN Y MANIPULACIÓN:")
    
    array_mixto = np.array([1, 2.5, 3+4j])
    print(f"  Array mixto: {array_mixto}")
    print(f"  dtype: {array_mixto.dtype}")  # NumPy elige el tipo más general
    
    # Verificar tipo específico
    print(f"  ¿Es complejo? {np.iscomplexobj(array_mixto)}")
    print(f"  ¿Es real? {np.isrealobj(array_mixto)}")
    print(f"  ¿Es entero? {np.issubdtype(array_mixto.dtype, np.integer)}")
    
    # 4. Dtypes para optimización de memoria
    print("\n4. OPTIMIZACIÓN DE MEMORIA:")
    
    # Comparación de tamaño en memoria
    array_int64 = np.ones(1000, dtype=np.int64)
    array_int32 = np.ones(1000, dtype=np.int32)
    array_float64 = np.ones(1000, dtype=np.float64)
    array_float32 = np.ones(1000, dtype=np.float32)
    
    print(f"  int64: {array_int64.nbytes} bytes")
    print(f"  int32: {array_int32.nbytes} bytes ({(array_int32.nbytes/array_int64.nbytes*100):.1f}% del int64)")
    print(f"  float64: {array_float64.nbytes} bytes")
    print(f"  float32: {array_float32.nbytes} bytes ({(array_float32.nbytes/array_float64.nbytes*100):.1f}% del float64)")
    
    # 5. Dtypes en operaciones
    print("\n5. DTYPES EN OPERACIONES:")
    
    a = np.array([1, 2, 3], dtype=np.int32)
    b = np.array([1.5, 2.5, 3.5], dtype=np.float64)
    
    # Suma de diferentes tipos
    suma = a + b
    print(f"  int32 + float64 = {suma}, dtype: {suma.dtype}")
    
    # Promoción de tipos (type casting)
    print(f"  Tipo resultante: {np.result_type(a.dtype, b.dtype)}")

# Ejecutar demostración
demostracion_tipos_datos()
```

### Dimensiones y Forma (`shape`, `ndim`)

```python
import numpy as np

def demostracion_dimensiones_forma():
    """
    Demuestra el manejo de dimensiones y forma en arrays NumPy.
    """
    
    print("DIMENSIONES Y FORMA EN ARRAYS NUMPY")
    print("=" * 70)
    
    # Crear arrays de diferentes dimensiones
    print("1. ARRAYS DE DIFERENTES DIMENSIONES:")
    
    # Escalar (0D)
    escalar = np.array(42)
    print(f"\n  Escalar (0D): {escalar}")
    print(f"    shape: {escalar.shape}, ndim: {escalar.ndim}")
    print(f"    size: {escalar.size} (elementos totales)")
    
    # Vector (1D)
    vector = np.array([1, 2, 3, 4, 5])
    print(f"\n  Vector (1D): {vector}")
    print(f"    shape: {vector.shape}, ndim: {vector.ndim}")
    print(f"    size: {vector.size}")
    print(f"    len: {len(vector)} (solo para 1D)")
    
    # Matriz (2D)
    matriz = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
    print(f"\n  Matriz (2D):\n{matriz}")
    print(f"    shape: {matriz.shape}, ndim: {matriz.ndim}")
    print(f"    size: {matriz.size}")
    
    # Tensor (3D)
    tensor = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
    print(f"\n  Tensor (3D) shape {tensor.shape}:")
    print(tensor)
    print(f"    shape: {tensor.shape}, ndim: {tensor.ndim}")
    print(f"    size: {tensor.size}")
    
    # 2. Manipulación de forma
    print("\n2. MANIPULACIÓN DE FORMA:")
    
    # Reshape (cambiar forma sin cambiar datos)
    vector_12 = np.arange(12)
    print(f"  Vector original (12 elementos): {vector_12}")
    
    # Reshape a 3x4
    matriz_3x4 = vector_12.reshape(3, 4)
    print(f"  Reshape a (3, 4):\n{matriz_3x4}")
    
    # Reshape a 2x3x2
    tensor_2x3x2 = vector_12.reshape(2, 3, 2)
    print(f"  Reshape a (2, 3, 2):\n{tensor_2x3x2}")
    
    # Reshape automático con -1
    auto_reshape = vector_12.reshape(3, -1)  # -1 calcula automáticamente
    print(f"  Reshape a (3, -1):\n{auto_reshape}")
    
    # 3. Aplanar arrays
    print("\n3. APLANAR ARRAYS:")
    
    matriz_ejemplo = np.array([[1, 2, 3], [4, 5, 6]])
    
    # flatten() - copia
    aplanado_copy = matriz_ejemplo.flatten()
    aplanado_copy[0] = 99
    print(f"  Original después de flatten() (copia):\n{matriz_ejemplo}")
    print(f"  Aplanado modific