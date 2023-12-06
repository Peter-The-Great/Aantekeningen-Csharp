Komt van: [[Method Overriding and hiding]]

When used as a declaration modifier, the `new` keyword explicitly hides a member that is inherited from a base class. When you hide an inherited member, the derived version of the member replaces the base class version. This assumes that the base class version of the member is visible, as it would already be hidden if it were marked as `private` or, in some cases, `internal`. Although you can hide `public` or `protected` members without using the `new` modifier, you get a compiler warning. If you use `new` to explicitly hide a member, it suppresses this warning.

You can also use the `new` keyword to [create an instance of a type](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/new-operator) or as a [generic type constraint](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/new-constraint).

To hide an inherited member, declare it in the derived class by using the same member name, and modify it with the `new` keyword. For example:

```cs
public class BaseC
{
    public int x;
    public void Invoke() { }
}
public class DerivedC : BaseC
{
    new public void Invoke() { }
}
```

In this example, `BaseC.Invoke` is hidden by `DerivedC.Invoke`. The field `x` is not affected because it is not hidden by a similar name.

Name hiding through inheritance takes one of the following forms:

- Generally, a constant, field, property, or type that is introduced in a class or struct hides all base class members that share its name. There are special cases. For example, if you declare a new field with name `N` to have a type that is not invocable, and a base type declares `N` to be a method, the new field does not hide the base declaration in invocation syntax. For more information, see the [Member lookup](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/expressions#125-member-lookup) section of the [C# language specification](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/readme).
    
- A method introduced in a class or struct hides properties, fields, and types that share that name in the base class. It also hides all base class methods that have the same signature.
    
- An indexer introduced in a class or struct hides all base class indexers that have the same signature.
    

It is an error to use both `new` and [override](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/override) on the same member, because the two modifiers have mutually exclusive meanings. The `new` modifier creates a new member with the same name and causes the original member to become hidden. The `override` modifier extends the implementation for an inherited member.

Using the `new` modifier in a declaration that does not hide an inherited member generates a warning.

[](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/new-modifier#examples)

## Examples

In this example, a base class, `BaseC`, and a derived class, `DerivedC`, use the same field name `x`, which hides the value of the inherited field. The example demonstrates the use of the `new` modifier. It also demonstrates how to access the hidden members of the base class by using their fully qualified names.

C#Copy

```cs
public class BaseC
{
    public static int x = 55;
    public static int y = 22;
}

public class DerivedC : BaseC
{
    // Hide field 'x'.
    new public static int x = 100;

    static void Main()
    {
        // Display the new value of x:
        Console.WriteLine(x);

        // Display the hidden value of x:
        Console.WriteLine(BaseC.x);

        // Display the unhidden member y:
        Console.WriteLine(y);
    }
}
/*
Output:
100
55
22
*/
```

In this example, a nested class hides a class that has the same name in the base class. The example demonstrates how to use the `new` modifier to eliminate the warning message and how to access the hidden class members by using their fully qualified names.

C#Copy

```cs
public class BaseC
{
    public class NestedC
    {
        public int x = 200;
        public int y;
    }
}

public class DerivedC : BaseC
{
    // Nested type hiding the base type members.
    new public class NestedC
    {
        public int x = 100;
        public int y;
        public int z;
    }

    static void Main()
    {
        // Creating an object from the overlapping class:
        NestedC c1  = new NestedC();

        // Creating an object from the hidden class:
        BaseC.NestedC c2 = new BaseC.NestedC();

        Console.WriteLine(c1.x);
        Console.WriteLine(c2.x);
    }
}
/*
Output:
100
200
*/
```

If you remove the `new` modifier, the program will still compile and run, but you will get the following warning:

textCopy

```cs
The keyword new is required on 'MyDerivedC.x' because it hides inherited member 'MyBaseC.x'.
```

[](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/new-modifier#c-language-specification)

## C# language specification

For more information, see [The new modifier](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/classes#1535-the-new-modifier) section of the [C# language specification](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/readme).