# Chapter 7: Understanding Requirements - Detailed Academic Notes

## Overview of Requirements Engineering

**Definition**: Requirements engineering encompasses the broad spectrum of tasks and techniques that lead to an understanding of requirements. It is a major software engineering action that begins during the communication activity and continues into the modeling activity.

**Core Purpose**: To establish a solid foundation for design and construction by understanding what the customer wants before beginning to design and build a computer-based system.

**Key Challenge**: Understanding problem requirements is among the most difficult tasks facing a software engineer. Customers and end users often cannot state their needs explicitly, and those needs will change throughout the project.

---

## 7.1 Requirements Engineering

### Foundation Concepts

Requirements engineering builds a bridge between stakeholders (managers, customers, end users) and the design/construction phases. It encompasses **seven interconnected tasks**:

1. **Inception**
2. **Elicitation** 
3. **Elaboration**
4. **Negotiation**
5. **Specification**
6. **Validation**
7. **Management**

**Important Note**: These tasks have "muddy boundaries" - some occur in parallel, all are adapted to project needs, and expect to do design during requirements work and requirements work during design.

### 7.1.1 Inception

**Purpose**: Establish basic understanding at project startup
- Identify the business need or market opportunity
- Understand the problem, the people seeking a solution, and desired solution nature
- Establish communication between stakeholders and software team
- Begin effective collaboration

**Key Activities**:
- Define scope and nature of problem to be solved
- Establish stakeholder communication channels
- Set foundation for collaborative work

### 7.1.2 Elicitation

**Core Challenge**: "It certainly seems simple enough—ask the customer... But it isn't simple—it's very hard."

**Business Goals Understanding**:
- Goals are long-term aims that system/product must achieve
- May deal with functional or nonfunctional concerns (reliability, security, usability)
- Goals explain requirements to stakeholders and manage conflicts
- Must be specified precisely for requirements elaboration, verification, validation, conflict management, negotiation, explanation, and evolution

**Key Responsibilities**:
- Engage stakeholders and encourage honest goal sharing
- Establish prioritization mechanisms
- Create design rationale for potential architecture meeting stakeholder goals
- Maintain agility - transfer ideas smoothly without delay
- Recognize new requirements will emerge during iterative development

### 7.1.3 Elaboration

**Focus**: Developing refined requirements model identifying software function, behavior, and information aspects

**Process**:
- Driven by creation and refinement of user scenarios from elicitation
- Scenarios describe end user and actor interactions with system
- Parse scenarios to extract analysis classes (business domain entities visible to end users)
- Define attributes of each analysis class
- Identify required services for each class
- Identify relationships and collaboration between classes

**Critical Guideline**: "Elaboration is a good thing, but you need to know when to stop. The key is to describe the problem in a way that establishes a firm base for design and then move on. Do not obsess over unnecessary details."

### 7.1.4 Negotiation

**Context**: Customers/users often ask for more than achievable with limited resources; different stakeholders may propose conflicting requirements claiming their version is "essential"

**Approach**:
- Iterative process prioritizing requirements
- Assess cost and risk of requirements
- Address internal conflicts
- Requirements are eliminated, combined, and/or modified
- Goal: "no winner, no loser" - both sides achieve satisfaction through acceptable compromise

**Process Steps**:
1. Ask stakeholders to rank requirements
2. Discuss conflicts in priority
3. Use iterative approach for prioritization
4. Assess cost and risk
5. Address internal conflicts

### 7.1.5 Specification

**Definition**: In computer-based systems context, specification can be:
- Written document
- Set of graphical models
- Formal mathematical model
- Collection of usage scenarios
- Prototype
- Any combination of above

**Flexibility vs. Standardization**:
- Some advocate "standard template" for consistency and understandability
- Must remain flexible based on system size and complexity
- Large systems: written document combining natural language and graphical models
- Smaller systems: usage scenarios may suffice for well-understood technical environments

**Template Reference**: Formal software requirements specification document template available at: https://web.cs.dal.ca/~hawkey/3130/srs_template-ieee.doc

### 7.1.6 Validation

**Purpose**: Assess quality of requirements engineering work products

**Key Concern**: **Consistency** - use analysis model to ensure requirements consistently stated

**Validation Objectives**:
- Ensure all software requirements stated unambiguously
- Detect and correct inconsistencies, omissions, and errors
- Verify work products conform to established standards (process, project, product)

**Primary Mechanism**: Technical review with team including software engineers, customers, users, and stakeholders

**Review Team Examines**:
- Errors in content or interpretation
- Areas requiring clarification
- Missing information
- Inconsistencies (major problem in large products/systems)
- Conflicting requirements
- Unrealistic/unachievable requirements

