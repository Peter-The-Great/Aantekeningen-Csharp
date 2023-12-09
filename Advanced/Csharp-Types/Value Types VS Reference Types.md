In C# zijn er twee soorten typen: value types en reference types.

Value types zijn typen die hun waarde opslaan in hun eigen geheugenruimte. Dit betekent dat de variabelen van deze typen de waarden direct bevatten. Voorbeelden van value types zijn `int`, `float`, `bool`, `struct`, en `enum`. Value types worden op de stack opgeslagen.

Reference types zijn typen die een verwijzing naar een object in het geheugen bevatten. Dit betekent dat de variabelen van deze typen een referentie naar de locatie van het object bevatten. Voorbeelden van reference types zijn `string`, `object`, `class`, en `delegate`. Reference types worden op de heap opgeslagen.

Value types worden meestal gebruikt voor eenvoudige gegevensstructuren die klein zijn en weinig overhead hebben. Reference types worden meestal gebruikt voor complexe objecten die groter zijn en meer overhead hebben.

Het belangrijkste verschil tussen value types en reference types is hoe ze worden opgeslagen in het geheugen en hoe ze worden doorgegeven tussen methoden. Value types worden doorgegeven als kopieën, terwijl reference types worden doorgegeven als referenties.

Ik zal hier een voorbeeld geven van Pascal:
```cs
using System;

public class Persoon { public string Naam; }
public struct PersoonStruct { public string Naam; }

public class HelloWorld
{
    public static void Func2(Persoon p)
    {
        p.Naam = "Bob";
    }
    public static void func3(ref PersoonStruct p)
    {
        p.Naam = "Bob";
    }
    public static void func(ref int i)
    {
        i = 3;
    }
    public static void Main(string[] args)
    {
        var j = 2;
        func(ref j);
        Console.WriteLine(j);
        Console.WriteLine();

        Persoon q = new Persoon { Naam = "Alice" };
        Func2(q);
        Console.WriteLine(q.Naam);

        PersoonStruct z = new PersoonStruct { Naam = "Alice" };
        func3(ref z);
        Console.WriteLine(z.Naam);
    }
}
```

Hier zien we drie variabelen, j, q en z. J is een int, een value type. Value types worden overgenomen als kopieën, dus als je graag wilt dat die variabel veranderd en dat ook terug komt in j, moet je ref gebruiken in je methode kijk naar func(). Ik heb hier twee ref keywords gebruikt voor beide input parameters. Hierdoor kun je een parameter referentie houden. Want zonder zou j niet veranderen want alleen binnen in de functie begint de verandering. Test het maar zelf uit.

Persoon wordt bob omdat het een reference type is dus dan houdt de compiler er rekening mee dat je q wilt veranderen en niet alleen p. PersoonStruct is een struct en dat is een value type het werkt hetzelfde als elk ander value type als je via functies verandering wilt brengen in struct moet je ze wel met ref doorgeven.