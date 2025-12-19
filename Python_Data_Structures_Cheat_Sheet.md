# Python Data Structures Cheat Sheet

Esta guía completa proporciona una referencia detallada de las principales estructuras de datos en Python, incluyendo sus métodos, casos de uso, complejidad temporal y ejemplos prácticos.

**Haz clic en cada estructura de datos para expandir su información detallada.**

## 📊 Tabla de Comparación Rápida

| Estructura | Mutable | Ordenada | Única | Complejidad Búsqueda | Caso de Uso Principal |
|------------|---------|----------|-------|---------------------|----------------------|
| List | ✅ | ✅ | ❌ | O(n) | Secuencias mutables |
| Tuple | ❌ | ✅ | ❌ | O(n) | Datos inmutables |
| Dict | ✅ | ❌ (3.7+) | ❌ | O(1) | Mapeo clave-valor |
| Set | ✅ | ❌ | ✅ | O(1) | Unicidad |
| Frozenset | ❌ | ❌ | ✅ | O(1) | Unicidad inmutable |
| Deque | ✅ | ✅ | ❌ | O(1) | Colas eficientes |
| NamedTuple | ❌ | ✅ | ❌ | O(n) | Datos estructurados |
| DefaultDict | ✅ | ❌ (3.7+) | ❌ | O(1) | Valores por defecto |
| Counter | ✅ | ❌ | ❌ | O(1) | Conteo de frecuencias |
| OrderedDict | ✅ | ✅ | ❌ | O(1) | Orden de inserción |

---

## 📋 Listas (Lists)

<details>
<summary>Ver detalles completos de Listas</summary>

### Descripción
Estructura de datos mutable y ordenada que puede contener elementos de diferentes tipos. Implementa arrays dinámicos.

### Complejidad Temporal
- Acceso por índice: O(1)
- Búsqueda: O(n)
- Inserción/Eliminación al final: O(1) amortizado
- Inserción/Eliminación en medio: O(n)

### Sintaxis Básica
```python
# Creación
lista = [1, 2, 3, 4, 5]
lista_vacia = []
lista_mixta = [1, "hola", 3.14, True]
lista_por_comprension = [x**2 for x in range(10)]

# Acceso por índice
primer_elemento = lista[0]        # 1
ultimo_elemento = lista[-1]       # 5
sub_lista = lista[1:4]           # [2, 3, 4]
reversa = lista[::-1]            # [5, 4, 3, 2, 1]
```

### Métodos Principales
- `append(x)`: Agrega un elemento al final - O(1)
- `extend(iterable)`: Extiende con elementos de un iterable - O(k)
- `insert(i, x)`: Inserta en posición i - O(n)
- `remove(x)`: Remueve primera ocurrencia de x - O(n)
- `pop([i])`: Remueve y devuelve elemento en i (último si no especifica) - O(1)/O(n)
- `index(x[, start[, end]])`: Índice de primera ocurrencia - O(n)
- `count(x)`: Cuenta ocurrencias de x - O(n)
- `sort(key=None, reverse=False)`: Ordena in-place - O(n log n)
- `reverse()`: Invierte in-place - O(n)
- `copy()`: Copia superficial - O(n)
- `clear()`: Remueve todos los elementos - O(1)

### Casos de Uso
- Almacenar colecciones de elementos que pueden cambiar
- Implementar pilas y colas simples
- Procesamiento de secuencias de datos
- Listas de tareas, historiales, buffers

### Ejemplos Avanzados
```python
# Pila (LIFO) - Last In, First Out
pila = []
pila.append('documento1')  # ['documento1']
pila.append('documento2')  # ['documento1', 'documento2']
ultimo = pila.pop()        # 'documento2', pila = ['documento1']

# Cola (FIFO) - First In, First Out (ineficiente con listas)
cola = []
cola.append('cliente1')    # ['cliente1']
cola.append('cliente2')    # ['cliente1', 'cliente2']
atendido = cola.pop(0)     # 'cliente1', cola = ['cliente2']

# Lista como buffer circular simple
buffer = [0] * 5
pos = 0
for i in range(10):
    buffer[pos] = i
    pos = (pos + 1) % len(buffer)
print(buffer)  # [5, 6, 7, 8, 9]
```

### Consejos
- Use `deque` para colas eficientes
- Para inserciones frecuentes en medio, considere `collections.deque` o estructuras enlazadas
- Las listas vacías son falsy: `if not lista:`

</details>

---

## 📄 Tuplas (Tuples)

<details>
<summary>Ver detalles completos de Tuplas</summary>

### Descripción
Estructura de datos inmutable y ordenada. Más eficiente que listas para datos que no cambian.

