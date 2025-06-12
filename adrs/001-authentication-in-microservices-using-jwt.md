# ADR 001: Authentication in microservices using JWT

**Date:** 2024-09-23

## Context
In our project, we have an API Gateway and microservices, including visits and accounts. Previously, JWT authentication was managed at the API Gateway level. It became necessary to determine where the JWT token verification should take place.

## Decision
We decided to move the JWT token verification to the accounts microservice. This way, the API Gateway will only serve as a pass-through for requests, while the actual user verification will occur in the accounts microservice, which manages user data.

## Consequences
  - **Positive:** Better separation of responsibilities between components. Verification happens in the service that manages user data.
  - **Negative:** The additional HTTP request between microservices may introduce some latency.

## Alternatives
Keeping the verification in the API Gateway: We considered keeping JWT verification in the API Gateway, but this would have required moving user logic to the Gateway level, complicating its functionality.