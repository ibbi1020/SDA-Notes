## Combined Notes: Creating a Domain Model (Chapters 10, 11, 12)

These chapters guide you through the most important activity in object-oriented analysis: creating a Domain Model. This model is built incrementally in three main stages:
1.  **Finding Conceptual Classes** (Chapter 10)
2.  **Adding Associations** (Chapter 11)
3.  **Adding Attributes** (Chapter 12)

The Domain Model serves as a "visual dictionary" of the noteworthy concepts, vocabulary, and relationships in the problem domain[cite: 937].

### 🌍 1. What is a Domain Model?

A Domain Model is a visual representation of **real-world conceptual classes** (ideas, things, or objects) in a domain of interest[cite: 882, 968].

**Key Principles:**
* **It is NOT a Software Diagram:** A Domain Model shows real-world concepts, *not* software components[cite: 878, 879, 942].
* **No Operations:** The class boxes do not contain methods or operations (e.g., no `print()`)[cite: 885, 945].
* **It is NOT a Data Model:** It is not a design for a database[cite: 893].
* **Purpose:** It serves as a source of inspiration for later software design[cite: 865, 1331]. By using names from the domain (like `Sale`, `Item`), the final software has a "lower representational gap," making it easier to understand[cite: 1332, 1364].

---

### 🔎 2. Step 1: Identify Conceptual Classes (Chapter 10)

A conceptual class is an idea, thing, or object in the real world[cite: 968]. The goal is to find classes relevant to the current requirements (e.g., the "Process Sale" use case)[cite: 1006].

#### How to Find Them

1.  **Conceptual Class Category List:** Review a checklist of common categories and see what fits[cite: 1024, 1029]. Key categories include:
    * **Physical Objects:** `Register`, `Item` [cite: 1034]
    * **Transactions:** `Sale`, `Payment` [cite: 1034]
    * **Transaction Line Items:** `SalesLineItem` [cite: 1034]
    * **Roles of People:** `Cashier`, `Customer` [cite: 1034, 1081, 1082]
    * **Specifications/Descriptions:** `ProductSpecification` [cite: 1034]
    * **Places/Containers:** `Store` [cite: 1034]
    * **Catalogs:** `ProductCatalog` [cite: 1034]
2.  **Noun Phrase Identification:** Mine the text of your use cases for nouns and noun phrases[cite: 1039]. These are candidates for either classes or attributes[cite: 1065].

#### Common Pitfall: Class vs. Attribute

The most common mistake is to make a conceptual class an attribute[cite: 1126].

* **Rule of Thumb:** If you don't think of something as just a **number or text** in the real world, it is probably a **conceptual class**, not an attribute[cite: 1128].
* **Example (from book):** Should `store` be an attribute of `Sale`? [cite: 1130] No. A `Store` is a physical, legal entity, not just a string of text[cite: 1136, 1137]. Therefore, `Store` should be its own class.
* **Example (Real World):** In a university system, should `publisher` be an attribute of `Book`? A publisher (e.g., "Penguin Books") is an organization, a legal entity, not just a word. Therefore, **`Publisher`** should be a separate conceptual class.

#### Crucial Concept: Specification (or Description) Classes

This is a common and vital pattern[cite: 1182, 1205].

* **The Problem:** Imagine `Item` (a physical object) has attributes for `price` and `description`[cite: 1211, 1212, 1213]. What happens when the store sells the last `Item`? The software object is deleted, and the *knowledge* of its price and description is lost[cite: 1195, 1196]. This also creates redundant data, as every single `Item` duplicates the same `price` and `description`[cite: 1197].
* **The Solution:** Create a **`ProductSpecification`** class[cite: 1200].
    * `ProductSpecification` stores the shared information: `description`, `price`, `itemID`[cite: 1217].
    * `Item` stores the information unique to the physical instance: `serial number`[cite: 1224].
    * An association is created: a `ProductSpecification` *Describes* one or more `Item`s[cite: 1204, 1218].
* **Guideline:** Add a specification class when you need to maintain a description of something *independent* of the existence of any physical instances [cite: 1231], or to reduce redundant information[cite: 1233].
* **Example (Real World):** For a library, you need this pattern:
    * **`BookSpecification`** (or `Title`): Holds the `ISBN`, `title`, and `author`.
    * **`BookCopy`:** Represents one physical copy, with its own `copyID` and `condition`.
    * The `BookSpecification` *Describes* many `BookCopy`s. This way, if all copies are lost, you still know the `title` and `author` of the books the library *can* stock.