### Complejidad Temporal
- Acceso por índice: O(1)
- Búsqueda: O(n)
- Inmutable: No hay operaciones de modificación

### Sintaxis Básica
```python
# Creación
tupla = (1, 2, 3, 4, 5)
tupla_un_elemento = (1,)           # Nota la coma obligatoria
tupla_sin_parentesis = 1, 2, 3     # Tupla implícita
tupla_vacia = ()
tupla_anidada = ((1, 2), (3, 4))

# Acceso
primer_elemento = tupla[0]
ultimo = tupla[-1]
sub_tupla = tupla[1:4]             # (2, 3, 4)
```

### Métodos Principales
- `count(x)`: Cuenta ocurrencias de x - O(n)
- `index(x[, start[, end]])`: Índice de primera ocurrencia - O(n)

### Casos de Uso
- Datos que no deben cambiar (constantes)
- Claves de diccionarios (si contienen elementos hashables)
- Retornar múltiples valores de funciones
- Desempaquetado de variables
- Configuraciones inmutables

### Ejemplos Avanzados
```python
# Retorno múltiple de funciones
def dividir_con_resto(a, b):
    return a // b, a % b

cociente, resto = dividir_con_resto(17, 5)
print(f"{17} ÷ 5 = {cociente} con resto {resto}")  # 17 ÷ 5 = 3 con resto 2

# Desempaquetado avanzado
punto = (10, 20, 30)
x, y, z = punto
print(f"Coordenadas: x={x}, y={y}, z={z}")

# Ignorar valores con _
resultado, _ = dividir_con_resto(100, 7)  # Solo nos interesa el cociente

# Desempaquetado extendido
primero, *medio, ultimo = (1, 2, 3, 4, 5)
print(f"Primero: {primero}, Medio: {medio}, Último: {ultimo}")
# Primero: 1, Medio: [2, 3, 4], Último: 5

# Tuplas como claves de diccionario
coordenadas_a_colores = {
    (0, 0): "negro",
    (255, 0, 0): "rojo",
    (0, 255, 0): "verde",
    (0, 0, 255): "azul"
}
```

### Consejos
- Más eficientes en memoria que listas
- Pueden contener cualquier tipo de objeto
- Hashables si todos sus elementos lo son
- Útiles para datos de configuración que no cambian

</details>

---

## 📚 Diccionarios (Dictionaries)

<details>
<summary>Ver detalles completos de Diccionarios</summary>

### Descripción
Estructura de datos mutable que almacena pares clave-valor. Implementa tablas hash.

### Complejidad Temporal
- Acceso/Búsqueda/Inserción/Eliminación: O(1) promedio
- Peor caso: O(n) (colisiones hash)
- Iteración: O(n)

### Sintaxis Básica
```python
# Creación
diccionario = {'clave1': 'valor1', 'clave2': 'valor2'}
dict_vacio = {}
dict_por_comprension = {x: x**2 for x in range(5)}  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
dict_desde_iterables = dict(zip(['a', 'b', 'c'], [1, 2, 3]))  # {'a': 1, 'b': 2, 'c': 3}

# Acceso
valor = diccionario['clave1']
valor_default = diccionario.get('clave_inexistente', 'default')
valor_o_error = diccionario.setdefault('nueva_clave', 'valor_default')
```

### Métodos Principales
- `keys()`: Vista de claves - O(1)
- `values()`: Vista de valores - O(1)
- `items()`: Vista de pares (clave, valor) - O(1)
- `get(key[, default])`: Valor de clave o default - O(1)
- `pop(key[, default])`: Remueve y devuelve valor - O(1)
- `popitem()`: Remueve y devuelve último par - O(1)
- `update([other])`: Actualiza con otro dict - O(m)
- `clear()`: Remueve todos los elementos - O(1)
- `copy()`: Copia superficial - O(n)

### Casos de Uso
- Almacenar datos con acceso rápido por clave
- Conteo de frecuencias
- Mapeo de relaciones
- Configuraciones y parámetros
- Caché de resultados

