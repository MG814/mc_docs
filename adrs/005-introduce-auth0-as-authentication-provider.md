# ADR 005: Introduce Auth0 as Authentication Provider

**Date:** 2025-02-01

## Context
The project requires a reliable, scalable, and secure authentication mechanism. The previous implementation of a custom authentication system:
- Required additional development and maintenance effort,
- Involved handling passwords, password resets, session management, and security features internally,
- Did not fully meet security and compliance requirements (e.g., GDPR, SOC2).

To accelerate development and improve security, we considered adopting an external authentication provider.

After evaluating available options (Auth0, AWS Cognito, custom solution), we decided to use **Auth0**.

## Decision
We will use **Auth0** as the main authentication provider for all users.

- Users will register and log in through Auth0.
- JWT tokens issued by Auth0 will be used for internal authorization in microservices.
- Additional user data (e.g., phone number) will be synchronized with our `accounts` microservice database after registration or first login.
- The API Gateway will verify the validity of the Auth0 token before forwarding requests to microservices.
- Additional security features (MFA, account lockout, password reset) will be handled by Auth0.

## Consequences
**Positive:**
- Saves time on developing and maintaining a custom authentication system.
- Improves the security level of the application.
- Enables easy integration of features like SSO, MFA, and third-party login (Google, Apple).
- Ensures scalability and compliance with legal regulations.

**Negative:**
- Introduces dependency on an external provider.
- Increases costs (after exceeding Auth0's free tier).
- Requires adaptation of existing login and registration flows.

## Status

Decision implemented.