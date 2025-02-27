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
### Composite Design Pattern

The **Composite Design Pattern** is a structural pattern that is used to treat individual objects and compositions of objects uniformly. It allows you to compose objects into tree-like structures to represent part-whole hierarchies. This pattern is particularly useful when you need to work with complex tree structures, and you want to treat both individual objects and groups of objects in the same way.

In the context of the Composite pattern:
- **Leaf**: Represents the basic object, which doesn’t have any children.
- **Composite**: Represents an object that contains other objects (both leaf and other composites).

Both **Leaf** and **Composite** share the same interface, so the client can treat individual objects and composite objects in the same way.

### Why Use the Composite Design Pattern in Document Management (e.g., Google Workspace)?

The Composite Design Pattern is particularly useful in **Document Management** because:
1. **Hierarchical Structure**: In a document management system, documents can have various components, such as paragraphs, sections, tables, images, etc. These components can be treated uniformly as individual objects or collections.
2. **Flexible Representation**: Documents may be simple or may have nested sub-documents. Using the Composite pattern allows you to handle both simple and complex documents using the same interface.
3. **Ease of Manipulation**: You can easily perform operations such as editing, adding, or deleting items (e.g., text, images, tables) in documents that may contain other documents.
4. **Unified Operations**: In a system like Google Workspace, where documents can have varied content types (e.g., Docs, Sheets, Slides), the Composite Pattern allows for treating all elements (text, tables, slides, etc.) as a part of a unified structure.

### Example of the Composite Design Pattern in Document Management

Let’s implement a simple Java example to demonstrate how the **Composite Design Pattern** could be applied to a document management system in the context of Google Workspace. The idea is to simulate documents that may contain other documents or various components like paragraphs, images, and tables.

Here’s the Java code for a simple **Document Management System** using the Composite Pattern:

```java
import java.util.ArrayList;
import java.util.List;

// Component Interface
interface DocumentComponent {
    void display();
}

// Leaf: Represents a simple Document Component (e.g., Text, Image, etc.)
class Text implements DocumentComponent {
    private String content;
    
    public Text(String content) {
        this.content = content;
    }

    @Override
    public void display() {
        System.out.println("Text: " + content);
    }
}

// Leaf: Represents another type of Document Component (e.g., Image, Table, etc.)
class Image implements DocumentComponent {
    private String imageName;
    
    public Image(String imageName) {
        this.imageName = imageName;
    }

    @Override
    public void display() {
        System.out.println("Image: " + imageName);
    }
}

// Composite: Represents a Document or a Container for multiple Document Components
class Document implements DocumentComponent {
    private String title;
    private List<DocumentComponent> components = new ArrayList<>();

    public Document(String title) {
        this.title = title;
    }

    public void addComponent(DocumentComponent component) {
        components.add(component);
    }

    public void removeComponent(DocumentComponent component) {
        components.remove(component);
    }

    @Override
    public void display() {
        System.out.println("Document Title: " + title);
        for (DocumentComponent component : components) {
            component.display();
        }
    }
}

public class CompositePatternExample {
    public static void main(String[] args) {
        // Create individual components (Leaf objects)
        DocumentComponent text1 = new Text("This is the first paragraph of the document.");
        DocumentComponent text2 = new Text("This is the second paragraph with more details.");
        DocumentComponent image1 = new Image("image1.jpg");
        
        // Create a document (Composite)
        Document document = new Document("My Google Document");
        
        // Add components (text and images) to the document
        document.addComponent(text1);
        document.addComponent(text2);
        document.addComponent(image1);
        
        // Display the document structure
        document.display();
        
        // Create another nested document (Composite inside Composite)
        Document subDocument = new Document("Subdocument");
        subDocument.addComponent(new Text("This is a subdocument with some content."));
        
        // Add subdocument to the main document
        document.addComponent(subDocument);
        
        // Display the updated document structure
        System.out.println("\nUpdated Document:");
        document.display();
    }
}
```

### Explanation:
1. **DocumentComponent**: This is the common interface that both leaf nodes (like `Text`, `Image`) and composite nodes (like `Document`) will implement.
2. **Text and Image**: These are leaf components, representing individual items within a document (e.g., paragraphs, images).
3. **Document**: This is the composite class, which can hold other `DocumentComponent` instances, including other `Documents`. This allows creating nested structures.
4. The `display()` method is implemented by both the leaf and composite classes, making it easy to process documents in a uniform way.

