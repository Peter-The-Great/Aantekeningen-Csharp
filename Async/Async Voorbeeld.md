Hieronder is een voorbeeld van hoe async werkt,
```cs
public static async Task Main()
{
	Task task1 = Bericht1();
	Task task2 = Bericht2();
	//await Bericht1();
	//await Bericht2();
	await Task.WhenAll(task1, task2);
}

public static async Task Bericht1()
{
	Console.WriteLine("In bericht 1");
	await Task.Delay(2000);
	Console.WriteLine("In bericht 1 klaar");
}

public static async Task Bericht2()
{
	Console.WriteLine("In bericht 2");
	await Task.Delay(2000);
	Console.WriteLine("In bericht 2 klaar");
}
```