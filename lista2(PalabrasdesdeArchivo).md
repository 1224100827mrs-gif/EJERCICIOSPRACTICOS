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
