Bronnen:
[DotNET-ORM](https://softchris.github.io/pages/dotnet-orm.html#install-and-set-up-2)
[NET Basics: ORM (Object Relational Mapping)](https://www.telerik.com/blogs/dotnet-basics-orm-object-relational-mapping)
[Understanding Object-Relational Mapping: Pros, Cons, and Types](https://www.altexsoft.com/blog/object-relational-mapping/)
[ORM-C#](https://www.javatpoint.com/orm-c-sharp)
# How YOU can use an ORM in .NET Core and C# to type less SQL -starring Entity Framework

Follow me on [Twitter](https://twitter.com/chris_noring), happy to take your suggestions on topics or improvements /Chris

![](https://thepracticaldev.s3.amazonaws.com/i/senihoqu8bizs8oepx82.jpg)

> We all love SQL right? No? Well sometimes a good SQL query is the best approach but most of the time it's the same CRUD operations that you need to carry out, Create, Read, Update, Delete, on each new entity. With an ORM, an Object Relational Mapper, you are able to define what the structure in your database should look like, using code. Additionally, you can use code for your queries as well. The main ORM for .Net and .Net Core is called Entity Framework and that's what we are covering in this article.

I just wanted to say a very important thing. A tool like an ORM should NEVER replace learning SQL. An ORM is there to make your life easier so when you end up writing SQL it's for the important things like a reporting query or a query that needs to be really performant. The idea is for the ORM to take care of simpler SQL like creating tables and doing simple inserts. If you use this without a decent knowledge of SQL then please have a look here and try grasp the basics first:

> https://www.w3schools.com/sql/

TLDR; This article is somewhat lengthy but it starts from the beginning to teach you Entity Framework and covers a lot of really great topics, worth the read.

In this article we will cover:

- **WHY an ORM**, we always need to ask ourselves why we use something. ORM can really shine if you have a lot of simple interaction to a database. You can really speed up your operation using it.
- **WHAT** it can help you with.
- **Install** and Set up
- A CRUD Demo. We will go through reading data, creating, updating and deleting data

## [#](https://softchris.github.io/pages/dotnet-orm.html#resources)Resources

- [Database providers](https://docs.microsoft.com/en-us/ef/core/providers/?wt.mc_id=academic-0000-chnoring) You can work with quite a number of different databases using Entity Framework. The whole idea is to have an agnostic approach so you, in theory, could replace one database for another and your code remains the same. We all know we almost never do that but it's a nice idea.
    
- [Beginner EF Core article](https://docs.microsoft.com/en-us/ef/core/get-started/netcore/new-db-sqlite?wt.mc_id=academic-0000-chnoring) This article is partly based on this one even if we take it a step further
    
- [Using EF Core in ASP .Net MVC](https://docs.microsoft.com/en-us/aspnet/core/data/ef-mvc/intro?view=aspnetcore-2.2&wt.mc_id=academic-0000-chnoring)
    
- [Eager loading](https://docs.microsoft.com/en-us/ef/core/querying/related-data?wt.mc_id=academic-0000-chnoring) We cover the basics of how this works in the article but there is always more to learn.
    
- [Basics of Querying](https://docs.microsoft.com/en-us/ef/core/querying/basic?wt.mc_id=academic-0000-chnoring)
    
- [Overview page on everything EF Core](https://docs.microsoft.com/en-us/ef/core/?wt.mc_id=academic-0000-chnoring)
    

## [#](https://softchris.github.io/pages/dotnet-orm.html#why-orm)Why ORM

Using an ORM is about beeing faster, more productive and about knowing exactly what goes into a database.

> So when do I use it, always or?

Well for most simple applications it's definitely good to use. For applications that need really performant queries you can definitely still use it but you need to be more observant on what SQL your ORM produces. Sometimes it's good enough and sometimes you need to write those queries by hand using SQL. Typically reporting queries is something I personally don't use ORMs for as they tend to be complex and hard to express in code. But everyone is different. I've seen even complex queries being authored in code.

### [#](https://softchris.github.io/pages/dotnet-orm.html#the-orm-landscape)The ORM landscape

There is more than one ORM choice for .Net. Entity Framework is the most known one but there are other ones. You have to decide which one fits your project.

- [Linq 2 db](https://github.com/linq2db/linq2db) Offers a similar experience to Entity Framework if you look at the syntax alone. Some say the syntax is close to what you get in actual SQL
    
- [Dapper](https://dapper-tutorial.net/) It has been descriptions like _Object Mapper_ and _Micro ORM_
    
- [NHibernate](https://nhibernate.info/) .Net port of Hibernate. One of the oldest ORMs out there.
    

There are more ORMs out there but the three above are well-known choices.

## [#](https://softchris.github.io/pages/dotnet-orm.html#what)What

Most ORMs lets you define the table structure in code and you can map a class so that it corresponds to a table. The columns are simply properties on the class. Depending on the ORM several approaches are possible

- **Schema first**, in this scenario you define a schema of what tables you have, how they relate like 1-1, 1-Many, Man-to-Many and so on. You end up generating code from the schema.
- **Code first**, In this approach, you define the code first. Every table corresponds to a class and you can express how everything relates in code. Your ORM will then take a look at your code and generate structural SQL from it.

### [#](https://softchris.github.io/pages/dotnet-orm.html#migrations)Migrations

A lot of ORMs comes with a concept called _migrations_. A migration is simply a piece of script that either alters the structure of the database or runs a piece of SQL that affects the data like for example _seeding_ the database with some initial data. The idea is that every time you do a change of the database that should be a small transactional change captured in a migration. That migration can then be _applied_ to the database and thereby the database will be altered in the desired way. For example, adding a Customer table to database would be a migration that when applied would create the table in the Database. A Migration can either be expressed as SQL or in Code.

## [#](https://softchris.github.io/pages/dotnet-orm.html#install-and-set-up)Install and Set up

To get started with Entity Framework we need a couple of NuGet packages but also a project that we can install the NuGet packages to. So for this exercise, we will do the following:

1. **Create** a solution
2. **Scaffold** a Console project and add a reference to the solution
3. **Install** the needed NuGet packages to the Console project

### [#](https://softchris.github.io/pages/dotnet-orm.html#create-a-solution)Create a solution

This is quite simply done. First, we need a directory. So create a directory, you can choose the name yourself but here is an example.

```
mkdir demo
```

1  

Then we need to place ourselves in the directory like so:

```
cd demo
```

1  

### [#](https://softchris.github.io/pages/dotnet-orm.html#scaffold-a-console-project)Scaffold a Console project

Next up we need to create our Console project. Again you can choose the name but we go with `App`. Type the following:

```
dotnet new console -o App
```

1  

This will create a new project of type `console` with name `App`.

Lastly we add this project to the solution like so:

```
dotnet sln add App/App.csproj
```

1  

### [#](https://softchris.github.io/pages/dotnet-orm.html#install-and-set-up-2)Install and Set up

For this we will install the core library for Entity Framework but also support for the database type SqlLite. Note, there is support for different databases, have a look at the full list of supported databases here:

> [https://docs.microsoft.com/en-us/ef/core/providers/](https://docs.microsoft.com/en-us/ef/core/providers/?wt.mc_id=academic-0000-chnoring)

SqlLite is a very simple database that just stores structure and data in a file on your hard drive.

> But I'm working with a real database, what about me, will I benefit from this article?

Yes, what we are showing is generic knowledge that is widely applicable regardless of database type.

Ok then let's first navigate into our Console app directory, like so:

```
cd App
```

1  

Then install the needed NuGet libraries:

```cs
dotnet add package Microsoft.EntityFrameworkCore.Sqlite
dotnet add package Microsoft.EntityFrameworkCore.Design
```

1  
2  

This will add references to your project. Open up `App.csproj` and you should find something like this:

```cs
<ItemGroup>
  <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="2.2.6" />
  <PackageReference Include="Microsoft.EntityFrameworkCore.Sqlite" Version="2.2.6" />
</ItemGroup>
```

1  
2  
3  
4  

Now we need to actually install the libraries, we do that with the following command:

```
dotnet restore
```

1  

## [#](https://softchris.github.io/pages/dotnet-orm.html#a-crud-demo)A CRUD Demo

We will show how to do the full CRUD, Create, Read, Update and Delete.

Here we will attempt the following:

- **Create** the database
- **Create a migration** that represents the structure of the database and then apply it to create the database
- **Read** from the database
- **Write** to the database
- **Seed** our database with initial data

### [#](https://softchris.github.io/pages/dotnet-orm.html#create-the-database)Create the database

First off we need a Database so let's create one.

We will create a file called `Database.cs` with the following content:

```c#
// Database.cs

using Microsoft.EntityFrameworkCore;
using System;
using System.Collections.Generic;

namespace App
{
  public class DatabaseContext : DbContext
  {
    public DbSet<Product> Products { get; set; }

    public DbSet<OrderItem> OrderItems { get; set; }

    public DbSet<Order> Orders { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
      optionsBuilder.UseSqlite("Data Source=database.db");
    }
  }

  public class Order
  {
    public int OrderId { get; set; }

    public DateTime? Created { get; set; }
  
    public ICollection<OrderItem> Items { get; set; }
  }

  public class OrderItem
  {
    public int OrderItemId { get; set; }
    public int Quantity { get; set; }
    public virtual Product Product { get; set; }
  }

  public class Product 
  {
    public int ProductId { get; set; }
    public double Price { get; set; }
    public string Description { get; set; }
  }
}
```

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  
18  
19  
20  
21  
22  
23  
24  
25  
26  
27  
28  
29  
30  
31  
32  
33  
34  
35  
36  
37  
38  
39  
40  
41  
42  
43  
44  
45  

As you can see from the above code we have the following classes:

- **Order**, this is a class representing orders.
- **OrderItem**, an Order has many OrderItems and each OrderItem has a `Quantity` property and reference to a `Product`
- **Product**, this represents the Product we are trying to order. It has information on it like `Price` and `Description`.

Let's comment on some interesting constructs in the code.

**1-Many**

We are expressing a 1-Many relationship by the following construct on the `Order` class:

```cs
public ICollection<OrderItem> Items { get; set; }
```

1  

Above we are saying that we a list of of OrderItems on the Order.

**Foreign key**

We are also expressing another database concept namely _Foreign key_. In the `OrderItem` entity we are saying that we have a reference to a Product. In code, we write this as:

```cs
public virtual Product Product { get; set; }
```

1  

**DbContext and DbSet**

Let's also comment on first `DbContext`. When we want a new Database we should inherit from this class like so:

```cs
public class DatabaseContext : DbContext
```

1  

`DbSet` represents a table in a Database. It's a generic that takes a `type` as a template argument, like so:

```cs
public DbSet<OrderItem> OrderItems { get; set; }
```

1  

### [#](https://softchris.github.io/pages/dotnet-orm.html#create-a-migration)Create a migration

Now we have saved our file `Database.cs`. It's time to create the database. To do that we need to do two things:

- **Generate a migration**, this takes a snapshot of the current state of your code and diff this to any previous snapshot. If it doesn't have a previous snapshot, generating a migration will simply create the _initial migration_.
    
- **Apply the migration**, this will run the migration. Depending on the content of the migration it will either, create a database, affect the database structure or alter the data.
    

**Generate a migration**

Let's create our migration with the following command:

```
dotnet ef migrations add InitialCreate
```

1  

The last argument is the name of the migration and we can call it what we want but it's good to give it a descriptive name like `InitialCreate`.

Running the command should give the following result in the terminal:

![](https://thepracticaldev.s3.amazonaws.com/i/pfk5a3yk4h8b0ovdaoh6.png)

As you can see above it's nice enough to tell us how to _undo_ what we just di with the command `ef migrations remove`.

This created some files for us namely the following:

![](https://thepracticaldev.s3.amazonaws.com/i/rh7ugmlqutp59qu9yr7w.png)

Above you can see that we got our migration `InitialCreate` but that the name is being prepended by a timestamp. This is so Entity Framework knows what to run and in what order. We can also see that we have two versions of this file, a _.cs_ and a `Designer.cs` file. We only care about the first one. Let's have a look at it:

```cs
using System;
using Microsoft.EntityFrameworkCore.Migrations;

namespace App.Migrations
{
    public partial class InitialCreate : Migration
    {
        protected override void Up(MigrationBuilder migrationBuilder)
        {
            migrationBuilder.CreateTable(
                name: "Orders",
                columns: table => new
                {
                    OrderId = table.Column<int>(nullable: false)
                        .Annotation("Sqlite:Autoincrement", true),
                    Created = table.Column<DateTime>(nullable: true)
                },
                constraints: table =>
                {
                    table.PrimaryKey("PK_Orders", x => x.OrderId);
                });

            migrationBuilder.CreateTable(
                name: "Products",
                columns: table => new
                {
                    ProductId = table.Column<int>(nullable: false)
                        .Annotation("Sqlite:Autoincrement", true),
                    Price = table.Column<double>(nullable: false),
                    Description = table.Column<string>(nullable: true)
                },
                constraints: table =>
                {
                    table.PrimaryKey("PK_Products", x => x.ProductId);
                });

            migrationBuilder.CreateTable(
                name: "OrderItems",
                columns: table => new
                {
                    OrderItemId = table.Column<int>(nullable: false)
                        .Annotation("Sqlite:Autoincrement", true),
                    Quantity = table.Column<int>(nullable: false),
                    ProductId = table.Column<int>(nullable: true),
                    OrderId = table.Column<int>(nullable: true)
                },
                constraints: table =>
                {
                    table.PrimaryKey("PK_OrderItems", x => x.OrderItemId);
                    table.ForeignKey(
                        name: "FK_OrderItems_Orders_OrderId",
                        column: x => x.OrderId,
                        principalTable: "Orders",
                        principalColumn: "OrderId",
                        onDelete: ReferentialAction.Restrict);
                    table.ForeignKey(
                        name: "FK_OrderItems_Products_ProductId",
                        column: x => x.ProductId,
                        principalTable: "Products",
                        principalColumn: "ProductId",
                        onDelete: ReferentialAction.Restrict);
                });

            migrationBuilder.CreateIndex(
                name: "IX_OrderItems_OrderId",
                table: "OrderItems",
                column: "OrderId");

            migrationBuilder.CreateIndex(
                name: "IX_OrderItems_ProductId",
                table: "OrderItems",
                column: "ProductId");
        }

        protected override void Down(MigrationBuilder migrationBuilder)
        {
            migrationBuilder.DropTable(
                name: "OrderItems");

            migrationBuilder.DropTable(
                name: "Orders");

            migrationBuilder.DropTable(
                name: "Products");
        }
    }
}

```

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  
18  
19  
20  
21  
22  
23  
24  
25  
26  
27  
28  
29  
30  
31  
32  
33  
34  
35  
36  
37  
38  
39  
40  
41  
42  
43  
44  
45  
46  
47  
48  
49  
50  
51  
52  
53  
54  
55  
56  
57  
58  
59  
60  
61  
62  
63  
64  
65  
66  
67  
68  
69  
70  
71  
72  
73  
74  
75  
76  
77  
78  
79  
80  
81  
82  
83  
84  
85  
86  
87  
88  

The first thing we see is that we inherit from the class `Migration`. The second thing is that we have two methods `Up()` and `Down()`. `Up()` is run when we want to apply something. `Down()` is run when we want to _undo_ the migration. Looking at our `Up()` method we can see that we invoke `CreateTable()` once for each of the tables `Order`, `OrderItem` and `Product`. We can also see that it defines all the Foreign keys needed. The `Down()` method calls `DropTable()` to _undo_ our table creation.

**Apply the Migration**

Ok, we have a Migration, let's _apply_ it. We do that with the following command:

```cs
dotnet ef database update
```

1  

This will first create the database if needed and then apply the migration.

![](https://thepracticaldev.s3.amazonaws.com/i/topziid6t8af3o4bwwci.png)

We can see in our file structure that we got a new file created `database.db`. We can either use a SQlLite client or why not write some code to connect to it ? 😃

## [#](https://softchris.github.io/pages/dotnet-orm.html#read-from-the-database)Read from the database

Ok, now we want to see if we can connect to our database and maybe read out out some data. Open up `Program.cs` and go to the method `Main()` and add the following:

```
using (var db = new DatabaseContext())
{
}
```

1  
2  
3  

This will establish a connection to our database. To read from the database we only need to read from it like this:

```
using (var db = new DatabaseContext())
{
  var orders = db.Orders;
  foreach(var order in orders)
  {
    Console.WriteLine("Order: order.Created");
  }
}
```

1  
2  
3  
4  
5  
6  
7  
8  

Shall we try it out?

![](https://thepracticaldev.s3.amazonaws.com/i/pe8gwgvdq3myct922qhi.png)

Ok, we got no orders 😦.

Well, this is expected, we didn't put anything in the database. How bout we change that?

## [#](https://softchris.github.io/pages/dotnet-orm.html#write-to-the-database)Write to the Database

Ok, we know how to connect to the Database. What about writing to it?

Well to be able to create an `Order`, we need a little data first in the form of at least one `Product` and one `OrderItem`. If you want to save something to the database you need to call `db.SaveChanges()`.

We need to take all of this in steps cause there are some moving parts.

### [#](https://softchris.github.io/pages/dotnet-orm.html#creating-a-product)Creating a Product

First, we will create a `Product`.

Let's add the following code:

```
using (var db = new DatabaseContext())
{
    
    var product = new Product(){ Price = 100, Description = "Movie" };
    db.Products.Add(product);
    db.SaveChanges();

    foreach(var p in db.Products) 
    {
        Console.WriteLine("{0} {1} {2}", p.ProductId, p.Description, p.Price);
    }
    
}
```

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  

The above will create our `Product` and by invoking `db.SaveChanges()` we make sure to persist it to the database.

Running the code leads to

![](https://thepracticaldev.s3.amazonaws.com/i/3mmuogs3rswgof67f0my.png)

**OrderItem**

Ok, that bit works. What about creating an `OrderItem`? Well that's just as easy, we just need the following code:

```
using (var db = new DatabaseContext())
{
    var product = db.Products.SingleOrDefault();
    
    if(product != null)
    {
        var item = new OrderItem
        {
            Quantity = 1,
            Product = product
        };
        db.OrderItems.Add(item);
        db.SaveChanges();

        Console.WriteLine("{0} {1} Product: {2}", item.OrderItemId, item.Quantity, item.Product.Description);
    }
}
```

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  

Let's try to highlight the important parts.

![](https://thepracticaldev.s3.amazonaws.com/i/h1rn0g903qcu5k0h9gyw.png)

Above we can see that we first read out a `product` from the database. The next thing we do is to assign that same product to the `Product` property on the `OrderItem`. Then we save it all by adding our `OrderItem` to `db.OrderItems` followed by calling `db.SaveChanges()`.

### [#](https://softchris.github.io/pages/dotnet-orm.html#create-an-order)Create an Order

By now we have a `Product` and an `OrderItem` in the database. So how do we go about creating an Order containing those two entities?

Well creating an Order is not just creating an Order, it's creating an Order AND associate the OrderItem with the Order.

The association part can be done in two different ways:

1. Add the OrderItem to `order.Items`
2. Add a foreign key to our OrderItem and assign our Order id.

Both of the above solutions require us to know a bit more about Entity Framework.

**Load related entities**

Let's start with the first approach. For that, we need to know how to load related entities.

> Why?

Well, when you have an `Order` instance its `Items` will be `null` unless we tell it explicitly to be filled with something. For this approach to work, we need it to be an empty list at least so we can add our `OrderItem`.

> Ok, think you better show me.

Sure, have a look at the following code below:

```
var item = db.OrderItems.SingleOrDefault();
var order = new Order() { Created = DateTime.Now };
db.Orders.Add(order);
db.SaveChanges();
```

1  
2  
3  
4  

This creates an Order. What about adding our `item`? Well, we have a problem:

![](https://thepracticaldev.s3.amazonaws.com/i/6k8fschsk4sx9ru1ff1f.png)

Were we to attempt to our `item` at after we save our `Order` at row 49 our `order.Items` would be `null` and we would get a runtime exception. To solve that we need to use the method `Include()`. `Include()` takes a lambda where we need to point out what we want to load. In this case, we want to load the property `Items` on our `Order`.

Let's run this code:

![](https://thepracticaldev.s3.amazonaws.com/i/43h25e3kb6t2e4r5zzue.png)

At this point our `order.Items` is an empty array and we can add our `OrderItem` without the code crashing as you can see because we make it to line 54.

**Add a foreign key to OrderItem**

Behind the scenes, we have already gotten a foreign key on `OrderItem`. We can see that if we open up our migration:

![](https://thepracticaldev.s3.amazonaws.com/i/izsvemi4ucxibcxdoljc.png)

Our problem right now is that it doesn't exist as a property on our `OrderItem`, so how do we solve that?

Well, we just added to the class definition:

![](https://thepracticaldev.s3.amazonaws.com/i/c4txnmgwgrjqit0mq4p9.png)

Then because we have an existing Order that's associated with an OrderItem the following is actually populated `item.OrderId`:

![](https://thepracticaldev.s3.amazonaws.com/i/2rb3kx9lm8sg5a6j0r3o.png)

Had we wanted to make the connection between the Order and the OrderItem, and there already wasn't one, we could easily have done so with the following code:

```
using(var db = new DatabaseContext()) 
{
  var order = db.Orders.SingleOrDefault();
  var item = db.OrderItems.SingleOrDefault();
  item.OrderId = order.OrderId;
  db.SaveChanges();
}
```

1  
2  
3  
4  
5  
6  
7  

### [#](https://softchris.github.io/pages/dotnet-orm.html#update)Update

Updating is as easy as following the second creating scenario we did for an Order. That is read up an entity, set a property and call `db.SaveChanges()`. Like so:

```
using(var db = new DatabaseContext()) 
{
  var item = db.OrderItems.SingleOrDefault();
  item.Quantity++;
  db.SaveChanges();
}
```

1  
2  
3  
4  
5  
6  

### [#](https://softchris.github.io/pages/dotnet-orm.html#deletion)Deletion

Deleting is as easy as removing something from a list. If we want to delete a `Product` we just need to do the following:

```
using(var db = new DatabaseContext()) 
{
  var product = db.Products.SingleOrDefault();
  db.Products.Remove(product);
  db.SaveChanges();
}
```

1  
2  
3  
4  
5  
6  

It should be noted that if your Product is part of an `OrderItem` you would need to remove that connection first like so:

```
using(var db = new DatabaseContext()) 
{
  
  var item = db.OrderItems.Include(i => i.Product)SingleOrDefault();

  item.Product = null;
  db.SaveChanges();

  var product = db.Products.SingleOrDefault();
  db.Products.Remove(product);
  db.SaveChanges();
}
```

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  

## [#](https://softchris.github.io/pages/dotnet-orm.html#summary)Summary

This where we stop. We learned a ton in this article if we started from absolute zero

We learned:

- What an ORM is
- Define our database structure
- Create a migration and apply it
- Read data
- Create data
- Update data
- Delete data
- Load related entities
- Foreign keys

That's a lot for one article. Hopefully, you are now so interested that you want to learn more. Have a look at the Resources section to learn more if you want to learn more advanced concepts and about dealing with different kinds of databases.