### Output:
```
Document Title: My Google Document
Text: This is the first paragraph of the document.
Text: This is the second paragraph with more details.
Image: image1.jpg

Updated Document:
Document Title: My Google Document
Text: This is the first paragraph of the document.
Text: This is the second paragraph with more details.
Image: image1.jpg
Document Title: Subdocument
Text: This is a subdocument with some content.
```

### Conclusion:
This design pattern allows for flexible document structures that can easily accommodate complex documents, where each document can contain other documents or individual components like text and images. This type of structure is ideal for document management systems like Google Workspace, where different types of content can be combined and treated uniformly.

Using the Composite Design Pattern, Google Workspace’s document editing system (like Google Docs) can manage and display complex documents with nested content (e.g., images, text, tables, and sub-documents) in a structured, easy-to-manage way.
### Decorator

### Decorator Design Pattern Overview

The **Decorator Design Pattern** is a structural design pattern used to dynamically add new functionality to an object at runtime without altering its structure. The main idea is to "decorate" an object by adding behavior to it through composition, rather than inheritance. This allows for greater flexibility, as new functionality can be added to an object without modifying its class, making the system more scalable and easier to maintain.

Key characteristics of the Decorator Pattern:
- **Component Interface**: Defines the common interface for both the core object and its decorators.
- **Concrete Component**: The class that implements the component interface and represents the original object.
- **Decorator**: A class that wraps the original object and implements the same interface. It adds additional functionality while still passing calls to the original object.
- **Concrete Decorators**: These are specific implementations of the decorator class that add new behavior or modify existing behavior.

### Why Use the Decorator Design Pattern in Document Management: Google Workspace?

In systems like Google Workspace (Docs, Sheets, etc.), documents often require a variety of dynamic features or behaviors, such as formatting, security features, or real-time collaboration. The Decorator Design Pattern is useful in such contexts for the following reasons:

1. **Dynamic Behavior Addition**: In document management, there could be a need to add functionalities like tracking, access control, or version history to a document. With the decorator pattern, you can add these features dynamically without changing the original document object.

2. **Open/Closed Principle**: The decorator allows you to adhere to the open/closed principle, where the document classes are open for extension but closed for modification. You can keep extending document functionality as needed, without touching the core classes of the system.

3. **Flexibility and Reusability**: You can create various decorators to handle different requirements (e.g., logging, editing, sharing), and they can be composed together as needed, allowing flexibility in different scenarios.

### Example: Decorator Pattern in Learning Management Systems (LMS) - Moodle

Let’s look at how the Decorator Design Pattern can be applied to a Learning Management System (LMS) like **Moodle**. Imagine you have a basic `Assignment` object in Moodle, but you want to extend its functionality to support different features, such as grading, deadline extensions, or plagiarism checks.

#### Key Components:
1. **Assignment Interface**: Defines the common methods for all types of assignments.
2. **Concrete Assignment**: Implements the basic functionality for an assignment (e.g., submitting assignments).
3. **Decorator Classes**: Add features like grading, plagiarism checking, etc.
4. **Concrete Decorators**: Specific decorators that add particular behaviors.

#### Java Example Code

