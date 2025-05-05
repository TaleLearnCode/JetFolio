[JetFolio](..\README.md) \ [docs](../README.md) \ [Architecture Decision Records (ADRs)](README.md) \

# Framework and Language – C#/.NET Core for Console and API

- **Id**: 0003
- **Status:** Accepted
- **Date:** 2025-04-28
- **Work Item:** *003-FrameworkLanguageDecision*

## Context and Problem

JetFolio requires a framework and programming language that can support both the Web API backend and the console application frontend. The selected framework and language must enable code sharing, cross-platform functionality, and productive development. Given JetFolio's moderate initial scope, we aim to minimize complexity while delivering a reliable and performant application.

The team's expertise is in C#, making .NET Core a natural consideration. .NET Core provides cross-platform support, allowing the console application to run on any OS. Using the same framework and language for both client and server simplifies development, fosters code reuse (e.g., model classes and validation logic), and ensures a consistent development environment.

## Decision Drivers

- **Team Expertise:** Leverage the team's proficiency in C# and .NET to accelerate development.
- **Cross-Platform Compatibility:** Ensure the console app can run on both Windows and Linux.
- **Code Sharing:** Promote reusability of models, validation logic, and utilities between client and server.
- **Performance and Productivity:** Choose a language and framework that balances speed and developer efficiency.
- **Ecosystem and Libraries:** Utilize a mature ecosystem with robust support for development, libraries, and tools.

## Considered Options

- **C#/.NET Core for Console and API**  
- **Python (Flask API) and Python Script for Console**  
- **Node.js for API and a separate client solution**  

## Decision Outcome

**Chosen option:** **C#/.NET Core for Console and API**, because it provides a homogeneous stack, excellent cross-platform support, and leverages the team's existing expertise. The ecosystem's maturity and libraries, combined with .NET Core's performance, make it an ideal choice for JetFolio’s requirements.

### Consequences

- **Good:**  
  - Simplifies development by using a single language and framework for both backend and frontend.  
  - Cross-platform compatibility ensures flexibility for the console app deployment.  
  - Efficient libraries (e.g., for date handling and API design) enhance productivity.  

- **Bad:**  
  - Dependency on a single stack may limit flexibility for future components in different environments.  
  - Requires all developers to be proficient in C#.  

### Implementation

1. Develop the Web API backend using ASP.NET Core, leveraging its support for RESTful API design.  
2. Build the console application using .NET Core with libraries like Spectre.Console for enhanced terminal UI.  
3. Share common code, such as model classes and validation logic, between the client and server.  
4. Use modern C# features to improve code quality and maintainability.  
5. Ensure the project is set up for cross-platform compatibility from the start.  

### Confirmation

The decision will be confirmed by successfully running integration tests between the console application and the Web API on both Windows and Linux environments. Additionally, developer feedback on productivity and ecosystem support will validate the choice.

## Pros and Cons of the Options

### C#/.NET Core for Console and API

- **Good:**  
  - Single stack for client and server simplifies development and maintenance.  
  - Strong cross-platform support ensures wide compatibility.  
  - Mature ecosystem offers productivity-enhancing libraries and tools.  
  - Excellent performance characteristics for both client and backend operations.  

- **Bad:**  
  - Dependence on a single language limits flexibility for future use of other stacks.  
  - Requires developers to stay proficient in C# and .NET.

### Python (Flask API) and Python Script for Console

- **Good:**  
  - Lightweight and easy to use, with many libraries for rapid prototyping.  
  - Simple syntax and broad developer familiarity.  

- **Bad:**  
  - Less suited for high-performance applications compared to .NET Core.  
  - Python does not natively support strongly typed models, which may lead to runtime issues.  
  - No native compatibility or code-sharing between a console script and a Flask-based API.  

### Node.js for API and a Separate Client Solution

- **Good:**  
  - Excellent for asynchronous operations in the API.  
  - Large ecosystem of libraries and tools.  

- **Bad:**  
  - Requires separate solutions for the console application (e.g., a script or UI framework).  
  - JavaScript/TypeScript runtime is less performant for certain backend tasks compared to .NET Core.  
  - Increased complexity with different languages for client and server.  

## More Information

C#/.NET Core was chosen for its combination of performance, cross-platform capabilities, and developer productivity. ASP.NET Core provides robust tools for building APIs, and the language’s strong typing ensures fewer runtime issues. Modern C# features, such as pattern matching and async/await, further contribute to developer efficiency.

No more additional information available.

## Follow-On Information

This ADR will be revisited if future requirements arise for integrating JetFolio with systems built in other languages or if significant limitations are encountered with C#/.NET Core.

## Record History

* **Proposed:** 2025-04-20  
* **Accepted:** 2025-04-28  
* **Last Reviewed:** 2025-04-28  