Bronnen: [Microsoft Docs](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/operator-overloading)

Operator overloading is een functie in C# die het mogelijk maakt om de betekenis van een operator te wijzigen voor gebruikersgedefinieerde typen. Dit betekent dat we de betekenis van een operator kunnen wijzigen, zodat deze kan worden gebruikt met objecten van onze eigen klassen.

Bijvoorbeeld, als we een klasse `Vector` hebben die een vector in twee dimensies vertegenwoordigt, kunnen we de `+` operator overschrijven om twee vectoren bij elkaar op te tellen:

```csharp
class Vector {
    public int X { get; set; }
    public int Y { get; set; }

    public static Vector operator +(Vector a, Vector b) {
        return new Vector { X = a.X + b.X, Y = a.Y + b.Y };
    }
}
```

In dit voorbeeld hebben we een `Vector` klasse gedefinieerd met `X` en `Y` eigenschappen. We hebben ook de `+` operator overschreven om twee vectoren bij elkaar op te tellen. Wanneer we twee vectoren bij elkaar optellen, worden de `X` en `Y` eigenschappen van de vectoren bij elkaar opgeteld.

We kunnen de `+` operator nu gebruiken om twee vectoren bij elkaar op te tellen:

```csharp
Vector a = new Vector { X = 1, Y = 2 };
Vector b = new Vector { X = 3, Y = 4 };
Vector c = a + b;
```

In dit voorbeeld maken we twee vectoren `a` en `b` en voegen we ze samen om een nieuwe vector `c` te maken. De `+` operator roept automatisch de `operator +` methode aan die we hebben gedefinieerd.