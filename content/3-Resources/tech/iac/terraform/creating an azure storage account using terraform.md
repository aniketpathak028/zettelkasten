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

- but we don't want to create the resources using our personal account, instead follow the standard practice of creating it using a service principle which can be created using the command below:
```shell
az ad sp create-for-rbac -n az-demo --role="Contributor" --scopes="/subscriptions/$SUBSCRIPTION_ID"
```

- to know your subscription id use command:
```shell
az account show
```

- once you have created the service principle account, we recieve some info which is needed to authenticate with azure which creating/destroying resourcesand can be exported as below. These values would be generated as a part of the service principle account creation!
```shell
export ARM_CLIENT_ID=""
export ARM_CLIENT_SECRET=""
export ARM_SUBSCRIPTION_ID=""
export ARM_TENANT_ID=""
```

- then simply run `terraform init` to initialize terraform and create a lock file and a provider file which is a binary to convert terraform code into code that can make cloud api calls based on your OS!
```shell
terraform init # generates lock file, and binary for the provider based on OS
terraform plan # validates the resources and checks stuff like syntax mistakes and also shows a highlight of the changes to be made!
terraform apply # applies the changes into the infra
terraform destroy
```

> Note: some changes ex - changing the account replication type from GRS to LRS doesn't need the resources to be deleted and re-created while some might need the resources to be re-created!

> Tip: use command `terraform apply --auto-approve` to skip approval step!

~aniket
## Links:

202604150009
