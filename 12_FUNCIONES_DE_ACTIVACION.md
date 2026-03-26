# MÓDULO 12: FUNCIONES DE ACTIVACIÓN
## No Linealidades para Redes Neuronales

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Comprender el papel de las funciones de activación en redes neuronales
2. Implementar y visualizar diferentes funciones de activación
3. Seleccionar la función de activación apropiada para diferentes problemas
4. Analizar las propiedades matemáticas de cada función
5. Aplicar funciones de activación en contextos científicos
6. Comprender problemas como vanishing/exploding gradients

---

## 12.1 Sigmoid

### Concepto: La Función Sigmoid

La función sigmoid (también llamada función logística) es una de las primeras funciones de activación utilizadas en redes neuronales. Transforma valores de entrada en el rango **(0, 1)**, lo que la hace ideal para problemas de **clasificación binaria** donde necesitamos interpretar la salida como una probabilidad.

### Definición Matemática

La función sigmoid se define como:

$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$

**Propiedades:**
- **Rango de salida:** (0, 1)
- **Función monótona:** Siempre creciente
- **Punto de saturación:** Se satura para valores extremos de x
- **Derivada simple:** $\sigma'(x) = \sigma(x)(1 - \sigma(x))$

### Implementación y Visualización

```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

def demostracion_sigmoid():
    """
    Demuestra la función sigmoid y sus propiedades.
    """
    
    print("FUNCIÓN SIGMOID (LOGÍSTICA)")
    print("=" * 70)
    
    # 1. Definición de la función
    def sigmoid(x):
        """Implementación de la función sigmoid."""
        return 1 / (1 + np.exp(-x))
    
    def sigmoid_derivada(x):
        """Derivada de la función sigmoid."""
        s = sigmoid(x)
        return s * (1 - s)
    
    # 2. Evaluación en diferentes puntos
    print("1. EVALUACIÓN EN PUNTOS CLAVE:")
    
    puntos_clave = [-10, -5, -2, -1, 0, 1, 2, 5, 10]
    
    print(f"\n  {'x':>6} {'σ(x)':>12} {'σ\'(x)':>12}")
    print(f"  {'-'*6} {'-'*12} {'-'*12}")
    
    for x in puntos_clave:
        s = sigmoid(x)
        s_prime = sigmoid_derivada(x)
        print(f"  {x:6.1f} {s:12.6f} {s_prime:12.6f}")
    
    # 3. Propiedades matemáticas
    print("\n2. PROPIEDADES MATEMÁTICAS:")
    
    # Rango
    x_test = np.array([-100, -10, 0, 10, 100])
    rango = sigmoid(x_test)
    print(f"  Rango: σ(x) ∈ ({rango.min():.10f}, {rango.max():.10f})")
    
    # Simetría
    x_sym = 2.0
    print(f"  σ({x_sym}) = {sigmoid(x_sym):.6f}")
    print(f"  1 - σ({-x_sym}) = {1 - sigmoid(-x_sym):.6f}")
    print(f"  ¿σ(x) = 1 - σ(-x)? {np.isclose(sigmoid(x_sym), 1 - sigmoid(-x_sym))}")
    
    # Punto de inflexión
    print(f"  σ(0) = {sigmoid(0):.6f} (punto medio)")
    print(f"  σ'(0) = {sigmoid_derivada(0):.6f} (máxima pendiente)")
    
    # 4. Visualización
    print("\n3. VISUALIZACIÓN:")
    
    # Crear datos para graficar
    x = np.linspace(-10, 10, 1000)
    y_sigmoid = sigmoid(x)
    y_derivada = sigmoid_derivada(x)
    
    # Crear figura
    fig, axes = plt.subplots(2, 2, figsize=(12, 10))
    
    # Gráfico 1: Función sigmoid
    axes[0, 0].plot(x, y_sigmoid, 'b-', linewidth=3, label='σ(x)')
    axes[0, 0].axhline(y=0.5, color='r', linestyle='--', alpha=0.5, label='y=0.5')
    axes[0, 0].axvline(x=0, color='g', linestyle='--', alpha=0.5, label='x=0')
    axes[0, 0].set_xlabel('x')
    axes[0, 0].set_ylabel('σ(x)')
    axes[0, 0].set_title('Función Sigmoid')
    axes[0, 0].grid(True, alpha=0.3)
    axes[0, 0].legend()
    axes[0, 0].set_ylim(-0.1, 1.1)
    
    # Gráfico 2: Derivada de sigmoid
    axes[0, 1].plot(x, y_derivada, 'r-', linewidth=3, label="σ'(x)")
    axes[0, 1].axvline(x=0, color='g', linestyle='--', alpha=0.5, label='x=0')
    axes[0, 1].set_xlabel('x')
    axes[0, 1].set_ylabel("σ'(x)")
    axes[0, 1].set_title('Derivada de Sigmoid')
    axes[0, 1].grid(True, alpha=0.3)
    axes[0, 1].legend()
    
    # Gráfico 3: Efecto de saturación
    x_sat = np.linspace(-20, 20, 1000)
    y_sat = sigmoid(x_sat)
    
    axes[1, 0].plot(x_sat, y_sat, 'b-', linewidth=3)
    axes[1, 0].axhline(y=0, color='r', linestyle='--', alpha=0.5, label='y=0')
    axes[1, 0].axhline(y=1, color='r', linestyle='--', alpha=0.5, label='y=1')
    axes[1, 0].fill_between(x_sat, 0, 0.01, alpha=0.3, color='red', label='Saturación inferior')
    axes[1, 0].fill_between(x_sat, 0.99, 1, alpha=0.3, color='red', label='Saturación superior')
    axes[1, 0].set_xlabel('x')
    axes[1, 0].set_ylabel('σ(x)')
    axes[1, 0].set_title('Efecto de Saturación')
    axes[1, 0].grid(True, alpha=0.3)
    axes[1, 0].legend()
    
    # Gráfico 4: Interpretación como probabilidad
    # Simular clasificación binaria
    np.random.seed(42)
    n_samples = 100
    x_clasif = np.random.randn(n_samples, 2)
    # Separar con una línea diagonal
    y_true = (x_clasif[:, 0] + x_clasif[:, 1] > 0).astype(int)
    
    # Aplicar sigmoid para obtener probabilidades
    scores = x_clasif[:, 0] + x_clasif[:, 1]
    probs = sigmoid(scores)
    
    scatter = axes[1, 1].scatter(x_clasif[:, 0], x_clasif[:, 1], 
                                c=probs, cmap='RdYlBu', s=50, 
                                edgecolors='black', alpha=0.8)
    axes[1, 1].set_xlabel('Característica 1')
    axes[1, 1].set_ylabel('Característica 2')
    axes[1, 1].set_title('Sigmoid como Probabilidad (Clasificación Binaria)')
    axes[1, 1].grid(True, alpha=0.3)
    
    # Añadir barra de color
    cbar = plt.colorbar(scatter, ax=axes[1, 1])
    cbar.set_label('Probabilidad P(y=1|x)')
    
    plt.suptitle('ANÁLISIS COMPLETO DE LA FUNCIÓN SIGMOID', 
                fontsize=14, fontweight='bold')
    plt.tight_layout()
    plt.show()
    
    # 5. Aplicación en regresión logística
    print("\n4. APLICACIÓN: REGRESIÓN LOGÍSTICA:")
    
    from sklearn.linear_model import LogisticRegression
    from sklearn.datasets import make_classification
    
    # Generar datos de clasificación binaria
    X, y = make_classification(
        n_samples=1000,
        n_features=2,
        n_informative=2,
        n_redundant=0,
        n_clusters_per_class=1,
        random_state=42
    )
    
    # Entrenar modelo de regresión logística
    model = LogisticRegression()
    model.fit(X, y)
    
    # Obtener probabilidades
    x_test_point = np.array([[0.5, 0.5]])
    proba = model.predict_proba(x_test_point)[0]
    
    print(f"  Punto de prueba: {x_test_point[0]}")
    print(f"  Probabilidad clase 0: {proba[0]:.4f}")
    print(f"  Probabilidad clase 1: {proba[1]:.4f}")
    print(f"  Clase predicha: {model.predict(x_test_point)[0]}")
    
    # 6. Problemas con sigmoid
    print("\n5. PROBLEMAS CON SIGMOID:")
    
    problemas = [
        ("Vanishing Gradient", 
         "Para |x| grandes, σ'(x) ≈ 0 → gradientes muy pequeños"),
        ("Output no zero-centered", 
         "Salidas siempre positivas (0,1) → gradientes siempre del mismo signo"),
        ("Computacionalmente costosa", 
         "Involucra exponenciales en forward y backward pass"),
        ("Saturación", 
         "Para |x| > 5, la función se satura → aprendizaje lento")
    ]
    
    print(f"  {'Problema':<25} {'Descripción'}")
    print(f"  {'-'*25} {'-'*40}")
    
    for problema, descripcion in problemas:
        print(f"  {problema:<25} {descripcion}")
    
    # Demostración de vanishing gradient
    print("\n  Demostración Vanishing Gradient:")
    x_large = np.array([-10, -5, 5, 10])
    gradients = sigmoid_derivada(x_large)
    
    for x_val, grad in zip(x_large, gradients):
        print(f"    σ'({x_val:3.0f}) = {grad:.10f}")
    
    return sigmoid, sigmoid_derivada

# Ejecutar demostración
sigmoid_func, sigmoid_deriv = demostracion_sigmoid()
```

