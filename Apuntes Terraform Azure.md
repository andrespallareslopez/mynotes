---
Titulo: "Apuntes Terraform Azure"
---
# Apuntes Terraform Azure

- [Apuntes Terraform Azure](#apuntes-terraform-azure)
    - [Getting Started with Terraform for Azure: Quick Azure Primer](#getting-started-with-terraform-for-azure-quick-azure-primer)
    - [Desplegar infraestructura en Azure con Terraform(Desplegar un App service para desplegar aplicaciones web) (Alberto picazo)](#desplegar-infraestructura-en-azure-con-terraformdesplegar-un-app-service-para-desplegar-aplicaciones-web-alberto-picazo)
    - [Getting Started with Terraform for Azure: Authentication Demo (Otra forma de autenticarnos)](#getting-started-with-terraform-for-azure-authentication-demo-otra-forma-de-autenticarnos)
    - [4 ways to create an SQL Database in Azure](#4-ways-to-create-an-sql-database-in-azure)
    - [Terraforming Azure SQL Database](#terraforming-azure-sql-database)
    - [Building Azure SQL Db with Terraform using Azure DevOps](#building-azure-sql-db-with-terraform-using-azure-devops)
    - [Building SQL Server in Azure with Terraform](#building-sql-server-in-azure-with-terraform)
    - [Terraform in Azure with Azure DevOps](#terraform-in-azure-with-azure-devops)
    - [«Terraformando» nuestra infraestructura desde Azure Pipelines](#terraformando-nuestra-infraestructura-desde-azure-pipelines)
    - [How To Deploy an Azure SQL Database using Terraform](#how-to-deploy-an-azure-sql-database-using-terraform)
    - [Como crear un SQL Server y Base de datos con Azure](#como-crear-un-sql-server-y-base-de-datos-con-azure)
    - [From Zero to WOW! with HashiCorp Nomad](#from-zero-to-wow-with-hashicorp-nomad)
    - [From Zero to WOW! with Nomad](#from-zero-to-wow-with-nomad)



### Getting Started with Terraform for Azure: Quick Azure Primer

https://www.youtube.com/watch?v=CRueD4fU0AI&list=PLD7svyKaquTlE9dErhMazFhWbSSCfMP_4

- Cloud Models
- Azure Core Infrastructure
        Azure Regions
        Resource Groups
- Network
- Virtual Machines (IaaS)
- App and DB Services (PassS)
- Other Services (SaaS)
- Azure Portal

_____________________________________________________
***Estructura de una llamada en Terraform***

Component    Provider      Type         Name
resource    "Azurerm_resource_group"  "miGrupoEnAzure"




___

### Desplegar infraestructura en Azure con Terraform(Desplegar un App service para desplegar aplicaciones web) (Alberto picazo)

https://www.youtube.com/watch?v=EN1CnJIK-n4

para desplegar con terraform antes tenemos que lanzar el comando az login en powershell:

az login


___

### Getting Started with Terraform for Azure: Authentication Demo (Otra forma de autenticarnos)

https://www.youtube.com/watch?v=IHHIXf39Igo&list=PLD7svyKaquTlE9dErhMazFhWbSSCfMP_4&index=8

provider "azurerm" {
    subscription_id="..." //tipo guid
    client_id="..."   //tipo guid
    client_secret="..." //tipo guid
    tenant_id="..."  //tipo guid
}

resource "azurerm_resource_group" "resource_gp" {
    name="demo 1"
    location="eastus"

    tags {
        Owner="andres pallares lopez"
    }


}


Explica como hacer variables en terraform, un fichero aparte.

provider "azurerm" {
    suscription_id = "${var.subscription.id}"
    cliend_id      = "${var.cliend_id}"
    client_secret  = "${var.client_secret}"
    tenant_id      = "${var.tenant_id}" 
}


//declaramos las variables
variable "client_id" {
   descriptcion="..."
}
variable "subscription_id" {
   description="..."
}
variable "client_secret" {
   description="..."
}
variable "tenant_id" {
    description="..."
}
 En un fichero a aparte llamado terraform.tfvars estaria lo siguiente:

subscription_id ="..."
client_id="..."
client_secret="...·
tenenat_id="...."

terraform init

terraform plan

terraform apply

terraform destroy

terraform graph




___

### 4 ways to create an SQL Database in Azure

https://www.youtube.com/watch?v=6e_YPjxFURc

una manera seria con el comanzo az en powershell de crear una base de datos en azure sql

az group create --name "cloud5mins"  --location eastus

az sql server create \
       --name "sqlcloud5minutes" \
       --resource-group "cloud5mins" \
       --location eastus  \
       --admin-user "frank"  \
       --admin-password "p@lehais51"

az sql db create --resource-group "cloud5mins" --server "sqlcloud5minutes"  --name "cloud5db" \

___

### Terraforming Azure SQL Database

https://www.phillipsj.net/posts/terraforming-azure-sql-db/


___

### Building Azure SQL Db with Terraform using Azure DevOps

https://sqldbawithabeard.com/2019/04/20/building-azure-sql-db-with-terraform-using-azure-devops/


___

### Building SQL Server in Azure with Terraform

http://www.winopsdba.com/blog/Building-SQL-server-in-Azure-with-Terraform.html

___

### Terraform in Azure with Azure DevOps

https://ifi.tech/2020/07/23/terraform-in-azure-with-azure-devops/

___

### «Terraformando» nuestra infraestructura desde Azure Pipelines

https://www.fixedbuffer.com/terraform-azure-pipelines/

___

### How To Deploy an Azure SQL Database using Terraform

http://dbainthecloud.com/tag/azure-sql-database/

En este ejemplo se puede lanzar un comando con "local-exec"

resource "azurerm_sql_server" "test2" {
  name                         = "sqldbsrvrtf01"
  resource_group_name          = "${azurerm_resource_group.test2.name}"
  location                     = "North Central US"
  version                      = "12.0"
  administrator_login          = "sqldbadmin"
  administrator_login_password = "chang3Me!"

  provisioner "local-exec" {
    command     = "Set-AzureRmSqlServerAuditing -State Enabled -ResourceGroupName ${azurerm_resource_group.test2.name}  -ServerName 'sqldbsrvrtf01' -StorageAccountName ${azurerm_storage_account.test2sa.name}"
    interpreter = ["PowerShell", "-Command"]
  }
}





___

### Como crear un SQL Server y Base de datos con Azure

https://www.youtube.com/watch?v=QrCa25p4ixE&t=681s



___

### From Zero to WOW! with HashiCorp Nomad


https://www.hashicorp.com/resources/from-zero-to-wow-with-hashicorp-nomad

___

### From Zero to WOW! with Nomad

https://www.youtube.com/watch?v=xl58mjMJjrg&t=2732s





