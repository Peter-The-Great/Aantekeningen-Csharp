Dependency Injection (DI) en Dependency Inversion (DI) zijn twee ontwerppatronen die in de softwareontwikkeling worden gebruikt om de afhankelijkheden tussen objecten te verminderen en de code flexibeler te maken.

**Dependency Injection** is een techniek waarbij objecten (‘afhankelijkheden’) aan een klasse worden geleverd door middel van het Dependency Injection-ontwerppatroon. Dit kan typisch door afhankelijkheden via een van de volgende manieren door te geven:

- Een constructor
- Een openbare eigenschap of veld
- Een openbare setter

**Dependency Inversion** is een softwareontwerprichtlijn die neerkomt op twee aanbevelingen over het loskoppelen van een klasse van zijn concrete afhankelijkheden:

- ‘Modules op hoog niveau mogen niet afhankelijk zijn van modules op laag niveau. Beide moeten afhankelijk zijn van abstracties.’
- ‘Abstracties mogen niet afhankelijk zijn van details. Details moeten afhankelijk zijn van abstracties.’

Het belangrijkste verschil tussen DI en DI is dat DI een techniek is die wordt gebruikt om afhankelijkheden te leveren, terwijl DI een richtlijn is die wordt gebruikt om de afhankelijkheden van een klasse te ontwerpen.

**Dependency Injection (DI)**

Laten we zeggen dat we een klasse hebben genaamd `Car` die afhankelijk is van een klasse genaamd `Engine`. In plaats van de `Engine`-klasse rechtstreeks in de `Car`-klasse te instantiëren, kunnen we de `Engine`-klasse via de constructor aan de `Car`-klasse leveren. Dit is een voorbeeld van DI.

C#:

```csharp
public class Engine
{
    public Engine()
    {
    }
}

public class Car
{
    private Engine engine;

    public Car(Engine engine)
    {
        this.engine = engine;
    }
}
```

**Dependency Inversion (DI)**

Laten we zeggen dat we een klasse hebben genaamd `Car` die afhankelijk is van een klasse genaamd `Engine`. In plaats van de `Car`-klasse rechtstreeks afhankelijk te maken van de `Engine`-klasse, kunnen we een abstractie maken van de `Engine`-klasse en de `Car`-klasse afhankelijk maken van de abstractie. Dit is een voorbeeld van DI.

C#

```csharp
public interface IEngine
{
    void Start();
}

public class GasolineEngine : IEngine
{
    public void Start()
    {
        Console.WriteLine("Starting gasoline engine");
    }
}

public class ElectricEngine : IEngine
{
    public void Start()
    {
        Console.WriteLine("Starting electric engine");
    }
}

public class Car
{
    private IEngine engine;

    public Car(IEngine engine)
    {
        this.engine = engine;
    }

    public void Start()
    {
        engine.Start();
    }
}
```
