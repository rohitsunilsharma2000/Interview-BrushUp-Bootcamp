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

### What is a Prototype Design pattern?

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

### **Adapter Design Pattern**

The **Adapter Design Pattern** is a structural design pattern used to enable compatibility between two incompatible interfaces. It allows classes with different interfaces to work together by providing a wrapper (adapter) that transforms the interface of a class into another expected by the client.

In simpler terms, an adapter "adapts" one class or object to another class or object by modifying the interface. It's particularly useful when integrating with external systems, libraries, or APIs that you can't modify but need to be compatible with the system you're building.

### **When to Use the Adapter Pattern?**
- When you need to integrate third-party classes or libraries that are incompatible with your system but cannot be modified.
- When you're working with legacy code and want to integrate it into a new system without modifying the legacy code.
- When you need to work with external services or APIs that provide data in a format (like XML, JSON, etc.) that needs to be transformed into something your application can understand.

### **Why Use the Adapter Pattern in SML, JSON, and Other Formats?**

In scenarios where you're consuming various formats like SML (Standard Meta Language), JSON, or other data formats, different systems might have incompatible structures or formats. The adapter pattern helps by providing a way to standardize how you consume these formats:

- **Different Formats**: If your application needs to process data in multiple formats like JSON and XML, but your processing logic only works with a specific format (e.g., JSON), an adapter can convert the data from XML or another format into the format your system expects.

- **Third-Party Integration**: When consuming external APIs that return data in a non-compatible format, the adapter can convert it into a structure your application can use seamlessly.

- **Loose Coupling**: By using an adapter, you can isolate the external system or format from your core business logic, allowing you to switch formats or services without major changes to the underlying application.

### **Example: Working Java Code for Adapter Pattern**

Let's imagine we need to work with a legacy system that provides data in XML, but our application uses JSON.

#### Step 1: The "Target" Interface
This is the interface that your application expects to work with. Let's say it expects a method to get the "user" data in a standardized format (JSON).

```java
// The interface that the client expects
public interface UserData {
    String getUserData();
}
```

#### Step 2: The "Adaptee" Class
This is the class that provides data in a non-compatible format (XML in this case).

```java
// The class we cannot change
public class XMLUserData {
    public String getXMLData() {
        return "<user><name>John Doe</name><age>30</age></user>";
    }
}
```

#### Step 3: The Adapter Class
The adapter class is the one that bridges the gap between the target and the adaptee.

```java
// The adapter class that adapts the XMLUserData to UserData
public class XMLUserDataAdapter implements UserData {
    private XMLUserData xmlUserData;

    public XMLUserDataAdapter(XMLUserData xmlUserData) {
        this.xmlUserData = xmlUserData;
    }

    @Override
    public String getUserData() {
        // Convert XML to a JSON representation (example, could use a library for real conversion)
        String xmlData = xmlUserData.getXMLData();
        // For simplicity, let's just manually convert it
        String jsonData = "{ \"name\": \"John Doe\", \"age\": 30 }";
        return jsonData;
    }
}
```

#### Step 4: Client Code
Now, the client can use the `UserData` interface, and it doesn't need to worry about whether the data is coming from an XML source, JSON source, or anything else. It just works with the adapter.

```java
// Client code that uses the adapter
public class Main {
    public static void main(String[] args) {
        XMLUserData xmlUserData = new XMLUserData();
        UserData userData = new XMLUserDataAdapter(xmlUserData); // Adapter being used
        System.out.println(userData.getUserData()); // Prints the JSON format
    }
}
```

### **Output:**
```json
{ "name": "John Doe", "age": 30 }
```

### **Why This Works**
- **Encapsulation**: The client doesn't need to know anything about how the XML data is structured or how it's being converted. It only works with the `UserData` interface, which is expected.
- **Reusability**: You can create different adapters for other data sources or formats (e.g., JSON to XML adapter) without changing the core business logic.
- **Separation of Concerns**: The XML handling is isolated inside the adapter class, so the client code is free of XML-related logic.

### **Conclusion**
The **Adapter Pattern** allows for flexibility when working with different data formats, enabling smooth interaction with external systems without altering their code or structure. By applying the adapter pattern, your system becomes more maintainable and scalable, particularly when dealing with multiple, possibly incompatible data formats like XML, JSON, or others.

