# Ejercicio práctico 3
### 3. Verificar si una pila está vacía
### Objetivo: Comprobar si la pila tiene elementos.
### Pseudocódigo:
### Algoritmo:
### 1. Crear pila vacía
### 2. Usar método isEmpty()

``` java
package Pila.Practicos;

import java.util.Stack;

/**
 *
 * @author Marisol Rincón Solís
 * Ejercicio Práctico 3
 * 28 de Octubre de 2025
 * Verificar si una pila está vacía
 *Objetivo: Comprobar si la pila tiene elementos
 */


public class Ejercicio3 {
    public static void main(String[] args) {
        Stack<Integer> pila = new Stack<>();

        // Verificar si está vacía
        System.out.println("¿Está vacía la pila? " + pila.isEmpty());

        // Insertar un elemento
        pila.push(1);

        // Verificar nuevamente
        System.out.println("¿Está vacía la pila? " + pila.isEmpty());
    }
}

```
# Ejercicio práctico 4
### Invertir una palabra
### Objetivo: Invertir una palabra usando una pila de caracteres.
### Pseudocódigo:
### Algoritmo:
### 1. Leer palabra
### 2. Apilar cada letra
### 3. Desapilar e imprimir

``` Java
package Pila.Practicos;
/**
 * @author Marisol Rincón Solíds
 * Ejercicios Prácticos
 * Objetivo: Invertir una palabra usando una pila de caracteres.
 * 28/10/2025
 */

import java.util.Stack;
import java.util.Scanner;

public class Ejercicio4 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Ingrese una palabra: ");
        String palabra = sc.nextLine();

        Stack<Character> pila = new Stack<>();

        // Apilar cada carácter de la palabra
        for (char c : palabra.toCharArray()) {
            pila.push(c);
        }

        // Desapilar para mostrar la palabra invertida
        System.out.print("Invertida: ");
        while (!pila.isEmpty()) {
            System.out.print(pila.pop());
        }
    }
}
```
