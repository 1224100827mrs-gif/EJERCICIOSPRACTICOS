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
### Actividad 02: Lista Enlazada de Palabras desde Archivo
#### Objetivo:
##### Desarrollar un programa que lea palabras desde un archivo de texto y las almacene en una
##### lista enlazada, permitiendo su manipulación dinámica.
``` java
package EjerciciosPracticosListas;
import java.io.*;
import java.util.Scanner;
/**
 *@author Marisol
 * 20 de Octubre de 2025
 * Tema: Listas 
 * Ejercicios Prácticos
 * lee palabras desde un archivo de texto,las guarda en una lista enlazada, permite agregar o 
 * eliminar palabras y luego guarda los cambios de nuevo en el archivo.
 */
public class P2PalabrasdesdeArchivo {
     // Clase interna Nodo: representa un nodo de la lista enlazada
    static class Nodo {
        private String palabra;   // Palabra almacenada en el nodo
        private Nodo siguiente;   // Referencia al siguiente nodo

        public Nodo(String p) {
            this.palabra = p;
            this.siguiente = null;
        }

        // Getters y setters (encapsulación)
        public String getPalabra() {
            return palabra;
        }

        public void setPalabra(String palabra) {
            this.palabra = palabra;
        }

        public Nodo getSiguiente() {
            return siguiente;
        }

        public void setSiguiente(Nodo siguiente) {
            this.siguiente = siguiente;
        }
    }

    // Atributo privado que apunta al primer nodo de la lista
    private Nodo cabeza;

    // Constructor: inicializa la lista vacía
    public P2PalabrasdesdeArchivo() {
        cabeza = null;
    }

    // Inserta una palabra al final de la lista
    public void insertarFinal(String palabra) {
        Nodo nuevo = new Nodo(palabra);
        if (cabeza == null) {
            cabeza = nuevo;
        } else {
            Nodo actual = cabeza;
            // Recorrer hasta el último nodo
            while (actual.getSiguiente() != null) {
                actual = actual.getSiguiente();
            }
            // Conectar el nuevo nodo al final
            actual.setSiguiente(nuevo);
        }
    }

    // Muestra todas las palabras de la lista
    public void mostrar() {
        System.out.println("Lista de palabras:");
        Nodo actual = cabeza;
        while (actual != null) {
            System.out.print(actual.getPalabra() + " ");
            actual = actual.getSiguiente();
        }
        System.out.println(); // Salto de línea final
    }

    // Elimina la primera ocurrencia de una palabra específica
    public void eliminarPalabra(String target) {
        if (cabeza == null) return;

        // Si la cabeza es la que debe eliminarse
        if (cabeza.getPalabra().equals(target)) {
            cabeza = cabeza.getSiguiente();
            return;
        }

        Nodo actual = cabeza;
        // Buscar la palabra en el resto de la lista
        while (actual.getSiguiente() != null) {
            if (actual.getSiguiente().getPalabra().equals(target)) {
                // Saltar el nodo a eliminar
                actual.setSiguiente(actual.getSiguiente().getSiguiente());
                return;
            } else {
                actual = actual.getSiguiente();
            }
        }
    }

    // Escribe todas las palabras de la lista en el archivo (sobrescribe)
    public void escribirArchivo(String nombreArchivo) {
        try (PrintWriter pw = new PrintWriter(new FileWriter(nombreArchivo))) {
            Nodo actual = cabeza;
            while (actual != null) {
                pw.print(actual.getPalabra());
                if (actual.getSiguiente() != null) {
                    pw.print(" "); // Separar palabras con espacios
                }
                actual = actual.getSiguiente();
            }
            System.out.println("Archivo escrito correctamente.");
        } catch (IOException e) {
            System.err.println("Error al escribir el archivo: " + e.getMessage());
        }
    }

    // Método principal: ejecución del programa
    public static void main(String[] args) {
        P2PalabrasdesdeArchivo lista = new P2PalabrasdesdeArchivo();
        String nombreArchivo = "palabras.txt";

        // 1. Lectura del archivo y formación de la lista
        try (Scanner sc = new Scanner(new File(nombreArchivo))) {
            while (sc.hasNext()) {
                String palabra = sc.next();
                lista.insertarFinal(palabra); // Inserta en orden
            }
        } catch (FileNotFoundException e) {
            System.err.println("Archivo no encontrado: " + e.getMessage());
        }

        // Muestra la lista después de leer del archivo
        lista.mostrar();

        // 2. Manipulación dinámica: añadir/eliminar palabras
        try (Scanner sc = new Scanner(System.in)) {
            // Añadir palabra
            System.out.print("¿Quieres añadir una nueva palabra? (sí/no): ");
            String resp = sc.next();
            if (resp.equalsIgnoreCase("sí") || resp.equalsIgnoreCase("si")) {
                System.out.print("Ingresa la palabra a añadir: ");
                String nueva = sc.next();
                lista.insertarFinal(nueva);
            }

            // Eliminar palabra
            System.out.print("¿Quieres eliminar una palabra? (sí/no): ");
            resp = sc.next();
            if (resp.equalsIgnoreCase("sí") || resp.equalsIgnoreCase("si")) {
                System.out.print("Ingresa la palabra a eliminar: ");
                String eliminar = sc.next();
                lista.eliminarPalabra(eliminar);
            }
        }

        // Mostrar lista final después de las modificaciones
        lista.mostrar();

        // 3. Escritura de la lista modificada al archivo
        lista.escribirArchivo(nombreArchivo);
    }
}
```
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
````

