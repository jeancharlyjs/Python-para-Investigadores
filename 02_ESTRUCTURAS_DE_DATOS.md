# MÓDULO 2: ESTRUCTURAS DE DATOS COLECTORAS
## Organizando Información Científica

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Comprender las diferentes estructuras de datos colectoras en Python
2. Seleccionar la estructura adecuada para diferentes tipos de datos científicos
3. Manipular listas, tuplas, diccionarios y conjuntos eficientemente
4. Aplicar comprensiones de listas y diccionarios para procesamiento científico
5. Diferenciar entre listas y arreglos NumPy para cálculos numéricos

---

## 2.1 Listas

### Concepto: ¿Qué es una Lista en Ciencia?

Una lista en Python es una **colección ordenada y mutable** de elementos. En términos científicos, es como un **tubo de ensayo múltiple** o una **placa de microtitulación** donde puedes almacenar múltiples muestras en orden.

```python
# Ejemplo: Lista de temperaturas de un experimento
temperaturas = [22.5, 23.1, 21.8, 24.3, 22.9]
print(f"Temperaturas registradas: {temperaturas}")
print(f"Número de mediciones: {len(temperaturas)}")
```

### Creación y Características de Listas

```python
# Diferentes formas de crear listas científicas

# 1. Lista vacía (para llenar con datos experimentales)
muestras_vacias = []
datos_experimentales = list()

# 2. Lista con datos iniciales
concentraciones = [0.1, 0.2, 0.3, 0.4, 0.5]  # Concentraciones en M
nombres_reactivos = ["HCl", "NaOH", "NaCl", "H2SO4", "KOH"]

# 3. Lista con tipos mixtos (común en datos experimentales)
registro_experimento = ["Experimento #1", 25.5, True, 0.1, "NaOH"]
# Contiene: string, float, boolean, float, string

# 4. Lista anidada (matriz de datos)
datos_completos = [
    ["Muestra", "pH", "Temperatura", "Conductividad"],
    ["A1", 7.2, 25.0, 1.2],
    ["A2", 7.3, 25.1, 1.3],
    ["A3", 7.1, 24.9, 1.1]
]
```

### Indexación y Slicing

```python
# Ejemplo científico: Análisis de series temporales
# Datos de temperatura cada hora durante 24 horas
temperaturas_24h = [
    22.5, 22.3, 22.0, 21.8, 21.5, 21.0,  # 00:00 - 05:00
    20.8, 21.0, 21.5, 22.0, 23.0, 24.5,  # 06:00 - 11:00
    26.0, 27.5, 28.0, 27.8, 27.0, 26.5,  # 12:00 - 17:00
    25.0, 24.0, 23.5, 23.0, 22.8, 22.5   # 18:00 - 23:00
]

# Indexación básica (empezando en 0)
temperatura_medianoche = temperaturas_24h[0]      # 22.5°C (00:00)
temperatura_mediodia = temperaturas_24h[12]       # 26.0°C (12:00)
temperatura_ultima = temperaturas_24h[-1]         # 22.5°C (23:00)

# Slicing (rebanadas) para análisis por períodos
temperaturas_noche = temperaturas_24h[0:6]        # 00:00 - 05:00
temperaturas_manana = temperaturas_24h[6:12]      # 06:00 - 11:00
temperaturas_tarde = temperaturas_24h[12:18]      # 12:00 - 17:00
temperaturas_noche2 = temperaturas_24h[18:]       # 18:00 - 23:00

print(f"Temperatura a medianoche: {temperatura_medianoche}°C")
print(f"Temperatura al mediodia: {temperatura_mediodia}°C")
print(f"Temperaturas de la mañana: {temperaturas_manana}")
```

### Métodos de Listas para Análisis Científico

