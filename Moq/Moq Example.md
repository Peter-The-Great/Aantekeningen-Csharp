[Veder Lezen van Telerik over Moq](https://www.telerik.com/blogs/how-to-simplify-your-csharp-unit-testing-mocking-framework)
Hieronder staat een goed voorbeeld over hoe je een moq kan aanmaken in C#:
```cs
using Moq;

public interface IMyInterface
{
    int GetValue();
}

public class MyClass : IMyInterface
{
    private readonly IMyInterface _myInterface;

    public MyClass(IMyInterface myInterface)
    {
        _myInterface = myInterface;
    }

    public int GetDoubleValue()
    {
        return _myInterface.GetValue() * 2;
    }
}

public class MyTests
{
    [Fact]
    public void TestMyClass()
    {
        var mock = new Mock<IMyInterface>();
        mock.Setup(x => x.GetValue()).Returns(5);

        var myClass = new MyClass(mock.Object);
        var result = myClass.GetDoubleValue();

        Assert.Equal(10, result);
    }
}
```
