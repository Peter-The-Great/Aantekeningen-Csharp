Inprincipe hetzelfde als hier:[[Meer attributen van EF]]
Maar ik zal het nog een keer uitleggen.
Modelvalidatie is een belangrijk onderdeel van het ASP.NET Core framework. Het stelt je in staat om de gegevens die door de gebruiker worden ingevoerd te valideren en te controleren of deze voldoen aan de verwachte regels. Dit helpt bij het voorkomen van ongeldige gegevens en het verbeteren van de gebruikerservaring.

In ASP.NET Core kun je modelvalidatie implementeren met behulp van de `ModelState`-klasse. Deze klasse bevat informatie over de status van de validatie van het model en eventuele fouten die zijn opgetreden.

Hier is een voorbeeld van hoe je modelvalidatie kunt gebruiken in een ASP.NET Core-applicatie:

```csharp
public class Person
{
    [Required]
    public string Name { get; set; }

    [Range(0, 120)]
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
        if (!ModelState.IsValid)
        {
            return View(person);
        }

        // Code om de persoon op te slaan

        return RedirectToAction("Index");
    }
}
```

In dit voorbeeld wordt de `Person`-klasse gedefinieerd met twee eigenschappen: `Name` en `Age`. De `[Required]`-attribuut wordt gebruikt om aan te geven dat de `Name`-eigenschap verplicht is en de `[Range]`-attribuut wordt gebruikt om aan te geven dat de `Age`-eigenschap een waarde tussen 0 en 120 moet hebben.

In de `Create`-actie van de `PersonController`-klasse wordt een nieuw `Person`-object gemaakt op basis van de gegevens die door de gebruiker zijn ingevoerd. De `ModelState.IsValid`-eigenschap wordt vervolgens gecontroleerd om te zien of er fouten zijn opgetreden tijdens de validatie. Als er fouten zijn opgetreden, wordt de `Create`-weergave opnieuw weergegeven met de ingevoerde gegevens en de foutmeldingen. Als er geen fouten zijn opgetreden, wordt de persoon opgeslagen en wordt de gebruiker doorgestuurd naar de `Index`-weergave.
[1. Microsoft Learn](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-8.0)