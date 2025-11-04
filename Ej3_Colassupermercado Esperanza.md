# Ejercicio3 
## Tema>:Colas

```java
package Cola.EjerciciosPracticos.Ej3;

/**
 * Interfaz para simuladores de supermercado
 * @author Marisol Rincón Solís
 */
public interface Simulador {
     /** Ejecuta la simulación completa. */
    void ejecutar();

    /** Muestra las resultado  final de la simulación. */
    void mostrarResultados();
}

```

```java
package Cola.EjerciciosPracticos.Ej3;

/**
 *Clase que representa un cliente de supermercado
 * @author Marisol Rincón Solís
 */
public class Cliente {
     /** Identificador único del cliente */
    private int id;

    /** Minuto en el que el cliente llegó al supermercado */
    private int minutoLlegada;

    /** Minuto en el que el cliente empezó a ser atendido */
    private int minutoInicioAtencion;

    /**
     * Crea un cliente con un identificador y el minuto de llegada.
     * @param id identificador del cliente
     * @param minutoLlegada momento en que llegó a la fila
     */
    public Cliente(int id, int minutoLlegada) {
        this.id = id;
        this.minutoLlegada = minutoLlegada;
    }

    /** @return identificador del cliente */
    public int getId() {
        return id;
    }

    /** @return minuto en que llegó el cliente */
    public int getMinutoLlegada() {
        return minutoLlegada;
    }

    /** @return minuto en que empezó a ser atendido */
    public int getMinutoInicioAtencion() {
        return minutoInicioAtencion;
    }

    /**
     * Define el momento en que el cliente comienza a ser atendido.
     * @param minutoInicioAtencion minuto actual de inicio
     */
    public void setMinutoInicioAtencion(int minutoInicioAtencion) {
        this.minutoInicioAtencion = minutoInicioAtencion;
    }
    
    @Override
    public String toString() { return "Cliente-" + id; }
    
}

```

```java
package Cola.EjerciciosPracticos.Ej3;

import java.util.LinkedList;
import java.util.Queue;

/**
 *Clase que representa una caja en el supermercado
 * @author Marisol Rincón Solís
 */
public class Caja  {
    private Cliente atendiendo; // Cliente que está siendo atendido
    private int id;

    public Caja(int id) { this.id = id; }

    public boolean estaLibre() { 
        return atendiendo == null; 
    }
    public void agregarCliente(Cliente c) {
        atendiendo = c; 
    }
    public void atender() {
        atendiendo = null; 
    }
    public int getId() {
        return id; 
    }
    
}

```

```java
package Cola.EjerciciosPracticos.Ej3;

import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;
import java.util.Random;

/**
 *Simulación de atención al cliente con fila única y hasta 4 cajas
 * Genera estadísticas de clientes atendidos, tiempo de espera y apertura de cuarta caja
 * @author Marisol Rincón Solís
 */
public class SimuladorEsperanza  implements Simulador{
 
    private Queue<Cliente> filaClientes = new LinkedList<>();
    private List<Caja> cajas = new ArrayList<>();
    private int clientesAtendidos, tiempoMaximoEspera, sumaTiemposEspera, clientesConEspera;
    private int tamanoMaximoFila;
    private int tiempoSimulacion, frecuenciaLlegadas, umbralApertura;
    private Integer minutoAperturaCuartaCaja = null;

    // Constructor con parámetros de simulación
    public SimuladorEsperanza(int tiempoSimulacion, int frecuenciaLlegadas, int umbralApertura) {
        this.tiempoSimulacion = tiempoSimulacion;
        this.frecuenciaLlegadas = frecuenciaLlegadas;
        this.umbralApertura = umbralApertura;

        // Inicializamos con 3 cajas activas
        for (int i = 1; i <= 3; i++) cajas.add(new Caja(i));
    }

    @Override
    public void ejecutar() {
        System.out.println("=== INICIO SIMULACION ESPERANZA ===");

        for (int minuto = 0; minuto < tiempoSimulacion; minuto++) {

            // Llegada de clientes cada frecuenciaLlegadas minutos
            if (minuto % frecuenciaLlegadas == 0) {
                Cliente c = new Cliente(minuto + 1, minuto);
                filaClientes.add(c);
                tamanoMaximoFila = Math.max(tamanoMaximoFila, filaClientes.size());
            }

            // Atención de clientes en cada caja disponible
            for (Caja caja : cajas) {
                if (caja.estaLibre() && !filaClientes.isEmpty()) {
                    Cliente siguiente = filaClientes.poll();
                    siguiente.setMinutoInicioAtencion(minuto);

                    int espera = siguiente.getMinutoInicioAtencion() - siguiente.getMinutoLlegada();
                    tiempoMaximoEspera = Math.max(tiempoMaximoEspera, espera);
                    sumaTiemposEspera += espera;
                    clientesConEspera++;

                    caja.agregarCliente(siguiente);
                    clientesAtendidos++;
                }
            }

            // Verificamos si necesitamos abrir la cuarta caja
            int promedioFila = filaClientes.size() / Math.max(1, cajas.size());
            if (promedioFila > umbralApertura && cajas.size() == 3) {
                cajas.add(new Caja(4));
                minutoAperturaCuartaCaja = minuto;
                System.out.println("Se abre cuarta caja en minuto " + minuto);
            }
        }

        mostrarResultados();
    }

    @Override
    public void mostrarResultados() {
        System.out.println("\n=== RESULTADOS SIMULACION ===");
        System.out.println("Clientes atendidos: " + clientesAtendidos);
        System.out.println("Tamaño máximo de fila: " + tamanoMaximoFila);
        System.out.println("Tiempo máximo de espera: " + tiempoMaximoEspera + " min");
        System.out.printf("Tiempo promedio de espera: %.2f min%n",
            clientesConEspera == 0 ? 0.0 : (double)sumaTiemposEspera / clientesConEspera);
        System.out.println("Cajas utilizadas: " + cajas.size());
        if (minutoAperturaCuartaCaja != null)
            System.out.println("Minuto de apertura de cuarta caja: " + minutoAperturaCuartaCaja);
    }

    public static void main(String[] args) {
        SimuladorEsperanza sim = new SimuladorEsperanza(420, 1, 20); // 7 horas simuladas, llegada cada minuto, apertura > 20
        sim.ejecutar();
        sim.mostrarResultados();
    }
 
}
```
