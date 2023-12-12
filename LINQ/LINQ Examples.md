Bronnen:
https://linqsamples.com/

Meeste van de voorbeelden die hier gegeven zijn in principe queries. Er is wel een degelijk verschil tussen een query en een query als Lambda expression. Meestal gebruiken we in de toets een Lambda Query om antwoord te gegeven op onze formulieren.

**Het grappige aan LINQ is dat het lijkt op SQL.**

Voorbeeld van hoe je een list van een array moet maken **(Lambda Query)**:
```cs
static void Sample_ToList_Lambda()
{
    string[] names = { "Brenda", "Carl", "Finn" };

    List<string> result = names.ToList();

    Console.WriteLine(String.Format("names is of type: {0}", names.GetType().Name));
    Console.WriteLine(String.Format("result is of type: {0}", result.GetType().Name));
}
```

Voorbeeld van op de Microsoft docs **(Normale Query)**:
```cs
using System;
using System.Linq;

public class Program
{
	public static void Main()
	{
		// Data source
		string[] names = {"Bill", "Steve", "James", "Mohan" };
        
		// LINQ Query 
        var myLinqQuery =  from name in names
            			   where name.Contains('a')
            				select name;
        
		// Query execution
        foreach (var name in myLinqQuery)
            Console.WriteLine(name);
	}
}
```

Voorbeeld om met empty te gebruiken:
```cs
static void Sample_Empty_Lambda()
{
    var empty = Enumerable.Empty<string>();
    // To make sequence into an array use empty.ToArray()

    Console.WriteLine("Sequence is empty:");
    Console.WriteLine(empty.Count() == 0);
}
```

Voorbeeld van het laatste onderdeel te pakken uit de lijst:
```cs
static void Sample_Last_Lambda()
{
    int[] numbers = { 7, 3, 5 };

    var result = numbers.Last();

    Console.WriteLine("Last number in array is:");
    Console.WriteLine(result);
}
```

Voorbeeld van Max:
```cs
static void Sample_Max_Lambda()
{
    int[] numbers = { 2, 8, 5, 6, 1 };

    var result = numbers.Max();

    Console.WriteLine("Highest number is:");
    Console.WriteLine(result);
}
```

Voorbeeld van Single
```cs
// Note: Single will throw an Exception, if there is not exactly one element in the array.
static void Sample_Single_Lambda()
{
    string[] names1 = { "Peter" };
    string[] names3 = { "Peter", "Joe", "Wilma" };
    string[] empty = { };

    var result1 = names1.Single();

    Console.WriteLine("The only name in the array is:");
    Console.WriteLine(result1);

    try
    {
        // This will throw an exception because array contains no elements
        var resultEmpty = empty.Single();
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }

    try
    {
        // This will throw an exception as well because array contains more than one element
        var result3 = names3.Single();
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }
}
```

Voorbeeld van GroupBy, meer over groupby vind je hier. [[GroupBy Voorbeelden]]
```cs
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<Person> people = new List<Person>
        {
            new Person { Name = "Alice", Age = 25 },
            new Person { Name = "Bob", Age = 30 },
            new Person { Name = "Charlie", Age = 25 },
            new Person { Name = "David", Age = 30 },
            new Person { Name = "Eve", Age = 20 }
        };

        // GroupBy leeftijdscategorieën
        var groupedByAge = people.GroupBy(p => p.Age);

        // Itereer over de groepen en toon de resultaten
        foreach (var group in groupedByAge)
        {
            Console.WriteLine($"Leeftijdscategorie: {group.Key}");
            foreach (var person in group)
            {
                Console.WriteLine($"- {person.Name}");
            }
        }
    }
}

class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```

`Aggregate` is een LINQ-functie waarmee je een aggregatie uitvoert op een verzameling elementen. Het voert een specifieke bewerking uit op elk element van de verzameling en houdt een geaccumuleerd resultaat bij terwijl het door de elementen gaat.

### Voorbeeld:

Stel dat we een lijst van getallen hebben en we willen de som van alle elementen berekenen met behulp van `Aggregate`.

```csharp
using System;
using System.Linq;

class Program
{
    static void Main()
    {
        int[] numbers = { 1, 2, 3, 4, 5 };

        // Bereken de som van alle getallen met behulp van Aggregate
        int sum = numbers.Aggregate((acc, x) => acc + x);

        Console.WriteLine($"De som van de getallen is: {sum}");
    }
}
```

In dit voorbeeld wordt `Aggregate` gebruikt om de som van alle getallen in de lijst te berekenen. De `acc` parameter houdt het geaccumuleerde resultaat bij, terwijl `x` door elk element in de lijst gaat en dat toevoegt aan het geaccumuleerde resultaat `acc`.

De uitvoer zal zijn:

```
De som van de getallen is: 15
```

Dit is slechts een eenvoudig voorbeeld van `Aggregate`. De kracht van `Aggregate` ligt in het feit dat je het kunt gebruiken om complexere bewerkingen uit te voeren op elementen in een collectie, zoals het uitvoeren van reductiebewerkingen, het samenstellen van strings, het vinden van het maximum/minimum, enzovoort. Je kunt ook een beginwaarde opgeven voor het geaccumuleerde resultaat.

Bijvoorbeeld, als je een beginwaarde wilt specificeren, zou je de `Aggregate`-methode als volgt gebruiken:

```csharp
int sumWithSeed = numbers.Aggregate(0, (acc, x) => acc + x);
```

Hier wordt `0` gebruikt als het startpunt voor de som. Dit zal resulteren in dezelfde uitvoer als eerder, namelijk `15`.