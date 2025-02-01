# Observer Pattern

## Overview

The **Observer** pattern defines a one-to-many dependency between objects, so that when one object changes state, all its dependents are notified and updated automatically. It is commonly used to implement event handling systems or messaging frameworks.

## When to Use

- When you want to notify multiple objects of state changes in another object without tightly coupling the objects.
- When multiple objects need to be updated automatically based on the state of a subject object.
- When implementing event systems or subscribing to notifications.

## Problem it Solves

Without the **Observer** pattern, you would have to manually notify all dependent objects of changes to the state of a subject. This could lead to tightly coupled code and difficulties in maintaining the system. The **Observer** pattern decouples the subject from its observers.

## Solution

The **Observer** pattern defines a subject that maintains a list of observers. When the subject's state changes, it notifies all registered observers. Observers can subscribe and unsubscribe from the subject without altering the subject itself.

## C# Code Example

%%%
public interface IObserver
{
    void Update(string state);
}

public class ConcreteObserver : IObserver
{
    private string _name;

    public ConcreteObserver(string name)
    {
        _name = name;
    }

    public void Update(string state)
    {
        Console.WriteLine($"{_name} received state update: {state}");
    }
}

public class Subject
{
    private List<IObserver> _observers = new List<IObserver>();
    private string _state;

    public void Attach(IObserver observer)
    {
        _observers.Add(observer);
    }

    public void Detach(IObserver observer)
    {
        _observers.Remove(observer);
    }

    public void SetState(string state)
    {
        _state = state;
        Notify();
    }

    private void Notify()
    {
        foreach (var observer in _observers)
        {
            observer.Update(_state);
        }
    }
}
%%%

## Visual Example

Imagine a **weather monitoring system** where multiple display devices (observers) need to be updated whenever the weather changes (subject). When the weather station detects a change in temperature, all registered devices (observers) are notified and updated automatically with the new temperature.

This allows you to add or remove devices without altering the weather station itself, following the **Observer** pattern for loose coupling between the subject and its observers.

## Benefits

- **Loose coupling**: The subject does not need to know about the concrete observers, only their interface.
- **Dynamic updates**: Observers are automatically updated when the subject's state changes.
- **Scalability**: New observers can be added without modifying existing code.
