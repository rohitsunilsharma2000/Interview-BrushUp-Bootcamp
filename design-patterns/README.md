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

The **Builder** design pattern is one of the **Creational Design Patterns** that provides a way to construct a complex object step by step. It allows you to create objects with different representations using the same construction process.

In simpler terms, the **Builder pattern** allows the creation of an object with a lot of configuration options (fields), without having to deal with complex constructors or multiple parameters. It helps in scenarios where you want to build complex objects, like in your case, a cloud-based accounting software with various features (e.g., invoicing, payroll, reporting, etc.).

In Java, the **Builder pattern** is typically used when creating objects with many optional fields, providing a clean and readable way to construct those objects.

---

### Java Code Example for Builder Pattern in a Cloud-Based Accounting Software

Below is a simplified example where we build a `CloudAccountingSoftware` object that includes features like **invoicing**, **payroll**, and **financial reporting**.

#### Step-by-Step:

1. **Create a `CloudAccountingSoftware` class** with various properties for each feature.
2. **Create a Builder class** that constructs the `CloudAccountingSoftware` object.

```java
// CloudAccountingSoftware.java - The Product Class
public class CloudAccountingSoftware {
    private boolean invoicing;
    private boolean payroll;
    private boolean financialReporting;
    private String companyName;
    private String version;

    // Private constructor - Builder pattern forces users to use the builder
    private CloudAccountingSoftware(Builder builder) {
        this.invoicing = builder.invoicing;
        this.payroll = builder.payroll;
        this.financialReporting = builder.financialReporting;
        this.companyName = builder.companyName;
        this.version = builder.version;
    }

    // Getters for the fields
    public boolean isInvoicing() { return invoicing; }
    public boolean isPayroll() { return payroll; }
    public boolean isFinancialReporting() { return financialReporting; }
    public String getCompanyName() { return companyName; }
    public String getVersion() { return version; }

    // Builder Class
    public static class Builder {
        private boolean invoicing;
        private boolean payroll;
        private boolean financialReporting;
        private String companyName;
        private String version;

        // Required parameter: Company name
        public Builder(String companyName) {
            this.companyName = companyName;
        }

        // Optional parameters
        public Builder withInvoicing(boolean invoicing) {
            this.invoicing = invoicing;
            return this;
        }

        public Builder withPayroll(boolean payroll) {
            this.payroll = payroll;
            return this;
        }

        public Builder withFinancialReporting(boolean financialReporting) {
            this.financialReporting = financialReporting;
            return this;
        }

        public Builder withVersion(String version) {
            this.version = version;
            return this;
        }

        // Build method to create the CloudAccountingSoftware instance
        public CloudAccountingSoftware build() {
            return new CloudAccountingSoftware(this);
        }
    }

    // toString method to display the details of the CloudAccountingSoftware
    @Override
    public String toString() {
        return "CloudAccountingSoftware{" +
                "invoicing=" + invoicing +
                ", payroll=" + payroll +
                ", financialReporting=" + financialReporting +
                ", companyName='" + companyName + '\'' +
                ", version='" + version + '\'' +
                '}';
    }
}
```

#### Explanation:

1. **CloudAccountingSoftware** - This is the main class that represents your accounting software. It contains features like invoicing, payroll, and financial reporting. These are boolean properties, but you can extend them further based on your needs.

2. **Builder** - The `Builder` class is responsible for constructing the `CloudAccountingSoftware` object. It has methods for each feature you want to include (invoicing, payroll, financial reporting) and a constructor for required parameters (company name). The builder follows a fluent interface pattern, allowing for method chaining.

3. **Build method** - The `build()` method creates the final `CloudAccountingSoftware` object using the set parameters.

#### How to Use it:

