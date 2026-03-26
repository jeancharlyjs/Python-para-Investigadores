# MÓDULO 11: MACHINE LEARNING BASICS
## Fundamentos de Aprendizaje Automático para Ciencia

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Comprender los conceptos fundamentales de Machine Learning
2. Implementar regresión lineal para modelado predictivo
3. Realizar regresión múltiple con múltiples características
4. Evaluar modelos usando métricas apropiadas
5. Implementar clasificación con regresión logística
6. Aplicar validación cruzada para estimación robusta

---

## 11.1 Conceptos Fundamentales

### Concepto: ¿Qué es Machine Learning en Ciencia?

Machine Learning (ML) es el campo de estudio que permite a las computadoras **aprender de los datos** sin ser programadas explícitamente. En ciencia, ML se utiliza para:
- **Descubrir patrones** en datos experimentales
- **Predecir resultados** basados en variables de entrada
- **Clasificar muestras** en categorías
- **Optimizar procesos** experimentales

### Tipos de Aprendizaje

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

def introduccion_ml_cientifico():
    """
    Introducción a los conceptos fundamentales de ML para ciencia.
    """
    
    print("INTRODUCCIÓN A MACHINE LEARNING PARA CIENCIA")
    print("=" * 70)
    
    # 1. Tipos de aprendizaje
    print("1. TIPOS DE APRENDIZAJE:")
    
    tipos_aprendizaje = {
        'Supervisado': {
            'Descripción': 'Aprendizaje con etiquetas conocidas',
            'Ejemplos_cientificos': [
                'Predecir concentración a partir de absorbancia',
                'Clasificar células como sanas o cancerosas',
                'Estimar propiedades químicas a partir de estructura molecular'
            ],
            'Algoritmos': ['Regresión lineal', 'Regresión logística', 'SVM', 'Random Forest']
        },
        'No supervisado': {
            'Descripción': 'Aprendizaje sin etiquetas, descubriendo estructura',
            'Ejemplos_cientificos': [
                'Agrupar genes con expresión similar',
                'Reducir dimensionalidad de datos espectroscópicos',
                'Identificar patrones en series temporales'
            ],
            'Algoritmos': ['K-means', 'PCA', 'Autoencoders', 'DBSCAN']
        },
        'Por refuerzo': {
            'Descripción': 'Aprendizaje mediante interacción y recompensa',
            'Ejemplos_cientificos': [
                'Optimización de condiciones experimentales',
                'Control de reactores químicos',
                'Diseño automático de moléculas'
            ],
            'Algoritmos': ['Q-learning', 'Policy Gradient', 'Deep Q-Networks']
        }
    }
    
    for tipo, info in tipos_aprendizaje.items():
        print(f"\n  {tipo.upper()}:")
        print(f"    {info['Descripción']}")
        print(f"    Ejemplos científicos:")
        for ejemplo in info['Ejemplos_cientificos']:
            print(f"      • {ejemplo}")
        print(f"    Algoritmos comunes: {', '.join(info['Algoritmos'])}")
    
    # 2. Flujo de trabajo típico en ML científico
    print("\n2. FLUJO DE TRABAJO EN ML CIENTÍFICO:")
    
    pasos_ml = [
        ("1. Definición del problema", "¿Qué queremos predecir/clasificar?"),
        ("2. Recopilación de datos", "Datos experimentales, simulaciones, literatura"),
        ("3. Preprocesamiento", "Limpieza, normalización, manejo de valores faltantes"),
        ("4. Ingeniería de características", "Extracción/transformación de variables relevantes"),
        ("5. División de datos", "Train/validation/test sets"),
        ("6. Selección de modelo", "Elección del algoritmo apropiado"),
        ("7. Entrenamiento", "Ajuste de parámetros del modelo"),
        ("8. Evaluación", "Métricas de desempeño en datos no vistos"),
        ("9. Interpretación", "Análisis de importancia de características"),
        ("10. Despliegue", "Implementación para predicciones nuevas")
    ]
    
    for paso, descripcion in pasos_ml:
        print(f"  {paso:<30} {descripcion}")
    
    # 3. Conceptos clave
    print("\n3. CONCEPTOS CLAVE:")
    
    conceptos = {
        'Features (Características)': 'Variables de entrada (X) que usamos para hacer predicciones',
        'Target (Objetivo)': 'Variable que queremos predecir (y)',
        'Overfitting (Sobreajuste)': 'Modelo que se ajusta demasiado a los datos de entrenamiento',
        'Underfitting (Subajuste)': 'Modelo demasiado simple que no captura patrones',
        'Bias (Sesgo)': 'Error debido a suposiciones simplificadoras del modelo',
        'Variance (Varianza)': 'Error debido a sensibilidad a fluctuaciones en datos de entrenamiento',
        'Regularización': 'Técnica para prevenir overfitting penalizando parámetros complejos'
    }
    
    for concepto, definicion in conceptos.items():
        print(f"  {concepto:<30} {definicion}")
    
    return tipos_aprendizaje, pasos_ml

