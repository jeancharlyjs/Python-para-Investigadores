# MÓDULO 4: FUNCIONES
## Modularización y Reutilización en Ciencia Computacional

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Diseñar y definir funciones para tareas científicas específicas
2. Utilizar diferentes tipos de parámetros y argumentos
3. Implementar funciones lambda para operaciones rápidas
4. Comprender y aplicar funciones recursivas
5. Utilizar funciones de orden superior para procesamiento de datos
6. Manejar correctamente el alcance de variables en contextos científicos

---

## 4.1 Definición y Sintaxis

### Concepto: ¿Qué es una Función en Ciencia Computacional?

Una función es un **bloque de código reutilizable** que realiza una tarea específica. En ciencia, las funciones son como **procedimientos de laboratorio estandarizados**: una vez definidos, pueden ejecutarse múltiples veces con diferentes insumos (parámetros) para producir resultados consistentes.

### Estructura Básica de una Función

```python
def nombre_funcion(parametro1, parametro2, ...):
    """
    Docstring: Documentación de la función
    Describe qué hace, qué parámetros recibe y qué retorna
    """
    # Cuerpo de la función
    # Código que realiza la tarea
    return resultado  # Opcional
```

### Ejemplo: Función para Cálculos de Concentración

```python
def calcular_concentracion(masa_reactivo, volumen_solvente, pureza=1.0):
    """
    Calcula la concentración de una solución.
    
    Parámetros:
    -----------
    masa_reactivo : float
        Masa del reactivo en gramos
    volumen_solvente : float
        Volumen del solvente en mililitros
    pureza : float, opcional (default=1.0)
        Pureza del reactivo como fracción (0-1)
    
    Retorna:
    --------
    float
        Concentración en g/mL
    """
    # Validación de parámetros
    if masa_reactivo <= 0:
        raise ValueError("La masa del reactivo debe ser positiva")
    if volumen_solvente <= 0:
        raise ValueError("El volumen del solvente debe ser positivo")
    if not 0 <= pureza <= 1:
        raise ValueError("La pureza debe estar entre 0 y 1")
    
    # Cálculo de concentración
    masa_pura = masa_reactivo * pureza
    concentracion = masa_pura / volumen_solvente
    
    return concentracion

# Uso de la función
print("CÁLCULOS DE CONCENTRACIÓN")
print("=" * 50)

# Caso 1: Reactivo puro
conc1 = calcular_concentracion(2.5, 100.0)
print(f"2.5g en 100mL (puro): {conc1:.4f} g/mL")

# Caso 2: Reactivo al 95% de pureza
conc2 = calcular_concentracion(2.5, 100.0, 0.95)
print(f"2.5g en 100mL (95%): {conc2:.4f} g/mL")

# Caso 3: Múltiples cálculos
masas = [1.0, 2.0, 3.0, 4.0, 5.0]
volumen = 50.0

print("\nConcentraciones para diferentes masas en 50mL:")
for masa in masas:
    conc = calcular_concentracion(masa, volumen)
    print(f"  {masa}g -> {conc:.4f} g/mL")
```

### Parámetros y Argumentos

```python
def preparar_solucion(reactivo, concentracion, volumen, unidad="M", notas=""):
    """
    Genera instrucciones para preparar una solución.
    
    Parámetros:
    -----------
    reactivo : str
        Nombre del reactivo
    concentracion : float
        Concentración deseada
    volumen : float
        Volumen a preparar
    unidad : str, opcional (default="M")
        Unidad de concentración (M, mM, %)
    notas : str, opcional (default="")
        Notas adicionales
    
    Retorna:
    --------
    str
        Instrucciones detalladas
    """
    instrucciones = f"""
    PREPARACIÓN DE SOLUCIÓN
    =======================
    Reactivo: {reactivo}
    Concentración: {concentracion} {unidad}
    Volumen: {volumen} mL
    
    PROCEDIMIENTO:
    1. Calcular masa necesaria según fórmula estequiométrica
    2. Pesar {concentracion * volumen:.2f} {unidad} equivalentes
    3. Disolver en aproximadamente {volumen * 0.8:.1f} mL de solvente
    4. Ajustar a volumen final de {volumen} mL
    5. Homogeneizar completamente
    
    PRECAUCIONES:
    - Usar equipo de protección personal
    - Verificar compatibilidad química
    """
    
    if notas:
        instrucciones += f"\nNOTAS: {notas}"
    
    return instrucciones

# Diferentes formas de llamar la función
print("EJEMPLOS DE PREPARACIÓN DE SOLUCIONES")
print("=" * 60)

# 1. Argumentos posicionales
inst1 = preparar_solucion("NaCl", 0.1, 100)
print(inst1)

# 2. Argumentos nombrados (keyword arguments)
inst2 = preparar_solucion(
    reactivo="HCl",
    concentracion=1.0,
    volumen=50,
    unidad="M",
    notas="Ácido corrosivo. Manipular en campana."
)
print(inst2)

# 3. Mezcla de posicionales y nombrados
inst3 = preparar_solucion("NaOH", 0.5, 200, notas="Base fuerte. Genera calor al disolver.")
print(inst3)
```