---

### 🔗 3. Step 2: Add Associations (Chapter 11)

An association is a relationship between classes that indicates a "meaningful and interesting connection"[cite: 550].

#### How to Find Them

* **Primary Filter: "Need-to-Know":** This is the most important criterion. Only add associations for which knowledge of the relationship *must* be preserved for some duration to meet the system's requirements[cite: 562, 567, 786].
    * **Example:** We *need to know* which `SalesLineItems` are part of a `Sale` to print a receipt or get a total[cite: 564, 565]. This justifies the `Sale` *Contained-in* `SalesLineItem` association[cite: 770].
    * **Counter-Example:** Do we *need to know* which `Manager` *Started-by* a `Register`? The requirements don't state this, so we can probably leave it out[cite: 836].
* **Common Associations List:** Use this checklist to brainstorm possibilities[cite: 600, 608]:
    * `A` is a part of `B` (`SalesLineItem` - `Sale`)
    * `A` is contained in `B` (`Register` - `Store`, `Item` - `Store`)
    * `A` is recorded in `B` (`Sale` - `Register`)
    * `A` is a member of `B` (`Cashier` - `Store`)
    * `A` uses `B` (`Cashier` - `Register`)

#### Association Notation

* **Name:** Use a `TypeName-VerbPhrase-TypeName` format (e.g., `Sale` *Paid-by* `Payment`)[cite: 686]. The name is capitalized[cite: 687].
* **Multiplicity:** This defines how many instances of class `A` can be associated with *one* instance of class `B` at a *particular moment in time*[cite: 629, 655].
    * `*` (or `0..*`): Zero or more ("many") [cite: 639]
    * `1..*`: One or more [cite: 644]
    * `1`: Exactly one
    * `0..1`: Zero or one
* **Example (Real World):** In a library model:
    * A `Patron` (`1`) can have many `Loan`s (`*`).
    * A `Loan` (`1`) is for exactly one `Patron` (`1`).
    * A `BookCopy` (`1`) can be on *at most one* `Loan` at a time (`0..1`).
    * A `BookSpecification` (`1`) can have one or more `BookCopy`s (`1..*`).

---

### 🏷️ 4. Step 3: Add Attributes (Chapter 12)

An attribute is a "logical data value of an object"[cite: 239]. Add attributes only when the requirements imply a need to remember specific information[cite: 240].

* **Example:** A receipt needs to show the sale's date and time, so the `Sale` class needs `date` and `time` attributes[cite: 243, 244].

#### Valid Attribute Types

* **Keep Attributes Simple:** Attributes should be simple "data types"[cite: 259, 299].
* **Common Data Types:** `Boolean`, `Date`, `Number`, `String`, `Time`[cite: 260].
* **Definition of "Data Type":** A value for which *unique identity is not meaningful*[cite: 299]. You don't care about two different instances of the number 5 [cite: 301] or the string 'cat'[cite: 302]; you only care about their *value*. This is the opposite of a `Person` object, where two "Jill Smith" instances are distinct individuals[cite: 305].

#### Crucial Pitfall: Attributes vs. Associations (The "Design Creep" Problem)

This is the most critical rule in attribute modeling. It is a common violation to use attributes to relate conceptual classes[cite: 366].

1.  **Do NOT Use Attributes for Complex Concepts:**
    * **Rule:** Relate conceptual classes with an **association**, not with an attribute[cite: 290].
    * **Worse:** A `Cashier` class with an attribute `currentRegister: Register`[cite: 257, 267].
    * **Better:** A `Cashier` class with a `Uses` **association** to the `Register` class[cite: 258, 271, 273].
    * **Why?** `Register` is a complex domain concept, not a simple data type like `Number` or `String`[cite: 256, 257].

