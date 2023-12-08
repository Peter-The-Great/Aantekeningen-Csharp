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

	public T Add()
	{
		dynamic? c = a;
		return b + c;
	}
}
```