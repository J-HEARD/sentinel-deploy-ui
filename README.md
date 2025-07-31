# 🛡️ Sentinel Deploy 🛡️

This repository contains the infrastructure templates used to deploy a baseline Microsoft Sentinel environment into an Azure tenant. It is intended to be launched using the Deploy to Azure button below or integrated into an Azure DevOps pipeline.

---

## What This Deploys

This deployment will:

- Create a Log Analytics Workspace (`CISO-WS-SENTINEL`)
- Enable Microsoft Sentinel on that workspace
- Configure workspace retention and daily quota settings
- Deploy a core set of Microsoft-native data connectors
- Provision a User Assigned Managed Identity (UAMI) if required
- Prepare the environment for automated Sentinel content deployment via DevOps

All names and locations follow a "CISO"-aligned naming convention and will deploy into your selected Azure Subscription and Resource Group.

---

## Included Data Connectors

The following Microsoft-native connectors are deployed:

- Azure Activity
- Microsoft 365 (formerly Office 365)
- Microsoft Defender for Identity
- Microsoft Entra ID Protection
- Microsoft Defender for Cloud (Legacy - subscription-based)
- Microsoft Defender XDR 

> **Note:** This deployment does **not** configure individual data types for each connector.  
> That task is handled during the **DevOps phase**, which ensures proper streaming and validation for all connectors, including Defender XDR.

---

## Usage Requirements

You must have the following permissions to deploy:

- Contributor on the target subscription or resource group
- Permission to register resource providers (required for first-time workspace deployment)
- Optional: Security Admin to connect certain services manually (e.g., Defender XDR)

---

## Deployment

Click the button below to open the deployment interface in the Azure Portal:

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FJ-HEARD%2Fsentinel-deploy-ui%2Fmain%2Fazuredeploy.json)

---

## Repo Contents

| File/Folder               | Purpose                                                         |
|---------------------------|-----------------------------------------------------------------|
| `azuredeploy.json`        | Master template for infrastructure deployment                   |
| `createUiDefinition.json` | (Optional) Custom deployment interface for Azure Portal         |
| `LinkedTemplates/`        | Modular templates for workspace, connectors, identity, and settings |

---

## Security Note

This repository focuses strictly on deploying static infrastructure — it does not include any analytics rules, automation, playbooks, or hunting queries.  
All operational Sentinel content is managed separately via DevOps pipelines.

---

