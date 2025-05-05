[JetFolio](..\README.md) \ [docs](../README.md) \

# Architecture Decision Records (ADRs)

This folder contains the **Architecture Decision Records (ADRs)** for JetFolio. ADRs document the key architectural decisions made during the development of JetFolio, including the context, alternatives considered, and reasoning behind each decision. These records ensure transparency, consistency, and traceability throughout the project lifecycle.

## Purpose

ADRs serve as a historical record of the architectural direction of JetFolio. By documenting decisions, we can:
- Understand why certain choices were made at specific points in time.
- Evaluate the impact of these decisions on the project’s evolution.
- Provide a reference for revisiting decisions as new requirements or constraints emerge.

## Structure

Each ADR follows a standardized format to ensure consistency and readability. The typical structure includes:
- **Status:** Indicates whether the decision is proposed, accepted, rejected, deprecated, or superseded.
- **Context and Problem:** Describes the situation and challenges prompting the decision.
- **Decision Drivers:** Outlines the key factors influencing the decision.
- **Considered Options:** Lists the options evaluated and their pros/cons.
- **Decision Outcome:** Details the chosen solution and its implications.
- **Implementation:** Steps required to execute the decision.
- **Confirmation:** Criteria for validating the decision's success.

## Current ADRs

| Id                                           | Status   | Name                                                         |
| -------------------------------------------- | -------- | ------------------------------------------------------------ |
| [0001](0001-choice-of-database.md)           | Accepted | Choice of Database – Azure SQL vs. NoSQL                     |
| [0002](0002-deployment-platform.md)          | Accepted | Deployment Platform – Azure Container Apps vs. Azure App Service or AKS |
| [0003](0003-framework-and-language.md)       | Accepted | Framework and Language – C#/.NET Core for Console and API    |
| [0004](0004-use-of-entity-framework-core.md) | Accepted | Use of Entity Framework Core (ORM) – Adopt vs. Direct SQL or Dapper |

## How to Propose a New ADR

To propose a new ADR:
1. Copy the [ADR Template](./adr-template.md) and create a new file following the naming convention.
2. Complete all sections in the template with clear and concise information.
3. Submit the ADR for review through the established approval process (e.g., pull request or team discussion).
4. Update the **Current ADRs** section once the ADR is accepted.

## Maintaining ADRs

- **Review Regularly:** Revise ADRs to ensure they remain relevant and valid as the project evolves.
- **Supersede When Necessary:** If a decision is outdated or no longer applicable, create a new ADR to supersede it. Maintain references to the superseded record for traceability.

## Additional Resources

- [About Architecture Decision Records](https://adr.github.io/)
- [JetFolio Flight Plan](../JetFolio-Flight-Plan.md)

---

By maintaining this repository of decisions, JetFolio ensures a clear and consistent architectural vision while embracing the flexibility to adapt as needed.