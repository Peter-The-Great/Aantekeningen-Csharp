Hierin zal ik opschrijven hoe je een mock kan maken in c# zonder gebruik te maken van Moq:
```cs
//Hier Kun je iets hebben zoals een iinterface of class
interface IMyInterface
{
	int GetValue();
}

//Dit is je mock die dan de functies implementeerd van de Interface en class.
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
	    //return 5 * 2; (10)
        return _myInterface.GetValue() * 2;
    }
}

public class MyTests
{
    [Fact]
    public void TestMyClass()
    {
	    //Arrange
        var myInterfaceMock = new MyInterfaceMock();
        var myClass = new MyClass(myInterfaceMock);
        
        //Act
        var result = myClass.GetDoubleValue();
		
		//Assert
        Assert.Equal(10, result);
    }
}

```
