package productos;

import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Random;

public class GenerateInfoFiles {

	// Método para generar archivo de información de vendedores
    public void createSalesManInfoFile(int salesmanCount) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("vendedores.txt"))) {
            for (int i = 1; i <= salesmanCount; i++) {
                writer.write("CC;" + i + ";Nombre_" + i + ";Apellido_" + i);
                writer.newLine();
            }
            System.out.println("Archivo de información de vendedores generado.");
        } catch (IOException e) {
            System.err.println("Error al generar archivo: " + e.getMessage());
        }
    }

    // Método para generar archivo de productos
    public void createProductsFile(int productsCount) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("productos.txt"))) {
            Random random = new Random();
            for (int i = 1; i <= productsCount; i++) {
                writer.write(i + ";Producto_" + i + ";" + (random.nextDouble() * 100));
                writer.newLine();
            }
            System.out.println("Archivo de productos generado.");
        } catch (IOException e) {
            System.err.println("Error al generar archivo: " + e.getMessage());
        }
    }

    // Método para generar archivo de ventas de un vendedor
    public void createSalesMenFile(int randomSalesCount, String name, long id) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(name + "_ventas.txt"))) {
            Random random = new Random();
            writer.write("CC;" + id);
            writer.newLine();
            for (int i = 0; i < randomSalesCount; i++) {
                int productId = random.nextInt(100) + 1;
                int quantity = random.nextInt(10) + 1;
                writer.write(productId + ";" + quantity);
                writer.newLine();
            }
            System.out.println("Archivo de ventas de " + name + " generado.");
        } catch (IOException e) {
            System.err.println("Error al generar archivo: " + e.getMessage());
        }
    }

    // Método principal para ejecutar el programa
    public static void main(String[] args) {
        GenerateInfoFiles generador = new GenerateInfoFiles();
        
        // Generar archivos de ejemplo
        generador.createSalesManInfoFile(10); // 10 vendedores
        generador.createProductsFile(50);     // 50 productos
        generador.createSalesMenFile(5, "Vendedor1", 123456789);  // Ventas de Vendedor1
    }

}
