# Samenvatting WPFW deel 1
Laatste update: 12-12-2023
Door: William

## C# (D-1) 16%

### Method hiding
Method hiding wordt gebruikt wanneer een afgeleide klasse een methode met dezelfde naam als de basis klasse heeft, maar met het "new" sleutelwoord om aan te geven dat het de bedoeling is om de methode te verbergen. In dit voorbeeld wordt de methode Display in de afgeleide klasse verborgen ten opzichte van de basis klasse.
```csharp
class BaseClass
{
    public void Display()
    {
        Console.WriteLine("Dit is de basis display-methode");
    }
}

class DerivedClass : BaseClass
{
    public new void Display()
    {
        Console.WriteLine("Dit is de afgeleide display-methode");
    }
}
```
### Properties
get en set
```csharp
public class TimePeriod
{
    private double _seconds;

    public double Hours
    {
        get { return _seconds / 3600; }
        set
        {
            if (value < 0 || value > 24)
                throw new ArgumentOutOfRangeException(nameof(value),
                      "The valid range is between 0 and 24.");

            _seconds = value * 3600;
        }
    }
}
```
### Contravariance en covariance
Covariantie (out T) staat toe dat een meer specifiek type wordt gebruikt dan oorspronkelijk gespecificeerd. Contravariantie (in T) staat toe dat een meer algemeen type wordt gebruikt. In de voorbeelden wordt dit gedemonstreerd met interfaces en klassen.
#### Covariantie
Covariantie maakt het mogelijk om een meer specifiek type te gebruiken dan het oorspronkelijk gespecificeerde type. In dit geval wordt het uitvoertype (out T) gebruikt.
```csharp
// Covariantie (out T)
public interface IVariantie<out T>
{
    T GeefWaarde();
}

public class Hoofdklasse
{
    public string Naam { get; set; }
}

public class Subklasse : Hoofdklasse
{
    public int Leeftijd { get; set; }
}

public class CovariantieVoorbeeld
{
    public IVariantie<Hoofdklasse> Methode()
    {
        return new ImplementatieKlasse<Subklasse>();
    }
}

public class ImplementatieKlasse<T> : IVariantie<T>
{
    public T GeefWaarde()
    {
        // Implementatie om een waarde van type T terug te geven
        return default(T);
    }
}
```
#### Contravariantie
Contravariantie maakt het mogelijk om een meer algemeen type te gebruiken dan het oorspronkelijk gespecificeerde type. In dit geval wordt het invoertype (in T) gebruikt.
```csharp
// Contravariantie (in T)
public interface IVariantie<in T>
{
    void NeemWaarde(T waarde);
}

public class Hoofdklasse
{
    public string Naam { get; set; }
}

public class Subklasse : Hoofdklasse
{
    public int Leeftijd { get; set; }
}

public class ContravariantieVoorbeeld
{
    public IVariantie<Subklasse> Methode()
    {
        return new ImplementatieKlasse<Hoofdklasse>();
    }
}

public class ImplementatieKlasse<T> : IVariantie<T>
{
    public void NeemWaarde(T waarde)
    {
        // Implementatie om de ontvangen waarde van type T te verwerken
    }
}
```
### Generic type constraints
Generic type constraints stellen beperkingen aan de types die als argumenten kunnen worden gebruikt. In dit geval is de constraint where T : class, wat betekent dat T een referentietype moet zijn.
```csharp
public class Voorbeeld<T> where T : class
{
    // Implementatie met generic type constraint
}
```
### Object en list initializers
Object initializers bieden syntactic sugar om objecten te initialiseren zonder expliciete constructors te gebruiken. 
List initializers stellen je in staat om collecties te initialiseren.
```csharp
// Object Initializer
var person = new Person { Name = "John", Age = 30 };

// List Initializer
var numbers = new List<int> { 1, 2, 3, 4, 5 };
```

