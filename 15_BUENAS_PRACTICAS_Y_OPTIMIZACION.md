# MÓDULO 15: BUENAS PRÁCTICAS
## Desarrollo de Código Científico Profesional y Reproducible

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Escribir código Python siguiendo el estándar PEP 8
2. Documentar funciones y módulos efectivamente
3. Implementar pruebas unitarias para validar código científico
4. Utilizar técnicas de debugging para resolver errores
5. Optimizar el rendimiento del código científico
6. Gestionar la memoria eficientemente en análisis de datos

---

## 15.1 Estilo de Código

### Concepto: ¿Por qué el Estilo de Código es Importante en Ciencia?

Un código bien escrito y estilizado es **esencial para la investigación reproducible**. Permite:
- **Colaboración efectiva** entre investigadores
- **Mantenimiento** a largo plazo del código
- **Reproducibilidad** de resultados
- **Detección temprana** de errores
- **Legibilidad** para revisores y colegas

### PEP 8 - Guía de Estilo Oficial de Python

```python
"""
Ejemplo de código científico siguiendo PEP 8.

Este módulo demuestra buenas prácticas de estilo de código
para análisis de datos científicos.
"""

import numpy as np
import pandas as pd
from typing import Tuple, List, Optional, Union
from dataclasses import dataclass
import matplotlib.pyplot as plt


@dataclass
class ExperimentalConditions:
    """Almacena condiciones experimentales de forma estructurada."""
    
    temperature: float  # en grados Celsius
    pressure: float     # en hPa
    ph: float          # unidad adimensional
    duration: float    # en minutos
    
    def validate(self) -> bool:
        """Valida que las condiciones estén dentro de rangos razonables."""
        valid_temperature = 0 <= self.temperature <= 100
        valid_pressure = 900 <= self.pressure <= 1100
        valid_ph = 0 <= self.ph <= 14
        valid_duration = self.duration > 0
        
        return all([valid_temperature, valid_pressure, valid_ph, valid_duration])


def calculate_reaction_rate(
    concentration_reactant: np.ndarray,
    concentration_product: np.ndarray,
    time_points: np.ndarray,
    method: str = "central_difference"
) -> Tuple[np.ndarray, np.ndarray]:
    """
    Calcula la tasa de reacción a partir de datos de concentración.
    
    La tasa de reacción se calcula como la derivada numérica de la
    concentración del producto respecto al tiempo, o la derivada negativa
    de la concentración del reactante.
    
    Parámetros
    ----------
    concentration_reactant : np.ndarray
        Concentración del reactante en función del tiempo (M)
    concentration_product : np.ndarray
        Concentración del producto en función del tiempo (M)
    time_points : np.ndarray
        Puntos de tiempo correspondientes (min)
    method : str, opcional
        Método para cálculo de derivada ("forward", "backward", "central_difference")
        (default="central_difference")
    
    Retorna
    -------
    Tuple[np.ndarray, np.ndarray]
        Tupla con (tasa_reactante, tasa_producto) en M/min
    
    Raises
    ------
    ValueError
        Si los arrays de entrada no tienen la misma longitud
        Si el método de derivada no es válido
    
    Ejemplos
    --------
    >>> time = np.array([0, 1, 2, 3, 4])
    >>> conc_a = np.array([1.0, 0.8, 0.6, 0.4, 0.2])
    >>> conc_b = np.array([0.0, 0.2, 0.4, 0.6, 0.8])
    >>> rate_a, rate_b = calculate_reaction_rate(conc_a, conc_b, time)
    >>> rate_a[0]
    -0.2
    """
    # Validación de parámetros
    if not (len(concentration_reactant) == len(concentration_product) == len(time_points)):
        raise ValueError("Todos los arrays deben tener la misma longitud")
    
    if method not in ["forward", "backward", "central_difference"]:
        raise ValueError(f"Método '{method}' no válido. Use 'forward', 'backward' o 'central_difference'")
    
    # Cálculo de derivada numérica
    if method == "forward":
        delta_time = np.diff(time_points)
        rate_reactant = -np.diff(concentration_reactant) / delta_time
        rate_product = np.diff(concentration_product) / delta_time
        
        # Ajustar longitud para coincidir con tiempo
        time_points = time_points[:-1]
        
    elif method == "backward":
        delta_time = np.diff(time_points)
        rate_reactant = -np.diff(concentration_reactant) / delta_time
        rate_product = np.diff(concentration_product) / delta_time
        
        # Ajustar longitud para coincidir con tiempo
        time_points = time_points[1:]
        rate_reactant = rate_reactant[1:]
        rate_product = rate_product[1:]
        
    else:  # central_difference (default)
        rate_reactant = -np.gradient(concentration_reactant, time_points)
        rate_product = np.gradient(concentration_product, time_points)
    
    return rate_reactant, rate_product


class SpectrophotometerData:
    """
    Clase para manejar y analizar datos de espectrofotometría.
    
    Esta clase proporciona métodos para procesar, normalizar y analizar
    datos de absorbancia obtenidos de un espectrofotómetro.
    
    Atributos
    ---------
    wavelength : np.ndarray
        Longitudes de onda en nanómetros
    absorbance : np.ndarray
        Valores de absorbancia
    sample_name : str
        Nombre de la muestra
    measurement_date : str
        Fecha de medición en formato YYYY-MM-DD
    
    Métodos
    -------
    normalize_baseline()
        Normaliza los datos restando la absorbancia mínima
    find_peak_wavelength()
        Encuentra la longitud de onda de máxima absorbancia
    calculate_area_under_curve()
        Calcula el área bajo la curva del espectro
    """
    
    def __init__(
        self,
        wavelength: np.ndarray,
        absorbance: np.ndarray,
        sample_name: str = "Unknown",
        measurement_date: Optional[str] = None
    ):
        """
        Inicializa un objeto SpectrophotometerData.
        
        Parámetros
        ----------
        wavelength : np.ndarray
            Array de longitudes de onda en nm
        absorbance : np.ndarray
            Array de valores de absorbancia
        sample_name : str, opcional
            Nombre de la muestra (default="Unknown")
        measurement_date : str, opcional
            Fecha de medición en formato YYYY-MM-DD (default=None)
        
        Raises
        ------
        ValueError
            Si wavelength y absorbance no tienen la misma longitud
            Si hay valores NaN en los datos
        """
        # Validación de datos
        if len(wavelength) != len(absorbance):
            raise ValueError("wavelength y absorbance deben tener la misma longitud")
        
        if np.any(np.isnan(wavelength)) or np.any(np.isnan(absorbance)):
            raise ValueError("Los datos no pueden contener valores NaN")
        
        # Asignación de atributos
        self.wavelength = wavelength
        self.absorbance = absorbance
        self.sample_name = sample_name
        self.measurement_date = measurement_date
        
        # Atributos calculados
        self._normalized = False
        self._peak_wavelength = None
        self._area_under_curve = None
    
    def normalize_baseline(self) -> np.ndarray:
        """
        Normaliza los datos restando la absorbancia mínima.
        
        Retorna
        -------
        np.ndarray
            Datos de absorbancia normalizados
        
        Notas
        -----
        Este método modifica el atributo `absorbance` in-place
        y marca la muestra como normalizada.
        """
        min_absorbance = np.min(self.absorbance)
        self.absorbance = self.absorbance - min_absorbance
        self._normalized = True
        
        return self.absorbance
    
    def find_peak_wavelength(self) -> Tuple[float, float]:
        """
        Encuentra la longitud de onda de máxima absorbancia.
        
        Retorna
        -------
        Tuple[float, float]
            Tupla con (longitud_onda_pico, absorbancia_pico)
        
        Ejemplos
        --------
        >>> data = SpectrophotometerData(np.array([400, 500]), np.array([0.1, 0.5]))
        >>> wavelength_peak, absorbance_peak = data.find_peak_wavelength()
        >>> wavelength_peak
        500.0
        """
        if self._peak_wavelength is None:
            max_index = np.argmax(self.absorbance)
            self._peak_wavelength = (self.wavelength[max_index], self.absorbance[max_index])
        
        return self._peak_wavelength
    
    def calculate_area_under_curve(self, method: str = "trapezoidal") -> float:
        """
        Calcula el área bajo la curva del espectro.
        
        Parámetros
        ----------
        method : str, opcional
            Método de integración ("trapezoidal" o "simpson")
            (default="trapezoidal")
        
        Retorna
        -------
        float
            Área bajo la curva
        
        Raises
        ------
        ValueError
            Si el método de integración no es válido
        """
        if method == "trapezoidal":
            area = np.trapz(self.absorbance, self.wavelength)
        elif method == "simpson":
            from scipy.integrate import simpson
            area = simpson(self.absorbance, self.wavelength)
        else:
            raise ValueError(f"Método '{method}' no válido. Use 'trapezoidal' o 'simpson'")
        
        self._area_under_curve = area
        return area
    
    def plot_spectrum(
        self,
        ax: Optional[plt.Axes] = None,
        show_peak: bool = True,
        **plot_kwargs
    ) -> plt.Axes:
        """
        Genera un gráfico del espectro de absorbancia.
        
        Parámetros
        ----------
        ax : plt.Axes, opcional
            Ejes de matplotlib para graficar (default=None, crea nuevos ejes)
        show_peak : bool, opcional
            Si True, marca el pico de absorbancia (default=True)
        **plot_kwargs
            Argumentos adicionales para plt.plot()
        
        Retorna
        -------
        plt.Axes
            Ejes con el gráfico generado
        """
        if ax is None:
            fig, ax = plt.subplots(figsize=(10, 6))
        
        # Graficar espectro
        ax.plot(
            self.wavelength,
            self.absorbance,
            label=self.sample_name,
            **plot_kwargs
        )
        
        # Marcar pico si se solicita
        if show_peak:
            peak_wavelength, peak_absorbance = self.find_peak_wavelength()
            ax.scatter(
                peak_wavelength,
                peak_absorbance,
                color='red',
                s=100,
                zorder=5,
                label=f'Pico: {peak_wavelength:.1f} nm'
            )
        
        # Configurar gráfico
        ax.set_xlabel('Longitud de onda (nm)', fontsize=12)
        ax.set_ylabel('Absorbancia', fontsize=12)
        ax.set_title(f'Espectro de absorbancia - {self.sample_name}', fontsize=14)
        ax.grid(True, alpha=0.3)
        ax.legend()
        
        return ax
    
    def __str__(self) -> str:
        """Representación en string de los datos."""
        peak_info = self.find_peak_wavelength()
        return (
            f"SpectrophotometerData: {self.sample_name}\n"
            f"  Longitudes de onda: {len(self.wavelength)} puntos\n"
            f"  Rango: {self.wavelength.min():.1f} - {self.wavelength.max():.1f} nm\n"
            f"  Pico: {peak_info[0]:.1f} nm (A={peak_info[1]:.3f})\n"
            f"  Normalizado: {self._normalized}"
        )


# Ejemplo de uso siguiendo PEP 8
def ejemplo_uso_pep8():
    """
    Ejemplo de uso de las clases y funciones definidas anteriormente.
    
    Este ejemplo demuestra cómo usar el código de manera clara y legible.
    """
    print("EJEMPLO DE USO - SIGUIENDO PEP 8")
    print("=" * 70)
    
    # 1. Crear condiciones experimentales
    conditions = ExperimentalConditions(
        temperature=25.0,
        pressure=1013.25,
        ph=7.0,
        duration=60.0
    )
    
    print("1. Condiciones experimentales:")
    print(f"   Temperatura: {conditions.temperature}°C")
    print(f"   Presión: {conditions.pressure} hPa")
    print(f"   pH: {conditions.ph}")
    print(f"   Duración: {conditions.duration} min")
    print(f"   Válidas: {conditions.validate()}")
    
    # 2. Calcular tasa de reacción
    print("\n2. Cálculo de tasa de reacción:")
    
    # Datos simulados
    time = np.linspace(0, 10, 100)
    conc_a = np.exp(-0.5 * time)  # Decaimiento exponencial
    conc_b = 1 - conc_a           # Producto formado
    
    try:
        rate_a, rate_b = calculate_reaction_rate(
            concentration_reactant=conc_a,
            concentration_product=conc_b,
            time_points=time,
            method="central_difference"
        )
        
        print(f"   Tasa inicial de A: {rate_a[0]:.4f} M/min")
        print(f"   Tasa inicial de B: {rate_b[0]:.4f} M/min")
        print(f"   Tasa final de A: {rate_a[-1]:.4f} M/min")
        
    except ValueError as e:
        print(f"   Error: {e}")
    
    # 3. Analizar datos de espectrofotometría
    print("\n3. Análisis de datos espectrofotométricos:")
    
    # Datos simulados de espectro
    wavelength = np.linspace(400, 700, 301)
    absorbance = np.exp(-(wavelength - 550)**2 / (2 * 30**2)) + 0.1 * np.random.randn(301)
    
    # Crear objeto de datos
    spectrum_data = SpectrophotometerData(
        wavelength=wavelength,
        absorbance=absorbance,
        sample_name="Muestra de prueba",
        measurement_date="2024-03-26"
    )
    
    # Normalizar
    spectrum_data.normalize_baseline()
    
    # Encontrar pico
    peak_wavelength, peak_absorbance = spectrum_data.find_peak_wavelength()
    
    # Calcular área bajo la curva
    area = spectrum_data.calculate_area_under_curve(method="trapezoidal")
    
    print(f"   Muestra: {spectrum_data.sample_name}")
    print(f"   Pico: {peak_wavelength:.1f} nm (A={peak_absorbance:.3f})")
    print(f"   Área bajo la curva: {area:.3f}")
    
    # Graficar
    fig, ax = plt.subplots(figsize=(10, 6))
    spectrum_data.plot_spectrum(ax=ax, color='blue', linewidth=2)
    plt.tight_layout()
    plt.show()
    
    # 4. Mostrar representación en string
    print("\n4. Representación completa:")
    print(spectrum_data)


# Ejecutar ejemplo
if __name__ == "__main__":
    ejemplo_uso_pep8()
```

### Nomenclatura de Variables

```python
def demostracion_nomenclatura_variables():
    """
    Demuestra buenas prácticas de nomenclatura de variables en ciencia.
    """
    
    print("NOMENCLATURA DE VARIABLES - BUENAS PRÁCTICAS")
    print("=" * 70)
    
    # 1. Variables para datos científicos
    print("1. VARIABLES PARA DATOS CIENTÍFICOS:")
    
    # ✅ CORRECTO - Descriptivo y claro
    temperature_celsius = 25.5
    pressure_hpa = 1013.25
    concentration_glucose_mM = 5.0
    absorbance_450nm = 0.423
    sample_id = "BIO-2024-001"
    experiment_date = "2024-03-26"
    
    # ❌ INCORRECTO - Poco descriptivo
    # temp = 25.5
    # p = 1013.25
    # c = 5.0
    # a = 0.423
    # id = "BIO-2024-001"
    # d = "2024-03-26"
    
    print(f"  ✅ temperature_celsius = {temperature_celsius}")
    print(f"  ✅ pressure_hpa = {pressure_hpa}")
    print(f"  ✅ concentration_glucose_mM = {concentration_glucose_mM}")
    print(f"