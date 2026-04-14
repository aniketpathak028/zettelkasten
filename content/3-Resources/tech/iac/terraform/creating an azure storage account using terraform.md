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

```tf
terraform {
  required_providers {
    azurerm = {
        source = "hashicorp/azurerm"
        version = "~> 4.8.0"
    }
  }
  required_version = ">=1.9.0"
}

provider "azurerm" {
    features {
      
    }
  
}

resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "West Europe"
}

resource "azurerm_storage_account" "example" {
 
  name                     = "techtutorial101"
  resource_group_name      = azurerm_resource_group.example.name
  location                 = azurerm_resource_group.example.location # implicit dependency
  account_tier             = "Standard"
  account_replication_type = "LRS"

  tags = {
    environment = "staging"
  }
}
```





## Links:

202604150009
