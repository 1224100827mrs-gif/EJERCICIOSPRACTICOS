# Ejercicio 9 
``` java
import java.util.Stack;

/**
 *
 * @author Marisol Rincón Solís
 * 28 de octubre de 2025
 * Ejercicio9: Revertir lista
 *Objetivo: Usar pila para invertir los elementos de una lista.
 *Pseudocódigo:
 *Algoritmo:
 *1. Apilar elementos de la lista
 *2. Desapilar e imprimir
 */


public class Ejercicio9 {
    public static void main(String[] args) {
        int[] lista = {1, 2, 3, 4};
        Stack<Integer> pila = new Stack<>();

        // Apilar los elementos
        for (int n : lista) {
            pila.push(n);
        }

        // Mostrar los elementos en orden inverso
        System.out.print("Lista invertida: ");
        while (!pila.isEmpty()) {
            System.out.print(pila.pop() + " ");
        }
    }
}
```
 # Ejercicio 10 
 ``` java
package Pila.Practicos;

import java.util.Scanner;
import java.util.Stack;

/**
 *
 * @author Marisol Rincón Solís
 * 28 de Octubre de 2025
 * 10. Verificar palíndromo
 *Objetivo: Determinar si una palabra es palíndroma usando pila.
 */
    
public class Ejercicio10 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Ingrese palabra: ");
        String palabra = sc.nextLine();

        Stack<Character> pila = new Stack<>();

        // Apilar los caracteres
        for (char c : palabra.toCharArray()) {
            pila.push(c);
        }

        // Desapilar para formar la palabra invertida
        String invertida = "";
        while (!pila.isEmpty()) {
            invertida += pila.pop();
        }

        // Comparar palabra original e invertida
        if (palabra.equalsIgnoreCase(invertida))
            System.out.println("Es palíndromo");
        else
            System.out.println("No es palíndromo");
    }
}
  

```
