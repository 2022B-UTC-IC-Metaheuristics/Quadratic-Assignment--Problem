# Quadratic-Assignment--Problem


## Definición del problema
El problema de asignación cuadrática (QAP) es un problema clásico de optimización combinatoria de alta complejidad que pertenece a la clase de los problemas NP-hard. El objetivo es encontrar la asignación de actividades a localidades que minimice la suma de los productos entre flujos y distancias.

Dados el conjunto IN = {1, 2, ..., n} y las matrices A=(aij) y B=(bij)∈ IRnxn, el problema se plantea de la forma:
![descripccion](https://user-images.githubusercontent.com/25113662/161483775-a455ae2a-e130-4c2e-889f-91af1c6ae1d2.PNG)

donde Sn es el conjunto de permutaciones de {1, 2, ..., n}, se debe encontrar una permutación π∈Sn de tal manera que minimice la doble sumatoria. Normalmente se habla de minimización y no de maximización ya que, maximizar _f_ puede obtenerse de minimizar -_f_. Dado que las matrices A y B son simétricas, computacionalmente se pueden representar en una sola matriz _C_ como se muestra a continuación:
![repComp](https://user-images.githubusercontent.com/25113662/163293020-753b193f-0870-42de-87eb-154df1a56dd7.PNG)


### Aplicaciones
El QAP inicialmente fue planteada como una técnica enfocada a la economía, sin embargo, sus aplicaciones han empezado a cubrir  otros campos muy variados. Algunas aplicaciones son:
* Logística e infraestructuras aeroportuarias
* Diseño de componentes electrónicos
* Planificación y diseño de:
  * Centros comerciales 
  * Campus universitario
  * Hospitales
* Problemas de flujo en línea generalizado
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
![representación](https://user-images.githubusercontent.com/25113662/161484529-293f9768-e1c7-4d78-9dad-f86cab6e1244.PNG)

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
def costo(A,B,p,n):
    z=0
    #doble sumatoria
    for i in range(n):
        for j in range(n):        
            z += A[i][j]*B[p[i]][p[j]]
    return z
``` 
### Instancias a ejecutar
1. -
2. -
3. -