### Bridge
### Bridge Design Pattern

The **Bridge Design Pattern** is a structural design pattern that is used to separate an abstraction from its implementation so that both can evolve independently. The goal of the Bridge pattern is to decouple the abstraction (what is being done) from the implementation (how it is done), allowing both to be modified or extended independently.

#### Key Concepts:
- **Abstraction**: This defines the high-level interface that delegates the work to the implementation.
- **Implementation**: This defines the low-level operations and functionality. It is independent of the abstraction.

In the Bridge pattern, the abstraction and implementation are linked using composition, allowing the client to work with the abstraction without being aware of the specific implementation.

### Why Use the Bridge Design Pattern in Marketing Management Software?

In a marketing management software system, such as an email marketing platform, there are often two main areas that could benefit from the Bridge pattern:
1. **Abstraction (High-Level Interface)**: The features or services that are available to the marketing team, such as creating email campaigns, sending emails, tracking analytics, customer segmentation, etc.
2. **Implementation (Low-Level Operations)**: The underlying details of how these features are executed, such as which email service is used to send emails, which analytics tool is used to track user actions, or which customer segmentation algorithm is applied.

The **Bridge pattern** would allow the high-level features (e.g., creating an email campaign or generating an analytics report) to be decoupled from the specific low-level implementation (e.g., sending an email using different email service providers or using different segmentation strategies).

By using the Bridge pattern, you can easily extend or modify the implementation without affecting the abstraction, and vice versa. For example, if you want to switch from one email service provider to another, the abstraction layer wouldn't need to change, but only the implementation layer would need to be updated.

### Example: Email Marketing Platform with the Bridge Design Pattern in Java

Below is a basic example where we use the **Bridge pattern** to model an email marketing platform. We'll use the **Bridge pattern** to separate the high-level operations of sending emails and tracking email campaigns (Abstraction) from the actual implementation details (the email service provider).

#### Java Code Example:

```java
// Implementor (Implementation)
interface EmailService {
    void sendEmail(String to, String subject, String body);
}

// Concrete Implementors
class SMTPService implements EmailService {
    @Override
    public void sendEmail(String to, String subject, String body) {
        System.out.println("Sending email via SMTP to " + to);
        // Logic for sending email via SMTP
    }
}

class SendGridService implements EmailService {
    @Override
    public void sendEmail(String to, String subject, String body) {
        System.out.println("Sending email via SendGrid to " + to);
        // Logic for sending email via SendGrid
    }
}

// Abstraction (High-Level Interface)
abstract class Campaign {
    protected EmailService emailService; // "Bridge" to the implementation

    public Campaign(EmailService emailService) {
        this.emailService = emailService;
    }

    public abstract void sendCampaign(String[] recipients, String subject, String body);
}

// Refined Abstraction (Extends the Abstract Campaign)
class PromotionalCampaign extends Campaign {
    public PromotionalCampaign(EmailService emailService) {
        super(emailService);
    }

    @Override
    public void sendCampaign(String[] recipients, String subject, String body) {
        for (String recipient : recipients) {
            emailService.sendEmail(recipient, subject, body);
        }
        System.out.println("Promotional campaign sent to all recipients.");
    }
}

class NewsletterCampaign extends Campaign {
    public NewsletterCampaign(EmailService emailService) {
        super(emailService);
    }

    @Override
    public void sendCampaign(String[] recipients, String subject, String body) {
        for (String recipient : recipients) {
            emailService.sendEmail(recipient, subject, body);
        }
        System.out.println("Newsletter campaign sent to all recipients.");
    }
}

// Client Code (Marketing Platform Usage)
public class EmailMarketingPlatform {
    public static void main(String[] args) {
        // Using different email service providers
        EmailService smtpService = new SMTPService();
        EmailService sendGridService = new SendGridService();

        // Using the Bridge to create campaigns
        Campaign promotionalCampaign = new PromotionalCampaign(smtpService);
        Campaign newsletterCampaign = new NewsletterCampaign(sendGridService);

        // Sending campaigns
        String[] recipients = {"customer1@example.com", "customer2@example.com"};
        promotionalCampaign.sendCampaign(recipients, "Big Discount on Your Favorite Products", "Don't miss this great offer!");
        newsletterCampaign.sendCampaign(recipients, "Monthly Newsletter", "Here are the latest updates from our company.");
    }
}
```

