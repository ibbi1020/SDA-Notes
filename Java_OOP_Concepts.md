# Java OOP Concepts Explained

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects", which can contain data (attributes) and code (methods). Java is a popular OOP language.

Here are the core concepts explained simply with code snippets.

## 1. Classes and Objects

Think of a **Class** as a blueprint or a template. It describes what an object will look like.
Think of an **Object** as the actual thing created from that blueprint.

**Example:** A "Car" is a class (blueprint). A specific red Toyota Corolla is an object.

```java
// The Class (Blueprint)
class Car {
    String color;
    String model;

    void drive() {
        System.out.println("The " + color + " " + model + " is driving.");
    }
}

public class Main {
    public static void main(String[] args) {
        // The Object (Instance)
        Car myCar = new Car(); 
        myCar.color = "Red";
        myCar.model = "Toyota";
        
        myCar.drive(); // Output: The Red Toyota is driving.
    }
}
```

---

## 2. Encapsulation

**Encapsulation** is about bundling data (variables) and methods together and restricting direct access to some of an object's components. It's like a protective shield.

*   **How:** Make variables `private` and provide `public` methods (getters and setters) to access them.
*   **Why:** To control how data is accessed or modified (e.g., preventing a negative age).

```java
class Person {
    // Private data: cannot be accessed directly from outside
    private int age;

    // Public method to set data (Setter)
    public void setAge(int newAge) {
        if (newAge > 0) {
            age = newAge;
        } else {
            System.out.println("Age must be positive!");
        }
    }

    // Public method to get data (Getter)
    public int getAge() {
        return age;
    }
}

public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        // p.age = -5; // Error! Cannot access private variable directly.
        
        p.setAge(25); // Allowed
        System.out.println(p.getAge()); // Output: 25
    }
}
```

---

## 3. Inheritance

**Inheritance** allows one class to acquire the properties (fields) and methods of another class. It promotes code reusability.

*   **Parent Class (Superclass):** The class being inherited from.
*   **Child Class (Subclass):** The class that inherits.
*   **Keyword:** `extends`

```java
// Parent Class
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// Child Class inherits from Animal
class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        
        myDog.eat();  // Inherited from Animal
        myDog.bark(); // Defined in Dog
    }
}
```

---

## 4. Polymorphism

**Polymorphism** means "many forms". It allows us to perform a single action in different ways.

### A. Compile-time Polymorphism (Method Overloading)
Multiple methods with the **same name** but **different parameters** in the same class.

```java
class Calculator {
    // Method 1: Adds two integers
    int add(int a, int b) {
        return a + b;
    }

    // Method 2: Adds three integers
    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

### B. Runtime Polymorphism (Method Overriding)
A child class provides a specific implementation of a method that is already defined in its parent class.

```java
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Cat extends Animal {
    // Overriding the parent's method
    @Override
    void makeSound() {
        System.out.println("Meow");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Cat(); // Upcasting
        myAnimal.makeSound(); // Output: Meow (The overridden method is called)
    }
}
```

---

## 5. Abstraction

**Abstraction** is about hiding the implementation details and showing only the functionality to the user. It lets you focus on *what* an object does instead of *how* it does it.

### A. Abstract Class
A class that cannot be instantiated on its own and may contain abstract methods (methods without a body).

```java
abstract class Shape {
    // Abstract method (no body)
    abstract void draw();
    
    // Regular method
    void info() {
        System.out.println("I am a shape.");
    }
}

class Circle extends Shape {
    // Must implement the abstract method
    void draw() {
        System.out.println("Drawing a Circle");
    }
}
```

### B. Interface
A completely abstract "contract". All methods are abstract by default (before Java 8). A class `implements` an interface.

```java
interface RemoteControl {
    void powerOn();
    void powerOff();
}

class TV implements RemoteControl {
    public void powerOn() {
        System.out.println("TV is turning ON.");
    }
    
    public void powerOff() {
        System.out.println("TV is turning OFF.");
    }
}
```

---

## Summary Table

| Concept | Keyword(s) | Simple Definition |
| :--- | :--- | :--- |
| **Class** | `class` | Blueprint for objects. |
| **Object** | `new` | Instance of a class. |
| **Encapsulation** | `private`, `public` | Hiding data, accessing via methods. |
| **Inheritance** | `extends` | Child class gets Parent class features. |
| **Polymorphism** | Overloading/Overriding | Same name, different behavior. |
| **Abstraction** | `abstract`, `interface` | Hiding details, showing essentials. |

---

## 6. Basic Java Syntax Cheat Sheet

Here are some common syntax patterns you will use frequently.

### A. Creating Objects
To use a class, you must create an instance of it using the `new` keyword.

```java
// ClassName variableName = new ClassName();
Car myCar = new Car();
ArrayList<String> list = new ArrayList<>();
```

### B. Control Flow (If-Else)
Making decisions in code.

```java
int score = 85;

if (score >= 90) {
    System.out.println("Grade: A");
} else if (score >= 80) {
    System.out.println("Grade: B");
} else {
    System.out.println("Grade: C");
}
```

### C. Loops
Repeating code multiple times.

**1. Standard For Loop**
Used when you know how many times to loop.
```java
// for (initialization; condition; update)
for (int i = 0; i < 5; i++) {
    System.out.println("Count: " + i);
}
```

**2. Enhanced For Loop (For-Each)**
Best for looping through Lists or Arrays.
```java
String[] fruits = {"Apple", "Banana", "Orange"};

for (String fruit : fruits) {
    System.out.println(fruit);
}
```

**3. While Loop**
Used when you want to loop as long as a condition is true.
```java
int count = 0;
while (count < 3) {
    System.out.println("Still running...");
    count++;
}
```

### D. Data Structures

**1. Arrays**
Fixed size collection of items of the same type.
```java
// Declaration and initialization
int[] numbers = {1, 2, 3, 4, 5};

// Accessing elements
System.out.println(numbers[0]); // Output: 1

// Setting elements
numbers[1] = 10;
```

**2. ArrayList (Dynamic List)**
Resizable list. Requires `import java.util.ArrayList;`.
```java
import java.util.ArrayList;

ArrayList<String> names = new ArrayList<>();

// Adding items
names.add("Alice");
names.add("Bob");

// Accessing items
System.out.println(names.get(0)); // Output: Alice

// Removing items
names.remove("Bob");

// Checking size
System.out.println(names.size());
```