### Ejemplos Avanzados
```python
# Conteo de frecuencias optimizado
def contar_palabras(texto):
    palabras = texto.lower().split()
    frecuencias = {}
    for palabra in palabras:
        frecuencias[palabra] = frecuencias.get(palabra, 0) + 1
    return frecuencias

texto = "el gato negro salta sobre el perro blanco"
resultado = contar_palabras(texto)
print(resultado)  # {'el': 2, 'gato': 1, 'negro': 1, 'salta': 1, 'sobre': 1, 'perro': 1, 'blanco': 1}

# Configuración con valores por defecto
config = {
    'host': 'localhost',
    'port': 8080,
    'debug': True,
    'timeout': 30
}

# Merge de diccionarios (Python 3.9+)
config_actualizada = config | {'port': 9000, 'ssl': True}
print(config_actualizada)
# {'host': 'localhost', 'port': 9000, 'debug': True, 'timeout': 30, 'ssl': True}

# Diccionario como caché simple
cache = {}
def fibonacci_cacheado(n):
    if n in cache:
        return cache[n]
    if n <= 1:
        cache[n] = n
        return n
    cache[n] = fibonacci_cacheado(n-1) + fibonacci_cacheado(n-2)
    return cache[n]
```

### Consejos
- Las claves deben ser hashables (inmutables)
- El orden se mantiene desde Python 3.7+
- `dict.keys()`, `dict.values()`, `dict.items()` devuelven vistas, no listas
- Use `collections.defaultdict` para valores por defecto automáticos

</details>

---

## 🔗 Conjuntos (Sets)

<details>
<summary>Ver detalles completos de Conjuntos</summary>

### Descripción
Estructura de datos mutable que almacena elementos únicos sin orden. Implementa tablas hash.

### Complejidad Temporal
- Búsqueda/Inserción/Eliminación: O(1) promedio
- Operaciones entre conjuntos: O(min(len(s), len(t)))
- Iteración: O(n)

### Sintaxis Básica
```python
# Creación
conjunto = {1, 2, 3, 4, 5}
conjunto_vacio = set()  # No usar {} que crea diccionario vacío
set_por_comprension = {x for x in range(10) if x % 2 == 0}  # {0, 2, 4, 6, 8}
set_desde_iterable = set([1, 2, 2, 3, 3, 3])  # {1, 2, 3}

# Operaciones básicas
conjunto.add(6)           # Agrega elemento
conjunto.remove(3)        # Error si no existe
conjunto.discard(10)      # No error si no existe
elemento = conjunto.pop() # Remueve elemento arbitrario
```

### Métodos Principales
- `add(x)`: Agrega elemento - O(1)
- `remove(x)`: Remueve elemento (error si no existe) - O(1)
- `discard(x)`: Remueve elemento (sin error) - O(1)
- `pop()`: Remueve y devuelve elemento arbitrario - O(1)
- `clear()`: Remueve todos los elementos - O(1)
- `copy()`: Copia superficial - O(n)

### Operaciones entre Conjuntos
- `union(*others)` o `|`: Unión - O(len(s) + len(t))
- `intersection(*others)` o `&`: Intersección - O(min(len(s), len(t)))
- `difference(*others)` o `-`: Diferencia - O(len(s))
- `symmetric_difference(other)` o `^`: Diferencia simétrica - O(len(s))
- `issubset(other)` o `<=`: Subconjunto - O(len(s))
- `issuperset(other)` o `>=`: Superconjunto - O(len(t))
- `isdisjoint(other)`: Conjuntos disjuntos - O(min(len(s), len(t)))

### Casos de Uso
- Eliminar duplicados de colecciones
- Operaciones matemáticas de conjuntos
- Verificación rápida de pertenencia
- Filtrado de datos únicos
- Implementación de grafos

### Ejemplos Avanzados
```python
# Eliminar duplicados manteniendo orden (Python 3.7+)
def eliminar_duplicados_manteniendo_orden(iterable):
    return list(dict.fromkeys(iterable))

lista = [1, 2, 2, 3, 1, 4, 3, 5]
unicos = eliminar_duplicados_manteniendo_orden(lista)
print(unicos)  # [1, 2, 3, 4, 5]

# Análisis de conjuntos
estudiantes_matematicas = {"Ana", "Juan", "María", "Pedro"}
estudiantes_fisica = {"Juan", "Pedro", "Carlos", "Luis"}

# Operaciones de conjuntos
solo_matematicas = estudiantes_matematicas - estudiantes_fisica  # {"Ana", "María"}
solo_fisica = estudiantes_fisica - estudiantes_matematicas       # {"Carlos", "Luis"}
ambas_materias = estudiantes_matematicas & estudiantes_fisica    # {"Juan", "Pedro"}
una_o_ambas = estudiantes_matematicas | estudiantes_fisica       # {"Ana", "Juan", "María", "Pedro", "Carlos", "Luis"}

# Verificación de pertenencia rápida
usuarios_premium = {"user123", "user456", "user789"}
def es_premium(usuario):
    return usuario in usuarios_premium

print(es_premium("user123"))  # True
print(es_premium("user999"))  # False
```