# Ejecutar introducción
tipos_aprendizaje, pasos_ml = introduccion_ml_cientifico()
```

### Train-Test Split

```python
def demostracion_train_test_split():
    """
    Demuestra la importancia de dividir datos en entrenamiento y prueba.
    """
    
    print("DIVISIÓN DE DATOS: TRAIN-TEST SPLIT")
    print("=" * 70)
    
    # Generar datos científicos simulados
    np.random.seed(42)
    
    # Ejemplo: Relación entre concentración y absorbancia
    n_muestras = 100
    concentraciones = np.random.uniform(0, 1, n_muestras)  # Concentración en M
    
    # Ley de Beer-Lambert: A = ε * l * C + ruido
    epsilon = 1500  # Coeficiente de extinción (M⁻¹ cm⁻¹)
    longitud = 1.0  # Longitud de celda (cm)
    ruido = np.random.normal(0, 0.05, n_muestras)  # Ruido experimental
    
    absorbancia = epsilon * longitud * concentraciones + ruido
    
    # Crear DataFrame
    datos = pd.DataFrame({
        'Concentracion': concentraciones,
        'Absorbancia': absorbancia
    })
    
    print("DATOS SIMULADOS:")
    print(f"  Número de muestras: {n_muestras}")
    print(f"  Concentración: {concentraciones.min():.3f} - {concentraciones.max():.3f} M")
    print(f"  Absorbancia: {absorbancia.min():.3f} - {absorbancia.max():.3f}")
    print(f"  Relación teórica: A = {epsilon} * C")
    
    # 1. División básica (80% train, 20% test)
    from sklearn.model_selection import train_test_split
    
    X = datos[['Concentracion']]  # Features
    y = datos['Absorbancia']      # Target
    
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, 
        test_size=0.2,           # 20% para test
        random_state=42,         # Semilla para reproducibilidad
        shuffle=True             # Mezclar datos antes de dividir
    )
    
    print("\nDIVISIÓN TRAIN-TEST (80-20):")
    print(f"  Train set: {X_train.shape[0]} muestras ({X_train.shape[0]/n_muestras*100:.1f}%)")
    print(f"  Test set:  {X_test.shape[0]} muestras ({X_test.shape[0]/n_muestras*100:.1f}%)")
    
    # 2. Estadísticas descriptivas de cada conjunto
    print("\nESTADÍSTICAS DESCRIPTIVAS:")
    
    stats_train = {
        'Concentración': {
            'Media': X_train['Concentracion'].mean(),
            'Std': X_train['Concentracion'].std(),
            'Min': X_train['Concentracion'].min(),
            'Max': X_train['Concentracion'].max()
        },
        'Absorbancia': {
            'Media': y_train.mean(),
            'Std': y_train.std(),
            'Min': y_train.min(),
            'Max': y_train.max()
        }
    }
    
    stats_test = {
        'Concentración': {
            'Media': X_test['Concentracion'].mean(),
            'Std': X_test['Concentracion'].std(),
            'Min': X_test['Concentracion'].min(),
            'Max': X_test['Concentracion'].max()
        },
        'Absorbancia': {
            'Media': y_test.mean(),
            'Std': y_test.std(),
            'Min': y_test.min(),
            'Max': y_test.max()
        }
    }
    
    print(f"\n  TRAIN SET:")
    print(f"    Concentración: μ={stats_train['Concentración']['Media']:.3f}, "
          f"σ={stats_train['Concentración']['Std']:.3f}, "
          f"range=[{stats_train['Concentración']['Min']:.3f}, {stats_train['Concentración']['Max']:.3f}]")
    print(f"    Absorbancia:   μ={stats_train['Absorbancia']['Media']:.3f}, "
          f"σ={stats_train['Absorbancia']['Std']:.3f}, "
          f"range=[{stats_train['Absorbancia']['Min']:.3f}, {stats_train['Absorbancia']['Max']:.3f}]")
    
    print(f"\n  TEST SET:")
    print(f"    Concentración: μ={stats_test['Concentración']['Media']:.3f}, "
          f"σ={stats_test['Concentración']['Std']:.3f}, "
          f"range=[{stats_test['Concentración']['Min']:.3f}, {stats_test['Concentración']['Max']:.3f}]")
    print(f"    Absorbancia:   μ={stats_test['Absorbancia']['Media']:.3f}, "
          f"σ={stats_test['Absorbancia']['Std']:.3f}, "
          f"range=[{stats_test['Absorbancia']['Min']:.3f}, {stats_test['Absorbancia']['Max']:.3f}]")
    
    # 3. Visualización de la división
    fig, axes = plt.subplots(1, 3, figsize=(15, 5))
    
    # Gráfico 1: Todos los datos
    axes[0].scatter(datos['Concentracion'], datos['Absorbancia'], 
                   alpha=0.6, color='blue', label='Todos los datos')
    axes[0].set_xlabel('Concentración (M)')
    axes[0].set_ylabel('Absorbancia')
    axes[0].set_title('Todos los datos (n=100)')
    axes[0].grid(True, alpha=0.3)
    axes[0].legend()
    
    # Gráfico 2: Train set
    axes[1].scatter(X_train['Concentracion'], y_train, 
                   alpha=0.6, color='green', label='Train set')
    axes[1].set_xlabel('Concentración (M)')
    axes[1].set_ylabel('Absorbancia')
    axes[1].set_title(f'Train set (n={X_train.shape[0]})')
    axes[1].grid(True, alpha=0.3)
    axes[1].legend()
    
    # Gráfico 3: Test set
    axes[2].scatter(X_test['Concentracion'], y_test, 
                   alpha=0.6, color='red', label='Test set')
    axes[2].set_xlabel('Concentración (M)')
    axes[2].set_ylabel('Absorbancia')
    axes[2].set_title(f'Test set (n={X_test.shape[0]})')
    axes[2].grid(True, alpha=0.3)
    axes[2].legend()
    
    plt.suptitle('DIVISIÓN TRAIN-TEST SPLIT', fontsize=14, fontweight='bold')
    plt.tight_layout()
    plt.show()
    
    # 4. Importancia de la división aleatoria
    print("\n4. IMPORTANCIA DE LA DIVISIÓN ALEATORIA:")
    
    # Diferentes semillas aleatorias
    semillas = [42, 123, 777, 999]
    
    resultados = []
    for semilla in semillas:
        X_train_temp, X_test_temp, y_train_temp, y_test_temp = train_test_split(
            X, y, test_size=0.2, random_state=semilla, shuffle=True
        )
        
        resultados.append({
            'Semilla': semilla,
            'Train_mean_X': X_train_temp['Concentracion'].mean(),
            'Test_mean_X': X_test_temp['Concentracion'].mean(),
            'Train_mean_y': y_train_temp.mean(),
            'Test_mean_y': y_test_temp.mean(),
            'Diferencia_X': abs(X_train_temp['Concentracion'].mean() - X_test_temp['Concentracion'].mean()),
            'Diferencia_y': abs(y_train_temp.mean() - y_test_temp.mean())
        })
    
    resultados_df = pd.DataFrame(resultados)
    
    print(f"\n  Comparación con diferentes semillas:")
    print(resultados_df.to_string(index=False))
    
    # 5. Estrategias de división avanzadas
    print("\n5. ESTRATEGIAS DE DIVISIÓN AVANZADAS:")
    
    estrategias = [
        ("Hold-out simple", "80-20 split básico", "train_test_split(test_size=0.2)"),
        ("Hold-out estratificado", "Mantiene proporción de clases", "train_test_split(stratify=y)"),
        ("K-Fold Cross Validation", "K divisiones, cada una como test una vez", "KFold(n_splits=5)"),
        ("Stratified K-Fold", "K-Fold manteniendo proporción de clases", "StratifiedKFold(n_splits=5)"),
        ("Leave-One-Out", "Cada muestra como test una vez", "LeaveOneOut()"),
        ("Time Series Split", "Para datos temporales (no mezclar tiempo)", "TimeSeriesSplit(n_splits=5)")
    ]
    
    print(f"\n  {'Estrategia':<30} {'Descripción':<40} {'Implementación'}")
    print(f"  {'-'*30} {'-'*40} {'-'*30}")
    
    for estrategia, descripcion, implementacion in estrategias:
        print(f"  {estrategia:<30} {descripcion:<40} {implementacion}")
    
    return X_train, X_test, y_train, y_test, datos

