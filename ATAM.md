**Scenario (QA-7):** Integrate a new academic database using GraphQL.

| Category | Details |
| :--- | :--- |
| **Attributes** | Interoperability and Modifiability |
| **Stimulus** | A new database is to be added with GraphQL instead of REST |
| **Environment** | N/A / Normal load |
| **Response** | The system adds the new database without changing any other relevant code. The integration translates GraphQL to work with the predefined REST system |

---

## Architecture Decisions (AD)

| Architecture Decision | Sensitivity | Tradeoff | Risk | Non-Risk |
| :--- | :--- | :--- | :--- | :--- |
| **AD1 - Adapter Pattern** | | T1 | R1 | N1 |
| **AD2 - Integration Router** | | T2 | R2 | N2 |
| **AD3 - Security Module** | | | R3 | N3 |

---

## Analysis Breakdown

### Risks
* **R1:** The risk of accuracy given the use of an adapter, rather than speaking directly through REST.
* **R2:** Single point of failure for outside applications.
* **R3:** Using one Security module for both REST and GRAPHQL could allow malicious GraphQL commands.

### Non-risks
* **N1:** Adapter pattern is standard and mature making it low risk.
* **N2:** Direct integration with REST or GraphQL through integration router.
* **N3:** Adds a barrier from the external application to the core system.

### Trade-offs
* **T1 (Interoperability (+) vs Correctness (-)):** Improves interoperability by adapting to many different databases, at the potential cost of data accuracy if database is not fully compatible with GraphQL.
* **T2 (Speed (-) vs Scalability(+)):** Lowers the speed of the interaction but gains flexibility and scalability.
### Utility Tree
<img width="651" height="291" alt="Utility Tree drawio" src="https://github.com/user-attachments/assets/74254f5c-7e7f-4191-a9d7-d8cf7dc05dfc" />
