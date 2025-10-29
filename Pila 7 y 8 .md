# Ejercicio Practico 7 

```java
package Pila.Practicos;
import java.util.Scanner;
import java.util.Stack;
/**
 *
 * @author Marisol Rincón Solís
 * Nombre del ejercicio: Simular función Deshacer (Undo)
 *Objetivo: Implementar acciones y deshacer la última con una pila.
 * 28 de Octubre de 2025
 */



public class Ejercicio7 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Stack<String> acciones = new Stack<>();

        while (true) {
            System.out.print("Acción (UNDO/FIN): ");
            String act = sc.nextLine();

            if (act.equalsIgnoreCase("FIN")) break;

            // Si se ingresa "UNDO", eliminar la última acción
            if (act.equalsIgnoreCase("UNDO")) {
                if (!acciones.isEmpty()) {
                    acciones.pop();
                } else {
                    System.out.println("Nada que deshacer.");
                }
            } else {
                acciones.push(act);
            }

            // Mostrar estado actual de la pila
            System.out.println("Acciones actuales: " + acciones);
        }
    }
}
```

# Ejercicio 8 
```java
package Pila.Practicos;

import java.util.Stack;

/**
 *
 * @author Marisol Rincón Solís
 * Nombre del ejercicio:Evaluar expresión postfija
 *Objetivo: Evaluar notación polaca inversa con una pila.
 */
public class Ejercicio8 {
    
    public static int evaluar(String expr) {
        Stack<Integer> pila = new Stack<>();

        for (String token : expr.split(" ")) {
            if (token.matches("\\d+")) {
                pila.push(Integer.parseInt(token)); // Apilar número
            } else {
                // Desapilar los dos últimos operandos
                int b = pila.pop();
                int a = pila.pop();

                // Aplicar operación
                switch (token) {
                    case "+": pila.push(a + b); break;
                    case "-": pila.push(a - b); break;
                    case "*": pila.push(a * b); break;
                    case "/": pila.push(a / b); break;
                }
            }
        }
        return pila.pop(); // Resultado final
    }

    public static void main(String[] args) {
        System.out.println("Resultado: " + evaluar("5 3 + 8 2 - *"));
    }
}
```
