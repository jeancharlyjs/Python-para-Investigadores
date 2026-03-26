# MÓDULO 5: PROGRAMACIÓN ORIENTADA A OBJETOS (POO)
## Modelado de Entidades Científicas

## Objetivos de Aprendizaje

Al finalizar este módulo, serás capaz de:
1. Diseñar clases para representar entidades científicas
2. Implementar encapsulación para proteger datos sensibles
3. Utilizar herencia para crear jerarquías de clases científicas
4. Aplicar polimorfismo para operaciones flexibles
5. Implementar métodos especiales para comportamiento personalizado
6. Modelar sistemas científicos complejos usando POO

---

## 5.1 Conceptos Básicos

### Concepto: ¿Qué es la Programación Orientada a Objetos en Ciencia?

La POO es un paradigma de programación que organiza el código alrededor de **objetos** que representan entidades del mundo real. En ciencia, esto significa modelar **reactivos, instrumentos, experimentos y organismos** como objetos con propiedades (atributos) y comportamientos (métodos).

### Clases y Objetos: La Base de la POO

```python
class ReactivoQuimico:
    """
    Clase que representa un reactivo químico.
    
    Atributos:
    ----------
    nombre : str
        Nombre del reactivo
    formula : str
        Fórmula química
    peso_molecular : float
        Peso molecular en g/mol
    pureza : float
        Pureza como fracción (0-1)
    estado : str
        Estado físico (sólido, líquido, gas)
    """
    
    def __init__(self, nombre, formula, peso_molecular, pureza=1.0, estado="sólido"):
        """
        Constructor de la clase ReactivoQuimico.
        
        Parámetros:
        -----------
        nombre : str
            Nombre del reactivo
        formula : str
            Fórmula química
        peso_molecular : float
            Peso molecular en g/mol
        pureza : float, opcional
            Pureza como fracción (default=1.0)
        estado : str, opcional
            Estado físico (default="sólido")
        """
        # Atributos de instancia
        self.nombre = nombre
        self.formula = formula
        self.peso_molecular = peso_molecular
        self.pureza = pureza
        self.estado = estado
        self.lote = None
        self.fecha_caducidad = None
        
        # Validación de parámetros
        self._validar_parametros()
    
    def _validar_parametros(self):
        """Valida los parámetros del reactivo."""
        if self.peso_molecular <= 0:
            raise ValueError("El peso molecular debe ser positivo")
        if not 0 <= self.pureza <= 1:
            raise ValueError("La pureza debe estar entre 0 y 1")
        if self.estado not in ["sólido", "líquido", "gas"]:
            raise ValueError("Estado debe ser 'sólido', 'líquido' o 'gas'")
    
    def calcular_masa_molar(self, moles):
        """
        Calcula la masa necesaria para una cantidad dada de moles.
        
        Parámetros:
        -----------
        moles : float
            Cantidad de moles deseada
        
        Retorna:
        --------
        float
            Masa en gramos
        """
        masa_pura = moles * self.peso_molecular
        masa_real = masa_pura / self.pureza
        return masa_real
    
    def preparar_solucion(self, concentracion, volumen):
        """
        Genera instrucciones para preparar una solución.
        
        Parámetros:
        -----------
        concentracion : float
            Concentración deseada en M (mol/L)
        volumen : float
            Volumen deseado en mL
        
        Retorna:
        --------
        str
            Instrucciones detalladas
        """
        # Convertir volumen a litros
        volumen_l = volumen / 1000
        
        # Calcular moles necesarios
        moles = concentracion * volumen_l
        
        # Calcular masa necesaria
        masa = self.calcular_masa_molar(moles)
        
        instrucciones = f"""
        PREPARACIÓN DE SOLUCIÓN DE {self.nombre}
        =======================================
        Fórmula: {self.formula}
        Peso molecular: {self.peso_molecular} g/mol
        Pureza: {self.pureza*100:.1f}%
        
        PARA PREPARAR {volumen} mL DE {concentracion} M:
        1. Pesar {masa:.4f} g de {self.nombre}
        2. Disolver en aproximadamente {volumen*0.8:.1f} mL de solvente
        3. Ajustar a volumen final de {volumen} mL
        4. Homogeneizar completamente
        
        MASA MOLAR CALCULADA:
        - Moles necesarios: {moles:.6f} mol
        - Masa pura: {moles * self.peso_molecular:.4f} g
        - Masa real (considerando pureza): {masa:.4f} g
        """
        
        return instrucciones
    
    def __str__(self):
        """Representación en string del reactivo."""
        return f"{self.nombre} ({self.formula}) - {self.peso_molecular} g/mol"

# Creación de objetos (instancias)
print("CREACIÓN DE REACTIVOS QUÍMICOS")
print("=" * 60)

# Reactivo 1: Cloruro de sodio
nacl = ReactivoQuimico(
    nombre="Cloruro de sodio",
    formula="NaCl",
    peso_molecular=58.44,
    pureza=0.995,
    estado="sólido"
)

# Reactivo 2: Ácido clorhídrico
hcl = ReactivoQuimico(
    nombre="Ácido clorhídrico",
    formula="HCl",
    peso_molecular=36.46,
    pureza=0.37,  # 37% en solución
    estado="líquido"
)

# Reactivo 3: Hidróxido de sodio
naoh = ReactivoQuimico(
    nombre="Hidróxido de sodio",
    formula="NaOH",
    peso_molecular=40.00,
    pureza=0.98,
    estado="sólido"
)

# Uso de los objetos
print(f"Reactivo 1: {nacl}")
print(f"Reactivo 2: {hcl}")
print(f"Reactivo 3: {naoh}")

# Preparar soluciones
print("\nPREPARACIÓN DE SOLUCIONES")
print("=" * 60)

# Solución de NaCl 0.1M
instrucciones_nacl = nacl.preparar_solucion(concentracion=0.1, volumen=100)
print("Solución de NaCl 0.1M:")
print(instrucciones_nacl)

# Solución de HCl 1.0M
instrucciones_hcl = hcl.preparar_solucion(concentracion=1.0, volumen=50)
print("\nSolución de HCl 1.0M:")
print(instrucciones_hcl)

# Cálculos de masa
print("\nCÁLCULOS DE MASA")
print("=" * 60)
moles_nacl = 0.5
masa_nacl = nacl.calcular_masa_molar(moles_nacl)
print(f"Para {moles_nacl} moles de {nacl.nombre}:")
print(f"  Masa necesaria: {masa_nacl:.2f} g")
```