### return - Retornar Valores

```python
def analizar_datos_experimentales(datos_crudos, umbral_ruido=0.1):
    """
    Analiza datos experimentales y retorna múltiples valores.
    
    Parámetros:
    -----------
    datos_crudos : list of float
        Datos experimentales crudos
    umbral_ruido : float, opcional (default=0.1)
        Umbral para filtrar ruido
    
    Retorna:
    --------
    tuple
        (media, desviacion, datos_filtrados, n_validos)
    """
    # Filtrar datos por umbral de ruido
    datos_filtrados = [d for d in datos_crudos if d > umbral_ruido]
    
    if not datos_filtrados:
        return 0, 0, [], 0  # Retorno temprano si no hay datos válidos
    
    # Cálculos estadísticos
    n_validos = len(datos_filtrados)
    media = sum(datos_filtrados) / n_validos
    
    # Calcular desviación estándar
    suma_cuadrados = sum((d - media) ** 2 for d in datos_filtrados)
    desviacion = (suma_cuadrados / n_validos) ** 0.5
    
    # Retornar múltiples valores como tupla
    return media, desviacion, datos_filtrados, n_validos

# Datos experimentales (simulados)
datos_crudos = [0.05, 0.423, 0.512, 0.02, 0.467, 0.03, 0.512, 0.423]

print("ANÁLISIS DE DATOS EXPERIMENTALES")
print("=" * 60)

# Llamada a la función y desempaquetado del retorno
media, desviacion, datos_filtrados, n = analizar_datos_experimentales(datos_crudos)

print(f"Datos crudos: {datos_crudos}")
print(f"Datos filtrados (>0.1): {datos_filtrados}")
print(f"Número de datos válidos: {n}")
print(f"Media: {media:.3f}")
print(f"Desviación estándar: {desviacion:.3f}")
print(f"Coeficiente de variación: {(desviacion/media*100):.1f}%")

# También podemos capturar el retorno como una tupla
resultados = analizar_datos_experimentales(datos_crudos, umbral_ruido=0.2)
print(f"\nCon umbral 0.2: {resultados}")
```

### Docstrings (Documentación de Funciones)

```python
def ley_beer_lambert(absorbancia, coeficiente_extincion, longitud_celda):
    """
    Calcula la concentración usando la Ley de Beer-Lambert.
    
    La Ley de Beer-Lambert establece que la absorbancia (A) es
    proporcional a la concentración (C) según:
    
        A = ε * l * C
    
    donde:
        ε = coeficiente de extinción molar (M⁻¹ cm⁻¹)
        l = longitud de la celda (cm)
        C = concentración (M)
    
    Parámetros:
    -----------
    absorbancia : float
        Valor de absorbancia medido (adimensional)
    coeficiente_extincion : float
        Coeficiente de extinción molar en M⁻¹ cm⁻¹
    longitud_celda : float
        Longitud de la celda en cm
    
    Retorna:
    --------
    float
        Concentración en molaridad (M)
    
    Ejemplos:
    ---------
    >>> ley_beer_lambert(0.5, 1500, 1.0)
    0.0003333333333333333
    
    >>> ley_beer_lambert(1.2, 2500, 1.0)
    0.00048
    
    Notas:
    ------
    - La ley es válida para soluciones diluidas
    - Asume que no hay interacciones entre moléculas
    - La absorbancia debe estar en el rango lineal del instrumento
    """
    # Validación de parámetros
    if absorbancia < 0:
        raise ValueError("La absorbancia no puede ser negativa")
    if coeficiente_extincion <= 0:
        raise ValueError("El coeficiente de extinción debe ser positivo")
    if longitud_celda <= 0:
        raise ValueError("La longitud de la celda debe ser positiva")
    
    # Cálculo de concentración
    concentracion = absorbancia / (coeficiente_extincion * longitud_celda)
    
    return concentracion

# La documentación es accesible mediante help()
print("DOCUMENTACIÓN DE LA FUNCIÓN:")
print("=" * 60)
print(ley_beer_lambert.__doc__)

# Ejemplo de uso
print("\nEJEMPLO PRÁCTICO:")
print("=" * 60)
absorbancia_medida = 0.423
epsilon = 1500  # M⁻¹ cm⁻¹
l = 1.0  # cm

concentracion = ley_beer_lambert(absorbancia_medida, epsilon, l)
print(f"Absorbancia: {absorbancia_medida}")
print(f"Coeficiente de extinción: {epsilon} M⁻¹ cm⁻¹")
print(f"Longitud de celda: {l} cm")
print(f"Concentración calculada: {concentracion:.6f} M")
print(f"Concentración en mM: {concentracion*1000:.3f} mM")
```

---

## 4.2 Tipos de Parámetros

### Parámetros Posicionales

