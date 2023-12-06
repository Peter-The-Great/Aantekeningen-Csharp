[In C# is een **property** een lid van een klasse dat toegangsfuncties gebruikt om de waarde van een privéveld te lezen, schrijven of berekenen alsof het een openbaar gegevenslid was](https://learn.microsoft.com/en-us/dotnet/csharp/properties) [1](https://learn.microsoft.com/en-us/dotnet/csharp/properties)[2](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/properties)[3](https://www.tutorialspoint.com/csharp/csharp_properties.htm).

Een property is een vorm van slimme velden in een klasse of object. Van buitenaf gezien lijken ze op velden in het object. Properties kunnen echter worden geïmplementeerd met behulp van de volledige functionaliteit van C#. [U kunt validatie, verschillende toegankelijkheid, lazy evaluation of andere vereisten bieden die uw scenario’s nodig hebben](https://learn.microsoft.com/en-us/dotnet/csharp/properties) [1](https://learn.microsoft.com/en-us/dotnet/csharp/properties).

Hier is een voorbeeld van een property in C#:

```csharp
public class Person
{
    public string FirstName { get; set; }
}
```

In dit voorbeeld is `FirstName` de naam van de property. De `get`- en `set`-accessors worden gebruikt om de waarde van de privéveld `FirstName` te lezen en te schrijven.