### Atributos y Métodos

```python
class InstrumentoLaboratorio:
    """
    Clase base para instrumentos de laboratorio.
    
    Atributos:
    ----------
    nombre : str
        Nombre del instrumento
    modelo : str
        Modelo específico
    fabricante : str
        Empresa fabricante
    año_fabricacion : int
        Año de fabricación
    calibrado : bool
        Estado de calibración
    ubicacion : str
        Ubicación en el laboratorio
    """
    
    # Atributo de clase (compartido por todas las instancias)
    contador_instrumentos = 0
    
    def __init__(self, nombre, modelo, fabricante, año_fabricacion, ubicacion):
        """Constructor de InstrumentoLaboratorio."""
        self.nombre = nombre
        self.modelo = modelo
        self.fabricante = fabricante
        self.año_fabricacion = año_fabricacion
        self.ubicacion = ubicacion
        self.calibrado = False
        self.fecha_ultima_calibracion = None
        self.horas_uso = 0
        
        # Incrementar contador de clase
        InstrumentoLaboratorio.contador_instrumentos += 1
        self.id_instrumento = InstrumentoLaboratorio.contador_instrumentos
    
    def calibrar(self, fecha_calibracion):
        """
        Calibra el instrumento.
        
        Parámetros:
        -----------
        fecha_calibracion : str
            Fecha de calibración en formato YYYY-MM-DD
        """
        self.calibrado = True
        self.fecha_ultima_calibracion = fecha_calibracion
        print(f"{self.nombre} calibrado el {fecha_calibracion}")
    
    def usar(self, horas):
        """
        Registra uso del instrumento.
        
        Parámetros:
        -----------
        horas : float
            Horas de uso a registrar
        """
        if not self.calibrado:
            print(f"ADVERTENCIA: {self.nombre} no está calibrado")
        
        self.horas_uso += horas
        print(f"{self.nombre} usado por {horas} horas. Total: {self.horas_uso} horas")
    
    def necesita_calibracion(self, meses_validez=12):
        """
        Verifica si el instrumento necesita calibración.
        
        Parámetros:
        -----------
        meses_validez : int, opcional
            Meses de validez de la calibración (default=12)
        
        Retorna:
        --------
        bool
            True si necesita calibración, False en caso contrario
        """
        if not self.fecha_ultima_calibracion:
            return True
        
        # En una implementación real, aquí se calcularía la fecha
        # Para este ejemplo, simulamos que necesita calibración si tiene más de 100 horas de uso
        return self.horas_uso > 100
    
    def generar_reporte(self):
        """Genera un reporte del estado del instrumento."""
        reporte = f"""
        REPORTE DE INSTRUMENTO #{self.id_instrumento}
        ===========================================
        Nombre: {self.nombre}
        Modelo: {self.modelo}
        Fabricante: {self.fabricante}
        Año: {self.año_fabricacion}
        Ubicación: {self.ubicacion}
        
        ESTADO:
        - Calibrado: {'SÍ' if self.calibrado else 'NO'}
        - Última calibración: {self.fecha_ultima_calibracion or 'Nunca'}
        - Horas de uso: {self.horas_uso}
        - Necesita calibración: {'SÍ' if self.necesita_calibracion() else 'NO'}
        """
        return reporte
    
    @classmethod
    def get_total_instrumentos(cls):
        """
        Método de clase: Obtiene el total de instrumentos creados.
        
        Retorna:
        --------
        int
            Número total de instrumentos
        """
        return cls.contador_instrumentos
    
    @staticmethod
    def validar_año_fabricacion(año):
        """
        Método estático: Valida un año de fabricación.
        
        Parámetros:
        -----------
        año : int
            Año a validar
        
        Retorna:
        --------
        bool
            True si el año es válido, False en caso contrario
        """
        año_actual = 2024  # En realidad se obtendría del sistema
        return 1900 <= año <= año_actual

# Creación y uso de instrumentos
print("GESTIÓN DE INSTRUMENTOS DE LABORATORIO")
print("=" * 70)

# Crear instrumentos
balanza = InstrumentoLaboratorio(
    nombre="Balanza analítica",
    modelo="AX224",
    fabricante="Ohaus",
    año_fabricacion=2022,
    ubicacion="Mesa central"
)

phmetro = InstrumentoLaboratorio(
    nombre="pH-metro",
    modelo="pH700",
    fabricante="Eutech",
    año_fabricacion=2021,
    ubicacion="Campana 1"
)

espectrofotometro = InstrumentoLaboratorio(
    nombre="Espectrofotómetro UV-Vis",
    modelo="Genesys 150",
    fabricante="Thermo Scientific",
    año_fabricacion=2023,
    ubicacion="Sala de instrumentación"
)

# Usar los instrumentos
balanza.calibrar("2024-01-15")
phmetro.calibrar("2024-02-20")

balanza.usar(25.5)
phmetro.usar(42.0)
espectrofotometro.usar(15.0)  # No calibrado - mostrará advertencia

# Generar reportes
print("\nREPORTES DE INSTRUMENTOS:")
print("=" * 70)
print(balanza.generar_reporte())
print(phmetro.generar_reporte())
print(espectrofotometro.generar_reporte())

# Métodos de clase y estáticos
print("\nINFORMACIÓN GENERAL:")
print("=" * 70)
print(f"Total de instrumentos registrados: {InstrumentoLaboratorio.get_total_instrumentos()}")

año_prueba = 2025
valido = InstrumentoLaboratorio.validar_año_fabricacion(año_prueba)
print(f"Año {año_prueba} válido para fabricación: {'SÍ' if valido else 'NO'}")
```