**Validation Examples**:

*Problematic Requirement 1*: "The software should be user friendly"
- **Issue**: Too vague for testing/assessment
- **Solution**: Must be quantified or qualified

*Problematic Requirement 2*: "The probability of successful unauthorized database intrusion should be less than 0.0001"
- **Issues**: Quantitative but testing difficult/time-consuming; security level may not be warranted
- **Consider**: Alternative complementary security requirements (password protection, specialized handshaking)

### Requirements Validation Checklist

**Essential Questions**:
1. Are requirements stated clearly? Can they be misinterpreted?
2. Is the source (person, regulation, document) identified and verified?
3. Is the requirement bounded in quantitative terms?
4. What other requirements relate? Are they cross-referenced?
5. Does requirement violate system domain constraints?
6. Is requirement testable with specifiable validation criteria?
7. Is requirement traceable to system models?
8. Is requirement traceable to overall system/product objectives?
9. Is specification structured for easy understanding, reference, and technical translation?
10. Has specification index been created?
11. Have performance, behavior, operational characteristics been clearly stated? What appears implicit?

### 7.1.7 Requirements Management

**Context**: Requirements change throughout system life; desire to change persists constantly

**Definition**: Set of activities helping project team identify, control, and track requirements and changes at any project time

**Relationship**: Many activities identical to Software Configuration Management (SCM) techniques

---

## 7.2 Establishing the Groundwork

### Reality vs. Ideal

**Ideal Setting**: Stakeholders and software engineers work together on same team with meaningful colleague conversations

**Reality Challenges**:
- Customers/users in different cities/countries
- Vague understanding of requirements
- Conflicting opinions about system
- Limited technical knowledge
- Limited interaction time with requirements engineer

### 7.2.1 Identifying Stakeholders

**Stakeholder Definition** (Sommerville and Sawyer): "Anyone who benefits in a direct or indirect way from the system which is being developed"

**Stakeholder Categories**:
- Business operations managers
- Product managers
- Marketing people
- Internal and external customers
- End users
- Consultants
- Product engineers
- Software engineers
- Support and maintenance engineers

**Key Characteristics**:
- Each has different system view
- Achieves different benefits from successful development
- Open to different risks if development fails

**Process**: Create initial contributor list at inception; list grows as stakeholders contacted (ask each: "Whom else should I talk to?")

### 7.2.2 Recognizing Multiple Viewpoints

**Stakeholder Perspectives**:
- **Marketing**: Features exciting potential market, easy to sell
- **Business Managers**: Feature set buildable within budget, ready for market windows
- **End Users**: Familiar, easy-to-learn, easy-to-use features
- **Software Engineers**: Infrastructure-enabling functions (invisible to nontechnical stakeholders)
- **Support Engineers**: Software maintainability

**Challenge**: Information from multiple viewpoints may be inconsistent or conflicting

**Solution**: Categorize all stakeholder information (including inconsistent/conflicting) enabling decision makers to choose internally consistent requirement sets

**Common Elicitation Problems**:
- Unclear project goals
- Differing stakeholder priorities
- Unspoken assumptions
- Different meaning interpretations
- Requirements difficult to verify

### 7.2.3 Working Toward Collaboration

**Challenge**: Multiple stakeholders = multiple opinions about proper requirements

**Requirements Engineer Role**:
- Identify commonality areas (agreed-upon requirements)
- Identify conflict/inconsistency areas (conflicting stakeholder desires)

**Collaboration Models**:
- Not necessarily "defined by committee"
- Stakeholders provide requirement views
- Strong "project champion" (business manager/senior technologist) may make final decisions

### Planning Poker Technique

**Purpose**: Resolve conflicting requirements while understanding relative importance

**Process**:
1. Provide all stakeholders with priority points to "spend"
2. Present requirements list
3. Each stakeholder indicates relative importance by spending points
4. Spent points cannot be reused
5. No further action when points exhausted
6. Total points per requirement indicate overall importance

### 7.2.4 Asking the First Questions

**Context-Free Questions**: Asked at project inception

**First Set - Customer and Stakeholder Focus**:
- Who is behind the request for this work?
- Who will use the solution?
- What will be the economic benefit of a successful solution?
- Is there another source for the solution that you need?

**Purpose**: Identify all interested stakeholders, measurable benefits, possible alternatives to custom development

**Second Set - Problem Understanding**:
- How would you characterize "good" output from successful solution?
- What problem(s) will this solution address?
- Can you show/describe the business environment for solution use?
- Will special performance issues or constraints affect solution approach?

