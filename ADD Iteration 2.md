# 1.0 Refined Decomposition of Major Components
## 1.1 AI Engine Subcomponents
- Intent Classifier  
- Entity Extractor  
- Dialogue Manager  
- Response Generator  
- Model Selector  
- Context Retriever

## 1.2 User Interaction Service Subcomponents
- Session Manager  
- User Profile Manager  
- History Manager  
- Preference Manager  

## 1.3 Integration Service Subcomponents
- LMS Adapter  
- Registration Adapter  
- Calendar Adapter  
- Email Adapter  
- Data Normalizer  
- Retry / Circuit Breaker Module  

## 1.4 Dashboard Service Subcomponents
- Schedule Aggregator  
- Deadline Tracker  
- Performance Analyzer  
- Export-to-Calendar Processor  

## 1.5 Notification Service Subcomponents
- Push Notification Sender  
- Email Broadcaster  
- Reminder Scheduler  
- Event Trigger Processor
---
# 2.0 Domain-Specific Components
These components implement AIDAP-specific logic:
- Academic Query Processor  
- Student Schedule Mapper  
- Course Announcement Broadcaster  
- Analytics Aggregator  
- SSO Role Resolver  
- Offline Cache Handler
---
# 3.0 Interface Specifications
## 3.1 External Interfaces
### API Gateway → Clients
- **POST /ask** — Submit question  
- **GET /dashboard** — Personalized dashboard  
- **POST /login** — Redirect to SSO  
- **GET /notifications** — Fetch preferences
### Integration Service → External Systems
- `GET /lms/course/{id}`
- `GET /calendar/events?user={id}`
- `GET /registration/enrollments/{studentId}`
- `POST /email/send`

## 3.2 Internal Interfaces
### API Gateway → AI Engine
```plaintext
POST /ai/process
Input: user query, session ID
Output: structured AI response
```
### AI Engine → Integration Service
- `GET /data/schedule/{studentId}`
- `GET /data/grades/{courseId}`
### AI Engine → User Service
- `GET /history/{userId}`
- `POST /history/update`
### Notification Service → User Service
- `GET /preferences/{userId}`
---
# 4.0 Domain-Specific Models
## 4.1 Conceptual Data Model  
**Entities:**
- **User** (id, name, role, language, preferences)  
- **ConversationHistory** (userId, timestamp, query, response)  
- **Course** (courseId, instructorId, schedule)  
- **Event** (title, deadline, courseId, date)  
- **Notification** (userId, channel, trigger, message)
---
## 4.2 AI Processing Pipeline Model
1. User Query → Intent Classifier  
2. → Entity Extractor  
3. → Dialogue Manager  
4. → Context Retriever  
5. → Integration Fetch  
6. → Response Generator  
7. → User Service for logging  
---
# 5.0 Deployment View
## Deployment Refinements
- Multiple replicas of the AI Engine  
- Dedicated Redis cache cluster  
- Separate analytics database  
- Event bus (Kafka / PubSub)  
- Circuit breaker pattern on Integration Service  
- Secrets manager for API keys  
## Node Details
- Worker nodes for AI workloads  
- Gateway cluster for high availability  
- Monitoring with alerts  
---
