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
