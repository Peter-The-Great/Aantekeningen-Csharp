[Generics](Generics.md)
C# allows you to use constraints to restrict client code to specify certain types while instantiating generic types. It will give a compile-time error if you try to instantiate a generic type using a type that is not allowed by the specified constraints.

You can specify one or more constraints on the generic type using the `where` clause after the generic type name.

Syntax:

```csharp
GenericTypeName<T> where T  : contraint1, constraint2
```

The following example demonstrates a generic class with a constraint to reference types when instantiating the generic class.

Example: Declare Generic Constraints

```csharp
class DataStore<T> where T : class
{
    public T Data { get; set; }
}
```

Above, we applied the class constraint, which means only a reference type can be passed as an argument while creating the DataStore class object. So, you can pass reference types such as class, interface, delegate, or array type. Passing value types will give a compile-time error, so we cannot pass primitive data types or struct types.

```csharp
DataStore<string> store = new DataStore<string>(); // valid
DataStore<MyClass> store = new DataStore<MyClass>(); // valid
DataStore<IMyInterface> store = new DataStore<IMyInterface>(); // valid
DataStore<IEnumerable> store = new DataStore<IMyInterface>(); // valid
DataStore<ArrayList> store = new DataStore<ArrayList>(); // valid
//DataStore<int> store = new DataStore<int>(); // compile-time error 
```

The following table lists the types of generic constraints.
![[Pasted image 20231205153348.png]]
## where T : struct

The following example demonstrates the `struct` constraint that restricts type argument to be non-nullable value type only.

Example: struct Constraints

```csharp
class DataStore<T> where T : struct
{
    public T Data { get; set; }
}

DataStore<int> store = new DataStore<int>(); // valid
DataStore<char> store = new DataStore<char>(); // valid
DataStore<MyStruct> store = new DataStore<MyStruct>(); // valid
//DataStore<string> store = new DataStore<string>(); // compile-time error 
//DataStore<IMyInterface> store = new DataStore<IMyInterface>(); // compile-time error 
//DataStore<ArrayList> store = new DataStore<ArrayList>(); // compile-time error 
```

## where T : new()

The following example demonstrates the `struct` constraint that restricts type argument to be non-nullable value type only.

Example: new() Constraint

```csharp
class DataStore<T> where T : class, new()
{
    public T Data { get; set; }
}

DataStore<MyClass> store = new DataStore<MyClass>(); // valid
DataStore<ArrayList> store = new DataStore<ArrayList>(); // valid
//DataStore<string> store = new DataStore<string>(); // compile-time error 
//DataStore<int> store = new DataStore<int>(); // compile-time error 
//DataStore<IMyInterface> store = new DataStore<IMyInterface>(); // compile-time error 
```

## where T : baseclass

The following example demonstrates the `base class` constraint that restricts type argument to be a derived class of the specified class, abstract class, or an interface.

Example: BaseClass Constraint

```csharp
class DataStore<T> where T : IEnumerable
{
    public T Data { get; set; }
}

DataStore<ArrayList> store = new DataStore<ArrayList>(); // valid
DataStore<List> store = new DataStore<List>(); // valid
//DataStore<string> store = new DataStore<string>(); // compile-time error 
//DataStore<int> store = new DataStore<int>(); // compile-time error 
//DataStore<IMyInterface> store = new DataStore<IMyInterface>(); // compile-time error 
//DataStore<MyClass> store = new DataStore<MyClass>(); // compile-time error 
```