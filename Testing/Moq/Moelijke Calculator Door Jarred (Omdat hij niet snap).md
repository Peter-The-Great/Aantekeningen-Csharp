```cs
using System.NUmerics

interface ICalculator
{
	public T Add(T a, T b);
	public T Subtract(T a, T b);
}

struct MockCalculator<T>(uint counter = 0) : ICalculator<T>
{
    public uint Count() => counter += 1;

    public T Add(T a, T b)
    {
        dynamic? c = a;
        return c + b;
    }

    public T Substract(T a, T b)
    {
        dynamic? c = a;
        return c - b;
    }
}

public readonly struct Calculator<T>(ICalculator<T> iCalculator)
where T : INumber<T>
{
    private ICalculator<T> Icalculator { get; } = iCalculator;
    public T Add(T a, T b) => Icalculator.Add(a, b);
    public T Substract(T a, T b) => Icalculator.Substract(a, b);
}

public class TestCalculator
    {
        [Fact]
        public void TestCalculateAdd()
        {
            //Arrange
            var mock = new MockCalculator<uint>();
            var calculator = new Calculator<uint>(mock);

            //Act
            var count = mock.Count();
            var calculate = calculator.Add(7, 23);

            //Assert
            Assert.Equal(1, Convert.ToInt32(count));
            Assert.Equal(30, Convert.ToInt32(calculate));
        }

        [Theory]
        [InlineData(700, 34)]
        public void TestCalculateSubstract(int a, int b)
        {
            //Arrange
            var mock = new MockCalculator<int>();
            var calculator = new Calculator<int>(mock);

            //Act
            var count = mock.Count();
            var calculate = calculator.Substract(a, b);

            //Assert
            Assert.Equal(1, Convert.ToInt32(count));
            Assert.Equal(666, Convert.ToInt32(calculate));
        }
    }
```