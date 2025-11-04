
#  Ejercicio 2: Simulación de supermercado con carritos y cajas
## Marisol Rincón Solís
### GTID141


```java
package Cola.EjerciciosPracticos.Eje2;

import java.util.LinkedList;
import java.util.Queue;

/**
 * Clase que representa una caja de pago en el supermercado
 * @author DELL
 */
public class Caja {
    /** Identificador de la caja */
    private int id;
    /** Cola de clientes esperando en esta caja */
    private Queue<Cliente> colaClientes = new LinkedList<>();

    /**
     * Constructor de la caja con su id
     * @param id identificador de la caja
     */
    public Caja(int id) {
        this.id = id;
    }

    /**
     * Agrega un cliente a la cola
     * @param c cliente a agregar
     */
    public void agregarCliente(Cliente c) {
        colaClientes.add(c);
    }

    /**
     * Atiende al siguiente cliente en la cola
     * @return cliente atendido o null si la cola está vacía
     */
    public Cliente atender() {
        return colaClientes.poll();
    }

    /** @return número de clientes en la cola */
    public int cantidadClientes() {
        return colaClientes.size();
    }

    /** @return id de la caja */
    public int getId() {
        return id;
    }
}


```

``` java

package Cola.EjerciciosPracticos.Eje2;
/**
 * Clase que representa un cliente del supermercado
 * @author Marisol Rincón Solis
 */
public class Cliente {
    /** Identificador del cliente */
    private int id;

    /**
     * Constructor que crea un cliente con un identificador único
     * @param id identificador del cliente
     */
    public Cliente(int id) {
        this.id = id;
    }

    @Override
    public String toString() {
        return "Cliente-" + id;
    }
}

```

``` java
package Cola.EjerciciosPracticos.Eje2;

import java.util.ArrayList;
import java.util.List;

/**
 * Simulación de supermercado con carritos y cajas
 * Los clientes se asignan a la caja con menos clientes y luego son atendidos en orden
 * @author Marisol Rincón Solis
 */
public class Supermercado {
    /** Arreglo de clientes con carritos disponibles */
    private Cliente[] filaCarritos;
    /** Arreglo de cajas disponibles */
    private Caja[] cajas;

    /**
     * Constructor de la simulación
     * @param totalClientes número total de clientes
     * @param totalCajas número de cajas
     * @param totalCarritos número de carritos disponibles
     */
    public Supermercado(int totalClientes, int totalCajas, int totalCarritos) {
        filaCarritos = new Cliente[totalCarritos];
        for (int i = 0; i < totalCarritos; i++) {
            filaCarritos[i] = new Cliente(i + 1);
        }

        cajas = new Caja[totalCajas];
        for (int i = 0; i < totalCajas; i++) {
            cajas[i] = new Caja(i + 1);
        }
    }

    /**
     * Ejecuta la simulación
     */
    public void ejecutar() {
        System.out.println("=== SIMULACIÓN SUPERMERCADO ===");

        int indexCliente = 0;
        while (indexCliente < filaCarritos.length) {
            Cliente cliente = filaCarritos[indexCliente++];

            // Selecciona la caja con menos clientes
            Caja cajaSeleccionada = cajas[0];
            for (Caja c : cajas) {
                if (c.cantidadClientes() < cajaSeleccionada.cantidadClientes()) {
                    cajaSeleccionada = c;
                }
            }

            // Cliente se coloca en la caja
            cajaSeleccionada.agregarCliente(cliente);
            System.out.println(cliente + " se va a la caja " + cajaSeleccionada.getId());
        }

        // Atender a los clientes de cada caja
        for (Caja c : cajas) {
            System.out.println("\nAtendiendo clientes de la caja " + c.getId());
            Cliente atendido;
            while ((atendido = c.atender()) != null) {
                System.out.println("Atendido: " + atendido);
            }
        }
    }

    public static void main(String[] args) {
        Supermercado sim = new Supermercado(25, 3, 25);
        sim.ejecutar();
    }
}

```

## Evidencia 
<img width="254" height="537" alt="image" src="https://github.com/user-attachments/assets/0f657874-1a30-4d25-b786-4739abd858d7" />


