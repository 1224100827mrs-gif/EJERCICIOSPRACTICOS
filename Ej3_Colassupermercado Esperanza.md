# Ejercicio3 
## Tema>:Colas
## Descripción:
### Simular el flujo de atención durante 7 horas considerando:
#### • Una fila única de clientes.
#### • 3 cajas activas, con posibilidad de abrir una cuarta caja si hay más de 20 clientes.
#### • Tiempos de atención distribuidos uniformemente por caja.
#### • Llegadas de clientes cada minuto (en promedio).
#### • Estadísticas a calcular:
#### o Total de clientes atendidos.
#### o Tamaño medio y máximo de la fila.
#### o Tiempo máximo de espera.
#### o Tiempo de apertura de la cuarta caja.

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

/**
 * Clase que representa una caja en el supermercado
 * @author Marisol Rincón Solis
 */
public class Caja {
    private Cliente atendiendo;
    private int id;
    private int minutosRestantes = 0;

    public Caja(int id) {
        this.id = id;
    }

    public boolean estaLibre() {
        return atendiendo == null;
    }

    public void agregarCliente(Cliente c) {
        this.atendiendo = c;
    }

    public void setMinutosRestantes(int minutos) {
        this.minutosRestantes = minutos;
    }

    /** Decrementa el tiempo restante. Si llega a 0, libera la caja */
    public void decrementarMinutosRestantes() {
        if (atendiendo != null) {
            minutosRestantes--;
            if (minutosRestantes <= 0) {
                atender();  // libera
            }
        }
    }

    public void atender() {
        this.atendiendo = null;
        this.minutosRestantes = 0;
    }

    public int getId() {
        return id;
    }
}


```

```java
package Cola.EjerciciosPracticos.Ej3;

import java.util.LinkedList;
import java.util.Queue;
import java.util.List;
import java.util.ArrayList;
import java.util.Random;

/**
 * Simulación de atención al cliente con fila única y hasta 4 cajas
 * Genera estadísticas de clientes atendidos, tiempo de espera y apertura de cuarta caja
 * @author Marisol Rincón Solis
 */
public class SimuladorEsperanza implements Simulador {
    private Queue<Cliente> filaClientes = new LinkedList<>();
    private List<Caja> cajas = new ArrayList<>();
    private int clientesAtendidos = 0;
    private int tiempoMaximoEspera = 0;
    private int sumaTiemposEspera = 0;
    private int clientesConEspera = 0;
    private int tamanoMaximoFila = 0;
    private long sumaTamanoFila = 0;  // para promedio de tamaño de fila
    private int tiempoSimulacion;
    private int frecuenciaLlegadas;
    private int umbralApertura;
    private Integer minutoAperturaCuartaCaja = null;
    private Random random = new Random();

    /**
     * Constructor con parámetros de simulación
     * @param tiempoSimulacion duración en minutos de la simulación
     * @param frecuenciaLlegadas cada cuántos minutos llega un cliente
     * @param umbralApertura si el promedio de clientes por caja > umbral abre cuarta caja
     */
    public SimuladorEsperanza(int tiempoSimulacion, int frecuenciaLlegadas, int umbralApertura) {
        this.tiempoSimulacion = tiempoSimulacion;
        this.frecuenciaLlegadas = frecuenciaLlegadas;
        this.umbralApertura = umbralApertura;

        // Inicializamos con 3 cajas activas
        for (int i = 1; i <= 3; i++) {
            cajas.add(new Caja(i));
        }
    }

    @Override
    public void ejecutar() {
        System.out.println("=== INICIO SIMULACION ESPERANZA ===");

        for (int minuto = 0; minuto < tiempoSimulacion; minuto++) {
            // Llegada de clientes cada frecuenciaLlegadas minutos
            if (minuto % frecuenciaLlegadas == 0) {
                Cliente c = new Cliente(clientesAtendidos + filaClientes.size() + 1, minuto);
                filaClientes.add(c);
            }

            // Actualizamos estadísticas de fila
            tamanoMaximoFila = Math.max(tamanoMaximoFila, filaClientes.size());
            sumaTamanoFila += filaClientes.size();

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

                    // Asignar duración de atención aleatoria entre 1 y 4 minutos
                    int duracionAtencion = 1 + random.nextInt(4);
                    caja.setMinutosRestantes(duracionAtencion);
                }
                // Reducir el tiempo restante de atención si está ocupado
                if (!caja.estaLibre()) {
                    caja.decrementarMinutosRestantes();
                }
            }

            // Verificamos si necesitamos abrir la cuarta caja
            int promedioActualCaja = filaClientes.size() / Math.max(1, cajas.size());
            if (promedioActualCaja > umbralApertura && cajas.size() == 3) {
                cajas.add(new Caja(4));
                minutoAperturaCuartaCaja = minuto;
                System.out.println("Se abre cuarta caja en minuto " + minuto);
            }
        }

        mostrarResultados();
    }

    @Override
    public void mostrarResultados() {
        double promedioTamanoFila = (double) sumaTamanoFila / tiempoSimulacion;
        double promedioEspera = clientesConEspera == 0 ? 0.0 : (double) sumaTiemposEspera / clientesConEspera;

        System.out.println("\n=== RESULTADOS SIMULACION ===");
        System.out.println("Clientes atendidos: " + clientesAtendidos);
        System.out.println("Tamaño máximo de fila: " + tamanoMaximoFila);
        System.out.printf("Tamaño promedio de fila: %.2f%n", promedioTamanoFila);
        System.out.println("Tiempo máximo de espera: " + tiempoMaximoEspera + " min");
        System.out.printf("Tiempo promedio de espera: %.2f min%n", promedioEspera);
        System.out.println("Cajas utilizadas: " + cajas.size());
        if (minutoAperturaCuartaCaja != null) {
            System.out.println("Minuto de apertura de cuarta caja: " + minutoAperturaCuartaCaja);
        }
    }

    public static void main(String[] args) {
        SimuladorEsperanza sim = new SimuladorEsperanza(420, 1, 20); // 420 minutos (7 horas), llegada cada 1 minuto, umbral 20
        sim.ejecutar();
    }
}
```

## Evidencia 
<img width="570" height="489" alt="image" src="https://github.com/user-attachments/assets/2eefac0a-e7ee-499a-829b-a929d4736b0c" />