### Consejos
- Más eficientes que listas para verificación de pertenencia
- No mantienen orden (use `collections.OrderedDict` si lo necesita)
- Solo elementos hashables
- `frozenset` para versiones inmutables

</details>

---

## ❄️ Conjuntos Inmutables (Frozensets)

<details>
<summary>Ver detalles de Frozensets</summary>

### Descripción
Versión inmutable de los conjuntos. Hashables y pueden ser usados como claves de diccionarios.

### Complejidad Temporal
- Mismas que sets: O(1) promedio para operaciones

### Sintaxis Básica
```python
frozenset_inmutable = frozenset([1, 2, 3, 4, 5])
frozenset_vacio = frozenset()
frozenset_desde_set = frozenset({1, 2, 3})
```

### Casos de Uso
- Claves de diccionarios o elementos de otros sets
- Datos que no deben modificarse
- Caching de resultados de operaciones de conjuntos

### Ejemplos
```python
# Usar frozenset como clave de diccionario
cache_resultados = {}
conjunto_busqueda = frozenset([1, 2, 3])
cache_resultados[conjunto_busqueda] = "resultado"

# Set de sets
set_de_conjuntos = {frozenset([1, 2]), frozenset([3, 4])}
```

</details>

---

## 🔄 Deque (Double-Ended Queue)

<details>
<summary>Ver detalles completos de Deque</summary>

### Descripción
Cola de doble extremo de `collections.deque`. Eficiente para operaciones en ambos extremos.

### Complejidad Temporal
- Acceso por índice: O(1)
- Inserción/Eliminación en extremos: O(1)
- Inserción/Eliminación en medio: O(n)
- Rotación: O(k)

### Sintaxis Básica
```python
from collections import deque

# Creación
cola = deque([1, 2, 3])
cola_vacia = deque()
cola_con_maxlen = deque(maxlen=5)  # Cola circular automática

# Operaciones en extremos
cola.append(4)         # Agrega al final: [1, 2, 3, 4]
cola.appendleft(0)     # Agrega al inicio: [0, 1, 2, 3, 4]
final = cola.pop()     # Remueve del final: 4, cola = [0, 1, 2, 3]
inicio = cola.popleft() # Remueve del inicio: 0, cola = [1, 2, 3]
```

### Métodos Principales
- `append(x)`: Agrega al final - O(1)
- `appendleft(x)`: Agrega al inicio - O(1)
- `pop()`: Remueve del final - O(1)
- `popleft()`: Remueve del inicio - O(1)
- `extend(iterable)`: Extiende al final - O(k)
- `extendleft(iterable)`: Extiende al inicio - O(k)
- `rotate(n)`: Rota n posiciones - O(k)
- `clear()`: Remueve todos los elementos - O(1)

### Casos de Uso
- Implementar colas eficientes (FIFO)
- Implementar pilas eficientes (LIFO)
- Buffers circulares
- Algoritmos que requieren acceso a ambos extremos
- Implementación de estructuras como sliding window

### Ejemplos Avanzados
```python
from collections import deque

# Cola FIFO eficiente
cola_atencion = deque()
cola_atencion.append("Cliente 1")
cola_atencion.append("Cliente 2")
cola_atencion.append("Cliente 3")

while cola_atencion:
    cliente = cola_atencion.popleft()
    print(f"Atendiendo a {cliente}")

# Pila LIFO eficiente
pila_navegador = deque()
pila_navegador.append("pagina1.html")
pila_navegador.append("pagina2.html")
pila_navegador.append("pagina3.html")

# Simular "volver atrás"
pagina_actual = pila_navegador.pop()  # pagina3.html
pagina_anterior = pila_navegador.pop()  # pagina2.html

# Buffer circular con maxlen
buffer_sensores = deque(maxlen=10)
for i in range(15):
    buffer_sensores.append(f"lectura_{i}")
    print(f"Buffer: {list(buffer_sensores)}")
# El buffer mantiene solo las últimas 10 lecturas

# Sliding window maximum (ventana deslizante)
def maximo_ventana(nums, k):
    if not nums:
        return []

    resultado = []
    ventana = deque()

    for i, num in enumerate(nums):
        # Remover elementos fuera de la ventana
        while ventana and ventana[0] <= i - k:
            ventana.popleft()

        # Remover elementos menores que el actual
        while ventana and nums[ventana[-1]] <= num:
            ventana.pop()

        ventana.append(i)

        # El primer elemento de la ventana es el máximo
        if i >= k - 1:
            resultado.append(nums[ventana[0]])

    return resultado

print(maximo_ventana([1, 3, -1, -3, 5, 3, 6, 7], 3))
# [3, 3, 5, 5, 6, 7]
```

