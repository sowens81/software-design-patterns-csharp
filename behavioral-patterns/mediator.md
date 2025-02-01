# Mediator Pattern

## Overview

The **Mediator** pattern defines an object that centralizes communication between components, reducing direct dependencies between them. It facilitates loose coupling by preventing components from referring to each other explicitly.

## When to Use

- When you have a system with many components that interact with each other, and you want to reduce direct communication between them.
- When you want to centralize communication and control how components interact.
- When the interactions between components are complex and should be abstracted.

## Problem it Solves

Without the **Mediator** pattern, components in a system might become tightly coupled because they directly reference each other. This can make the system hard to maintain and extend. The **Mediator** pattern helps reduce this complexity by centralizing the communication between components.

## Solution

The **Mediator** pattern introduces a mediator object that manages communication between components. Components interact with the mediator instead of communicating directly with each other.

## C# Code Example

%%%
public class Mediator
{
    private readonly List<IComponent> _components = new List<IComponent>();

    public void Register(IComponent component)
    {
        _components.Add(component);
    }

    public void SendMessage(string message, IComponent sender)
    {
        foreach (var component in _components)
        {
            if (component != sender)
            {
                component.ReceiveMessage(message);
            }
        }
    }
}

public interface IComponent
{
    void ReceiveMessage(string message);
}

public class ComponentA : IComponent
{
    public void ReceiveMessage(string message) => Console.WriteLine($"Component A received: {message}");
}
%%%

## Visual Example

In a **chatroom** application, the **Mediator** pattern can be used to manage communication between users. Rather than users communicating directly with each other, they send messages to the **ChatRoomMediator**, which broadcasts the message to all users in the room. This keeps the users decoupled and the communication centralized.

## Benefits

- **Decoupling**: Reduces direct dependencies between components.
- **Centralized communication**: All interactions pass through a mediator, making the system easier to maintain.