### Operator overloading
Operator overloading stelt je in staat om aangepast gedrag te definiëren voor operatoren zoals +, -, \*, enz. 
*Het voorbeeld toont hoe je de "+"-operator kunt overladen voor de klasse Punt.*
```csharp
public class Punt
{
    public int X { get; set; }
    public int Y { get; set; }

    public static Punt operator +(Punt a, Punt b)
    {
        return new Punt { X = a.X + b.X, Y = a.Y + b.Y }; <- voorbeeld van object initializing
    }
}
```

### Implicit types
Implicit types stellen de compiler in staat om het datatype te bemiddelen op basis van de toegewezen waarde. In het voorbeeld wordt getal als een impliciete int geïnitialiseerd.
```csharp
var getal = 10; // impliciete int
int getal2 = 20; // Explicit int
```

### Extension methods
Extensiemethoden stellen je in staat om nieuwe methoden toe te voegen aan bestaande klassen zonder de klassen zelf te wijzigen. In het voorbeeld wordt een extensiemethode toegevoegd aan de string-klasse.
```csharp
public static class StringExtensions
{
    public static bool IsLang(this string tekst, int lengte) // <- this keyword om aan te geven aan de compiler dat het om een extension method gaat
    {
        return tekst.Length > lengte;
    }
    //var tekts = "Fuckyou";
    //tekts.IsLang(2); 
}
```

### Value en reference types
Dit voorbeeld illustreert het verschil tussen value types (struct) en reference types (class) in C#. De Swap-methode toont hoe je waarden van een value type kunt omwisselen met het gebruik van ref.
```csharp
// Value Type (Struct)
public struct Point
{
    public int X;
    public int Y;
}

// Reference Type (Class)
public class Person
{
    public string Name { get; set; }
}

// Gebruik van ref om waarden van x en y om te wisselen
public static void Swap(ref int a, ref int b)
{
    int temp = a;
    a = b;
    b = temp;
}

public static void Main()
{
    int x = 5;
    int y = 10;

    Console.WriteLine($"Before Swap: x = {x}, y = {y}");

    // Gebruik van ref om waarden van x en y om te wisselen
    Swap(ref x, ref y);

    Console.WriteLine($"After Swap: x = {x}, y = {y}");
}
```

## Testen mocks (D-2) 15%

### Dependency injection
Dependency Injection (DI) is een ontwerppatroon waarbij afhankelijkheden van een klasse van buitenaf worden geïnjecteerd, waardoor de klasse eenvoudiger kan worden getest en onderhouden.
```csharp
public class Service
{
    private readonly IRepository _repository;

    public Service(IRepository repository)
    {
        _repository = repository;
    }
}
```
### Mock class en xunit test (GEEN MOQ)
Het voorbeeld toont het gebruik van een mockklasse (MockRepository) om een interface (IRepository) te implementeren voor testdoeleinden. De xUnit test gebruikt deze mock om een verwacht resultaat te testen.
```csharp
public interface IRepository
{
    string GetData();
}

public class MockRepository : IRepository
{
    public string GetData()
    {
        // Mock-implementatie voor het ophalen van gegevens
        return "Mock Data";
    }
}

public class MijnTestKlasse
{
    [Fact]
    public void TestGetDataFromMockRepository()
    {
        // Arrange
        IRepository repository = new MockRepository();

        // Act
        string resultaat = repository.GetData();

        // Assert
        Assert.Equal("Mock Data", resultaat);
    }

    [Theory]
    [InlineData("Mock Data")]
    //Succes het valt toch.
    [InlineData("Another Mock Data")]
    [InlineData("Yet Another Mock Data")]
    public void TestGetDataFromMockRepositoryWithTheory(string verwachteData)
    {
        // Arrange
        IRepository repository = new MockRepository();

        // Act
        string resultaat = repository.GetData();

        // Assert
        Assert.Equal(verwachteData, resultaat);
    }
}

// Best practices voor testen
// - Commentaar toevoegen aan testmethoden
// - Duidelijke testnamen gebruiken
// - Arrange-Act-Assert (AAA) patroon volgen
// - Mocks gebruiken om externe afhankelijkheden te isoleren
// - etc.
```

