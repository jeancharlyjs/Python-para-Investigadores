# MÓDULO 1: FUNDAMENTOS DE PYTHON
## Tu Primera Herramienta Científica

## 🎯 **Objetivos de Aprendizaje**

Al finalizar este módulo, serás capaz de:
1. ✅ **Configurar** tu entorno científico de Python
2. ✅ **Comprender** los conceptos básicos de programación
3. ✅ **Manipular** diferentes tipos de datos científicos
4. ✅ **Realizar** operaciones matemáticas básicas
5. ✅ **Interactuar** con programas mediante entrada/salida

---

## 1.1 Introducción a Python

### 🧠 **Concepto: ¿Qué es Python y por qué es ideal para ciencia?**

**Python** es un lenguaje de programación de alto nivel que se ha convertido en el **estándar de facto para la investigación científica**. Pero ¿por qué?

**Analogía científica**: Si los lenguajes de programación fueran herramientas de laboratorio:
- **C/C++** sería un microscopio electrónico: potente pero complejo
- **Java** sería una centrífuga industrial: robusta pero pesada
- **Python** sería un **microscopio confocal moderno**: fácil de usar, versátil y potente

### 📊 **Ventajas de Python para Ciencia**

| Característica | Beneficio Científico | Ejemplo de Aplicación |
|---------------|---------------------|----------------------|
| **Sintaxis simple** | Menos tiempo codificando, más tiempo investigando | Análisis rápido de datos experimentales |
| **Comunidad activa** | Miles de librerías científicas disponibles | NumPy, Pandas, SciPy, Matplotlib |
| **Multiplataforma** | Mismo código en Windows, macOS, Linux | Colaboración internacional sin problemas |
| **Interpretado** | Prueba inmediata de hipótesis computacionales | Simulación interactiva de modelos |
| **Open Source** | Total transparencia y reproducibilidad | Investigación reproducible y verificable |

### 🛠️ **Instalación y Configuración del Entorno**

#### **Paso 1: Instalar Python**
```bash
# Verifica si ya tienes Python instalado
python --version
# Debe mostrar: Python 3.9 o superior

# Si no lo tienes, descarga desde:
# https://www.python.org/downloads/
```

#### **Paso 2: Configurar Entorno Virtual (Buenas Prácticas)**
```bash
# Crear entorno virtual para proyectos científicos
python -m venv lab_cientifico

# Activar entorno (Windows)
lab_cientifico\Scripts\activate

# Activar entorno (macOS/Linux)
source lab_cientifico/bin/activate
```

#### **Paso 3: Instalar Herramientas Básicas**
```bash
# Instalar IPython (Python interactivo mejorado)
pip install ipython

# Instalar Jupyter Notebook (laboratorio digital)
pip install notebook

# Verificar instalación
ipython --version
jupyter --version
```

### 🧪 **Primeros Pasos: "Hello World" Científico**

```python
# EJEMPLO 1: El clásico "Hello World"
print("Hello, Scientific World!")
# Output: Hello, Scientific World!

# EJEMPLO 2: Versión científica
print("🔬 ¡Bienvenido al Laboratorio Digital de Python!")
print("🧪 Preparado para comenzar experimentos computacionales")
print("📊 Python versión:", __import__('sys').version)
```

### 💡 **Consejo del Docente**
> **No te preocupes por memorizar todo ahora**. La programación científica se aprende haciendo, no memorizando. Cada concepto lo practicaremos con ejemplos reales.

---

## 1.2 Variables y Tipos de Datos Primitivos

### 🧠 **Concepto: ¿Qué es una Variable en Ciencia?**

**Analogía del laboratorio**: Una variable es como un **tubo de ensayo etiquetado**. Tiene:
- **Nombre** (la etiqueta)
- **Contenido** (lo que hay dentro)
- **Tipo** (qué tipo de sustancia contiene)

```python
# EJEMPLO: Variables como tubos de ensayo
temperatura = 25.5          # Tubo "temperatura" con 25.5°C
ph_solucion = 7.2           # Tubo "ph_solucion" con pH 7.2
nombre_reactivo = "HCl"     # Tubo "nombre_reactivo" con "HCl"
```

### 📝 **Nomenclatura de Variables (PEP 8)**

**PEP 8** es la guía de estilo oficial de Python. Para ciencia:

```python
# ✅ CORRECTO - Estilo científico claro
temperatura_promedio = 22.5
concentracion_molar = 0.1
velocidad_reaccion = 2.5e-3
muestra_control = True

# ❌ EVITAR - Confuso o poco científico
tmp = 22.5          # ¿Qué es tmp?
conc = 0.1          # ¿Qué concentración?
v_r = 2.5e-3        # ¿Velocidad de qué?
ctrl = True         # ¿Control de qué?
```

### 🔤 **Strings (Cadenas de Texto)**

