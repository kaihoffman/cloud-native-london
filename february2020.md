# February 2020

## Kubernetesdays.london - conference in September 2020 in Westminster

## The Cheesy Analogy of MLflow and Kubeflow, Byron Allen, Servian (Data analytics company)

### Machine Learning Ops - plenty of tools in the landscape, but what is useful?

MLFlow, Kubeflow, Seldom Core
MLFlow - tracking of models, their parameters and associated artifacts
KubeFlow - Collection of Kubernetes projects for the whole process

- ProductionML Value Chain
  - Master Data Management
  - Data Integration Hub
  - DevOps, Monitoring, Support
  - Governance
- ProductionML Activities
  - Collaborate
  - ML Model Design
  - Data Pipe Management
  - Model Management
  - Hosting

But how does the data you gather affect your model?

- You need to manage it in a similar way to CI/CDing your code. Think model Experimentation

## KubeFlow

- Runs locally nicely, but limited integration with other notebooks
- But you can run notebooks within the Kubernetes environment, which can be useful for larger teams
-- As a result, teams running KubeFlow might need more knowledge and skills from the team

## Disaster Recovery in the Cloud, Ines Cheikhrouhou, Agyla

### Specifically focusing on AWS but generic enough

### Move to Cloud Native

- Docker for Microservices
- Change teams to be independent for each Microservice (incl different languages!)
- Helped with Orchestration - decision to go with Amazon ECR (for management simplicity)
- Infrastructure code in Terraform and Ansible, Pipelines in GitLab
- Fargate orchestration for Docker - CloudWatch manages events for Lambda as replacements for scripts
- Switched on-premises wholesale to cloud with move to Route53

Result: Easier to do disaster recovery!!
- Databases are now managed, scalable, available.
- Observability through Cloudwatch -> Splunk

Disaster Recovery - from server failures to power outages to software issues to natural disasters

- Phases to achieve disaster recovery readiness
  - Preparation:
    - You need buy-in from management!
    - After buy-in you need _data_ and planning for it
    - Identify and evaluate risks
    - Determine recovery stratregies
    - DOCUMENT YOUR PLAN
    - RTO / RPO (time you can get running as of, time you can recover in)
  - Restoring backups
    - With AWS, minimal issue
    - Main cost is TIME
    - Pilot Light: Host another database to be a constant replica
      - RTO/RPO are going to both improve
    - Warm standby: Fault tolerant architecture
      - Copy of infrastructure in region with minimal resources
      - Scales horizontally quickly
      - RTO seconds, RPO minutes, but increased costs.
      - Useful only for truly business critical, sensitive-data components, or components that others depend on.
        - You literally need to replicate the whole infra!
        - But if you have true Infrastructure As Code, this is easy, only costly in monetary terms
      - But currently only focused on multiple regions within AWS - not multiple providers.
  - There is a genuine use for avoiding vendor lock-in. Using Kubernetes over AWS own brand, using Terraform over Fargate, etc

Comment from the audience - nothing is perfect, but this is an actual example of disaster recovery planning which is RARE.

## My journey into SRE, Jai Campbell

- "A long road" - moving into the cloud single piece at a time
- Use O'Reilly SRE book, but embrace it with Wikipedia
- Original experience: SRE team of 7 to use 150,000 internal g-suite users
  - managed to automate enough so that two engineers could be away with no issues!
  - Newest member of the team had in fact no technical experience, but he was a good problem solver (and had to learn Go)
    - To pivot and to move around takes determination but is doable!
- Mastery is a lifelong endeavour. It's always two steps further away. George Leonard, "Mastery"
- Yes, it's a dive into the deep end, with dozens and dozens of tools being used daily. Daunting, but exciting!
  - For every tool you can master, there'll be something new behind it
- Chaos engineering: Valuable toolkit!
- Mastering SRE is similar to learning a martial art technique - you're in it for life.
- With the enjoyment comes the stress of on-call
- It's hard work, a little bit of luck, but ultimately something you have to work toward and find your niche in
- Explore your strengths, find what entertains you and specialise.
Create and/or contribute to an OSS project!
