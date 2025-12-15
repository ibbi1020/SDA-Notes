# Gang of Four (GoF) Design Patterns

The **Gang of Four (GoF)** patterns are a collection of 23 classic software design patterns from the book *"Design Patterns: Elements of Reusable Object-Oriented Software"*. They are categorized into Creational, Structural, and Behavioral patterns.

Here are notes on six essential GoF patterns, structured similarly to the GRASP patterns, with Java examples.

---

## 1. 🏭 Factory Method (Creational)

*   **What it's for (Problem):**
    How can a class instantiate objects of classes it needs to use, without knowing the exact class of the object it needs to create? How do we avoid tight coupling to specific concrete classes?
*   **How to apply it (Solution):**
    Define an interface (or abstract class) for creating an object, but let subclasses decide which class to instantiate. The Factory Method lets a class defer instantiation to subclasses.
*   **Java Example:**
    Imagine a logistics app that handles different types of transport.

```java
// 1. The Product Interface
interface Transport {
    void deliver();
}

// 2. Concrete Products
class Truck implements Transport {
    public void deliver() { System.out.println("Delivering by land in a box."); }
}

class Ship implements Transport {
    public void deliver() { System.out.println("Delivering by sea in a container."); }
}

// 3. The Creator (Factory)
abstract class Logistics {
    // The Factory Method
    abstract Transport createTransport();

    // Core business logic uses the product interface
    public void planDelivery() {
        Transport t = createTransport();
        t.deliver();
    }
}

// 4. Concrete Creators
class RoadLogistics extends Logistics {
    @Override
    Transport createTransport() {
        return new Truck();
    }
}

class SeaLogistics extends Logistics {
    @Override
    Transport createTransport() {
        return new Ship();
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Logistics logistics = new RoadLogistics();
        logistics.planDelivery(); // Output: Delivering by land in a box.
    }
}
```

*   **Benefits:**
    *   **Decoupling:** The creator code (`Logistics`) is decoupled from the concrete products (`Truck`, `Ship`).
    *   **Extensibility:** Adding a new transport type (e.g., `Plane`) doesn't change the core `Logistics` logic.

---

## 2. 🦄 Singleton (Creational)

*   **What it's for (Problem):**
    How do we ensure that a class has only **one instance** and provide a global point of access to it? (e.g., Database connection, Configuration manager).
*   **How to apply it (Solution):**
    Make the class constructor `private`. Create a `static` variable to hold the single instance and a `public static` method to return it.
*   **Java Example:**

```java
class DatabaseConnection {
    // 1. Static variable to hold the single instance
    private static DatabaseConnection instance;

    // 2. Private constructor prevents instantiation from other classes
    private DatabaseConnection() {
        System.out.println("Connecting to Database...");
    }

    // 3. Public static method to provide global access
    public static DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }

    public void query(String sql) {
        System.out.println("Executing: " + sql);
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        // DatabaseConnection db = new DatabaseConnection(); // Error! Constructor is private.
        
        DatabaseConnection db1 = DatabaseConnection.getInstance();
        db1.query("SELECT * FROM users");
        
        DatabaseConnection db2 = DatabaseConnection.getInstance();
        // db1 and db2 are the EXACT same object.
    }
}
```

*   **Benefits:**
    *   Controlled access to a sole instance.
    *   Reduced namespace pollution (avoids global variables).
*   **Contraindications:**
    *   Can make unit testing difficult (global state).
    *   Can hide dependencies.

---

## 3. 🔌 Adapter (Structural)

*   **What it's for (Problem):**
    How can classes with incompatible interfaces work together? How can we use an existing class (e.g., a 3rd party library) that doesn't match the interface our code expects?
*   **How to apply it (Solution):**
    Create a wrapper class (the Adapter) that implements the interface the client expects and translates the calls to the wrapped object (the Adaptee).
*   **Java Example:**
    We have a `Bird` interface, but we want to use a `PlasticToyDuck` in our bird simulation.

```java
// Target Interface
interface Bird {
    void makeSound();
}

class Sparrow implements Bird {
    public void makeSound() { System.out.println("Chirp Chirp"); }
}

// Adaptee (Incompatible interface)
class PlasticToyDuck {
    public void squeak() { System.out.println("Squeak"); }
}

// Adapter
class BirdAdapter implements Bird {
    private PlasticToyDuck toyDuck;

    public BirdAdapter(PlasticToyDuck toyDuck) {
        this.toyDuck = toyDuck;
    }

    @Override
    public void makeSound() {
        // Translate the call
        toyDuck.squeak();
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        PlasticToyDuck toy = new PlasticToyDuck();
        Bird birdAdapter = new BirdAdapter(toy);

        birdAdapter.makeSound(); // Output: Squeak
        // The client code thinks it's treating a Bird, but it's actually a ToyDuck.
    }
}
```

*   **Benefits:**
    *   Allows reuse of existing code without modifying it.
    *   Decouples the client from the specific implementation of the adaptee.

---

## 4. 🎭 Facade (Structural)

*   **What it's for (Problem):**
    How do we provide a simple interface to a complex subsystem (a set of many classes)?
