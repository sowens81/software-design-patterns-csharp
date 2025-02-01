# GRASP Principles

The **GRASP** (General Responsibility Assignment Software Patterns) principles are a set of guidelines that help software designers assign responsibilities to classes and objects. These principles focus on designing a system that is flexible, maintainable, and easy to extend. GRASP principles aim to improve the organization of code and ensure that responsibilities are assigned to the most appropriate classes or objects in an object-oriented system.

## 1. Information Expert

- **Definition**: Assign the responsibility to the class that has the necessary information to fulfill it.
- **Purpose**: This principle encourages assigning responsibilities to classes that have the necessary data or knowledge to perform the task. This leads to greater cohesion and better organization of responsibilities.

## 2. Creator

- **Definition**: Assign the responsibility for creating instances of objects to the class that has the appropriate data, relationship, or control over the created object.
- **Purpose**: This principle helps in determining which class should be responsible for creating new objects. It ensures that object creation is assigned to the class that has the most natural responsibility for it, promoting maintainability and logical organization.

## 3. Controller

- **Definition**: Assign the responsibility for handling system events to a class that represents a use-case scenario or the system itself.
- **Purpose**: The **Controller** is responsible for managing user inputs or system events and acting as an intermediary between the view and model layers. It reduces the coupling between the user interface and the business logic.

## 4. Low Coupling

- **Definition**: Assign responsibilities to minimize dependencies between classes, reducing the impact of changes in the system.
- **Purpose**: This principle focuses on reducing tight coupling between classes, making the system more flexible and easier to maintain. Low coupling means that classes are less dependent on each other, reducing the risk of breaking the system when changes are made.

## 5. High Cohesion

- **Definition**: Assign responsibilities to classes that are highly focused and have well-defined roles, making them easier to maintain and extend.
- **Purpose**: The principle of high cohesion encourages grouping related functionalities together in a single class, making the class easier to understand and maintain. A highly cohesive class has a clear purpose and is less likely to change frequently.

## 6. Polymorphism

- **Definition**: Assign responsibilities for handling varied behaviors based on the common abstraction, rather than using conditional logic.
- **Purpose**: **Polymorphism** encourages handling different types of behaviors (such as different types of objects or actions) through common interfaces or base classes. This simplifies code by avoiding conditionals and promotes extensibility.

## 7. Pure Fabrication

- **Definition**: Create a class that does not represent a real-world concept but is created to fulfill a specific responsibility that is not fitting for any existing class.
- **Purpose**: **Pure Fabrication** is used when a responsibility cannot be assigned to any existing class in the system. It creates a new class for that responsibility, helping to keep the system clean and organized.

## 8. Indirection

- **Definition**: Assign the responsibility of mediation to an intermediary class to decouple classes that have a direct relationship.
- **Purpose**: This principle uses an intermediary class to handle requests or actions between other classes, helping to reduce direct dependencies and improve flexibility.

## 9. Protected Variations

- **Definition**: Assign responsibility to create a stable interface for a concept, protecting it from the impact of changes in its subclasses or related components.
- **Purpose**: The **Protected Variations** principle helps in creating stable interfaces that shield the core system from changes in related or subclassed components. This ensures that changes in subclasses don’t propagate through the system, reducing potential breaking changes.
