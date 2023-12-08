There is a distinction being made between _**covariance**_ and _**contravariance**_.  
Very roughly, an operation is covariant if it preserves the ordering of types, and contravariant if it **reverses** this order.

The ordering itself is meant to represent more general types as larger than more specific types.  
Here's one example of a situation where C# supports covariance. First, this is an array of objects:

```csharp
var objects = new object[3];
objects[0] = new object();
objects[1] = "Just a string";
objects[2] = 10;
```

Of course it is possible to insert different values into the array because in the end they all derive from `System.Object` in .Net framework. In other words, `System.Object` is a very general or **large** type. Now here's a spot where covariance is supported:  
_**assigning a value of a smaller type to a variable of a larger type**_

```csharp
var strings = new string[] { "one", "two", "three" };
objects = strings;
```

The variable objects, which is of type `object[]`, can store a value that is in fact of type `string[]`.

Think about it — to a point, it's what you expect, but then again it isn't. After all, while `string` derives from `object`, `string[]` **DOES NOT** derive from `object[]`. The language support for covariance in this example makes the assignment possible anyway, which is something you'll find in many cases. _Variance_ is a feature that makes the language work more intuitively.

The considerations around these topics are extremely complicated. For instance, based on the preceding code, here are two scenarios that will result in errors.

```csharp
// Runtime exception here - the array is still of type string[],
// ints can't be inserted
objects[2]=10;

// Compiler error here - covariance support in this scenario only
// covers reference types, and int is a value type
var ints = new int[] { 1, 2, 3 };
objects = ints;
```

An example for the workings of contravariance is a bit more complicated. Imagine these two classes:

```csharp
public partial class Person: IPerson 
{
    public Person() 
    {
    }
}

public partial class Woman: Person
{
    public Woman()
    {
    }
}
```

`Woman` is derived from `Person`, obviously. Now consider you have these two functions:

```csharp
static void WorkWithPerson(Person person)
{
}

static void WorkWithWoman(Woman woman)
{
}
```

One of the functions does something(it doesn't matter what) with a `Woman`, the other is more general and can work with any type derived from `Person`. On the `Woman` side of things, you now also have these:

```scss
delegate void AcceptWomanDelegate(Woman person);

static void DoWork(Woman woman, AcceptWomanDelegate acceptWoman)
{
    acceptWoman(woman);
}
```

`DoWork` is a function that can take a `Woman` and a reference to a function that also takes a `Woman`, and then it passes the instance of `Woman` to the delegate. Consider the _polymorphism_ of the elements you have here. `Person` is _larger_ than `Woman`, and `WorkWithPerson` is _larger_ than `WorkWithWoman`. `WorkWithPerson` is also considered _larger_ than `AcceptWomanDelegate` for the purpose of variance.

Finally, you have these three lines of code:

```lisp
var woman = new Woman();
DoWork(woman, WorkWithWoman);
DoWork(woman, WorkWithPerson);
```

A `Woman` instance is created. Then DoWork is called, passing in the `Woman` instance as well as a reference to the `WorkWithWoman` method. The latter is obviously compatible with the delegate type `AcceptWomanDelegate` — one parameter of type `Woman`, no return type. The third line is a bit odd, though. The method `WorkWithPerson` takes a `Person` as parameter, not a `Woman`, as required by `AcceptWomanDelegate`. Nevertheless, `WorkWithPerson` is compatible with the delegate type. _**Contravariance**_ makes it possible, so in the case of delegates the larger type `WorkWithPerson` can be stored in a variable of the smaller type `AcceptWomanDelegate`. Once more it's the intuitive thing: _**if `WorkWithPerson` can work with any `Person`, passing in a `Woman` can't be wrong**_, right?

By now, you may be wondering how all this relates to generics. The answer is that variance can be applied to generics as well. The preceding example used `object` and `string` arrays. Here the code uses generic lists instead of the arrays:

```csharp
var objectList = new List<object>();
var stringList = new List<string>();
objectList = stringList;
```

If you try this out, you will find that this is not a supported scenario in C#. In C# version 4.0 as well as .Net framework 4.0, variance support in generics has been cleaned up, and it is now possible to use the new keywords _**in**_ and _**out**_ with generic type parameters. They can define and restrict the direction of data flow for a particular type parameter, allowing variance to work. But in the case of `List<T>`, the data of type `T` flows in both directions — there are methods on the type `List<T>` that return `T` values, and others that receive such values.

The point of these directional restrictions is **to allow variance where it makes sense**, but to **prevent problems** like the runtime error mentioned in one of the previous array examples. When type parameters are correctly decorated with _in_ or _out_, the compiler can check, and allow or disallow, its variance at _**compile time**_. Microsoft has gone to the effort of adding these keywords to many standard interfaces in .Net framework, like `IEnumerable<T>`:

```csharp
public interface IEnumerable<out T>: IEnumerable
{
    // ...
}
```

For this interface, the data flow of type `T` objects is clear: _**they can only ever be retrieved from methods supported by this interface, not passed into them**_. As a result, it is possible to construct an example similar to the `List<T>` attempt described previously, but using `IEnumerable<T>` :

```csharp
IEnumerable<object> objectSequence = new List<object>();
IEnumerable<string> stringSequence = new List<string>();
objectSequence = stringSequence;
```

This code is acceptable to the C# compiler since version 4.0 because `IEnumerable<T>` is covariant due to the _out_ specifier on the type parameter `T`.

When working with generic types, it is important to be aware of variance and the way the compiler is applying various kinds of trickery in order to make your code work the way you expect it to.

There's more to know about variance than is covered in this chapter, but this shall suffice to make all further code understandable.

Ref:

- [`PROFESSIONAL Functional Programming in C#`](https://rads.stackoverflow.com/amzn/click/com/0470744588)