---
Titulo: "Azure Devops"
---

# Azure Devops

Pool Agent

Provision deployment groups[https://docs.microsoft.com/en-us/azure/devops/pipelines/release/deployment-groups/?view=azure-devops]

Ventajas de Azure Deployment Groups:



___

Colin's ALM Corner Build Tasks - Tokenizer

https://github.com/colindembovsky/cols-agent-tasks/tree/master/Tasks/Tokenizer


___


Automating infrastructure deployments in the Cloud with Terraform and Azure Pipelines

https://azuredevopslabs.com/labs/vstsextend/terraform/


___


Especificar condiciones en yaml en azure devops

https://docs.microsoft.com/es-es/azure/devops/pipelines/process/conditions?view=azure-devops&tabs=yaml


Condiciones en los stages ejemplo sacado :

<pre>
variables:
  isMain: $[eq(variables['Build.SourceBranch'], 'refs/heads/main')]

stages:
- stage: A
  jobs:
  - job: A1
    steps:
      - script: echo Hello Stage A!

- stage: B
  condition: and(succeeded(), eq(variables.isMain, 'true'))
  jobs:
  - job: B1
    steps:
      - script: echo Hello Stage B!
      - script: echo $(isMain)
<pre>

____



