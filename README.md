### Intro
Let’s consider the following three containerized web applications:

![Three containerized web application](/images/app-scenario.jpg "app")

- App1 needs to communicate to App2 and App3
- How would we set this up in ECS?

### ECS Implementation Overview
- Create task definition for each application
- Create Service (i.e. long running tasks) - 1 replica
- How do we get the service to communicate with each other?
  - Service Discovery
  - Internal Load Balancers
  - Service Connect
- To save cost and complexity, service discovery is a good option

Service Discovery overview and show diagram:

![Three containerized web application in ECS with Service Discovery](/images/app-ecs.jpg "app-ecs")

- Create Service with Service discovery

### AppMesh Implementation
- Requirement is now to use AppMesh because the application here needs to be able to communicate with applications hosted in EKS.
- How can this be achieved?
  - Create Mesh
  - Create Virtual Nodes (logical pointer to the actual ECS service/K8 Deployment)
  - Create Virtual Router?
  - Create Virtual Service (abstraction of the real service)

![Three containerized web application with App Mesh and ECS](/images/app-appmesh.jpg "app-appmesh")


- How can this service be exposed outside of the Mesh? (Virtual Gateway)
  - Typically fronted by NLB, however ALB also possible

![Containerized web application access using virtual gateway ](/images/app-appmesh-vgw.jpg "app-appmesh-vgw")
