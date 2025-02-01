# Adapter Pattern

## Overview

The **Adapter** pattern allows incompatible interfaces to work together by creating a bridge between them. It converts one interface to another that a client expects.

## When to Use

- When you have existing code (a third-party class or an old system) that needs to be adapted to a new interface.
- When you need to integrate new and old systems that are incompatible, but you don't want to modify their source code.
- When you need to use a class that has a different interface than the one required by your system.

## Problem it Solves

Without the **Adapter** pattern, you may have to modify the existing classes, which may be difficult, especially when dealing with third-party or legacy code. The Adapter pattern allows for seamless integration between incompatible systems without changing their internal structure.

## Solution

The Adapter pattern works by creating a wrapper or adapter class that converts the interface of the existing system into one that is understood by the new system, allowing them to work together.

## C# Code Example

%%%
public class OldSystem
{
    public void OldRequest()
    {
        Console.WriteLine("Old system request.");
    }
}

public interface INewSystem
{
    void NewRequest();
}

public class Adapter : INewSystem
{
    private readonly OldSystem _oldSystem;

    public Adapter(OldSystem oldSystem)
    {
        _oldSystem = oldSystem;
    }

    public void NewRequest()
    {
        _oldSystem.OldRequest();
    }
}
%%%

## Visual Example

Imagine integrating a modern application with a legacy system. The **Adapter** pattern allows you to keep the old system unchanged while using it in the new system by adapting the old system's interface to the new one. This way, you can work with the old system without modifying its code.

For instance, an **old printer system** may use one interface for printing, while the new system requires a different one. The **Adapter** pattern can help integrate these two by wrapping the old system with a new interface that the modern application expects.

## Benefits

- **Compatibility**: Enables integration between incompatible systems.
- **Code reuse**: The old system can continue being used without modifying it.
