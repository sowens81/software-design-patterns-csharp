# GRASP Principles

The **GRASP** (General Responsibility Assignment Software Patterns) principles are a set of guidelines that help software designers assign responsibilities to classes and objects. These principles focus on designing a system that is flexible, maintainable, and easy to extend. GRASP principles aim to improve the organization of code and ensure that responsibilities are assigned to the most appropriate classes or objects in an object-oriented system.

---

## 1. Information Expert

- **Definition**: Assign the responsibility to the class that has the necessary information to fulfill it.
- **Purpose**: This principle encourages assigning responsibilities to classes that have the necessary data or knowledge to perform the task. This leads to greater cohesion and better organization of responsibilities.

### Code Example

``` C#
public class Order
{
    public double Total { get; set; }
}

public class DiscountCalculator
{
    public double CalculateDiscount(Order order)
    {
        if (order.Total > 100)
        {
            return order.Total * 0.1; // 10% discount
        }
        return 0;
    }
}
```

In this case, the **Order** class is an information expert because it knows the details about the order, including the total. The **DiscountCalculator** class is responsible for calculating the discount, using the information provided by the **Order** class.

---

## 2. Creator

- **Definition**: Assign the responsibility for creating instances of objects to the class that has the appropriate data, relationship, or control over the created object.
- **Purpose**: This principle helps in determining which class should be responsible for creating new objects. It ensures that object creation is assigned to the class that has the most natural responsibility for it, promoting maintainability and logical organization.

### Code Example

``` C#
public class Customer
{
    public string Name { get; set; }
}

public class Order
{
    public Customer Customer { get; set; }

    public Order(Customer customer)
    {
        Customer = customer;
    }
}
```

Here, the **Customer** class is responsible for creating an **Order** because it has the necessary relationship with the **Order** object.

---

## 3. Controller

- **Definition**: Assign the responsibility for handling system events to a class that represents a use-case scenario or the system itself.
- **Purpose**: The **Controller** is responsible for managing user inputs or system events and acting as an intermediary between the view and model layers. It reduces the coupling between the user interface and the business logic.

### Code Example

``` C#
public class OrderController
{
    private readonly Order _order;

    public OrderController(Order order)
    {
        _order = order;
    }

    public void ProcessOrder()
    {
        // Perform actions to process the order
        Console.WriteLine("Order processed for: " + _order.Customer.Name);
    }
}
```

In this example, **OrderController** acts as the **Controller**, handling events related to the **Order**.

---

## 4. Low Coupling

- **Definition**: Assign responsibilities to minimize dependencies between classes, reducing the impact of changes in the system.
- **Purpose**: This principle focuses on reducing tight coupling between classes, making the system more flexible and easier to maintain. Low coupling means that classes are less dependent on each other, reducing the risk of breaking the system when changes are made.

### Code Example

``` C#
public interface IEmailSender
{
    void SendEmail(string emailAddress, string message);
}

public class EmailService : IEmailSender
{
    public void SendEmail(string emailAddress, string message)
    {
        Console.WriteLine("Sending email to " + emailAddress);
    }
}

public class UserRegistration
{
    private readonly IEmailSender _emailSender;

    public UserRegistration(IEmailSender emailSender)
    {
        _emailSender = emailSender;
    }

    public void RegisterUser(string emailAddress)
    {
        Console.WriteLine("User registered with email: " + emailAddress);
        _emailSender.SendEmail(emailAddress, "Welcome!");
    }
}
```

Here, **UserRegistration** depends on the **IEmailSender** abstraction, ensuring low coupling. It doesn't directly depend on a specific implementation of **IEmailSender**, making the system more flexible.

---

## 5. High Cohesion

- **Definition**: Assign responsibilities to classes that are highly focused and have well-defined roles, making them easier to maintain and extend.
- **Purpose**: The principle of high cohesion encourages grouping related functionalities together in a single class, making the class easier to understand and maintain. A highly cohesive class has a clear purpose and is less likely to change frequently.

### Code Example