### Consejos
- Mucho más eficiente que listas para operaciones en extremos
- Use `maxlen` para buffers circulares automáticos
- Ideal para algoritmos de sliding window
- Thread-safe para operaciones append/pop

</details>

---

## 🏷️ NamedTuple

<details>
<summary>Ver detalles completos de NamedTuple</summary>

### Descripción
Tupla con campos nombrados de `collections.namedtuple`. Inmutable y eficiente en memoria.

### Complejidad Temporal
- Mismas que tuplas: O(1) acceso por índice, O(n) búsqueda

### Sintaxis Básica
```python
from collections import namedtuple

# Definición
Persona = namedtuple('Persona', ['nombre', 'edad', 'ciudad'])
Empleado = namedtuple('Empleado', 'id nombre salario', defaults=[None, None, 0])

# Creación
persona1 = Persona('Juan', 25, 'Madrid')
persona2 = Persona(nombre='María', edad=30, ciudad='Barcelona')
empleado1 = Empleado(1, 'Pedro', 50000)
empleado2 = Empleado(id=2, nombre='Ana')  # salario usa default 0

# Acceso
print(persona1.nombre)    # 'Juan'
print(persona1[1])        # 25
nombre, edad, ciudad = persona1  # Desempaquetado
```

### Métodos y Atributos
- `_fields`: Tupla con nombres de campos
- `_field_defaults`: Diccionario con valores por defecto
- `_replace(**kwargs)`: Crea nueva instancia con campos modificados
- `_asdict()`: Convierte a diccionario

### Casos de Uso
- Representar datos estructurados de forma inmutable
- Mejorar legibilidad del código vs tuplas simples
- Alternativa ligera a clases de datos simples
- Retorno de funciones con datos nombrados

### Ejemplos Avanzados
```python
from collections import namedtuple

# Definir estructuras de datos
Punto = namedtuple('Punto', ['x', 'y'])
Circulo = namedtuple('Circulo', ['centro', 'radio'])
Rectangulo = namedtuple('Rectangulo', ['esquina1', 'esquina2'])

# Crear instancias
p1 = Punto(0, 0)
p2 = Punto(3, 4)
circulo = Circulo(centro=Punto(1, 1), radio=5)
rect = Rectangulo(esquina1=p1, esquina2=p2)

# Acceso legible
print(f"Círculo en {circulo.centro} con radio {circulo.radio}")
print(f"Rectángulo de {rect.esquina1} a {rect.esquina2}")

# Conversión a diccionario
circulo_dict = circulo._asdict()
print(circulo_dict)  # {'centro': Punto(x=1, y=1), 'radio': 5}

# Creación modificada
circulo_grande = circulo._replace(radio=10)
print(circulo_grande)  # Circulo(centro=Punto(x=1, y=1), radio=10)

# Función que retorna datos estructurados
def analizar_texto(texto):
    palabras = texto.split()
    return namedtuple('AnalisisTexto', ['palabras', 'longitud', 'unicas'])(
        palabras=len(palabras),
        longitud=sum(len(p) for p in palabras),
        unicas=len(set(palabras))
    )

resultado = analizar_texto("el gato negro salta sobre el perro blanco")
print(f"Palabras: {resultado.palabras}, Longitud total: {resultado.longitud}, Únicas: {resultado.unicas}")
```

### Consejos
- Más eficiente en memoria que clases
- Inmutables por defecto
- Campos accesibles por nombre o índice
- Útil para APIs que retornan datos estructurados

</details>

---

## 🔧 DefaultDict

<details>
<summary>Ver detalles completos de DefaultDict</summary>

### Descripción
Diccionario que proporciona valores por defecto para claves inexistentes de `collections.defaultdict`.

### Complejidad Temporal
- Mismas que dict: O(1) promedio para operaciones

### Sintaxis Básica
```python
from collections import defaultdict

# Valor por defecto: lista vacía
dd_lista = defaultdict(list)
dd_lista['a'].append(1)  # {'a': [1]}
dd_lista['b'].append(2)  # {'b': [2]}

# Valor por defecto: 0
dd_int = defaultdict(int)
dd_int['contador'] += 1  # {'contador': 1}

# Valor por defecto: conjunto
dd_set = defaultdict(set)
dd_set['letras'].add('a')  # {'letras': {'a'}}

# Función personalizada como factory
dd_custom = defaultdict(lambda: "valor_default")
print(dd_custom['nueva'])  # "valor_default"
```

