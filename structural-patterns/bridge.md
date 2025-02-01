# Bridge Pattern

## Overview

The **Bridge** pattern decouples an abstraction from its implementation, allowing them to vary independently. This pattern is typically used to separate the abstraction of an object from the implementation of that abstraction.

## When to Use

- When you need to decouple an abstraction from its implementation so that both can evolve independently.
- When you have several variants of an object and its implementation that should not depend on each other.
- When you need to avoid a proliferation of classes due to the combination of multiple features or dimensions.

## Problem it Solves

Without the **Bridge** pattern, if you try to combine multiple features with different implementations, the number of classes could quickly grow out of control. The **Bridge** pattern separates the abstraction (what the object does) from the implementation (how the object does it), making it easier to manage and extend the code.

## Solution

The **Bridge** pattern provides an abstraction layer that holds a reference to an implementation object, allowing you to change the implementation independently from the abstraction. This helps avoid an explosion of classes when combining various features.

## C# Code Example

%%%
public interface IDriver
{
    void Drive();
}

public class CarDriver : IDriver
{
    public void Drive() => Console.WriteLine("Driving a car.");
}

public class BikeDriver : IDriver
{
    public void Drive() => Console.WriteLine("Riding a bike.");
}

public abstract class Vehicle
{
    protected IDriver _driver;

    public Vehicle(IDriver driver)
    {
        _driver = driver;
    }

    public abstract void DriveVehicle();
}

public class Car : Vehicle
{
    public Car(IDriver driver) : base(driver) { }

    public override void DriveVehicle()
    {
        _driver.Drive();
    }
}

public class Bike : Vehicle
{
    public Bike(IDriver driver) : base(driver) { }

    public override void DriveVehicle()
    {
        _driver.Drive();
    }
}
%%%

## Visual Example

The **Bridge** pattern is useful when you have different kinds of vehicles (e.g., cars, bikes) and different types of drivers (e.g., car driver, bike rider). By using the **Bridge**, you can separate the driver and vehicle logic into independent classes. This allows you to easily change or add new types of drivers or vehicles without modifying the entire system.

For instance, in an **automobile application**, the **Bridge** pattern could allow you to add new vehicles (such as trucks, buses) or new types of drivers (e.g., automated drivers) without having to rewrite existing code.

## Benefits

- **Independence of abstraction and implementation**: Both can vary independently without affecting each other.
- **Extensibility**: You can add new types of abstractions or implementations easily.