#### Explanation of the Code:
1. **EmailService (Implementor)**: This is the interface that defines the low-level operation of sending an email. Different classes (like `SMTPService` and `SendGridService`) implement this interface with their specific logic for sending emails.

2. **Campaign (Abstraction)**: This abstract class defines the high-level interface for sending a campaign. It holds a reference to the `EmailService` and delegates the actual email-sending task to the implementation. The `sendCampaign` method is abstract, and each subclass provides its own specific campaign behavior (like `PromotionalCampaign` or `NewsletterCampaign`).

3. **Refined Abstractions (PromotionalCampaign and NewsletterCampaign)**: These are concrete implementations of the `Campaign` class. They specify the type of campaign, but they delegate the actual task of sending emails to the `EmailService`.

4. **Client Code (EmailMarketingPlatform)**: The client code demonstrates how the `Bridge` pattern is used. It creates a campaign with a specific email service provider and sends the campaign to a list of recipients.

#### Advantages of Using the Bridge Pattern in This Example:
1. **Flexibility**: You can easily switch between different email service providers (e.g., SMTP vs. SendGrid) without changing the high-level campaign logic.
2. **Extendability**: You can add new types of campaigns (e.g., `SurveyCampaign`, `ProductLaunchCampaign`) without modifying the email service logic.
3. **Decoupling**: The abstraction (the campaign) is decoupled from the implementation (the email service), so both can evolve independently.

### Conclusion
In this example, the **Bridge pattern** allows the email marketing platform to separate the abstraction of campaign sending from the concrete implementations of email services. This makes the platform flexible and easier to maintain, as you can introduce new email services or change the campaign structure without impacting the other parts of the system. The **Adapter pattern** could be used in a similar context, but it's more suited for converting incompatible interfaces, whereas the **Bridge pattern** is ideal for decoupling abstraction and implementation.

### Composite

### Bridge Design Pattern Overview:

The **Bridge Design Pattern** is a structural design pattern that is used to separate the abstraction (interface) from the implementation. This allows the two to vary independently, making the system more flexible and easier to maintain.

In the Bridge pattern, there are two key components:

1. **Abstraction** – This defines the interface for the higher-level control. It usually contains a reference to an object that implements the **Implementor** interface.

2. **Implementor** – This defines the interface for the lower-level, platform-specific operations. It doesn't define the complete behavior, but rather the components that the Abstraction relies on.

By separating the abstraction from the implementation, we can change either one without affecting the other.

### Why Use the Bridge Design Pattern in Document Management (Google Workspace)?

In the context of **Document Management** and platforms like **Google Workspace**, the **Bridge Design Pattern** can be particularly useful in scenarios where:

- **Cross-platform compatibility**: If Google Docs or Google Sheets needs to be supported across multiple platforms (such as Android, iOS, Web), you can use the Bridge pattern to separate the abstraction of document management features (e.g., editing, saving) from the platform-specific implementations (e.g., Google Drive integration, offline support).

- **Modularization and Scalability**: Google Workspace services are evolving rapidly, and the Bridge pattern allows for easier updates and scaling. You can change the implementation of the backend (e.g., from Google Drive API to another cloud storage system) without affecting the document management system's interface.

- **Extending functionality**: As new features are added (e.g., document sharing, version control), the Bridge pattern allows you to implement these features with minimal disruption to existing code, as the abstraction layer can be extended while keeping the implementation layer separate.

### Example: Using the Bridge Pattern in Document Management (Google Workspace)

Let’s say we want to create a simple document management system where we can edit and save documents, but we need to support multiple platforms. We’ll separate the abstraction of document management (e.g., editing) from the implementation (e.g., saving to Google Drive, saving to Dropbox, or saving locally).

Here is an example of how we could implement this pattern in **Java**:

#### Step 1: Define the `Document` Abstraction

This represents the higher-level abstraction for document management.