### Async en functioneel programmeren (D-1) 15%
Async- en await worden gebruikt om asynchroon mogelijk te maken. Asynchrone code stelt je in staat om taken uit te voeren zonder te wachten tot ze zijn voltooid, waardoor je efficiënter met resources kunt omgaan en de algehele responsiviteit van je applicatie kunt verbeteren. Async maakt parallelle uitvoering van taken mogelijk zonder de hoofdthread te blokkeren, waardoor responsiviteit en efficiëntie verbeteren ten opzichte van synchrone, blokkerende code.

Belangrijk:
- Async methodes worden aangegeven met het async keyword: static async Task<int> BerekenWaardeAsync()
- Het await-sleutelwoord wordt gebruikt binnen een asynchrone methode om te wachten op de voltooiing van een asynchrone taak zonder de thread te blokkeren. Bijvoorbeeld: int resultaat = await BerekenIetsAsync();
- Asynchrone methoden retourneren vaak een Task<TResult> of Task. Task<TResult> wordt gebruikt als de methode een resultaat heeft, anders wordt Task gebruikt. Bijvoorbeeld: Task<int> BerekenIetsAsync()

```cs
class Program
{
    static async Task Main()
    {
        Console.WriteLine("Start programma");

        int resultaat = await BerekenWaardeAsync();

        Console.WriteLine($"Eindresultaat: {resultaat}");
    }

    static async Task<int> BerekenWaardeAsync()
    {
        Console.WriteLine("Begonnen met berekening");

        int waarde1 = await GetValueAsync(10);
        int waarde2 = await GetValueAsync(20);

        int eindresultaat = waarde1 + waarde2;

        Console.WriteLine("Einde berekening");

        return eindresultaat;
    }

    static async Task<int> GetValueAsync(int basisWaarde)
    {
        Console.WriteLine($"Begonnen met het ophalen van waarde voor {basisWaarde}");

        await Task.Delay(1000); // Simuleer een asynchrone taak, bijvoorbeeld een API-oproep

        Console.WriteLine($"Einde ophalen van waarde voor {basisWaarde}");

        return basisWaarde * 2;
    }
}
```
Uitvoer:
- Start programma
- Begonnen met berekening
- Begonnen met het ophalen van waarde voor 10
- Einde ophalen van waarde voor 10
- Begonnen met het ophalen van waarde voor 20
- Einde ophalen van waarde voor 20
- Einde berekening
- Eindresultaat: 60

### ORM & LINQ (D-1) 16%

### LINQ
LINQ (Language Integrated Query) biedt een consistente manier om gegevens te queryen, ongeacht de gegevensbron. Het voorbeeld laat een LINQ-query zien die wordt gebruikt met Entity Framework om personen te filteren en te sorteren.
```csharp
// LINQ query in method syntax
var resultaat = context.Personen
    .Where(p => p.Leeftijd > 18)
    .OrderBy(p => p.Naam)
    .ToList();
```

#### Lazy loading
Lazy loading laadt gerelateerde gegevens alleen wanneer deze voor het eerst worden benaderd. 
```csharp
var author = context.Authors.Single(a => a.Id == 1);
var books = author.Books; // De Books property wordt geaccessed en lazy loading zal automatisch de bijbehorende gegevens laden.
```

#### Explicit loading
Explicit loading laadt gerelateerde gegevens op aanvraag via de Load-methode.
```csharp
var author = context.Authors.Single(a => a.Id == 1);
context.Entry(author).Collection(a => a.Books).Load(); // Hier wordt expliciet de Books property geladen.
```

#### Eager loading
Eager loading laadt gerelateerde gegevens op hetzelfde moment als het hoofdobject.
```csharp
var author = context.Authors.Include(a => a.Books).Single(a => a.Id == 1); // Hier worden de Books tegelijkertijd geladen met de Author.
```


