# Ejercicios Prácticos 
## Tema: Listas
### Marisol Rincón Solís

### Actividad 01: Manipulación de Lista Enlazada
#### Objetivo:
##### Desarrollar un programa que implemente operaciones básicas sobre una lista enlazada
##### simple de números enteros positivos.
``` java

package EjerciciosPracticosListas;
import java.util.Random;
import java.util.Scanner;

/**
 * @author Marisol Rincón Solís
 * Fecha: 20 de Octubre de 2025
 * Tema:Listas.
 * Ejercicios Prácticos
 * Programa para manipular una lista enlazada simple de números enteros positivos.
 * Realiza inserciones al final, muestra los elementos y elimina nodos mayores a un valor dado.
 */
public class P1ManipulaciónListasEnlazadas {

    // Clase interna Nodo (representa cada elemento de la lista)
    static class Nodo {
        private int dato;             // Valor almacenado
        private Nodo siguiente;      // Referencia al siguiente nodo

        public Nodo(int d) {
            this.dato = d;
            this.siguiente = null;
        }

        // Métodos de acceso (getters y setters)
        public int getDato() {
            return dato;
        }

        public void setDato(int dato) {
            this.dato = dato;
        }

        public Nodo getSiguiente() {
            return siguiente;
        }

        public void setSiguiente(Nodo siguiente) {
            this.siguiente = siguiente;
        }
    }

    private Nodo cabeza;  // Referencia al primer nodo de la lista

    // Constructor: inicializa la lista vacía
    public P1ManipulaciónListasEnlazadas() {
        cabeza = null;
    }

    // Inserta un nuevo nodo al final de la lista
    public void insertarFinal(int valor) {
        Nodo nuevo = new Nodo(valor);
        if (cabeza == null) {
            cabeza = nuevo;  // Si la lista está vacía, el nuevo nodo es la cabeza
        } else {
            Nodo actual = cabeza;
            // Avanzar hasta el último nodo
            while (actual.getSiguiente() != null) {
                actual = actual.getSiguiente();
            }
            // Conectar el nuevo nodo al final
            actual.setSiguiente(nuevo);
        }
    }

    // Recorre la lista y muestra los elementos
    public void mostrar() {
        Nodo actual = cabeza;
        System.out.println("Contenido de la lista:");
        // Avanzar por cada nodo hasta llegar al final (null)
        while (actual != null) {
            System.out.print(actual.getDato() + " ");
            actual = actual.getSiguiente();
        }
        System.out.println();
    }

    // Elimina los nodos cuyo dato sea mayor al valor límite dado
    public void eliminarMayores(int limite) {
        // Eliminar nodos al inicio que sean mayores al límite
        while (cabeza != null && cabeza.getDato() > limite) {
            cabeza = cabeza.getSiguiente();
        }

        Nodo actual = cabeza;
        // Recorre la lista y elimina nodos intermedios o finales que cumplan la condición
        while (actual != null && actual.getSiguiente() != null) {
            if (actual.getSiguiente().getDato() > limite) {
                // Saltar el nodo que se va a eliminar
                actual.setSiguiente(actual.getSiguiente().getSiguiente());
            } else {
                actual = actual.getSiguiente();
            }
        }
    }

    // Método principal (main): ejecución del programa
    public static void main(String[] args) {
        P1ManipulaciónListasEnlazadas lista = new P1ManipulaciónListasEnlazadas();
        Random rnd = new Random();
        Scanner sc = new Scanner(System.in);

        // Genera 10 números aleatorios entre 1 y 100, e insértalos en la lista
        for (int i = 0; i < 10; i++) {
            int valor = 1 + rnd.nextInt(100);  // Valor entre 1 y 100
            lista.insertarFinal(valor);
        }

        // Muestra la lista original
        lista.mostrar();

        // Pide al usuario un valor límite
        System.out.print("Ingresa el valor límite (eliminar > límite): ");
        int limite = sc.nextInt();

        // Elimina nodos cuyo valor sea mayor al límite
        lista.eliminarMayores(limite);

        // Muestra la lista actualizada
        lista.mostrar();
    }
}
```