2.  **Do NOT Use Attributes as Foreign Keys:**
    * **Rule:** Do not add attributes that serve as foreign keys to relate objects[cite: 366, 386].
    * **Worse:** A `Cashier` class with an attribute `currentRegisterNumber`[cite: 368, 376].
    * **Better:** A `Cashier` class with a `Uses` **association** to the `Register` class[cite: 369, 383].
    * **Why?** This is "design creep"[cite: 365]. How the association will be *implemented* (e.g., with a foreign key in a database or a pointer in code) is a *design* decision to be deferred[cite: 294, 371]. In the *analysis* model, we are simply stating that a conceptual relationship exists.

#### Advanced Attributes: Non-Primitive Data Types (Value Objects)

Sometimes, an attribute that looks simple (like a number or string) has complex behavior. In these cases, it should be modeled as its own non-primitive data type class[cite: 314, 319].

Represent a simple type as a non-primitive class when:
1.  **It is composed of separate sections**[cite: 322].
    * *Example:* `address` should be an `Address` class (with street, city, zip)[cite: 339]. `phone number` should be a `PhoneNumber` class (with area code, number)[cite: 323].
2.  **It has operations, like validation**[cite: 324].
    * *Example:* `itemID` should be an `ItemID` class because it has validation rules (check-sum digits)[cite: 335, 337].
3.  **It is a quantity with a unit**[cite: 330].
    * *Example:* `amount` on a `Payment` should not be a plain `Number`[cite: 396]. It should be a `Money` (or `Quantity`) class, which contains both a value *and* a currency unit[cite: 331, 338, 391, 393].
4.  **It has other attributes**[cite: 328].
    * *Example:* A `promotional price` might have a `startDate` and `endDate`[cite: 329].

**How to Show Them:** Since these are still "data types" (identity doesn't matter), you can show them in the attribute compartment (e.g., `amount: Money`) [cite: 346, 414] or as a separate class box associated with the main class[cite: 391, 400]. This is a choice based on what you want to communicate[cite: 348, 364].

---

## ✅ Rules for Creating a Domain Model (A Succinct Guide)

Here is an easy-to-understand list of rules you must follow, based on the teachings of these chapters.

1.  **Model the Real World, Not Software.**
    Your model must show real-world concepts (a `Sale`, a `Person`), not software artifacts (a `SaleDatabase`, a `Window`)[cite: 878, 942]. Do not include methods/operations[cite: 885, 945].

2.  **Use the Domain's Vocabulary.**
    Use the names that people in the domain actually use (the "Mapmaker" principle)[cite: 1111, 1117]. If library staff call them "Patrons," use `Patron`, not `Customer`.

3.  **A Class Is a "Thing," Not Just a Number or Text.**
    This is the key rule for deciding if something is a class or an attribute[cite: 1128]. A `Store` is a physical place, so it's a class[cite: 1137]. A `Store`'s `name` is just text, so it's an attribute.

4.  **Use "Specification" Classes for Descriptions.**
    If you have a physical item (like `BookCopy`) and a description of it (like `BookSpecification`), make them two separate classes[cite: 1200, 1230]. This prevents data loss and redundancy[cite: 1196, 1197].

5.  **An Attribute Is a Simple Data Value.**
    Attributes are for "simple" data types like `String`, `Number`, `Date`, `Boolean`, or `Time` [cite: 259, 260]—things where only the *value* matters, not the identity[cite: 299].

6.  **CRITICAL RULE: Use Associations, Not Attributes, to Relate Classes.**
    Do NOT use an attribute as a "pointer" or "foreign key" to another class[cite: 290, 366].
    * **Wrong:** A `Cashier` class with a `registerNumber` attribute[cite: 368, 376].
    * **Right:** A `Cashier` class with a `Uses` **association** to a `Register` class[cite: 369, 383].
    This avoids "design creep" and keeps your model in the analysis (real-world) perspective[cite: 365, 371].

7.  **Only Add Associations That You "Need to Know."**
    Your model should not be a spider web of every possible relationship. Focus *only* on the associations you must remember to satisfy the system's requirements[cite: 567, 786].

8.  **Make "Smart Attributes" into Their Own Classes.**
    If an attribute has parts (like an `Address`), has rules (like an `ItemID`), or has a unit (like `Money`), make it its own separate class [cite: 319-333]. You can then list it as `amount: Money`[cite: 414].

9.  **Keep it Simple and Readable.**
    The model is a tool for communication[cite: 364]. Avoid "visual noise" [cite: 573] and redundant associations[cite: 787]. A good model helps people understand the domain[cite: 483].