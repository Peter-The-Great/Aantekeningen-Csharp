```cs
using System;
using System.Linq;
using System.Collections.Generic;
using System.Numerics;
using System.IO;

public class Movie
{
    public string? Title { get; set; }

    public int Year { get; set; }

    public string? Director { get; set; }

    public string? Genre { get; set; }
}

public class Program
{
    public static IList<Movie> Movies = new List<Movie>
        {
            new Movie{Title = "2001 A Space Odessy", Year = 1968, Director = "Stanley Kubrick", Genre = "Sci-Fi"},
            new Movie{Title = "The Shining", Year = 1980, Director = "Stanley Kubrick", Genre = "Horror"},
            new Movie{Title = "Dead Poets Society", Year = 1989, Director = "Peter Weir", Genre = "Drama"},
            new Movie{Title = "The Truman Show", Year = 1998, Director = "Peter Weir", Genre = "Sci-Fi"},
            new Movie{Title = "Blade Runner", Year = 1982, Director = "Ridley Scott", Genre = "Sci-Fi"},
            new Movie{Title = "Easy Rider", Year = 1969, Director = "Dennis Hopper", Genre = "Adventure"},
            new Movie{Title = "Once Upon a Time in the West", Year = 1968, Director = "Sergio Leone", Genre = "Western"},
            new Movie{Title = "12 Angry Men", Year = 1957, Director = "Sidney Lumet", Genre = "Drama"},
            new Movie{Title = "A Clockwork Orange", Year = 1971, Director = "Stanley Kubrick", Genre = "Drama"},
            new Movie{Title = "One Flew Over the Cuckoo's Nest", Year = 1975, Director = "Milos Forman", Genre = "Drama"},
            new Movie{Title = "Brazil", Year = 1985, Director = "Terry Gilliam", Genre = "Sci-Fi"},
            new Movie{Title = "Rain Man", Year = 1988, Director = "Barry Levinson", Genre = "Drama"},
            new Movie{Title = "The Good, the Bad and the Ugly", Year = 1968, Director = "Sergio Leone", Genre = "Western"},
            new Movie{Title = "The Perks of Being a Wallflower", Year = 2012, Director = "Stephen Chosky", Genre = "Drama"},
            new Movie{Title = "Wag The Dog", Year = 1997, Director = "Barry Levinson", Genre = "Drama"},
            new Movie{Title = "For A Few Dollars More", Year = 1965, Director = "Sergio Leone", Genre = "Western"},
            new Movie{Title = "Thelma & Louise", Year = 1991, Director = "Ridley Scott", Genre = "Drama"},
            new Movie{Title = "Ali G IndaHouse", Year = 2002, Director = "Mark Mylod", Genre = "Comedy"}
        };


    // Fibonacci sequence
    static IEnumerable<BigInteger> Fibonacci()
    {
        //Hier hebben we twee variabelen aangemaakt die we gebruiken om de Fibonacci getallen te berekenen.
        BigInteger number1 = 1;
        BigInteger number2 = 1;
        //We returnen eerst het eerste getal en daarna het tweede getal.
        //Yield return zorgt ervoor dat de functie niet stopt en dat we de volgende keer verder gaan waar we gebleven waren.
        yield return number1;

        //Terwijl de functie loopt, blijven we de Fibonacci getallen berekenen.
        while (true)
        {
            //We returnen het tweede getal en berekenen het volgende getal.
            yield return number2;
            
            //We maken een tijdelijke variabele aan om het volgende getal in op te slaan.   
            BigInteger temp = number1 + number2;

            //
            number1 = number2;
            
            //We zetten het volgende getal in de variabele number2.
            number2 = temp;
        }
    }

    static void Main(string[] args)
    {
        Opdracht1();
        Console.WriteLine();
        Opdracht2();
        Console.WriteLine();
        Opdracht3();
        Console.WriteLine();
        Opdracht4();
        Console.WriteLine();
        Opdracht5();
        Console.WriteLine();
        Opdracht6();
        Console.WriteLine();
        Opdracht7();
    }

    static void Opdracht1() // Toon van alle films de titel en het jaartal, gesorteerd op jaartal.
    {
        foreach (Movie movie in Movies.OrderBy(m => m.Year))
        {
            Console.WriteLine("{0} - {1}", movie.Title, movie.Year);
        }
    }

    static void Opdracht2() // In welk jaar bracht 'Sergio Leone' zijn eerste film uit?
    {
        Console.WriteLine(Movies.Where(m => m.Director == "Sergio Leone").Select(m => m.Year).OrderBy(year => year).First());
    }

    static void Opdracht3() // Hoeveel films zijn er van 'Peter Weir' van het genre 'Sci-Fi'?.
    {
        Console.WriteLine(Movies.Where(m => m.Director == "Peter Weir" && m.Genre == "Sci-Fi").Count());
    }

    static void Opdracht4() // Toon de 6e t/m 10e film uit de lijst.
    {
        foreach (Movie movie in Movies.Skip(5).Take(5))
        {
            Console.WriteLine("{0}", movie.Title);
        }
    }

    static void Opdracht5() // Is er een film uit 1997 (True/False)?
    {
        Console.WriteLine(Movies.Any(m => m.Year.Equals(1997)));
    }

    static void Opdracht6() // Van welke regisseur is de film 'One Flew over the Cuckoo's Nest'?
    {
        Console.WriteLine(Movies.Single(m => m.Title == "One Flew Over the Cuckoo's Nest").Director);
    }

    static void Opdracht7() // Wat is het 1000e Fibonacci getal?
    {
        Console.WriteLine(Fibonacci().ElementAt(1000 - 1));
    }
}

```