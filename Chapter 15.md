## Detailed Notes: Interaction Diagram Notation (Chapter 15)

### Introduction to Interaction Diagrams

* **Purpose:** UML Interaction Diagrams are used to illustrate how objects interact with each other via messages[cite: 1487].
* **Role in Design:** They are the primary language used to illustrate object designs[cite: 1485].
* **Notation vs. Principles:** This chapter focuses on notation (the syntax)[cite: 1490]. Creating well-designed interactions also requires understanding design principles, which are covered in subsequent chapters[cite: 1490, 1491].
* **Value:** Spending non-trivial time on interaction diagrams is valuable[cite: 1557]. They provide a "thoughtful, cohesive, common starting point for inspiration during programming"[cite: 1559]. It is recommended to create them in pairs[cite: 1561]. This is a highly creative step where design skill is applied[cite: 1562, 1567].

---

### Sequence vs. Collaboration Diagrams

"Interaction diagram" is a general term for two specific types: sequence diagrams and collaboration diagrams[cite: 1495, 1496]. Both can express similar interactions[cite: 1496].

#### 1. Sequence Diagrams
* **Strengths:**
    * Clearly shows the sequence or time ordering of messages[cite: 1516].
    * Has a simple notation[cite: 1516].
    * Often preferred by CASE tools for reverse-engineering code[cite: 1518].
* **Weaknesses:**
    * Must extend to the right to add new objects, which consumes horizontal space[cite: 1514, 1516].

#### 2. Collaboration Diagrams
* **Format:** Illustrates object interactions in a graph or network format, where objects can be placed anywhere[cite: 1500].
* **Strengths:**
    * Space-economical, allowing new objects to be added in two dimensions[cite: 1513, 1516].
    * Better for illustrating complex branching, iteration, and concurrent behavior[cite: 1516].
* **Weaknesses:**
    * Makes it difficult to easily see the sequence of messages[cite: 1515, 1516].
    * Has a more complex notation[cite: 1516].

---

### Common Notation: Instances and Messages

#### Classes vs. Instances
* **Classifier (e.g., Class):** A standard box with the class name[cite: 1581].
* **Instance:** Uses the *same* graphic symbol (the box), but the designator string is **underlined**[cite: 1575, 1586].
    * `:Sale` $\rightarrow$ An anonymous instance of class `Sale`[cite: 1582, 1588].
    * `s1: Sale` $\rightarrow$ A named instance `s1` of class `Sale`[cite: 1583, 1587].
* **Static/Class Members:** To show a message to a class (a static method call), the box is **not underlined**[cite: 1741, 1748, 1849, 1870].

#### Basic Message Syntax
* The standard syntax is: `return := message(parameter : parameterType) : returnType`[cite: 1593].
* Type information can be omitted if it's obvious or unimportant (e.g., `spec := getProductSpect(id)`)[cite: 1594, 1595].

---

### Basic Collaboration Diagram Notation

#### Links
* A **link** is the connection path between two objects, shown as a solid line[cite: 1599, 1608].
* It indicates that navigation and visibility between the objects are possible[cite: 1599].
* A single link can have multiple messages flowing in both directions[cite: 1609].

#### Messages and Sequencing
* A message is shown as a text expression with a small arrow indicating its direction[cite: 1611].
* **Sequence Numbering:**
    * The *first message* (from an unidentified sender) is **not numbered**[cite: 1652].
    * The first internal message is numbered `1`, the next is `2`, and so on[cite: 1653].
    * **Nesting:** A message sent *as a result* of another message is numbered by prepending the outer message's number. For example, message `1.1` is sent during the execution of message `1`[cite: 1653, 1654].

#### Instance Creation
* A `create` message is the UML convention for creating an instance[cite: 1632].
* Parameters can be included, representing a constructor call[cite: 1634, 1635].
* If another message name (like `make`) is used, it can be stereotyped as `«create»`[cite: 1633, 1644].
* The newly created instance box can be marked with the `{new}` property[cite: 1639].

#### Messages to "self"
* An object can send a message to itself, illustrated by a link line that starts and ends on the same object box[cite: 1625, 1626].

#### Conditional Messages
* A **conditional clause** in `[square brackets]` is placed after the sequence number (e.g., `1 [color = red]: calculate()`)[cite: 1682, 1687].
* The message is sent only if the condition is `true`[cite: 1684].
* **Mutually Exclusive Paths:**
    * A conditional path letter (e.g., `a`, `b`) is added to the sequence number[cite: 1710].
    * Example: `1a [test1]: msg2()` and `1b [not test1]: msg4()`[cite: 1700, 1705].
    * Both are sequence number "1" because either could be the first message[cite: 1712].
    * Nesting follows this (e.g., `1a.1: msg3()`)[cite: 1713].

#### Iteration (Looping)
* **Iteration:** Indicated by a `*` after the sequence number (e.g., `1*`)[cite: 1721].
* An optional iteration clause can be added: `1* [i := 1..N]`[cite: 1716, 1719].
* **Iteration Over a Collection (Multiobject):**
    * A "multiobject" (a collection like a list) is shown as a stacked/double box[cite: 1727, 1736].
    * To show iteration over each member, a `*` is used in the message (`1*: getSubtotal()`)[cite: 1731, 1734].
    * A `*` multiplicity marker is also placed on the link line next to the multiobject[cite: 1738]. This signifies the message is sent to each *element*, not repeatedly to the collection itself[cite: 1738].

