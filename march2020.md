# Cloud Native March 2020

## Cloud State of Play, Richard Simon, World Wide Technology

Word Wide Tech have an Advanced Tech Centre (ATC) data centre that users can view and learn from. https://atc.com allows you to play with it yourself!

### Introduction

Focus is on cloud migration strategies, optimising their approach, rather than a deep technical outlook.

### Journey to the Cloud

Digital distruption is forcing a multicloud architecture - public cloud vs multicloud
You shouldn't "move to the cloud" just for the sake of it! (Dilbert cartoon on Kubernetes)

"Heritage DataCentre" - Traditional IT and "transitional" IT -> monolithic
Transitional = knee-jerk reaction, e.g. HCI, OpenStack, Software Defined Infrastructure, SD(everything) Converged Infra -> i.e. a convergence.

Developed into a hybrid cloud - specific workloads into a cloud environment.

SAP and Oracle tend to remain in the data centre (or go into an MSP environment) - hard to just "move".

Movement to microservices, CI/CD pipelines, faster development, automation and automation of config management

WHat about security? -> DevSecOps is a focus now.

The "goal" is "serverless" and infrastructure as code - get spot instances and only pay for what you actively use.

  - "World engines" - describe the world that you want and a machine creates the environment.

### Migration Strategies

- Migration into cloud native does NOT save money.
  - Instead, it increases business agility/flexibility
  - Broader geographic distribution

- "The 6 Rs" - Retiring, rehosting, refactoring, Repurchasing, Replatforming (putting it on a different platform host), Rewriting
  - As your application moves to the cloud, you have to move data to the cloud too, whether cost-effective cloud database or new tech that allows you to apply into existing data for insights.
  - Backup recovery / replication as solutions you need to consider for cloud too

### Cloud Native Architecture

You need to consider the architecture as a whole. It's not just infrastructure modernisation, it's a wider strategy, an architecture (multicloud, public cloud) question, with observability and security baked in.

### Cloud Operating Model

The two most important parts to get right:

- Connectivity - from static IP host-based to dynamic IP and service-based
- Security - from High trust account-based to low/zero trust identity-based. Two pods sitting next to each other should not trust each other.
- From dedicated hardware to capacity on demand in provisioning

### Conclusions

- Journey to the cloud: Have a cloud strategy! You need to actually write a document to plan the process out. A "Cloud Charter" that everyone signs up to and supports.
  - Look at options/choices between hybrid/public/multicloud - what is the best option for your immediate needs? What about into the future?
  - Computing unit size: needs to be well-defined for each work load considered. Dedicated container or can you run it as a serverless function?

- Migration into the cloud: Plan your journey, plan your automation, plan your optimisation. You need to find a way to automate the migration for all your applications.
  - Optimise your expenditure, see if partial moves to the cloud can offer you a saving.

Cloud Native Architecture:
Design for a cloud native operating model!

- Don't just copy and paste your security policies from your on-premises/Data Centre model!
- Look at the way to migrate all parts of your application - entire database etc! Is it still worth it monetarily?

Other considerations: Security? Observability? Data management, infrastructure security

## Build and test GCP Infrastructure Using Terraform Module, Pradeep Bahadani, Cloud Native Technologies (founder)

### Terraform

- Open-source tool to build infrastructure as declarative code.
- Lifecycle: 4 stages
  - `Terraform init` to initialise repository and modules
  - `terraform plan` to execution plan
  - `terraform apply` to actually execute this with the cloud API to create resources.
  - `terraform destroy` to get rid of resources

- On GCP, the complexity of the platform (storage, service ccount, Web Server, Subnets, etc) means that multiple instances are a pain to create the same way.
  - You can create the code, but it's environment-specific for each project. Leads into code duplication and possible security / divergence issues.
  - Solution: Terraform Modules

### Terraform Modules

- Modules: Abstract your logic into a function and call the function with arguments you provide (e.g. environment specifics)
  - Re-usable: Helps avoid code duplication.
  - Collaborative development - resides in a single repository
  - Helps you to get started quickly with different platforms - c.f. Docker registry!
- Passing variables to terraform module, calling different values in different blocks, and the function gets executed each time for each block.

### Testing

- Frameworks: Open source test frameworks e.g. Test Kitchen - Ruby files defining tests
  - Lifecycle - `create`, `converge`, `verify`, `destroy`.

## Kubernetes Lifecycle Management With Cluster API, Nadir Jeewa, VMware

### Why ClusterAPI exists
What is a Kubernetes Cluster?

- Infrastructure
  - Networking
  - Firewall Rules
  - Provider specific services
  - Load Balancer
- Minimum: Container runtime, kubeletc, etcd, kube-apiserver, kube-scheduler, kube-controller-manager, kube-proxy, CNI provider, CoreDNS
- "Kubernetes is not a container orchestrator. It is a web server that lets you write values and have them reflected back, and part of the service is a component that runs orchestration"
- Bootstrapping the components?
  - One of the options: Kubeadm (cf. Docker Swarm, i.e. simplicity)
    - Owned by Kubernetes SIG Lifecycle, helps create a new control plane node, then you can join other nodes.
    - Building block for higher-level systems.
    - Does NOT handle infrastructure (images, firewalls, etc above). All it does is get kubelet and etcd running.
  - Puppet / Chef / Terraform / etc - declaratively write configurations for your whole pre-planned components.
    - Important to think about the strategy in advance to make things work.
  - ClusterAPI: Part of "Kubernetes in Layers" (cf. "Turtles all the way down")
    - Declarative Li
    Lifecycle Management of Kubernetes Clusters


### Demo

[Lots of Yaml]

### How ClusterAPI works

- You need a Kubernetes cluster to start off with! E.g. KIND
  - It needs to run Cluster API and controllers for your providers
- v1Alpha3 - abstracts out clusters, machines, machinesSets, machineDeployments, MachineTemplates as cluster components

In Kubernetes - everything is a controller (comes from robotics theory). Constantly check the state of the world and then make changes to try to reconcile the world to make them more your intention. It's an infinite loop to keep the state correct or try and MAKE the state correct.
  - Each controller only controls its own context. E.g. machine set will notice that YAML now has 3 machines declared. This will then try and create a new machine - which then passes the request to e.g. AWS controller to actually implement.

[Look up Cluster API v1Alpha3 architecture. It's pretty neat. They are also making `clusterctl` to allow you to manage these.]

### Some of the Challenges

- To work with AWS, you have to understand how AWS works internally! It's quite opaque.

[Time ran out, sadly]