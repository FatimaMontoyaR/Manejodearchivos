# Manejodearchivos
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.HashMap;
import java.util.Map;

public class AnalisisCodigosPostales {

    public static void main(String[] args) {

        String rutaArchivo = "data/codigos_postales_hmo.csv";
        HashMap<String, Integer> conteoCodigos = new HashMap<>();

        // Lectura del archivo CSV
        try (BufferedReader br = new BufferedReader(new FileReader(rutaArchivo))) {
            String linea;

            while ((linea = br.readLine()) != null) {
                // Separa por coma (asentamiento,codigo_postal)
                String[] datos = linea.split(",");

                if (datos.length >= 2) {
                    String codigoPostal = datos[1].trim();

                    // Actualiza el conteo del código postal
                    conteoCodigos.put(
                        codigoPostal,
                        conteoCodigos.getOrDefault(codigoPostal, 0) + 1
                    );
                }
            }

        } catch (IOException e) {
            System.out.println("Error al leer el archivo: " + e.getMessage());
            return;
        }

        // Mostrar resultados
        System.out.println("Resultados del análisis:\n");

        for (Map.Entry<String, Integer> entry : conteoCodigos.entrySet()) {
            System.out.println(
                "Código postal: " + entry.getKey() +
                " - Número de asentamientos: " + entry.getValue()
            );
        }

    