**Third Set - Meta-Questions** (Communication Effectiveness):
- Are you the right person to answer these questions? Are your answers "official"?
- Are my questions relevant to your problem?
- Am I asking too many questions?
- Can anyone else provide additional information?
- Should I be asking you anything else?

**Important Note**: Q&A format should be used for first encounter only, then replaced with requirements elicitation format combining problem solving, negotiation, and specification elements.

### 7.2.5 Nonfunctional Requirements (NFRs)

**Definition**: Quality attribute, performance attribute, security attribute, or general system constraint

**Challenge**: Often difficult for stakeholders to articulate; lopsided emphasis on functionality despite NFRs being necessary for useful/usable software

**Two-Phase Approach**:

**Phase 1**:
- Establish software engineering guidelines for system (best practices, architectural style, design patterns)
- Develop NFR list (usability, testability, security, maintainability)
- Create relationship matrix comparing guideline pairs (complementary, overlapping, conflicting, independent)

**Phase 2**:
- Prioritize each NFR
- Create homogeneous NFR set using decision rules
- Determine which guidelines to implement/reject

### 7.2.6 Traceability

**Definition**: Documented links between software engineering work products (requirements and test cases)

**Traceability Matrix Structure**:
- Rows: Requirement names
- Columns: Software engineering work product names (design elements, test cases)
- Cells: Marked to indicate links between requirements and work products

**Benefits**:
- Provide developer continuity across project phases (regardless of process model)
- Ensure engineering work products account for all requirements
- Track requirement impact and evolution

**Challenge**: Increasingly difficult to maintain as requirements and work products grow

**Importance**: Essential to create tracking means for product requirement impact and evolution

---

## 7.3 Requirements Gathering

**Nature**: Combines elements of problem solving, elaboration, negotiation, and specification

**Approach**: Collaborative, team-oriented with stakeholders working together to:
- Identify the problem
- Propose solution elements
- Negotiate different approaches
- Specify preliminary solution requirements

### 7.3.1 Collaborative Requirements Gathering

**Basic Guidelines** (applied across various approaches):
- Meetings (real or virtual) with software engineers and stakeholders
- Established preparation and participation rules
- Formal enough agenda covering important points, informal enough for free idea flow
- Facilitator control (customer, developer, or outsider)
- Definition mechanism (worksheets, flip charts, wall stickers, electronic bulletin board, chat room, virtual forum)

**Process Foundation**:
- One or two-page "product request" generated during inception
- Meeting logistics arranged (place, time, date)
- Facilitator chosen
- Stakeholder organization attendees invited
- Product request distributed before meeting

**Critical User Representation**: If system serves many users, ensure requirements elicited from representative cross-section (high acceptance risk if only one user defines requirements)

### SafeHome Project Example

**Product Request Excerpt** (Marketing perspective):
> "Our research indicates that the market for home management systems is growing at a rate of 40 percent per year. The first SafeHome function we bring to market should be the home security function. Most people are familiar with 'alarm systems,' so this would be an easy sell. We might also consider using voice control of the system using some technology like Alexa.

> The home security function would protect against and/or recognize a variety of undesirable 'situations' such as illegal entry, fire, flooding, carbon monoxide levels, and others. It'll use our wireless sensors to detect each situation, can be programmed by the homeowner, and will automatically contact a monitoring agency and the owner's cell phone when a situation is detected."

**Pre-Meeting Preparation** (Each attendee creates lists):

**Objects List**: Environment components, system-produced items, system-used items
- *SafeHome examples*: control panel, smoke detectors, window/door sensors, motion detectors, alarm, event, display, tablet, telephone numbers, telephone call

**Services List**: Processes/functions manipulating or interacting with objects
- *SafeHome examples*: configuring system, setting alarm, monitoring sensors, dialing phone via wireless router, programming control panel, reading display

**Constraints List**: Limitations and business rules
- *SafeHome examples*: must recognize non-operating sensors, must be user friendly, must interface to standard phone line

**Performance Criteria List**: Speed, accuracy, security requirements
- *SafeHome examples*: sensor event recognition within 1 second, event priority scheme implementation

**Meeting Process**:
1. Post individual lists (wall sheets, adhesive sheets, wall board, group forum, website, social networking)
2. Ensure individual list entry manipulation capability
3. **Strict prohibition of critique and debate initially**
4. Create combined lists by eliminating redundancy, adding new ideas, avoiding deletions
5. Facilitator-coordinated discussion
6. Develop consensus through shortening, lengthening, or rewording
7. Create mini-specifications or use cases for items requiring further explanation

