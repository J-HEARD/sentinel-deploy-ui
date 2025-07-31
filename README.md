# 🛡️ Sentinel Deploy UI

This repository contains the infrastructure templates used to deploy a baseline Microsoft Sentinel environment into an Azure tenant. It is intended to be launched using the **Deploy to Azure** button below.

---

## 🚀 What This Deploys

This deployment will:

- Create a **Log Analytics Workspace** (`CISO-SENTINEL-WORKSPACE`)
- Enable **Microsoft Sentinel** on that workspace
- Configure **data retention policies**
- Deploy **core Microsoft-native data connectors**
- Create a **User Assigned Managed Identity (UAMI)** (if required)
- Prepare the environment for additional security content

> All names and locations have been aligned to CISO conventions and will deploy into your selected Azure Subscription and Resource Group.

---

## 📌 Usage Requirements

You must have the following permissions to deploy:

- **Contributor** on the target subscription or resource group
- Permission to register resource providers (for first-time workspace deployment)
- Optional: **Security Admin** to connect certain services via data connectors

---

## 📦 Deploy Now

Click the button below to open the deployment interface in the Azure Portal:

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](
https://portal.azure.com/#create/Microsoft.Template/uri/
https%3A%2F%2Fraw.githubusercontent.com%2FJ-HEARD%2Fsentinel-deploy-ui%2Fmain%2Fazuredeploy.json)

---

## 🧱 Repo Contents

| File | Purpose |
|------|---------|
| `azuredeploy.json` | Master template for deployment |
| `createUiDefinition.json` | (Optional) Custom deployment UI |
| `LinkedTemplates/` | Modular templates for workspace, connectors, and settings |

---

## 🔒 Security Note

This repository contains **infrastructure templates only** — no analytics rules, playbooks, or operational content. All dynamic Sentinel content is managed privately via DevOps pipelines.

