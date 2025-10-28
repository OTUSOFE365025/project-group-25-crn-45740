# 2.3 Quality Attribute Scenarios 
| **ID**   | **Quality Attribute** | **Scenario**                                                                                                                                           | **Associated Use Case** |
|------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| QA-1 | Availability      | The server goes down due to a cyber attack, causing the automatic failover to initiate and recover backup information from a parallel database.    | UC-4                |
| QA-2 | Security          | A student tries to login as their professor, blocking the attempt after failed attempts, while also notifying the professor of an attempted login. | UC-6                |
| QA-3 | Usability         | A student asks administration for his time schedule, and the AIDAP AI filters through the database to find the specific student’s time table.      | UC-1                |
| QA-4 | Scalability       | After an influx of students, the maintainer will be able to scale systems to accommodate said influx.                                              | UC-2                |
| QA-5 | Availability      | When a professor posts an assignment, a notification is broadcasted to everyone in the selected course at the time of posting.                     | UC-3                |
| QA-6 | Modifiability     | A system maintainer updates the AI model’s API key without downtime or code changes                                                                | UC-9                |
| QA-7 | Interoperability  | A new academic database is added via GraphQL without changing the core system                                                                      | UC-5                |
| QA-8 | Reliability       | If the calendar data source fails, AIDAP retries the connection every minute until recovery                                                        | UC-4/UC-10          |