```java
// Component: The common interface for Assignment
interface Assignment {
    void submit();
}

// Concrete Component: Basic Assignment
class BasicAssignment implements Assignment {
    @Override
    public void submit() {
        System.out.println("Assignment submitted.");
    }
}

// Decorator: The abstract decorator class
abstract class AssignmentDecorator implements Assignment {
    protected Assignment decoratedAssignment;

    public AssignmentDecorator(Assignment decoratedAssignment) {
        this.decoratedAssignment = decoratedAssignment;
    }

    public void submit() {
        decoratedAssignment.submit();  // Call the wrapped assignment's submit method
    }
}

// Concrete Decorator 1: Adds Grading functionality
class GradingDecorator extends AssignmentDecorator {
    public GradingDecorator(Assignment decoratedAssignment) {
        super(decoratedAssignment);
    }

    @Override
    public void submit() {
        super.submit(); // Submit the assignment
        addGrading();
    }

    private void addGrading() {
        System.out.println("Grading has been added to the assignment.");
    }
}

// Concrete Decorator 2: Adds Plagiarism Check functionality
class PlagiarismCheckDecorator extends AssignmentDecorator {
    public PlagiarismCheckDecorator(Assignment decoratedAssignment) {
        super(decoratedAssignment);
    }

    @Override
    public void submit() {
        super.submit(); // Submit the assignment
        performPlagiarismCheck();
    }

    private void performPlagiarismCheck() {
        System.out.println("Plagiarism check completed.");
    }
}

// Concrete Decorator 3: Adds Deadline Extension functionality
class DeadlineExtensionDecorator extends AssignmentDecorator {
    public DeadlineExtensionDecorator(Assignment decoratedAssignment) {
        super(decoratedAssignment);
    }

    @Override
    public void submit() {
        super.submit(); // Submit the assignment
        extendDeadline();
    }

    private void extendDeadline() {
        System.out.println("Deadline has been extended.");
    }
}

// Client code
public class LMS {
    public static void main(String[] args) {
        // A basic assignment
        Assignment basicAssignment = new BasicAssignment();

        // Add grading functionality
        Assignment gradedAssignment = new GradingDecorator(basicAssignment);

        // Add plagiarism check to the already graded assignment
        Assignment plagiarizedCheckedAssignment = new PlagiarismCheckDecorator(gradedAssignment);

        // Add deadline extension to the plagiarized checked assignment
        Assignment finalAssignment = new DeadlineExtensionDecorator(plagiarizedCheckedAssignment);

        // Submit the fully decorated assignment
        finalAssignment.submit();
    }
}
```

### Explanation:

- **BasicAssignment**: This is the base assignment with basic functionality (submission).
- **GradingDecorator**: Adds grading functionality to the assignment.
- **PlagiarismCheckDecorator**: Adds plagiarism checking to the assignment.
- **DeadlineExtensionDecorator**: Adds functionality for extending the assignment deadline.

The **finalAssignment** object, which has been decorated with all three decorators, will have all the features combined. The decorators are applied in a flexible and reusable way, allowing them to be stacked as needed, without changing the core `Assignment` class.

### Advantages of Using the Decorator Pattern in LMS like Moodle:

1. **Extensibility**: The LMS can easily add new features without modifying existing code. For example, a new decorator can be created to add a feature like `AutoGradingDecorator` without altering other functionality.
2. **Separation of Concerns**: Each decorator is focused on adding a single responsibility (e.g., grading, plagiarism check), making the code modular and easier to maintain.
3. **Flexibility**: Users can combine different decorators for assignments depending on the needs of the course. One assignment might need grading and plagiarism checking, while another might just need a deadline extension.
4. **Open/Closed Principle**: The assignment class itself is not modified. New behaviors are added only by extending the functionality through decorators, ensuring that the system is open for extension but closed for modification.

In summary, the **Decorator Pattern** in the context of a learning management system like Moodle provides an elegant way to extend functionality without changing the core code, offering flexibility and scalability.

### Facade

### What is the Facade Design Pattern?

The **Facade Design Pattern** is a structural design pattern that provides a simplified interface to a complex subsystem. Instead of exposing the complexities of multiple classes or components, a facade class is created to provide a unified, high-level interface that hides the details of the underlying system. The goal is to simplify interactions with complex systems or subsystems.

In essence, it acts as a "wrapper" around a set of interfaces, enabling easier use and reducing the complexity exposed to the client.

### Why Use the Facade Design Pattern in Help Desk/Customer Support?

In a customer support or help desk system, various subsystems or components like ticket management, live chat, reporting, notifications, and knowledge base are involved. These systems may have complex APIs and operations, making it difficult for customer support agents or other users to interact with them efficiently.

Using the **Facade Design Pattern** simplifies this by providing a single interface through which the customer support team can interact with the various components of the system. This approach makes it easier to manage the system, improve efficiency, and hide the underlying complexity.

### Example: Applying the Facade Design Pattern in a Help Desk System

Imagine a help desk system where multiple subsystems are involved, like:

- **Zendesk** for ticket management.
- **Freshdesk** for live chat and email support.
- A **Knowledge Base** subsystem for customer support articles.

