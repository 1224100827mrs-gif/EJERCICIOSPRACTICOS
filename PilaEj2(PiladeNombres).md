# Ejercicio Práctico 2
## Marisol Rincón Solís
### 2. Pila de nombres
### Objetivo: Permitir al usuario ingresar nombres y mostrarlos en orden inverso.
### Pseudocódigo:
### Algoritmo:
### 1. Leer nombres hasta escribir 'FIN'
### 2. Apilar cada nombre
### 3. Desapilar e imprimir en orden inverso

``` java

import java.util.Scanner;
import java.util.Stack;

/**
 * @author Marisol Rincón Solís
 * Ejercicio Practico 2
 * 28 de Octubre de 2025
 * Objetivo: Permitir al usuario ingresar nombres y mostrarlos en orden inverso.
 */


import java.util.Scanner;
import java.util.Stack;

public class Ejercicio2 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Stack<String> pila = new Stack<>();
        String nombre;

        // Leer nombres hasta que el usuario escriba "FIN"
        while (true) {
            System.out.print("Ingrese un nombre (FIN para salir): ");
            nombre = sc.nextLine();
            if (nombre.equalsIgnoreCase("FIN")) break;
            pila.push(nombre); // Apilar el nombre
        }

        // Mostrar los nombres en orden inverso
        System.out.println("Nombres en orden inverso:");
        while (!pila.isEmpty()) {
            System.out.println(pila.pop());
        }
    }
}


```