### Factory Functions Comunes
- `int`: 0
- `float`: 0.0
- `str`: ""
- `list`: []
- `dict`: {}
- `set`: set()
- `lambda: valor`: Cualquier valor personalizado

### Casos de Uso
- Conteo de frecuencias sin verificación previa
- Agrupación de datos por categorías
- Construcción de grafos y árboles
- Caché con valores por defecto

### Ejemplos Avanzados
```python
from collections import defaultdict

# Conteo de palabras por longitud
def contar_por_longitud(texto):
    palabras = texto.split()
    conteo = defaultdict(int)
    for palabra in palabras:
        conteo[len(palabra)] += 1
    return dict(conteo)  # Convertir a dict normal

texto = "el gato negro salta sobre el perro blanco"
resultado = contar_por_longitud(texto)
print(resultado)  # {2: 2, 4: 2, 5: 2, 6: 1, 6: 1, 5: 1, 6: 1}

# Agrupación de datos
def agrupar_por_inicial(datos):
    grupos = defaultdict(list)
    for dato in datos:
        inicial = dato[0].upper()
        grupos[inicial].append(dato)
    return dict(grupos)

nombres = ["Ana", "Antonio", "Beatriz", "Carlos", "Carmen"]
agrupados = agrupar_por_inicial(nombres)
print(agrupados)
# {'A': ['Ana', 'Antonio'], 'B': ['Beatriz'], 'C': ['Carlos', 'Carmen']}

# Grafo de adyacencia
grafo = defaultdict(list)
grafo['A'].extend(['B', 'C'])
grafo['B'].extend(['A', 'D'])
grafo['C'].extend(['A', 'D'])
grafo['D'].extend(['B', 'C'])

print(dict(grafo))  # {'A': ['B', 'C'], 'B': ['A', 'D'], 'C': ['A', 'D'], 'D': ['B', 'C']}

# Análisis de logs
def analizar_logs(logs):
    estadisticas = defaultdict(lambda: {'count': 0, 'errors': 0})
    for log in logs:
        partes = log.split()
        usuario = partes[0]
        tipo = partes[1]
        estadisticas[usuario]['count'] += 1
        if tipo == 'ERROR':
            estadisticas[usuario]['errors'] += 1
    return dict(estadisticas)

logs = [
    "user1 INFO login",
    "user2 ERROR timeout",
    "user1 INFO action",
    "user2 INFO login",
    "user1 ERROR failed"
]

stats = analizar_logs(logs)
print(stats)
# {'user1': {'count': 3, 'errors': 1}, 'user2': {'count': 2, 'errors': 1}}
```

### Consejos
- Evita KeyError automáticamente
- Más eficiente que usar `dict.get()` con valores por defecto
- Factory function se llama solo cuando se necesita el valor por defecto
- Convierte a dict normal si necesitas serializar o pasar a funciones que esperan dict

</details>

---

## 🧮 Counter

<details>
<summary>Ver detalles completos de Counter</summary>

### Descripción
Diccionario especializado para conteo de elementos hashables de `collections.Counter`.

### Complejidad Temporal
- Mismas que dict: O(1) promedio
- `most_common(k)`: O(n log k) aproximadamente

### Sintaxis Básica
```python
from collections import Counter

# Creación
contador = Counter(['a', 'b', 'a', 'c', 'a', 'b'])
# Counter({'a': 3, 'b': 2, 'c': 1})

contador2 = Counter("palabra")  # Counter({'a': 2, 'r': 1, 'b': 1, 'l': 1, 'p': 1})
contador3 = Counter({'a': 1, 'b': 2})  # Counter({'b': 2, 'a': 1})

# Acceso
print(contador['a'])     # 3
print(contador['z'])     # 0 (no existe, devuelve 0)

# Más comunes
print(contador.most_common(2))  # [('a', 3), ('b', 2)]
```

### Métodos Principales
- `most_common([n])`: n elementos más comunes
- `elements()`: Iterador sobre elementos (repite según conteo)
- `subtract([iterable-or-mapping])`: Resta conteos
- `update([iterable-or-mapping])`: Suma conteos
- `keys()`, `values()`, `items()`: Vistas como dict

### Operaciones Matemáticas
- Suma: `counter1 + counter2`
- Resta: `counter1 - counter2`
- Intersección: `counter1 & counter2` (mínimo común)
- Unión: `counter1 | counter2` (máximo común)

### Casos de Uso
- Análisis de frecuencias en texto o datos
- Conteo de elementos en colecciones grandes
- Estadísticas básicas
- Análisis de logs y eventos

