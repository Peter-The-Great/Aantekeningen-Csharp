Bronnen:
https://linqsamples.com/linq-to-objects/generation/Empty-lambda
https://www.tutorialsteacher.com/linq/why-linq

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