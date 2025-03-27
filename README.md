# 3. POO (Módulo CSharp)

1. Crea una función isBookRead que reciba una lista de libros y un título y devuelva si se ha leído o no dicho libro. Un libro es un objeto con title como string y isRead como booleano. En caso de no existir el libro devolver false.

    ```
    public bool IsBookRead(Boook books, string titleToSearch)
    {
        // Implementation here
    }
    ```

    Ejemplo

    ```
    var books = new Book[] {
        new Book
        {
            Title = "Harry Potter y la piedra filosofal",
            IsRead = true
        },
        new Book
        {
            Title = "Canción de hielo y fuego",
            IsRead = false
        },
        new Book
        {
            Title = "Devastación",
            IsRead = true
        },
    }; 

    Console.WriteLine(IsBookRead(books, "Devastación")); // true
    Console.WriteLine(IsBookRead(books, "Canción de hielo y fuego")); // false
    Console.WriteLine(IsBookRead(books, "Los Pilares de la Tierra")); // false
    ```

```csharp
namespace curso_csharp
{
    public class Book
    {
        public String title
        {
            get; set;
        }

        public Boolean isRead
        {
            get; set;
        }   

        public Book(String title, Boolean isRead)
        {
            this.title = title;
            this.isRead = isRead;
        }
    }

    internal class Program
    {
        static void Main(string[] args)
        {
            Book libro1 = new Book("El fuego de la venganza", true);
            Book libro2 = new Book("Buenas noches Punpun", false);
            Book libro3 = new Book("El secreto", true);

            List<Book> books = new List<Book>();
            books.Add(libro1);
            books.Add(libro2);
            books.Add(libro3);

            Console.WriteLine(IsBookRead(books, "El fuego de la venganza"));    // true
            Console.WriteLine(IsBookRead(books, "Buenas noches Punpun"));       // false
            Console.WriteLine(IsBookRead(books, "El secreto"));                 // true
            Console.WriteLine(IsBookRead(books, "Soy un libro inexistente"));   // false
            Console.ReadLine();
        }

        private static bool IsBookRead(List<Book> books, String titleToSearch)
        {
            foreach (Book book in books)
            {
                if (titleToSearch.Equals(book.title))
                {
                    return book.isRead;
                }
            }
            return false;
        }
    }
}
```

2. El objetivo de este ejercicio es crear una máquina tragaperras utilizando clases donde cada vez que juguemos insertemos una moneda. Cada máquina tragaperras (instancia) tendrá un **contador de monedas** que automáticamente se irá incrementando conforme vayamos jugando.

    Cuando se llame al **método play** el número de monedas se debe incrementar de forma automática y debe generar **tres booleanos aleatorios** que representarán el estado de las 3 ruletas. El usuario habrá ganado en caso de que los tres booleanos sean true, y por tanto deberá mostrarse por consola el mensaje:

    ```
    "Congratulations!!!. You won <número de monedas> coins!!";
    ```

    y reiniciar las monedas almacenadas, ya que las hemos conseguido y han salido de la máquina. En caso contrario deberá mostrar otro mensaje:

    ```
    "Good luck next time!!".
    ```

    Se preguntará al usuario si quiere jugar o dejar.

    - Si el usuario elige jugar. Se llamará al método play.
    - Si usuario elige cualquier otra opción se terminará   la ejecución de la aplicación.

```csharp
namespace curso_csharp
{
    internal class Program
    {
        public class Tragaperras
        {
            private int contadorMonedas {  get; set; }

            public Tragaperras(int contadorMonedas)
            {
                this.contadorMonedas = contadorMonedas;
            }

            public void Play()
            {
                contadorMonedas++;
                Random r1 = new Random();
                Random r2 = new Random();
                Random r3 = new Random();

                int num1 = r1.Next(1, 3);
                int num2 = r2.Next(1, 3);
                int num3 = r3.Next(1, 3);

                Boolean ruleta1;
                Boolean ruleta2;
                Boolean ruleta3;

                if (num1 == 1)
                {
                    ruleta1 = true;
                } else
                {
                    ruleta1 = false;
                }

                if (num2 == 1)
                {
                    ruleta2 = true;
                }
                else
                {
                    ruleta2 = false;
                }

                if (num3 == 1)
                {
                    ruleta3 = true;
                } else
                {
                    ruleta3 = false;
                }

                if (ruleta1 == true && ruleta2 == true && ruleta3 == true)
                {
                    Console.WriteLine($"Enhorabuena!!! Has ganado {contadorMonedas} monedas!!!");
                    Console.WriteLine();
                    contadorMonedas = 0;
                    Console.ReadLine();
                    Environment.Exit(0);
                }
                else
                {
                    Console.WriteLine("Has perdido... Buena suerte la proxima vez!!!");
                    Console.WriteLine();
                }
            }
        }
        static void Main(string[] args)
        {
            int opcion = 0; ;

            // Se imagina que en la maquina ya hay 50 monedas
            // de otras personas que han jugado
            int monedas_iniciales = 50;
            Tragaperras t1 = new Tragaperras(monedas_iniciales);

            while (true)
            {
                Console.WriteLine("~ Bienvenido al salon de juegos ~");
                Console.WriteLine("1) Jugar.");
                Console.WriteLine("2) Salir."); // Realmente es cualquier otro int
                opcion = Convert.ToInt32(Console.ReadLine());

                if (opcion == 1)
                {
                    t1.Play();
                } else
                {
                    Console.WriteLine("Hasta luego!");
                    break;
                }
            }
            
            Console.ReadLine();
        }   
    }
}
```