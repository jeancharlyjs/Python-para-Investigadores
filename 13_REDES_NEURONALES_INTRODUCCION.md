# MÓDULO 13: REDES NEURONALES INTRODUCCIÓN
## Fundamentos de Aprendizaje Profundo para Ciencia

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Comprender la estructura básica de una neurona artificial
2. Implementar forward propagation en redes neuronales
3. Entender el concepto de backpropagation y gradiente descendente
4. Diseñar arquitecturas de redes neuronales para problemas científicos
5. Configurar hiperparámetros para entrenamiento eficiente
6. Implementar funciones de pérdida apropiadas para diferentes tareas

---

## 13.1 Conceptos Básicos

### Concepto: ¿Qué es una Red Neuronal Artificial?

Una red neuronal artificial es un modelo computacional inspirado en el **cerebro biológico**. Consiste en unidades interconectadas (neuronas) que procesan información. En ciencia, las redes neuronales se utilizan para:
- **Modelar relaciones complejas** no lineales en datos
- **Predecir propiedades** de moléculas y materiales
- **Analizar imágenes** médicas y científicas
- **Procesar secuencias** de ADN y proteínas

### Neurona Artificial: La Unidad Básica

```python
import numpy as np
import matplotlib.pyplot as plt

def demostracion_neurona_artificial():
    """
    Demuestra el funcionamiento de una neurona artificial.
    """
    
    print("NEURONA ARTIFICIAL - UNIDAD BÁSICA")
    print("=" * 70)
    
    # 1. Estructura de una neurona artificial
    print("1. ESTRUCTURA DE UNA NEURONA ARTIFICIAL:")
    
    class NeuronaArtificial:
        """Implementación de una neurona artificial simple."""
        
        def __init__(self, n_inputs, activation='sigmoid'):
            """
            Inicializa una neurona artificial.
            
            Parámetros:
            -----------
            n_inputs : int
                Número de entradas
            activation : str
                Función de activación ('sigmoid', 'relu', 'tanh')
            """
            # Inicializar pesos aleatoriamente
            self.weights = np.random.randn(n_inputs) * 0.1
            self.bias = np.random.randn() * 0.1
            self.activation = activation
            
            # Historial para visualización
            self.inputs_history = []
            self.output_history = []
            self.activation_history = []
        
        def activacion(self, x):
            """Aplica función de activación."""
            if self.activation == 'sigmoid':
                return 1 / (1 + np.exp(-x))
            elif self.activation == 'relu':
                return np.maximum(0, x)
            elif self.activation == 'tanh':
                return np.tanh(x)
            else:
                return x  # Linear (sin activación)
        
        def forward(self, inputs):
            """
            Propagación hacia adelante.
            
            Parámetros:
            -----------
            inputs : array-like
                Vector de entradas
            
            Retorna:
            --------
            float
                Salida de la neurona
            """
            # Guardar entradas para visualización
            self.inputs_history.append(inputs.copy())
            
            # Calcular suma ponderada
            z = np.dot(inputs, self.weights) + self.bias
            
            # Aplicar función de activación
            a = self.activacion(z)
            
            # Guardar para visualización
            self.output_history.append(a)
            self.activation_history.append(self.activation)
            
            return a
        
        def __str__(self):
            """Representación en string de la neurona."""
            return f"Neurona({len(self.weights)} inputs, activación={self.activation})"
    
    # 2. Crear y probar diferentes neuronas
    print("\n2. EJEMPLOS DE NEURONAS:")
    
    # Neurona con 3 entradas y activación sigmoid
    neurona_sigmoid = NeuronaArtificial(n_inputs=3, activation='sigmoid')
    print(f"  {neurona_sigmoid}")
    print(f"    Pesos: {neurona_sigmoid.weights}")
    print(f"    Bias: {neurona_sigmoid.bias:.4f}")
    
    # Neurona con 2 entradas y activación ReLU
    neurona_relu = NeuronaArtificial(n_inputs=2, activation='relu')
    print(f"\n  {neurona_relu}")
    print(f"    Pesos: {neurona_relu.weights}")
    print(f"    Bias: {neurona_relu.bias:.4f}")
    
    # 3. Propagación hacia adelante
    print("\n3. PROPAGACIÓN HACIA ADELANTE (FORWARD PASS):")
    
    # Entradas de ejemplo
    inputs_sigmoid = np.array([0.5, -0.2, 0.8])
    inputs_relu = np.array([1.0, -0.5])
    
    # Calcular salidas
    output_sigmoid = neurona_sigmoid.forward(inputs_sigmoid)
    output_relu = neurona_relu.forward(inputs_relu)
    
    print(f"  Neurona Sigmoid:")
    print(f"    Entradas: {inputs_sigmoid}")
    print(f"    z = w·x + b = {np.dot(inputs_sigmoid, neurona_sigmoid.weights):.4f} + {neurona_sigmoid.bias:.4f}")
    print(f"    z = {np.dot(inputs_sigmoid, neurona_sigmoid.weights) + neurona_sigmoid.bias:.4f}")
    print(f"    a = σ(z) = {output_sigmoid:.4f}")
    
    print(f"\n  Neurona ReLU:")
    print(f"    Entradas: {inputs_relu}")
    print(f"    z = w·x + b = {np.dot(inputs_relu, neurona_relu.weights):.4f} + {neurona_relu.bias:.4f}")
    print(f"    z = {np.dot(inputs_relu, neurona_relu.weights) + neurona_relu.bias:.4f}")
    print(f"    a = ReLU(z) = {output_relu:.4f}")
    
    # 4. Visualización de la neurona
    print("\n4. VISUALIZACIÓN DE LA NEURONA:")
    
    # Crear figura
    fig, axes = plt.subplots(1, 2, figsize=(12, 5))
    
    # Gráfico 1: Esquema de la neurona
    ax1 = axes[0]
    ax1.axis('off')
    
    # Dibujar neurona
    circle = plt.Circle((0.5, 0.5), 0.4, color='lightblue', ec='black', lw=2)
    ax1.add_patch(circle)
    
    # Entradas
    for i in range(3):
        y_pos = 0.3 + i * 0.2
        ax1.plot([0.1, 0.3], [y_pos, y_pos], 'k-', lw=2)
        ax1.text(0.05, y_pos, f'x{i+1}', fontsize=12, va='center')
        ax1.text(0.15, y_pos + 0.02, f'w{i+1}', fontsize=10, color='blue')
    
    # Suma
    ax1.text(0.5, 0.5, 'Σ', fontsize=24, ha='center', va='center')
    ax1.text(0.5, 0.4, '+b', fontsize=12, ha='center', va='center')
    
    # Activación
    ax1.text(0.5, 0.3, 'σ(z)', fontsize=12, ha='center', va='center', 
            bbox=dict(boxstyle='round', facecolor='yellow', alpha=0.5))
    
    # Salida
    ax1.plot([0.7, 0.9], [0.5, 0.5], 'k-', lw=2)
    ax1.text(0.95, 0.5, 'a', fontsize=12, va='center')
    
    ax1.set_xlim(0, 1)
    ax1.set_ylim(0, 1)
    ax1.set_title('Esquema de Neurona Artificial', fontsize=14)
    
    # Gráfico 2: Proceso de cálculo
    ax2 = axes[1]
    
    # Datos para el proceso
    x_vals = np.linspace(-3, 3, 100)
    
    # Funciones de activación
    sigmoid_vals = 1 / (1 + np.exp(-x_vals))
    relu_vals = np.maximum(0, x_vals)
    tanh_vals = np.tanh(x_vals)
    
    ax2.plot(x_vals, sigmoid_vals, 'b-', lw=2, label='Sigmoid')
    ax2.plot(x_vals, relu_vals, 'r-', lw=2, label='ReLU')
    ax2.plot(x_vals, tanh_vals, 'g-', lw=2, label='Tanh')
    ax2.plot(x_vals, x_vals, 'k--', lw=1, alpha=0.5, label='Linear')
    
    # Marcar punto de operación de nuestras neuronas
    z_sigmoid = np.dot(inputs_sigmoid, neurona_sigmoid.weights) + neurona_sigmoid.bias
    z_relu = np.dot(inputs_relu, neurona_relu.weights) + neurona_relu.bias
    
    ax2.scatter([z_sigmoid], [output_sigmoid], color='blue', s=100, 
               edgecolors='black', zorder=5, label=f'Sigmoid: z={z_sigmoid:.2f}')
    ax2.scatter([z_relu], [output_relu], color='red', s=100, 
               edgecolors='black', zorder=5, label=f'ReLU: z={z_relu:.2f}')
    
    ax2.set_xlabel('z (suma ponderada + bias)')
    ax2.set_ylabel('a (activación)')
    ax2.set_title('Funciones de Activación')
    ax2.grid(True, alpha=0.3)
    ax2.legend()
    
    plt.suptitle('NEURONA ARTIFICIAL - CONCEPTOS BÁSICOS', fontsize=16, fontweight='bold')
    plt.tight_layout()
    plt.show()
    
    # 5. Ejemplo científico: Detección de anomalías
    print("\n5. EJEMPLO CIENTÍFICO: DETECCIÓN DE ANOMALÍAS")
    
    # Simular datos de sensores
    np.random.seed(42)
    n_muestras = 100
    
    # Datos normales (media 0, desviación 1)
    datos_normales = np.random.normal(0, 1, (n_muestras, 3))
    
    # Datos anómalos (media diferente)
    datos_anomalos = np.random.normal(3, 1, (10, 3))
    
    # Combinar datos
    X = np.vstack([datos_normales, datos_anomalos])
    y = np.array([0] * n_muestras + [1] * 10)  # 0=normal, 1=anómalo
    
    print(f"  Datos de sensores simulados:")
    print(f"    Muestras normales: {n_muestras}")
    print(f"    Muestras anómalas: {10}")
    print(f"    Características por muestra: {X.shape[1]}")
    
    # Crear neurona para detección de anomalías
    neurona_deteccion = NeuronaArtificial(n_inputs=3, activation='sigmoid')
    
    # Entrenar simple (solo para demostración)
    print(f"\n  Entrenamiento simplificado:")
    
    # Pesos "ideales" para detectar valores altos
    neurona_deteccion.weights = np.array([0.5, 0.5, 0.5])  # Pesos positivos
    neurona_deteccion.bias = -1.5  # Bias negativo para activar solo con valores altos
    
    # Probar con ejemplos
    ejemplo_normal = np.array([0.1, -0.2, 0.3])
    ejemplo_anomalo = np.array([3.5, 2.8, 4.1])
    
    prob_normal = neurona_deteccion.forward(ejemplo_normal)
    prob_anomalo = neurona_deteccion.forward(ejemplo_anomalo)
    
    print(f"    Ejemplo normal: {ejemplo_normal}")
    print(f"      Probabilidad de anomalía: {prob_normal:.4f}")
    print(f"      Clasificación: {'Normal' if prob_normal < 0.5 else 'Anómalo'}")
    
    print(f"\n    Ejemplo anómalo: {ejemplo_anomalo}")
    print(f"      Probabilidad de anomalía: {prob_anomalo:.4f}")
    print(f"      Clasificación: {'Normal' if prob_anomalo < 0.5 else 'Anómalo'}")
    
    return neurona_sigmoid, neurona_relu, neurona_deteccion

# Ejecutar demostración
neurona_sigmoid, neurona_relu, neurona_deteccion = demostracion_neurona_artificial()
```