### Ejemplos Avanzados
```python
from collections import Counter

# Análisis de texto avanzado
def analizar_frecuencia_palabras(texto, n_mas_comunes=5):
    palabras = texto.lower().split()
    # Filtrar palabras comunes
    palabras_filtradas = [p for p in palabras if len(p) > 2]
    contador = Counter(palabras_filtradas)
    return contador.most_common(n_mas_comunes)

texto = """
Python es un lenguaje de programación interpretado cuya filosofía hace hincapié
en la legibilidad de su código. Se trata de un lenguaje de programación multiparadigma,
ya que soporta parcialmente la orientación a objetos, programación imperativa y,
en menor medida, programación funcional.
"""

frecuencias = analizar_frecuencia_palabras(texto)
print("Palabras más frecuentes:")
for palabra, count in frecuencias:
    print(f"  {palabra}: {count}")

# Análisis de logs
def analizar_errores_por_hora(logs):
    errores_por_hora = Counter()
    for log in logs:
        if 'ERROR' in log:
            # Extraer hora del log (asumiendo formato "HH:MM:SS ERROR mensaje")
            hora = log.split()[0].split(':')[0]
            errores_por_hora[hora] += 1
    return errores_por_hora

logs = [
    "10:15:23 INFO usuario login",
    "10:16:45 ERROR conexión fallida",
    "11:02:12 INFO procesamiento completado",
    "11:05:33 ERROR timeout",
    "11:15:01 ERROR conexión fallida",
    "12:00:00 INFO backup iniciado"
]

errores = analizar_errores_por_hora(logs)
print(f"Errores por hora: {dict(errores)}")

# Operaciones entre counters
ventas_lunes = Counter(manzana=10, banana=5, naranja=8)
ventas_martes = Counter(manzana=12, banana=3, naranja=6, pera=4)

# Comparar ventas
diferencia = ventas_martes - ventas_lunes  # Solo incrementos
print(f"Incremento en ventas: {dict(diferencia)}")

# Ventas mínimas (intersección)
ventas_minimas = ventas_lunes & ventas_martes
print(f"Ventas mínimas diarias: {dict(ventas_minimas)}")

# Ventas totales (unión)
ventas_totales = ventas_lunes | ventas_martes
print(f"Ventas totales: {dict(ventas_totales)}")
```

### Consejos
- Más eficiente que defaultdict(int) para conteo simple
- Soporta operaciones matemáticas entre contadores
- `elements()` es útil para reconstruir la colección original
- `most_common()` sin argumentos devuelve todos ordenados

</details>

---

## 📋 OrderedDict

<details>
<summary>Ver detalles completos de OrderedDict</summary>

### Descripción
Diccionario que mantiene el orden de inserción de `collections.OrderedDict`.

### Complejidad Temporal
- Mismas que dict: O(1) promedio
- `move_to_end()`: O(1)

### Sintaxis Básica
```python
from collections import OrderedDict

od = OrderedDict()
od['primero'] = 1
od['segundo'] = 2
od['tercero'] = 3

# Mantiene orden de inserción
print(list(od.keys()))  # ['primero', 'segundo', 'tercero']

# Reordenar
od.move_to_end('primero')  # Mueve 'primero' al final
print(list(od.keys()))    # ['segundo', 'tercero', 'primero']
```

### Métodos Adicionales
- `move_to_end(key, last=True)`: Mueve clave al final (o inicio si last=False)
- `popitem(last=True)`: Remueve último par (o primero si last=False)

### Casos de Uso
- Cuando el orden de inserción es importante
- Implementaciones de LRU cache
- Procesamiento de datos ordenados
- Mantener orden en configuraciones

### Ejemplos
```python
# LRU Cache simple
class LRUCache:
    def __init__(self, capacity):
        self.cache = OrderedDict()
        self.capacity = capacity

    def get(self, key):
        if key in self.cache:
            self.cache.move_to_end(key)  # Marcar como usado recientemente
            return self.cache[key]
        return -1

    def put(self, key, value):
        if key in self.cache:
            self.cache.move_to_end(key)
        self.cache[key] = value
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)  # Remover el menos reciente

# Uso
cache = LRUCache(3)
cache.put(1, 'a')
cache.put(2, 'b')
cache.put(3, 'c')
print(cache.get(1))  # 'a' (mueve al final)
cache.put(4, 'd')    # Remueve el 2 (menos reciente)
```

</details>

---

## 🔗 ChainMap

<details>
<summary>Ver detalles de ChainMap</summary>

### Descripción
Combina múltiples diccionarios en una sola vista de `collections.ChainMap`.