### Constructor (`__init__`)

```python
class Experimento:
    """
    Clase que representa un experimento científico.
    
    El constructor inicializa todos los atributos necesarios
    y valida los parámetros de entrada.
    """
    
    def __init__(self, nombre, objetivo, hipotesis, duracion_horas, responsable):
        """
        Constructor de la clase Experimento.
        
        Parámetros:
        -----------
        nombre : str
            Nombre del experimento
        objetivo : str
            Objetivo científico
        hipotesis : str
            Hipótesis a probar
        duracion_horas : float
            Duración estimada en horas
        responsable : str
            Nombre del investigador responsable
        """
        # Atributos obligatorios
        self.nombre = nombre
        self.objetivo = objetivo
        self.hipotesis = hipotesis
        self.duracion_horas = duracion_horas
        self.responsable = responsable
        
        # Atributos con valores por defecto
        self.estado = "planificado"  # planificado, en_progreso, completado, cancelado
        self.fecha_inicio = None
        self.fecha_fin = None
        self.resultados = None
        self.conclusiones = None
        self.incidentes = []
        self.materiales = []
        self.metodos = []
        
        # Validaciones en el constructor
        self._validar_parametros()
        
        # Generar ID único
        import uuid
        self.id_experimento = str(uuid.uuid4())[:8]
        
        print(f"Experimento '{self.nombre}' creado con ID: {self.id_experimento}")
    
    def _validar_parametros(self):
        """Valida los parámetros del experimento."""
        if not self.nombre or len(self.nombre.strip()) < 3:
            raise ValueError("El nombre del experimento debe tener al menos 3 caracteres")
        
        if not self.objetivo:
            raise ValueError("Debe especificar un objetivo")
        
        if not self.hipotesis:
            raise ValueError("Debe especificar una hipótesis")
        
        if self.duracion_horas <= 0:
            raise ValueError("La duración debe ser positiva")
        
        if not self.responsable:
            raise ValueError("Debe especificar un responsable")
    
    def iniciar(self, fecha_inicio):
        """
        Inicia el experimento.
        
        Parámetros:
        -----------
        fecha_inicio : str
            Fecha de inicio en formato YYYY-MM-DD
        """
        if self.estado != "planificado":
            raise ValueError(f"No se puede iniciar un experimento en estado '{self.estado}'")
        
        self.estado = "en_progreso"
        self.fecha_inicio = fecha_inicio
        print(f"Experimento '{self.nombre}' iniciado el {fecha_inicio}")
    
    def agregar_material(self, material, cantidad, unidad):
        """
        Agrega un material al experimento.
        
        Parámetros:
        -----------
        material : str
            Nombre del material
        cantidad : float
            Cantidad necesaria
        unidad : str
            Unidad de medida
        """
        self.materiales.append({
            'material': material,
            'cantidad': cantidad,
            'unidad': unidad
        })
        print(f"Material agregado: {cantidad} {unidad} de {material}")
    
    def agregar_metodo(self, paso, descripcion):
