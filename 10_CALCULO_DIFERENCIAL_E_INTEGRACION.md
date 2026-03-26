# MÓDULO 10: CÁLCULO DIFERENCIAL E INTEGRACIÓN
## Herramientas Matemáticas para Modelado Científico

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Calcular derivadas numéricas para análisis de tasas de cambio
2. Implementar y analizar diferentes funciones matemáticas
3. Aplicar técnicas de optimización para problemas científicos
4. Realizar operaciones de álgebra lineal con matrices
5. Resolver sistemas de ecuaciones lineales
6. Aplicar descomposición de valores y vectores propios

---

## 10.1 Derivadas

### Concepto: La Derivada en Ciencias

La derivada representa la **tasa de cambio instantánea** de una función. En ciencia, esto se traduce en:
- **Velocidad** = derivada de la posición respecto al tiempo
- **Aceleración** = derivada de la velocidad respecto al tiempo
- **Tasa de reacción** = derivada de la concentración respecto al tiempo
- **Gradiente de temperatura** = derivada de la temperatura respecto a la posición

### Derivada Numérica

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.misc import derivative

def demostracion_derivadas_numericas():
    """
    Demuestra el cálculo de derivadas numéricas para aplicaciones científicas.
    """
    
    print("DERIVADAS NUMÉRICAS PARA CIENCIA")
    print("=" * 70)
    
    # 1. Derivada usando diferencias finitas
    print("1. DIFERENCIAS FINITAS:")
    
    def f(x):
        """Función de ejemplo: f(x) = x²"""
        return x**2
    
    # Punto donde calcular la derivada
    x0 = 2.0
    
    # Diferencia hacia adelante
    h = 0.001
    derivada_adelante = (f(x0 + h) - f(x0)) / h
    
    # Diferencia hacia atrás
    derivada_atras = (f(x0) - f(x0 - h)) / h
    
    # Diferencia central (más precisa)
    derivada_central = (f(x0 + h) - f(x0 - h)) / (2 * h)
    
    # Derivada exacta: f'(x) = 2x, f'(2) = 4
    derivada_exacta = 2 * x0
    
    print(f"  f(x) = x², f'({x0}) = 2*{x0} = {derivada_exacta}")
    print(f"  Diferencia hacia adelante: {derivada_adelante:.6f} (error: {abs(derivada_adelante - derivada_exacta):.6f})")
    print(f"  Diferencia hacia atrás:    {derivada_atras:.6f} (error: {abs(derivada_atras - derivada_exacta):.6f})")
    print(f"  Diferencia central:        {derivada_central:.6f} (error: {abs(derivada_central - derivada_exacta):.6f})")
    
    # 2. Derivada de funciones más complejas
    print("\n2. DERIVADAS DE FUNCIONES COMPLEJAS:")
    
    def funcion_compleja(x):
        """f(x) = sin(x) * exp(-x/5)"""
        return np.sin(x) * np.exp(-x/5)
    
    def derivada_exacta_compleja(x):
        """f'(x) = cos(x)*exp(-x/5) - (1/5)*sin(x)*exp(-x/5)"""
        return np.cos(x) * np.exp(-x/5) - (1/5) * np.sin(x) * np.exp(-x/5)
    
    # Calcular derivada en múltiples puntos
    x_vals = np.linspace(0, 20, 5)
    
    print(f"  f(x) = sin(x) * exp(-x/5)")
    print(f"  {'x':>6} {'f(x)':>12} {'f\'(x) numérica':>18} {'f\'(x) exacta':>18} {'Error':>10}")
    print(f"  {'-'*6} {'-'*12} {'-'*18} {'-'*18} {'-'*10}")
    
    for x in x_vals:
        # Derivada numérica usando diferencia central
        h = 0.0001
        derivada_num = (funcion_compleja(x + h) - funcion_compleja(x - h)) / (2 * h)
        
        # Derivada exacta
        derivada_exacta = derivada_exacta_compleja(x)
        
        # Error
        error = abs(derivada_num - derivada_exacta)
        
        print(f"  {x:6.2f} {funcion_compleja(x):12.6f} {derivada_num:18.6f} {derivada_exacta:18.6f} {error:10.6f}")
    
    # 3. Derivadas parciales (funciones multivariables)
    print("\n3. DERIVADAS PARCIALES:")
    
    def f_xy(x, y):
        """Función de dos variables: f(x,y) = x² + y² + x*y"""
        return x**2 + y**2 + x*y
    
    # Punto donde calcular derivadas parciales
    x0, y0 = 1.0, 2.0
    
    # Derivada parcial respecto a x
    h = 0.0001
    df_dx = (f_xy(x0 + h, y0) - f_xy(x0 - h, y0)) / (2 * h)
    
    # Derivada parcial respecto a y
    df_dy = (f_xy(x0, y0 + h) - f_xy(x0, y0 - h)) / (2 * h)
    
    # Gradiente (vector de derivadas parciales)
    gradiente = np.array([df_dx, df_dy])
    
    print(f"  f(x,y) = x² + y² + x*y")
    print(f"  Punto: (x,y) = ({x0}, {y0})")
    print(f"  ∂f/∂x = 2x + y = {2*x0 + y0:.6f} (numérico: {df_dx:.6f})")
    print(f"  ∂f/∂y = 2y + x = {2*y0 + x0:.6f} (numérico: {df_dy:.6f})")
    print(f"  Gradiente: {gradiente}")
    
    # 4. Aplicación: Velocidad y aceleración a partir de posición
    print("\n4. APLICACIÓN: CINEMÁTICA:")
    
    # Datos de posición vs tiempo (simulados)
    tiempo = np.linspace(0, 10, 100)
    posicion = 2 * tiempo + 0.5 * 9.8 * tiempo**2  # Movimiento con aceleración constante
    
    # Calcular velocidad (primera derivada)
    velocidad = np.gradient(posicion, tiempo)
    
    # Calcular aceleración (segunda derivada)
    aceleracion = np.gradient(velocidad, tiempo)
    
    print(f"  Movimiento: posición = 2t + 0.5*9.8*t²")
    print(f"  Velocidad teórica: v(t) = 2 + 9.8*t")
    print(f"  Aceleración teórica: a(t) = 9.8 m/s²")
    print(f"\n  Resultados numéricos:")
    print(f"    Velocidad media: {np.mean(velocidad):.3f} m/s")
    print(f"    Aceleración media: {np.mean(aceleracion):.3f} m/s²")
    print(f"    Error en aceleración: {abs(np.mean(aceleracion) - 9.8):.6f} m/s²")
    
    # 5. Visualización de derivadas
    print("\n5. VISUALIZACIÓN DE DERIVADAS:")
    
    # Crear figura
    fig, axes = plt.subplots(2, 2, figsize=(12, 10))
    
    # Función y su derivada
    x = np.linspace(0, 2*np.pi, 100)
    y = np.sin(x)
    y_prime = np.cos(x)  # Derivada exacta de sin(x)
    
    # Derivada numérica
    y_prime_num = np.gradient(y, x)
    
    # Gráfico 1: Función original
    axes[0, 0].plot(x, y, 'b-', linewidth=2, label='f(x) = sin(x)')
    axes[0, 0].set_xlabel('x')
    axes[0, 0].set_ylabel('f(x)')
    axes[0, 0].set_title('Función original')
    axes[0, 0].grid(True, alpha=0.3)
    axes[0, 0].legend()
    
    # Gráfico 2: Derivada exacta vs numérica
    axes[0, 1].plot(x, y_prime, 'r-', linewidth=2, label="f'(x) = cos(x) (exacta)")
    axes[0, 1].plot(x, y_prime_num, 'g--', linewidth=2, label="f'(x) (numérica)")
    axes[0, 1].set_xlabel('x')
    axes[0, 1].set_ylabel("f'(x)")
    axes[0, 1].set_title('Derivada exacta vs numérica')
    axes[0, 1].grid(True, alpha=0.3)
    axes[0, 1].legend()
    
    # Gráfico 3: Error
    error = np.abs(y_prime - y_prime_num)
    axes[1, 0].plot(x, error, 'm-', linewidth=2)
    axes[1, 0].set_xlabel('x')
    axes[1, 0].set_ylabel('Error absoluto')
    axes[1, 0].set_title('Error en derivada numérica')
    axes[1, 0].grid(True, alpha=0.3)
    axes[1, 0].set_yscale('log')  # Escala logarítmica para mejor visualización
    
    # Gráfico 4: Función y su derivada juntas
    axes[1, 1].plot(x, y, 'b-', linewidth=2, label='f(x)')
    axes[1, 1].plot(x, y_prime, 'r-', linewidth=2, label="f'(x)")
    axes[1, 1].set_xlabel('x')
    axes[1, 1].set_ylabel('Valor')
    axes[1, 1].set_title('Función y su derivada')
    axes[1, 1].grid(True, alpha=0.3)
    axes[1, 1].legend()
    
    plt.suptitle('ANÁLISIS DE DERIVADAS NUMÉRICAS', fontsize=14, fontweight='bold')
    plt.tight_layout()
    plt.show()
    
    return tiempo, posicion, velocidad, aceleracion

