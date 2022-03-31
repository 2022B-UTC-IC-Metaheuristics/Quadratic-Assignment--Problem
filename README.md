# Quadratic-Assignment--Problem

## Definición del problema
El problema de asignación cuadrática (QAP) es un problema clásico de optimización combinatoria de alta complejidad que pertenece a la clase de los problemas NP-hard. El objetivo es encontrar la asignación de actividades a localidades que minimice la suma de los productos entre flujos y distancias.

![img1](https://user-images.githubusercontent.com/25113662/160808642-f8d2d374-34d4-441b-b693-f810e3bc68f0.PNG)

* Matriz de distancias: D={dij}, dij representa la distancia entre la localidad i y la localidad j.

* Matriz de flujos: F={fkl}, fkl representa el flujo entre la actividad k y la actividad l.

Ambas matrices de tamaño nxn.
Teniendo en cuenta las matrices F y D, el QAP consiste en la búsqueda de una permutación p∈Π de n elementos que minimice la función objetivo:

![img2](https://user-images.githubusercontent.com/25113662/160813146-a14dfbc5-9ada-46cb-85dd-1e11032fc162.PNG)


--

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
Suponemos que existen _n_ sitios disponibles y _n_ instalaciones por edificar. Sea _dkl_ la distancia entre dos sitios _k_ y _l_ donde se cosntruirán las nuevas intalaciones. Además, _fij_ es el flujo semanal de personas que se transladarpian entre las construcciones _i_ y _j_. Cada asignación puede ser escrita como una permutación _p_ del conjunto _N={1,2,...,n}_, tal que _p(i)=k_ significa que la instalación _i_ es asignada al sitio _k_. El producto
## Modelo
## Especificación
## Representación de la solución
## Generación de una solución vecina
## Función de costo
## Instancias a ejecutar
