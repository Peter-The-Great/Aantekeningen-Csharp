In C# is `lock` een synchronisatiemechanisme dat wordt gebruikt om toegang tot gedeelde bronnen te synchroniseren en race-voorwaarden te voorkomen. Het `lock`-statement zorgt ervoor dat slechts één thread tegelijkertijd toegang heeft tot de gedeelde bron. Wanneer een thread een `lock`-statement tegenkomt, probeert deze de exclusieve toegang tot de gedeelde bron te verkrijgen. Als de gedeelde bron al door een andere thread wordt gebruikt, wacht de huidige thread tot de andere thread de `lock`-verklaring vrijgeeft [1](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/lock).

Hier is een voorbeeld van hoe u `lock` in C# kunt gebruiken:

C#Door AI gegenereerde code. Controleer en gebruik zorgvuldig. .

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        var account = new Account(1000);

        // Start 100 threads to update the account balance
        var tasks = new Task[100];
        for (int i = 0; i < tasks.Length; i++)
        {
            tasks[i] = Task.Run(() => Update(account));
        }

        // Wait for all threads to complete
        Task.WaitAll(tasks);

        Console.WriteLine($"Account balance is {account.GetBalance()}");
    }

    public static void Update(Account account)
    {
        decimal[] amounts = { 0, 2, -3, 6, -2, -1, 8, -5, 11, -6 };

        foreach (var amount in amounts)
        {
            if (amount >= 0)
            {
                account.Credit(amount);
            }
            else
            {
                account.Debit(Math.Abs(amount));
            }
        }
    }
}

public class Account
{
    private readonly object balanceLock = new object();
    private decimal balance;

    public Account(decimal initialBalance)
    {
        balance = initialBalance;
    }

    public decimal Debit(decimal amount)
    {
        if (amount < 0)
        {
            throw new ArgumentOutOfRangeException(nameof(amount), "Debit amount cannot be negative.");
        }

        decimal appliedAmount = 0;

        lock (balanceLock)
        {
            if (balance >= amount)
            {
                balance -= amount;
                appliedAmount = amount;
            }
        }

        return appliedAmount;
    }

    public void Credit(decimal amount)
    {
        if (amount < 0)
        {
            throw new ArgumentOutOfRangeException(nameof(amount), "Credit amount cannot be negative.");
        }

        lock (balanceLock)
        {
            balance += amount;
        }
    }

    public decimal GetBalance()
    {
        lock (balanceLock)
        {
            return balance;
        }
    }
}
```

In dit voorbeeld wordt de `Account`-klasse gebruikt om toegang te synchroniseren tot de `balance`-veld van de klasse. De `Debit`- en `Credit`-methoden zijn beide beveiligd met een `lock`-verklaring om ervoor te zorgen dat slechts één thread tegelijkertijd toegang heeft tot de `balance`-veld. De `Update`-methode start 100 threads om de `Account`-balans bij te werken. Omdat de `Debit`- en `Credit`-methoden zijn beveiligd met een `lock`-verklaring, worden race-voorwaarden voorkomen en wordt de integriteit van de `balance`-veld gehandhaafd.

Meer informatie:
[1. learn.microsoft.com](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/lock "lock statement - synchronize thread access to a shared resource - C# ...")[2. stackoverflow.com](https://stackoverflow.com/questions/6029804/what-does-a-lock-statement-do-under-the-hood "c# - What does a lock statement do under the hood? - Stack Overflow")[3. dotnettutorials.net](https://dotnettutorials.net/lesson/interlocked-vs-lock-in-csharp/ "Interlocked vs Lock in C# with Examples - Dot Net Tutorials")[4. stackove](https://stackoverflow.com/questions/11788582/best-practices-in-using-a-lock "c# - Best Practices in using a lock - Stack Overflow")[5. rocksolidknowledge](https://www.rocksolidknowledge.com/articles/locking-and-asyncawait)[6. cdemi](https://blog.cdemi.io/async-waiting-inside-c-sharp-locks/)