### ORM
Object-Relational Mapping (ORM) is een techniek die objectgeoriënteerde concepten integreert met een relationele database. Het voorbeeld toont een eenvoudige implementatie van een ORM met Entity Framework.
```csharp
// ORM implementatie met Entity Framework
public class DbContext : System.Data.Entity.DbContext
{
    public DbSet<Persoon> Personen { get; set; }
}
```

## Internet (C-1 en C-8) 16%

### Hoe werkt HTTP
HTTP (Hypertext Transfer Protocol) is het protocol dat wordt gebruikt voor communicatie op het wereldwijde web. Het maakt gebruik van een client-servermodel, waarbij een client (bijvoorbeeld een webbrowser) verzoeken indient en een server (bijvoorbeeld een webserver) de verzoeken verwerkt en de bijbehorende reacties retourneert. Hier is een vereenvoudigd voorbeeld van een HTTP-verzoek en -reactie:

**Verzoek (GET)**
```html
GET /index.html HTTP/1.1 <- request
Host: www.example.com <- header
```

**Reactie**
```html
HTTP/1.1 200 OK <- status
Content-Type: text/html  <- header
    
Payload:
<!DOCTYPE html>
<html>
<head>
    <title>Voorbeeldpagina</title>
</head>
<body>
    <h1>Hallo, wereld!</h1>
</body>
</html>
```
**Payload ^**

### XSS (Cross Site Scripting)
XSS is een kwetsbaarheid waarbij aanvallers schadelijke scripts injecteren in webpaginas die vervolgens worden uitgevoerd door de browsers van andere gebruikers. Bijvoorbeeld: 

`<script>alert('Geïnjecteerd XSS-script');</script>`

### CORS (Cross-Origin Resource Sharing)
CORS is een beveiligingsmaatregel die bepaalt welke bronnen een webpagina mag aanroepen vanaf een ander domein. Hier is een voorbeeld van een CORS-koptekst in een HTTP-reactie:

`Access-Control-Allow-Origin: https://vertrouwde-domein.com`

Dit geeft aan dat alleen verzoeken van https://vertrouwde-domein.com zijn toegestaan.

### HTTPS (Hypertext Transfer Protocol Secure)
HTTPS versleutelt de gegevens die worden uitgewisseld tussen een client en een server, waardoor de communicatie veiliger wordt. Het wordt aangegeven in een URL als https:// en vereist het gebruik van een SSL/TLS-certificaat.

### JWT Tokens (JSON Web Tokens)
Een JWT is een compacte, URL-veilige manier om informatie tussen partijen te delen. Het kan worden ondertekend en versleuteld. Hier is een vereenvoudigd JWT-token:

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c`

Een JWT bevat claims (informatie) die door een server kunnen worden gemaakt en door een client kunnen worden geverifieerd.

### DDoS (Distributed Denial of Service)
Een DDoS-aanval is gericht op het overweldigen van een webserver met een grote hoeveelheid verkeer, waardoor de service voor legitieme gebruikers niet beschikbaar wordt. Maatregelen zoals het gebruik van een CDN (Content Delivery Network) kunnen helpen bij het verminderen van het risico op DDoS-aanvallen.

## API (C-1) 15%

### JSON (JavaScript Object Notation)
JSON is een lichtgewicht gegevensindeling die eenvoudig door mensen kan worden gelezen en geschreven, en eenvoudig door machines kan worden verwerkt en gegenereerd. Het heeft de vorm van sleutel-waardeparen en geordende lijsten. Een voorbeeld van JSON:

```json
{
  "naam": "John Doe",
  "leeftijd": 30,
  "isStudent": false,
  "vakken": ["Wiskunde", "Geschiedenis", "Engels"]
}
```

### Postman
Postman is een populaire tool voor het testen van API's. Het biedt een gebruiksvriendelijke interface voor het maken, verzenden en ontvangen van HTTP-verzoeken en -reacties. Met Postman kun je verschillende HTTP-methoden testen, parameters toevoegen, headers instellen en de respons van de server inspecteren.

### Services in ASP.NET Core Framework
ASP.NET Core biedt een krachtig framework voor het bouwen van webapplicaties en services. Enkele belangrijke functies zijn:

#### Routing
Hiermee kun je URL's koppelen aan controlleracties en weergaven in je applicatie.
```csharp
[Route("api/[controller]")]
  [ApiController]
  public class BooksController : ControllerBase
  {
    ...
    [HttpGet]
    public IActionResult GetAll() {  // GET api/Books
      ...
    }
    [HttpHead("{id}")]               // HEAD api/Books/1
    ...
    [HttpGet("{id}")]                // GET api/Books/1
    ...
    [HttpPut("{id}")]                // PUT api/Books/1
    ...
    [HttpPost]                       // POST api/Books
    ...
    [HttpDelete("{id}")]             // DELETE api/Books/1
    ...
    [Route("api/post")]              // POST api/post LET OP, dit hoeft niet een POST te zijn, maar is wel logisch.
    ...
    [Route("api/another")]
    ...
  }
