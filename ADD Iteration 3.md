## Step 2: Establish Goal By Selecting Drivers
* **Primary Driver:** QA-7 
  * Scenario: A new academic database is added via GraphQL without changing the core system.
  * Rationale: External data sources change frequently. Decoupling them prevents bugs in the main application.
  * Success Criteria: Integration of the new database requires zero lines of code changed in the Core System.
* **Secondary Driver:** Constraint 
  * Scenario: The adapter must run within the existing Application Server Cluster without requiring new hardware.

## Step 3: Choose one or more elements of the system to refine
* **Database Cluster**
  * Add an adapter pattern using GraphQL to allow for interoperability and the ability to implement new databases without changing the core system
* **Integration Service**
  * Redefine the service to support a hybrid interface pattern, partially REST and partially GraphQL
* **Configuration Management**
  * Update the configuration service to load database schemas externally, so the system can adapt to new databases without code changes
* **Security Module**
  * Extend the current authentication filters to validate GraphQL requests alongside existing REST requests
## Step 4: Choose one or more design concepts that satisfy the inputs considered in the iteration

### Design Decisions and Location vs. Rationale

| Design Decisions and Location | Rationale and Assumptions |
| :--- | :--- |
| **Adapter Pattern** | The adapter pattern acts as the interface for GraphQL, allowing the core system to speak directly with GraphQL, simplifying the database integration process. |
| **Abstract Common Services** | The abstract common service tactic routes the database through the existing API service. This allows us to use both the REST API and GraphQL. |
| **External Configuration Pattern** | Move connection strings and schemas to external files. This satisfies the constraint that we shouldn't recompile the code just to add a new database. |
| **Security Filter Chain** | Reuse the existing authentication filters by applying them to the GraphQL endpoint. This ensures the new data path is just as secure as the REST path without rewriting security logic. |

---
# Step 5: Instantiate architectural elements, responsibilities, and define interfaces

## Design Decisions and Location

### 1. Implement the adapter pattern in the applications server cluster
**Rationale and Assumptions**
The adapter pattern element will live in the applications server cluster as it is part of the application logic, and it wraps the GraphQL APIs on the application side.

### 2. Integration router
**Rationale and Assumptions**
Routes the data request to the appropriate adapter either REST or GraphQL. This component serves as an entry point so the system doesn't need to know which protocol is being used.

### 3. External Configuration Manager
**Rationale and Assumptions**
This component loads database connection strings and schemas from external files. This allows the system to adapt to new databases without recompiling the source code.

### 4. Security Filter Chain
**Rationale and Assumptions**
Reuse the existing authentication filters by applying them to the GraphQL endpoint. This ensures the new data path is just as secure as the REST path without rewriting security logic.

## Step 6: Sketch Views
### Sequence Diagram
![Sequence Diagram1](https://github.com/user-attachments/assets/29e813ac-865f-4738-816b-572b1607eff6)
### Deployment Diagram
<img width="1781" height="1082" alt="Iteration 3 drawio" src="https://github.com/user-attachments/assets/6315a016-0376-43b3-8f8b-289a7b3099fc" />
### Utility Tree
<img width="651" height="291" alt="Utility Tree drawio" src="https://github.com/user-attachments/assets/74254f5c-7e7f-4191-a9d7-d8cf7dc05dfc" />


## Step 7: Design Decisions and Location vs. Rationale

| Design Decisions and Location | Rationale and Assumptions |
| :--- | :--- |
| `Adapter Pattern` | **(QA-7 Interoperability)** Wraps the GraphQL APIs so the main application can communicate with the new database easily. |
| `Integration Router` | **(QA-7 Interoperability)** Directs data requests to the correct adapter (REST or GraphQL) so the core system doesn't need to worry about the protocol. |
| `External Configuration Manager` | **(QA-6 Modifiability)** Loads settings from external files, allowing updates to schemas or keys without needing to change the code. |
| `Security Filter Chain` | **(QA-2 Security)** Applies existing security checks to the new GraphQL endpoint to ensure all requests are properly authenticated. |
