# Quadratic-Assignment-Problem


## Definición del problema
Planteado por Koopmans y Beckmann en 1957, el problema de asignación cuadrática (QAP) es un problema clásico de optimización combinatoria de alta complejidad que pertenece a la clase de los problemas NP-completos, el cual **trata de asignar $n$ instalaciones a una misma cantidad $n$ de localizaciones con un coste asociado a cada una de ellas. Este coste depende de las distancias y flujos entre las instalaciones**, además de que puede existir un coste adicional por instalar cierta facilidad en cierta localización específica. El objetivo es buscar aquella combinación que minimice el coste total.

![QAP_1](https://user-images.githubusercontent.com/25113662/226206123-901ea03f-bc6b-4e68-b4aa-81cfd6aa2dd6.PNG)

Como cualquier problema de combinatoria, el QAP puede resolverse mediante métodos exactos o aproximados. El método exacto más eficiente que ha logrado resolver el QAP ha sido el Branch & Bound para el tamaño de la instancia de orden 30. Otros métodos exactos que se suelen implementar para resolver problemas de este tipo son el método de planos de corte, la programación dinámica e incluso se han propuesto métodos de relajación de la función objetivo para linealizarla que consisten en transformar el problema haciendo cambios de variables de tal manera que se elimine el término cuadrático de la función objetivo. Lamentablemente estos métodos exactos son incapaces de resolver este problema debido a la necesidad de ofrecer respuestas en tiempos razonables y por ese motivo se han implementado metaheurísticas que evitan la enumeración total y mediante estrategias bien definidas efectúan búsquedas parciales en el espacio de soluciones.
De momento algunas de las metaheurísticas más eficientes que se han usado para resolver el QAP son: 
* _Búsqueda Tabú_
* _Algoritmos Genéticos_
* _Recocido Simulado_
* _Colonia de Hormigas_
* Búsqueda Dispersa o Scatter Search
* GRASP

y su combinación entre ellos para formar los Algoritmos Híbridos.

### Aplicaciones
El QAP inicialmente fue planteada como una técnica enfocada a la economía, sin embargo, sus aplicaciones han empezado a cubrir  otros campos muy variados. Algunas aplicaciones son:
* Logística e infraestructuras aeroportuarias
* Diseño de componentes electrónicos
* Planificación y diseño de:
  * Centros comerciales 
  * Campus universitario
  * Hospitales
* Problemas de flujo en línea generalizado

![QAP_8](https://user-images.githubusercontent.com/25113662/226206188-a7c8fb3d-4d52-4f89-938d-350fe2032625.png)

## Ejemplo
![QAP_14](https://user-images.githubusercontent.com/25113662/227623633-d7ab4f10-eaff-4ef4-8cf7-e14ed1dd0248.PNG)

![QAP_11](https://user-images.githubusercontent.com/25113662/227624060-0b7317bd-8fb1-4362-8bb7-bd0d1833a5dd.png)


Se pretende mostrar como tenemos el problema de asignar 4 entidades como por ejemplo unas fábricas, en 4 localidades diferentes. El gráfico muestra una posible solución asignando la fábricas 1 en la ciudad 2, la fábricas 2 en la localidad 1, la fábricas 3 en la ciudad 4 y por última la fábricas 4 en la localidad 3.
La manera más común de plantear el problema de forma combinatoria matemáticamente es de la siguiente manera:
```math
{\Huge \sum_{i=1}^{n} {\sum_{j=1}^{n} { f_{ij} d_{p(i) p(j)} }} }
```
Donde $f$ y $d$ son las matrices de flujos y distancias de tamaño $nxn$ cuyos índices $i$, $j$ en la matriz de flujos representan el flujo entre las entidades de $i$ a $j$ y a su vez los mismos índices $i$, $j$ para la matriz de distancias representan las distancias entre las localidades $i$ y $j$. El vector $p$ es una permutación de números {1,2,…,n} siendo $p(j)$ la localización donde la entidad $j$ es asignada.

### Representación de la solución
La solución es la permutación $p$ en $S_n$ que permita la minimización de la doble sumatoria. **La solución se representa como un arreglo de números en el rango de 1 a n, dichos valores no se repiten**.
![QAP_12](https://user-images.githubusercontent.com/25113662/227285012-5d85d778-2253-40f1-acb0-87b9f515fd2a.png)


### Solución inicial
Como el problema es de permutación, la solución inicial se genera de manera aleatoria. Cuando nuestra `n = 4`, una posible solución inicial podría ser: `[2, 1, 4, 3]`

### Generación de soluciones vecinas
Para generar soluciones vecinas se selecciona de forma aleatoria dos elementos del vector para después intercambiarlos. Por ejemplo, si nuestra solución actual es `[2, 1, 4, 3]` y generamos de forma aleatoria los índices `0` y `3`, después de intercambiar sus valores la solución vecina sería `[3, 1, 4, 2]`.

### Función objetivo
La función objetivo es la que se encarga de evaluar la solución actual. En este caso, la función objetivo es la doble sumatoria que se mencionó anteriormente. Esta sería:
```python
def f(x: list[int], flows: np.ndarray, distances: np.ndarray) -> float:
    """Función objetivo para el Problema de Asignación Cuadrática.

    Parameters
    ----------
    x : list[int]
        La solución a evaluar, es decir, la permutación de las entidades. Es de tamaño n.
    flows : np.ndarray
		Matriz de flujos. Es de tamaño nxn.
    distances : np.ndarray
		Matriz de distancias. Es de tamaño nxn.

    Returns
    -------
    float
        Costo de la solución x.
    """

    # Obtenemos el número de entidades
    n = len(x)

    # Acumulador para el calculo del costo
    cost = 0

    for i in range(n):
        for j in range(n):
            cost += flows[i, j] * distances[x[i] - 1, x[j] - 1]

    return cost
```
`NOTA:` Se resta 1 a los valores del vector pues su rango es de 1 a n, pero dado que en la fórmula se utilizan como índices, se les resta -1 para que coincidan con la forma en que se accede a los elementos de las matrices (que empiezan en 0).

### Instancias a resolver
La siguiente tabla muestra las instancias que se van a resolver. Cada instancia tiene un tamaño de `n` entidades y se cuenta con las matrices de flujos y distancias de tamaño `nxn`.

| Instancia    | _n_ | Costo | Solución |
| :---:        |:---:|  :---: |  :---: |
| chr12.csv   | 12| 9742     | (5,7,1,10,11,3,4,2,9,6,12,8) |
| tai100.csv  |100| 21052466 | (...) |
| tai256.csv  |256| 44759294 | (...) |

### Como leer los CSVs de las instancias
En el archivo `Instancias2024.zip` se encuentran los archivos CSV con las matrices de flujos y distancias divididos en carpetas. Es importante notar que cada carpeta tiene 2 archivos, los que terminan en `*A.csv` contienen la matriz de flujos y los que terminan en `*B.csv`, la matriz de distancias del problema.

Para leerlos, por ejemplo, para `Chr12`, se puede hacer de la siguiente manera:

```python
import numpy as np

flows = np.loadtxt("Chr12/Chr12A.csv", delimiter=",")
distances = np.loadtxt("Chr12/Chr12B.csv", delimiter=",")

# Obtenemos el número de entidades
n = flows.shape[0]
```

### Tip
Como la función objetivo recibe 3 parámetros pero la metaheurística solo pueden mandar 1, que es el vector solución (el parámetro `x` en la función), se puede hacer uso de la función `functools.partial` para crear una función que reciba solo un parámetro y que los otros dos sean fijos. Por ejemplo:

```python
import functools

# Se fijan los valores de flows y distances
fn = functools.partial(f, flows=flows, distances=distances)

# Se manda la función generada a la metaheurística
sa.run(fn, objective_type="min")
```

De esta forma aseguramos que a la metaheurística solo le importe mandar el vector solución a la función objetivo sin preocuparse por las matrices de flujo y distancia pues ya están implícitas en la llamada. 