### Casos de Uso: Clasificación Binaria

```python
def aplicacion_sigmoid_clasificacion():
    """
    Aplicación práctica de sigmoid en clasificación binaria.
    """
    
    print("APLICACIÓN PRÁCTICA: CLASIFICACIÓN BINARIA CON SIGMOID")
    print("=" * 70)
    
    import numpy as np
    import matplotlib.pyplot as plt
    from sklearn.datasets import make_classification
    from sklearn.model_selection import train_test_split
    from sklearn.preprocessing import StandardScaler
    
    # 1. Generar datos de diagnóstico médico
    print("1. DATOS DE DIAGNÓSTICO MÉDICO:")
    
    # Simular datos de pacientes: Edad y Nivel de glucosa vs Diabetes
    np.random.seed(42)
    n_pacientes = 500
    
    # Características
    edad = np.random.normal(50, 15, n_pacientes)
    glucosa = np.random.normal(100, 30, n_pacientes)
    
    # Función logística para probabilidad de diabetes
    # Probabilidad aumenta con edad y glucosa
    log_odds = -5 + 0.05 * edad + 0.03 * glucosa + np.random.normal(0, 0.5, n_pacientes)
    probabilidad = 1 / (1 + np.exp(-log_odds))
    
    # Generar etiquetas binarias
    diabetes = (probabilidad > 0.5).astype(int)
    
    # Crear DataFrame
    import pandas as pd
    datos = pd.DataFrame({
        'Edad': edad,
        'Glucosa': glucosa,
        'Probabilidad_Diabetes': probabilidad,
        'Diabetes': diabetes
    })
    
    print(f"  Número de pacientes: {n_pacientes}")
    print(f"  Pacientes con diabetes: {diabetes.sum()} ({diabetes.sum()/n_pacientes*100:.1f}%)")
    print(f"  Edad promedio: {edad.mean():.1f} ± {edad.std():.1f} años")
    print(f"  Glucosa promedio: {glucosa.mean():.1f} ± {glucosa.std():.1f} mg/dL")
    
    # 2. Implementación manual de regresión logística
    print("\n2. IMPLEMENTACIÓN MANUAL DE REGRESIÓN LOGÍSTICA:")
    
    def sigmoid(x):
        return 1 / (1 + np.exp(-x))
    
    class LogisticRegressionManual:
        """Implementación manual de regresión logística."""
        
        def __init__(self, learning_rate=0.01, n_iterations=1000):
            self.lr = learning_rate
            self.n_iter = n_iterations
            self.weights = None
            self.bias = None
            self.loss_history = []
        
        def fit(self, X, y):
            """Entrena el modelo usando gradiente descendente."""
            n_samples, n_features = X.shape
            
            # Inicializar parámetros
            self.weights = np.zeros(n_features)
            self.bias = 0
            
            # Gradiente descendente
            for iteration in range(self.n_iter):
                # Predicciones lineales
                linear_model = np.dot(X, self.weights) + self.bias
                y_pred = sigmoid(linear_model)
                
                # Calcular pérdida (log loss)
                loss = -np.mean(y * np.log(y_pred + 1e-15) + (1 - y) * np.log(1 - y_pred + 1e-15))
                self.loss_history.append(loss)
                
                # Calcular gradientes
                dw = (1 / n_samples) * np.dot(X.T, (y_pred - y))
                db = (1 / n_samples) * np.sum(y_pred - y)
                
                # Actualizar parámetros
                self.weights -= self.lr * dw
                self.bias -= self.lr * db
                
                # Mostrar progreso cada 100 iteraciones
                if iteration % 100 == 0:
                    print(f"    Iteración {iteration:4d}: Loss = {loss:.6f}")
            
            return self
        
        def predict_proba(self, X):
            """Retorna probabilidades predichas."""
            linear_model = np.dot(X, self.weights) + self.bias
            return sigmoid(linear_model)
        
        def predict(self, X, threshold=0.5):
            """Retorna predicciones binarias."""
            probas = self.predict_proba(X)
            return (probas >= threshold).astype(int)
    
    # 3. Preparar datos
    X = datos[['Edad', 'Glucosa']].values
    y = datos['Diabetes'].values
    
    # Normalizar características
    scaler = StandardScaler()
    X_scaled = scaler.fit_transform(X)
    
    # Dividir datos
    X_train, X_test, y_train, y_test = train_test_split(
        X_scaled, y, test_size=0.2, random_state=42
    )
    
    print(f"\n  División de datos:")
    print(f"    Train: {X_train.shape[0]} muestras")
    print(f"    Test:  {X_test.shape[0]} muestras")
    
    # 4. Entrenar modelo
    print("\n  Entrenando modelo...")
    model = LogisticRegressionManual(learning_rate=0.1, n_iterations=1000)
    model.fit(X_train, y_train)
    
    # 5. Evaluar modelo
    from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score
    
    y_pred = model.predict(X_test)
    y_pred_proba = model.predict_proba(X_test)
    
    accuracy = accuracy_score(y_test, y_pred)
    precision = precision_score(y_test, y_pred)
    recall = recall_score(y_test, y_pred)
    f1 = f1_score(y_test, y_pred)
    
    print(f"\n  Resultados en test set:")
    print