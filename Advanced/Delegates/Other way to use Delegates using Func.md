Check de: [[Delegates]]
```cs
Console.WriteLine(Shape.square(4));

class Shape
{
	public static Func<int, int> square = x => x * x;
}
```

```cs
using System;
using System.Collections.Generic;
using System.Linq;

public class Func3Example
{
	public static void Main()
	{
		//Check of de string length het zelfde is als het index nummer.
		Func<String, int, bool> predicate = (str, index) => str.Length == index;
		
		String[] words = {"orange", "apple", "Article", "elephant", "star", "and"};
		
		IEnumerable<String> aWords = words.Where(predicate).Select(str => str);
		
		foreach (String word in aWords)
			Console.WriteLine(word);
	
	}
}
```