## Ejercicio 1 Pilas
### Objetivo: Practicar las operaciones básicas push y pop en una pila.
### Pseudocódigo:
### Algoritmo:
### 1. Crear una pila vacía
### 2. Insertar 5, 10, 15, 20
### 3. Eliminar dos elementos
### 4. Mostrar contenido

```java
package Pila.Practicos;

/*
*@author: Marisol Rincón Solís
*Ejercicio1.java
*Simulación simple de pila con operaciones push y pop
* Fecha: 28/10/2025
*GTID141
*/
import java.util.Stack;

public class Ejercicio1 {
    public static void main(String[] args) {
        // Crear una pila vacía de enteros
        Stack<Integer> pila = new Stack<>();

        // Insertar elementos en la pila
        pila.push(5);
        pila.push(10);
        pila.push(15);
        pila.push(20);

        // Eliminar los dos últimos elementos
        pila.pop();
        pila.pop();

        // Mostrar el contenido actual de la pila
        System.out.println("Contenido actual: " + pila);
    }
}

```
