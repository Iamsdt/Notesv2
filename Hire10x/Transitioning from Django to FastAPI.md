---
Created by: Shudipto Trafder
Created time: 2024-11-12T22:05:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - guidline
  - django
  - fastapi
---

## Summary

In response to evolving technological demands and the need for enhanced performance and scalability, we propose transitioning our platform from Django to FastAPI. This document outlines the strategic benefits, anticipated learning curve, and projected timeline for this significant migration.

## Learning and Adoption Strategy

### Learning Curve Assessment

Our team has already successfully implemented FastAPI in our Stats Server and Admin Server, significantly mitigating the learning curve. For ORM functionality, we propose transitioning from Django ORM to Tortoise ORM, which shares similarities with our current system and has been successfully integrated into our Stats Server. This existing experience positions us favorably for a smooth transition.

## Code Migration Strategy

### Codebase Adaptation

1. **Routing Architecture**: FastAPI employs a more explicit routing system compared to Django's approach. This will necessitate a careful restructuring of our URL patterns to align with FastAPI's methodology.

2. **Data Models and Schemas**: The migration involves transitioning from Django's ORM models to Tortoise ORM. This change offers enhanced support for database routing and multi-schema operations. Additionally, Tortoise ORM's seamless integration with Pydantic provides robust data validation capabilities, extending to API input validation.

3. **Asynchronous Programming Paradigm**: While the core logic from our Django implementation can be largely preserved, a key aspect of this migration involves converting synchronous code to asynchronous. This transformation is crucial for leveraging FastAPI's performance benefits.

### Database and API Design Considerations

- **Database Architecture**: We plan to implement Tortoise ORM, which aligns closely with Django ORM's paradigms. This approach has been validated in our Stats Server, particularly in customer onboarding processes.

- **API Design Optimization**: FastAPI's comprehensive support for OpenAPI standards necessitates a strategic redesign of our API endpoints. This redesign will fully capitalize on these features, facilitating automatic documentation generation for both Swagger and ReDoc interfaces. Furthermore, we can leverage Swagger to develop our mock server, enhancing our development and testing processes.

## Implementation Timeline

Considering the scope of changes required, including a comprehensive review of our database structure and API design, we propose a strategic migration timeline. The process of converting reusable code from synchronous to asynchronous paradigms is a critical factor in our timeline estimation. Taking these considerations into account, we recommend a soft deadline of 15 business days for completing this migration.

## Anticipated Performance Enhancements

### Enhanced API Serving Capabilities

- FastAPI's asynchronous architecture is expected to significantly boost our request handling capacity, particularly in high-concurrency scenarios.
- We anticipate marked improvements in response times and a reduction in server load, contributing to a more scalable and efficient system architecture.

### Benchmark Results

We conducted comprehensive benchmarks to quantify the performance improvements. The testing scenarios and results are as follows:

**Test Scenarios**:

1. **Operations Without Database Interaction**:
   - GET Request: Generate and return a random number.
   - POST Request: Receive and echo JSON data.

2. **Operations With Database Interaction** (1M pre-existing records):
   - GET Request: Retrieve a record by randomly generated ID.
   - POST Request: Persist received JSON data and return the saved entity.

**Testing Environment**:
- Database: PostgreSQL (containerized)
- Application Container: Docker
- Worker Processes: 2
- Hardware: 12 GB RAM, 4 CPUs (limited to 2 CPU usage)

![[Pasted image 20240712230242.png]]

## Conclusion and Recommendations

The proposed transition from Django to FastAPI represents a strategic enhancement of our technology stack, aimed at significantly improving our system's performance and scalability. By leveraging our team's existing proficiency with FastAPI and Tortoise ORM, we are well-positioned to execute this migration efficiently.

This strategic move is expected to yield several key benefits:
1. Enhanced capability to handle higher concurrency
2. Reduced server load
3. Improved response times

These improvements will collectively contribute to a more robust and scalable system architecture, better equipped to meet our evolving technological demands.

We recommend proceeding with this migration, allocating a 15-business-day timeline for implementation. This time frame reflects our commitment to a thorough yet efficient transition, positioning our organization for continued technological advancement and market leadership.