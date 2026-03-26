# MÓDULO 6: BIBLIOTECAS ESTÁNDAR
## Herramientas Integradas para la Ciencia Computacional

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Importar y utilizar módulos de la biblioteca estándar de Python
2. Realizar operaciones matemáticas avanzadas con el módulo math
3. Generar números aleatorios para simulaciones científicas
4. Manejar fechas y tiempos en experimentos de larga duración
5. Interactuar con el sistema operativo para gestión de archivos
6. Procesar archivos en formatos JSON y CSV para intercambio de datos

---

## 6.1 Módulos y Paquetes

### Concepto: Organización del Código Científico

En proyectos científicos complejos, es esencial organizar el código en **módulos** (archivos .py) y **paquetes** (directorios con módulos). La biblioteca estándar de Python proporciona cientos de módulos listos para usar en investigación científica.

### Importación de Módulos

```python
# Ejemplo: Análisis estadístico básico usando múltiples módulos

# Diferentes formas de importar módulos
import math                    # Importar todo el módulo
import statistics as stats     # Importar con alias
from random import randint     # Importar función específica
from datetime import datetime, timedelta  # Importar múltiples clases
import os, sys                 # Múltiples importaciones en una línea
import json                    # Para manejo de datos JSON
import csv                     # Para archivos CSV

print("MÓDULOS IMPORTADOS EXITOSAMENTE")
print("=" * 50)
print(f"math version: {math.__version__ if hasattr(math, '__version__') else 'N/A'}")
print(f"statistics version: {stats.__version__ if hasattr(stats, '__version__') else 'N/A'}")
print(f"datetime disponible: {datetime.now()}")
print(f"Directorio actual: {os.getcwd()}")
```

### Estructura de un Proyecto Científico

```
proyecto_cientifico/
├── main.py                    # Punto de entrada principal
├── config.py                  # Configuraciones del proyecto
├── requirements.txt           # Dependencias
├── data/                      # Datos del experimento
│   ├── raw/                  # Datos crudos
│   ├── processed/            # Datos procesados
│   └── results/              # Resultados finales
├── src/                      # Código fuente
│   ├── __init__.py           # Hace que src sea un paquete
│   ├── analysis/             # Análisis de datos
│   │   ├── __init__.py
│   │   ├── statistical.py
│   │   └── visualization.py
│   ├── experiments/          # Experimentos
│   │   ├── __init__.py
│   │   ├── protocol.py
│   │   └── simulation.py
│   └── utils/                # Utilidades
│       ├── __init__.py
│       ├── file_handling.py
│       └── validation.py
└── tests/                    # Pruebas unitarias
    ├── __init__.py
    ├── test_analysis.py
    └── test_experiments.py
```

### Importación Relativa vs Absoluta

```python
# Ejemplo de estructura de importaciones en un proyecto científico

# En src/analysis/statistical.py
"""
Módulo para análisis estadístico.
"""

# Importaciones absolutas (recomendadas)
import math
import statistics
from datetime import datetime

# Importaciones relativas dentro del mismo paquete
from . import visualization  # Mismo nivel
from ..utils import validation  # Un nivel arriba

# En main.py
"""
Punto de entrada principal del proyecto.
"""

# Importaciones desde paquetes
from src.analysis import statistical
from src.experiments import protocol
from src.utils import file_handling

# Uso de los módulos importados
data = [1.2, 2.3, 3.4, 4.5, 5.6]
mean = statistical.calculate_mean(data)
print(f"Media calculada: {mean}")
```

---

## 6.2 Módulos Útiles para Ciencia

### math: Operaciones Matemáticas

