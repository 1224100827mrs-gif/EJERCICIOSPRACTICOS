### Actividad 04: Polinomio con Lista Enlazada Circular
#### Objetivo:
##### Modificar la representación de un polinomio mediante lista enlazada simple para que se
##### convierta en una lista circular, optimizando el acceso y recorrido continuo.
``` java
/*
 * @author Marisol Rincón Solis
 * 21 de Octubre de 2025
 * Ejercicio practico : Listas
 * Programa que representa un polinomio usando una lista enlazada circular.
 * Permite ingresar coeficientes y exponentes, y recorre el polinomio desde
 * el primer término hasta volver al inicio.
 */
package EjerciciosPracticosListas;

import java.util.Scanner;

public class P4PolinomioCircular {

    // Clase interna Nodo con encapsulamient
    private static class Nodo {
        private double coeficiente;
        private int exponente;
        private Nodo siguiente;

        public Nodo(double coeficiente, int exponente) {
            this.coeficiente = coeficiente;
            this.exponente = exponente;
            this.siguiente = null;
        }

        // Getters y Setters
        public double getCoeficiente() {
            return coeficiente;
        }

        public void setCoeficiente(double coeficiente) {
            this.coeficiente = coeficiente;
        }

        public int getExponente() {
            return exponente;
        }

        public void setExponente(int exponente) {
            this.exponente = exponente;
        }

        public Nodo getSiguiente() {
            return siguiente;
        }

        public void setSiguiente(Nodo siguiente) {
            this.siguiente = siguiente;
        }
    }

    // Referencia al último nodo (clave para lista circular)
    private Nodo ultimo;

    // Constructor: lista vacía
    public P4PolinomioCircular() {
        this.ultimo = null;
    }

    /**
     * Inserta un nuevo término al final del polinomio
     * y actualiza los enlaces para mantener la estructura circular.
     */
    public void insertarTermino(double coef, int expo) {
        Nodo nuevo = new Nodo(coef, expo);
        if (ultimo == null) {
            // Primer nodo: se apunta a sí mismo
            nuevo.setSiguiente(nuevo);
            ultimo = nuevo;
        } else {
            nuevo.setSiguiente(ultimo.getSiguiente()); // Apunta al primero
            ultimo.setSiguiente(nuevo); // Último apunta al nuevo
            ultimo = nuevo;             // Nuevo pasa a ser el último
        }
    }

    /**
     * Recorre la lista circular desde el primer nodo
     * y muestra los términos (coeficiente, exponente).
     */
    public void mostrar() {
        if (ultimo == null) {
            System.out.println("Lista vacía.");
            return;
        }

        System.out.println("Polinomio (coeficiente, exponente):");
        Nodo actual = ultimo.getSiguiente(); // Comenzar desde el primero
        do {
            System.out.printf("(%.2f, %d) ", actual.getCoeficiente(), actual.getExponente());
            actual = actual.getSiguiente();
        } while (actual != ultimo.getSiguiente()); // Hasta volver al inicio
        System.out.println();
    }

    public static void main(String[] args) {
        P4PolinomioCircular pol = new P4PolinomioCircular();
        Scanner teclado = new Scanner(System.in);

        System.out.println("Ingresa términos del polinomio (coeficiente exponente).");
        System.out.println("Para terminar, ingresa un exponente negativo.");

        while (true) {
            System.out.print("Coeficiente: ");
            double c = teclado.nextDouble();
            System.out.print("Exponente: ");
            int e = teclado.nextInt();
            if (e < 0) {
                break;
            }
            pol.insertarTermino(c, e);
        }

        System.out.println("\nTérminos del polinomio ingresado:");
        pol.mostrar();

       
    }
}
```