#### **Creación y Manipulación**
```python
# EJEMPLO CIENTÍFICO: Nombres de compuestos químicos
compuesto = "Ácido acetilsalicílico"
formula = "C9H8O4"
nombre_comun = "Aspirina"

print(f"Compuesto: {compuesto}")
print(f"Fórmula: {formula}")
print(f"Nombre común: {nombre_comun}")
```

#### **Métodos de Strings Útiles en Ciencia**
```python
# Datos de un experimento
datos_crudos = "Temperatura:25.5,Presión:1013,Humedad:65%"

# 🧪 Separar datos
valores = datos_crudos.split(',')
print("Valores separados:", valores)
# Output: ['Temperatura:25.5', 'Presión:1013', 'Humedad:65%']

# 🧪 Extraer números
temperatura_str = valores[0]  # 'Temperatura:25.5'
temperatura_num = temperatura_str.split(':')[1]  # '25.5'
temperatura = float(temperatura_num)  # Convertir a número

print(f"Temperatura: {temperatura}°C")
```

#### **Indexación y Slicing**
```python
# EJEMPLO: Analizar código de muestra
codigo_muestra = "BIO-2024-001-A"

# Indexación (empezando en 0)
tipo = codigo_muestra[0:3]      # 'BIO'
anio = codigo_muestra[4:8]      # '2024'
numero = codigo_muestra[9:12]   # '001'
replica = codigo_muestra[13]    # 'A'

print(f"Tipo: {tipo}, Año: {anio}, Número: {numero}, Réplica: {replica}")
```

#### **Formato de Strings (f-strings - Recomendado)**
```python
# 📊 Resultados de experimento
reactivo = "NaOH"
concentracion = 0.1
volumen = 50
unidad = "mL"

# Formato tradicional
print("Preparar " + str(volumen) + " " + unidad + " de " + reactivo)

# Formato con f-string (¡Mucho mejor!)
print(f"Preparar {volumen} {unidad} de {reactivo} {concentracion}M")

# Formato con decimales controlados
ph = 7.245
print(f"pH medido: {ph:.2f}")  # Muestra 2 decimales: 7.25
print(f"pH medido: {ph:.3f}")  # Muestra 3 decimales: 7.245
```

### 🔢 **Integers y Floats (Números Enteros y Decimales)**

#### **Operaciones Básicas**
```python
# 🧪 Cálculos de laboratorio básicos

# Enteros (conteos, repeticiones)
repeticiones_experimento = 3
muestras_por_grupo = 5
total_muestras = repeticiones_experimento * muestras_por_grupo
print(f"Total de muestras: {total_muestras}")

# Decimales (mediciones continuas)
masa_reactivo = 2.5  # gramos
volumen_solvente = 100.0  # mL
concentracion = masa_reactivo / volumen_solvente  # g/mL
print(f"Concentración: {concentracion} g/mL")

# Notación científica (muy común en ciencia)
constante_avogadro = 6.02214076e23  # 6.02214076 × 10^23
carga_electron = 1.602176634e-19    # 1.602176634 × 10^-19 C

print(f"Constante de Avogadro: {constante_avogadro}")
print(f"Carga del electrón: {carga_electron} C")
```

#### **Conversión de Tipos**
```python
# ⚠️ CUIDADO: Python es de tipado dinámico pero estricto

# Esto funciona
lectura_str = "25.5"
temperatura = float(lectura_str)  # Convertir string a float
print(f"Temperatura: {temperatura}°C")

# Esto NO funciona (error común)
# temperatura = "25.5" + 1  # ERROR: No se puede sumar string y número

# Solución correcta
temperatura = float("25.5") + 1
print(f"Temperatura ajustada: {temperatura}°C")
```

### ⚖️ **Boolean (Valores Lógicos)**

#### **True y False en Experimentos**
```python
# 📊 Control de condiciones experimentales

experimento_completado = True
datos_validos = False
equipo_calibrado = True

# Verificación de condiciones
if experimento_completado and equipo_calibrado:
    print("✅ Experimento listo para análisis")
else:
    print("❌ Verificar condiciones experimentales")

# Valores truthy y falsy
muestra = ""  # String vacío es falsy
if muestra:
    print("Hay muestra para analizar")
else:
    print("No hay muestra")  # Esto se ejecuta
```

### 🔮 **Complex (Números Complejos)**

```python
# 🎯 Aplicación: Análisis de circuitos eléctricos (ingeniería)
# o funciones de onda (física cuántica)

# Número complejo: a + bj (j es la unidad imaginaria)
impedancia = 3 + 4j  # 3 ohms resistencia, 4 ohms reactancia

# Componentes
resistencia = impedancia.real  # 3.0
reactancia = impedancia.imag   # 4.0

# Magnitud (módulo)
magnitud = abs(impedancia)  # √(3² + 4²) = 5

# Fase (ángulo)
import cmath
fase = cmath.phase(impedancia)  # arctan(4/3) ≈ 0.93 radianes

print(f"Impedancia: {impedancia} Ω")
print(f"Resistencia: {resistencia} Ω, Reactancia: {reactancia} Ω")
print(f"Magnitud: {magnitud:.2f} Ω, Fase: {fase:.2f} rad")
```