``` C#
public class Invoice
{
    public double Amount { get; set; }
    
    public void CalculateTotalAmount()
    {
        // Calculate total logic
        Amount = 100; // Example calculation
    }
}

public class InvoicePrinter
{
    public void PrintInvoice(Invoice invoice)
    {
        // Print invoice logic
        Console.WriteLine("Invoice amount: " + invoice.Amount);
    }
}
```

Here, **Invoice** is highly cohesive because it is responsible only for managing the invoice's total, while **InvoicePrinter** handles printing the invoice, ensuring that each class has a clear responsibility.

---

## 6. Polymorphism

- **Definition**: Assign responsibilities for handling varied behaviors based on the common abstraction, rather than using conditional logic.
- **Purpose**: **Polymorphism** encourages handling different types of behaviors (such as different types of objects or actions) through common interfaces or base classes. This simplifies code by avoiding conditionals and promotes extensibility.

### Code Example

``` C#
public interface IDocument
{
    void Print();
}

public class PDFDocument : IDocument
{
    public void Print()
    {
        Console.WriteLine("Printing PDF document...");
    }
}

public class WordDocument : IDocument
{
    public void Print()
    {
        Console.WriteLine("Printing Word document...");
    }
}

public class DocumentPrinter
{
    public void PrintDocument(IDocument document)
    {
        document.Print();
    }
}
```

Here, the **PrintDocument** class uses polymorphism to handle different document types (PDF, Word) without needing to check for specific types or behaviors.

---

## 7. Pure Fabrication

- **Definition**: Create a class that does not represent a real-world concept but is created to fulfill a specific responsibility that is not fitting for any existing class.
- **Purpose**: **Pure Fabrication** is used when a responsibility cannot be assigned to any existing class in the system. It creates a new class for that responsibility, helping to keep the system clean and organized.

### Code Example

``` C#
public class DataManager
{
    public void SaveData(string data)
    {
        // Logic to save data
        Console.WriteLine("Saving data: " + data);
    }

    public void LoadData()
    {
        // Logic to load data
        Console.WriteLine("Loading data...");
    }
}
```

Here, **DataManager** is a **Pure Fabrication** that is created to manage data operations, even though it doesn't represent a real-world object.

---

## 8. Indirection

- **Definition**: Assign the responsibility of mediation to an intermediary class to decouple classes that have a direct relationship.
- **Purpose**: This principle uses an intermediary class to handle requests or actions between other classes, helping to reduce direct dependencies and improve flexibility.

### Code Example

``` C#
public class Mediator
{
    private readonly CustomerService _customerService;
    private readonly OrderService _orderService;

    public Mediator(CustomerService customerService, OrderService orderService)
    {
        _customerService = customerService;
        _orderService = orderService;
    }

    public void HandleOrder(Order order)
    {
        _customerService.ValidateCustomer(order.Customer);
        _orderService.ProcessOrder(order);
    }
}
```

Here, the **Mediator** acts as an intermediary to decouple the **CustomerService** and **OrderService**, allowing them to interact without directly depending on each other.

---

## 9. Protected Variations

- **Definition**: Assign responsibility to create a stable interface for a concept, protecting it from the impact of changes in its subclasses or related components.
- **Purpose**: The **Protected Variations** principle helps in creating stable interfaces that shield the core system from changes in related or subclassed components. This ensures that changes in subclasses don’t propagate through the system, reducing potential breaking changes.

### Code Example

``` C#
public interface IPaymentProcessor
{
    void ProcessPayment(decimal amount);
}

public class PayPalProcessor : IPaymentProcessor
{
    public void ProcessPayment(decimal amount)
    {
        Console.WriteLine("Processing payment via PayPal: " + amount);
    }
}

public class CreditCardProcessor : IPaymentProcessor
{
    public void ProcessPayment(decimal amount)
    {
        Console.WriteLine("Processing payment via CreditCard: " + amount);
    }
}
```

Here, **IPaymentProcessor** serves as a stable interface, and both **PayPalProcessor** and **CreditCardProcessor** are decoupled from the core system, protecting it from changes.
