###  Actividad 03: Representación y Evaluación de Polinomios con Listas Enlazadas
#### Objetivo:
##### Desarrollar un programa que permita representar polinomios mediante una lista enlazada
##### simple y calcular sus valores para distintos puntos de evaluació

``` java
/*
 *@autor Marisol Rincón Solís
 *20 de octubre de 2025
 *Ejercicio Practico Listas
 * Programa simple que permite ingresar un polinomio como lista enlazada,
 * evaluarlo desde x = 0.0 hasta x = 5.0 (en incrementos de 0.5)
 * y mostrar una tabla de valores.
 */
package EjerciciosPracticosListas;

import java.util.Scanner;

public class P3Polinomios {

    // Clase interna Nodo: representa un término del polinomio
    static class Nodo {
        private double coeficiente; // Coeficiente del término
        private int exponente;      // Exponente del término
        private Nodo siguiente;     // Siguiente nodo en la lista

        public Nodo(double coeficiente, int exponente) {
            this.coeficiente = coeficiente;
            this.exponente = exponente;
            this.siguiente = null;
        }

        // Getters y setters
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

    // Atributo que apunta al primer nodo del polinomio
    private Nodo cabeza;

    // Constructor: inicializa el polinomio vacío
    public P3Polinomios() {
        cabeza = null;
    }

    // Inserta un nuevo término al final del polinomio
    public void insertarTermino(double coef, int expo) {
        Nodo nuevo = new Nodo(coef, expo);
        if (cabeza == null) {
            cabeza = nuevo;
        } else {
            Nodo actual = cabeza;
            while (actual.getSiguiente() != null) {
                actual = actual.getSiguiente();
            }
            actual.setSiguiente(nuevo);
        }
    }

    // Evalúa el polinomio en un valor x dado: P(x)
    public double evaluar(double x) {
        double suma = 0.0;
        Nodo actual = cabeza;
        while (actual != null) {
            suma += actual.getCoeficiente() * Math.pow(x, actual.getExponente());
            actual = actual.getSiguiente();
        }
        return suma;
    }

    // Muestra una tabla de valores para x = 0.0 hasta x = 5.0 con incrementos de 0.5
    public void mostrarTabla() {
        System.out.println(" x  |  P(x)");
        System.out.println("--------------");
        for (double x = 0.0; x <= 5.0 + 1e-6; x += 0.5) {
            double px = evaluar(x);
            System.out.printf("%3.1f | %.4f%n", x, px);
        }
    }

    // Método principal: ejecución del programa
    public static void main(String[] args) {
        P3Polinomios pol = new P3Polinomios();
        Scanner teclado = new Scanner(System.in);

        System.out.println("Ingresa los términos del polinomio:");
        System.out.println("(coeficiente exponente). Usa exponente negativo para terminar.");

        // Entrada de datos del usuario
        while (true) {
            System.out.print("Coeficiente: ");
            double c = teclado.nextDouble();
            System.out.print("Exponente: ");
            int e = teclado.nextInt();
            if (e < 0) {
                break; // Condición de parada
            }
            pol.insertarTermino(c, e); // Inserta cada término
        }

        // Mostrar tabla de valores evaluando el polinomio
        System.out.println("\nTabla de valores:");
        pol.mostrarTabla();
    }
}
```
