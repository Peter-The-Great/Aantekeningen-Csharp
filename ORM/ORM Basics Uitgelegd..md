[[Entity Framework uitgelegd.]]

Een ORM, of Object-Relational Mapping, is een techniek die wordt gebruikt om objecten in een applicatie te koppelen aan tabellen in een relationele database. Het doel van een ORM is om de ontwikkelaar te helpen bij het schrijven van code die toegang heeft tot de database, zonder dat de ontwikkelaar SQL hoeft te schrijven.

Een ORM lost een aantal problemen op, zoals het verminderen van de hoeveelheid code die nodig is om toegang te krijgen tot de database en het verminderen van de kans op fouten in de SQL-code. Het maakt het ook gemakkelijker om de code te onderhouden en te wijzigen, omdat de ontwikkelaar zich minder zorgen hoeft te maken over de details van de database.

Er zijn echter ook enkele problemen waar je tegenaan kunt lopen bij het gebruik van een ORM. Een van de grootste problemen is de prestatie-impact. Omdat een ORM extra code moet uitvoeren om de objecten te koppelen aan de database, kan dit leiden tot een vertraging in de prestaties van de applicatie. Een ander probleem is dat het gebruik van een ORM kan leiden tot een minder efficiënte database-ontwerp, omdat de ontwikkelaar minder aandacht hoeft te besteden aan de details van de database.

Wij gaan zelf Entity Framework gebruiken aangezien dat de makkelijkste:
Entity Framework is een ORM die wordt geleverd met .NET Framework en is ontwikkeld door Microsoft. Het is een van de meest populaire ORM’s voor C# en biedt ondersteuning voor LINQ [1](https://learn.microsoft.com/en-us/ef/)[2](https://learn.microsoft.com/en-us/aspnet/entity-framework).

Entity Framework maakt het gemakkelijk om toegang te krijgen tot een database vanuit een .NET-applicatie. Het biedt een abstractielaag tussen de applicatie en de database, waardoor de ontwikkelaar zich minder zorgen hoeft te maken over de details van de database. Het maakt gebruik van LINQ om query’s te schrijven, wat het gemakkelijk maakt om gegevens uit de database te halen en te manipuleren.

Entity Framework biedt ook ondersteuning voor het maken van databaseschema’s en het uitvoeren van migraties. Dit betekent dat de ontwikkelaar zich minder zorgen hoeft te maken over het handmatig maken van tabellen en kolommen in de database.

# Model Builder

## Seeding Data
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

## Data toevoegen.

Je kunt gegevens toevoegen aan een database met Entity Framework door gebruik te maken van de `DbSet.Add`-methode. Hier is een voorbeeld:

Voorbeeld:
```csharp
using (var context = new MyContext())
{
    var entity = new MyEntity { Name = "John Doe" };
    context.MyEntities.Add(entity);
    context.SaveChanges();
}
```

In dit voorbeeld is `MyContext` de klasse die is afgeleid van `DbContext`. Het bevat een `DbSet`-eigenschap genaamd `MyEntities`, die overeenkomt met een tabel in de database. De `Add`-methode voegt een nieuw object toe aan de database en de `SaveChanges`-methode slaat de wijzigingen op in de database.
## Data Wijzigen
Je kunt gegevens toevoegen aan een database met Entity Framework door gebruik te maken van de `DbSet.Add`-methode. Hier is een voorbeeld:

C#AI-generated code. Review and use carefully. .

```csharp
using (var context = new MyContext())
{
    var entity = new MyEntity { Name = "John Doe" };
    context.MyEntities.Add(entity);
    context.SaveChanges();
}
```

In dit voorbeeld is `MyContext` de klasse die is afgeleid van `DbContext`. Het bevat een `DbSet`-eigenschap genaamd `MyEntities`, die overeenkomt met een tabel in de database. De `Add`-methode voegt een nieuw object toe aan de database en de `SaveChanges`-methode slaat de 
wijzigingen op in de database.

## Data Bijwerken
Je kunt gegevens bijwerken in een database met Entity Framework door gebruik te maken van de `DbSet.Update`-methode. Hier is een voorbeeld:

C#AI-generated code. Review and use carefully. .

```csharp
using (var context = new MyContext())
{
    var entity = new MyEntity { Id = 1, Name = "Jane Doe" };
    context.MyEntities.Update(entity);
    context.SaveChanges();
}
```

In dit voorbeeld is `MyContext` de klasse die is afgeleid van `DbContext`. Het bevat een `DbSet`-eigenschap genaamd `MyEntities`, die overeenkomt met een tabel in de database. De `Update`-methode werkt het object bij in de database en de `SaveChanges`-methode slaat de wijzigingen op in de database.

## Data verwijderen.
Je kunt gegevens verwijderen uit een database met Entity Framework door gebruik te maken van de `DbSet.Remove`-methode. Hier is een voorbeeld:

C#AI-generated code. Review and use carefully. .

```csharp
using (var context = new MyContext())
{
    var entity = new MyEntity { Id = 1 };
    context.MyEntities.Remove(entity);
    context.SaveChanges();
}
```

In dit voorbeeld is `MyContext` de klasse die is afgeleid van `DbContext`. Het bevat een `DbSet`-eigenschap genaamd `MyEntities`, die overeenkomt met een tabel in de database. De `Remove`-methode verwijdert het object uit de database en de `SaveChanges`-methode slaat de wijzigingen op in de database.

Als je meer informatie nodig hebt, raad ik je aan om de officiële documentatie van Microsoft te raadplegen [1](https://stackoverflow.com/questions/8835434/insert-data-using-entity-framework-model)[2](https://learn.microsoft.com/en-us/ef/core/saving/basic). Daar vind je meer informatie over hoe je Entity Framework kunt gebruiken in je project.

## OnModelCreating functie
De `OnModelCreating`-methode wordt aangeroepen wanneer het model voor een afgeleide context is geïnitialiseerd, maar voordat het model is vergrendeld en gebruikt om de context te initialiseren [1](https://learn.microsoft.com/en-us/dotnet/api/system.data.entity.dbcontext.onmodelcreating?view=entity-framework-6.2.0). De `ModelBuilder`-klasse wordt gebruikt om een model voor een context te construeren door `OnModelCreating(ModelBuilder)` in je afgeleide context te overschrijven [2](https://learn.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.modelbuilder?view=efcore-7.0).

De `ModelBuilder`-klasse biedt een manier om het model verder te configureren voordat het wordt vergrendeld. Het biedt een fluent API waarmee je de configuratie van het model kunt aanpassen [3](https://learn.microsoft.com/en-us/ef/core/modeling/). Hier zijn enkele voorbeelden van wat je kunt doen met de `ModelBuilder`-klasse:

- Het toevoegen van entiteiten aan het model.
- Het configureren van de primaire sleutels van entiteiten.
- Het configureren van de eigenschappen van entiteiten.
- Het configureren van relaties tussen entiteiten.
- Het configureren van de namen van tabellen en kolommen in de database.

Hier is een voorbeeld van hoe je de `ModelBuilder`-klasse kunt gebruiken om een entiteit toe te voegen aan het model:

C#AI-generated code. Review and use carefully. .

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<MyEntity>();
}
```

In dit voorbeeld is `MyEntity` de klasse die overeenkomt met een entiteit in de database. De `Entity`-methode van de `ModelBuilder`-klasse wordt gebruikt om de entiteit toe te voegen aan het model.


