[JetFolio](..\README.md) \ [docs](README.md) \

# JetFolio Flight Plan Summary

JetFolio is a travel tracking application designed to log, analyze, and manage detailed flight data. It is built using modern cloud and development practices to ensure scalability, usability, and extensibility. This document outlines the foundational architectural vision that guides JetFolio's development and future enhancements.

---

## Vision and Goals

JetFolio's vision is to empower travelers to gain actionable insights from their travel data, enabling smarter decisions and optimized planning. Its primary goals are:
- **Comprehensive Tracking:** Logging flight bookings, segments, and flights, alongside expenses and loyalty program metrics.
- **Actionable Analytics:** Providing insights into travel trends, costs, and loyalty program thresholds.
- **Scalable Design:** Supporting personal use initially, with extensibility for multi-user and enterprise scenarios.

---

## Key Architectural Components

### 1. **Console Application**
A lightweight, text-based interface built with Spectre.Console in C#. This serves as the initial user-facing component, enabling quick input and retrieval of travel data.

### 2. **Web API**
The core business logic layer is implemented in ASP.NET Core and hosted in Azure Container Apps. It:
- Processes user requests via RESTful endpoints.
- Integrates with Entity Framework Core for database interactions.
- Ensures scalability and separation of concerns between interface and backend.

### 3. **Azure SQL Database**
A relational database designed to store structured flight data and relationships. The schema includes:
- Flights, segments, and bookings.
- Supporting tables for airlines, loyalty programs, and currencies.
Its ACID compliance ensures transactional reliability, while SQL queries enable robust analytics.

### 4. **Monitoring and Logging**
JetFolio leverages Azure Monitor and Application Insights for real-time metrics, error tracking, and performance optimization. This ensures operational transparency and quick resolution of issues.

---

## Process Flows Overview

JetFolio implements several high-level flows:
1. **Flight Record Creation:** Users input flight details, which are validated and persisted to the database.
2. **Data Retrieval:** Retrieve all flights or filter by parameters (e.g., airline, date range) for reports and analytics.
3. **Analytics Generation:** Analyze accumulated travel data, calculate expenses, and forecast loyalty program milestones.

Each flow ensures efficiency and reliability, with clear interaction between components.

---

## Architectural Principles

JetFolio is guided by the following principles:
- **Separation of Concerns:** Clear division between user interface, business logic, and data storage.
- **Scalability:** Designed to scale out for multi-user scenarios, leveraging serverless technologies.
- **Flexibility:** Supports raw SQL alongside ORM-driven operations for performance-critical workflows.
- **Extensibility:** Modular design allows for future additions like mobile apps and real-time flight updates.

---

## Core Technology Decisions

### Framework and Language
JetFolio uses C# and .NET Core for both client and server, ensuring consistency and leveraging team expertise.

### Data Access Strategy
Entity Framework Core (ORM) was adopted for its balance between productivity and performance in managing SQL interactions.

### Deployment Platform
Azure Container Apps was chosen for hosting the Web API, offering serverless scaling, event-driven capabilities, and low management overhead.

---

## Key Features and Benefits

- **Detailed Flight Logging:** Track each flight with relevant metrics (departure/arrival, aircraft type, service class, loyalty points).
- **Expense Tracking:** Monitor costs, upgrades, and loyalty point valuations.
- **Loyalty Program Insights:** Forecast earned points/MQDs for upcoming flights to hit elite status thresholds.
- **Travel Analytics:** Generate reports for miles flown, costs per mile, and trends over time.

---

## Scalability and Future Enhancements

JetFolio is built to evolve:
- **Multi-User Support:** Transitioning from single-user to multi-user scenarios with API-based access control.
- **Expanded Modules:** Adding tracking for hotels, car rentals, and ancillary travel costs.
- **Integration with External APIs:** Potentially pulling real-time flight status or importing flight data from email confirmations.

---

## Conclusion

The JetFolio Flight Plan is the foundational guide to building a robust, scalable travel tracking application. It focuses on delivering immediate functionality while maintaining a forward-looking approach to extensibility and innovation. As JetFolio grows, its architecture will adapt to meet new demands, ensuring both usability and technological excellence.

---