```java
// Abstraction
public abstract class Document {
    protected Storage storage;

    // Constructor injecting the Implementor (Storage)
    public Document(Storage storage) {
        this.storage = storage;
    }

    public abstract void edit();
    public abstract void save();
}
```

#### Step 2: Define the `Storage` Implementor Interface

This is the interface for the lower-level implementation (e.g., saving to Google Drive, Dropbox, or local storage).

```java
// Implementor
public interface Storage {
    void saveDocument(String content);
}
```

#### Step 3: Concrete Implementors (e.g., Google Drive, Dropbox)

These are the specific implementations of the `Storage` interface.

```java
// Concrete Implementor - GoogleDriveStorage
public class GoogleDriveStorage implements Storage {
    @Override
    public void saveDocument(String content) {
        System.out.println("Saving document to Google Drive: " + content);
    }
}

// Concrete Implementor - DropboxStorage
public class DropboxStorage implements Storage {
    @Override
    public void saveDocument(String content) {
        System.out.println("Saving document to Dropbox: " + content);
    }
}

// Concrete Implementor - LocalStorage
public class LocalStorage implements Storage {
    @Override
    public void saveDocument(String content) {
        System.out.println("Saving document locally: " + content);
    }
}
```

#### Step 4: Concrete Document Classes

These classes represent different types of documents that need to be edited and saved.

```java
// Refined Abstraction - WordDocument
public class WordDocument extends Document {
    private String content;

    public WordDocument(Storage storage, String content) {
        super(storage);
        this.content = content;
    }

    @Override
    public void edit() {
        System.out.println("Editing Word Document: " + content);
    }

    @Override
    public void save() {
        System.out.println("Saving Word Document...");
        storage.saveDocument(content);
    }
}

// Refined Abstraction - SpreadsheetDocument
public class SpreadsheetDocument extends Document {
    private String content;

    public SpreadsheetDocument(Storage storage, String content) {
        super(storage);
        this.content = content;
    }

    @Override
    public void edit() {
        System.out.println("Editing Spreadsheet: " + content);
    }

    @Override
    public void save() {
        System.out.println("Saving Spreadsheet Document...");
        storage.saveDocument(content);
    }
}
```

#### Step 5: Client Code

Here’s how you could use the Bridge pattern to create a document and save it to different platforms (e.g., Google Drive, Dropbox, local storage).

```java
public class BridgePatternExample {
    public static void main(String[] args) {
        // Create storage implementors
        Storage googleDriveStorage = new GoogleDriveStorage();
        Storage dropboxStorage = new DropboxStorage();
        Storage localStorage = new LocalStorage();

        // Create documents with different storage options
        Document wordDocument1 = new WordDocument(googleDriveStorage, "Google Docs Content");
        Document wordDocument2 = new WordDocument(dropboxStorage, "Dropbox Docs Content");
        Document spreadsheet1 = new SpreadsheetDocument(localStorage, "Local Spreadsheet Content");

        // Edit and save documents
        wordDocument1.edit();
        wordDocument1.save();

        wordDocument2.edit();
        wordDocument2.save();

        spreadsheet1.edit();
        spreadsheet1.save();
    }
}
```

#### Output:
```
Editing Word Document: Google Docs Content
Saving Word Document...
Saving document to Google Drive: Google Docs Content
Editing Word Document: Dropbox Docs Content
Saving Word Document...
Saving document to Dropbox: Dropbox Docs Content
Editing Spreadsheet: Local Spreadsheet Content
Saving Spreadsheet Document...
Saving document locally: Local Spreadsheet Content
```

### Conclusion:

- **Flexibility and Extensibility**: The Bridge Design Pattern helps in creating flexible systems where the abstraction (document editing) and implementation (storage solutions like Google Drive, Dropbox, etc.) can evolve independently.

- **Adaptability**: If you want to introduce a new document type or add a new storage solution, the Bridge pattern allows you to do so without modifying existing code, promoting the **Open/Closed Principle** (open for extension, closed for modification).

- **Separation of Concerns**: It allows developers to keep the concerns of editing documents and storing them separate, which simplifies the management and maintenance of the code.

This pattern is particularly useful in large systems like Google Workspace where multiple features (editing, saving, sharing) can be easily extended to various platforms.


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