**Mini-Specification Example** (SafeHome Control Panel):
> "The control panel is a wall-mounted unit that is approximately 230 × 130 mm in size. The control panel has wireless connectivity to sensors and a tablet. User interaction occurs through a keypad containing 12 keys. A 75 × 75 mm OLED color display provides user feedback. Software provides interactive prompts, echo, and similar functions."

**Issues Management**: Maintain issues list for unresolvable meeting items requiring later action

### Case Study: Requirements Gathering Meeting

**Participants**: Jamie Lazar, Vinod Raman, Ed Robbins (software team); Doug Miller (software engineering manager); marketing members; product engineering representative; facilitator

**Key Discussion Points**:
- Internet accessibility for all SafeHome functionality
- Security constraints (technical and legal)
- Liability concerns regarding system hacking
- System refinement and expansion needs

**Process Observations**:
- Facilitator manages discussion flow
- Technical debates deferred to maintain focus
- Action items noted for later resolution
- Continuous refinement and expansion of requirements

**Critical Stakeholder Questions**:
- Can we build the system?
- Will development process enable market competition?
- Do adequate resources exist for building and maintenance?
- Will system performance meet customer needs?

### 7.3.2 Usage Scenarios

**Purpose**: Understand how features will be used by different end user classes

**Definition**: Scenarios (use cases) provide system usage descriptions from user perspective

**Development Process**: Developers and users create scenario sets identifying system usage threads

**Function**: Bridge between requirements gathering and technical software engineering activities

### Case Study: Preliminary User Scenario Development

**Scenario Context**: Remote access to home security function

**Example Process**:
1. Marketing person describes usage motivation (letting housekeeper/repair person into house)
2. Step-by-step usage description:
   - Access secure website
   - Provide user ID and two-level passwords
   - Select home security function
   - Verify identity (address/phone number)
   - View control panel representation
   - Access available functions (arm/disarm system, sensor control, zone reconfiguration)

**Exception Handling**: Note forgotten password scenarios and other edge cases for later resolution

**Documentation**: Facilitator or participant notes form basis for informal usage scenarios

### 7.3.3 Elicitation Work Products

**Large Systems Work Products**:
1. Statement of need and feasibility
2. Bounded scope statement for system/product
3. List of customers, users, other stakeholders participating in elicitation
4. Description of system's technical environment
5. Requirements list (organized by function) with applicable domain constraints
6. Usage scenarios set providing insight into system use under different operating conditions

**Review Process**: All work products reviewed by all requirements elicitation participants

---

## 7.4 Developing Use Cases

### Fundamental Concepts

**Use Case Definition**: Stylized story about end user interaction with system under specific circumstances

**Story Formats**:
- Narrative text (user story)
- Outline of tasks or interactions
- Template-based description
- Diagrammatic representation

**Perspective**: Always depicts software/system from end user's point of view

### Actor Definition and Identification

**Actor Definition**: Anything communicating with system/product that is external to the system itself

**Key Characteristics**:
- Represents roles people/devices play during system operation
- External entities (often people) playing one role in use case context
- Each actor has one or more goals when using system

**Important Distinction**: Actor ≠ End User
- Typical user may play several different roles
- Actor represents class of external entities playing just one role in use case context

**First Step**: Define set of "actors" involved in the story

**Process**: Use cases are discussed in greater detail in subsequent sections (referenced as Section 7.4 continuation)

---

## Key Takeaways

### Critical Success Factors
1. **Early Engagement**: Begin requirements engineering during communication activity
2. **Stakeholder Collaboration**: Essential for successful system development
3. **Iterative Approach**: Expect continuous refinement throughout project
4. **Multiple Perspectives**: Recognize and accommodate different stakeholder viewpoints
5. **Validation**: Continuous review and validation prevent late-project disasters

### Common Pitfalls
1. **Premature Development**: Jumping into coding without clear requirements understanding
2. **Single Stakeholder Dependence**: High acceptance risk when only one user defines requirements
3. **Inadequate Validation**: Insufficient review leading to ambiguous or conflicting requirements
4. **Change Resistance**: Failing to establish change management mechanisms
5. **Documentation Neglect**: Poor traceability and specification management

### Process Integration
- Requirements engineering spans multiple software engineering activities
- Boundaries between tasks are often "muddy"
- Design work occurs during requirements activities and vice versa
- Continuous stakeholder communication essential throughout process
- Work products must be reviewed and validated by all participants

### Long-term Perspective
- Requirements will change throughout project life
- Change desire persists throughout system life
- Management mechanisms essential for tracking and controlling changes
- Traceability becomes increasingly important as system complexity grows
- Foundation quality directly impacts design and construction success