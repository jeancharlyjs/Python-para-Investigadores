# MÓDULO 3: CONTROL DE FLUJO
## Toma de Decisiones en el Análisis Científico

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Implementar estructuras condicionales para análisis de datos científicos
2. Utilizar bucles para procesamiento iterativo de experimentos
3. Aplicar comprensiones avanzadas para transformación de datos
4. Manejar excepciones en procesos científicos
5. Diseñar algoritmos eficientes para análisis automatizado

---

## 3.1 Estructuras Condicionales

### Concepto: Toma de Decisiones en Ciencia

En investigación científica, constantemente necesitamos tomar decisiones basadas en datos: ¿Es válida esta medición? ¿Debo continuar el experimento? ¿Qué tratamiento aplicar? Las estructuras condicionales nos permiten **automatizar estas decisiones** en código.

### if, elif, else - La Base de la Decisión

```python
# Ejemplo: Clasificación de muestras por pH

def clasificar_ph(pH):
    """Clasifica una muestra según su valor de pH"""
    if pH < 0:
        return "ERROR: pH fuera de rango válido"
    elif pH < 3:
        return "MUY ÁCIDO - Precaución extrema"
    elif pH < 6:
        return "ÁCIDO"
    elif pH < 7.5:
        return "LIGERAMENTE ÁCIDO"
    elif pH == 7:
        return "NEUTRO"
    elif pH <= 8.5:
        return "LIGERAMENTE BÁSICO"
    elif pH <= 11:
        return "BÁSICO"
    elif pH <= 14:
        return "MUY BÁSICO - Precaución extrema"
    else:
        return "ERROR: pH fuera de rango válido"

# Pruebas con diferentes valores de pH
muestras_ph = [2.5, 5.8, 7.0, 8.2, 12.0, -1.0, 15.0]

print("CLASIFICACIÓN DE MUESTRAS POR pH")
print("=" * 50)
for ph in muestras_ph:
    clasificacion = clasificar_ph(ph)
    print(f"pH {ph:5.1f}: {clasificacion}")
```

### Operadores de Comparación en Contexto Científico

```python
# Ejemplo: Control de calidad en mediciones

def evaluar_calidad_medicion(valor_medido, valor_esperado, tolerancia):
    """Evalúa si una medición está dentro de tolerancia"""
    
    diferencia = abs(valor_medido - valor_esperado)
    
    # Evaluación con múltiples condiciones
    if diferencia <= tolerancia * 0.5:
        return "EXCELENTE - Dentro del 50% de tolerancia"
    elif diferencia <= tolerancia:
        return "ACEPTABLE - Dentro de tolerancia"
    elif diferencia <= tolerancia * 2:
        return "REGULAR - Fuera de tolerancia pero dentro del doble"
    else:
        return "INACEPTABLE - Fuera del doble de tolerancia"

# Datos de calibración de un instrumento
valor_esperado = 100.0  # Valor de referencia
tolerancia = 5.0  # ±5 unidades

mediciones = [98.5, 102.3, 94.8, 107.2, 110.5]

print("EVALUACIÓN DE CALIDAD DE MEDICIONES")
print("=" * 60)
print(f"Valor esperado: {valor_esperado}, Tolerancia: ±{tolerancia}")
print("-" * 60)

for i, medicion in enumerate(mediciones, 1):
    evaluacion = evaluar_calidad_medicion(medicion, valor_esperado, tolerancia)
    print(f"Medición {i}: {medicion:6.1f} -> {evaluacion}")
```

### Operadores Lógicos en Análisis Científico

```python
# Ejemplo: Validación de condiciones experimentales

def validar_condiciones_experimento(temperatura, ph, oxigeno, agitacion):
    """Valida múltiples condiciones para un experimento"""
    
    # Condiciones individuales
    temp_ok = 20 <= temperatura <= 30
    ph_ok = 6.5 <= ph <= 7.5
    oxigeno_ok = oxigeno >= 5.0  # mg/L mínimo
    agitacion_ok = agitacion in ["lenta", "media", "rapida"]
    
    # Evaluación combinada
    if temp_ok and ph_ok and oxigeno_ok and agitacion_ok:
        return "CONDICIONES ÓPTIMAS - Experimento puede proceder"
    
    # Identificar problemas específicos
    problemas = []
    if not temp_ok:
        problemas.append(f"Temperatura fuera de rango ({temperatura}°C)")
    if not ph_ok:
        problemas.append(f"pH fuera de rango ({ph})")
    if not oxigeno_ok:
        problemas.append(f"Oxígeno insuficiente ({oxigeno} mg/L)")
    if not agitacion_ok:
        problemas.append(f"Modo de agitación inválido ({agitacion})")
    
    return f"CONDICIONES NO ÓPTIMAS - Problemas: {', '.join(problemas)}"

# Pruebas con diferentes condiciones
condiciones_prueba = [
    (25.0, 7.2, 6.5, "media"),      # Óptimas
    (35.0, 7.2, 6.5, "media"),      # Temperatura alta
    (25.0, 5.0, 6.5, "media"),      # pH bajo
    (25.0, 7.2, 2.0, "media"),      # Oxígeno bajo
    (25.0, 7.2, 6.5, "parada"),     # Agitación inválida
    (35.0, 5.0, 2.0, "parada")      # Múltiples problemas
]

print("VALIDACIÓN DE CONDICIONES EXPERIMENTALES")
print("=" * 70)

for i, (temp, ph, oxi, agi) in enumerate(condiciones_prueba, 1):
    resultado = validar_condiciones_experimento(temp, ph, oxi, agi)
    print(f"Prueba {i}: {resultado}")
```

