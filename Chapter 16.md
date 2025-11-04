## 🎯 The Core of Object Design: Responsibilities

Object design is not just about drawing diagrams; it's the critical step of deciding how objects should interact and what methods belong to which classes[cite: 553, 555].The fundamental principles for making these decisions can be learned methodically through patterns of assigning **responsibilities**[cite: 561, 563].

### What is a Responsibility?
A responsibility is "a contract or obligation of a classifier"[cite: 565]. It's about an object's obligations in terms of its behavior[cite: 566].

There are two main types of responsibilities [cite: 567-568]:

* **Doing:**
    * Doing something itself (e.g., creating an object, doing a calculation)[cite: 571].
    * Initiating action in other objects[cite: 572].
    * Controlling and coordinating activities in other objects[cite: 573].
* **Knowing:**
    * Knowing about its own private, encapsulated data[cite: 575].
    * Knowing about related objects[cite: 576].
    * Knowing about things it can derive or calculate[cite: 577].

Responsibilities are assigned to classes during design and are implemented as **methods**[cite: 578, 585]. Interaction diagrams (like sequence diagrams) are the tools used to visualize these responsibility assignments[cite: 591, 601]. For example, showing a `makePayment` message sent to a `:Sale` object implies the `Sale` class has a responsibility to handle that message[cite: 599].

---

## 🧩 What are Patterns?

In object technology, a **pattern** is a "named description of a problem and solution that can be applied to new contexts"[cite: 617].

* **Not New Ideas:** Patterns codify existing, "tried-and-true" knowledge and principles[cite: 627].
* **Named for Communication:** Giving a pattern a name (e.g., "Creator") allows designers to communicate a complex idea with a simple, shared vocabulary[cite: 636, 642].

### GRASP: The Foundational Patterns
**GRASP** stands for **General Responsibility Assignment Software Patterns**[cite: 659]. They are a set of fundamental principles that help you, the designer, make decisions about where to assign responsibilities[cite: 656].

This chapter introduces the first five key GRASP patterns.

---

### 1. 🧠 Information Expert (or Expert)

* **What it's for (Problem):**
    What is a basic principle by which to assign responsibilities to objects? [cite: 686]
* **How to apply it (Solution):**
    Assign a responsibility to the class that has the **information necessary to fulfill it**[cite: 685]. This class is the "information expert."
* **Example (Calculating a Sale Total):**
    1.  **Responsibility:** Who should be responsible for knowing the grand total of a `Sale`? [cite: 694]
    2.  **Find the Expert:** To calculate the total, you need all the `SalesLineItem` instances for that sale. Looking at the Domain Model, the `Sale` object "Contains" a list of its `SalesLineItem`s[cite: 722].
    3.  **Assign Responsibility:** Therefore, `Sale` is the **Information Expert** for calculating the total. We add a `getTotal()` method to the `Sale` class[cite: 705, 723].
    4.  **Collaboration:** The `Sale` object doesn't have all the information itself. It must collaborate with its parts. To get the grand total, it must sum the subtotals of all its `SalesLineItem`s[cite: 739].
    5.  **New Responsibility:** Who should know the subtotal of a `SalesLineItem`?
    6.  **Find the Expert:** The `SalesLineItem` knows its `quantity` and knows its associated `ProductSpecification`, which knows the `price`[cite: 737].
    7.  **Assign Responsibility:** `SalesLineItem` is the **Information Expert** for calculating its subtotal. We add a `getSubtotal()` method to it[cite: 738, 751].
    8.  **Chain of Experts:** The `SalesLineItem` will fulfill this by getting the `price` from the `ProductSpecification` (which is the expert for `price`) and multiplying it by its own `quantity` [cite: 754-756].
* **Benefits:**
    * Information encapsulation is maintained[cite: 824].
    * This usually supports **Low Coupling** and **High Cohesion** (other GRASP patterns)[cite: 825, 828].
