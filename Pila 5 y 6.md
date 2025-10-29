# Ejercicio Práctico 5
### 5. Balanceo de paréntesis
### Objetivo: Verificar si los paréntesis están correctamente balanceados.
### Pseudocódigo:
### Algoritmo:
### 1. Recorrer expresión
### 2. Apilar '(' y desapilar cuando haya ')'
### 3. Si la pila queda vacía → balanceada
```java
package Pila.Practicos;
/**
 * author Marisol Rincón Solís
 * Ejercicio5:Balanceo de paréntesis
 * Objetivo: Verificar si los paréntesis están correctamente balanceados
 */
import java.util.Stack;

public class Ejercicio5 {
    // Método que evalúa si una expresión está balanceada
    public static boolean estaBalanceada(String expr) {
        Stack<Character> pila = new Stack<>();

        for (char c : expr.toCharArray()) {
            if (c == '(') {
                pila.push(c);
            } else if (c == ')') {
                if (pila.isEmpty()) return false;
                pila.pop();
            }
        }

        return pila.isEmpty(); // Si está vacía, está balanceada
    }

    public static void main(String[] args) {
        System.out.println(estaBalanceada("((2+3)*5)")); // true
        System.out.println(estaBalanceada("((2+3)*5"));  // false
    }
}
```
# Ejercicio Practico 6
### Decimal a binario
### Objetivo: Convertir número decimal a binario usando una pila.
### Pseudocódigo:
### Algoritmo:
### 1. Dividir número por 2 y apilar restos
### 2. Mostrar elementos desde la pila
``` java
package Pila.Practicos;

import java.util.Scanner;
import java.util.Stack;

/**
 * Nombre del ejercicio: Decimal a binario
 * @author Marisol Rincón Solís
 * Objetivo: Convertir número decimal a binario usando una pila.
 */

public class Ejercicio6 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Ingrese número: ");
        int num = sc.nextInt();

        Stack<Integer> pila = new Stack<>();

        // Dividir entre 2 y apilar los restos
        while (num > 0) {
            pila.push(num % 2);
            num /= 2;
        }

        // Mostrar los restos (binario)
        System.out.print("Binario: ");
        while (!pila.isEmpty()) {
            System.out.print(pila.pop());
        }
    }
}
```