Without a facade, an agent might need to interact with each subsystem individually. Using the **Facade Design Pattern**, we can create a facade that abstracts and unifies interactions with these subsystems.

### Example: Working Java Code for Help Desk/Customer Support Using Facade Design Pattern

Here’s a simplified example in Java, where a **HelpDeskFacade** class provides a simplified interface for interacting with Zendesk, Freshdesk, and a KnowledgeBase system:

```java
// Subsystem 1: Zendesk
class Zendesk {
    public void createTicket(String issueDetails) {
        System.out.println("Creating ticket in Zendesk: " + issueDetails);
    }
}

// Subsystem 2: Freshdesk
class Freshdesk {
    public void startLiveChat(String customerName) {
        System.out.println("Starting live chat with " + customerName + " in Freshdesk");
    }

    public void sendEmail(String emailAddress, String message) {
        System.out.println("Sending email to " + emailAddress + " via Freshdesk: " + message);
    }
}

// Subsystem 3: KnowledgeBase
class KnowledgeBase {
    public void searchArticle(String query) {
        System.out.println("Searching for article related to: " + query);
    }
}

// Facade: HelpDeskFacade
class HelpDeskFacade {
    private Zendesk zendesk;
    private Freshdesk freshdesk;
    private KnowledgeBase knowledgeBase;

    public HelpDeskFacade() {
        zendesk = new Zendesk();
        freshdesk = new Freshdesk();
        knowledgeBase = new KnowledgeBase();
    }

    // Simplified method for handling customer issue
    public void handleCustomerIssue(String customerName, String issueDetails, String emailAddress) {
        // Interacting with multiple subsystems through a single facade
        zendesk.createTicket(issueDetails);
        freshdesk.startLiveChat(customerName);
        freshdesk.sendEmail(emailAddress, "We are looking into your issue.");
        knowledgeBase.searchArticle(issueDetails);
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        HelpDeskFacade helpDeskFacade = new HelpDeskFacade();
        
        // Customer has an issue
        String customerName = "John Doe";
        String issueDetails = "Unable to log in to the platform.";
        String emailAddress = "john.doe@example.com";
        
        // Use the facade to handle the issue
        helpDeskFacade.handleCustomerIssue(customerName, issueDetails, emailAddress);
    }
}
```

### Explanation of the Code:

1. **Subsystems (Zendesk, Freshdesk, KnowledgeBase):**
  - These are the individual subsystems that interact with specific functionalities like ticket creation, live chat, and searching articles.

2. **Facade (HelpDeskFacade):**
  - The **HelpDeskFacade** class simplifies the interaction with the subsystems. It offers a single method, `handleCustomerIssue`, that encapsulates the process of creating a ticket, starting live chat, sending an email, and searching for relevant knowledge base articles.

3. **Client:**
  - The client (e.g., a customer support representative) interacts only with the **HelpDeskFacade**, which simplifies the process of dealing with multiple subsystems. The client doesn’t need to know the details of how each subsystem works; it just calls the `handleCustomerIssue` method.

### Benefits of Using the Facade Design Pattern in Help Desk/Customer Support:
1. **Simplified Interaction:**
  - By providing a unified interface, the customer support agent interacts with the facade, not the individual subsystems.

2. **Reduced Complexity:**
  - Agents don't need to learn about the intricate details of the underlying systems (e.g., Zendesk or Freshdesk). They focus only on solving customer issues.

3. **Flexibility and Maintainability:**
  - The facade can be modified without affecting the client code, making it easier to maintain and scale. For example, if a new subsystem is added, the facade can integrate it without changing the way the client interacts with the system.

4. **Code Organization:**
  - The pattern helps to organize code better, especially when dealing with a large number of subsystems or external services. It isolates the complex subsystem code, making the system easier to debug and maintain.

### Conclusion:

In customer support systems, using the **Facade Design Pattern** significantly enhances the ease of use for support agents, making it simpler to interact with various tools like Zendesk, Freshdesk, and KnowledgeBase systems. By hiding the complexity behind a simple interface, the design pattern helps improve productivity, reduces errors, and makes the system easier to maintain.

### Flyweight
### Flyweight Design Pattern

