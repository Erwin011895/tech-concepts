# App Architecture Types

## N-tier architecture

```
Client
Presentation Layer
Business Logic Layer
Data Access layer
Database
```

## Monolithic architecture

```
Client

------------------- single app bundle
Presentation Layer
Business Logic Layer
Data Access layer
-------------------

Database
```

## Microservice architecture

```
Client
API Gateway
Service1    Service2    Service3
Database1   Database2   Database3
```

## Event Driven architecture

```
Client
API Gateway
EventProducer1 -> EventConsumer1
EventProducer2 -> EventConsumer2 -> Database
```