```

#### Model Validation 
Het valideren van ingediende gegevens volgens de gedefinieerde regels in je modellen.
```csharp
// In een modelklasse
public class UserModel
{
    [Required(ErrorMessage = "Naam is verplicht")]
    public string Naam { get; set; }

    [Range(18, 99, ErrorMessage = "Leeftijd moet tussen 18 en 99 liggen")]
    public int Leeftijd { get; set; }
}
```

#### Model Binding
Het proces van het koppelen van HTTP-verzoekgegevens aan actieparameters in je controller.
```csharp
// In een controller
[HttpPost]
public IActionResult Register([FromBody] UserModel userModel)
{
    if (ModelState.IsValid)
    {
        // Doe iets met de geverifieerde gegevens
        return Ok("Gebruiker geregistreerd");
    }
    else
    {
        return BadRequest(ModelState);
    }
}
```
#### Middleware
Een pijplijn van componenten die HTTP-verzoeken en -reacties verwerken. Standaardmiddelen omvatten onder andere routing, authenticatie, en statische bestandsbediening (bv. UseHttpsRedirection)
```csharp
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseAuthorization();

app.MapControllers();

app.MapFallbackToFile("/index.html");
```

Security middleware in ASP.NET Core
```csharp
app.UseHttps();
app.UseCors();
```

## Specflow (D-2) 7%

### Specflow in feature format
    Feature: BMI berekenen
    Scenario: BMI berekenen aan de hand van gewicht, leeftijd en lengte
    	Given ik voer het gewicht 70kg in
    	And ik voer de lengte 175 in
    	And ik voer de leeftijd 25 in
    	When ik druk op de knop Bereken
    	Then print de waarde van mijn bmi op het scherm

### Specflow in step definition
```csharp
[Binding]
public class BMICalculatorSteps
{
    private double _gewicht;
    private double _lengte;
    private int _leeftijd;
    private double _bmiResultaat;

    [Given(@"ik voer het gewicht (.*)kg in")]
    public void GegevenIkVoerHetGewichtInKg(double gewicht)
    {
        _gewicht = gewicht;
    }

    [Given(@"ik voer de lengte (.*) in")]
    public void GegevenIkVoerDeLengteIn(double lengte)
    {
        _lengte = lengte;
    }

    [Given(@"ik voer de leeftijd (.*) in")]
    public void GegevenIkVoerDeLeeftijdIn(int leeftijd)
    {
        _leeftijd = leeftijd;
    }

    [When(@"ik druk op de knop Bereken")]
    public void AlsIkDrukOpDeKnopBereken()
    {
        _bmiResultaat = BerekenBMI(_gewicht, _lengte);
    }

    [Then(@"print de waarde van mijn bmi op het scherm")]
    public void DanPrintDeWaardeVanMijnBmiOpHetScherm()
    {
        Console.WriteLine($"BMI Resultaat: {_bmiResultaat}");
    }

    private double BerekenBMI(double gewicht, double lengte)
    {
        return gewicht / ((lengte / 100) * (lengte / 100));
    }
}
```