The **Flyweight Design Pattern** is a structural design pattern that focuses on minimizing memory usage by sharing common parts of the state between multiple objects. It is especially useful when dealing with a large number of objects that have some shared intrinsic state but also some unique extrinsic state. The main idea is to avoid storing the common part of the state for each object and instead share it across many objects.

In essence, the Flyweight pattern breaks objects into two parts:
1. **Intrinsic State**: The part of the state that is shared and immutable across all instances of the object.
2. **Extrinsic State**: The part of the state that is unique to each instance and can vary depending on the context.

By using the Flyweight pattern, you save memory, as you don’t need to duplicate the intrinsic state for each object instance.

### Why Use the Flyweight Design Pattern in Help Desk/Customer Support?

In a help desk or customer support system, you can face many instances of similar requests or tickets with shared states, such as:
- Request categories (e.g., Billing, Technical Support, etc.)
- Common solutions or responses
- Frequently used templates for tickets
- Shared information across multiple support agents

The Flyweight pattern can be used to manage these shared components more efficiently by ensuring they are not duplicated unnecessarily, thus improving performance and reducing memory usage.

**Benefits in Help Desk/Customer Support:**
- **Reduced Memory Usage**: Instead of creating new objects for each request with the same data, shared objects can be reused.
- **Better Performance**: When handling a large number of requests, the system can be more responsive since it reuses existing objects instead of creating new ones.
- **Efficient Data Management**: You can centralize common information and resources like templates, support responses, and ticket categories.

### Example: Working Java Code for ShipBob Using Flyweight Pattern

Let's assume ShipBob provides an inventory management and logistics platform, and we want to use the Flyweight pattern to optimize memory usage when handling various orders. For simplicity, we will assume that each order has a shared state (like product information) and an extrinsic state (like order tracking details).

**Step 1: Create the Flyweight Interface**

```java
public interface Order {
    void processOrder(String orderDetails);
}
```

**Step 2: Concrete Flyweight (Shared State)**

```java
public class ProductOrder implements Order {
    private final String productName; // Shared state

    public ProductOrder(String productName) {
        this.productName = productName;
    }

    @Override
    public void processOrder(String orderDetails) {
        System.out.println("Processing order for: " + productName + " with details: " + orderDetails);
    }
}
```

**Step 3: Flyweight Factory**

```java
import java.util.HashMap;
import java.util.Map;

public class OrderFactory {
    private static final Map<String, Order> productOrders = new HashMap<>();

    public static Order getProductOrder(String productName) {
        if (!productOrders.containsKey(productName)) {
            productOrders.put(productName, new ProductOrder(productName));
        }
        return productOrders.get(productName);
    }
}
```

**Step 4: Client Code**

```java
public class ShipBobClient {
    public static void main(String[] args) {
        // Shared intrinsic state for the product
        Order order1 = OrderFactory.getProductOrder("Laptop");
        Order order2 = OrderFactory.getProductOrder("Laptop"); // This will reuse the same object

        // Extrinsic state for each order
        order1.processOrder("Order ID: 001, Quantity: 2, Shipping: Standard");
        order2.processOrder("Order ID: 002, Quantity: 1, Shipping: Expedited");
        
        // Order with different product
        Order order3 = OrderFactory.getProductOrder("Smartphone");
        order3.processOrder("Order ID: 003, Quantity: 5, Shipping: Same Day");
    }
}
```

### Explanation of Code:
- **ProductOrder** represents a concrete implementation of the **Flyweight** interface, with the **product name** as the intrinsic state shared between orders.
- The **OrderFactory** class manages the creation and reuse of shared `ProductOrder` objects. If an order with the same product name exists, it returns the same object from the map, otherwise, it creates a new one.
- In **ShipBobClient**, different orders are processed using shared product information, but the order details (quantity, shipping type) are unique to each instance, representing the extrinsic state.

### Key Takeaways:
- **Intrinsic state** (product name) is shared and only one object is created for each unique product name.
- **Extrinsic state** (order details) is passed as a parameter when processing the order and is unique for each order.
- The **Flyweight pattern** allows you to handle a large number of orders more efficiently by reusing the product objects while keeping memory usage low.

This pattern is ideal for systems like ShipBob’s where there are a large number of orders, many of which have similar product information but differ in details like quantity, shipping, or customer data.
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
