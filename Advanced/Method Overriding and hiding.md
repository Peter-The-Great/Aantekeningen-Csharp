In C# zijn method overriding en method hiding twee manieren om methoden te overschrijven in afgeleide klassen.

Method overriding is het proces waarbij een afgeleide klasse een methode van de basis klasse overschrijft met een nieuwe implementatie. Dit betekent dat als we een methode in de afgeleide klasse definiëren met dezelfde naam, parameters en retourtype als de methode in de basis klasse, de methode in de afgeleide klasse de methode in de basis klasse overschrijft. Hier is een voorbeeld:

```csharp
class Animal {
    public virtual void MakeSound() {
        Console.WriteLine("The animal makes a sound");
    }
}

class Dog : Animal {
    public override void MakeSound() {
        Console.WriteLine("The dog barks");
    }
}
```

In dit voorbeeld hebben we een `Animal` klasse met een `MakeSound` methode die een bericht naar de console schrijft. We hebben ook een `Dog` klasse die is afgeleid van de `Animal` klasse en een `MakeSound` methode heeft die de `MakeSound` methode van de `Animal` klasse overschrijft. Wanneer we een `Dog` object maken en de `MakeSound` methode aanroepen, wordt de `MakeSound` methode van de `Dog` klasse uitgevoerd.

```csharp
Animal dier = new Dog();
dier.MakeSound();

// The dog Barks
```

Method hiding is het proces waarbij een afgeleide klasse een methode van de basis klasse verbergt met een nieuwe implementatie. Dit betekent dat als we een methode in de afgeleide klasse definiëren met dezelfde naam als de methode in de basis klasse, de methode in de afgeleide klasse de methode in de basis klasse verbergt. Hier is een voorbeeld:

```csharp
class Animal {
    public void MakeSound() {
        Console.WriteLine("The animal makes a sound");
    }
}

class Dog : Animal {
    public new void MakeSound() {
        Console.WriteLine("The dog barks");
    }
}
```

```csharp
Animal dier = new Dog();
dier.MakeSound();

// The animal makes a sound
```

In dit voorbeeld hebben we een `Animal` klasse met een `MakeSound` methode die een bericht naar de console schrijft. We hebben ook een `Dog` klasse die is afgeleid van de `Animal` klasse en een `MakeSound` methode heeft die de `MakeSound` methode van de `Animal` klasse verbergt. Wanneer we een `Dog` object maken en de `MakeSound` methode aanroepen, wordt de `MakeSound` methode van de `Dog` klasse uitgevoerd, zelfs als het object wordt gecast naar de `Animal` klasse.