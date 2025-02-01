# Chain of Responsibility Pattern

## Overview

The **Chain of Responsibility** pattern passes requests along a chain of handlers, allowing each handler to process the request or pass it along further. It decouples the sender of a request from the receiver by giving multiple objects a chance to handle the request.

## When to Use

- When multiple objects can handle a request, and the handler is not known in advance.
- When you want to pass a request along a chain of handlers to see if any handler can process it.
- When you want to decouple the sender and receiver of a request, providing more flexibility in handling the request.

## Problem it Solves

Without the **Chain of Responsibility** pattern, the sender would need to know the exact recipient of a request. This tightly couples the sender and receiver. The **Chain of Responsibility** pattern allows the sender to pass the request along a chain, and any handler can process it without the sender knowing which handler is responsible.

## Solution

The **Chain of Responsibility** pattern creates a chain of handler objects. Each handler in the chain either processes the request or passes it along to the next handler. This provides a flexible way to process requests with different handlers.

## C# Code Example

``` C#
public abstract class Handler
{
    protected Handler _nextHandler;

    public void SetNext(Handler nextHandler)
    {
        _nextHandler = nextHandler;
    }

    public abstract void HandleRequest(string request);
}

public class ConcreteHandlerA : Handler
{
    public override void HandleRequest(string request)
    {
        if (request == "A")
        {
            Console.WriteLine("Handler A processed request.");
        }
        else if (_nextHandler != null)
        {
            _nextHandler.HandleRequest(request);
        }
    }
}

public class ConcreteHandlerB : Handler
{
    public override void HandleRequest(string request)
    {
        if (request == "B")
        {
            Console.WriteLine("Handler B processed request.");
        }
        else if (_nextHandler != null)
        {
            _nextHandler.HandleRequest(request);
        }
    }
}
```

## Visual Example

In a **customer support system**, requests might need to be handled by different departments based on the type of request (e.g., technical support, billing, etc.). The **Chain of Responsibility** pattern allows you to pass a request through a chain of handlers, and the appropriate department can process the request based on its type.

For example, if a customer sends a billing-related inquiry, the request will be handled by the billing department's handler, while technical inquiries will be passed to the technical support handler.