```python
# Ejemplo: Procesamiento de datos experimentales

# Datos crudos de un experimento (valores de absorbancia)
absorbancia_cruda = [0.423, 0.512, 0.398, 0.467, 0.512, 0.423]

# 1. append() - Añadir nueva medición
absorbancia_cruda.append(0.489)
print(f"Después de append: {absorbancia_cruda}")

# 2. extend() - Añadir múltiples mediciones
nuevas_mediciones = [0.501, 0.476]
absorbancia_cruda.extend(nuevas_mediciones)
print(f"Después de extend: {absorbancia_cruda}")

# 3. insert() - Insertar medición en posición específica
# Insertar valor de calibración al inicio
absorbancia_cruda.insert(0, 0.000)  # Blanco
print(f"Después de insert: {absorbancia_cruda}")

# 4. remove() - Eliminar valor específico (primera ocurrencia)
absorbancia_cruda.remove(0.512)  # Elimina el primer 0.512
print(f"Después de remove: {absorbancia_cruda}")

# 5. pop() - Eliminar por índice y obtener el valor
valor_eliminado = absorbancia_cruda.pop(2)  # Elimina índice 2
print(f"Valor eliminado: {valor_eliminado}")
print(f"Después de pop: {absorbancia_cruda}")

# 6. sort() - Ordenar datos (importante para análisis)
absorbancia_cruda.sort()
print(f"Datos ordenados: {absorbancia_cruda}")

# 7. reverse() - Invertir orden
absorbancia_cruda.reverse()
print(f"Datos invertidos: {absorbancia_cruda}")

# 8. count() - Contar ocurrencias (útil para estadística)
conteo_0423 = absorbancia_cruda.count(0.423)
print(f"El valor 0.423 aparece {conteo_0423} veces")

# 9. index() - Encontrar posición de un valor
posicion = absorbancia_cruda.index(0.467)
print(f"El valor 0.467 está en la posición {posicion}")

# 10. copy() - Crear copia para análisis independiente
copia_absorbancia = absorbancia_cruda.copy()
copia_absorbancia.append(0.600)
print(f"Original: {absorbancia_cruda}")
print(f"Copia modificada: {copia_absorbancia}")
```

### Iteración sobre Listas

```python
# Ejemplo: Procesamiento de datos de espectrofotometría

# Datos: longitud de onda (nm) y absorbancia
longitud_onda = [400, 450, 500, 550, 600, 650, 700]
absorbancia = [0.12, 0.45, 0.78, 0.92, 0.85, 0.60, 0.35]

print("ESPECTRO DE ABSORBANCIA")
print("=" * 40)
print("Longitud (nm) | Absorbancia")
print("-" * 40)

# Iteración básica con for
for i in range(len(longitud_onda)):
    print(f"{longitud_onda[i]:12} | {absorbancia[i]:.3f}")

# Encontrar máxima absorbancia (pico espectral)
max_absorbancia = max(absorbancia)
indice_max = absorbancia.index(max_absorbancia)
longitud_max = longitud_onda[indice_max]

print("-" * 40)
print(f"Pico máximo: {max_absorbancia:.3f} a {longitud_max} nm")
```

### List Comprehensions (Comprensiones de Lista)

```python
# Ejemplo: Transformación de datos científicos

# 1. Conversión de temperaturas de °C a °K
temperaturas_celsius = [0, 10, 20, 30, 40, 50]
temperaturas_kelvin = [c + 273.15 for c in temperaturas_celsius]

print(f"Celsius: {temperaturas_celsius}")
print(f"Kelvin:  {[round(k, 2) for k in temperaturas_kelvin]}")

# 2. Filtrar valores anómalos (outliers)
lecturas_presion = [1013, 1015, 1020, 950, 1018, 1012, 1100, 1014]
# Eliminar valores fuera de 1000-1030 hPa
presiones_validas = [p for p in lecturas_presion if 1000 <= p <= 1030]

print(f"Lecturas crudas: {lecturas_presion}")
print(f"Lecturas válidas: {presiones_validas}")

# 3. Cálculo de concentraciones a partir de absorbancia
# Ley de Beer-Lambert: C = A / (ε * l)
absorbancia_muestras = [0.25, 0.38, 0.42, 0.31, 0.29]
coeficiente_extincion = 1500  # M^-1 cm^-1
longitud_celda = 1.0  # cm

concentraciones = [a / (coeficiente_extincion * longitud_celda) 
                   for a in absorbancia_muestras]

print(f"Absorbancia: {absorbancia_muestras}")
print(f"Concentraciones (M): {[f'{c:.6f}' for c in concentraciones]}")

# 4. List comprehension anidada (matriz de datos)
# Crear matriz de diluciones (filas: muestras, columnas: réplicas)
num_muestras = 3
num_replicas = 4

matriz_diluciones = [[f"M{i+1}R{j+1}" for j in range(num_replicas)] 
                     for i in range(num_muestras)]

print("Matriz de diluciones:")
for fila in matriz_diluciones:
    print(f"  {fila}")
```

---

## 2.2 Tuplas

### Concepto: ¿Qué es una Tupla en Ciencia?

Una tupla es una **colección ordenada e inmutable** de elementos. En ciencia, es ideal para representar datos que no deben cambiar, como **coordenadas espaciales**, **parámetros constantes** o **configuraciones experimentales fijas**.

