## Step 2: Establish Goal By Selecting Drivers
* Addressing the QA-7 quality attribute scenario: A new academic database is added via GraphQL without changing the core system.

## Step 3: Choose one or more elements of the system to refine
* **Database Cluster**
  * Add an adapter pattern using GraphQL to allow for interoperability and the ability to implement new databases without changing the core system
* **Integration Service**
  * Redefine the service to support a hybrid interface pattern, partially REST and partially GraphQL
## Step 4: Choose one or more design concepts that satisfy the inputs considered in the iteration

### Design Decisions and Location vs. Rationale

| Design Decisions and Location | Rationale and Assumptions |
| :--- | :--- |
| **Adapter pattern to adapt** | The adapter pattern acts as the interface for GraphQL, allowing the core system to speak directly with GraphQL, simplifying the database integration process. |
| **Abstract Common Services** | The abstract common service tactic routes the database through the existing API service. This allows us to use both the REST API and GraphQL |

---

## Step 5: Instantiate architectural elements, responsibilities, and define interfaces

## Step 6: Sketch Views
![Sequence Diagram1](https://github.com/user-attachments/assets/29e813ac-865f-4738-816b-572b1607eff6)

## Step 7:Design Decisions and Location vs. Rationale

| Design Decisions and Location | Rationale and Assumptions |
| :--- | :--- |
| **Implement the adapter pattern in the applications server cluster** | The adapter pattern element will live in the applications server cluster as it is part of the application logic, and it wraps the GraphQL APIs on the application side. |
| **Integration router** | Routes the data request to the appropriate adapter either REST or GraphQL. This component serves as an entry point so the system doesn't need to know which protocol is being used |