```python
import math

def analisis_matematico_cientifico():
    """
    Demuestra el uso del módulo math para cálculos científicos.
    """
    
    print("MÓDULO MATH - OPERACIONES MATEMÁTICAS CIENTÍFICAS")
    print("=" * 70)
    
    # 1. Constantes matemáticas fundamentales
    print("CONSTANTES MATEMÁTICAS:")
    print(f"π (pi) = {math.pi:.10f}")
    print(f"e (número de Euler) = {math.e:.10f}")
    print(f"τ (tau) = {math.tau:.10f}")
    print(f"∞ (infinito) = {math.inf}")
    print(f"NaN (Not a Number) = {math.nan}")
    
    # 2. Funciones trigonométricas (ángulos en radianes)
    print("\nFUNCIONES TRIGONOMÉTRICAS (ángulo = π/4 rad = 45°):")
    angulo = math.pi / 4
    print(f"sin({angulo:.3f}) = {math.sin(angulo):.6f}")
    print(f"cos({angulo:.3f}) = {math.cos(angulo):.6f}")
    print(f"tan({angulo:.3f}) = {math.tan(angulo):.6f}")
    
    # Funciones inversas
    print(f"asin(0.707) = {math.asin(0.707):.6f} rad")
    print(f"acos(0.707) = {math.acos(0.707):.6f} rad")
    print(f"atan(1) = {math.atan(1):.6f} rad")
    
    # 3. Funciones exponenciales y logarítmicas
    print("\nFUNCIONES EXPONENCIALES Y LOGARÍTMICAS:")
    print(f"exp(2) = e² = {math.exp(2):.6f}")
    print(f"log(100) (base e) = {math.log(100):.6f}")
    print(f"log10(100) (base 10) = {math.log10(100):.6f}")
    print(f"log2(256) (base 2) = {math.log2(256):.6f}")
    
    # 4. Funciones de potencia y raíz
    print("\nFUNCIONES DE POTENCIA Y RAÍZ:")
    print(f"2³ = {math.pow(2, 3):.1f}")
    print(f"√16 = {math.sqrt(16):.1f}")
    print(f"∛27 = {math.pow(27, 1/3):.1f}")
    print(f"hypot(3, 4) = √(3² + 4²) = {math.hypot(3, 4):.1f}")
    
    # 5. Funciones de redondeo y valor absoluto
    print("\nFUNCIONES DE REDONDEO:")
    valores = [3.14159, 2.71828, -1.41421]
    for val in valores:
        print(f"  {val:8.5f} -> floor: {math.floor(val):6}, ceil: {math.ceil(val):6}, trunc: {math.trunc(val):6}")
    
    print(f"\nValor absoluto de -5.5: {math.fabs(-5.5):.1f}")
    
    # 6. Funciones especiales para ciencia
    print("\nFUNCIONES ESPECIALES PARA CIENCIA:")
    print(f"Gamma(5) = 4! = {math.gamma(5):.1f}")
    print(f"Factorial(5) = {math.factorial(5)}")
    print(f"Combinaciones C(10,3) = {math.comb(10, 3)}")
    print(f"Permutaciones P(10,3) = {math.perm(10, 3)}")
    
    # 7. Conversión de ángulos
    print("\nCONVERSIÓN DE ÁNGULOS:")
    grados = 45
    radianes = math.radians(grados)
    print(f"{grados}° = {radianes:.6f} rad")
    print(f"{radianes:.6f} rad = {math.degrees(radianes):.6f}°")
    
    # 8. Funciones hiperbólicas
    print("\nFUNCIONES HIPERBÓLICAS:")
    x = 1.0
    print(f"sinh({x}) = {math.sinh(x):.6f}")
    print(f"cosh({x}) = {math.cosh(x):.6f}")
    print(f"tanh({x}) = {math.tanh(x):.6f}")

# Ejemplo aplicado: Cálculo de pH
def calcular_ph(concentracion_h):
    """
    Calcula el pH a partir de la concentración de H⁺.
    
    pH = -log₁₀([H⁺])
    """
    if concentracion_h <= 0:
        raise ValueError("La concentración de H⁺ debe ser positiva")
    
    ph = -math.log10(concentracion_h)
    return ph

# Ejemplo aplicado: Ley de los gases ideales
def ley_gases_ideales(presion, volumen, temperatura, constante_r=0.0821):
    """
    Calcula el número de moles usando PV = nRT.
    
    Parámetros:
    -----------
    presion : float
        Presión en atm
    volumen : float
        Volumen en litros
    temperatura : float
        Temperatura en Kelvin
    constante_r : float, opcional
        Constante de los gases (default=0.0821 L·atm/(mol·K))
    
    Retorna:
    --------
    float
        Número de moles
    """
    if temperatura <= 0:
        raise ValueError("La temperatura debe ser mayor que 0 K")
    
    moles = (presion * volumen) / (constante_r * temperatura)
    return moles

# Ejecutar demostración
analisis_matematico_cientifico()

print("\n" + "=" * 70)
print("EJEMPLOS APLICADOS")
print("=" * 70)

# Cálculo de pH
concentraciones = [1e-7, 1e-3, 1e-1, 1e-14]
print("\nCÁLCULO DE pH:")
for conc in concentraciones:
    ph = calcular_ph(conc)
    print(f"[H⁺] = {conc:.1e} M -> pH = {ph:.2f}")

# Ley de gases ideales
print("\nLEY DE GASES IDEALES:")
condiciones = [
    (1.0, 22.4, 273.15),  # Condiciones estándar
    (2.0, 10.0, 298.15),  # Presión doble
    (0.5, 30.0, 310.15),  # Temperatura corporal
]

for P, V, T in condiciones:
    n = ley_gases_ideales(P, V, T)
    print(f"P={P} atm, V={V} L, T={T} K -> n={n:.3f} moles")
```

### random: Generación de Números Aleatorios

