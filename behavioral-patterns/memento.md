# Memento Pattern

## Overview

The **Memento** pattern captures the state of an object without exposing its internal structure, allowing for later restoration of that state. This pattern is typically used for undo or rollback functionality.

## When to Use

- When you need to store and restore an object’s state.
- When you need to implement undo functionality in applications like text editors or drawing applications.
- When you want to preserve an object's state but don’t want to expose its implementation details.

## Problem it Solves

Without the **Memento** pattern, you would need to expose the internal structure of an object to store and restore its state. The **Memento** pattern allows you to capture the state of an object without needing to expose its internal fields.

## Solution

The **Memento** pattern defines three main components:

- The **Originator**: The object whose state is being saved or restored.
- The **Memento**: The object that stores the state.
- The **Caretaker**: The object that manages the memento, keeping track of saved states.

## C# Code Example

``` C#
public class Memento
{
    public string State { get; }

    public Memento(string state)
    {
        State = state;
    }
}

public class Originator
{
    private string _state;

    public void SetState(string state)
    {
        _state = state;
    }

    public string GetState() => _state;

    public Memento SaveStateToMemento() => new Memento(_state);

    public void RestoreStateFromMemento(Memento memento)
    {
        _state = memento.State;
    }
}

public class Caretaker
{
    private List<Memento> _mementoList = new List<Memento>();

    public void AddMemento(Memento memento)
    {
        _mementoList.Add(memento);
    }

    public Memento GetMemento(int index) => _mementoList[index];
}
```

## Visual Example

In a **text editor**, you can use the **Memento** pattern to implement the undo functionality. Each time a user types something, the current state of the text is saved into a memento. When the user presses "undo," the editor restores the state from the memento, returning the text to the previous state.

The **Memento** pattern allows you to easily implement this functionality without exposing the internal structure of the text editor, such as its cursor position or document structure.

## Benefits

- **Encapsulation**: The object's state is saved and restored without exposing its internal structure.
- **Undo functionality**: It provides an easy way to implement undo/redo operations.