# Ejecutar demostración
X_train, X_test, y_train, y_test, datos = demostracion_train_test_split()
```

### Validación Cruzada

```python
def demostracion_validacion_cruzada():
    """
    Demuestra diferentes técnicas de validación cruzada.
    """
    
    print("VALIDACIÓN CRUZADA PARA EVALUACIÓN ROBUSTA")
    print("=" * 70)
    
    from sklearn.model_selection import (
        KFold, StratifiedKFold, LeaveOneOut, 
        cross_val_score, cross_validate
    )
    from sklearn.linear_model import LinearRegression
    from sklearn.metrics import mean_squared_error, r2_score
    
    # Generar datos más complejos para demostración
    np.random.seed(42)
    n_samples = 50
    
    # Características múltiples
    X = np.random.randn(n_samples, 3)  # 3 características
    # Relación no lineal con ruido
    y = 2 * X[:, 0] + 0.5 * X[:, 1]**2 - 1.5 * X[:, 2] + np.random.randn(n_samples) * 0.5
    
    # Crear modelo
    model = LinearRegression()
    
    # 1. K-Fold Cross Validation
    print("1. K-FOLD CROSS VALIDATION:")
    
    kfold = KFold(n_splits=5, shuffle=True, random_state=42)
    
    # Calcular scores para cada fold
    mse_scores = cross_val_score(model, X, y, cv=kfold, scoring='neg_mean_squared_error')
    r2_scores = cross_val_score(model, X, y, cv=kfold, scoring='r2')
    
    # Convertir MSE negativo a positivo
    mse_scores = -mse_scores
    
    print(f"  K-Fold (k=5) resultados:")
    print(f"  Fold | {'MSE':>10} | {'R²':>10}")
    print(f"  {'-'*4} | {'-'*10} | {'-'*10}")
    
    for i, (mse, r2) in enumerate(zip(mse_scores, r2_scores), 1):
        print(f"  {i:4d} | {mse:10.4f} | {r2