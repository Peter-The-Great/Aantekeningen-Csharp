Hieronder is een goed voorbeeld van hoe je een object Initializer moet starten.
```cs				
public class Program
{
	public static void Main()
	{
		Student std = new Student() { StudentID = 1, 
                                      StudentName = "Bill", 
                                      Age = 20, 
                                      Address = "New York"   
                                    };

		Console.WriteLine(std.StudentName);
	}
}

public class Student
{
    public int StudentID { get; set; }
    public string StudentName { get; set; }
    public int Age { get; set; }
	public string Address { get; set; }

}
```

Hieronder is een list:
```cs			
public class Program
{
	public static void Main()
	{
		var student1 = new Student() { StudentID = 1, StudentName = "John" };
		var student2 = new Student() { StudentID = 2, StudentName = "Steve" };
		var student3 = new Student() { StudentID = 3, StudentName = "Bill" } ;
		var student4 = new Student() { StudentID = 3, StudentName = "Bill" };
		var student5 = new Student() { StudentID = 5, StudentName = "Ron" };

		IList<Student> studentList = new List<Student>() { 
                                                    student1, 
                                                    student2, 
                                                    student3, 
                                                    student4, 
                                                    student5 
                                                };

		Console.WriteLine("Total Students: {0}",studentList.Count);
	}
}

public class Student
{
    public int StudentID { get; set; }
    public string StudentName { get; set; }

}
```

Goed voorbeeld van het gebruik van Initializer override is dit:
```csharp
public readonly struct Initializer<T>(T latitude, T longtitude)
{
  public T Latitude { get; init; } = latitude;
  public T Longtitude { get; init; } = longtitude;
}
private static void Initialize()
  {
  //Eerst wordt er iets gemaakt in de primary constructor
    var initialize = new Initializer<float>(4.653861f, 3.293164f)
    {
    //Hier worden ze geoverride.
      Latitude = 6.490459f,
      Longtitude = 2.640913f
    };

    var data = new List<Initializer<float>>
    {
      initialize
    };
    
    data.Add(new Initializer<float>(9.393452f, 14.421363f));
    Console.WriteLine($"5.\nThe following data is: {data}.\n");
  }
```