### Sintaxis Básica
```python
from collections import ChainMap

dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 20, 'c': 30}
dict3 = {'c': 300, 'd': 400}

chain = ChainMap(dict1, dict2, dict3)
print(chain['a'])  # 1 (del primer dict)
print(chain['b'])  # 2 (del primer dict, no 20)
print(chain['c'])  # 30 (del segundo dict, no 300)
print(chain['d'])  # 400 (del tercer dict)
```

### Casos de Uso
- Configuraciones con valores por defecto
- Variables de entorno y configuraciones locales
- Búsqueda en múltiples contextos

</details>

---

## 💡 Consejos Generales y Mejores Prácticas

<details>
<summary>Ver consejos generales y mejores prácticas</summary>

### 1. Elegir la Estructura Correcta

**Para datos que cambian frecuentemente:**
- Use `list` para secuencias ordenadas mutables
- Use `dict` para acceso rápido por clave
- Use `set` para unicidad y pertenencia rápida

**Para datos inmutables:**
- Use `tuple` para secuencias ordenadas
- Use `frozenset` para conjuntos inmutables
- Use `namedtuple` para datos estructurados

### 2. Eficiencia y Complejidad

| Operación | List | Tuple | Dict | Set | Deque |
|-----------|------|-------|------|-----|-------|
| Acceso por índice | O(1) | O(1) | - | - | O(1) |
| Búsqueda | O(n) | O(n) | O(1) | O(1) | O(n) |
| Inserción final | O(1) | - | O(1) | O(1) | O(1) |
| Inserción inicio | O(n) | - | - | - | O(1) |
| Eliminación final | O(1) | - | O(1) | O(1) | O(1) |
| Eliminación inicio | O(n) | - | - | - | O(1) |

### 3. Inmutabilidad vs Mutabilidad

**Ventajas de estructuras inmutables:**
- Thread-safe sin sincronización
- Hashables (pueden ser claves de dict/set)
- Previenen modificaciones accidentales
- Más eficientes en memoria para datos compartidos

**Cuándo usar inmutables:**
- Claves de diccionarios
- Elementos de conjuntos
- Constantes y configuraciones
- Datos que se pasan entre funciones/hilos

### 4. Comprensions y Generadores

```python
# List comprehension
cuadrados = [x**2 for x in range(10) if x % 2 == 0]

# Dict comprehension
cuadrados_dict = {x: x**2 for x in range(10)}

# Set comprehension
cuadrados_set = {x**2 for x in range(10)}

# Generator (más eficiente para grandes datos)
cuadrados_gen = (x**2 for x in range(10))
```

### 5. Collections Module

**Estructuras avanzadas:**
- `deque`: Colas eficientes
- `defaultdict`: Valores por defecto
- `Counter`: Conteo de frecuencias
- `namedtuple`: Tuplas con nombres
- `OrderedDict`: Dict con orden
- `ChainMap`: Múltiples dicts como uno

### 6. Patrones Comunes

**Eliminar duplicados manteniendo orden (Python 3.7+):**
```python
unicos = list(dict.fromkeys(iterable))
```

**Contar frecuencias:**
```python
from collections import Counter
frecuencias = Counter(iterable)
```

**Agrupar datos:**
```python
from collections import defaultdict
grupos = defaultdict(list)
for item in datos:
    grupos[categoria(item)].append(item)
```

### 7. Consideraciones de Memoria

- `tuple` usa menos memoria que `list`
- `set` puede usar más memoria que `list` para pocos elementos
- `dict` overhead por tabla hash
- `namedtuple` más eficiente que clases simples

### 8. Debugging y Testing

```python
# Verificar tipos
assert isinstance(datos, list)
assert all(isinstance(x, int) for x in datos)

# Verificar estructura
from collections.abc import Mapping, Sequence
assert isinstance(config, Mapping)
assert isinstance(secuencia, Sequence)
```

### 9. Serialización

```python
import json

# Solo tipos nativos serializables
datos_serializables = {
    'lista': [1, 2, 3],
    'tupla': (1, 2, 3),  # Se convierte a lista
    'dict': {'a': 1, 'b': 2},
    'set': list({1, 2, 3})  # Convertir a lista
}
```

### 10. Alternativas Modernas (Python 3.9+)

```python
# Dict merge
config = base_config | user_config

# Dict update con |
d1 = {'a': 1, 'b': 2}
d2 = {'b': 20, 'c': 30}
merged = d1 | d2  # {'a': 1, 'b': 20, 'c': 30}
```

Esta guía completa cubre las estructuras de datos más importantes en Python. Para documentación oficial, visita [docs.python.org](https://docs.python.org/3/library/stdtypes.html) y [docs.python.org/3/library/collections.html](https://docs.python.org/3/library/collections.html).

</details>
