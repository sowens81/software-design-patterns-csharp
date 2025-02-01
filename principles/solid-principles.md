# Solid Principles

The SOLID principles are a set of five design principles that help software developers create maintainable, flexible, and scalable systems. These principles were introduced by Robert C. Martin and are considered fundamental to object-oriented programming.

## S - Single Responsibility Principle (SRP)

- Definition: A class should have only one reason to change, meaning that it should have only one job or responsibility.
- Purpose: This principle encourages the creation of classes that are highly focused on a single responsibility, which leads to better maintainability and reduced complexity.

## O - Open/Closed Principle (OCP)

- Definition: Software entities (classes, modules, functions) should be open for extension but closed for modification.
- Purpose: This principle ensures that existing code does not need to be changed every time new functionality is added. Instead, new functionality is added by extending existing code, making the system more flexible and less prone to bugs.

## L - Liskov Substitution Principle (LSP)

- Definition: Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.
- Purpose: This principle ensures that a subclass can be used interchangeably with its superclass, without introducing errors or unexpected behavior. It promotes proper inheritance and ensures that the subclass does not break functionality.

## I - Interface Segregation Principle (ISP)

- Definition: A client should not be forced to depend on interfaces it does not use.
- Purpose: This principle advocates for creating smaller, more specific interfaces, instead of large, general-purpose ones. It helps avoid unnecessary dependencies and ensures that classes are only concerned with methods they need, improving code clarity and maintainability.

## D - Dependency Inversion Principle (DIP)

- Definition: High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions.
- Purpose: This principle encourages the use of abstractions to decouple high-level and low-level modules. It ensures that the system is more flexible and easier to change or extend, promoting dependency injection and inversion of control.
