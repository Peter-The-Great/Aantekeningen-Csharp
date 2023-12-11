Er zijn drie manieren om gegevens in LINQ te laden: **Lazy Loading**, **Eager Loading** en **Explicit Loading** [1](https://www.c-sharpcorner.com/article/lazy-loading-and-eager-loading-in-linq-to-sql/)[2](https://learn.microsoft.com/en-us/ef/core/querying/related-data/)[3](https://stackoverflow.com/questions/13011808/does-linq-load-all-items-from-sql-server-into-memory-or-chunks-only) [4 (Mijn Microsoft Docs)](https://learn.microsoft.com/en-us/ef/ef6/querying/related-data) [5 TutorialTeacher](https://www.entityframeworktutorial.net/entityframework6/lazyloading-in-entity-framework.aspx).

**Lazy Loading** betekent dat gerelateerde gegevens niet worden geladen totdat we er doorheen itereren of ze aan de gegevens binden [1](https://www.c-sharpcorner.com/article/lazy-loading-and-eager-loading-in-linq-to-sql/). Standaard laadt LINQ to SQL de gerelateerde entiteiten met behulp van Lazy Loading [1](https://www.c-sharpcorner.com/article/lazy-loading-and-eager-loading-in-linq-to-sql/). Er is een één-op-veel relatie tussen de entiteiten Afdelingen en Werknemers. Een afdeling kan één of meer werknemers hebben. Wanneer de afdelingen worden geladen, worden de gerelateerde entiteiten (werknemersentiteiten) niet geladen. Werknemersentiteiten worden alleen geladen wanneer we door de objecten van een bepaalde afdeling itereren [1](https://www.c-sharpcorner.com/article/lazy-loading-and-eager-loading-in-linq-to-sql/).

Voorbeeld:
```cs
using (var ctx = new SchoolDBEntities())
{
    //Loading students only
    IList<Student> studList = ctx.Students.ToList<Student>();

    Student std = studList[0];

    //Loads Student address for particular Student only (seperate SQL query)
    StudentAddress add = std.StudentAddress;
}
```

**Eager Loading** betekent dat gerelateerde gegevens worden geladen vanuit de database als onderdeel van de initiële query [2](https://learn.microsoft.com/en-us/ef/core/querying/related-data/). Dit kan worden bereikt door de `Include`-methode te gebruiken [2](https://learn.microsoft.com/en-us/ef/core/querying/related-data/). Hier is een voorbeeld van hoe u de `Include`-methode kunt gebruiken om gerelateerde gegevens te laden:

Voorbeeld:
```csharp
var query = context.Customers.Include("Orders").Select(c => c);
```

Dit laadt alle klanten en hun bijbehorende bestellingen in één query [2](https://learn.microsoft.com/en-us/ef/core/querying/related-data/).

**Explicit Loading** betekent dat gerelateerde gegevens expliciet worden geladen vanuit de database op een later tijdstip [3](https://stackoverflow.com/questions/13011808/does-linq-load-all-items-from-sql-server-into-memory-or-chunks-only). Dit kan worden bereikt door de `Load`-methode te gebruiken [3](https://stackoverflow.com/questions/13011808/does-linq-load-all-items-from-sql-server-into-memory-or-chunks-only). Hier is een voorbeeld van hoe u de `Load`-methode kunt gebruiken om gerelateerde gegevens te laden:

Voorbeeld:
```csharp
var customer = context.Customers.Find(1);
context.Entry(customer).Collection(c => c.Orders).Load();
```

Dit laadt alle bestellingen voor de klant met ID 1 [3](https://stackoverflow.com/questions/13011808/does-linq-load-all-items-from-sql-server-into-memory-or-chunks-only).

# Lazy Loading Voorbeeld

```cs
using (var ctx = new SchoolDBEntities())
{
    //Loading students only
    IList<Student> studList = ctx.Students.ToList<Student>();

    Student std = studList[0];

    //Loads Student address for particular Student only (seperate SQL query)
    StudentAddress add = std.StudentAddress;
}
```
# Explicit Loading Voorbeeld

```cs
using (var context = new SchoolContext())
{
    var student = context.Students
                        .Where(s => s.FirstName == "Bill")
                        .FirstOrDefault<Student>();

    context.Entry(student).Reference(s => s.StudentAddress).Load(); // loads StudentAddress
    context.Entry(student).Collection(s => s.StudentCourses).Load(); // loads Courses collection 
}
```
# Eager Loading Voorbeeld

```cs
using (var ctx = new SchoolDBEntities())
{
    var stud1 = ctx.Students
                   .Include("Standard")
                   .Where(s => s.StudentName == "Bill")
                   .FirstOrDefault<Student>();
}
```
