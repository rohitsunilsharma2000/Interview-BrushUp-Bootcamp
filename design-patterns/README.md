# The Catalog of Design Patterns

## Table of Contents

- [Creational Patterns](#creational-patterns)
    - [Factory Method](#factory-method)
    - [Abstract Factory](#abstract-factory)
    - [Builder](#builder)
    - [Prototype](#prototype)
    - [Singleton](#singleton)
- [Structural Patterns](#structural-patterns)
    - [Adapter](#adapter)
    - [Bridge](#bridge)
    - [Composite](#composite)
    - [Decorator](#decorator)
    - [Facade](#facade)
    - [Flyweight](#flyweight)
    - [Proxy](#proxy)
- [Behavioral Patterns](#behavioral-patterns)
    - [Chain of Responsibility](#chain-of-responsibility)
    - [Command](#command)
    - [Iterator](#iterator)
    - [Mediator](#mediator)
    - [Memento](#memento)
    - [Observer](#observer)
    - [State](#state)
    - [Strategy](#strategy)
    - [Template Method](#template-method)
    - [Visitor](#visitor)

---

## Creational Patterns

These patterns provide various object creation mechanisms, which increase flexibility and reuse of existing code.
Creational patterns are a set of design patterns that focus on how objects are created. For a layman software engineer, think of them as smart, flexible blueprints for building objects in your program. Instead of writing the code to create objects in many places (which can lead to errors and messy code), creational patterns provide a structured way to handle object creation. This makes your code easier to maintain and change.

In essence, creational patterns help you create objects in a clean, reusable, and flexible way.

### Factory Method

### What is Factory Method?

The **Factory Method** is a design pattern in object-oriented programming that provides a way to create objects without specifying the exact class of the object that will be created. Instead of creating objects directly using `new`, it delegates the object creation to a separate method or function. This allows you to create different objects depending on the situation or need, without needing to know the details of how those objects are created.

### Real-World Analogy for Layman Engineer:
Imagine you're working with a large CRM system (a software used to manage customer relationships, sales processes, and marketing efforts). This CRM system needs to generate different types of reports like:
- **Sales Report**
- **Customer Engagement Report**
- **Marketing Report**

Now, instead of manually creating each report type every time, the system can use a "report factory" to generate the report you need. You don’t have to worry about how each report is generated—just ask the factory for a report, and it will return the right one based on your request.

### Java Code Example Using Factory Method:

Here’s a simple example of how you can use the Factory Method in Java. Imagine we're building a system that generates different types of reports for a CRM platform.

```java
// Step 1: Create a common interface for all reports
interface Report {
    void generateReport();
}

// Step 2: Create different types of reports (Sales, Customer, Marketing)
class SalesReport implements Report {
    @Override
    public void generateReport() {
        System.out.println("Generating Sales Report...");
    }
}

class CustomerReport implements Report {
    @Override
    public void generateReport() {
        System.out.println("Generating Customer Engagement Report...");
    }
}

class MarketingReport implements Report {
    @Override
    public void generateReport() {
        System.out.println("Generating Marketing Performance Report...");
    }
}

// Step 3: Create a factory class that will create reports based on the report type
class ReportFactory {
    public static Report createReport(String reportType) {
        if (reportType == null) {
            return null;
        }
        
        if (reportType.equalsIgnoreCase("SALES")) {
            return new SalesReport();
        } else if (reportType.equalsIgnoreCase("CUSTOMER")) {
            return new CustomerReport();
        } else if (reportType.equalsIgnoreCase("MARKETING")) {
            return new MarketingReport();
        }
        
        return null;
    }
}

// Step 4: Main class to test the factory method
public class Main {
    public static void main(String[] args) {
        // Requesting a Sales Report
        Report salesReport = ReportFactory.createReport("SALES");
        salesReport.generateReport();

        // Requesting a Customer Report
        Report customerReport = ReportFactory.createReport("CUSTOMER");
        customerReport.generateReport();

        // Requesting a Marketing Report
        Report marketingReport = ReportFactory.createReport("MARKETING");
        marketingReport.generateReport();
    }
}
```

### Explanation of the Code:
1. **`Report` Interface**: This is a common interface that all report types (Sales, Customer, Marketing) will implement. It has a `generateReport()` method that every report type will override to specify how it generates the report.

2. **Report Classes**: `SalesReport`, `CustomerReport`, and `MarketingReport` implement the `Report` interface and provide their own implementation of `generateReport()` to generate their respective reports.

3. **`ReportFactory` Class**: This is the core of the Factory Method pattern. The `createReport()` method checks the type of report the user wants and returns the appropriate report object. This way, you don't have to manually create each report yourself.

4. **Main Class**: In the `main` method, we test the factory method. Instead of directly creating `SalesReport`, `CustomerReport`, or `MarketingReport`, we use the `ReportFactory` to request the desired report. The factory returns the right object for us, and we call `generateReport()` on that object to generate the report.

### Output:
```
Generating Sales Report...
Generating Customer Engagement Report...
Generating Marketing Performance Report...
```

### Why Use the Factory Method?
- It makes your code more **flexible** and **extensible**. If you need to add a new type of report (e.g., **Financial Report**), you just add a new class implementing `Report` and update the factory, without changing the rest of the system.
- It **hides** the complexity of object creation from the user and abstracts the process. The user doesn't need to know which exact class is being used—they just call the factory and get the right object.

This is a simple, practical way to use the Factory Method pattern in a CRM-like system, where different types of reports need to be created dynamically.

### Abstract Factory

### What is Abstract Factory?

The **Abstract Factory** is a **creational design pattern** used to provide an interface for creating families of related or dependent objects without specifying their concrete classes. In simpler terms, it allows you to create related objects (like products in a product family) without worrying about the exact types of those objects.

This pattern is useful when your system needs to work with various families of products, but you don't want to tightly couple the code to specific classes. Instead, you create factories that are responsible for creating objects in a way that the client code doesn't need to know the exact class names.

### Key Concepts:
- **Factory**: A method that creates objects.
- **Abstract Factory**: A factory that creates families of related objects.
- **Product Family**: A set of related products created by a factory.

### Example in Layman's Terms:
Imagine you have a **furniture store** that sells two types of furniture: **Modern** and **Victorian**. Each type of furniture has a set of related products, such as chairs, tables, and sofas.

- If you want to buy a **Modern** chair, the store provides a **Modern Furniture Factory**.
- If you want to buy a **Victorian** chair, the store provides a **Victorian Furniture Factory**.

The **Abstract Factory** allows you to ask for furniture without worrying about whether you're getting modern or Victorian; you just ask for a factory that fits your need.

### Java Code Example:

In the context of a **Payroll and HR management platform** for small businesses, let's say the platform can offer payroll services for different types of businesses like **small business** and **large business**. Both will need similar services but with different configurations.

We'll use the **Abstract Factory** pattern to define these services.

#### Step 1: Define the Abstract Factory Interface
```java
// Abstract Factory
interface EmployeeFactory {
    Payroll createPayroll();
    Benefits createBenefits();
}
```

#### Step 2: Create Concrete Factories for Different Types of Businesses

```java
// Concrete Factory for Small Business
class SmallBusinessFactory implements EmployeeFactory {
    public Payroll createPayroll() {
        return new SmallBusinessPayroll();
    }

    public Benefits createBenefits() {
        return new SmallBusinessBenefits();
    }
}

// Concrete Factory for Large Business
class LargeBusinessFactory implements EmployeeFactory {
    public Payroll createPayroll() {
        return new LargeBusinessPayroll();
    }

    public Benefits createBenefits() {
        return new LargeBusinessBenefits();
    }
}
```

#### Step 3: Define the Abstract Product Interfaces

```java
// Abstract Product for Payroll
interface Payroll {
    void processPayroll();
}

// Abstract Product for Benefits
interface Benefits {
    void manageBenefits();
}
```

#### Step 4: Create Concrete Products for Small Business

```java
// Concrete Payroll for Small Business
class SmallBusinessPayroll implements Payroll {
    public void processPayroll() {
        System.out.println("Processing payroll for small business.");
    }
}

// Concrete Benefits for Small Business
class SmallBusinessBenefits implements Benefits {
    public void manageBenefits() {
        System.out.println("Managing benefits for small business.");
    }
}
```

#### Step 5: Create Concrete Products for Large Business

```java
// Concrete Payroll for Large Business
class LargeBusinessPayroll implements Payroll {
    public void processPayroll() {
        System.out.println("Processing payroll for large business.");
    }
}

// Concrete Benefits for Large Business
class LargeBusinessBenefits implements Benefits {
    public void manageBenefits() {
        System.out.println("Managing benefits for large business.");
    }
}
```

#### Step 6: Client Code
```java
public class Client {
    public static void main(String[] args) {
        // Small Business
        EmployeeFactory smallBusinessFactory = new SmallBusinessFactory();
        Payroll smallBusinessPayroll = smallBusinessFactory.createPayroll();
        Benefits smallBusinessBenefits = smallBusinessFactory.createBenefits();
        smallBusinessPayroll.processPayroll();
        smallBusinessBenefits.manageBenefits();

        // Large Business
        EmployeeFactory largeBusinessFactory = new LargeBusinessFactory();
        Payroll largeBusinessPayroll = largeBusinessFactory.createPayroll();
        Benefits largeBusinessBenefits = largeBusinessFactory.createBenefits();
        largeBusinessPayroll.processPayroll();
        largeBusinessBenefits.manageBenefits();
    }
}
```

### Explanation of the Code:
- The **`EmployeeFactory`** is the **Abstract Factory** that declares the methods for creating related products (Payroll and Benefits).
- **`SmallBusinessFactory`** and **`LargeBusinessFactory`** are concrete factories that implement the `EmployeeFactory` interface. They create specific products (payroll and benefits) for small and large businesses.
- **`Payroll`** and **`Benefits`** are abstract products, and `SmallBusinessPayroll`, `SmallBusinessBenefits`, `LargeBusinessPayroll`, and `LargeBusinessBenefits` are concrete implementations of these products.
- The **client code** uses the factory methods to create the necessary objects (payroll and benefits) without knowing the exact class types, thus adhering to the Abstract Factory pattern.

### Benefits of Using Abstract Factory:
1. **Encapsulation of Object Creation**: You don't need to worry about the specifics of how objects are created.
2. **Flexibility**: You can easily add new types of businesses or product configurations without changing much in the existing code.
3. **Consistency**: Ensures that all objects in a family are created to work together (for instance, the payroll and benefits are always compatible for a given business type).

This structure is useful in your scenario of a payroll and HR management platform as it allows flexibility for various types of businesses to use the platform's services.

### Builder

### Prototype

### Singleton

---

## Structural Patterns

These patterns explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient.

### Adapter

### Bridge

### Composite

### Decorator

### Facade

### Flyweight

### Proxy

---

## Behavioral Patterns

These patterns are concerned with algorithms and the assignment of responsibilities between objects.

### Chain of Responsibility

### Command

### Iterator

### Mediator

### Memento

### Observer

### State

### Strategy

### Template Method

### Visitor
