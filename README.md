# Lab A11: Remote State Storage with Azure Blob Storage

**Name:** Savas Erturk  
**Course:** CST8918 – Cloud Infrastructure  
**Lab:** A11 – Remote State with Azure Blob Storage  
**Date:** March 22, 2025

---
## 📸 Screenshots

### Screenshot 1 – Azure Portal showing the `dev.terraform.tfstate` file  
![Screenshot 1](./screenshots/screenshot1.png)

### Screenshot 2 – Your Azure profile visible in the upper-right corner  
![Screenshot 2](./screenshots/screenshot2.png)

### Screenshot 3 – Terraform apply output in the terminal  
![Screenshot 3](./screenshots/screenshot3.png)

---

## ✅ Objective

Configure Terraform to use Azure Blob Storage for remote state management, which enables secure and collaborative infrastructure deployment in team environments or CI/CD pipelines.

---

## 📁 Project Structure

```
cst8918-w25-a11/
└── terraform/
    ├── terraform.tf
    ├── main.tf
    ├── a11.tfplan
    └── .terraform/
```

---

## ☁️ Azure Resources Created

- **Resource Group:** `savaserturk-a11-rg`
- **Virtual Network:** `savaserturk-a11-vnet`
- **Subnet:** `savaserturk-a11-test-subnet`

---

## 🏗️ Remote Backend Configuration

Terraform was configured to use Azure Blob Storage for remote state:

- **Resource Group:** `savaserturk-cst8918-tf-backend`
- **Storage Account:** `savaserturktfstorage`
- **Container Name:** `tfstate`
- **Blob Key (State File):** `dev.terraform.tfstate`

```hcl
terraform {
  required_version = "~> 1.5"

  backend "azurerm" {
    resource_group_name  = "savaserturk-cst8918-tf-backend"
    storage_account_name = "savaserturktfstorage"
    container_name       = "tfstate"
    key                  = "dev.terraform.tfstate"
  }

  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "3.96.0"
    }
  }
}
```

---```

---

## ⚙️ Terraform Commands

### Plan
```bash
terraform fmt && terraform validate && terraform plan -out=a11.tfplan
```

### Apply
```bash
terraform apply a11.tfplan
```

**Result:**  
- 3 resources created  
- No errors or warnings  
- State file successfully stored in Azure Blob Storage

---

## 📸 Screenshots (Add Below)

1. Screenshot of Azure Portal → Storage Account → `tfstate` container → `dev.terraform.tfstate` selected  
2. Screenshot showing your Azure profile in the top-right corner  
3. Screenshot of Terraform apply output (optional or CLI view of success)

---

## 🧹 Clean Up

To destroy all provisioned resources:
```bash
terraform destroy
```

State file (`dev.terraform.tfstate`) remains in storage unless manually removed. It's recommended to keep it for future use.

---

## ✅ Completion Status

- ✅ Remote backend configured and verified  
- ✅ Infrastructure provisioned with Terraform  
- ✅ State file stored securely in Azure  
- ✅ Screenshots captured  
- ✅ Submission ready

---
