# Flyweight Pattern

## Overview

The **Flyweight** pattern reduces the number of objects created by sharing common data between similar objects. It is used to optimize memory usage by sharing objects rather than creating new ones each time.

## When to Use

- When you need to create a large number of objects that share many common data.
- When you want to save memory by sharing data that doesn’t change between objects.
- When your system creates objects that are often identical in many ways.

## Problem it Solves

Without the **Flyweight** pattern, creating many objects with identical data would be memory-inefficient. Each object would take up space for its common data, even though much of the data is identical across multiple objects.

## Solution

The **Flyweight** pattern allows objects to share common data. It defines a central **Flyweight Factory** that manages the shared data and returns references to shared objects instead of creating new ones. This reduces memory usage while maintaining the ability to manage many objects.

## C# Code Example

``` C#
public interface ICharacter
{
    void Display();
}

public class ConcreteCharacter : ICharacter
{
    private string _type;

    public ConcreteCharacter(string type)
    {
        _type = type;
    }

    public void Display() => Console.WriteLine($"Character of type: {_type}");
}

public class CharacterFactory
{
    private Dictionary<string, ICharacter> _characters = new Dictionary<string, ICharacter>();

    public ICharacter GetCharacter(string type)
    {
        if (!_characters.ContainsKey(type))
        {
            _characters[type] = new ConcreteCharacter(type);
        }
        return _characters[type];
    }
}
```

## Visual Example

Imagine a **text editor** that uses different fonts for characters. Rather than creating a new object for each character, the **Flyweight** pattern allows you to reuse the same object for characters with the same font. Each time a new character is added to the text, the system checks if it already has the character for that font style, and if so, it reuses it.

The **Flyweight** pattern optimizes memory usage by sharing common data like font type and size, while allowing unique data (like the character itself) to be stored separately.

## Benefits

- **Memory efficiency**: Reduces memory usage by sharing common data.
- **Improved performance**: Reduces the overhead of creating identical objects.
