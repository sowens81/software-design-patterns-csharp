# Composite Pattern

## Overview

The **Composite** pattern allows you to compose objects into tree structures to represent part-whole hierarchies. It allows individual objects and compositions of objects to be treated uniformly.

## When to Use

- When you want to represent part-whole hierarchies.
- When individual objects and composite objects (collections of objects) should be treated uniformly.
- When you need to create complex structures from simple objects.

## Problem it Solves

Without the **Composite** pattern, you might end up with code that treats individual objects and collections of objects differently. The **Composite** pattern allows you to treat both types of objects uniformly, simplifying the management of complex hierarchies.

## Solution

The **Composite** pattern enables you to work with part-whole hierarchies by treating individual objects and composites of objects in the same way. It does this by having a common interface for both simple and composite objects, allowing you to combine them easily.

## C# Code Example

%%%
public interface IComponent
{
    void Operation();
}

public class Leaf : IComponent
{
    public void Operation() => Console.WriteLine("Leaf operation");
}

public class Composite : IComponent
{
    private List<IComponent> _children = new List<IComponent>();

    public void Add(IComponent component)
    {
        _children.Add(component);
    }

    public void Operation()
    {
        foreach (var child in _children)
        {
            child.Operation();
        }
    }
}
%%%

## Visual Example

Imagine a file system where folders can contain both files and other folders. Using the **Composite** pattern, you can treat both files and folders as `IComponent` objects. This allows you to recursively call the `Operation()` method on both files and folders, simplifying the code that manages the file system hierarchy.

For example, in a **graphic design application**, you could use the **Composite** pattern to manage groups of shapes (like circles and rectangles). You could group multiple shapes into a "composite" shape, then treat the entire group and individual shapes as if they were the same type.

## Benefits

- **Uniformity**: Treat individual objects and compositions of objects uniformly.
- **Easy to extend**: You can add new components or leaf nodes easily without modifying the existing code.