* **Contraindications (Warning!):**
    Do not follow Expert blindly if it leads to problems with coupling or cohesion.
    * *Example:* Who should save a `Sale` to a database? The `Sale` object has the data, so Expert suggests the `Sale` class should be responsible [cite: 807-808].
    * *Why this is bad:* This design violates the "separation of major system concerns"[cite: 816]. It mixes application logic (`Sale`) with database logic (SQL commands) [cite: 811-812]. This **lowers cohesion** (the class is doing unrelated things) and **raises coupling** (the `Sale` class is now dependent on database subsystems like JDBC) [cite: 813-814].

---

### 2. 👶 Creator

* **What it's for (Problem):**
    Who should be responsible for creating a new instance of some class? [cite: 844]
* **How to apply it (Solution):**
    Assign class **B** the responsibility to create an instance of class **A** if one or more of these apply[cite: 835]:
    * B **aggregates** A objects[cite: 837].
    * B **contains** A objects (this is the preferred choice)[cite: 838, 843].
    * B **records** instances of A objects[cite: 839].
    * B **closely uses** A objects[cite: 840].
    * B **has the initializing data** for A (which is also an application of the Expert pattern)[cite: 841].
* **Example (Creating a SalesLineItem):**
    1.  **Responsibility:** Who should create a `SalesLineItem` instance? [cite: 850]
    2.  **Find the Creator:** We look at the Domain Model. The `Sale` class **Contains** all the `SalesLineItem` objects[cite: 866].
    3.  **Assign Responsibility:** `Sale` is the logical choice for creating `SalesLineItem`s. We add a `makeLineItem()` method to the `Sale` class[cite: 867, 874]. The interaction diagram will show the `:Sale` instance sending a `create()` message to the `SalesLineItem` class[cite: 871].
* **Benefits:**
    * Supports **Low Coupling** because the creator (e.g., `Sale`) is likely already associated with the created class (e.g., `SalesLineItem`)[cite: 896, 898].
* **Contraindications:**
    If the creation logic is very complex (e.g., recycling old instances, building one of many different classes based on a property), delegate this responsibility to a helper class called a **Factory** instead [cite: 892-893].

---

### 3. ⛓️ Low Coupling

* **What it's for (Problem):**
    How to support low dependency, low change impact, and increased reuse? [cite: 906]
* **How to apply it (Solution):**
    Assign a responsibility so that **coupling remains low**[cite: 905].
* **Core Concept:**
    **Coupling** is a measure of how strongly one class is connected to, has knowledge of, or relies on other classes[cite: 907].
    * **High Coupling (Bad):** A class relies on many other classes. This makes the system hard to understand, hard to reuse, and fragile (changes in one class force changes in related classes) [cite: 910-914].
    * **Low Coupling (Good):** A class is not dependent on too many others[cite: 908].
* **Example (Creating a Payment):**
    1.  **Responsibility:** Who should create a `Payment` instance?
    2.  **Option 1:** `Register` creates the `Payment` (based on Creator, since `Register` "records" a payment)[cite: 920]. The `Register` would then pass this new `Payment` to the `Sale`[cite: 921].
        * *Coupling Impact:* This design couples the `Register` class to the `Payment` class[cite: 930].
    3.  **Option 2:** `Register` delegates the `makePayment()` message to the `Sale`, and the `Sale` creates the `Payment`[cite: 936, 940].
        * *Coupling Impact:* This design does *not* increase coupling, assuming `Sale` has to be coupled to `Payment` anyway. The `Register` class does not become coupled to `Payment`[cite: 944].
    4.  **Conclusion:** Option 2 is preferable because it maintains lower overall coupling[cite: 945].
* **Key Points:**
    * This is an *evaluative principle* to consider during *all* design decisions[cite: 950].
    * **Pick Your Battles:** Don't worry about coupling to stable, common elements (like standard Java libraries) [cite: 974-975]. Focus on lowering coupling to elements that are unstable or likely to change (e.g., a third-party tax calculator interface) [cite: 984-986].

---

### 4. 🧩 High Cohesion

* **What it's for (Problem):**
    How to keep complexity manageable? [cite: 995]
