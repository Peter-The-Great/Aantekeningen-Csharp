Hierin zal ik opschrijven hoe je een mock kan maken in c# zonder gebruik te maken van Moq:
```cs
public class MyInterfaceMock : IMyInterface
{
    public int GetValue()
    {
        return 5;
    }
}

public class MyClass
{
    private readonly IMyInterface _myInterface;

    public MyClass(MyInterfaceMock myInterface)
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
        var myInterfaceMock = new MyInterfaceMock();

        var myClass = new MyClass(myInterfaceMock);
        var result = myClass.GetDoubleValue();

        Assert.Equal(10, result);
    }
}

```
