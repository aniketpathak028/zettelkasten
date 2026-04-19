---
title: terraform variables
draft: false
tags:
  - terraform
  - terraform-variables
date: 2026-04-19
description: what are the different tf variables?
---
# terraform variables

### types:
- input - as input to the terraform config
- output - get as return from the terraform command
- local - internal variables

### there are many ways to define and pass a variable in terraform and each method has a different priority

1. hardcode inside the `main.tf` file by defining it inside
```js
// define the variable
variable "environment" {
  type = string
  description = "the env type"
  default = "staging"
}


// create a resource group
resource "azurerm_resource_group" "tf_resource_group" {
  name     = "tf-resources"
  location = "West Europe"
}

// create a storage account in the resource group
resource "azurerm_storage_account" "tf_storage_account" {
  name                     = "uxotout7"
  resource_group_name      = azurerm_resource_group.tf_resource_group.name
  location                 = azurerm_resource_group.tf_resource_group.location # implicit dependency
  account_tier             = "Standard"
  account_replication_type = "LRS"

  tags = {
    environment = var.environment // access the variable using the dot operator
  }
}
```

2. pass as argument in the cli (has the highest priority)
```bash
terraform plan -var=environment=dev
```

3. create the variables in a file `terraform.tfvars` and run `tf plan`
```js
environment = "demo"
```

> Note: terraform variable precedence - https://developer.hashicorp.com/terraform/enterprise/variables

4. environment variables

we can also set env variables but it should be of the format TF_VAR_name
```shell
export TF_VAR_region=us-west-1
export TF_VAR_ami=ami-049d8641
export TF_VAR_alist='[1,2,3]'
export TF_VAR_amap='{ foo = "bar", baz = "qux" }'
```

5. output variable

we can also print an output variable using terraform, we just need to define the output in the `main.tf` file

```js
// create a storage account in the resource group
resource "azurerm_storage_account" "tf_storage_account" {
  name                     = "uxotout7"
  resource_group_name      = azurerm_resource_group.tf_resource_group.name
  location                 = azurerm_resource_group.tf_resource_group.location # implicit dependency
  account_tier             = "Standard"
  account_replication_type = "LRS"

  tags = {
    environment = var.environment
  }
}

output "storage_account_name" {
  value = azurerm_storage_account.tf_storage_account.name
}
```

once the output is defined just run:
```shell
terraform refresh
terraform plan
terraform output
```

> the output variable can be used to pass important Information about the infra once it is created!

6. local variable
- used when these variables are not changed very often

```js
locals{
  common_tags= {
    environment = "dev"
    lob = "abc"
    stage= "123"
  }
}

// create a storage account in the resource group
resource "azurerm_storage_account" "tf_storage_account" {
  name                     = "uxotout7"
  resource_group_name      = azurerm_resource_group.tf_resource_group.name
  location                 = azurerm_resource_group.tf_resource_group.location # implicit dependency
  account_tier             = "Standard"
  account_replication_type = "LRS"

  tags = {
    environment = local.common_tags.stage
  }
}
```

~aniket
## Links:

202604191322