* **How to apply it (Solution):**
    Assign a responsibility so that **cohesion remains high**[cite: 994].
* **Core Concept:**
    **Cohesion** (specifically, functional cohesion) is a measure of how strongly related and focused the responsibilities of a single class are[cite: 996].
    * **High Cohesion (Good):** The class has a moderate number of responsibilities, all highly related to a single purpose. It's easy to understand, maintain, and reuse[cite: 997, 1060].
    * **Low Cohesion (Bad):** The class does many unrelated things or "too much work"[cite: 999]. These are "bloated," "incohesive" objects that are hard to comprehend, maintain, and reuse [cite: 1000-1004, 1023].
* **Example (Creating a Payment):**
    1.  **Responsibility:** Who should create a `Payment` instance?
    2.  **Option 1:** The `Register` creates it.
        * *Cohesion Impact:* This one responsibility is fine, but if the `Register` also takes on responsibilities for *all* other system operations (totaling, item entry, returns), it will become a **bloated controller** with **low cohesion** [cite: 1021-1023].
    3.  **Option 2:** The `Sale` creates it, as delegated by the `Register`.
        * *Cohesion Impact:* This design keeps the `Register` lightweight and focused (high cohesion). The `Sale` is responsible for things related to the sale (like its payment), which is also cohesive[cite: 1026].
    4.  **Conclusion:** Option 2 is desirable because it supports both **High Cohesion** and **Low Coupling**[cite: 1027].
* **Key Points:**
    * Cohesion and Coupling are the "yin and yang" of software design; bad cohesion often leads to bad coupling, and vice versa[cite: 1076].

---

### 5. 🕹️ Controller

* **What it's for (Problem):**
    Who should be responsible for handling an **input system event**? (e.g., a user pressing a button) [cite: 1105-1106].
* **How to apply it (Solution):**
    Assign the responsibility for receiving or handling the system event message to a **non-UI** object representing one of these two choices:
    1.  **Facade Controller:** Represents the entire system, device, or subsystem (e.g., a class named `Register` or `POSSystem`)[cite: 1099, 1143].
    2.  **Use-Case Controller (or Session Controller):** Represents a specific use case scenario (e.g., a class named `ProcessSaleHandler` or `ProcessSaleSession`)[cite: 1099, 1144].
* **Example (Handling "enterItem"):**
    1.  **System Event:** The Cashier presses the "Enter Item" button[cite: 1124, 1129].
    2.  **The WRONG Way:** The `SaleJFrame` (the window object) should *not* handle this event. It must not contain the business logic[cite: 1103, 1263, 1316].
    3.  **The RIGHT Way:** The `SaleJFrame` receives the UI event (`actionPerformed`) and immediately **delegates** the system event (`enterItem`) to its controller[cite: 1267, 1291].
    4.  **Controller Choice 1 (Facade):** The controller is a `:Register` object. This single class would also handle `endSale`, `makePayment`, `makeNewReturn`, etc. [cite: 1150, 1204-1209].
    5.  **Controller Choice 2 (Use Case):** The controller is a `:ProcessSaleHandler` object. This class would handle `enterItem`, `endSale`, and `makePayment`. A *different* controller, `HandleReturnsHandler`, would exist for return-related events [cite: 1152, 1214-1215].
* **Benefits:**
    * **Reuse:** Keeps application logic out of the UI layer, so the logic can be reused with a different interface[cite: 1236, 1239].
    * **State Management:** A use-case controller can hold the state of a scenario (e.g., to know that `endSale` must happen before `makePayment`) [cite: 1241-1242].
* **Common Problems (Bloated Controllers):**
    A controller (especially a facade) can become **bloated** (low cohesion)[cite: 1246]. This happens when:
    * It's the only controller for many system events[cite: 1248].
    * It **does all the work itself** instead of **delegating** the work to Information Experts[cite: 1250].
* **Cures for Bloating:**
    1.  Use specific **use-case controllers** instead of one facade[cite: 1254].
    2.  Design the controller to **primarily delegate** tasks to other objects[cite: 1261].