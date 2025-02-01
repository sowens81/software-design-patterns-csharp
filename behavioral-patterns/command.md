# Command Pattern

## Overview

The **Command** pattern encapsulates a request as an object, allowing for parameterization and queuing of requests. It allows you to decouple the sender of a request from the object that processes it.

## When to Use

- When you need to issue requests to objects without knowing the operation being requested or the receiver of the request.
- When you want to queue or log requests, or provide undo functionality.
- When you want to decouple senders and receivers of requests, providing flexibility in request handling.

## Problem it Solves

Without the **Command** pattern, you might end up with direct invocations of methods on objects, leading to tightly coupled code. The **Command** pattern decouples the sender from the receiver by turning requests into objects that can be handled more flexibly.

## Solution

The **Command** pattern encapsulates requests as command objects. This allows you to pass requests along, queue them, log them, and even implement undo functionality. The sender does not need to know the specific details of the request, making the system more flexible.

## C# Code Example

``` C#
public interface ICommand
{
    void Execute();
}

public class LightOnCommand : ICommand
{
    private readonly Light _light;

    public LightOnCommand(Light light)
    {
        _light = light;
    }

    public void Execute() => _light.TurnOn();
}

public class Light
{
    public void TurnOn() => Console.WriteLine("Light is on");
}

public class RemoteControl
{
    private ICommand _command;

    public void SetCommand(ICommand command)
    {
        _command = command;
    }

    public void PressButton()
    {
        _command.Execute();
    }
}
```

## Visual Example

In a **home automation system**, a **remote control** could use the **Command** pattern to execute various commands like turning on the lights, adjusting the thermostat, or closing the curtains. Each action (e.g., turning on the light) is encapsulated in a command object, and the remote control simply invokes the `Execute()` method on the command object.

The **Command** pattern makes it easy to queue or log commands, and even provides the ability to add undo functionality if required.

## Benefits

- **Decoupling**: The sender and receiver are decoupled, promoting flexibility.
- **Extensibility**: New commands can be added without modifying existing code.
- **Undo functionality**: Command objects can be easily extended to support undo functionality.
