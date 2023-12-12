In het ASP.NET Core framework zijn services verantwoordelijk voor het uitvoeren van specifieke taken, zoals authenticatie, autorisatie, caching, enz. Services zijn geregistreerd in de DI-container van de app en kunnen worden geïnjecteerd in andere delen van de app, zoals controllers, middleware, enz.

Het ASP.NET Core framework bevat standaard services die kunnen worden gebruikt in een app, zoals Entity Framework Core, ASP.NET Core Identity, enz. Je kunt ook je eigen services maken en registreren in de DI-container van de app.

Services worden geregistreerd in de `ConfigureServices`-methode van de `Startup`-klasse. Hier is een voorbeeld van hoe je een service kunt registreren:

```csharp
services.AddTransient<IMyService, MyService>();
```

In dit voorbeeld wordt de `MyService`-klasse geregistreerd als implementatie van de `IMyService`-interface. De `AddTransient`-methode geeft aan dat een nieuwe instantie van de service moet worden gemaakt voor elke afhankelijkheid.

Om een ​​service te gebruiken in een controller, kun je de service injecteren in de constructor van de controller. Hier is een voorbeeld van hoe je een service kunt gebruiken in een controller:

```csharp
public class MyController : Controller
{
    private readonly IMyService _myService;

    public MyController(IMyService myService)
    {
        _myService = myService;
    }

    public IActionResult Index()
    {
        var data = _myService.GetData();
        return View(data);
    }
}
```

In dit voorbeeld wordt de `IMyService`-interface geïnjecteerd in de constructor van de `MyController`-klasse. De `GetData`-methode van de service wordt vervolgens aangeroepen in de `Index`-actie van de controller.

## Services Lifetimes
In het ASP.NET Core framework zijn services verantwoordelijk voor het uitvoeren van specifieke taken, zoals authenticatie, autorisatie, caching, enz. Services zijn geregistreerd in de DI-container van de app en kunnen worden geïnjecteerd in andere delen van de app, zoals controllers, middleware, enz.

Het ASP.NET Core framework bevat standaard services die kunnen worden gebruikt in een app, zoals Entity Framework Core, ASP.NET Core Identity, enz. Je kunt ook je eigen services maken en registreren in de DI-container van de app.

Services worden geregistreerd in de `ConfigureServices`-methode van de `Startup`-klasse. Hierbij kun je de levensduur van de service specificeren. Er zijn drie levensduuropties beschikbaar:

1. **Transient**: Er wordt elke keer dat de service wordt aangevraagd een nieuwe instantie van de service gemaakt.
2. **Scoped**: Er wordt één instantie van de service gemaakt voor elke scope. Een scope kan bijvoorbeeld een HTTP-verzoek zijn.
3. **Singleton**: Er wordt één instantie van de service gemaakt voor de hele app.

Het kiezen van de juiste levensduur is belangrijk om ervoor te zorgen dat de service correct werkt en de prestaties van de app niet negatief beïnvloedt. Over het algemeen geldt dat hoe korter de levensduur, hoe beter de prestaties van de app.

Om de levensduur van een service te wijzigen, moet je de methode gebruiken die overeenkomt met de gewenste levensduur. Hier is een voorbeeld van hoe je een service kunt registreren als een singleton:

```csharp
services.AddSingleton<IMyService, MyService>();
```

In dit voorbeeld wordt de `MyService`-klasse geregistreerd als implementatie van de `IMyService`-interface als een singleton. Dit betekent dat er slechts één instantie van de service wordt gemaakt voor de hele app.


## Wanneer moet ik wat gebruiken
Services met een Transient levensduur worden elke keer aangemaakt wanneer ze worden aangevraagd vanuit de servicecontainer. Dit type levensduur is geschikt voor lichtgewicht, stateless services [1](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-7.0)[2](https://mattruma.com/asp-net-core-service-lifetimes-explained/)[3](https://stackoverflow.com/questions/57968893/asp-net-core-2-0-service-life-time).

### Transiant
Je zou Transient-services kunnen gebruiken in de volgende scenario’s:

- Wanneer de service geen toestand (state) bevat en geen gegevens opslaat tussen aanroepen.
- Wanneer de service afhankelijk is van andere services met een Transient levensduur.
- Wanneer de service afhankelijk is van services met een Scoped of Singleton levensduur, maar de service zelf geen toestand bevat.

### Scoped
Services met een Scoped levensduur worden één keer per client request (verbinding) aangemaakt en worden binnen die request opnieuw gebruikt) [1](https://stackoverflow.com/questions/57968893/asp-net-core-2-0-service-life-time).

Je zou Scoped-services kunnen gebruiken in de volgende scenario’s:

- Wanneer de service toestand (state) bevat die specifiek is voor de huidige client request.
- Wanneer de service afhankelijk is van andere services met een Scoped of Singleton levensduur.
- Wanneer de service afhankelijk is van services met een Transient levensduur, maar de service zelf toestand bevat die specifiek is voor de huidige client request.

### Singleton