```java
public class Main {
    public static void main(String[] args) {
        // Creating an instance of CloudAccountingSoftware using the Builder pattern
        CloudAccountingSoftware software = new CloudAccountingSoftware.Builder("My Accounting Software")
                .withInvoicing(true)
                .withPayroll(true)
                .withFinancialReporting(true)
                .withVersion("1.0")
                .build();

        // Printing the created CloudAccountingSoftware object
        System.out.println(software);
    }
}
```

#### Output:

```
CloudAccountingSoftware{invoicing=true, payroll=true, financialReporting=true, companyName='My Accounting Software', version='1.0'}
```

---

### Why use the Builder pattern?

- **Clear and readable code**: Instead of passing a long list of parameters in a constructor, you can use the builder to construct an object with a clearer syntax.
- **Flexibility**: The builder allows you to specify only the properties you need, leaving others with default values. This is especially useful when building objects with many optional attributes.
- **Immutable Objects**: The object is immutable once it is created (you can't change its properties after it’s been built), which is a good practice when designing software systems, especially for cloud-based solutions.

---

### Final Thoughts:
This is a basic implementation of the Builder pattern in the context of a cloud-based accounting software. You can expand it with more features, validations, and additional configuration options as required. The Builder pattern is particularly useful in software systems where you need flexibility but want to avoid the complexity of multiple constructors or methods.

### Prototype

### What is a Prototype?

In software development, a **prototype** is an early version of a software application or system that demonstrates the core functionality of the system. Prototypes are often used in the early stages of a project to gather feedback from stakeholders and refine requirements. They help in understanding the system's design and usability before the full system is developed. Prototyping is often used in **rapid application development (RAD)** to iterate quickly and involve users early in the design process.

### Prototype in Object-Oriented Programming (OOP)

In the context of Object-Oriented Programming (OOP), the **Prototype design pattern** is a creational pattern used to clone objects, rather than creating them from scratch. This pattern allows the cloning of objects without making changes to their structure. This is useful in situations where creating a new object from scratch can be time-consuming or complex.

### Java Example for Cloud-Based Inventory and Order Management Software

To create a simple **cloud-based inventory and order management software** prototype, we will simulate the basic structure of the system. This will include:
- A `Product` class for tracking product details.
- An `Order` class to represent an order made by a customer.
- A simple `InventoryManager` to manage product inventory and orders.

Here’s a basic Java code to give you an idea of how to approach such a system:

```java
import java.util.*;

class Product {
    private String productId;
    private String name;
    private double price;
    private int stockQuantity;

    public Product(String productId, String name, double price, int stockQuantity) {
        this.productId = productId;
        this.name = name;
        this.price = price;
        this.stockQuantity = stockQuantity;
    }

    public String getProductId() {
        return productId;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public int getStockQuantity() {
        return stockQuantity;
    }

    public void reduceStock(int quantity) {
        if (quantity <= stockQuantity) {
            stockQuantity -= quantity;
        } else {
            System.out.println("Not enough stock for product: " + name);
        }
    }

    @Override
    public String toString() {
        return "Product ID: " + productId + ", Name: " + name + ", Price: $" + price + ", Stock: " + stockQuantity;
    }
}

class Order {
    private String orderId;
    private List<Product> orderedProducts;
    private double totalAmount;

    public Order(String orderId) {
        this.orderId = orderId;
        this.orderedProducts = new ArrayList<>();
        this.totalAmount = 0.0;
    }

    public void addProduct(Product product, int quantity) {
        if (product.getStockQuantity() >= quantity) {
            product.reduceStock(quantity);
            orderedProducts.add(product);
            totalAmount += product.getPrice() * quantity;
        } else {
            System.out.println("Not enough stock for: " + product.getName());
        }
    }

    public void displayOrderDetails() {
        System.out.println("Order ID: " + orderId);
        System.out.println("Ordered Products:");
        for (Product product : orderedProducts) {
            System.out.println(product.getName() + " - $" + product.getPrice());
        }
        System.out.println("Total Amount: $" + totalAmount);
    }
}

class InventoryManager {
    private Map<String, Product> productCatalog;

    public InventoryManager() {
        this.productCatalog = new HashMap<>();
    }

    public void addProduct(Product product) {
        productCatalog.put(product.getProductId(), product);
    }

    public Product getProductById(String productId) {
        return productCatalog.get(productId);
    }

    public void displayInventory() {
        System.out.println("Current Inventory:");
        for (Product product : productCatalog.values()) {
            System.out.println(product);
        }
    }
}

public class CloudInventorySystem {
    public static void main(String[] args) {
        // Creating an instance of InventoryManager
        InventoryManager inventoryManager = new InventoryManager();
        
        // Adding some products to the inventory
        inventoryManager.addProduct(new Product("P001", "Laptop", 1200.00, 10));
        inventoryManager.addProduct(new Product("P002", "Headphones", 150.00, 50));
        inventoryManager.addProduct(new Product("P003", "Mouse", 25.00, 100));

        // Display current inventory
        inventoryManager.displayInventory();

        // Creating an order and adding products to it
        Order order1 = new Order("ORD1001");
        Product laptop = inventoryManager.getProductById("P001");
        Product headphones = inventoryManager.getProductById("P002");
        order1.addProduct(laptop, 2);  // Add 2 Laptops
        order1.addProduct(headphones, 5);  // Add 5 Headphones

        // Display the order details
        order1.displayOrderDetails();

        // Display updated inventory after order
        inventoryManager.displayInventory();
    }
}
```

### Explanation of the Code:

1. **Product Class**:
  - Represents a product in the inventory with attributes like `productId`, `name`, `price`, and `stockQuantity`.
  - Methods include `reduceStock()` to decrement stock and `toString()` to display product details.

2. **Order Class**:
  - Represents an order with an `orderId`, a list of ordered products, and a `totalAmount`.
  - Method `addProduct()` adds a product to the order, reduces stock in the inventory, and calculates the total order amount.
  - `displayOrderDetails()` displays the order's contents.

3. **InventoryManager Class**:
  - Manages the inventory by storing products in a `Map`.
  - Methods include `addProduct()` to add products to the catalog and `getProductById()` to retrieve a product by its ID.

4. **CloudInventorySystem Class**:
  - The `main` method runs a simple simulation where products are added to the inventory, an order is created, products are added to the order, and then the inventory and order details are displayed.

### What to Take from This Prototype

This simple prototype demonstrates the structure of an inventory and order management system. In a real-world cloud-based application, you'd likely have:
- A database for storing inventory and orders.
- A cloud backend (e.g., AWS, Google Cloud, or Azure) to handle business logic.
- APIs for interacting with the system, especially for order placement, inventory tracking, and automated workflows (e.g., re-ordering products when stock runs low).
- A user interface for interacting with the software.

For a beginner, this code serves as a basic starting point, and you can expand it by adding features like customer management, order status tracking, and real-time data synchronization with a cloud service.

Would you like to further explore any part of this prototype or expand it?

### Singleton
To give you an example of how a **Singleton** pattern could be applied in a context like **Microsoft Teams**, let’s consider a **TeamManager** class that is responsible for managing the communication channels, file sharing, and configuration of the application.

Let’s simulate how this might work in Java. We will focus on the **Singleton pattern** for the **TeamManager** class to ensure there is only one instance that controls the team communication and channels.

### Use Case Scenario
In a team collaboration tool like Microsoft Teams, there may be a need to ensure that there is a single instance of the **TeamManager** responsible for overseeing the whole platform (handling the chat channels, video conferences, file sharing, etc.). This helps in managing state and resources efficiently and ensures consistency across the application.

Here is a **Java code example** demonstrating how the Singleton Pattern might be used in such a scenario.

### Java Code Example: TeamManager Singleton

```java
// Singleton class for managing the Teams application
public class TeamManager {

    // Private static variable to hold the single instance of TeamManager
    private static TeamManager instance;

    // Private constructor to prevent instantiation from outside
    private TeamManager() {
        // Initialization of team communication resources could go here
        System.out.println("Initializing Team Manager...");
    }

    // Public method to get the instance of TeamManager (Singleton)
    public static TeamManager getInstance() {
        if (instance == null) {
            instance = new TeamManager();
        }
        return instance;
    }

    // Method to simulate creating a new communication channel
    public void createChannel(String channelName) {
        System.out.println("Creating a new channel: " + channelName);
    }

    // Method to simulate sending a message in a channel
    public void sendMessage(String message) {
        System.out.println("Sending message: " + message);
    }

    // Method to simulate file sharing
    public void shareFile(String fileName) {
        System.out.println("Sharing file: " + fileName);
    }

    // Method to simulate a video call
    public void startVideoCall() {
        System.out.println("Starting a video call...");
    }
}

public class Main {
    public static void main(String[] args) {
        // Accessing the Singleton instance of TeamManager
        TeamManager teamManager1 = TeamManager.getInstance();
        
        // Performing some actions
        teamManager1.createChannel("Marketing Team");
        teamManager1.sendMessage("Welcome to the Marketing Team Channel!");
        teamManager1.shareFile("Marketing Plan.docx");
        teamManager1.startVideoCall();

        // Accessing the Singleton again
        TeamManager teamManager2 = TeamManager.getInstance();
        
        // Verify both references point to the same instance
        System.out.println("Is the same instance: " + (teamManager1 == teamManager2)); // Should print true
    }
}
```

### Explanation:

1. **Singleton Class (`TeamManager`)**:
  - We use a **private static instance** (`instance`) to hold the single instance of the `TeamManager` class.
  - The **private constructor** ensures that the class cannot be instantiated from outside the class.
  - The `getInstance()` method provides a **global point of access** to the instance. It initializes the instance if it’s not created yet, making sure only one instance of `TeamManager` exists.

2. **Methods**:
  - `createChannel()`: Simulates the creation of a new communication channel (e.g., team channels in Microsoft Teams).
  - `sendMessage()`: Simulates sending a message within a channel.
  - `shareFile()`: Simulates sharing a file with the team.
  - `startVideoCall()`: Simulates initiating a video call.

3. **Usage**:
  - The `Main` class demonstrates how you can interact with the **Singleton** `TeamManager` and perform operations like creating channels, sending messages, and initiating video calls.
  - The code checks that `teamManager1` and `teamManager2` point to the same instance.

### Why Use Singleton in a Team Collaboration Tool Like Microsoft Teams?

- **Resource Management**: You don’t want to create multiple instances of the TeamManager when managing resources like communication channels, file sharing, or video calls. Having one instance ensures that resources are used efficiently and consistently.

- **Consistency**: Since only one instance exists, there is no risk of conflicting states or data in different parts of the application. This ensures that any changes made by the `TeamManager` instance (e.g., creating a new channel) are reflected globally.

- **Global Access**: The Singleton provides a **global point of access** to the `TeamManager`, ensuring that any part of the application can access and interact with the team collaboration features.

- **Scalability**: By limiting the instance creation, it simplifies the process of managing shared components like chat, file storage, or video calls. This is especially important when dealing with multiple users and communication resources.

### Key Benefits of Singleton Pattern in This Scenario:
1. **Efficient Resource Use**: The Singleton pattern ensures that the `TeamManager` class is not repeatedly instantiated, making resource management more efficient.
2. **Easy Access to Global State**: All parts of the application can easily access the single instance to perform tasks like sending messages, creating channels, or managing video calls.
3. **Thread-Safety**: In a multi-threaded environment, the Singleton pattern can be adapted to be thread-safe to ensure only one instance is created, preventing race conditions.

In large applications like Microsoft Teams, the Singleton pattern helps in controlling shared resources, ensuring that everything is consistent and that unnecessary duplication is avoided.
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