### Condicionales Anidados para Análisis Complejo

```python
# Ejemplo: Sistema de diagnóstico de calidad de agua

def diagnosticar_calidad_agua(turbidez, coliformes, ph, oxigeno_disuelto):
    """Diagnostica la calidad del agua basado en múltiples parámetros"""
    
    # Evaluación de turbidez (NTU)
    if turbidez < 1:
        calidad_turbidez = "EXCELENTE"
    elif turbidez < 5:
        calidad_turbidez = "BUENA"
    elif turbidez < 10:
        calidad_turbidez = "REGULAR"
    else:
        calidad_turbidez = "POBRE"
    
    # Evaluación de coliformes (UFC/100mL)
    if coliformes == 0:
        calidad_coliformes = "EXCELENTE"
    elif coliformes < 10:
        calidad_coliformes = "BUENA"
    elif coliformes < 100:
        calidad_coliformes = "REGULAR"
    else:
        calidad_coliformes = "POBRE"
    
    # Evaluación de pH
    if 6.5 <= ph <= 8.5:
        calidad_ph = "ACEPTABLE"
    else:
        calidad_ph = "INACEPTABLE"
    
    # Evaluación de oxígeno disuelto (mg/L)
    if oxigeno_disuelto >= 6:
        calidad_oxigeno = "EXCELENTE"
    elif oxigeno_disuelto >= 4:
        calidad_oxigeno = "BUENA"
    elif oxigeno_disuelto >= 2:
        calidad_oxigeno = "REGULAR"
    else:
        calidad_oxigeno = "POBRE"
    
    # Diagnóstico final (anidado complejo)
    if calidad_turbidez == "EXCELENTE" and calidad_coliformes == "EXCELENTE":
        if calidad_oxigeno == "EXCELENTE" and calidad_ph == "ACEPTABLE":
            return "AGUA POTABLE - Cumple todos los estándares"
        elif calidad_oxigeno in ["EXCELENTE", "BUENA"]:
            return "AGUA TRATABLE - Requiere ajuste de pH"
        else:
            return "AGUA NO POTABLE - Oxígeno insuficiente"
    
    elif calidad_coliformes == "POBRE":
        return "AGUA CONTAMINADA - Alto nivel de coliformes"
    
    elif calidad_turbidez == "POBRE":
        return "AGUA TURBIA - Requiere filtración"
    
    else:
        return "AGUA DE CALIDAD INTERMEDIA - Requiere análisis adicional"

# Muestras de agua para diagnóstico
muestras_agua = [
    (0.5, 0, 7.2, 7.5),    # Excelente
    (3.2, 5, 6.8, 5.0),    # Buena
    (8.5, 50, 7.0, 3.5),   # Regular
    (15.0, 200, 5.5, 1.0), # Pobre
    (2.0, 0, 9.0, 6.5)     # pH alto
]

print("DIAGNÓSTICO DE CALIDAD DE AGUA")
print("=" * 70)
print("Parámetros: Turbidez(NTU), Coliformes(UFC), pH, O₂(mg/L)")
print("-" * 70)

for i, (turb, col, ph, oxi) in enumerate(muestras_agua, 1):
    diagnostico = diagnosticar_calidad_agua(turb, col, ph, oxi)
    print(f"Muestra {i}: {turb:4.1f} NTU, {col:4d} UFC, pH {ph:3.1f}, {oxi:3.1f} mg/L")
    print(f"  -> {diagnostico}")
    print()
```

---

## 3.2 Bucles (Loops)

### Concepto: Automatización de Procesos Repetitivos

En ciencia, muchos procesos son repetitivos: medir múltiples muestras, procesar series temporales, analizar imágenes celulares. Los bucles nos permiten **automatizar estas tareas repetitivas** de manera eficiente.

### for Loop - Iteración sobre Colecciones

