Bronnen: [TopCoder](https://www.topcoder.com/thrive/articles/Invariance,%20Covariance%20and%20Contravariance%20types%20in%20C%20Sharp%20-%20Part%20One)
## Basics
In C# programming language, we make the transition between types using Variance feature in three ways.

- Invariance feature: The type to be assigned and the type assigned must be the same. This means that there is no switch between a Child (More Derived) type and a Parent (Less Derived) type.
    
- Covariance feature: You can switch from a Child type to a Parent type.
    
    - More Derived -> Less Derived transition
        
- Contravariance feature: You can switch from a Parent type to a Child type.
    
    - Less Derived -> More Derived transition
        

As we frequently use the definitions of More Derived and Less Derived within the subject, let us clarify them.

Code:

```csharp
1 class Base {}
2 class Derived: Base {}
3 class Derived2: Derived {}
```

Let’s go step by step as the related description may change according to the direction we look at.

- Object is the ancestor of all types, it is always the Less Derived type compared to other types.
    
- Base type is More Derived according to Object type. So Derived is Less Derived type according to Derived2.
    
- The Derived type is More Derived according to Object and Base types, Less Derived type according to Derived2 type.


In C#, "contravariant" and "covariant" are terms related to generic type parameters and are primarily associated with delegates and interfaces. These concepts help define the direction in which type conversion is allowed when dealing with generic types. I'll explain the concepts and how they work in C#:

1. **Covariance:** Covariance allows you to use a more derived type than originally specified. It is denoted by the `out` keyword in C#. You can use covariance when a type parameter is only used as the return type of a method. For example:
    
 ```c#
    interface ICovariant<out T>
    {
	    T GetItem();
    } 
    class Animal { }
    class Dog : Animal { }
    ICovariant<Animal> covariant = new ICovariant<Dog>();
```
    
In this example, `ICovariant` is a covariant interface because it's marked with the `out` keyword. This allows us to assign an instance of `ICovariant<Dog>` to a variable of type `ICovariant<Animal>`. The `GetItem` method returns a `T`, which is allowed because of covariance.
    
2. **Contravariance:** Contravariance allows you to use a less derived type than originally specified. It is denoted by the `in` keyword in C#. You can use contravariance when a type parameter is only used as method parameter types. For example:
    
```c#
    interface IContravariant<in T>
    {
	    void UseItem(T item);
    }
    class Animal { } class Dog : Animal { }
    IContravariant<Dog> contravariant = new IContravariant<Animal>();
```
    
In this example, `IContravariant` is a contravariant interface because it's marked with the `in` keyword. This allows us to assign an instance of `IContravariant<Animal>` to a variable of type `IContravariant<Dog>`. The `UseItem` method accepts a `T` as a parameter, which is allowed because of contravariance.
    

It's important to note that contravariance and covariance only apply to reference types (classes and interfaces) and not to value types (structs).

These features help improve flexibility when working with generic types and can make your code more versatile.

In C#, when a type parameter is declared as invariant, it means that the type parameter must be used exactly as specified, without allowing any conversion to or from more derived or less derived types. In other words, you cannot use a more derived type or a less derived type than what is explicitly defined for the generic type. Invariant type parameters are the default behavior for most generic types.

For example:

csharpCopy code

```c#
class Invariant<T> {
private T data;
public Invariant(T data){this.data = data;}
public T GetData(){return data;}
}
```

In this case, the type parameter `T` is declared as invariant. You can only use `Invariant<T>` with the exact type specified. You cannot assign an instance of `Invariant<Derived>` to a variable of type `Invariant<Base>`, nor can you assign an instance of `Invariant<Base>` to a variable of type `Invariant<Derived>`.

Invariance is the default behavior for generic type parameters in C#. If you don't specify `in` or `out` for a generic type parameter when defining a generic type or interface, it is treated as invariant by default.

Sources:
https://www.youtube.com/watch?v=VHDYx7oPE84&ab_channel=Pluralsight

Tips:
Met parameters is contravariant
Met getters is covariant.

Photo
![[F0CD2A34-1A59-494E-BF1B-B1B3DCD33F21.jpeg]]