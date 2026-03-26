# MÓDULO 9: MATPLOTLIB Y VISUALIZACIÓN
## Comunicación Visual de Resultados Científicos

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Crear figuras y ejes para visualización científica
2. Generar diferentes tipos de gráficos para análisis de datos
3. Personalizar gráficos con títulos, etiquetas y leyendas
4. Crear subplots para comparaciones múltiples
5. Visualizar datos en 3D para análisis espacial
6. Utilizar Seaborn para visualización estadística avanzada

---

## 9.1 Conceptos Básicos

### Concepto: ¿Por qué la Visualización es Esencial en Ciencia?

La visualización de datos es **fundamental en la investigación científica** porque:
- **Revela patrones** que no son evidentes en tablas numéricas
- **Facilita la comunicación** de resultados complejos
- **Permite identificar outliers** y anomalías
- **Ayuda en la toma de decisiones** basada en datos
- **Mejora la reproducibilidad** de experimentos

### Instalación y Configuración

```python
# Instalación de bibliotecas de visualización
# pip install matplotlib seaborn

# Importación estándar
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# Configuración para mejores gráficos científicos
plt.style.use('seaborn-v0_8-whitegrid')  # Estilo con cuadrícula
plt.rcParams['figure.figsize'] = (10, 6)  # Tamaño por defecto
plt.rcParams['font.size'] = 12            # Tamaño de fuente
plt.rcParams['axes.titlesize'] = 14       # Tamaño de título
plt.rcParams['axes.labelsize'] = 12       # Tamaño de etiquetas

print("MATPLOTLIB PARA VISUALIZACIÓN CIENTÍFICA")
print("=" * 60)
print(f"Matplotlib versión: {plt.__version__}")
print(f"Estilo actual: {plt.style.available[:5]}...")  # Primeros 5 estilos
```

### Figuras y Ejes

```python
def demostracion_figuras_ejes():
    """
    Demuestra la creación y manipulación de figuras y ejes.
    """
    
    print("FIGURAS Y EJES - ESTRUCTURA BÁSICA")
    print("=" * 70)
    
    # 1. Creación básica de figura y ejes
    print("1. CREACIÓN BÁSICA:")
    
    # Método 1: plt.subplots() (recomendado)
    fig, ax = plt.subplots()
    print(f"  Figura creada: {fig}")
    print(f"  Ejes creados: {ax}")
    
    # Datos de ejemplo
    x = np.linspace(0, 10, 100)
    y = np.sin(x)
    
    # Graficar en los ejes
    ax.plot(x, y, label='sin(x)')
    ax.set_xlabel('Tiempo (s)')
    ax.set_ylabel('Amplitud')
    ax.set_title('Onda sinusoidal')
    ax.legend()
    ax.grid(True, alpha=0.3)
    
    # Mostrar la figura
    plt.show()
    
    # 2. Múltiples figuras
    print("\n2. MÚLTIPLES FIGURAS:")
    
    # Crear dos figuras separadas
    fig1, ax1 = plt.subplots()
    fig2, ax2 = plt.subplots()
    
    # Graficar en cada figura
    ax1.plot(x, np.sin(x), 'b-', label='sin(x)')
    ax1.set_title('Figura 1: Seno')
    
    ax2.plot(x, np.cos(x), 'r-', label='cos(x)')
    ax2.set_title('Figura 2: Coseno')
    
    # Ajustar layout
    fig1.tight_layout()
    fig2.tight_layout()
    
    plt.show()
    
    # 3. Guardar figuras
    print("\n3. GUARDAR FIGURAS:")
    
    fig, ax = plt.subplots()
    ax.plot(x, np.exp(-x/5) * np.sin(x), 'g-', linewidth=2)
    ax.set_xlabel('Tiempo')
    ax.set_ylabel('Amplitud')
    ax.set_title('Oscilación amortiguada')
    ax.grid(True, alpha=0.3)
    
    # Guardar en diferentes formatos
    fig.savefig('oscilacion_amortiguada.png', dpi=300, bbox_inches='tight')
    fig.savefig('oscilacion_amortiguada.pdf', bbox_inches='tight')
    fig.savefig('oscilacion_amortiguada.svg', bbox_inches='tight')
    
    print("  Figuras guardadas como PNG, PDF y SVG")
    
    # 4. Propiedades de figura y ejes
    print("\n4. PROPIEDADES DE FIGURA Y EJES:")
    
    fig, ax = plt.subplots(figsize=(8, 4))  # Tamaño personalizado
    
    # Configurar propiedades de ejes
    ax.set_xlim(0, 10)          # Límites del eje X
    ax.set_ylim(-1.5, 1.5)      # Límites del eje Y
    ax.set_xlabel('Eje X', fontsize=12, fontweight='bold')
    ax.set_ylabel('Eje Y', fontsize=12, fontweight='bold')
    ax.set_title('Gráfico con propiedades personalizadas', fontsize=14)
    
    # Añadir texto en coordenadas específicas
    ax.text(5, 1.0, 'Punto de interés', fontsize=10, 
            ha='center', va='center', 
            bbox=dict(boxstyle='round', facecolor='wheat', alpha=0.8))
    
    # Añadir anotación con flecha
    ax.annotate('Máximo local', xy=(np.pi/2, 1), xytext=(3, 1.3),
                arrowprops=dict(arrowstyle='->', color='red', lw=2),
                fontsize=10, color='red')
    
    # Graficar datos
    ax.plot(x, np.sin(x), 'b-', linewidth=2, label='sin(x)')
    ax.plot(x, np.cos(x), 'r--', linewidth=2, label='cos(x)')
    
    # Añadir leyenda
    ax.legend(loc='upper right', fontsize=10)
    
    # Añadir cuadrícula
    ax.grid(True, linestyle='--', alpha=0.5)
    
    # Ajustar márgenes
    plt.subplots_adjust(left=0.1, right=0.95, top=0.9, bottom=0.1)
    
    plt.show()
    
    # 5. Estilos predefinidos
    print("\n5. ESTILOS PREDEFINIDOS:")
    
    estilos = ['default', 'classic', 'ggplot', 'seaborn-v0_8', 'seaborn-v0_8-darkgrid']
    
    for estilo in estilos:
        plt.style.use(estilo)
        fig, ax = plt.subplots(figsize=(6, 4))
        ax.plot(x, np.sin(x), label='sin(x)')
        ax.plot(x, np.cos(x), label='cos(x)')
        ax.set_title(f'Estilo: {estilo}')
        ax.legend()
        ax.grid(True)
        plt.show()
    
    # Volver al estilo por defecto
    plt.style.use('default')

# Ejecutar demostración
demostracion_figuras_ejes()
```

