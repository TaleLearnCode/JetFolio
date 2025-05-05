[JetFolio](..\README.md) \ [docs](../README.md) \ [Architecture Decision Records (ADRs)](README.md) \

# Choice of Database – Azure SQL vs. NoSQL

- **Id**: 0001
- **Status:** Accepted
- **Date:** 2025-04-28
- **Work Item:** *001-DatabaseDecision*

## Context and Problem

JetFolio needs a reliable and scalable database to store structured flight data, including bookings, segments, flights, airlines, and loyalty program information. The database must handle relational data and provide transactional consistency, as the integrity of flight records and relationships between entities is critical for analytics and functionality.

However, as JetFolio grows, scalability and flexibility become increasingly important. The decision was whether to use a relational database (Azure SQL) or a NoSQL database (Azure Cosmos DB) to meet the initial and evolving requirements of the system.

## Decision Drivers

- **Structured, Relational Data:** Flight records and related entities (e.g., Airlines, Loyalty Programs) naturally fit into a structured schema with clear relationships.
- **Transactional Consistency:** JetFolio requires ACID compliance to ensure that operations like adding flights and updating loyalty data are atomic and reliable.
- **Analytics Requirements:** The system needs SQL querying capabilities for calculating travel metrics and aggregating data, which relational databases excel at.
- **Projected Data Volume:** JetFolio’s initial scope involves moderate data volumes that do not justify NoSQL’s horizontal scaling.
- **Familiarity:** The development team has expertise with Azure SQL and Entity Framework Core, easing implementation and reducing risk.

## Considered Options

- **Azure SQL Database (Relational)**  
- **Azure Cosmos DB (NoSQL)**  
- **File Storage**  

## Decision Outcome

**Chosen option:** **Azure SQL Database**, because it aligns well with JetFolio’s need for structured relational data, transactional consistency, and SQL querying capabilities. The dataset size is expected to be moderate, where a single relational database is more practical than NoSQL alternatives. 

### Consequences

- **Good:**  
  - ACID transactions ensure data integrity, even during complex operations.  
  - SQL querying supports robust analytics for reporting and insights.  
  - Entity Framework Core integration simplifies data access and management.  

- **Bad:**  
  - Schema rigidity may require migrations if the data model evolves.  
  - Relational databases scale less horizontally compared to NoSQL.  

### Implementation

1. Provision an Azure SQL Database instance with appropriate performance tier (initially Basic or Standard).  
2. Design the relational schema to represent flight records and their relationships.  
3. Scaffold Entity Framework Core models to map the database schema for use in the Web API.  
4. Optimize indexes for common queries and establish backup/restore policies.  
5. Monitor database usage and scale to higher tiers as necessary.

### Confirmation

Compliance will be confirmed through integration testing between the Web API and Azure SQL. Additionally, performance testing of data operations (e.g., querying flights) will validate the database meets expected benchmarks. Any schema updates will undergo review and testing.

## Pros and Cons of the Options

### Azure SQL Database

- **Good:**  
  - Supports structured relational data with well-defined relationships.  
  - Provides ACID compliance for transactional operations.  
  - Enables robust analytics via SQL queries.  
  - Familiar development and operational processes simplify implementation.  

- **Bad:**  
  - Schema rigidity makes major changes more challenging.  
  - Vertical scaling may be needed as data size grows, potentially increasing costs.

### Azure Cosmos DB

- **Good:**  
  - Highly scalable horizontally, suited for large datasets and distributed systems.  
  - Flexible schema supports unstructured and semi-structured data.  
  - Global distribution capabilities can improve performance for international users.  

- **Bad:**  
  - Less optimal for relational analytics due to lack of SQL joins.  
  - Eventual consistency models may lead to unpredictable results for transactional operations.  
  - Higher complexity in implementing data models compared to Azure SQL.

### File Storage

- **Good:**  
  - Minimal overhead; can store data in formats like JSON or CSV.  
  - Simple implementation with almost zero infrastructure costs.  

- **Bad:**  
  - No transactional consistency or relational capabilities.  
  - Lacks indexing and querying features required for analytics.  
  - Not scalable for larger datasets or multi-user scenarios.

## More Information

Entity Framework Core was chosen as the data access layer to simplify interaction with the Azure SQL Database. It supports LINQ queries and change tracking while allowing raw SQL queries when necessary for performance optimization. Future scalability needs (e.g., read replicas or partitioning) will be evaluated as usage grows.

No more additional information available.

## Follow-On Information

This ADR will be revisited if JetFolio’s dataset exceeds the capacity of Azure SQL’s performance tiers or if global distribution and eventual consistency are required for a NoSQL approach.

## Record History

* **Proposed:** 2025-04-20  
* **Accepted:** 2025-04-28  
* **Last Reviewed:** 2025-04-28  