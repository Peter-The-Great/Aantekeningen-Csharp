Method binding is een functie van het ASP.NET Core framework waarmee je de gegevens van een HTTP-verzoek kunt binden aan de parameters van een controlleractie. Dit betekent dat je de gegevens die door de gebruiker zijn ingevoerd, kunt gebruiken om de actie uit te voeren.

Hier is een voorbeeld van hoe je method binding kunt gebruiken in een ASP.NET Core-applicatie:

```csharp
public class PersonController : Controller
{
    public IActionResult Create()
    {
        return View();
    }

    [HttpPost]
    public IActionResult Create(string name, int age)
    {
        // Code om de persoon op te slaan

        return RedirectToAction("Index");
    }
}
```

In dit voorbeeld wordt de `Create`-actie van de `PersonController`-klasse gedefinieerd met twee parameters: `name` en `age`. Deze parameters worden automatisch ingevuld met de waarden die door de gebruiker zijn ingevoerd wanneer de actie wordt aangeroepen.

Om method binding te gebruiken, moet je ervoor zorgen dat de namen van de parameters overeenkomen met de namen van de velden in het formulier dat door de gebruiker is ingevuld. Als de namen niet overeenkomen, kun je de `[FromForm]`-attribuut gebruiken om aan te geven waar de gegevens vandaan moeten worden gehaald.

## Verschil Model en Method Binding
Modelbinding en method binding zijn beide functies van het ASP.NET Core framework die worden gebruikt om gegevens van HTTP-verzoeken te binden aan de parameters van een controlleractie. Het belangrijkste verschil tussen de twee is dat modelbinding wordt gebruikt om complexe objecten te binden aan controlleracties, terwijl method binding wordt gebruikt om eenvoudige gegevenstypen te binden.

Bij modelbinding wordt de gegevens van een HTTP-verzoek gebonden aan de eigenschappen van een complex object. Dit betekent dat je de gegevens die door de gebruiker zijn ingevoerd, kunt gebruiken om het complexe object te maken. Bij method binding worden de gegevens van een HTTP-verzoek gebonden aan de parameters van een controlleractie. Dit betekent dat je de gegevens die door de gebruiker zijn ingevoerd, kunt gebruiken om de actie uit te voeren.

Hier is een voorbeeld van hoe je modelbinding kunt gebruiken om een complex object te binden aan een controlleractie:

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

public class PersonController : Controller
{
    public IActionResult Create()
    {
        return View();
    }

    [HttpPost]
    public IActionResult Create(Person person)
    {
        // Code om de persoon op te slaan

        return RedirectToAction("Index");
    }
}
```

In dit voorbeeld wordt de `Person`-klasse gedefinieerd met twee eigenschappen: `Name` en `Age`. De `Create`-actie van de `PersonController`-klasse wordt gedefinieerd met één parameter: `person`. Deze parameter wordt automatisch ingevuld met de waarden die door de gebruiker zijn ingevoerd wanneer de actie wordt aangeroepen.

Hier is een voorbeeld van hoe je method binding kunt gebruiken om eenvoudige gegevenstypen te binden aan een controlleractie:

```csharp
public class PersonController : Controller
{
    public IActionResult Create()
    {
        return View();
    }

    [HttpPost]
    public IActionResult Create(string name, int age)
    {
        // Code om de persoon op te slaan

        return RedirectToAction("Index");
    }
}
```

In dit voorbeeld wordt de `Create`-actie van de `PersonController`-klasse gedefinieerd met twee parameters: `name` en `age`. Deze parameters worden automatisch ingevuld met de waarden die door de gebruiker zijn ingevoerd wanneer de actie wordt aangeroepen.

Learn more: [1.](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-7.0) [2.](https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/controller-methods-views?view=aspnetcore-8.0)
