### Covariant and contravariant generic type parameters

[Generic](https://en.wikipedia.org/wiki/Generic_programming "Generic programming") interfaces and delegates can have their type parameters marked as [covariant or contravariant](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science) "Covariance and contravariance (computer science)") using keywords `out` and `in` respectively. These declarations are then respected for type conversions, both implicit and explicit, and both compile time and run time. For example, the existing interface `IEnumerable<T>` has been redefined as follows:
```cs
interface IEnumerable<out T>
{
  IEnumerator<T> GetEnumerator();
}
```

Therefore, any class that implements `IEnumerable<Derived>` for some class `Derived` is also considered to be compatible with `IEnumerable<Base>` for all classes and interfaces `Base` that `Derived` extends, directly or indirectly. In practice, it makes it possible to write code such as:
```cs
void PrintAll(IEnumerable<object> objects)
{
  foreach (object o in objects)
  {
    System.Console.WriteLine(o);
  }
}

IEnumerable<string> strings = new List<string>();
PrintAll(strings); // IEnumerable<string> is implicitly converted to IEnumerable<object>
```
For contravariance, the existing interface `IComparer<T>` has been redefined as follows:
```cs
public interface IComparer<in T>
{
    int Compare(T x, T y);
}
```

Therefore, any class that implements `IComparer<Base>` for some class `Base` is also considered to be compatible with `IComparer<Derived>` for all classes and interfaces `Derived` that are extended from `Base`. It makes it possible to write code such as:
``
```cs
IComparer<object> objectComparer = GetComparer();
IComparer<string> stringComparer = objectComparer;
```


### C# examples
For example, in [C#](https://en.wikipedia.org/wiki/C_Sharp_(programming_language) "C Sharp (programming language)"), if `Cat` is a subtype of `Animal`, then:

- `IEnumerable<Cat>` is a subtype of `IEnumerable<Animal>`. The subtyping is preserved because `IEnumerable<T>` is **covariant** on `T`.
- `Action<Animal>` is a subtype of `Action<Cat>`. The subtyping is reversed because `Action<T>` is **contravariant** on `T`.
- Neither `IList<Cat>` nor `IList<Animal>` is a subtype of the other, because `IList<T>` is **invariant** on `T`.

The variance of a C# generic interface is declared by placing the `out` (covariant) or `in` (contravariant) attribute on (zero or more of) its type parameters. [2](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)#cite_note-Skeet-2): 144  The above interfaces are declared as `IEnumerable<out T>`, `Action<in T>`, and `IList<T>`. Types with more than one type parameter may specify different variances on each type parameter. For example, the delegate type `Func<in T, out TResult>` represents a function with a **contravariant** input parameter of type `T` and a **covariant** return value of type `TResult`.[3](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)#cite_note-3)[2](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)#cite_note-Skeet-2): 145  The compiler checks that all types are defined and used consistently with their annotations, and otherwise signals a compilation error.

The [typing rules for interface variance](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)#Interfaces) ensure type safety. For example, an `Action<T>` represents a first-class function expecting an argument of type `T`,[2](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)#cite_note-Skeet-2): 144  and a function that can handle any type of animal can always be used instead of one that can only handle cats.