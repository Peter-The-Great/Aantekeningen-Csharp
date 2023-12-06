In C# is een **base class** een klasse die wordt gebruikt om andere klassen te maken of af te leiden. Klassen die zijn afgeleid van een base class worden child classes, subclasses of derived classes genoemd. [Een base class erft niet van een andere klasse en wordt beschouwd als de ouder van een afgeleide klasse](https://www.techopedia.com/definition/3747/base-class-net-c) [1](https://www.techopedia.com/definition/3747/base-class-net-c).

Een **derived class** is een klasse die de leden van de base class erft. De klasse die de leden van de base class erft, wordt de derived class genoemd. C# en .NET ondersteunen alleen single inheritance. [Dat wil zeggen, een klasse kan alleen van één klasse erven](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/tutorials/inheritance) [2](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/tutorials/inheritance)[3](https://www.w3schools.com/cs/cs_inheritance.php).

Hier is een voorbeeld van een base class en een derived class in C#:

C#Door AI gegenereerde code. Controleer en gebruik zorgvuldig. .

```csharp
public class Animal
{
    public void Eat()
    {
        Console.WriteLine("The animal is eating.");
    }
}

public class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("The dog is barking.");
    }
}
```

In dit voorbeeld is `Animal` de base class en `Dog` is de derived class. De `Dog`-klasse erft de `Eat()`-methode van de `Animal`-klasse en voegt een nieuwe methode `Bark()` toe.