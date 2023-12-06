Bronnen: [Microsoft](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/generics)

Generic means the general form, not specific. In C#, generic means not specific to a particular data type.

C# allows you to define generic classes, interfaces, abstract classes, fields, methods, static methods, properties, events, delegates, and operators using the [type parameter](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/generic-type-parameters) and without the specific data type. A type parameter is a placeholder for a particular type specified when creating an instance of the generic type.

A generic type is declared by specifying a type parameter in an angle brackets after a type name, e.g. `TypeName<T>` where `T` is a type parameter.

## Generic Class

Generic classes are defined using a type parameter in an angle brackets after the class name. The following defines a generic class.

Example: Define Generic Class

```csharp
class DataStore<T>
{
    public T Data { get; set; }
}
```

Above, the `DataStore` is a generic class. `T` is called type parameter, which can be used as a type of fields, properties, method parameters, return types, and delegates in the `DataStore` class. For example, `Data` is generic property because we have used a type parameter `T` as its type instead of the specific data type.

##### Note:
It is not required to use `T` as a type parameter. You can give any name to a type parameter. Generally, `T` is used when there is only one type parameter. It is recommended to use a more readable type parameter name as per requirement like `TSession`, `TKey`, `TValue` etc. Learn more about [Type Parameter Naming Guidelines](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/generic-type-parameters#type-parameter-naming-guidelines)

You can also define multiple type parameters separated by a comma.

Example: Generic Class with Multiple Type Parameters

```csharp
class KeyValuePair<TKey, TValue>
{
    public TKey Key { get; set; }
    public TValue Value { get; set; }
}
```

## Instantiating Generic Class

You can create an instance of generic classes by specifying an actual type in angle brackets. The following creates an instance of the generic class `DataStore`.

```csharp
DataStore<string> store = new DataStore<string>();
```

Above, we specified the `string` type in the angle brackets while creating an instance. So, `T` will be replaced with a `string` type wherever `T` is used in the entire class at compile-time. Therefore, the type of `Data` property would be a `string`.

The following figure illustrates how generics works.

[![C# Generics](https://www.tutorialsteacher.com/Content/images/csharp/generics.png)](https://www.tutorialsteacher.com/Content/images/csharp/generics.png)

You can assign a string value to the `Data` property. Trying to assign values other than string will result in a compile-time error.

```csharp
DataStore<string> store = new DataStore<string>();
store.Data = "Hello World!";
//store.Data = 123; //compile-time error
```

You can specify the different data types for different objects, as shown below.

Example: Generic class

```csharp
DataStore<string> strStore = new DataStore<string>();
strStore.Data = "Hello World!";
//strStore.Data = 123; // compile-time error

DataStore<int> intStore = new DataStore<int>();
intStore.Data = 100;
//intStore.Data = "Hello World!"; // compile-time error

KeyValuePair<int, string> kvp1 = new KeyValuePair<int, string>();
kvp1.Key = 100;
kvp1.Value = "Hundred";

KeyValuePair<string, string> kvp2 = new KeyValuePair<string, string>();
kvp2.Key = "IT";
kvp2.Value = "Information Technology";
```

[Try it](https://www.tutorialsteacher.com/codeeditor?cid=cs-fsGJGF "Try this example code yourself")

### Generic Class Characteristics

- A generic class increases the reusability. The more type parameters mean more reusable it becomes. However, too much generalization makes code difficult to understand and maintain.
- A generic class can be a base class to other generic or non-generic classes or abstract classes.
- A generic class can be derived from other generic or non-generic interfaces, classes, or abstract classes.

## Generic Fields

A generic class can include generic fields. However, it cannot be initialized.

Example: Generic Field

```csharp
class DataStore<T>
{
    public T data;
}
```

The following declares a generic array.

Example: Generic Array

```csharp
class DataStore<T>
{
    public T[] data = new T[10];
}
```

## Generic Methods

A method declared with the type parameters for its return type or parameters is called a generic method.

Example: Generic Methods

```csharp
class DataStore<T>
{
    private T[] _data = new T[10];
    
    public void AddOrUpdate(int index, T item)
    {
        if(index >= 0 && index < 10)
            _data[index] = item;
    }

    public T GetData(int index)
    {
        if(index >= 0 && index < 10)
            return _data[index];
        else 
            return default(T);
    }
}
```

Above, the `AddorUpdate()` and the `GetData()` methods are generic methods. The actual data type of the `item` parameter will be specified at the time of instantiating the `DataStore<T>` class, as shown below.

Example: Generic Methods

```csharp
DataStore<string> cities = new DataStore<string>();
cities.AddOrUpdate(0, "Mumbai");
cities.AddOrUpdate(1, "Chicago");
cities.AddOrUpdate(2, "London");

DataStore<int> empIds = new DataStore<int>();
empIds.AddOrUpdate(0, 50);
empIds.AddOrUpdate(1, 65);
empIds.AddOrUpdate(2, 89);
```

[Try it](https://www.tutorialsteacher.com/codeeditor?cid=cs-vd9JRC "Try this example code yourself")

The generic parameter type can be used with multiple parameters with or without non-generic parameters and return type. The followings are valid generic method overloading.

Example: Generic Method Overloading

```csharp
public void AddOrUpdate(int index, T data) { }
public void AddOrUpdate(T data1, T data2) { }
public void AddOrUpdate<U>(T data1, U data2) { }
public void AddOrUpdate(T data) { }
```

A non-generic class can include generic methods by specifying a type parameter in angle brackets with the method name, as shown below.

Example: Generic Method in Non-generic Class

```csharp
class Printer
{
    public void Print<T>(T data)
    {
        Console.WriteLine(data);
    }
}

Printer printer = new Printer();
printer.Print<int>(100);
printer.Print(200); // type infer from the specified value
printer.Print<string>("Hello");
printer.Print("World!"); // type infer from the specified value
```

[Try it](https://www.tutorialsteacher.com/codeeditor?cid=cs-L4RcaT "Try this example code yourself")

## Advantages of Generics

1. Generics increase the reusability of the code. You don't need to write code to handle different data types.
2. Generics are type-safe. You get compile-time errors if you try to use a different data type than the one specified in the definition.
3. Generic has a performance advantage because it removes the possibilities of boxing and unboxing.