### Pesos y Sesgos

```python
def demostracion_pesos_sesgos():
    """
    Demuestra el papel de pesos y sesgos en neuronas artificiales.
    """
    
    print("PESOS Y SESGOS - PARÁMETROS APRENDIBLES")
    print("=" * 70)
    
    import numpy as np
    import matplotlib.pyplot as plt
    
    # 1. Definición de funciones de ayuda
    def neurona_forward(inputs, weights, bias, activation='sigmoid'):
        """Propagación hacia adelante de una neurona."""
        z = np.dot(inputs, weights) + bias
        
        if activation == 'sigmoid':
            return 1 / (1 + np.exp(-z))
        elif activation == 'relu':
            return np.maximum(0, z)
        elif activation == 'tanh':
            return np.tanh(z)
        else:
            return z
    
    # 2. Efecto de los pesos
    print("1. EFECTO DE LOS PESOS:")
    
    # Entrada fija
    x = np.array([1.0, 0.5])
    
    # Diferentes configuraciones de pesos
    configuraciones_pesos = [
        {'nombre': 'Pesos pequeños', 'weights': np.array([0.1, 0.1]), 'bias': 0},
        {'nombre': 'Pesos balanceados', 'weights': np.array([0.5, -0.5]), 'bias': 0},
        {'nombre': 'Pesos grandes', 'weights': np.array([2.0, 1.5]), 'bias': 0},
        {'nombre': 'Pesos opuestos', 'weights': np.array([1.0, -2.0]), 'bias': 0},
    ]
    
    print(f"\n  Entrada: x = {x}")
    print(f"  {'Configuración':<20} {'Pesos':<15} {'z = w·x':<10} {'σ(z)':<10}")
    print(f"  {'-'*20} {'-'*15} {'-'*10} {'-'*10}")
    
    for config in configuraciones_pesos:
        z = np.dot(x, config['weights']) + config['bias']
        a = neurona_forward(x, config['weights'], config['bias'], 'sigmoid')
        print(f"  {config['nombre']:<20} {str(config['weights']):<15} {z:10.3f} {a:10.3f}")
    
    # 3. Efecto del bias
    print("\n2. EFECTO DEL BIAS:")
    
    # Pesos fijos
    weights_fijos = np.array([0.5, 0.5])
    
    # Diferentes biases
    configuraciones_bias = [
        {'nombre': 'Bias negativo grande', 'bias': -2.0},
        {'nombre': 'Bias negativo pequeño', 'bias': -0.5},
        {'nombre': 'Sin bias', 'bias': 0.0},
        {'nombre': 'Bias positivo pequeño', 'bias': 0.5},
        {'nombre': 'Bias positivo grande', 'bias': 2.0},
    ]
    
    print(f"\n  Pesos fijos: w = {weights_fijos}")
    print(f"  Entrada: x = {x}")
    print(f"  {'Configuración':<25} {'Bias':<10} {'z = w·x + b':<12} {'σ(z)':<10}")
    print(f"  {'-'*25} {'-'*10} {'-'*12} {'-'*10}")
    
    for config in configuraciones_bias:
        z = np.dot(x, weights_fijos) + config['bias']
        a = neurona_forward(x, weights_fijos, config['bias'], 'sigmoid')
        print(f"  {config['nombre']:<25} {config['bias