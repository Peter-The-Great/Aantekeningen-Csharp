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


Nog een goed voorbeeld om te testen tussen await en niet await. Dan functioneerd het wel nog als async:

```cs
class Program
{
    static async Task Main(string[] args)
    {
    //Deze methode's awaiten niet maar gaan wel ondertussen door.
        Method1();
        Method2();
        Console.ReadKey();
    }

    public static async Task Method1()
    {
        await Task.Run(() =>
        {
            for (int i = 0; i < 100; i++)
            {
                Console.WriteLine(" Method 1");
                // Do something
                Task.Delay(100).Wait();
            }
        });
    }


    public static void Method2()
    {
        for (int i = 0; i < 25; i++)
        {
            Console.WriteLine(" Method 2");
            // Do something
            Task.Delay(100).Wait();
        }
    }
}
```

Nog een Voorbeeld:
```cs
using System;
using System.Threading.Tasks;
class Program
 {
   static async Task Main(string[] args)
   {
     await callMethod();
     Console.WriteLine("End");
   }

   public static async Task callMethod()
   {
     Method2();
     var count = await Method1();
     Method3(count);
   }

   public static async Task<int> Method1()
   {
     int count = 0;
     await Task.Run(() =>
     {
       for (int i = 0; i < 100; i++)
       {
         Console.WriteLine(" Method 1");
         count += 1;
       }
     });
     return count;
   }

   public static void Method2()
   {
     for (int i = 0; i < 25; i++)
     {
       Console.WriteLine(" Method 2");
     }
   }

   public static void Method3(int count)
   {
     Console.WriteLine("Total count is " + count);
   }
}
```

Meer leren:
[Microsoft Docs](https://learn.microsoft.com/en-us/dotnet/csharp/asynchronous-programming/task-asynchronous-programming-model)
[c-sharpcorner](https://www.c-sharpcorner.com/article/async-and-await-in-c-sharp/)
