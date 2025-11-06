# Ejercicio Práctico 1 
## Temas Colas 
### Marisol Rincón Solís
## Fecha: 03/11/2025


# 1. Colas.java

Clase que implementa la interfaz OperacionesCola<T> para manejar colas genéricas.  
Funciones principales:

- `encolar(T elemento)`: Agrega un elemento al final de la cola.  
- `desencolar()`: Retira y devuelve el primer elemento de la cola.  
- `estaVacia()`: Verifica si la cola está vacía.  
- `tamaño()`: Retorna el tamaño actual de la cola.  
- `obtenerCola()`: Devuelve la referencia a la cola interna.  
- `toString()`: Representación en texto de la cola.  

# 2. OperacionesCola.java

Interfaz genérica que define las operaciones básicas de una cola:

- `encolar(T elemento)`  
- `desencolar()`  
- `estaVacia()`  
- `tamaño()`  

# 3. ComparacionColas.java

Interfaz que define un método para comparar dos colas:

- `<T> boolean sonIguales(Queue<T> cola1, Queue<T> cola2)`  

# 4. ComparaciondeColas.java

Clase que implementa ComparacionColas.  
Funcionalidad principal:

- Verifica si dos colas contienen los mismos elementos en el mismo orden.  
- Incluye un `main` de prueba demostrando la comparación de dos colas con elementos de tipo `String`.


``` java 
package Cola.EjerciciosPracticos;

import java.util.LinkedList;
import java.util.Queue;

   /**
     * Implementación de una cola genérica usando LinkedList
     * @param <T> tipo de elementos de la cola
     * @author Marisol Ricón Solís 
     */

public class Colas <T> implements OperacionesCola<T> {
    private Queue<T> elementos;
 /** Agrega un elemento al final de la cola */
    public Colas() {
        this.elementos = new LinkedList<>();
    }

    @Override
    public void encolar(T elemento) {
        elementos.add(elemento);
    }
/** Retira y devuelve el primer elemento de la cola */
    @Override
    public T desencolar() {
        return elementos.poll();
    }
     /** @return true si la cola está vacía */
    @Override
    public boolean estaVacia() {
        return elementos.isEmpty();
    }
    /** @return tamaño actual de la cola */
    @Override
    public int tamaño() {
        return elementos.size();
    }

 /** @return referencia a la cola interna (para comparaciones) */
    public Queue<T> obtenerCola() {
        return elementos;
    }
/** Representación en texto de la cola */
    @Override
    public String toString() {
        return elementos.toString();
    }
}
```

``` java
package Cola.EjerciciosPracticos;

import java.util.Queue;

/**
 *
 * @author Marsol Rincón Solís
 */
public interface ComparacionColas {
     <T> boolean sonIguales(Queue<T> cola1, Queue<T> cola2);
}
```
``` java
package Cola.EjerciciosPracticos;

  /**
     * Interfaz genérica para operaciones básicas de una cola
     * @param <T> tipo de elementos de la cola
     * @author Marisol Rincón Solís
     */
public interface OperacionesCola<T> {
     void encolar(T elemento);
    T desencolar();
    boolean estaVacia();
    int tamaño();
}
```

``` Java

package Cola.EjerciciosPracticos;

import java.util.LinkedList;
import java.util.Queue;

/**
 * @author Marisol Rincón Solís
     * Implementación de ComparacionColas que verifica si dos colas son iguales
     */
public class ComparaciondeColas  implements ComparacionColas {
/**
         * Compara dos colas para verificar si son iguales
         * @param <T> tipo de elementos
         * @param cola1 primera cola
         * @param cola2 segunda cola
         * @return true si son idénticas, false en caso contrario
         */
    @Override
    public <T> boolean sonIguales(Queue<T> cola1, Queue<T> cola2) {
        if (cola1.size() != cola2.size()) return false;

        Queue<T> copia1 = new LinkedList<>();
        Queue<T> copia2 = new LinkedList<>();
        boolean iguales = true;

        while (!cola1.isEmpty()) {
            T e1 = cola1.poll();
            T e2 = cola2.poll();
            if (!e1.equals(e2)) {
                iguales = false;
            }
            copia1.add(e1);
            copia2.add(e2);
        }
 // Restaurar las colas originales
        cola1.addAll(copia1);
        cola2.addAll(copia2);

        return iguales;
    }
    
    /** Método principal para ejecutar la prueba */
     public static void main(String[] args) {
        OperacionesCola<String> colaA = new Colas<>();
        OperacionesCola<String> colaB = new Colas<>();

        colaA.encolar("Marisol");
        colaA.encolar("Kira");
        colaA.encolar("Romi");

        colaB.encolar("Marisol");
        colaB.encolar("Kira");
        colaB.encolar("Romi");

        ComparacionColas comparador = new ComparaciondeColas();
        boolean resultado = comparador.sonIguales(
                ((Colas<String>) colaA).obtenerCola(),
                ((Colas<String>) colaB).obtenerCola()
        );

        System.out.println("¿Colas iguales? " + resultado);
    }
}
```

# Evidencia
<img width="597" height="252" alt="image" src="https://github.com/user-attachments/assets/a1dd51ff-90d0-4209-ba79-eac3f46e9e57" />

<img width="1021" height="465" alt="image" src="https://github.com/user-attachments/assets/e6630d1a-e035-40e9-aaaf-d4a4d39d47bb" />