```python
# Ejemplo: Procesamiento de datos de espectrometría

def analizar_espectro(longitudes_onda, intensidades):
    """Analiza un espectro para encontrar picos y características"""
    
    print("ANÁLISIS DE ESPECTRO")
    print("=" * 60)
    print(f"{'Longitud (nm)':<15} {'Intensidad':<12} {'Análisis':<30}")
    print("-" * 60)
    
    # Variables para análisis
    intensidad_maxima = 0
    longitud_maxima = 0
    intensidad_total = 0
    picos_significativos = []
    
    # Iteración sobre todos los puntos del espectro
    for i in range(len(longitudes_onda)):
        longitud = longitudes_onda[i]
        intensidad = intensidades[i]
        
        # Actualizar máximo
        if intensidad > intensidad_maxima:
            intensidad_maxima = intensidad
            longitud_maxima = longitud
        
        # Acumular intensidad total
        intensidad_total += intensidad
        
        # Identificar picos significativos (> 0.5)
        if intensidad > 0.5:
            picos_significativos.append((longitud, intensidad))
        
        # Clasificar intensidad en tiempo real
        if intensidad > 0.8:
            clasificacion = "PUYO PRINCIPAL"
        elif intensidad > 0.5:
            clasificacion = "PUYO SECUNDARIO"
        elif intensidad > 0.2:
            clasificacion = "BANDA DÉBIL"
        else:
            clasificacion = "RUIDO DE FONDO"
        
        print(f"{longitud:<15} {intensidad:<12.3f} {clasificacion:<30}")
    
    # Resultados del análisis
    print("-" * 60)
    print(f"Intensidad total: {intensidad_total:.3f}")
    print(f"Pico máximo: {intensidad_maxima:.3f} a {longitud_maxima} nm")
    print(f"Picos significativos (>0.5): {len(picos_significativos)}")
    
    return {
        'intensidad_total': intensidad_total,
        'pico_maximo': (longitud_maxima, intensidad_maxima),
        'picos_significativos': picos_significativos
    }

# Datos de espectro simulado
longitudes = [400, 420, 440, 460, 480, 500, 520, 540, 560, 580]
intensidades = [0.1, 0.3, 0.7, 0.9, 0.6, 0.4, 0.8, 0.5, 0.2, 0.1]

resultados = analizar_espectro(longitudes, intensidades)
```

### for con enumerate() - Iteración con Índice

```python
# Ejemplo: Seguimiento de crecimiento bacteriano

def analizar_crecimiento_bacteriano(tiempos, densidades_opt):
    """Analiza datos de crecimiento bacteriano a lo largo del tiempo"""
    
    print("ANÁLISIS DE CRECIMIENTO BACTERIANO")
    print("=" * 70)
    print(f"{'Tiempo (h)':<12} {'Densidad (OD)':<15} {'Fase':<20} {'Tasa (OD/h)':<15}")
    print("-" * 70)
    
    tasas_crecimiento = []
    fase_actual = ""
    
    for i, (tiempo, densidad) in enumerate(zip(tiempos, densidades_opt)):
        
        # Calcular tasa de crecimiento (excepto primer punto)
        if i > 0:
            delta_t = tiempo - tiempos[i-1]
            delta_od = densidad - densidades_opt[i-1]
            tasa = delta_od / delta_t if delta_t > 0 else 0
            tasas_crecimiento.append(tasa)
        else:
            tasa = 0
        
        # Determinar fase de crecimiento
        if densidad < 0.1:
            fase = "LAG"
        elif densidad < 0.5:
            fase = "EXPONENCIAL"
        elif densidad < 1.0:
            fase = "ESTACIONARIA"
        else:
            fase = "MUERTE"
        
        # Detectar cambios de fase
        if fase != fase_actual:
            cambio = f"-> {fase}"
            fase_actual = fase
        else:
            cambio = ""
        
        print(f"{tiempo:<12.1f} {densidad:<15.3f} {fase:<20} {tasa:<15.3f} {cambio}")
    
    # Análisis estadístico
    if tasas_crecimiento:
        tasa_max = max(tasas_crecimiento)
        tasa_prom = sum(tasas_crecimiento) / len(tasas_crecimiento)
        
        print("-" * 70)
        print(f"Tasa máxima de crecimiento: {tasa_max:.3f} OD/h")
        print(f"Tasa promedio de crecimiento: {tasa_prom:.3f} OD/h")
        print(f"Duración fase exponencial: {sum(1 for d in densidades_opt if 0.1 <= d < 0.5)} horas")

# Datos de crecimiento bacteriano
horas = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
densidades = [0.05, 0.08, 0.15, 0.35, 0.65, 0.85, 0.90, 0.88, 0.82, 0.75, 0.65]

analizar_crecimiento_bacteriano(horas, densidades)
```

### for con zip() - Iteración Múltiple Sincronizada

```python
# Ejemplo: Análisis de datos meteorológicos paralelos

def analizar_datos_meteorologicos(fechas, temperaturas, humedades, precipitaciones):
    """Analiza múltiples variables meteorológicas simultáneamente"""
    
    print("ANÁLISIS METEOROLÓGICO DIARIO")
    print("=" * 90)
    print(f"{'Fecha':<12} {'Temp (°C)':<12} {'Humedad (%)':<12} {'Precip (mm)':<12} {'Clasificación':<30} {'Alerta':<15}")
    print("-" * 90)
    
    dias_calidos = 0
    dias_humedos = 0
    dias_lluviosos = 0
    alertas_totales = []
    
    for fecha, temp, hum, prec in zip(fechas, temperaturas, humedades, precipitaciones):
        
