[[ORM Basics Uitgelegd.]]
Entity Framework is een ORM die wordt geleverd met .NET Framework en is ontwikkeld door Microsoft. Het is een van de meest populaire ORM’s voor C# en biedt ondersteuning voor LINQ [1](https://learn.microsoft.com/en-us/ef/)[2](https://learn.microsoft.com/en-us/aspnet/entity-framework).

Entity Framework maakt het gemakkelijk om toegang te krijgen tot een database vanuit een .NET-applicatie. Het biedt een abstractielaag tussen de applicatie en de database, waardoor de ontwikkelaar zich minder zorgen hoeft te maken over de details van de database. Het maakt gebruik van LINQ om query’s te schrijven, wat het gemakkelijk maakt om gegevens uit de database te halen en te manipuleren.

Entity Framework biedt ook ondersteuning voor het maken van databaseschema’s en het uitvoeren van migraties. Dit betekent dat de ontwikkelaar zich minder zorgen hoeft te maken over het handmatig maken van tabellen en kolommen in de database.

Er zijn verschillende manieren om Entity Framework in je project te gebruiken, maar hier is een eenvoudige manier om te beginnen:

1. Open Visual Studio en maak een nieuw project.
2. Klik met de rechtermuisknop op het project en selecteer “Manage NuGet Packages”.
3. Zoek naar “EntityFramework” en installeer de nieuwste versie.
4. Maak een nieuwe klasse aan die overeenkomt met een tabel in je database.
5. Maak een nieuwe `DbContext`-klasse aan die overeenkomt met je database.
6. Gebruik LINQ-query’s om gegevens uit de database te halen en te manipuleren.

Als je meer informatie nodig hebt, raad ik je aan om de officiële documentatie van Microsoft te raadplegen [1](https://codingsight.com/entity-framework-tutorial-how-to-add-ef-to-your-net-project/). Daar vind je meer informatie over hoe je Entity Framework kunt gebruiken in je project.

Hier is een eenvoudig voorbeeld van hoe je Entity Framework kunt gebruiken in een C#-project:

Voorbeeld:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Entity;

namespace MyProject
{
    public class MyContext : DbContext
    {
        public DbSet<MyEntity> MyEntities { get; set; }
    }

    public class MyEntity
    {
        public int Id { get; set; }
        public string Name { get; set; }
    }

    class Program
    {
        static void Main(string[] args)
        {
            using (var context = new MyContext())
            {
                var entity = new MyEntity { Name = "John Doe" };
                context.MyEntities.Add(entity);
                context.SaveChanges();
                
                var query = context.MyEntities.Where(e => e.Name == "John Doe");

                foreach (var item in query)
                {
                    Console.WriteLine(item.Name);
                }
            }
        }
    }
}
```

Dit voorbeeld bevat een `DbContext`-klasse genaamd `MyContext`, die overeenkomt met een database. Het bevat ook een `MyEntity`-klasse die overeenkomt met een tabel in de database. De `Main`-methode maakt een nieuwe instantie van `MyContext` aan, voegt een nieuw object toe aan de database, haalt het object op uit de database en geeft de naam van het object weer in de console.

`DbContext` is een klasse in Entity Framework die fungeert als een brug tussen de objecten in je applicatie en de tabellen in de database. Het biedt een abstractielaag tussen de applicatie en de database, waardoor de ontwikkelaar zich minder zorgen hoeft te maken over de details van de database) [1](https://learn.microsoft.com/en-us/ef/ef6/fundamentals/working-with-dbcontext).

`DbContext` is verantwoordelijk voor het bijhouden van de wijzigingen die zijn aangebracht in de objecten in de applicatie en deze wijzigingen door te voeren in de database. Het biedt ook ondersteuning voor het maken van databaseschema’s en het uitvoeren van migraties [1](https://learn.microsoft.com/en-us/ef/ef6/fundamentals/working-with-dbcontext).

Om `DbContext` te gebruiken, moet je een klasse maken die hiervan afgeleid is en die overeenkomt met je database. Deze klasse moet de `DbSet`-eigenschappen bevatten die overeenkomen met de tabellen in de database [1](https://learn.microsoft.com/en-us/ef/ef6/fundamentals/working-with-dbcontext). Hier is een voorbeeld:

Voorbeeld:

```csharp
public class MyContext : DbContext
{
    public DbSet<MyEntity> MyEntities { get; set; }
}
```

In dit voorbeeld is `MyContext` de klasse die is afgeleid van `DbContext`. Het bevat een `DbSet`-eigenschap genaamd `MyEntities`, die overeenkomt met een tabel in de database.

Je kunt een database migratie uitvoeren met Entity Framework door de volgende stappen te volgen:

1. Open de **Package Manager Console** in Visual Studio.
2. Voer het commando `Add-Migration MigrationName` uit, waarbij `MigrationName` de naam is die je wilt geven aan de migratie. Dit commando genereert een nieuwe migratieklasse in je project.
3. Voer het commando `Update-Database` uit om de migratie toe te passen op de database. Dit commando past de wijzigingen toe die zijn beschreven in de migratieklasse op de database.

Als je meer informatie nodig hebt, raad ik je aan om de officiële documentatie van Microsoft te raadplegen [1](https://learn.microsoft.com/en-us/ef/core/managing-schemas/migrations/). Daar vind je meer informatie over hoe je Entity Framework kunt gebruiken in je project.

Je kunt een database seeden met Entity Framework door gebruik te maken van de **Data Seeding**-functionaliteit. Data seeding is het proces van het initialiseren van een database met een initiële set gegevens. Er zijn verschillende manieren om dit te doen in Entity Framework, maar de meest gebruikelijke manier is om gebruik te maken van model seed data [1](https://learn.microsoft.com/en-us/ef/core/modeling/data-seeding).

Model seed data is een manier om gegevens te initialiseren in een database die wordt gemaakt door Code First of geëvolueerd door Migrations. Dit kan testdata zijn, maar kan ook referentiedata zijn zoals lijsten van bekende studenten, cursussen, enzovoort [2](https://www.tutorialspoint.com/entity_framework/entity_framework_seed_database.htm).

Om model seed data te gebruiken, moet je een klasse maken die overeenkomt met een entiteitstype als onderdeel van de modelconfiguratie. Vervolgens kunnen EF Core-migraties automatisch berekenen welke invoeg-, update- of verwijderingsbewerkingen moeten worden toegepast bij het upgraden van de database naar een nieuwe versie van het model [1](https://learn.microsoft.com/en-us/ef/core/modeling/data-seeding).

Hier is een voorbeeld van hoe je model seed data kunt configureren voor een `Blog`-entiteit:

Voorbeeld:

```csharp
modelBuilder.Entity<Blog>().HasData(
    new Blog { BlogId = 1, Url = "http://sample.com" }
);
```

Als je meer informatie nodig hebt, raad ik je aan om de officiële documentatie van Microsoft te raadplegen [1](https://learn.microsoft.com/en-us/ef/core/modeling/data-seeding). Daar vind je meer informatie over hoe je Entity Framework kunt gebruiken in je project.

