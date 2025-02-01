# SOLID Principles

The **SOLID** principles are a set of five design principles that help software developers create maintainable, flexible, and scalable systems. These principles were introduced by Robert C. Martin and are considered fundamental to object-oriented programming.

---

## S - Single Responsibility Principle (SRP)

- **Definition**: A class should have only one reason to change, meaning that it should have only one job or responsibility.
- **Purpose**: This principle encourages the creation of classes that are highly focused on a single responsibility, which leads to better maintainability and reduced complexity.

### Code Example

Here’s an example that violates SRP:

``` C#
public class UserManager
{
    public void AddUser(string userName)
    {
        // Add user logic
        Console.WriteLine("User added: " + userName);
        LogAction("User added: " + userName);
    }

    public void LogAction(string message)
    {
        // Log action logic
        Console.WriteLine("Log: " + message);
    }
}
```

To fix this violation, we can separate the concerns:

``` C#
public class UserManager
{
    private readonly ILogger _logger;

    public UserManager(ILogger logger)
    {
        _logger = logger;
    }

    public void AddUser(string userName)
    {
        // Add user logic
        Console.WriteLine("User added: " + userName);
        _logger.Log("User added: " + userName);
    }
}

public interface ILogger
{
    void Log(string message);
}

public class FileLogger : ILogger
{
    public void Log(string message)
    {
        Console.WriteLine("Log to file: " + message);
    }
}
```

### Visual Example

Imagine you have a **ShoppingCart** class that is responsible for both managing the cart's contents and processing payments. The **Single Responsibility Principle** suggests splitting these responsibilities into separate classes: one for managing the cart's state (adding/removing items), and another for handling payments. This keeps the code focused and easier to maintain.

---

## O - Open/Closed Principle (OCP)

- **Definition**: Software entities (classes, modules, functions) should be open for extension but closed for modification.
- **Purpose**: This principle ensures that existing code does not need to be changed every time new functionality is added. Instead, new functionality is added by extending existing code, making the system more flexible and less prone to bugs.

### Code Example

Here’s an example violating OCP:

``` C#
public class DiscountCalculator
{
    public double CalculateDiscount(Order order)
    {
        if (order.Type == "Regular")
        {
            return order.Total * 0.1; // Regular discount
        }
        else if (order.Type == "Premium")
        {
            return order.Total * 0.2; // Premium discount
        }
        return 0;
    }
}
```

To adhere to OCP, we can use **polymorphism** to allow extensions without modifying the existing code:

``` C#
public abstract class Discount
{
    public abstract double CalculateDiscount(Order order);
}

public class RegularDiscount : Discount
{
    public override double CalculateDiscount(Order order)
    {
        return order.Total * 0.1;
    }
}

public class PremiumDiscount : Discount
{
    public override double CalculateDiscount(Order order)
    {
        return order.Total * 0.2;
    }
}

public class DiscountCalculator
{
    public double CalculateDiscount(Order order, Discount discount)
    {
        return discount.CalculateDiscount(order);
    }
}
```

### Visual Example

In a **payment system**, adding support for multiple payment methods (e.g., PayPal, CreditCard) should not require modifying the existing classes for **payment processing**. Instead, you should extend the system by creating new classes that implement a common interface for payment, thus adhering to OCP by allowing for extension without modification.

---

## L - Liskov Substitution Principle (LSP)

- **Definition**: Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.
- **Purpose**: This principle ensures that a subclass can be used interchangeably with its superclass, without introducing errors or unexpected behavior. It promotes proper inheritance and ensures that the subclass does not break functionality.

### Code Example

Here’s a violation of LSP:

``` C#
public class Bird
{
    public virtual void Fly() { Console.WriteLine("Flying..."); }
}

public class Ostrich : Bird
{
    public override void Fly() { throw new Exception("Ostriches can't fly!"); }
}
```

To adhere to LSP, we can refactor this example by creating more appropriate class hierarchies:

