([go-home](..\README.md)) 

# Terraform Setup instructions 
These steps go over setting up Terraform to deploy resources into your Azure environment. 

## Step 1 - Install Terraform
Terraform is the tool that will create and manage Azure resources using code.

- Signup for a Terrform Account. 
- Then download Terrform from [Terraform Downloads](https://developer.hashicorp.com/terraform/install)
    - For Windows, choose: 'AMD64'
- Extract the ZIP to a folder (e.g., C:\terraform)
- Press: 'Win + R' → type 'sysdm.cpl' → press Enter
- Go to: 'Advanced' tab → click 'Environment Variables'.
- Under System Variables: Find 'Path' → select it → click 'Edit'.
- Click 'New' → paste the folder path where you extracted Terraform (e.g., C:\terraform)
- Click 'OK' to save.
- Verify: Open PowerShell or Command Prompt:

```
terraform -v
```

**Note**: If you have VSC open you may have to close the entire VSC tehn reopen a new terminal after updating a new 'PATH' variable.

## Step 2 - Install Azure CLI
Azure CLI lets you log in to Azure and create credentials (Service Principal) for Terraform. It’s also useful for quick checks and troubleshooting.

- Download Instructions [Install the Azure CLI on Windows](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest&pivots=winget)

Else continue with install from PowerShell: 
```
winget install --exact --id Microsoft.AzureCLI
```
**Screenshot of Azure CLI install**
![Screenshot of Azure CLI install](..\etc\images\setup\terraform-screenshot.png "Screenshot of Azure CLI install")

**Note**: If you notice it taking longer, look for a Windows Admin Prompt. It might flash on your taskbar but not interupt your current screen activities. The install won't conitnue without approving it.

## Step 3 - Log in to Azure

## Step 4 - Create a Service Principal

## Step 5 - Configure Terraform Provider

## Step 6 - Initialize Terraform

## Step 7 - Deploy Your First Resource

---