# Ejecutar demostración
tiempo, posicion, velocidad, aceleracion = demostracion_derivadas_numericas()
```

### Aplicaciones: Tasas de Cambio

```python
def aplicaciones_tasas_cambio():
    """
    Aplicaciones prácticas de derivadas en problemas científicos.
    """
    
    print("APLICACIONES DE DERIVADAS: TASAS DE CAMBIO")
    print("=" * 70)
    
    # 1. Cinética química: Tasa de reacción
    print("1. CINÉTICA QUÍMICA:")
    
    # Datos de concentración vs tiempo (reacción de primer orden)
    tiempo_quimica = np.linspace(0, 100, 200)  # 0 a 100 segundos
    k = 0.05  # Constante de velocidad (s⁻¹)
    C0 = 1.0  # Concentración inicial (M)
    
    # Concentración: C(t) = C0 * exp(-k*t)
    concentracion = C0 * np.exp(-k * tiempo_quimica)
    
    # Tasa de reacción: dC/dt = -k * C0 * exp(-k*t) = -k * C(t)
    tasa_reaccion = -k * concentracion
    
    # Tasa numérica (para comparación)
    tasa_numerica = np.gradient(concentracion, tiempo_quimica)
    
    print(f"  Reacción de primer orden: A → productos")
    print(f"  C(t) = {C0} * exp(-{k}*t)")
    print(f"  dC/dt = -{k} * C(t)")
    print(f"\n  Resultados en t=50s:")
    print(f"    Concentración: {C0*np.exp(-k*50):.6f} M")
    print(f"    Tasa teórica: {-k * C0 * np.exp(-k*50):.6f} M/s")
    print(f"    Tasa numérica: {tasa_numerica[100]:.6f} M/s")
    print(f"    Error: {abs(tasa_numerica[100] - (-k * C0 * np.exp(-k*50))):.6f} M/s")
    
    # Vida media: t½ = ln(2)/k
    t_media = np.log(2) / k
    print(f"\n  Vida media teórica: {t_media:.2f} s")
    
    # Encontrar vida media numéricamente
    idx_media = np.argmin(np.abs(concentracion - C0/2))
    t_media_num = tiempo_quimica[idx_media]
    print(f"  Vida media numérica: {t_media_num:.2f} s")
    print(f"  Error en vida media: {abs(t_media_num - t_media):.4f} s")
    
    # 2. Crecimiento poblacional
    print("\n2. CRECIMIENTO POBLACIONAL:")
    
    # Modelo logístico: dP/dt = r*P*(1 - P/K)
    tiempo_bio = np.linspace(0, 50, 200)  # 0 a 50 unidades de tiempo
    r = 0.1    # Tasa de crecimiento intrínseca
    K = 1000   # Capacidad de carga
    P0 = 10    # Población inicial
    
    # Solución analítica del modelo logístico
    # P(t) = K / (1 + ((K - P0)/P0) * exp(-r*t))
    poblacion = K / (1 + ((K - P0)/P0) * np.exp(-r * tiempo_bio))
    
    # Tasa de crecimiento: dP/dt
    tasa_crecimiento = r * poblacion * (1 - poblacion/K)
    
    # Tasa numérica
    tasa_crecimiento_num = np.gradient(poblacion, tiempo_bio)
    
    print(f"  Modelo logístico: dP/dt = {r}*P*(1 - P/{K})")
    print(f"  P0 = {P0}, K = {K}")
    print(f"\n  Resultados en t=25:")
    print(f"    Población: {poblacion[100]:.1f} individuos")
    print(f"    Tasa teórica: {tasa_crecimiento[100]:.3f} ind/ut")
    print(f"    Tasa numérica: {tasa_crecimiento_num[100]:.3f} ind/ut")
    
    # Punto de máxima tasa de crecimiento (d²P/dt² = 0)
    # En el modelo logístico, ocurre cuando P = K/2
    idx_max_crecimiento = np.argmax(tasa_crecimiento)
    t_max = tiempo_bio[idx_max_crecimiento]
    P_max = poblacion[idx_max_crecimiento]
    
    print(f"\n  Máxima tasa de crecimiento:")
    print(f"    Ocurre en t = {t_max:.2f}")
    print(f"    Población en ese momento: {P_max:.1f} (K/2 = {K/2})")
    print(f"    Tasa máxima: {tasa_crecimiento[idx_max_crecimiento]:.3f} ind/ut")
    
    # 3. Transferencia de calor
    print("\n3. TRANSFERENCIA DE CALOR:")
    
    # Ley de enfriamiento de Newton: dT/dt = -k*(T - T_ambiente)
    tiempo_termo = np.linspace(0, 300, 300)  # 0 a 300 segundos
    k_termo = 0.02  # Constante de enfriamiento (s⁻¹)
    T0 = 100        # Temperatura inicial (°C)
    T_amb = 25      # Temperatura ambiente (°C)
    
    # Temperatura: T(t) = T_amb + (T0 - T_amb)*exp(-k*t)
    temperatura = T_amb + (T0 - T_amb) * np.exp(-k_termo * tiempo_termo)
    
    # Tasa de enfriamiento: d