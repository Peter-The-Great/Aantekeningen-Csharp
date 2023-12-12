# Niet belangrijk voor de toets dacht is leuk
De null-coalescing operators, `??` genoemd in C#, bieden een manier om met nullwaarden om te gaan door een standaardwaarde te specificeren die moet worden gebruikt als een uitdrukking null is.

### Null-coalescing operator `??`

De null-coalescing operator `??` wordt gebruikt om te bepalen of een expressie null is. Als de expressie niet null is, retourneert de operator die waarde. Als de expressie null is, retourneert de operator een standaardwaarde die je opgeeft aan de rechterkant van `??`.

#### Syntax:

csharpCopy code

`result = expression1 ?? expression2;`

- `expression1`: De uitdrukking waarvan je wilt controleren of deze null is.
- `expression2`: De waarde die wordt geretourneerd als `expression1` null is.

#### Voorbeeld:

csharpCopy code

`int? nullableValue = null; int result = nullableValue ?? 10; // Als nullableValue null is, wordt 10 gebruikt als standaardwaarde voor result.`

### Null-conditional operator `?.`

De null-conditional operator `?.` wordt gebruikt om te voorkomen dat er een `NullReferenceException` optreedt als de aanroepketen null bevat. Het stopt de evaluatie en retourneert null zodra een deel van de aanroepketen null is, in plaats van de rest van de aanroepketen te blijven evalueren.

#### Syntax:

csharpCopy code

`memberAccess = expression?.member;`

- `expression`: De uitdrukking waarop je een methode of een eigenschap wilt aanroepen.
- `member`: De methode of eigenschap die je wilt aanroepen.

#### Voorbeeld:

csharpCopy code

`string str = null; int length = str?.Length; // Als str null is, wordt length automatisch null.`

### Gecombineerd gebruik:

csharpCopy code

`var result = someNullableValue ?? fallbackValue; var length = someString?.Length ?? 0;`

Door deze operatoren te combineren, kun je soepel omgaan met scenario's waarin waarden mogelijk null kunnen zijn, en je kunt standaardwaarden opgeven om mee te werken als dat nodig is.

Mijn voorbeeld:
```cs
double SumNumbers(List<double[]> setsOfNumbers, int indexOfSetToSum)
{
return setsOfNumbers?[indexOfSetToSum]?.Sum() ?? double.NaN;
}

var help = new List<double[]>{ new double[] {1.5} };
var sum = SumNumbers(help, 0);
var sum2 = SumNumbers(null, 0);

Console.WriteLine(sum); // output: 1.5 of NaN als het null was.
Console.WriteLine(sum2); //Zoals hier
```

Help is ook een List Initializer  --> [[Object en List Initializer]]