```python
import random
import math
import statistics

def simulaciones_cientificas_con_random():
    """
    Demuestra el uso del módulo random para simulaciones científicas.
    """
    
    print("MÓDULO RANDOM - SIMULACIONES CIENTÍFICAS")
    print("=" * 70)
    
    # 1. Semilla para reproducibilidad (esencial en ciencia)
    random.seed(42)  # Semilla fija para resultados reproducibles
    print("Semilla establecida: 42 (para reproducibilidad)")
    
    # 2. Números aleatorios básicos
    print("\nNÚMEROS ALEATORIOS BÁSICOS:")
    print(f"Random float [0,1): {random.random():.6f}")
    print(f"Random float [1.5, 4.5): {random.uniform(1.5, 4.5):.6f}")
    print(f"Random int [1, 10]: {random.randint(1, 10)}")
    
    # 3. Distribuciones de probabilidad
    print("\nDISTRIBUCIONES DE PROBABILIDAD:")
    
    # Distribución normal (Gaussiana)
    media, desviacion = 100, 15
    muestras_normales = [random.gauss(media, desviacion) for _ in range(5)]
    print(f"Normal(μ={media}, σ={desviacion}): {[f'{x:.1f}' for x in muestras_normales]}")
    
    # Distribución exponencial (tiempos entre eventos)
    tasa = 0.5  # λ = 0.5 eventos por unidad de tiempo
    muestras_exp = [random.expovariate(tasa) for _ in range(5)]
    print(f"Exponencial(λ={tasa}): {[f'{x:.3f}' for x in muestras_exp]}")
    
    # Distribución triangular (valores con moda)
    low, high, mode = 0, 10, 7
    muestras_tri = [random.triangular(low, high, mode) for _ in range(5)]
    print(f"Triangular({low}, {high}, {mode}): {[f'{x:.3f}' for x in muestras_tri]}")
    
    # 4. Muestreo de poblaciones
    print("\nMUESTREO DE POBLACIONES:")
    
    # Población de valores
    poblacion = list(range(1, 101))  # Números del 1 al 100
    
    # Muestra aleatoria simple
    muestra_simple = random.sample(poblacion, 10)
    print(f"Muestra aleatoria simple (n=10): {muestra_simple}")
    
    # Muestreo con reemplazo
    muestra_con_reemplazo = [random.choice(poblacion) for _ in range(10)]
    print(f"Muestra con reemplazo (n=10): {muestra_con_reemplazo}")
    
    # Barajar (shuffle) - modifica la lista original
    lista_original = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    lista_copia = lista_original.copy()
    random.shuffle(lista_copia)
    print(f"Original: {lista_original}")
    print(f"Barajada: {lista_copia}")
    
    return muestras_normales

def simulacion_monte_carlo_pi(num_muestras=10000):
    """
    Simulación de Monte Carlo para estimar π.
    
    Método:
    1. Generar puntos aleatorios en un cuadrado [0,1] x [0,1]
    2. Contar puntos dentro del círculo unitario (x² + y² ≤ 1)
    3. π ≈ 4 * (puntos_dentro / total_puntos)
    """
    print("\n" + "=" * 70)
    print("SIMULACIÓN DE MONTE CARLO PARA ESTIMAR π")
    print("=" * 70)
    
    puntos_dentro = 0
    historial_estimaciones = []
    
    for i in range(1, num_muestras + 1):
        # Generar punto aleatorio
        x = random.random()
        y = random.random()
        
        # Verificar si está dentro del círculo
        if x**2 + y**2 <= 1:
            puntos_dentro += 1
        
        # Calcular estimación cada 1000 puntos
        if i % 1000 == 0:
            pi_estimado = 4 * puntos_dentro / i
            error = abs(pi_estimado - math.pi)
            historial_estimaciones.append(pi_estimado)
            
            print(f"Muestras: {i:6d} | π estimado: {pi_estimado:.8f} | Error: {error:.8f}")
    
    # Resultado final
    pi_final = 4 * puntos_dentro / num_muestras
    error_final = abs(pi_final - math.pi)
    
    print("\nRESULTADO FINAL:")
    print(f"π real: {math.pi:.10f}")
    print(f"π estimado: {pi_final:.10f}")
    print(f"Error absoluto: {error_final:.10f}")
    print(f"Error relativo: {(error_final/math.pi*100):.4f}%")
    
    return pi_final, error_final, historial_estimaciones

def simulacion_decaimiento_radioactivo(nucleos_iniciales=1000, constante_decaimiento=0.1, pasos_tiempo=50):
    """
    Simula el decaimiento radioactivo usando el método de Monte Carlo.
    
    En cada paso de tiempo, cada núcleo tiene probabilidad
    p = 1 - exp(-λΔt) de decaer.
    """
    print("\n" + "=" * 70)
    print("SIM