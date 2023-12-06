In C# is contravariantie een concept dat het mogelijk maakt om impliciete referentieconversie te gebruiken voor arraytypen, delegaat typen en generieke type argumenten. Covariantie behoudt de compatibiliteit van toewijzingen en contravariantie keert deze om. Hier is een voorbeeld van contravariantie in C#:

```cs
class Animal { }
class Mammal : Animal { }
class Giraffe : Mammal { }

delegate void MyDelegate(Mammal m);

class Program
{
    static void Main(string[] args)
    {
        MyDelegate del = new MyDelegate(Method1);
        del(new Giraffe());
    }

    static void Method1(Animal a)
    {
        Console.WriteLine("Method1(Animal)");
    }
}
```

In dit voorbeeld is `MyDelegate` een delegate type die een enkel argument van het type `Mammal` accepteert. De methode `Method1` accepteert een argument van het type `Animal`. Omdat `Mammal` is afgeleid van `Animal`, is het mogelijk om een ​​instantie van `MyDelegate` te maken die verwijst naar `Method1`. Wanneer de `MyDelegate`-instantie wordt aangeroepen met een argument van het type `Giraffe`, dat is afgeleid van `Mammal`, wordt de `Method1`-methode aangeroepen met het argument van het type `Giraffe`. Dit is een voorbeeld van contravariantie omdat de `Method1`-methode een argument accepteert van een type dat minder is afgeleid dan het type dat `MyDelegate` accepteert.