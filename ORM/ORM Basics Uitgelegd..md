[[Entity Framework uitgelegd.]]

Een ORM, of Object-Relational Mapping, is een techniek die wordt gebruikt om objecten in een applicatie te koppelen aan tabellen in een relationele database. Het doel van een ORM is om de ontwikkelaar te helpen bij het schrijven van code die toegang heeft tot de database, zonder dat de ontwikkelaar SQL hoeft te schrijven.

Een ORM lost een aantal problemen op, zoals het verminderen van de hoeveelheid code die nodig is om toegang te krijgen tot de database en het verminderen van de kans op fouten in de SQL-code. Het maakt het ook gemakkelijker om de code te onderhouden en te wijzigen, omdat de ontwikkelaar zich minder zorgen hoeft te maken over de details van de database.

Er zijn echter ook enkele problemen waar je tegenaan kunt lopen bij het gebruik van een ORM. Een van de grootste problemen is de prestatie-impact. Omdat een ORM extra code moet uitvoeren om de objecten te koppelen aan de database, kan dit leiden tot een vertraging in de prestaties van de applicatie. Een ander probleem is dat het gebruik van een ORM kan leiden tot een minder efficiënte database-ontwerp, omdat de ontwikkelaar minder aandacht hoeft te besteden aan de details van de database.

Wij gaan zelf Entity Framework gebruiken aangezien dat de makkelijkste:
Entity Framework is een ORM die wordt geleverd met .NET Framework en is ontwikkeld door Microsoft. Het is een van de meest populaire ORM’s voor C# en biedt ondersteuning voor LINQ [1](https://learn.microsoft.com/en-us/ef/)[2](https://learn.microsoft.com/en-us/aspnet/entity-framework).

Entity Framework maakt het gemakkelijk om toegang te krijgen tot een database vanuit een .NET-applicatie. Het biedt een abstractielaag tussen de applicatie en de database, waardoor de ontwikkelaar zich minder zorgen hoeft te maken over de details van de database. Het maakt gebruik van LINQ om query’s te schrijven, wat het gemakkelijk maakt om gegevens uit de database te halen en te manipuleren.

Entity Framework biedt ook ondersteuning voor het maken van databaseschema’s en het uitvoeren van migraties. Dit betekent dat de ontwikkelaar zich minder zorgen hoeft te maken over het handmatig maken van tabellen en kolommen in de database.

