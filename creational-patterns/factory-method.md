# Factory Method Pattern

## Overview

The **Factory Method** pattern defines an interface for creating objects, but lets subclasses decide which class to instantiate. It provides a way to delegate the instantiation of objects to subclasses, enabling more flexible and reusable code.

## When to Use

- When you want to delegate object creation to subclasses and avoid the direct instantiation of specific classes.
- When the exact type of the object isn't known until runtime, such as when implementing a plugin system or creating a product catalog with varying types of products.
- When a class doesn't know exactly what subclass of an object it needs to create.

## Problem it Solves

If you have a class that is responsible for creating objects of a particular type, and you want to extend that behavior (e.g., create different types of objects based on certain conditions), the Factory Method allows you to do this without altering the existing code.

## Solution

The Factory Method pattern provides an interface for creating objects in a super class but allows subclasses to alter the type of object that will be created. This allows for a cleaner and more flexible approach to object creation.

## C# Code Example

%%%
public abstract class Product
{
    public abstract void DoSomething();
}

public class ConcreteProductA : Product
{
    public override void DoSomething() => Console.WriteLine("Product A Action");
}

public class ConcreteProductB : Product
{
    public override void DoSomething() => Console.WriteLine("Product B Action");
}

public abstract class Creator
{
    public abstract Product FactoryMethod();
}

public class ConcreteCreatorA : Creator
{
    public override Product FactoryMethod() => new ConcreteProductA();
}

public class ConcreteCreatorB : Creator
{
    public override Product FactoryMethod() => new ConcreteProductB();
}
%%%

## Visual Example

Consider a software system where you need to create different types of vehicles (e.g., cars, trucks). You could use the **Factory Method** to create the appropriate vehicle type based on user input or other runtime conditions.

For example, a program might use the **Factory Method** to decide whether to create a car or truck object, depending on the user’s preference for a light or heavy-duty vehicle. The user may not need to know which specific vehicle class is being instantiated, but by calling a factory method, the right object is returned, simplifying object creation while keeping the code flexible.

## Benefits

- **Flexible object creation**: Allows the decision on which object to create to be deferred to subclasses.
- **Easier maintenance**: By isolating object creation, the code is easier to maintain and extend.
