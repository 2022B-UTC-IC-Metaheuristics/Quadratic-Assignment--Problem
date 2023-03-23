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
![QAP_11](https://user-images.githubusercontent.com/25113662/227270137-2084422d-a0c1-4f51-b893-e3a59de7240d.png)

Se pretende mostrar como tenemos el problema de asignar 4 entidades como por ejemplo unas oficinas, en 4 localidades diferentes. El gráfico muestra una posible solución asignando la oficina 1 en la ciudad 2, la oficina 2 en la localidad 1, la oficina 3 en la ciudad 4 y por última la oficina 4 en la localidad 3.
La manera más común de plantear el problema de forma combinatoria matemáticamente es de la siguiente manera:
```math
{\Huge \sum_{i=1}^{n} {\sum_{j=1}^{n} { f_{ij} d_{p(i) p(j)} }} }
```
Donde $f$ y $d$ son las matrices de flujos y distancias de tamaño $nxn$ cuyos índices $i$, $j$ en la matriz de flujos representan el flujo entre las entidades de $i$ a $j$ y a su vez los mismos índices $i$, $j$ para la matriz de distancias representan las distancias entre las localidades $i$ y $j$. El vector $p$ es una permutación de números {1,2,…,n} siendo $p(j)$ la localización donde la entidad $j$ es asignada.

### Representación de la solución
La solución es la permutación $p$ en $S_n$ que permita la minimización de la doble sumatoria.
![QAP_12](https://user-images.githubusercontent.com/25113662/227285012-5d85d778-2253-40f1-acb0-87b9f515fd2a.png)


### Solución Inicial
Parte de la eficacia del algoritmo de debe a que la solución inicial sea factible y buena, para ello se realiza lo siguiente:
* Para la primera celda de una matriz se genera un número aleatorio.
* A partir de ese número se calcula el sitio cuyo producto (flujo * distancia) sea el mínimo y se coloca en la siguiente celda.
* Con base en los números que ya están colocados, se busca el sitio que tenga el mínimo producto y se coloca en la siguiente celda, si es una instalación que ya fue ubicada, se busca el siguiente de menor producto (flujo * distancia). Se sigue este proceso hasta la celda $n-1$.
* La última celda lleva el número que falle en el arreglo.
```
def solini(n):
    p = [i for i in range(0,n)]
    random.shuffle(p)
    return p.copy()
```
### Solución Vecina
```
def vecino(p):
    idx = range(len(p))
    i1, i2 = random.sample(idx, 2)
    p[i1], p[i2] = p[i2], p[i1]
    return p
```
![QAP_13](https://user-images.githubusercontent.com/25113662/227287513-9c4b0950-b707-4e5a-bcd2-5514bb128ae4.PNG)

### Función de costo
```
#Costo para 2 matrices
def costo(A,B,p,n):
    z=0
    #doble sumatoria
    for i in range(n):
        for j in range(n):        
            z += A[i][j]*B[p[i]][p[j]]
    return z
``` 
```
#Costo para matrices simetricas (matriz unica)
def costo(A,p,n):
    z=0
    #doble sumatoria
    for i in range(n):
        for j in range(n):        
            if(i>j):
                z += A[j][i]*A[p[i]][p[j]]
            elif(i<j):
                z += A[i][j]*A[p[j]][p[i]]
    return z
``` 
### Instancias a ejecutar

| Instancia    | _n_ | Costo | Solución |
| :---:        |:---:|  :---: |  :---: |
| chr12.csv   | 12| 9742     | (5,7,1,10,11,3,4,2,9,6,12,8) |
| tai100.csv  |100| 21052466 | (...) |
| tai256.csv  |256| 44759294 | (...) |

### Leer CSV
```
import csv
import numpy

#Read CSV to Matrix A
CSVData= open("chr12a.csv")
tabla_A = np.loadtxt(CSVData, delimiter=",")

#Read CSV to Matrix A
CSVData= open("chr12b.csv")
tabla_B = np.loadtxt(CSVData, delimiter=",")

n=len(tabla_A) #matrix length
#visualization
print(n,"\nA:",tabla_A,"\nB:",tabla_B)
``` 

