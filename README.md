# microservices-fastapi
Building a full fledged  Microservices using FastAPI

### User Registration
```mermaid
sequenceDiagram
  App Client->>Backend: Create User (POST Request)
  Backend-->>Database: Log Credentials
  activate Database
  Database-->>Backend: Credentials Stored
  deactivate Database
  Backend->>App Client: HTTP 201 Response
```

### User Login
```mermaid
sequenceDiagram
  App Client->>Backend: User Credentials (POST Request)
  Backend-->>Database: Query using Username
  activate Database
  Database-->>Backend: Retrieve Credentials based on Username
  deactivate Database
  activate Backend
  Backend->>Backend: Validate Credentials
  deactivate Backend
  alt Validation Successful
    Backend->>App Client: Generate JWT Token
  else Validation Failed
    Backend->>App Client: HTTP 403 Response
  end
```

### Data Processing
#### Without using Celery/RabbitMQ
```mermaid
sequenceDiagram
  App Client->>Backend: Data + JWT Token(POST Request)
  activate Backend
  Backend->>Backend: Data Processing
  Backend-->>Database: Log Features
  deactivate Backend
  activate Database
  Database-->>Backend: Features Stored
  deactivate Database
  Backend->>App Client: HTTP 201 Response
```

### ML Training
#### Without using Celery/RabbitMQ
```mermaid
sequenceDiagram
  App Client->>Backend: Data + JWT Token(POST Request)
  Backend-->>Database: Retrieve Features
  activate Database
  Database-->>Backend: Features Retrieved
  deactivate Database
  activate Backend
  Backend->>Backend: Training
  Backend->>App Client: HTTP 201 Response
  deactivate Backend
```

### ML Realtime Inference
```mermaid
sequenceDiagram
  App Client->>Backend: Data + JWT Token(POST Request)
  activate Backend
  Backend->>Backend: Data Processing
  deactivate Backend
  activate Backend
  Backend->>Backend: Predict
  Backend->>App Client: Prediction HTTP 200 Response
  deactivate Backend
  Backend-->>Database: Log New Data
  activate Database
  Database-->>Backend: New Data Stored
  deactivate Database
```

### ML Batch Inference
#### Without using Celery/RabbitMQ
```mermaid
sequenceDiagram
  App Client->>Backend: Data + JWT Token(POST Request)
  Backend-->>Database: Retrieve Features
  activate Database
  Database-->>Backend: Features Retrieved
  deactivate Database
  activate Backend
  Backend->>Backend: Predict
  Backend-->>Database: Log New Data
  deactivate Backend
  activate Database
  Database-->>Backend: New Data Stored
  deactivate Database
```