``` C#
public class Bird
{
    public virtual void Move() { Console.WriteLine("Flying..."); }
}

public class Sparrow : Bird
{
    public override void Move() { Console.WriteLine("Flying..."); }
}

public class Ostrich : Bird
{
    public override void Move() { Console.WriteLine("Running..."); }
}
```

### Visual Example

Consider an **e-commerce system** where you have a class for **Products** and subclasses for **Electronics** and **Clothing**. According to **LSP**, the `Electronics` class should be replaceable with the base `Product` class without causing issues in any part of the system, ensuring that all subclasses maintain expected behavior.

---

## I - Interface Segregation Principle (ISP)

- **Definition**: A client should not be forced to depend on interfaces it does not use.
- **Purpose**: This principle advocates for creating smaller, more specific interfaces, instead of large, general-purpose ones. It helps avoid unnecessary dependencies and ensures that classes are only concerned with methods they need, improving code clarity and maintainability.

### Code Example

Here’s a violation of ISP:

``` C#
public interface IWorker
{
    void Work();
    void Eat();
}

public class Worker : IWorker
{
    public void Work() { Console.WriteLine("Working..."); }
    public void Eat() { Console.WriteLine("Eating..."); }
}

public class Robot : IWorker
{
    public void Work() { Console.WriteLine("Working..."); }
    public void Eat() { throw new NotImplementedException(); }
}
```

To adhere to ISP, split the interface into more focused ones:

``` C#
public interface IWorkable
{
    void Work();
}

public interface IEatable
{
    void Eat();
}

public class Worker : IWorkable, IEatable
{
    public void Work() { Console.WriteLine("Working..."); }
    public void Eat() { Console.WriteLine("Eating..."); }
}

public class Robot : IWorkable
{
    public void Work() { Console.WriteLine("Working..."); }
}
```

### Visual Example

In a **document processing application**, you might have a class for **Document** with methods for printing and scanning. However, devices that only support printing, like a printer, should not be forced to implement methods for scanning. Instead, the **Interface Segregation Principle** encourages creating separate interfaces for **Printable** and **Scannable**, allowing devices to implement only the functionality they need.

---

## D - Dependency Inversion Principle (DIP)

- **Definition**: High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions.
- **Purpose**: This principle encourages the use of abstractions to decouple high-level and low-level modules. It ensures that the system is more flexible and easier to change or extend, promoting dependency injection and inversion of control.

### Code Example

Here’s a violation of DIP:

``` C#
public class LightBulb
{
    public void TurnOn() { Console.WriteLine("Light is on"); }
    public void TurnOff() { Console.WriteLine("Light is off"); }
}

public class Switch
{
    private LightBulb _lightBulb;

    public Switch(LightBulb lightBulb)
    {
        _lightBulb = lightBulb;
    }

    public void Operate()
    {
        _lightBulb.TurnOn();
    }
}
```

To adhere to DIP, we can introduce an interface:

``` C#
public interface IDevice
{
    void TurnOn();
    void TurnOff();
}

public class LightBulb : IDevice
{
    public void TurnOn() { Console.WriteLine("Light is on"); }
    public void TurnOff() { Console.WriteLine("Light is off"); }
}

public class Switch
{
    private IDevice _device;

    public Switch(IDevice device)
    {
        _device = device;
    }

    public void Operate()
    {
        _device.TurnOn();
    }
}
```

### Visual Example

Imagine a **home automation system** where you have multiple devices (lights, fans, thermostats). Instead of tightly coupling the `Switch` class to each device (like the `LightBulb`), the **Dependency Inversion Principle** encourages using an abstraction (`IDevice`) so that new devices can be added without modifying the `Switch` class. This promotes flexibility and extensibility in the system.

---

### Summary of SOLID Principles

By adhering to the **SOLID Principles**, developers can create systems that are more maintainable, flexible, and scalable. Each principle addresses a specific challenge in software design, ensuring that code is modular, easily extensible, and easier to maintain.

---