---

## 1.3 Operadores

### ➕ **Operadores Aritméticos**
```python
# 🧪 Cálculos de preparación de soluciones

# Datos iniciales
concentracion_stock = 2.0  # M (molar)
volumen_necesario = 100    # mL
concentracion_final = 0.1  # M

# Cálculo: C1V1 = C2V2
volumen_stock = (concentracion_final * volumen_necesario) / concentracion_stock
volumen_agua = volumen_necesario - volumen_stock

print(f"Para preparar {volumen_necesario} mL de {concentracion_final}M:")
print(f"  • Tomar {volumen_stock:.1f} mL de stock {concentracion_stock}M")
print(f"  • Añadir {volumen_agua:.1f} mL de agua destilada")

# Operadores especiales
# División entera (//) y módulo (%)
total_muestras = 17
muestras_por_tubo = 5

tubos_completos = total_muestras // muestras_por_tubo  # 3
muestras_sobrantes = total_muestras % muestras_por_tubo  # 2

print(f"\nSe necesitan {tubos_completos} tubos completos")
print(f"Sobran {muestras_sobrantes} muestras para otro tubo")
```

### ⚖️ **Operadores de Comparación**
```python
# 📊 Control de calidad experimental

temperatura_actual = 25.3
temperatura_objetivo = 25.0
tolerancia = 0.5

# Verificaciones
dentro_tolerancia = abs(temperatura_actual - temperatura_objetivo) <= tolerancia
demasiado_caliente = temperatura_actual > temperatura_objetivo + tolerancia
demasiado_frio = temperatura_actual < temperatura_objetivo - tolerancia

print(f"Temperatura actual: {temperatura_actual}°C")
print(f"Temperatura objetivo: {temperatura_objetivo}°C ± {tolerancia}°C")
print(f"¿Dentro de tolerancia? {dentro_tolerancia}")
print(f"¿Demasiado caliente? {demasiado_caliente}")
print(f"¿Demasiado frío? {demasiado_frio}")
```

### 🔗 **Operadores Lógicos**
```python
# 🧪 Verificación de condiciones experimentales

temperatura_ok = True
ph_ok = False
oxigeno_ok = True
agitacion_ok = True

# Condiciones complejas
experimento_valido = temperatura_ok and ph_ok and oxigeno_ok
# False (porque ph_ok es False)

cultivo_creciendo = temperatura_ok and (oxigeno_ok or agitacion_ok)
# True (temperatura_ok Y (oxigeno_ok O agitacion_ok))

print(f"¿Experimento válido? {experimento_valido}")
print(f"¿Cultivo creciendo? {cultivo_creciendo}")

# Operador NOT (inversión)
if not ph_ok:
    print("⚠️  ADVERTENCIA: pH fuera de rango. Ajustar inmediatamente.")
```

### 📊 **Jerarquía de Operadores (Precedencia)**
```python
# ⚠️ IMPORTANTE: El orden SÍ importa en cálculos científicos

# Ejemplo: Cálculo de densidad
masa = 10  # gramos
volumen = 2  # mL

# ¿Cuál es la diferencia?
densidad1 = masa / volumen ** 2  # masa / (volumen²)
densidad2 = (masa / volumen) ** 2  # (masa/volumen)²

print(f"Densidad 1 (masa/volumen²): {densidad1} g/mL²")
print(f"Densidad 2 ((masa/volumen)²): {densidad2} (g/mL)²")

# Regla mnemotécnica: PEMDAS
# Paréntesis > Exponentes > Multiplicación/División > Adición/Sustracción
```

---

## 1.4 Entrada y Salida

### 🖨️ **print() - Mostrar Información en Consola**
```python
# 📊 Presentación profesional de resultados

# Resultados de un experimento
compuesto = "Glucosa"
concentracion = 0.05
absorbancia = 0.423
desviacion = 0.012

# Formas de mostrar resultados
print("=" * 50)
print("RESULTADOS DEL EXPERIMENTO")
print("=" * 50)
print(f"Compuesto: {compuesto}")
print(f"Concentración: {concentracion} M")
print(f"Absorbancia: {absorbancia} ± {desviacion}")
print("-" * 50)

# Múltiples valores
print("Parámetro", "Valor", "Unidad", sep=" | ")
print("-" * 30)
print("pH", 7.2, "", sep=" | ")
print("Temperatura", 25.5, "°C", sep=" | ")
print("Conductividad", 1.2, "mS/cm", sep=" | ")
```

### ⌨️ **input() - Recibir Datos del Usuario**
```python
# 🧪 Programa interactivo para preparar soluciones

print("🧪 PREPARADOR DE SOLUCIONES 🧪")
print("-" * 30)

# Entrada de datos
nombre_reactivo = input("Nombre del reactivo: ")
concentracion_deseada = float(input("Concentración deseada (M): "))
volumen_deseado = float(input("Vol