```python
# Ejemplo: Coordenadas de un punto en el espacio 3D
punto_3d = (10.5, 20.3, 5.7)  # (x, y, z) en metros
print(f"Coordenadas del punto: {punto_3d}")
print(f"Coordenada X: {punto_3d[0]}")
print(f"Coordenada Y: {punto_3d[1]}")
print(f"Coordenada Z: {punto_3d[2]}")
```

### Creación y Características de Tuplas

```python
# Diferentes formas de crear tuplas científicas

# 1. Tupla vacía (poco común, pero posible)
tupla_vacia = ()

# 2. Tupla con un elemento (¡atención a la coma!)
constante_unica = (3.14159,)  # La coma es necesaria
sin_comma = (3.14159)         # Esto es un float, NO una tupla

print(f"Tupla con un elemento: {constante_unica}, tipo: {type(constante_unica)}")
print(f"Sin coma: {sin_comma}, tipo: {type(sin_comma)}")

# 3. Tupla con múltiples elementos
parametros_experimento = ("Experimento #15", 25.0, 7.0, 60, True)
# Nombre, temperatura, pH, tiempo, agitación

# 4. Tupla sin paréntesis (packing implícito)
coordenadas = 10.5, 20.3, 5.7  # Python interpreta como tupla
print(f"Coordenadas sin paréntesis: {coordenadas}")

# 5. Tupla a partir de una lista
lista_parametros = [0.1, 0.01, 100]
tupla_parametros = tuple(lista_parametros)
print(f"Tupla desde lista: {tupla_parametros}")
```

### Desempaquetado de Tuplas (Unpacking)

```python
# Ejemplo: Análisis de resultados experimentales

# Resultados de un experimento: (media, desviación, n)
resultados = (24.8, 1.2, 10)  # media, desviación estándar, n

# Desempaquetado tradicional
media = resultados[0]
desviacion = resultados[1]
n_muestras = resultados[2]

# Desempaquetado elegante (Pythonic way)
media, desviacion, n_muestras = resultados

print(f"Media: {media} ± {desviacion} (n={n_muestras})")

# Ejemplo avanzado: Coordenadas esféricas
# (radio, ángulo polar, ángulo azimutal)
coordenada_esferica = (5.0, 0.78, 1.57)  # (r, θ, φ) en metros y radianes

radio, theta, phi = coordenada_esferica
print(f"Coordenadas esféricas: r={radio}m, θ={theta}rad, φ={phi}rad")

# Desempaquetado parcial (usando _ para ignorar valores)
datos_sensor = ("SENSOR-001", 25.5, 65.2, 1013.2, "2024-03-26")
id_sensor, temperatura, humedad, _, fecha = datos_sensor
# El _ ignora la presión (tercer elemento)

print(f"Sensor {id_sensor} a las {fecha}:")
print(f"  Temperatura: {temperatura}°C")
print(f"  Humedad: {humedad}%")
```

### Métodos Disponibles en Tuplas

```python
# Aunque las tuplas son inmutables, tienen algunos métodos útiles

# Datos constantes de un experimento
constantes = (3.14159, 2.71828, 6.626e-34, 1.380649e-23)

# 1. count() - Contar ocurrencias
conteo_pi = constantes.count(3.14159)
print(f"El valor pi aparece {conteo_pi} veces")

# 2. index() - Encontrar posición
posicion_h = constantes.index(6.626e-34)
print(f"La constante de Planck está en la posición {posicion_h}")

# 3. Concatenación de tuplas (crea nueva tupla)
constantes_matematicas = (3.14159, 2.71828)
constantes_fisicas = (6.626e-34, 1.380649e-23)
todas_constantes = constantes_matematicas + constantes_fisicas

print(f"Todas las constantes: {todas_constantes}")

# 4. Repetición (crea nueva tupla)
parametros_triplicados = ("CALIBRAR",) * 3
print(f"Parámetros triplicados: {parametros_triplicados}")
```

### Cuándo Usar Tuplas vs Listas

```python
# CASO 1: DATOS INMUTABLES - Usar TUPLA
# Coordenadas que no cambian
coordenadas_laboratorio = (40.7128, -74.0060)  # Nueva York
# ¡Error si intentas modificar!
# coordenadas_laboratorio[0] = 41.0  # TypeError

# CASO 2: DATOS MUTABLES - Usar LISTA
# Lecturas que se actualizan
lecturas_temperatura = [22.5, 23.1, 21.8]
lecturas_temperatura[0] = 22.7  # ¡Correcto!

# CASO 3: CLAVES DE DICCIONARIO - Usar TUPLA
# Las tuplas son hashable, las listas no
coordenadas_puntos = {
    (0, 0): "Origen",
    (1, 0): "Punto en eje X",
