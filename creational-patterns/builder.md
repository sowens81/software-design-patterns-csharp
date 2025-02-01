# Builder Pattern

## Overview

The **Builder** pattern allows you to construct complex objects step by step. It abstracts the construction process and allows you to create different representations of the same type of object.

## When to Use

- When an object needs to be constructed with many optional parameters.
- When you want to avoid telescoping constructors (constructors with many parameters).
- When the construction process involves several steps and you want to separate that logic from the final object.

## Problem it Solves

In situations where you have objects with many configuration options, the Builder pattern helps to avoid confusion and errors that may arise from calling a constructor with too many parameters or making the object creation process overly complicated.

## Solution

The Builder pattern separates the construction logic from the object itself, enabling the construction of different representations of an object. The client can provide specific configuration or details, and the Builder will assemble the object accordingly.

## C# Code Example

``` C#
public class Car
{
    public string Engine { get; set; }
    public string Wheels { get; set; }
    public string Color { get; set; }
}

public interface ICarBuilder
{
    void BuildEngine();
    void BuildWheels();
    void BuildColor();
    Car GetResult();
}

public class SportsCarBuilder : ICarBuilder
{
    private Car _car = new Car();

    public void BuildEngine() => _car.Engine = "V8 Engine";
    public void BuildWheels() => _car.Wheels = "Sport Wheels";
    public void BuildColor() => _car.Color = "Red";
    public Car GetResult() => _car;
}
```

## Visual Example

Think of a car manufacturing process where the customer can specify a range of features for the car (engine type, color, wheels). The **Builder** pattern allows the customer to specify the desired features, and the Builder will take care of constructing the car accordingly.

In this case, the **Builder** allows for flexibility in car creation by letting you customize each part without dealing with a complex constructor that has too many parameters.

## Benefits

- **Separation of concerns**: The creation logic is separated from the final object, making the code cleaner.
- **Customizability**: The object can be built step by step, allowing greater control over the creation process.
