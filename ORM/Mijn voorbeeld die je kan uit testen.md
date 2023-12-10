Program.cs:
```cs
using System;
using System.Linq;
using System.Reflection.Metadata;
namespace ef_task;
class Program
{
    static void Main(string[] args)
    {
        var db = new BloggingContext();

        // Note: This sample requires the database to be created before running.
        Console.WriteLine($"Database path: {db.DbPath}");

        // Create
        Console.WriteLine("Inserting a new blog");
        db.Add(new Blog { Url = "http://blogs.msdn.com/adonet" });
        db.SaveChanges();

        // Read, We want to grab the first blog
        Console.WriteLine("Querying for a blog");
        var blog = db.Blogs.OrderBy(b => b.BlogId).First();
        Console.WriteLine(blog.Url);

        //Update
        Console.WriteLine("Updating the blog and adding a post");
        blog.Url = "https://devblogs.microsoft.com/dotnet";
        blog.Posts.Add(new Post { Title = "First Post ever LOL", Content = "Help me please" });
        db.SaveChanges();
        Console.WriteLine(blog.Url);

        // Delete
        /*Console.WriteLine("Delete the blog");
        db.Remove(blog);
        db.SaveChanges();*/
    }
}
```

Model.cs:
```cs
using Microsoft.EntityFrameworkCore;
using Microsoft.EntityFrameworkCore.Sqlite;
using System;
using System.Collections.Generic;

namespace ef_task;

public class BloggingContext : DbContext
{
    public DbSet<Blog> Blogs { get; set; }
    public DbSet<Post> Posts { get; set; }

    public string? DbPath {get;}

    public BloggingContext()
    {
        var folder = Environment.CurrentDirectory;
        DbPath = Path.Combine(folder, "blogging.db");
        Database.EnsureCreated();
    }
    // The following configures EF to create a Sqlite database file in the
    // special "local" folder for your platform.
    protected override void OnConfiguring(DbContextOptionsBuilder options)
        => options.UseSqlite($"Data Source={DbPath}");
}

public class Blog
{
    public int BlogId { get; set; }
    public string? Url { get; set; }

    public List<Post>? Posts { get; } = new();
}
public class Post
{
    public int PostId { get; set; }
    public string? Title { get; set; }
    public string? Content { get; set; }

    public int BlogId { get; set; }
    public Blog? Blog { get; set; }
}
```