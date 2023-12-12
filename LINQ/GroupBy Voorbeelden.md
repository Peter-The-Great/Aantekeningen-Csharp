`GroupBy` is een LINQ-operatie die wordt gebruikt om een verzameling van elementen te groeperen op basis van een bepaalde sleutel of een kenmerk. Het resultaat is een `IEnumerable` van groepen, waar elke groep bestaat uit een sleutelwaarde en alle elementen die aan die specifieke sleutelwaarde voldoen.

### Syntax:

```csharp
IEnumerable<IGrouping<TKey, TSource>> GroupBy<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector
);
```

- `source`: De verzameling van elementen die je wilt groeperen.
- `keySelector`: Een functie om de sleutel te selecteren op basis waarvan de groepering zal plaatsvinden. Dit kan bijvoorbeeld een eigenschap zijn van de elementen of een berekende waarde.

### Voorbeeld:

Laten we eens kijken naar een voorbeeld met een lijst van steden en hun inwonersaantallen:

```csharp
class City
{
    public string Name { get; set; }
    public string Country { get; set; }
    public int Population { get; set; }
}

// Sample data
List<City> cities = new List<City>
{
    new City { Name = "New York", Country = "USA", Population = 8538000 },
    new City { Name = "Los Angeles", Country = "USA", Population = 3976000 },
    new City { Name = "London", Country = "UK", Population = 8908081 },
    new City { Name = "Manchester", Country = "UK", Population = 547627 },
    new City { Name = "Paris", Country = "France", Population = 2243833 },
    new City { Name = "Marseille", Country = "France", Population = 862211 }
};

// Groepeer steden op basis van het land en selecteer steden in elke groep
var citiesByCountry = cities.GroupBy(city => city.Country);

// Toon het resultaat
foreach (var countryGroup in citiesByCountry)
{
    Console.WriteLine($"Country: {countryGroup.Key}");
    foreach (var city in countryGroup)
    {
        Console.WriteLine($"- {city.Name} ({city.Population} inhabitants)");
    }
    Console.WriteLine();
}
```

Dit voorbeeld groepeert steden op basis van het land waarin ze zich bevinden. De uitvoer zal groepen van steden weergeven, geordend per land:

```
Country: USA
- New York (8538000 inhabitants)
- Los Angeles (3976000 inhabitants)

Country: UK
- London (8908081 inhabitants)
- Manchester (547627 inhabitants)

Country: France
- Paris (2243833 inhabitants)
- Marseille (862211 inhabitants)
```

De `GroupBy`-methode is handig wanneer je elementen wilt categoriseren op basis van gemeenschappelijke kenmerken, zoals eigenschappen, waarden of andere criteria die je kunt selecteren met behulp van de `keySelector`-functie. Het resultaat is een verzameling van groepen waarin de elementen zijn gegroepeerd volgens de gespecificeerde sleutel.

## Complex GroupBy

Complexer voorbeeld:
```cs
static void Sample_GroupBy_Lambda()
{
    int[] numbers = { 10, 15, 20, 25, 30, 35 };

    var result = numbers.GroupBy(n => (n % 10 == 0));

    Console.WriteLine("GroupBy has created two groups:");
    foreach (IGrouping<bool, int> group in result)
    {
        if (group.Key == true)
            Console.WriteLine("Divisible by 10");
        else
            Console.WriteLine("Not Divisible by 10");

        foreach (int number in group)
            Console.WriteLine(number);
    }
}
```
  
Deze functie gebruikt de `GroupBy`-methode om een verzameling van getallen op te splitsen in groepen op basis van een bepaalde voorwaarde, in dit geval, of een getal deelbaar is door 10.
Hier wordt `GroupBy` gebruikt om de getallen te groeperen op basis van de uitkomst van de voorwaarde `(n % 10 == 0)`. Deze voorwaarde controleert of elk getal deelbaar is door 10 en geeft `true` als het deelbaar is en `false` als het niet deelbaar is.

Dit deel van de code loopt door elk groepselement in het resultaat van `GroupBy`. Het controleert of de sleutel (`group.Key`) `true` is (wat betekent dat de getallen deelbaar zijn door 10) en schrijft vervolgens "Divisible by 10". Anders schrijft het "Not Divisible by 10". Vervolgens worden alle getallen in die groep afgedrukt.

De uitvoer van deze functie zal zijn:
```cs
GroupBy has created two groups:
Divisible by 10
10
20
30
Not Divisible by 10
15
25
35
```

## Kun je groupby als een distinct functie gebruiken in linq, kun je daar ook een voorbeeld van geven?

Ja, je kunt `GroupBy` gebruiken om een soortgelijk effect als `Distinct` te bereiken door te groeperen op een specifieke sleutel en vervolgens de eerste (of enige) waarde van elke groep te selecteren. Hier is een voorbeeld:

Laten we zeggen dat we een lijst hebben van getallen en we alleen unieke getallen willen behouden:

```cs
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 1, 2, 2, 3, 3, 4, 5, 5, 5 };

        // Groepeer op elk getal en selecteer het eerste getal in elke groep
        var distinctNumbers = numbers.GroupBy(n => n).Select(n => n.First());

        // Toon de unieke getallen
        foreach (var number in distinctNumbers)
        {
            Console.WriteLine(number);
        }
    }
}
```

In dit voorbeeld wordt `GroupBy` gebruikt om de getallen te groeperen op basis van de waarde zelf. Vervolgens wordt `Select` gebruikt om uit elke groep het eerste getal te selecteren. Dit resulteert in slechts één exemplaar van elk uniek getal in de lijst.

Hiermee verkrijg je hetzelfde resultaat als `Distinct`, waarbij elk element slechts één keer wordt weergegeven, maar dan met behulp van `GroupBy` en `Select`.