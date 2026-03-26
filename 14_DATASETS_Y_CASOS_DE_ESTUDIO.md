# MÓDULO 14: DATASETS Y CASOS DE ESTUDIO
## Aplicaciones Prácticas de Machine Learning en Ciencia

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Trabajar con el dataset Iris para clasificación de especies
2. Crear y analizar datasets personalizados para problemas específicos
3. Realizar análisis exploratorio de datos (EDA) completo
4. Implementar pipelines de ML para problemas científicos reales
5. Evaluar y comparar diferentes modelos de ML
6. Interpretar resultados y comunicar hallazgos científicos

---

## 14.1 Dataset Iris

### Concepto: El Dataset Clásico para Clasificación

El dataset Iris es un **conjunto de datos clásico** en machine learning y estadística. Contiene medidas de **150 flores de iris** de tres especies diferentes. Es ideal para:
- **Aprendizaje de clasificación** multiclase
- **Visualización de datos** multivariados
- **Prueba de algoritmos** de ML
- **Enseñanza de conceptos** fundamentales

### Características del Dataset

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import load_iris

def analisis_dataset_iris():
    """
    Análisis completo del dataset Iris.
    """
    
    print("DATASET IRIS - ANÁLISIS COMPLETO")
    print("=" * 70)
    
    # 1. Cargar el dataset
    iris = load_iris()
    
    print("1. INFORMACIÓN BÁSICA:")
    print(f"  Número de muestras: {iris.data.shape[0]}")
    print(f"  Número de características: {iris.data.shape[1]}")
    print(f"  Número de clases: {len(np.unique(iris.target))}")
    print(f"  Nombres de clases: {iris.target_names}")
    print(f"  Nombres de características: {iris.feature_names}")
    
    # 2. Crear DataFrame para análisis
    df_iris = pd.DataFrame(
        data=iris.data,
        columns=iris.feature_names
    )
    df_iris['species'] = iris.target
    df_iris['species_name'] = df_iris['species'].map(
        {0: 'setosa', 1: 'versicolor', 2: 'virginica'}
    )
    
    print("\n2. ESTADÍSTICAS DESCRIPTIVAS:")
    print(df_iris.describe())
    
    # 3. Distribución por clase
    print("\n3. DISTRIBUCIÓN POR CLASE:")
    distribucion = df_iris['species_name'].value_counts()
    print(distribucion.to_string())
    
    # 4. Visualización completa
    print("\n4. VISUALIZACIÓN COMPLETA:")
    
    # Configurar estilo
    plt.style.use('seaborn-v0_8-whitegrid')
    sns.set_palette("husl")
    
    # Crear figura con múltiples subplots
    fig = plt.figure(figsize=(15, 12))
    
    # 4.1. Pairplot (scatter matrix)
    print("  Generando Pairplot...")
    g = sns.pairplot(df_iris, hue='species_name', height=2.5)
    g.fig.suptitle('Pairplot - Dataset Iris', y=1.02, fontsize=16, fontweight='bold')
    
    plt.show()
    
    # 4.2. Boxplots por característica
    fig, axes = plt.subplots(2, 2, figsize=(12, 10))
    axes = axes.flatten()
    
    for idx, feature in enumerate(iris.feature_names):
        sns.boxplot(data=df_iris, x='species_name', y=feature, ax=axes[idx])
        axes[idx].set_title(f'Distribución de {feature}')
        axes[idx].set_xlabel('Especie')
        axes[idx].set_ylabel(feature)
        axes[idx].tick_params(axis='x', rotation=45)
    
    plt.suptitle('Boxplots por Característica y Especie', fontsize=16, fontweight='bold')
    plt.tight_layout()
    plt.show()
    
    # 4.3. Matriz de correlación
    fig, ax = plt.subplots(figsize=(10, 8))
    
    # Calcular matriz de correlación
    corr_matrix = df_iris[iris.feature_names].corr()
    
    # Heatmap
    sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', center=0,
                square=True, linewidths=1, cbar_kws={"shrink": 0.8}, ax=ax)
    
    ax.set_title('Matriz de Correlación - Características del Iris', fontsize=14, fontweight='bold')
    plt.tight_layout()
    plt.show()
    
    # 5. Análisis por especie
    print("\n5. ANÁLISIS POR ESPECIE:")
    
    especies = ['setosa', 'versicolor', 'virginica']
    
    for especie in especies:
        df_especie = df_iris[df_iris['species_name'] == especie]
        
        print(f"\n  {especie.upper()}:")
        print(f"    Número de muestras: {len(df_especie)}")
        print(f"    Estadísticas:")
        
        stats = df_especie[iris.feature_names].describe().loc[['mean', 'std', 'min', 'max']]
        for feature in iris.feature_names:
            mean_val = stats.loc['mean', feature]
            std_val = stats.loc['std', feature]
            print(f"      {feature}: {mean_val:.2f} ± {std_val:.2f}")
    
    # 6. Identificación de características discriminantes
    print("\n6. CARACTERÍSTICAS DISCRIMINANTES:")
    
    # Calcular separabilidad entre clases
    from scipy.spatial.distance import euclidean
    
    # Medias por clase
    medias = df_iris.groupby('species_name')[iris.feature_names].mean()
    
    print(f"\n  Medias por clase:")
    print(medias.to_string())
    
    # Distancias entre medias
    print(f"\n  Distancias euclidianas entre medias de clases:")
    for i in range(len(especies)):
        for j in range(i+1, len(especies)):
            dist = euclidean(medias.iloc[i], medias.iloc[j])
            print(f"    {especies[i]} - {especies[j]}: {dist:.3f}")
    
    return df_iris, iris

