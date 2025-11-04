## 📚 System Sequence Diagrams (SSDs) and Use Cases

### Introduction to System Sequence Diagrams (SSDs)
* A **System Sequence Diagram (SSD)** is a simple, quickly created artifact that illustrates the **input and output events** related to the system under discussion[cite: 24].
* It is a type of **UML sequence diagram** used to illustrate events that go from external actors to a system[cite: 25, 37].
* **Purpose:** The SSD shows, for a particular **scenario of a use case**, the events that external actors generate, their order, and inter-system events[cite: 38].
* **Black Box View:** In an SSD, the system is treated as a **"black box"**[cite: 27, 39]. The diagram focuses exclusively on the events that **cross the system boundary** from actors to systems[cite: 39, 46].
* **Timing:** Time proceeds **downward** in the diagram, and the ordering of events must follow their order in the use case scenario[cite: 47].
* **Scope:** An SSD should be created for the **main success scenario** of a use case, as well as for **frequent or complex alternative scenarios**[cite: 40].
    * *Note:* The UML does not define "system" sequence diagrams; the qualification emphasizes its application to systems as black boxes[cite: 41, 42].

---

### 📝 System Events and the System Boundary
The first step in drawing an SSD is clarifying the system boundary and identifying the relevant system events[cite: 17, 107].

#### Defining the System Boundary
* For software development, the **system boundary** is usually chosen to be the **software system itself** (and possibly hardware)[cite: 108, 112].
* A **system event** is an **external event** that directly stimulates the software[cite: 112].
* **Identifying Actors:** Only actors that **directly interact** with the software system generate system events.
    * *Example:* In the Process Sale use case, the Cashier interacts directly with the POS system, making the Cashier the generator of system events. The Customer interacts with the Cashier but not directly with the POS system (for a simple cash-only scenario), so the Customer is not a system event generator[cite: 114, 115, 116].

#### Identifying System Events from Use Cases
* SSDs are **derived from inspection of a use case** (specifically, a scenario of a use case)[cite: 82, 105].
* An actor generates events to a system, usually **requesting some operation** in response[cite: 33]. This request event initiates an operation upon the system[cite: 35].
    * *Example:* When a cashier enters an item's ID, the cashier is requesting the POS system to record that item's sale[cite: 34].
* System events may include **parameters**[cite: 48].

---

### 📐 Creating the SSD: Notation and Naming
The SSD uses specific notation to illustrate the sequence of events.

#### Core Elements
* **External Actor:** An actor that interacts directly with the system[cite: 46]. (e.g., `:Cashier` [cite: 52]).
* **System:** The system under discussion, treated as a black box (e.g., `:System` [cite: 58, 84]). The colon and underline imply an instance[cite: 55].
* **System Event/Message:** An arrow from the actor to the system, labeled with the event name and any parameters[cite: 46, 57, 64].
* **Return Value(s):** Optional dashed line from the system back to the actor, representing the system's output or response (e.g., `description, total`, `total with taxes`)[cite: 61, 63, 65, 68].
* **Iteration Marker:** A box enclosing an iteration area, marked with an iteration clause (e.g., `* [more items]`) to indicate repeated events[cite: 59, 60, 66].

#### Naming Conventions
System events (and their associated system operations) should be named at the **level of intent**, rather than describing the physical input medium or interface widget[cite: 126].
* Start the name with a **verb** (e.g., `add...`, `enter...`, `end...`, `make...`) to emphasize the command orientation[cite: 127].
* *Better Example:* **`enterItem(itemID, quantity)`** [cite: 128]
* *Worse Example:* **`scan(itemID, quantity)`** (as "scan" describes the laser input mechanism, not the intent)[cite: 128, 140].

#### Example from "Process Sale" Scenario
For the main success scenario of the Process Sale use case, the Cashier generates the following system events[cite: 49, 50]:
* `makeNewSale()` [cite: 57]
* `enterItem(itemID, quantity)` [cite: 64] (This event repeats for each item [cite: 66])
* `endSale()` [cite: 67]
* `makePayment(amount)` [cite: 69]


---

### 🗂️ SSDs in the Unified Process (UP)
SSDs are a visualization of the interactions implied in the use cases and are considered part of the **Use-Case Model**[cite: 170].

#### Timing and Effort
* **Phase:** Most SSDs are created during the **Elaboration** phase of the UP[cite: 175]. They are not usually needed in Inception[cite: 174].
* **Purpose in Elaboration:** To clarify system events, which helps in[cite: 175]:
    * Identifying the major operations the system must be designed to handle.
    * Writing **system operation contracts** (discussed in a later chapter)[cite: 175, 211].
    * Possibly supporting estimation.
* **Selection:** It is **not necessary** to create SSDs for all scenarios of all use cases; rather, create them only for some chosen scenarios of the current iteration[cite: 178, 179].
* **Timeframe:** Creating an SSD should only take a **few minutes or up to a half hour**[cite: 180].

#### Relationships to Other Artifacts
SSDs provide a necessary link between the high-level requirements (Use Cases) and the low-level design[cite: 190, 223].
* **Source:** SSDs are derived from **Use Case text**[cite: 143, 204].
* **Refinement:** The **Glossary** can be used to elaborate on the terse terms (operations, parameters, return data) shown in the SSDs, if not already explained in the use cases[cite: 145, 146, 147, 197, 202].
* **Input to Design:** SSDs define the **system events** which serve as input for creating the **Design Model**[cite: 206, 212]. **Design objects** are then created to handle these system events[cite: 221, 222].

