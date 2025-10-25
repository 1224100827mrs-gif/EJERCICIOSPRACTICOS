### Actividad 05: Lista Doblemente Enlazada de Caracteres
#### Objetivo:
##### Desarrollar un programa que construya una lista doblemente enlazada a partir de los
##### caracteres de una cadena ingresada por el usuario, y que luego ordene dicha lista
##### alfabéticamente para mostrarla en pantalla

``` java
/* 
 *@author Marisol Rincón Solís
 *21 de octubre de 2025
 * Programa de lista doblemente enlazada y a partir de una cadena ingresada por el usuario y luego
 * ordena alfabeticamente los caracteres para mostrarlos
 */

package EjerciciosPracticosListas;

import java.util.Scanner;

public class P5ListaDobleCaracteres {

    // Clase Nodo con encapsulamiento
    private static class Nodo {
        private char dato;
        private Nodo anterior;
        private Nodo siguiente;

        public Nodo(char dato) {
            this.dato = dato;
            this.anterior = null;
            this.siguiente = null;
        }

        // Getters y setters
        public char getDato() {
            return dato;
        }

        public void setDato(char dato) {
            this.dato = dato;
        }

        public Nodo getAnterior() {
            return anterior;
        }

        public void setAnterior(Nodo anterior) {
            this.anterior = anterior;
        }

        public Nodo getSiguiente() {
            return siguiente;
        }

        public void setSiguiente(Nodo siguiente) {
            this.siguiente = siguiente;
        }
    }

    // Punteros a los extremos de la lista
    private Nodo cabeza;
    private Nodo cola;

    // Constructor
    public P5ListaDobleCaracteres() {
        cabeza = null;
        cola = null;
    }

    /**
     * Construye la lista doblemente enlazada a partir de una cadena
     */
    public void construirDesdeCadena(String texto) {
        for (char c : texto.toCharArray()) {
            Nodo nuevo = new Nodo(c);
            if (cabeza == null) {
                cabeza = nuevo;
                cola = nuevo;
            } else {
                cola.setSiguiente(nuevo);
                nuevo.setAnterior(cola);
                cola = nuevo;
            }
        }
    }

    /**
     * Ordena alfabéticamente los caracteres de la lista usando burbuja
     */
    public void ordenarAlfabeticamente() {
        if (cabeza == null) return;

        boolean cambiado;
        do {
            cambiado = false;
            Nodo actual = cabeza;
            while (actual.getSiguiente() != null) {
                if (actual.getDato() > actual.getSiguiente().getDato()) {
                    // Intercambiar datos
                    char temp = actual.getDato();
                    actual.setDato(actual.getSiguiente().getDato());
                    actual.getSiguiente().setDato(temp);
                    cambiado = true;
                }
                actual = actual.getSiguiente();
            }
        } while (cambiado);
    }

    /**
     * Muestra los caracteres de la lista ordenada
     */
    public void mostrarOrdenada() {
        System.out.print("Caracteres ordenados: ");
        Nodo actual = cabeza;
        while (actual != null) {
            System.out.print(actual.getDato());
            actual = actual.getSiguiente();
        }
        System.out.println();
    }

    // Método principal
    public static void main(String[] args) {
        P5ListaDobleCaracteres lista = new P5ListaDobleCaracteres();
        Scanner tecla = new Scanner(System.in);

        System.out.print("Ingresa una cadena de texto: ");
        String texto = tecla.nextLine();

        lista.construirDesdeCadena(texto);
        lista.ordenarAlfabeticamente();
        lista.mostrarOrdenada();

        
    }
}
```