# Ejecutar análisis
df_iris, iris_obj = analisis_dataset_iris()
```

### Exploración del Dataset

```python
def exploracion_avanzada_iris():
    """
    Exploración avanzada del dataset Iris.
    """
    
    print("EXPLORACIÓN AVANZADA - DATASET IRIS")
    print("=" * 70)
    
    # Cargar datos si no están disponibles
    if 'df_iris' not in globals():
        from sklearn.datasets import load_iris
        iris = load_iris()
        df_iris = pd.DataFrame(
            data=iris.data,
            columns=iris.feature_names
        )
        df_iris['species'] = iris.target
        df_iris['species_name'] = df_iris['species'].map(
            {0: 'setosa', 1: 'versicolor', 2: 'virginica'}
        )
    
    # 1. Análisis de outliers
    print("1. ANÁLISIS DE OUTLIERS:")
    
    from scipy import stats
    
    # Calcular z-scores para cada característica
    features = iris_obj.feature_names
    
    outliers_info = {}
    for feature in features:
        z_scores = np.abs(stats.zscore(df_iris[feature]))
        outliers = df_iris[z_scores > 3]
        
        outliers_info[feature] = {
            'n_outliers': len(outliers),
            'indices': outliers.index.tolist() if len(outliers) > 0 else [],
            'values': outliers[feature].tolist() if len(outliers) > 0 else []
        }
    
    print(f"\n  Outliers (|z-score| > 3):")
    for feature, info in outliers_info.items():
        print(f"    {feature}: {info['n_outliers']} outliers")
        if info['n_outliers'] > 0:
            print(f"      Valores: {info['values']}")
    
    # 2. Análisis de distribución
    print("\n2. ANÁLISIS DE DISTRIBUCIÓN:")
    
    # Test de normalidad (Shapiro-Wilk)
    from scipy.stats import shapiro
    
    print(f"\n  Test de normalidad (Shapiro-Wilk):")
    print(f"    {'Característica':<25} {'W-statistic':<12} {'p-value':<12} {'Normal?'}")
    print(f"    {'-'*25} {'-'*12} {'-'*12} {'-'*10}")
    
    for feature in features:
        stat, p = shapiro(df_iris[feature])
        es_normal = p > 0.05
        print(f"    {feature:<25} {stat:12.4f} {p:12.4f} {'Sí' if es_normal else 'No'}")
    
    # 3. Análisis de varianza (ANOVA)
    print("\n3. ANÁLISIS DE VARIANZA (ANOVA):")
    
    from scipy.stats import f_oneway
    
    # Separar datos por especie
    setosa = df_iris[df_iris['species_name'] == 'setosa'][features]
    versicolor = df_iris[df_iris['species_name'] == 'versicolor'][features]
    virginica = df_iris[df_iris['species_name'] == 'virginica'][features]
    
    print(f"\n  ANOVA por característica:")
    print(f"    {'Característica':<25} {'F-statistic':<12} {'p-value':<12} {'Significativa?'}")
    print(f"    {'-'*25} {'-'*12} {'-'*12} {'-'*15}")
    
    for feature in features:
        f_stat, p_val = f_oneway(
            setosa[feature],
            versicolor[feature],
            virginica[feature]
        )
        significativa = p_val < 0.05
        print(f"    {feature:<25} {f_stat:12.4f} {p_val:12.4f} {'Sí' if significativa else 'No'}")
    
    # 4. Visualización 3D
    print("\n4. VISUALIZACIÓN 3D:")
    
    from mpl_toolkits.mplot3d import Axes3D
    
    fig = plt.figure(figsize=(12, 10))
    ax = fig.add_subplot(111, projection='3d')
    
    # Colores por especie
    colors = {'setosa': 'red', 'versicolor': 'green', 'virginica': 'blue'}
    
    for especie, color in colors.items():
        df_especie = df_iris[df_iris['species_name'] == especie]
        ax.scatter(
            df_especie['sepal length (cm)'],
            df_especie['sepal width (cm)'],
            df_especie['petal length (cm)'],
            c=color,
            s=50,
            label=especie,
            alpha=0.7,
            edgecolors='w',
            linewidth=0.5
        )
    
    ax.set_xlabel('Sepal Length (cm)')
    ax.set_ylabel('Sepal Width (cm)')
    ax.set_zlabel('Petal Length (cm)')
    ax.set_title('Visualización 3D - Dataset Iris', fontsize=14, fontweight='bold')
    ax.legend()
    
    # Añadir ángulo de vista
    ax.view_init(elev=20, azim=45)
    
    plt.tight_layout()
    plt.show()
    
    # 5. Análisis de componentes principales (PCA)
    print("\n5. ANÁLISIS DE COMPONENTES PRINCIPALES (PCA):")
    
    from sklearn.decomposition import PCA
    from sklearn.preprocessing import StandardScaler
    
    # Preparar datos
    X = df_iris[features].values
    y = df_iris['species'].values
    
    # Estandarizar
    scaler = StandardScaler()
    X_scaled = scaler.fit_transform(X)
    
    # Aplicar PCA
    pca = PCA(n_components=2)
    X_pca = pca.fit_transform(X_scaled)
    
    print(f"\n  Varianza explicada:")
    print(f"    PC1: {pca.explained_variance_ratio_[0]*100:.2f}%")
    print(f"    PC2: {pca.explained_variance_ratio_[1]*100:.2f}%")
    print(f"    Total: {sum(pca.explained_variance_ratio_)*100:.2f}%")
    
    print(f"\n  Componentes principales:")
    for i, component in enumerate(pca.components_, 1):
        print(f"    PC{i}: {component}")
    
    # Visualizar PCA
    fig, axes = plt.subplots(1, 2, figsize=(15, 6))
    
    # Gráfico 1: PCA scatter
    scatter = axes[0].scatter(
        X_pca[:, 0], X_pca[:, 1],
        c=y, cmap='viridis', s=50, alpha=0.7, edgecolors='w', linewidth=0.5
    )
    axes[0].set_xlabel(f'PC1 ({pca.explained_variance_ratio_[0]*100:.1f}% varianza)')
    axes[0].set_ylabel(f'PC2 ({pca.explained_variance_ratio_[1]*100:.1f}% varianza)')
    axes[0].set_title('PCA - Proyección 2D', fontsize=12, fontweight='bold')
    axes[0].grid(True, alpha=0.3)
    
    # Añadir leyenda
    legend_elements = [
        plt.Line2D([0], [0], marker='o', color='w', label='Setosa',
                  markerfacecolor='yellow', markersize=10),
        plt.Line2D([0], [0], marker='o', color='w', label='Versicolor',
                  markerfacecolor='green', markersize=10),
        plt.Line2D([0], [0], marker='o', color='w', label='Virginica',
                  markerfacecolor='blue', markersize=10)
    ]
    axes[0].legend(handles=legend_elements)
    
    # Gráfico 2: Varianza explicada acumulada
    pca_full = PCA().fit(X_scaled)
    explained_variance_ratio = pca_full.explained_variance_ratio_
    cumulative_variance = np.cumsum(explained_variance_ratio)
    
    axes[1].plot(range(1, len(cumulative_variance) + 1), cumulative_variance, 
                'bo-', linewidth=2, markersize=8)
    axes[1].axhline(y=0.95, color='r', linestyle='--', alpha=0.7, label='95% varianza')
    axes[1].set_xlabel('Número de Componentes')
    axes[1].set_ylabel('Varianza Explicada Acumulada')
    axes[1].set_title('Varianza Explicada por Componentes', fontsize=12, fontweight='bold')
    axes[1].grid(True, alpha=0.3)
    axes[1].legend()
    
    # Encontrar número de componentes para 95% varianza
    n_components_95 = np.argmax(cumulative_variance >= 0.95) + 1
    axes[1].axvline(x=n_components_95, color='g', linestyle='--', alpha=0.7,
                   label=f'{n_components_95} componentes para 95%')
    
    plt.suptitle('ANÁLISIS DE COMPONENTES PRINCIPALES (PCA)', fontsize=14, fontweight='bold')
    plt.tight_layout()
    plt.show()
    
    print(f"\n  Número de componentes para 95% de varianza: {n_components_95}")
    
    return df_iris, pca, X_pca

# Ejecutar exploración avanzada
df_iris, pca_result, X_pca = exploracion_avanzada_iris()
```

### Clasificación con Logistic Regression

```python
def clasificacion_iris_logistic_regression():
    """
    Clasificación del dataset Iris usando Regresión Logística.
    """
    
    print("CLASIFICACIÓN CON REGRESIÓN LOGÍSTICA - DATASET IRIS")
    print("=" * 70)
    
    from sklearn.linear_model import LogisticRegression
    from sklearn.model_selection import train_test_split, cross_val_score
    from sklearn.preprocessing import StandardScaler
    from sklearn.metrics import (
        classification_report, confusion_matrix, 
        accuracy_score, precision_score, recall_score, f1_score,
        roc_curve, auc
    )
    
    # 1. Preparación de datos
    print("1. PREPARACIÓN DE DATOS:")
    
    # Usar todas las características
    X = df_iris[iris_obj.feature_names].values
