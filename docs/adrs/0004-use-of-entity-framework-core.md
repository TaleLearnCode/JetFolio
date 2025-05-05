[JetFolio](..\README.md) \ [docs](../README.md) \ [Architecture Decision Records (ADRs)](README.md) \

# Use of Entity Framework Core (ORM) – Adopt vs. Direct SQL or Dapper

- **Id**: 0004
- **Status:** Accepted
- **Date:** 2025-04-28
- **Work Item:** *004-EntityFrameworkCoreDecision*

## Context and Problem

JetFolio requires a data access strategy to interact with the Azure SQL Database. The chosen approach must balance performance, ease of development, and maintainability. It should simplify common database operations like querying and updating, while also allowing flexibility for custom SQL when needed. 

Entity Framework Core (EF Core) provides an ORM that abstracts database interactions and enables developers to work with data as strongly-typed .NET objects. It also supports LINQ queries and change tracking, which streamline development. Alternatives like Dapper (a lightweight ORM) or ADO.NET (manual SQL queries) offer more control but require greater effort and expertise. The decision also considers JetFolio's Database-First strategy, where the schema evolves directly in the database.

## Decision Drivers

- **Development Velocity:** Minimize time spent on routine database operations.  
- **Flexibility:** Enable both ORM-based queries and raw SQL for complex use cases.  
- **Team Skills:** Leverage the team’s experience with EF Core and .NET.  
- **Maintainability:** Ensure long-term maintainability with standardized data access patterns.  
- **Performance:** Achieve acceptable performance for JetFolio's expected data volume and query complexity.  

## Considered Options

- **Entity Framework Core (ORM)**  
- **Dapper (Lightweight ORM)**  
- **ADO.NET (Direct SQL)**  

## Decision Outcome

**Chosen option:** **Entity Framework Core**, because it provides the best balance between performance, productivity, and maintainability. EF Core aligns well with JetFolio’s Database-First approach and supports both automated and manual SQL when needed, making it ideal for the project.

### Consequences

- **Good:**  
  - Speeds up development with LINQ and change tracking.  
  - Allows easier management of relationships and schema changes using EF Core models.  
  - Reduces boilerplate code compared to raw SQL approaches.  

- **Bad:**  
  - Slight overhead compared to direct SQL execution.  
  - Requires learning and understanding EF Core’s behavior and performance optimization techniques.

### Implementation

1. Scaffold EF Core models from the Azure SQL database schema using the `dotnet ef dbcontext scaffold` command.  
2. Use EF Core’s `DbContext` for querying and updating the database.  
3. Implement raw SQL queries for performance-critical operations using EF Core’s `FromSql` or `ExecuteSql` methods.  
4. Profile and optimize query performance where necessary using EF Core’s logging and query analyzer tools.  
5. Maintain migrations and model updates as the database schema evolves.  

### Confirmation

Compliance will be confirmed through unit and integration tests for all database operations. Performance benchmarks will be conducted to ensure query execution times remain within acceptable limits for JetFolio’s use case.

## Pros and Cons of the Options

### Entity Framework Core (ORM)

- **Good:**  
  - Abstracts complex database operations, improving productivity.  
  - Supports LINQ for intuitive, strongly-typed querying.  
  - Offers flexibility for raw SQL queries when needed.  
  - Facilitates change tracking for managing object states.  

- **Bad:**  
  - Slight performance overhead compared to direct SQL.  
  - Requires understanding EF Core’s behavior for complex scenarios (e.g., lazy vs. eager loading).

### Dapper (Lightweight ORM)

- **Good:**  
  - Minimal performance overhead, as it’s closer to raw SQL.  
  - Great for highly customized or complex queries.  

- **Bad:**  
  - Requires more boilerplate code compared to EF Core.  
  - Lacks advanced features like change tracking or schema management.  

### ADO.NET (Direct SQL)

- **Good:**  
  - Maximum control over SQL queries and execution.  
  - No abstraction layers, leading to optimal performance.  

- **Bad:**  
  - Time-consuming development due to verbose, boilerplate-heavy code.  
  - Increases risk of errors in query composition and result handling.  
  - Reduced maintainability due to the lack of built-in tools for schema management.  

## More Information

Entity Framework Core supports the Database-First approach, aligning with JetFolio's workflow where schema changes are directly applied to the database. It also allows partial migration support when changes occur. Query performance and memory usage are monitored during implementation to identify and optimize any bottlenecks.

No more additional information available.

## Follow-On Information

This ADR will be revisited if EF Core’s performance becomes a significant bottleneck for JetFolio. Possible triggers include data growth beyond expected volumes or the need for highly specialized queries that EF Core cannot optimize effectively.

## Record History

* **Proposed:** 2025-04-20  
* **Accepted:** 2025-04-28  
* **Last Reviewed:** 2025-04-28  