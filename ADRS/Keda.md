Architecture Design Record (ADR): Onboarding KEDA and Horizontal Pod Autoscaling (HPA) to Azure Kubernetes Service (AKS)
Context
The need to scale workloads dynamically in response to fluctuating demands is becoming more critical for our services running in Azure Kubernetes Service (AKS). With the increasing volume of data processing, high transaction throughput, and large queues in services like Azure Service Bus, the ability to adjust compute resources efficiently is essential. This would provide better performance, cost management, and avoid manual intervention in scaling.

At present, the existing system in AKS relies on static scaling configurations, primarily dependent on predefined limits. However, this approach has limitations in responding to dynamic workloads driven by event-driven triggers or fluctuating CPU and memory requirements. For example, high load on message queues or sudden database load cannot trigger scaling automatically with the current architecture, leading to performance bottlenecks.

To address this, KEDA (Kubernetes Event-driven Autoscaling) and Horizontal Pod Autoscaling (HPA) need to be integrated into the existing AKS environment. KEDA would provide event-based autoscaling capabilities, while HPA would improve the responsiveness of the system by scaling services based on resource metrics like CPU and memory.

However, the integration of KEDA and HPA needs careful planning and execution. The security of the system must be ensured to protect sensitive data, and the changes must be validated to ensure minimal disruption to the existing services. The integration will also require updates to Helm charts, Terraform configurations, and monitoring systems.

Decision
We will integrate KEDA and HPA into our AKS environment to enable dynamic scaling for both event-driven workloads and resource-driven workloads. This decision aims to achieve the following:

Event-Driven Scaling with KEDA: We will install and configure KEDA to enable autoscaling based on external event sources such as Azure Service Bus or database load, helping us manage unpredictable workload spikes effectively.

Resource-Based Scaling with HPA: We will update the Helm charts and Kubernetes configurations to enable Horizontal Pod Autoscaling (HPA), ensuring that workloads are automatically scaled up or down based on CPU and memory utilization.

Seamless Integration with Existing AKS Setup: The integration of KEDA and HPA will be carried out without interrupting existing workloads, with careful testing and validation in non-production environments before full deployment.

Security Considerations: We will adhere to best practices for security, including managed identities, Role-Based Access Control (RBAC), and Azure Active Directory (AAD) integration, ensuring that only authorized services trigger scaling and that sensitive data remains protected during scaling operations.

Automation and Monitoring: We will integrate CI/CD pipelines to automate the deployment of configurations, alongside monitoring tools like Azure Monitor and Prometheus, to ensure scaling actions are appropriately tracked and managed.

Consequences
Positive Consequences:
Improved Scalability and Performance:
With the integration of KEDA and HPA, our AKS clusters will automatically scale in response to varying loads. This dynamic scaling will enable services to perform efficiently under both high and low load conditions, improving overall system responsiveness and availability.

Cost Efficiency:
By using dynamic autoscaling, we will only utilize the resources required for the workloads, reducing unnecessary resource allocation and providing significant cost savings during low-demand periods.

Operational Efficiency:
With KEDA handling event-driven scaling and HPA managing resource scaling, the operations team will no longer need to manually intervene in scaling decisions, improving efficiency and reducing human error.

Enhanced Developer Enablement:
Developers will benefit from simplified configurations, with the new autoscaling mechanisms abstracting away the complexities of manual scaling. This will streamline the process for deploying new applications and scaling existing ones.

Better Resource Management:
The combination of event-driven and resource-based scaling allows for more granular control over resource consumption, ensuring that our infrastructure can handle unexpected events such as spikes in message queue lengths or sudden increases in database load.

Negative Consequences:
Complexity in Configuration:
The integration of KEDA and HPA requires careful updates to the existing infrastructure, including changes to Helm charts, Terraform configurations, and Kubernetes resource definitions. These changes must be thoroughly tested to avoid potential disruptions in production services.

Learning Curve:
Developers and operations teams may need time to familiarise themselves with KEDA and HPA, especially since these technologies bring new concepts (like event-driven scaling) that are not yet part of our standard operations.

Increased Resource Consumption during Scaling:
While autoscaling helps manage workload fluctuations, there is a possibility that incorrect configurations (such as improper scaling thresholds) could lead to inefficient scaling, resulting in resource waste or performance degradation.

Potential Security Risks:
Integrating KEDA with external event sources such as Azure Service Bus and databases introduces additional security considerations. The implementation of appropriate IAM policies and RBAC is crucial to mitigate risks related to unauthorized scaling triggers or data exposure.

Dependency on External Services:
Event-driven scaling introduces a dependency on the availability and reliability of external services such as Azure Service Bus. If these services face issues, it could impact the performance of the scaling mechanism.

Next Steps:
Approval of the Design:
We will seek approval from the Architecture Design Review Board (ADRB) to proceed with the KEDA and HPA integration.

Implementation Phases:
The implementation will be carried out in phases, starting with a pilot project in a non-critical environment, followed by broader rollout and integration testing.

Ongoing Monitoring and Adjustment:
Post-deployment, we will closely monitor the scaling performance and adjust configurations as needed based on real-world usage and feedback.

Documentation and Training:
Once the integration is complete, we will update internal documentation to guide teams through the new autoscaling mechanisms. Training sessions will be conducted to ensure teams understand how to configure and monitor KEDA and HPA.