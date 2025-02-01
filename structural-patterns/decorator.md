# Decorator Pattern

## Overview

The **Decorator** pattern allows you to add additional behavior to an object dynamically without altering its structure. It provides a flexible alternative to subclassing for extending functionality.

## When to Use

- When you need to add responsibilities to an object at runtime.
- When subclassing is impractical or would create an explosion of subclasses.
- When you need to extend functionality without altering the class itself.

## Problem it Solves

Without the **Decorator** pattern, you might end up with large, complex class hierarchies where functionality is added via subclassing. The **Decorator** pattern allows you to add functionality to objects dynamically, without creating subclasses for each combination of features.

## Solution

The **Decorator** pattern wraps an existing object with a decorator class, which can add additional behavior. Multiple decorators can be applied to a single object to extend its functionality.

## C# Code Example

``` C#
public interface ICar
{
    void Assemble();
}

public class BasicCar : ICar
{
    public void Assemble() => Console.WriteLine("Basic Car Assembly");
}

public class SportsCar : ICar
{
    private ICar _car;

    public SportsCar(ICar car)
    {
        _car = car;
    }

    public void Assemble()
    {
        _car.Assemble();
        Console.WriteLine("Sports Car Assembly");
    }
}

public class LuxuryCar : ICar
{
    private ICar _car;

    public LuxuryCar(ICar car)
    {
        _car = car;
    }

    public void Assemble()
    {
        _car.Assemble();
        Console.WriteLine("Luxury Car Assembly");
    }
}
```

## Visual Example

Imagine a basic car assembly line where you can add extra features dynamically. You start with a basic car, and then you can add different features like sports performance or luxury components without modifying the original car class.

The **Decorator** pattern lets you dynamically add these features at runtime. For instance, you could have a **SportsCarDecorator** that adds sports performance features, or a **LuxuryCarDecorator** that adds high-end features like leather seats.

## Benefits

- **Flexibility**: Behaviors can be added at runtime.
- **Avoids subclass explosion**: Multiple combinations of functionality can be achieved without subclassing.
