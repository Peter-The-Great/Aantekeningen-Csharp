https://linqsamples.com/linq-to-objects/generation/Empty-lambda

Voorbeeld van hoe je een list van een array moet maken:
```cs
static void Sample_ToList_Lambda()
{
    string[] names = { "Brenda", "Carl", "Finn" };

    List<string> result = names.ToList();

    Console.WriteLine(String.Format("names is of type: {0}", names.GetType().Name));
    Console.WriteLine(String.Format("result is of type: {0}", result.GetType().Name));
}
```

Voorbeeld van op de Microsoft docs:
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

    var result numbers.Last();

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

    Debug.WriteLine("Highest number is:");
    Debug.WriteLine(result);
}
```