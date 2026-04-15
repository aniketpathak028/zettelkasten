---
title: az storage using tf
draft: false
tags:
  - terraform
  - azure
  - azure-storage
date: 2026-04-15
description: how to create an azure storage account using terraform!
---
# creating an azure storage account using terraform

notes: https://github.com/piyushsachdeva/Terraform-Full-Course-Azure/tree/main/lessons/day03

- a terraform file looks somewhat like this:

```js
// terraform block
terraform {
  // add all the providers - azure, aws, gcp etc.
  required_providers {
    azurerm = {
	    // official hashicorp supported provider azurerm
        source = "hashicorp/azurerm"
        version = "~> 4.8.0"
    }
  }
  // terraform core version
  required_version = ">=1.9.0"
}

// provider block
provider "azurerm" {
    features {
     
    }
}

// resource block - azure resource group
resource "azurerm_resource_group" "tf_resource_group" {
  name     = "tf-resource"
  location = "West Europe"
}

resource "azurerm_storage_account" "tf_storage_account" {
  name                     = "tf-storage"
  resource_group_name      = azurerm_resource_group.tf_resource_group.name
  location                 = azurerm_resource_group.tf_resource_group.location // implicit dependency
  account_tier             = "Standard"
  account_replication_type = "GRS"

  tags = {
    environment = "staging"
  }
}
```

- now to authenticate with azure we can use the command:
```shell
az login
```

- but we don't want to create the resources using our personal account, instead follow the standard practice of creating it using a service principle

```shell

```


## Links:

202604150009
