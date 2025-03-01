# Mision-secreta-

using System;
using System.IO;

class Program
{
    static void Main()
    {
        int opcion;
        do
        {
            Console.WriteLine("\n=== Menú de Gestión de Inventos de Tony Stark ===");
            Console.WriteLine("1. Crear archivo de inventos");
            Console.WriteLine("2. Agregar invento");
            Console.WriteLine("3. Leer inventos línea por línea");
            Console.WriteLine("4. Leer todo el archivo");
            Console.WriteLine("5. Mover archivo");
            Console.WriteLine("7. Crear carpeta");
            Console.WriteLine("8. Listar archivos");
            Console.WriteLine("9.Copiar archivo");
            Console.WriteLine("10.Salir ");
            Console.Write("Seleccione una opción: ");
           

            if (!int.TryParse(Console.ReadLine(), out opcion))
            {
                Console.WriteLine("Por favor, ingrese un número válido.");
                continue;
            }

           
            switch (opcion)
            {
                case 1:
                    CrearArchivo();
                    break;
                case 2:
                    Console.Write("Ingrese el invento a agregar: ");
                    string invento = Console.ReadLine();
                    AgregarInvento(invento);
                    break;
                case 3:
                    LeerLineaPorLinea();
                    break;
                case 4:
                    LeerTodoElTexto();
                    break;
                case 5:
                    Console.Write("Ingrese la nueva ruta del archivo (incluya el nombre del archivo): ");
                    string nuevaRuta = Console.ReadLine();
                    MoverArchivo("inventos.txt", nuevaRuta);
                    break;
                case 7:
                    Console.Write("Ingrese el nombre de la carpeta: ");
                    string carpeta = Console.ReadLine();
                    CrearCarpeta(carpeta);
                    break;
                case 8:
                    ListarArchivos("LaboratorioAvengers");
                    break;
                case 9:
                    CopiarArchivo("inventos.txt", "Backup/inventos_backup.txt"); break;
                    break;

                case 10:
                    Console.WriteLine("Saliendo del programa...");
                    break;
                default:
                    Console.WriteLine("Opción no válida.");
                    break;
            }
        } while (opcion != 10);
    }
    static void CrearArchivo()
    {
        // Ruta completa incluyendo el nombre del archivo
        string path = "C:\\Users\\HP\\OneDrive\\Escritorio\\3r semestre 2025\\Programacion 1 2025\\LaboStark\\inventos.txt";

        // Contenido con saltos de línea correctos
        string contenido = "1. Traje Mark I\n2. Reactor Arc\n3. Inteligencia Artificial JARVIS";

        try
        {
            File.WriteAllText(path, contenido);
            Console.WriteLine("Archivo creado exitosamente.");
        }
        catch (FileNotFoundException)
        {
            Console.WriteLine("No existe el archivo.");
        }
        catch (DirectoryNotFoundException)
        {
            Console.WriteLine("Tu carpeta no existe.");
        }
        catch (Exception err)
        {
            Console.WriteLine($"Error desconocido: {err.Message}");
        }
    }

    static void AgregarInvento(string invento)
    {
        try
        {
            File.AppendAllText("inventos.txt", invento + "\n");
            Console.WriteLine("Invento agregado exitosamente.");
        }
        catch (Exception e)
        {
            Console.WriteLine($"Error al agregar invento: {e.Message}");
        }
    }

    static void LeerLineaPorLinea()
    {
        try
        {
            using (StreamReader lector = new StreamReader("inventos.txt"))
            {
                string linea;
                while ((linea = lector.ReadLine()) != null)
                {
                    Console.WriteLine(linea);
                }
            }
        }
        catch (Exception e)
        {
            Console.WriteLine($"Error al leer el archivo: {e.Message}");
        }
    }

    static void LeerTodoElTexto()
    {
        try
        {
            string contenido = File.ReadAllText("inventos.txt");
            Console.WriteLine(contenido);
        }
        catch (Exception e)
        {
            Console.WriteLine($"Error al leer el archivo: {e.Message}");
        }
    }
    static void CopiarArchivo(string origen, string destino)
    {
        try
        {
            Directory.CreateDirectory(Path.GetDirectoryName(destino));
            File.Copy(origen, destino, true);
            Console.WriteLine("Archivo copiado con éxito.");
        }
        catch (Exception err) { Console.WriteLine($"Error: {err.Message}"); }
    }

    static void MoverArchivo(string archivo1, string destino)
    {
        string path = "C:\\Users\\HP\\OneDrive\\Escritorio\\3r semestre 2025\\Programacion 1 2025\\LaboStark\\inventos";
        Console.WriteLine($"La ruta de la carpeta donde se moverá el archivo es: {destino}");

        if (!Directory.Exists(destino))
        {
            Directory.CreateDirectory(destino);
        }

        try
        {
            File.Move(archivo1, destino);
            Console.WriteLine("Archivo movido exitosamente.");
        }
        catch (Exception e)
        {
            Console.WriteLine($"Error al mover el archivo: {e.Message}");
        }
    }
    static void CrearCarpeta(string nombreCarpeta)
    {
        try
        {
            Directory.CreateDirectory(nombreCarpeta);
            Console.WriteLine("Carpeta creada con éxito.");
        }
        catch (Exception err) { Console.WriteLine($"Error: {err.Message}"); }
    }

    static void ListarArchivos(string ruta)
    {
        try
        {
            if (!Directory.Exists(ruta))
            {
                Console.WriteLine("La carpeta no existe.");
                return;
            }
            string[] archivos = Directory.GetFiles(ruta);
            Console.WriteLine("Archivos en la carpeta:");
            foreach (string archivo in archivos)
            {
                Console.WriteLine(Path.GetFileName(archivo));
            }
        }
        catch (Exception err) { Console.WriteLine($"Error: {err.Message}"); }
    }


}



