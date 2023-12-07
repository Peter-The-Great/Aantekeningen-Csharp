Asynchrone programmering in C# is een programmeerparadigma dat het mogelijk maakt om taken uit te voeren zonder de uitvoering van de rest van het programma te blokkeren. In plaats daarvan kunnen taken parallel worden uitgevoerd, waardoor de prestaties van het programma worden verbeterd. In C# wordt asynchrone programmering bereikt met behulp van de `async` en `await` sleutelwoorden. Het `Task` asynchrone programmeermodel (TAP) biedt een abstractie over asynchrone code. Je schrijft code als een reeks statements, net als altijd. Je kunt die code lezen alsof elke statement voltooid is voordat de volgende begint. De compiler voert veel transformaties uit omdat sommige van die statements werk starten en een `Task` retourneren die het lopende werk vertegenwoordigt. Het doel van deze syntaxis is om code mogelijk te maken die leest als een reeks statements, maar uitgevoerd wordt in een veel complexere volgorde op basis van externe resource allocatie en wanneer taken zijn voltooid. Het is analoog aan hoe mensen instructies geven voor processen die asynchrone taken bevatten. In dit artikel gebruik je een voorbeeld van instructies voor het maken van ontbijt om te zien hoe de `async` en `await` sleutelwoorden het gemakkelijker maken om code te begrijpen die een reeks asynchrone instructies bevat.

Meer informatie:
[1. learn.microsoft.com](https://learn.microsoft.com/en-us/dotnet/csharp/asynchronous-programming/ "Asynchronous programming in C# - C# | Microsoft Learn")[2. pluralsight.com](https://www.pluralsight.com/courses/c-sharp-10-asynchronous-programming "Asynchronous Programming in C# 10 | Pluralsight")[3. learn.microsoft.com](https://learn.microsoft.com/en-us/dotnet/csharp/asynchronous-programming/async-scenarios "Asynchronous programming scenarios - C# | Microsoft Learn")[4. educba.com](https://www.educba.com/c-sharp-asynchronous/ "C# Asynchronous | Working of Asynchronous Method in C# | Examples - EDUCBA")[5. tutorialsteacher.com](https://www.tutorialsteacher.com/articles/asynchronous-programming-with-async-await-task-csharp "Asynchronous programming with async, await, Task in C#")+4 meer
## Voorbeeld
```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static async Task Main(string[] args)
    {
        await DoSomethingAsync();
    }

    static async Task DoSomethingAsync()
    {
        Console.WriteLine("Start");
        await Task.Delay(1000);
        Console.WriteLine("End");
    }
}
```

In dit voorbeeld wordt de `DoSomethingAsync`-methode gebruikt om een taak uit te voeren die een vertraging van 1 seconde bevat. De `await`-operator wordt gebruikt om te wachten tot de taak is voltooid voordat de volgende regel code wordt uitgevoerd. De `Main`-methode roept de `DoSomethingAsync`-methode aan met behulp van de `await`-operator om te wachten tot de taak is voltooid voordat de toepassing wordt afgesloten.
# Tasks
Een `Task` in C# is een object dat een asynchrone operatie vertegenwoordigt. Het is een van de centrale componenten van het op taken gebaseerde asynchrone patroon dat voor het eerst werd geïntroduceerd in het .NET Framework 4 [1](https://learn.microsoft.com/en-us/dotnet/api/system.threading.tasks.task?view=net-8.0). Een `Task`-object vertegenwoordigt een enkele operatie die geen waarde retourneert en die meestal asynchroon wordt uitgevoerd. Omdat het werk dat door een `Task`-object wordt uitgevoerd typisch asynchroon op een threadpool-thread wordt uitgevoerd in plaats van synchroon op de hoofdthread van de toepassing, kunt u de `Status`-eigenschap, evenals de `IsCanceled`, `IsCompleted` en `IsFaulted` eigenschappen gebruiken om de status van een taak te bepalen [1](https://learn.microsoft.com/en-us/dotnet/api/system.threading.tasks.task?view=net-8.0). Voor operaties die waarden retourneren, gebruikt u de `Task<TResult>`-klasse [1](https://learn.microsoft.com/en-us/dotnet/api/system.threading.tasks.task?view=net-8.0).

De `Task`-klasse biedt een abstractie over asynchrone code. U schrijft code als een reeks statements, net als altijd. U kunt die code lezen alsof elke statement voltooid is voordat de volgende begint. De compiler voert veel transformaties uit omdat sommige van die statements werk starten en een `Task` retourneren die het lopende werk vertegenwoordigt. Het doel van deze syntaxis is om code mogelijk te maken die leest als een reeks statements, maar uitgevoerd wordt in een veel complexere volgorde op basis van externe resource allocatie en wanneer taken zijn voltooid .

Hier is een voorbeeld van hoe u een `Task` kunt maken en uitvoeren:

Voorbeeld:
```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static async Task Main(string[] args)
    {
        await Task.Run(() => Console.WriteLine("Hello, world!"));
    }
}
```

In dit voorbeeld wordt de `Task.Run`-methode gebruikt om een nieuwe taak te maken en uit te voeren die de tekst “Hello, world!” naar de console schrijft. De `await`-operator wordt gebruikt om te wachten tot de taak is voltooid voordat de toepassing wordt afgesloten .