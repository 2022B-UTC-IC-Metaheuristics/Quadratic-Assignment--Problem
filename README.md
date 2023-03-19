# Quadratic-Assignment-Problem


## Definición del problema
Planteado por Koopmans y Beckmann en 1957, el problema de asignación cuadrática (QAP) es un problema clásico de optimización combinatoria de alta complejidad que pertenece a la clase de los problemas NP-completos, el cual **trata de asignar _n_ instalaciones a una misma cantidad _n_ de localizaciones con un coste asociado a cada una de ellas. Este coste depende de las distancias y flujos entre las instalaciones**, además de que puede existir un coste adicional por instalar cierta facilidad en cierta localización específica. El objetivo es buscar aquella combinación que minimice el coste total.

![QAP_1](https://user-images.githubusercontent.com/25113662/226206123-901ea03f-bc6b-4e68-b4aa-81cfd6aa2dd6.PNG)

Como cualquier problema de combinatoria, el QAP puede resolverse mediante métodos exactos o aproximados. El método exacto más eficiente que ha logrado resolver el QAP ha sido el Branch & Bound para el tamaño de la instancia de orden 30. Otros métodos exactos que se suelen implementar para resolver problemas de este tipo son el método de planos de corte, la programación dinámica e incluso se han propuesto métodos de relajación de la función objetivo para linealizarla que consisten en transformar el problema haciendo cambios de variables de tal manera que se elimine el término cuadrático de la función objetivo. Lamentablemente estos métodos exactos son incapaces de resolver este problema debido a la necesidad de ofrecer respuestas en tiempos razonables y por ese motivo se han implementado metaheurísticas que evitan la enumeración total y mediante estrategias bien definidas efectúan búsquedas parciales en el espacio de soluciones.
De momento algunas de las metaheurísticas más eficientes que se han usado para resolver el QAP son la búsqueda Tabú, los Algoritmos Genéticos, la Búsqueda Dispersa o Scatter Search, GRASP, el Recocido Simulado, Colonia de Hormigas y su combinación entre ellos para formar los Algoritmos Híbridos.

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
[Dickey y Hopkins] En un campus universitario se deben construir viviendas en determinadas parcelas de terreno, el problema a resolver consiste en encontrar una asignación de los sitios a las viviendas de manera de minimizar la distancia total que deben recorrer los alumnos y el personal. 
### Especificación
Matemáticamente se formula de la siguiente manera:
Sean A = (a_ij ), B = (b_kl) ∈ IRn×n , donde 
* _n_ indica el número de viviendas que deben construirse. 
* _a_ij_ la distancia entre el sitio i y el sitio j sobre el campus donde deben construirse las viviendas. 
* _b_kl_ describe la frecuencia con la que los estudiantes y el personal camina entre las viviendas _k_ y _l_. 
El producto _a_ik b_π(i)π(k)_ describe la distancia que se debe caminar entre las viviendas _j = π(i)_ y _l = π(k)_, si la vivienda _j_ está construida sobre el sitio _i_ y la vivienda _l_ sobre el sitio _k_.
### Modelo
![funcionObjetivo2](https://user-images.githubusercontent.com/25113662/161483152-351a8022-d141-464c-950a-7e252d95d6a0.PNG)

### Representación de la solución
La solución es la permutación _p_ en _S_n_ que permita la minimización de la doble sumatoria.
![visualización](https://user-images.githubusercontent.com/25113662/163540014-8d057c0d-47d4-43ac-a31a-1eb74c355dd7.PNG)


### Generación de una solución vecina
Parte de la eficacia del algoritmo de debe a que la solución inicial sea factible y buena, para ello se realiza lo siguiente:
* Para la primera celda de una matriz se genera un número aleatorio.
* A partir de ese número se calcula el sitio cuyo producto (flujo * distancia) sea el mínimo y se coloca en la siguiente celda.
* Con base en los números que ya están colocados, se busca el sitio que tenga el mínimo producto y se coloca en la siguiente celda, si es una instalación que ya fue ubicada, se busca el siguiente de menor producto (flujo * distancia). Se sigue este proceso hasta la celda n-1.
* La última celda lleva el número que falle en el arreglo.
```
def GenerarVecino(p):
    #Se reordena la permutación p aleatoriamente
    l=random.shuffle(p)
    return l 
```
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
1. -
2. -
3. -

### Leer CSV
![ReadCSV](https://user-images.githubusercontent.com/25113662/165063962-5cf41743-cfdd-4d26-857c-9b246a229eca.PNG)
