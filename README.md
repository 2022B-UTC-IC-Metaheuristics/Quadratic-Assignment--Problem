# Quadratic-Assignment--Problem

## Definición del problema
El problema de asignación cuadrática (QAP) es un problema clásico de optimización combinatoria de alta complejidad que pertenece a la clase de los problemas NP-hard. El objetivo es encontrar la asignación de actividades a localidades que minimice la suma de los productos entre flujos y distancias.

![img1](https://user-images.githubusercontent.com/25113662/160808642-f8d2d374-34d4-441b-b693-f810e3bc68f0.PNG)

* Matriz de distancias: D={dij}, dij representa la distancia entre la localidad i y la localidad j.

* Matriz de flujos: F={fkl}, fkl representa el flujo entre la actividad k y la actividad l.

Ambas matrices de tamaño nxn.
Teniendo en cuenta las matrices F y D, el QAP consiste en la búsqueda de una permutación p∈Π de n elementos que minimice la función objetivo.

## Aplicaciones
El QAP inicialmente fue planteada como una técnica enfocada a la econimía, sin embargo, sus aplicaciones han empezado a ser cubrir  otros campos muy variados. Algunas aplicaciones son:
* Logística e infraestructuras aeroportuarias
* Diseño de componentes electrónicos
* Planificación y diseño de:
  * Centros comerciales 
  * Campus universitario
  * Hospitales
* Problemas de flujo en línea generalizado
## Ejemplo
Suponemos que existen _n_ sitios disponibles y _n_ instalaciones por edificar. Sea _dkl_ la distancia entre dos sitios _k_ y _l_ donde se cosntruirán las nuevas intalaciones. Además, _fij_ es el flujo semanal de personas que se transladarpian entre las construcciones _i_ y _j_. Cada asignación puede ser escrita como una permutación _p_ del conjunto _N={1,2,...,n}_, tal que _p(i)=k_ significa que la instalación _i_ es asignada al sitio _k_. El producto _fij * d p(i) p(j)_ describe la distancia caminada semnalmente entre las instalaciones _i_ y _j_. Por lo tanto, el problema será minimizar la distancia total recorrida semanlmente y se reduce a encontrar una _p_ que minimice la función _z_.
## Modelo

## Representación de la solución
![representación](https://user-images.githubusercontent.com/25113662/160997841-78cd06e4-3dcc-4761-ab51-d8399ceaf7ad.PNG)

## Generación de una solución vecina
Parte de la eficacia del algoritmo de debe a que la solución inicial sea factible y buena, para ello se realiza lo siguiente:
* Para la primera celda de una matriz se genera un número aleatorio.
* A partir de ese número se calcula el sitio cuyo producto (flujo * distancia) sea el mínimo y se coloca en la siguiente celda.
* Con base en los números que ya están colocados, se busca el sitio que tenga el mínimo producto y se coloca en la siguiente celda, si es una instalación que ya fue ubicada, se busca el siguiente de menor producto (flujo * distancia). Se sigue este proceso hasta la celda n-1.
* La última celda lleva el número que falle en el arreglo.

## Función de costo
## Función objetivo
![funcionObjetivo](https://user-images.githubusercontent.com/25113662/160996333-e245e1e6-19fb-4702-abe4-eb5719f9c414.PNG)
## Instancias a ejecutar
