# Grafos_FreddyP
//Ismael Ortega: 10145335

package logico;

import java.util.*;

class Grafos {
    private Map<String, List<String>> listaAdyacencia;

    public Grafos() {
        listaAdyacencia = new TreeMap<>(); // TreeMap para ordenar los vértices automáticamente
    }

    // Método para agregar una arista al grafo
    public void agregarArista(String v1, String v2) {
        listaAdyacencia.putIfAbsent(v1, new ArrayList<>());
        listaAdyacencia.putIfAbsent(v2, new ArrayList<>());
        listaAdyacencia.get(v1).add(v2);
        listaAdyacencia.get(v2).add(v1); // Grafo no dirigido
    }
 
    // Método para calcular la secuencia de grados de los vértices
    public List<Integer> calcularSecuenciaGrados() {
        List<Integer> secuenciaGrados = new ArrayList<>();
        for (String vertice : listaAdyacencia.keySet()) {
            secuenciaGrados.add(listaAdyacencia.get(vertice).size());
        }
        Collections.sort(secuenciaGrados);
        return secuenciaGrados;
    }

    // Método para generar la lista de adyacencia
    public void generarListaAdyacencia() {
    	
        System.out.println("\nLista de adyacencia del grafo:");
        for (Map.Entry<String, List<String>> entry : listaAdyacencia.entrySet()) {
        	
            List<String> vecinos = entry.getValue();
            Collections.sort(vecinos); // Ordenamos la lista de vecinos para mantener consistencia
            System.out.println(entry.getKey() + " -> " + vecinos);
            
        }
    }
}

// Clase Main para ejecutar el programa
public class Principal {
    public static void main(String[] args) {
        Grafo grafo = new Grafo();

     // Agregar las aristas proporcionadas
        String[][] aristas = {
                {"A", "B"}, {"A", "C"}, {"B", "D"}, {"B", "E"}, {"C", "F"},
                {"C", "G"}, {"D", "E"}, {"D", "H"}, {"E", "I"}, {"F", "G"},
                {"G", "H"}, {"H", "I"}, {"I", "F"}
            };

            for (String[] arista : aristas) {
                grafo.agregarArista(arista[0], arista[1]);
            }

        // Calcular y mostrar la secuencia de grados
        List<Integer> secuenciaGrados = grafo.calcularSecuenciaGrados();
        System.out.print("Secuencia de grados: ");
        for (int grado : secuenciaGrados) {
            System.out.print(grado + " ");
        }
        System.out.println();
        System.out.print("\t\t     A B C D E F G H I");
        System.out.println();

        grafo.generarListaAdyacencia();
    }
}