*   **How to apply it (Solution):**
    Create a `Facade` class that provides a simplified, higher-level interface. The facade delegates the actual work to the complex subsystem classes.
*   **Java Example:**
    Starting a computer involves complex interactions between CPU, Memory, and Hard Drive.

```java
// Complex Subsystem Parts
class CPU {
    void freeze() { System.out.println("CPU Frozen"); }
    void execute() { System.out.println("CPU Executing commands"); }
}

class Memory {
    void load(long position, String data) { System.out.println("Memory loading: " + data); }
}

class HardDrive {
    String read(long lba, int size) { return "OS Boot Data"; }
}

// Facade
class ComputerFacade {
    private CPU cpu;
    private Memory ram;
    private HardDrive hd;

    public ComputerFacade() {
        this.cpu = new CPU();
        this.ram = new Memory();
        this.hd = new HardDrive();
    }

    public void startComputer() {
        System.out.println("--- Starting Computer ---");
        cpu.freeze();
        String bootData = hd.read(0, 1024);
        ram.load(0, bootData);
        cpu.execute();
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        ComputerFacade computer = new ComputerFacade();
        computer.startComputer(); 
        // Client doesn't need to know about CPU, RAM, or HD details.
    }
}
```

*   **Benefits:**
    *   Simplifies the usage of a complex system for the client.
    *   Decouples the client from the subsystem components.

---

## 5. 👀 Observer (Behavioral)

*   **What it's for (Problem):**
    How can a one-to-many dependency be defined between objects so that when one object changes state, all its dependents are notified and updated automatically?
*   **How to apply it (Solution):**
    Define a `Subject` (Publisher) that maintains a list of `Observer` (Subscriber) objects. When the Subject's state changes, it iterates through the list and calls an `update()` method on each Observer.
*   **Java Example:**
    A YouTube channel (Subject) notifying subscribers (Observers).

```java
import java.util.ArrayList;
import java.util.List;

// Observer Interface
interface Subscriber {
    void update(String videoTitle);
}

// Subject
class YouTubeChannel {
    private List<Subscriber> subscribers = new ArrayList<>();
    private String channelName;

    public YouTubeChannel(String name) { this.channelName = name; }

    public void subscribe(Subscriber s) { subscribers.add(s); }
    public void unsubscribe(Subscriber s) { subscribers.remove(s); }

    public void uploadVideo(String title) {
        System.out.println(channelName + " uploaded: " + title);
        notifySubscribers(title);
    }

    private void notifySubscribers(String title) {
        for (Subscriber s : subscribers) {
            s.update(title);
        }
    }
}

// Concrete Observer
class User implements Subscriber {
    private String name;
    public User(String name) { this.name = name; }

    @Override
    public void update(String videoTitle) {
        System.out.println("Hey " + name + ", new video out: " + videoTitle);
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        YouTubeChannel channel = new YouTubeChannel("CodeMaster");
        User user1 = new User("Alice");
        User user2 = new User("Bob");

        channel.subscribe(user1);
        channel.subscribe(user2);

        channel.uploadVideo("Java Design Patterns Tutorial");
        // Both Alice and Bob get notified.
    }
}
```

*   **Benefits:**
    *   Supports the **Open/Closed Principle**: You can add new subscriber types without changing the Subject.
    *   Decouples the Subject from the Observers.

---

## 6. ♟️ Strategy (Behavioral)

*   **What it's for (Problem):**
    How can we define a family of algorithms, encapsulate each one, and make them interchangeable? How can the algorithm vary independently from clients that use it?
*   **How to apply it (Solution):**
    Define a common interface for the algorithm (Strategy). Create concrete classes for each specific algorithm. The context class holds a reference to the Strategy interface and calls it.
*   **Java Example:**
    A navigation app calculating routes using different strategies.

```java
// Strategy Interface
interface RouteStrategy {
    void buildRoute(String a, String b);
}

// Concrete Strategies
class RoadStrategy implements RouteStrategy {
    public void buildRoute(String a, String b) {
        System.out.println("Route by road (Car).");
    }
}

class WalkingStrategy implements RouteStrategy {
    public void buildRoute(String a, String b) {
        System.out.println("Route by walking paths.");
    }
}

class PublicTransportStrategy implements RouteStrategy {
    public void buildRoute(String a, String b) {
        System.out.println("Route by bus and train.");
    }
}

// Context
class Navigator {
    private RouteStrategy routeStrategy;

    public void setStrategy(RouteStrategy strategy) {
        this.routeStrategy = strategy;
    }

    public void buildRoute(String a, String b) {
        if (routeStrategy == null) {
            System.out.println("Please select a strategy.");
            return;
        }
        routeStrategy.buildRoute(a, b);
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Navigator nav = new Navigator();
        
        nav.setStrategy(new RoadStrategy());
        nav.buildRoute("Home", "Work"); // Output: Route by road (Car).
        
        nav.setStrategy(new WalkingStrategy());
        nav.buildRoute("Home", "Work"); // Output: Route by walking paths.
    }
}
```

*   **Benefits:**
    *   Eliminates complex conditional statements (if/else or switch) for selecting behaviors.
    *   Algorithms can be switched at runtime.
    *   Easy to add new strategies without changing the Context.
