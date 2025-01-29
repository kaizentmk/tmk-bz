# Architect

## microservices

- Highly maintainable and testable
- Loosely coupled
- Independently deployable
- Organized around business capabilities
- Owned by a small team

### Links

- [Best Practices for Building a Microservice Architecture](https://github.com/katopz/best-practices/blob/master/best-practices-for-building-a-microservice-architecture.md)
- [Best Practices for Building a Microservice Architecture](https://www.vinaysahni.com/best-practices-for-building-a-microservice-architecture)
- [the twelve-factor app](https://12factor.net/)
- [microservices io](https://microservices.io/)

__The patterns__

Application architecture patterns

- Monolithic architecture
- Microservice architecture

Decomposition

- Decompose by business capability
- Decompose by subdomain
- Self-contained Service
- Service per teamn

Refactoring to microservices

- Strangler Application
- Anti-corruption layer

Data management

- Database per Service
- Shared database
- Saga
- API Composition
- CQRS
- Domain event
- Event sourcing

Transactional messaging

- Transactional outbox
- Transaction log tailing
- Polling publisher

Testing

- Service Component Test
- Consumer-driven contract test
- Consumer-side contract test

Deployment patterns

- Multiple service instances per host
- Service instance per host
- Service instance per VM
- Service instance per Container
- Serverless deployment
- Service deployment platform

Cross cutting concerns

- Microservice chassis
- Service Template
- Externalized configuration

Communication style

- Remote Procedure Invocation
- Messaging
- Domain-specific protocol
- Idempotent Consumer

External API

- API gateway
- Backend for front-end

Service discovery

- Client-side discovery
- Server-side discovery
- Service registry
- Self registration
- 3rd party registration
        
Reliability

- Circuit Breaker

Security

- Access Token

Observability

- Log aggregation
- Application metrics
- Audit logging
- Distributed tracing
- Exception tracking
- Health check API
- Log deployments and changes
       
UI patterns

- Server-side page fragment composition
- Client-side UI composition

## Micro S communication

### gRPC

Benefits:

- Communicating through HTTP/2
- Receiving and sending data with binary form
- Using protocol buffers for parsing data
- Multiple parallel requests, Thanks to HTTP/2!

## Popular concepts in system design
    · Distributed System
    · Network & Protocols
    · Rational Databases
    · Non Rational Databases
    · Database Partition
    · ACID vs BASE
    · SQL vs NoSQL
    · Caching
    · CAP Theorem
    · Throughput
    · Scaling
    · Latency
    · Availability
    · Consistent Hashing
    · Proxies
    · Load Balancers
