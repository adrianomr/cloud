# Terraform

Folder to study terraform.

## Intro

Terraform is a solution to create Infrastructure as a Code (IaC). It manages different resources in cloud solutions, and guarantees that your cloud resources are available as described in your code. To do so, terraform works with a state. This is state is a definition of all resources you utilize into your application, and terraforms job is to keep the state consistent with yhe one declared.

Terraform is a provider agnostic solution, which means that your infrastructure can be created into any provider that you want, without the need to change your code. To do so, terraform works with plugins. It has plugins developed to integrate with the main providers suchs as AWS, Azure, GCP, etc.

## Code structure

```
resource "local_file" "example" {
    filename = "example.txt"
    content = var.content

}

variable "content" {
    type = "string"
    default = "Hello world"
}
```

resource -> code block
local -> provider name
file -> provider type
example -> resource name
variable -> declares a variable, the value will be initialized during terraform apply -> can be created also into terraform.tfvars file, by command line, enviroment variables and etc.

Provider documentation can be easily found into terraform registry page. This page contains all providers documentation.

## Executing

terraform init -> initialize providers, and install providers locally. -> installed providers list is saved into .lock

terraform plan -> generates action plan to achieve the disered state and describes the plan.

terraform apply -> shows execution plan and asks to confirm execution, then executes the plan.

## Idempotency

To assure idempotency, terraform creates a terraform.tfstate. If you run execution plan, terraform will only apply changes that are not already applied. Terraform also generates a backup file to allow rollback.

## Outputs

Externalizes a private value.

```
resource "local_file" "example" {
    filename = "example.txt"
    content = var.content

}

variable "content" {
    type = "string"
    default = "Hello world"
}

output "file-id" {
    value = resource.local_file.example.id
}
```

## Datasource

All providers have datasources.

```
resource "local_file" "example" {
    filename = "example.txt"
    content = var.content

}

data "local_file" "example-content"{
    filename = "example.txt"
}

output "data-source-result" {
    value = data.local_file.example-content.content
}

variable "content" {
    type = "string"
    default = "Hello world"
}

output "file-id" {
    value = resource.local_file.example.id
}
```