---

### Basic Sequence Diagram Notation

#### Lifelines and Messages
* **Links:** Sequence diagrams do *not* show link lines[cite: 1755].
* **Time:** Time is organized vertically, from top to bottom[cite: 1758].
* **Messages:** Shown as a horizontal arrow from one object's lifeline to another[cite: 1757].
* **Object Lifelines:** The vertical dashed line under an object, indicating its life during the diagram[cite: 1804, 1805].

#### Focus of Control (Activation Boxes)
* A thin rectangle (activation box) can be drawn on an object's lifeline[cite: 1769].
* It indicates the "focus of control," meaning the object is active (e.g., its operation is on the call stack)[cite: 1769].
* This notation is optional but common[cite: 1770].

#### Return Messages
* Showing returns is optional[cite: 1773].
* If shown, it is a **dashed, open-arrowed line** coming from the end of an activation box[cite: 1773].

#### Messages to "self"
* A message from an object to itself is shown by starting the message arrow on the object's lifeline and ending it on the same lifeline, creating a **nested activation box**[cite: 1785, 1789].

#### Instance Creation
* A `create` message arrow points directly to the **instance box** (not the lifeline) of the new object[cite: 1798].
* The newly created object is placed at the vertical "height" at which its creation message is received[cite: 1796].

#### Object Destruction
* Used to show explicit object destruction (e.g., in C++)[cite: 1806].
* A message with the `«destroy»` stereotype is sent to the object[cite: 1814].
* The message points to a large `X` on the object's lifeline, which then terminates[cite: 1813, 1814].

#### Conditional Messages
* A conditional clause `[in brackets]` is shown before the message expression on the message arrow[cite: 1817].
* **Mutually Exclusive Paths:**
    * Shown as **angled message lines** that emerge from a common point on the sender's lifeline[cite: 1824, 1825].

#### Iteration (Looping)
* **For a Single Message:** An iteration clause is prefixed to the message (e.g., `*[i := 1..N]: num := nextInt()`)[cite: 1836].
* **For a Series of Messages:** A **large box** is drawn *around* the group of messages that are to be repeated[cite: 1843]. The iteration clause is placed within this box[cite: 1856].
* **Iteration Over a Collection (Multiobject):**
    * The collection is shown as a stacked/double box[cite: 1868].
    * The message is prefixed with a `*` (e.g., `*: st := getSubtotal()`)[cite: 1861].

---

## How to Create (Draw) an Interaction Diagram

Here are the succinct, end-to-end steps for *drawing* an interaction diagram based on the notation provided.

1.  **Choose Your Diagram Type**
    * Choose a **Sequence Diagram** if you need to clearly show the *time and order* of messages[cite: 1516].
    * Choose a **Collaboration Diagram** if you need a flexible *network layout* (e.g., for complex branching) or are tight on horizontal space[cite: 1513, 1516].

2.  **Add the Participants (Instances and Classes)**
    * Draw a box for each participant[cite: 1573].
    * **For an instance:** **Underline the name** (e.g., `:Register` or `r1:Register`)[cite: 1575, 1586].
    * **For a class (static calls):** Do **not** underline the name (e.g., `java.util.Collections`)[cite: 1741, 1849].
    * **For a collection (multiobject):** Draw a stacked/double box[cite: 1736, 1868].

3.  **Draw the Interaction Flow**
    * **If Sequence Diagram:**
        * Place participants at the top, with vertical lifelines (dashed lines) extending down[cite: 1804].
        * Draw messages as horizontal arrows, starting from the top and moving down to show time order[cite: 1757, 1758].
        * (Optional) Add activation boxes on the lifeline to show when an object is active[cite: 1769, 1770].
    * **If Collaboration Diagram:**
        * Place participants on the diagram in a network layout[cite: 1500].
        * Draw a `link line` (solid line) between any two instances that need to communicate[cite: 1599].
        * Add messages along these links, using **sequence numbers** (e.g., `1:`, `1.1:`, `2:`) and small arrows to show order and direction[cite: 1611, 1614, 1653].

4.  **Add Detail and Special Conditions (as needed)**
    * **Instance Creation:** Send a `create` message (or `«create»` stereotype)[cite: 1632, 1633]. In a sequence diagram, this message points to the new instance box itself[cite: 1798].
    * **Iteration:** Prefix the message with a `*`[cite: 1721, 1836]. You can add a clause like `*[i := 1..N]`[cite: 1716, 1836]. For a *series* of messages in a sequence diagram, draw a large box around them[cite: 1843].
    * **Conditionals:** Add a guard condition in brackets (e.g., `[color=red]`) to the message[cite: 1682, 1817].
    * **Message to Self:** Draw a message (and nested activation box for sequence diagrams) that starts and ends on the same object[cite: 1625, 1785].