### Estructura de Plots

```python
def estructura_completa_plots():
    """
    Demuestra la estructura completa de un plot científico.
    """
    
    print("ESTRUCTURA COMPLETA DE UN PLOT CIENTÍFICO")
    print("=" * 70)
    
    # Crear datos científicos de ejemplo
    # Simulación de un experimento de cinética química
    tiempo = np.linspace(0, 60, 100)  # 0 a 60 minutos, 100 puntos
    concentracion_a = 1.0 * np.exp(-0.05 * tiempo)  # Decaimiento exponencial
    concentracion_b = 1.0 - concentracion_a         # Producto formado
    
    # Crear figura con tamaño personalizado
    fig = plt.figure(figsize=(12, 8))
    
    # 1. Ejes principales (gráfico grande)
    ax_main = plt.subplot2grid((3, 3), (0, 0), colspan=2, rowspan=2)
    
    # Graficar datos principales
    line_a, = ax_main.plot(tiempo, concentracion_a, 'b-', linewidth=2.5, 
                          label='Reactivo A', marker='o', markersize=4)
    line_b, = ax_main.plot(tiempo, concentracion_b, 'r-', linewidth=2.5, 
                          label='Producto B', marker='s', markersize=4)
    
    # Configurar ejes principales
    ax_main.set_xlabel('Tiempo (minutos)', fontsize=12, fontweight='bold')
    ax_main.set_ylabel('Concentración (M)', fontsize=12, fontweight='bold')
    ax_main.set_title('Cinética de Reacción: A → B', fontsize=14, fontweight='bold')
    ax_main.grid(True, linestyle='--', alpha=0.5)
    ax_main.legend(loc='upper right', fontsize=10)
    
    # Añadir anotaciones
    ax_main.annotate('Punto de equilibrio', 
                    xy=(30, 0.5), xytext=(40, 0.7),
                    arrowprops=dict(arrowstyle='->', color='green', lw=2),
                    fontsize=10, color='green',
                    bbox=dict(boxstyle='round', facecolor='white', alpha=0.8))
    
    # 2. Subplot 1: Gráfico semilogarítmico
    ax_semilog = plt.subplot2grid((3, 3), (0, 2))
    
    # Graficar en escala semilogarítmica
    ax_semilog.semilogy(tiempo, concentracion_a, 'b-', linewidth=1.5)
    ax_semilog.set_xlabel('Tiempo (min)')
    ax_semilog.set_ylabel('log(Concentración)')
    ax_semilog.set_title('Decaimiento exponencial\n(escala semilog)')
    ax_semilog.grid(True, linestyle=':', alpha=0.3)
    
    # 3. Subplot 2: Gráfico de velocidad instantánea
    ax_velocidad = plt.subplot2grid((3, 3), (1, 2))
    
    # Calcular velocidad (derivada numérica)
    velocidad = -np.gradient(concentracion_a, tiempo)
    
    ax_velocidad.plot(tiempo, velocidad, 'g-', linewidth=1.5)
    ax_velocidad.set_xlabel('Tiempo (min)')
    ax_velocidad.set_ylabel('Velocidad (M/min)')
    ax_velocidad.set_title('Velocidad instantánea')
    ax_velocidad.grid(True, linestyle=':', alpha=0.3)
    
    # 4. Subplot 3: Histograma de velocidades
    ax_hist = plt.subplot2grid((3, 3), (2, 0), colspan=2)
    
    ax_hist.hist(velocidad, bins=20, color='orange', edgecolor='black', alpha=0.7)
    ax_hist.set_xlabel('Velocidad (M/min)')
    ax_hist.set_ylabel('Frecuencia')
    ax_hist.set_title('Distribución de velocidades')
    ax_hist.grid(True, linestyle=':', alpha=0.3)
    
    # Añadir línea de media
    media_vel = np.mean(velocidad)
    ax_hist.axvline(media_vel, color='red', linestyle='--', linewidth=2, 
                   label=f'Media: {media_vel:.3f}')
    ax_hist.legend()
    
    # 5. Subplot 4: Texto con información
    ax_text = plt.subplot2grid((3, 3), (2, 2))
    
    # Ocultar ejes
    ax_text.axis('off')
    
    # Información del experimento
    info_text = """
    EXPERIMENTO: Cinética A → B
    
    Condiciones:
    • Temperatura: 25°C
    • pH: 7.0
    • [A] inicial: 1.0 M
    • Constante k: 0.05 min⁻¹
    
    Resultados:
    • t½ (vida media): 13.86 min
    • Equilibrio (~5t½): 69.3 min
    • [B] final: 1.0 M
    
    Métodos:
    • Espectrofotometría UV-Vis
    • Muestreo cada 0.6 min
    • n = 3 réplicas
    """
    
    ax_text.text(0.05, 0.95, info_text, fontsize=9, 
                verticalalignment='top',
                bbox=dict(boxstyle='round', facecolor='lightblue', alpha=0.5))
    
    # 6. Ajustar layout
    plt.suptitle('ANÁLISIS COMPLETO DE CINÉTICA QUÍMICA', 
                fontsize=16, fontweight='bold', y=0.98)
    
    plt.tight_layout(rect=[0, 0, 1, 0.96])  # Ajustar para el título superior
    
    # 7. Guardar figura
    fig.savefig('analisis_cinetica_completo.png', dpi=300, bbox_inches='tight')
    
    print("Gráfico científico completo creado y guardado como 'analisis_cinetica_completo.png'")
    plt.show()
    
    return fig

# Ejecutar demostración
figura_completa = estructura_completa_plots()
```

