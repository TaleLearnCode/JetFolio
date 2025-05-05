[JetFolio](..\README.md) \ [docs](../README.md) \ [Architecture Decision Records (ADRs)](README.md) \

# Deployment Platform – Azure Container Apps vs. Azure App Service or AKS

- **Id**: 0002
- **Status:** Accepted
- **Date:** 2025-04-28
- **Work Item:** *002-DeploymentPlatformDecision*

## Context and Problem

JetFolio requires a deployment platform to host the Web API. The platform must support containerized applications while offering simplicity, scalability, and minimal operational overhead. The goal is to focus on application development without the need to manage underlying infrastructure such as virtual machines or a full Kubernetes cluster.

Several options were evaluated, including Azure Container Apps, Azure App Service, and Azure Kubernetes Service (AKS). Each provides varying levels of control, scalability, and complexity. The challenge was to choose a platform that aligns with JetFolio's current scale and future potential.

## Decision Drivers

- **Ease of Management:** Minimize infrastructure management and operational complexity.
- **Scalability:** Ensure the ability to scale seamlessly with future growth and traffic demands.
- **Event-Driven Capabilities:** Allow integration with event-driven architectures for potential queue or background processing.
- **Familiarity and Learning Opportunity:** Leverage the team's ability to work with Azure services while gaining experience with newer technologies.
- **Cost Efficiency:** Reduce operational costs while ensuring necessary functionality and reliability.

## Considered Options

- **Azure Container Apps**  
- **Azure App Service (Web App)**  
- **Azure Kubernetes Service (AKS)**  

## Decision Outcome

**Chosen option:** **Azure Container Apps**, because it provides serverless scalability, integrated features like KEDA (Kubernetes-based Event-Driven Autoscaling), and Dapr support, with minimal management overhead. The platform is well-suited to JetFolio’s current needs and provides flexibility for future expansions.

### Consequences

- **Good:**  
  - Serverless scaling allows efficient resource usage, scaling out based on traffic.  
  - Simplifies deployment and management by abstracting away VM and Kubernetes complexities.  
  - Built-in support for event-driven scaling aligns with potential future needs (e.g., queue processing).  
  - Provides a learning opportunity to work with a modern Azure platform.  

- **Bad:**  
  - Container Apps is a newer service and still evolving, which could lead to limited documentation or feature gaps.  
  - Limited control compared to AKS may pose challenges if highly customized configurations are needed in the future.  

### Implementation

1. Containerize the Web API using Docker and push the image to Azure Container Registry.  
2. Deploy the container to Azure Container Apps with proper configuration for scaling, ingress, and secrets management.  
3. Configure Azure Monitor for logging and performance metrics to monitor the deployment.  
4. Test autoscaling rules and integration with other Azure services (e.g., Azure SQL).  
5. Prepare to re-evaluate the platform if scaling needs or requirements change substantially.  

### Confirmation

The implementation will be confirmed through end-to-end testing in the deployment environment, including integration with the Azure SQL database and handling simulated traffic to test scalability. Application performance and reliability metrics will validate the platform's suitability.

## Pros and Cons of the Options

### Azure Container Apps

- **Good:**  
  - Serverless and fully managed, reducing operational overhead.  
  - Scales automatically based on traffic or other triggers (event-driven with KEDA).  
  - Supports modern architectures with Dapr integration.  
  - Flexible configuration with minimal complexity compared to AKS.  

- **Bad:**  
  - Limited control compared to AKS for custom configurations.  
  - Newer platform with fewer community resources and documentation.

### Azure App Service

- **Good:**  
  - Proven and widely used platform with rich features for hosting applications.  
  - Supports both containerized apps and code-based deployments.  
  - Less operational overhead than AKS.  

- **Bad:**  
  - Lacks event-driven scaling compared to Container Apps with KEDA.  
  - Limited flexibility for containerized architectures compared to AKS or Container Apps.  

### Azure Kubernetes Service (AKS)

- **Good:**  
  - Full control over the Kubernetes cluster for custom configurations.  
  - Supports complex architectures and high scalability.  

- **Bad:**  
  - Higher operational overhead, requiring Kubernetes management expertise.  
  - More expensive to maintain compared to Container Apps or App Service.

## More Information

Azure Container Apps is a relatively new service, and while it has some limitations compared to established platforms like Azure App Service or AKS, its serverless nature makes it ideal for JetFolio’s use case. It allows efficient scaling without the burden of managing infrastructure. Future platform evaluations may include a review of Azure Container Apps’ feature maturity to ensure it continues meeting JetFolio’s needs.

## Follow-On Information

This ADR will be revisited if JetFolio’s deployment needs outgrow the capabilities of Azure Container Apps. Possible triggers for re-evaluation include the need for highly customized infrastructure, increased traffic beyond the scaling capabilities of Container Apps, or new Azure services offering better alignment with JetFolio’s goals.

## Record History

* **Proposed:** 2025-04-20  
* **Accepted:** 2025-04-28  
* **Last Reviewed:** 2025-04-28  