# Facade Pattern

## Overview

The **Facade** pattern provides a simplified interface to a complex subsystem, making it easier to use. It provides a higher-level interface that makes the subsystem easier to use and reduces the complexity for the client.

## When to Use

- When you have a complex subsystem with many interdependent classes and you want to provide a simpler interface.
- When you want to provide a uniform interface to a set of interfaces in a subsystem.
- When you need to decouple the client from the complex subsystem, hiding the internal workings of the subsystem.

## Problem it Solves

Without the **Facade** pattern, the client would have to interact directly with the complex subsystem, which might involve dealing with multiple classes and interfaces. The **Facade** simplifies this by providing a single entry point that hides the complexity.

## Solution

The **Facade** pattern defines a class that wraps the subsystem and provides a simplified interface for the client. It reduces the complexity of using the subsystem by abstracting away the details.

## C# Code Example

``` C#
public class SubsystemA
{
    public void OperationA() => Console.WriteLine("Subsystem A Operation");
}

public class SubsystemB
{
    public void OperationB() => Console.WriteLine("Subsystem B Operation");
}

public class SubsystemC
{
    public void OperationC() => Console.WriteLine("Subsystem C Operation");
}

public class Facade
{
    private SubsystemA _subsystemA;
    private SubsystemB _subsystemB;
    private SubsystemC _subsystemC;

    public Facade(SubsystemA subsystemA, SubsystemB subsystemB, SubsystemC subsystemC)
    {
        _subsystemA = subsystemA;
        _subsystemB = subsystemB;
        _subsystemC = subsystemC;
    }

    public void Operation()
    {
        _subsystemA.OperationA();
        _subsystemB.OperationB();
        _subsystemC.OperationC();
    }
}
```

## Visual Example

Imagine using a complex home theater system where you need to control various components such as the projector, sound system, and lights. The **Facade** pattern provides a **HomeTheaterFacade** class that simplifies the operation, letting the client just call `TurnOn()` without needing to interact with each individual system.

The **Facade** pattern hides the complexity of managing all the components, making the interaction simpler for the user.

## Benefits

- **Simplification**: Provides a simplified interface to a complex subsystem.
- **Decoupling**: Reduces the dependency between the client and the subsystem.
