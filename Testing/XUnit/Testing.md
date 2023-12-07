Hier is een voorbeeld van hoe je unit tests kunt uitvoeren in C# met behulp van xUnit:

Voorbeeld:
```csharp
using System;
using Xunit;

namespace MyNamespace
{
    public class MyTestClass
    {
        [Fact]
        public void MyTestMethod()
        {
            // Arrange
            var expected = 4;
            var a = 2;
            var b = 2;

            // Act
            var actual = a + b;

            // Assert
            Assert.Equal(expected, actual);
        }
    }
}
```

In dit voorbeeld wordt een test uitgevoerd om te controleren of de som van twee getallen correct is. De `[Fact]`-attribuut geeft aan dat de methode een test is. De `Assert.Equal`-methode vergelijkt de verwachte waarde met de werkelijke waarde. Als de waarden niet gelijk zijn, mislukt de test.


## Hieronder zijn ook attributes voor testing in Xunit

In xUnit zijn er twee attributen die worden gebruikt om tests te definiëren: `[Fact]` en `[Theory]`. `[Fact]` wordt gebruikt om een ​​test te definiëren die geen invoerparameters heeft`[Theory]` wordt gebruikt om een ​​parameterized test te definiëren die één of meer `DataAttribute`-instanties verwacht om de waarden voor de methodeargumenten te leveren [1](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-dotnet-test)[2](https://stackoverflow.com/questions/22373258/difference-between-fact-and-theory-xunit-net)[3](https://xunit.net/docs/comparisons). Hierdoor kun je dan makkelijker meerdere instanties testen.

Hier is een voorbeeld van hoe je `[Fact]` kunt gebruiken om een ​​test te definiëren:

Voorbeeld:
```csharp
[Fact]
public void MyTestMethod()
{
    // Arrange
    var expected = 4;
    var a = 2;
    var b = 2;

    // Act
    var actual = a + b;

    // Assert
    Assert.Equal(expected, actual);
}
```

In dit voorbeeld wordt een test uitgevoerd om te controleren of de som van twee getallen correct is. De `[Fact]`-attribuut geeft aan dat de methode een test is. De `Assert.Equal`-methode vergelijkt de verwachte waarde met de werkelijke waarde. Als de waarden niet gelijk zijn, mislukt de test.

Hier is een voorbeeld van hoe je `[Theory]` kunt gebruiken om een ​​parameterized test te definiëren:

Voorbeeld:
```csharp
[Theory]
[InlineData(3, 5, 8)]
[InlineData(2, 4, 6)]
[InlineData(0, 0, 0)]
public void MyTestMethod(int a, int b, int expected)
{
	//Arrange
	//Die wordt al gedaan in de [InlineData] attribute
	
    // Act
    var actual = a + b;

    // Assert
    Assert.Equal(expected, actual);
}
```

In dit voorbeeld wordt een parameterized test uitgevoerd om te controleren of de som van twee getallen correct is. De `[Theory]`-attribuut geeft aan dat de methode een parameterized test is. De `[InlineData]`-attribuut geeft de waarden voor de invoerparameters. De `Assert.Equal`-methode vergelijkt de verwachte waarde met de werkelijke waarde. Als de waarden niet gelijk zijn, mislukt de test.