### `plt.show()` y `plt.savefig()`

```python
def manejo_visualizacion_guardado():
    """
    Demuestra el manejo de visualización y guardado de figuras.
    """
    
    print("MANEJO DE VISUALIZACIÓN Y GUARDADO")
    print("=" * 70)
    
    # 1. Diferentes modos de visualización
    print("1. MODOS DE VISUALIZACIÓN:")
    
    # Crear datos de ejemplo
    x = np.linspace(0, 10, 50)
    y1 = np.sin(x)
    y2 = np.cos(x)
    
    # Modo interactivo (por defecto en notebooks)
    plt.ion()  # Modo interactivo ON
    fig, ax = plt.subplots()
    ax.plot(x, y1, 'b-', label='sin(x)')
    ax.set_title('Modo interactivo')
    plt.draw()
    plt.pause(0.1)  # Pausa breve para ver el gráfico
    
    print("  Modo interactivo activado")
    
    # Modo no interactivo (para scripts)
    plt.ioff()  # Modo interactivo OFF
    fig, ax = plt.subplots()
    ax.plot(x, y2, 'r-', label='cos(x)')
    ax.set_title('Modo no interactivo')
    
    print("  Modo no interactivo activado")
    
    # 2. Guardado con diferentes opciones
    print("\n2. OPCIONES DE GUARDADO:")
    
    # Crear figura de ejemplo
    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))
    
    # Gráfico 1: Datos con ruido
    np.random.seed(42)
    x_noise = np.linspace(0, 10, 100)
    y_noise = np.sin(x_noise) + np.random.normal(0, 0.1, 100)
    
    ax1.scatter(x_noise, y_noise, alpha=0.6, label='Datos experimentales')
    ax1.plot(x_noise, np.sin(x_noise), 'r-', linewidth=2, label='Modelo teórico')
    ax1.set_xlabel('Variable independiente')
    ax1.set_ylabel('Variable dependiente')
    ax1.set_title('Datos con ajuste')
    ax1.legend()
    ax1.grid(True, alpha=0.3)
    
    # Gráfico 2: Histograma
    datos_normales = np.random.normal(0, 1, 1000)
    ax2.hist(datos_normales, bins=30, density=True, alpha=0.7, 
            color='green', edgecolor='black')
    
    # Añadir curva normal teórica
    from scipy.stats import norm
    x_norm = np.linspace(-4, 4, 100)
    ax2.plot(x_norm, norm.pdf(x_norm, 0, 1), 'r-', linewidth=2, 
            label='Distribución normal')
    
    ax2.set_xlabel