```python
def calcular_dilucion(concentracion_inicial, volumen_inicial, volumen_final):
    """
    Calcula la concentración final después de una dilución.
    
    Usa la fórmula: C1 * V1 = C2 * V2
    
    Parámetros posicionales (orden importante):
    1. concentracion_inicial
    2. volumen_inicial  
    3. volumen_final
    """
    if volumen_final <= 0:
        raise ValueError("El volumen final debe ser positivo")
    
    concentracion_final = (concentracion_inicial * volumen_inicial) / volumen_final
    return concentracion_final

# Uso correcto (orden correcto)
resultado = calcular_dilucion(1.0, 10.0, 100.0)  # C1=1.0, V1=10.0, V2=100.0
print(f"Dilución 1:10 de 1.0M -> {resultado:.2f}M")

# Uso incorrecto (orden equivocado)
# resultado = calcular_dilucion(10.0, 1.0, 100.0)  # ¡Esto daría un resultado erróneo!
```

### Parámetros con Valores por Defecto

```python
def preparar_buffer(tampon, volumen, ph=7.4, concentracion=0.1, temperatura=25.0):
    """
    Genera protocolo para preparar buffer con parámetros por defecto.
    
    Parámetros con valores por defecto:
    - ph: 7.4 (pH fisiológico)
    - concentracion: 0.1 M
    - temperatura: 25.0 °C
    """
    protocolo = f"""
    PROTOCOLO PARA PREPARAR BUFFER
    ==============================
    Tampón: {tampon}
    Volumen: {volumen} mL
    pH objetivo: {ph}
    Concentración: {concentracion} M
    Temperatura: {temperatura} °C
    
    PROCEDIMIENTO:
    1. Disolver componentes según tabla estequiométrica
    2. Ajustar pH a {ph} usando HCl/NaOH
    3. Llevar a volumen final de {volumen} mL
    4. Verificar pH a {temperatura} °C
    5. Almacenar a 4°C si no se usa inmediatamente
    """
    return protocolo

# Diferentes formas de usar valores por defecto
print("EJEMPLOS DE PREPARACIÓN DE BUFFER")
print("=" * 60)

# 1. Usar todos los valores por defecto
buffer1 = preparar_buffer("Tris-HCl", 100)
print("Buffer 1 (valores por defecto):")
print(buffer1)

# 2. Especificar algunos parámetros
buffer2 = preparar_buffer("PBS", 500, ph=7.2)
print("\nBuffer 2 (pH específico):")
print(buffer2)

# 3. Especificar todos los parámetros
buffer3 = preparar_buffer("HEPES", 250, ph=7.8, concentracion=0.05, temperatura=37.0)
print("\nBuffer 3 (todos personalizados):")
print(buffer3)
```

### Parámetros Nombrados (Keyword Arguments)

```python
def configurar_experimento(
    nombre,
    duracion_horas,
    **kwargs  # Parámetros adicionales como diccionario
):
    """
    Configura un experimento con parámetros flexibles.
    
    Parámetros nombrados permiten gran flexibilidad.
    **kwargs captura todos los parámetros adicionales.
    """
    configuracion = {
        'nombre': nombre,
        'duracion_horas': duracion_horas,
        'estado': 'configurado'
    }
    
    # Añadir parámetros adicionales
    configuracion.update(kwargs)
    
    # Generar reporte
    reporte = f"""
    CONFIGURACIÓN DE EXPERIMENTO
    ============================
    Nombre: {nombre}
    Duración: {duracion_horas} horas
    Estado: {configuracion.get('estado', 'desconocido')}
    
    PARÁMETROS ESPECÍFICOS:
    """
    
    for key, value in kwargs.items():
        if key != 'estado':  # No repetir estado
            reporte += f"  {key}: {value}\n"
    
    return configuracion, reporte

# Ejemplos con diferentes combinaciones de parámetros
print("CONFIGURACIÓN FLEXIBLE DE EXPERIMENTOS")
print("=" * 60)

# Experimento simple
config1, reporte1 = configurar_experimento(
    nombre="Crecimiento bacteriano",
    duracion_horas=24
)
print("Experimento 1 (básico):")
print(reporte1)

# Experimento con múltiples parámetros
config2, reporte2 = configurar_experimento(
    nombre="Cinética enzimática",
    duracion_horas=2,
    temperatura=37.0,
    ph=7.4,
    concentracion_sustrato=0.01,
    volumen_reaccion=100,
    equipo=["espectrofotómetro", "baño termostatizado"],
    operador="Dr. García"
)
print("\nExperimento 2 (completo):")
print(reporte2)

# Experimento con parámetros inesperados
config3, reporte3 = configurar_experimento(
    nombre="Prueba de estabilidad",
    duracion_horas=168,  # 7 días
    condicion_almacenamiento="4°C",
    analisis_intermedio=[24, 48, 72, 168],
    criterio_aceptacion=">95% pureza",
    referencia="Farmacopea USP"
)
print("\nExperimento 3 (flexible):")
print(reporte3)
