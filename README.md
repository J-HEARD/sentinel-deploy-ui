# Microsoft Sentinel Core Deployment

This repository contains ARM templates for deploying the core infrastructure components of Microsoft Sentinel.

## What This Deploys

This deployment focuses on the essential foundation for Microsoft Sentinel:

1. **Resource Group** - Creates a new resource group for all Sentinel resources
2. **Log Analytics Workspace** - Sets up the workspace with configurable retention and pricing
3. **Microsoft Sentinel** - Enables Sentinel on the workspace
4. **Data Connectors** - Configures selected data connectors (optional)
5. **UEBA Settings** - Configures User Entity Behavior Analytics (optional)

## What This Does NOT Deploy

This repository intentionally excludes content that will be managed separately:
- Analytics Rules
- Hunting Queries
- Workbooks
- Playbooks/Logic Apps
- Watchlists
- Solutions from Content Hub
- Custom parsers
- Automation rules

These items should be managed in a separate repository for better content lifecycle management.

## Available Data Connectors

The following data connectors can be enabled during deployment:
- Azure Active Directory (includes Identity Protection alerts, with configurable log types)
- Azure Activity (subscription-level activity logs)
- Office 365 (Exchange, SharePoint, Teams)
- Microsoft Defender for Cloud
- Microsoft 365 Defender
- Dynamics 365
- Microsoft Defender for IoT
- Office 365 Project
- Office IRM
- Power BI
- Threat Intelligence

## Deployment Options

### Deploy via Azure Portal

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FJ-HEARD%2Fsentinel-deploy-ui%2Fmain%2Fazuredeploy.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FJ-HEARD%2Fsentinel-deploy-ui%2Fmain%2FcreateUiDefinition.json)

### Deploy via Azure CLI

```bash
az deployment sub create \
  --location <location> \
  --template-uri https://raw.githubusercontent.com/J-HEARD/sentinel-deploy-ui/main/azuredeploy.json \
  --parameters rgName=<resourceGroupName> workspaceName=<workspaceName>
```

### Deploy via PowerShell

```powershell
New-AzSubscriptionDeployment `
  -Location <location> `
  -TemplateUri "https://raw.githubusercontent.com/J-HEARD/sentinel-deploy-ui/main/azuredeploy.json" `
  -rgName <resourceGroupName> `
  -workspaceName <workspaceName>
```

## Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| rgName | Resource group name | CISO-RG-SENTINEL |
| workspaceName | Log Analytics workspace name | CISO-WS-SENTINEL |
| location | Azure region for deployment | Deployment location |
| pricingTier | Workspace pricing tier | PerGB2018 |
| capacityReservation | Daily commitment (GB) for CapacityReservation tier | 100 |
| dailyQuota | Daily ingestion limit in GB (0 = unlimited) | 0 |
| dataRetention | Data retention in days (7-730) | 90 |
| enableUeba | Enable User Entity Behavior Analytics | true |
| enableDataConnectors | Array of data connectors to enable | [] |
| aadStreams | Azure AD log types to collect | [] |

## Architecture

```
Subscription
└── Resource Group (rgName)
    └── Log Analytics Workspace (workspaceName)
        ├── Microsoft Sentinel (enabled)
        ├── UEBA (optional)
        └── Data Connectors (optional)
```

## Post-Deployment

After the core infrastructure is deployed:

1. **Verify Deployment**: Check that the workspace and Sentinel are properly configured
2. **Configure Additional Connectors**: Enable any additional data connectors through the Sentinel portal
3. **Deploy Content**: Use a separate repository/pipeline to deploy:
   - Analytics rules
   - Hunting queries
   - Workbooks
   - Playbooks
   - Other Sentinel content

## Support

For issues or questions, please open an issue in the repository.