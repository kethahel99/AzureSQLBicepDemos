# Code Sample for Tao Yang's blog

[Managing Cloud and Datacenter by Tao Yang](https://blog.tyang.org/)

## What Does This Repository Do?

This repository contains a collection of Azure Infrastructure-as-Code (Bicep) templates, PowerShell scripts, and System Center Operations Manager (SCOM) management packs authored by Tao Yang. The samples cover common Azure management scenarios including SQL Server VM deployments, Azure Policy governance, role-based access control, networking, monitoring, and hybrid cloud management.

---

## Repository Structure

```
AzureSQLBicepDemos/
├── Azure/              # Standalone PowerShell scripts for Azure resources
├── Azure-Bicep/        # Bicep IaC templates organized by scenario
├── BicepModules/       # Reusable Bicep modules
├── OMS/                # Operations Management Suite scripts
├── OpsMgr/             # SCOM management pack projects
├── Scripts/            # Utility and automation scripts
└── azure-pipelines/    # Azure Pipelines CI/CD definitions
```

---

## Azure-Bicep Templates

Each subdirectory under `Azure-Bicep/` is a self-contained deployment scenario with its own `main.bicep` and parameter files.

| Directory | Deployment Scope | Description |
|-----------|-----------------|-------------|
| `sql.vm/` | Subscription | Deploys a SQL Server VM cluster with configurable data disks, networking, and Always On availability group listeners. |
| `management.group/` | Tenant | Creates a multi-tier Azure Management Group hierarchy (up to 6 tiers). |
| `policy-definitions/` | Management Group | Deploys custom Azure Policy definitions for storage security, resource locations, and tagging enforcement. |
| `policy-initiatives/` | Management Group | Bundles multiple policy definitions into policy initiatives (policy sets). |
| `policy.monitor/` | Resource Group | Deploys Azure Monitor alert rules driven by Azure Policy, with action groups and a user-assigned managed identity. |
| `private.endpoint.static.ip/` | Resource Group | Creates storage account private endpoints (blob and DFS) with statically assigned IP addresses. |
| `role.definitions/` | Subscription | Deploys custom Azure RBAC role definitions with automatic scope discovery and assignment. |
| `static.ip.allocation/` | Subscription | Allocates static private IP addresses to VMs using CIDR host calculations. |
| `vm-run-cmd/` | VM Extension | Executes inline PowerShell or shell scripts on Azure VMs using the VM Run Command extension. |
| `vnet-isolated-cloud-shell/` | Resource Group | Deploys an isolated Azure Cloud Shell environment inside a VNet with an Azure Relay private endpoint. |
| `adf-global-parameters/` | Resource Group | Deploys Azure Data Factory with global parameters and optional Git integration. |

---

## Reusable Bicep Modules (`BicepModules/`)

| Module | Description |
|--------|-------------|
| `authorization/policy-definition/` | Reusable module for deploying Azure Policy definitions at subscription or management group scope. |
| `authorization/policy-set-definition/` | Reusable module for deploying policy initiatives at subscription or management group scope. |
| `network-security-group/` | Reusable module for deploying Network Security Groups with configurable rules. |

---

## Scripts

### `Azure/` – Azure Resource Scripts
| Script | Description |
|--------|-------------|
| `CreatePurviewIR.ps1` | Creates self-hosted or managed Integration Runtimes on an Azure Purview account. |
| `Get-AzureSQLDBDTU.ps1` | Calculates the DTU requirement for an Azure SQL Database based on core count and performance metrics. |
| `Get-AzureSQLDBElasticPoolDTU.ps1` | Calculates the DTU requirement for an Azure SQL Elastic Pool. |

### `Scripts/Azure/`
| Script | Description |
|--------|-------------|
| `AzPolicyRestriction.ps1` | Queries the Azure Policy Insights API to check whether a resource would be denied or audited by existing policies. |

### `Scripts/psDocs/`
| Script | Description |
|--------|-------------|
| `generateBicepReadme.ps1` | Auto-generates Markdown README files from Bicep templates using the [PSDocs](https://github.com/microsoft/PSDocs) PowerShell module. |

---

## Operations Manager (`OpsMgr/`)

| Project | Description |
|---------|-------------|
| `OMS.NRT.Perf.Collection.Demo/` | SCOM management pack that collects SQL Database cache hit ratio performance counters and forwards them to Log Analytics. |
| `OMS.Network.Performance.Monitor.Agent.Task/` | SCOM management pack tasks for enabling, disabling, and configuring the OMS Network Performance Monitor agent. |

---

## OMS

| Script | Description |
|--------|-------------|
| `OMS/New-ConfigMgr-OMS-App.ps1` | Registers System Center Configuration Manager (SCCM) as an application in Azure Active Directory and connects it to a Log Analytics workspace. |

---

## CI/CD (`azure-pipelines/`)

The `azure-pipelines/` directory contains Azure Pipelines YAML files for build-validation workflows that enforce branch policies on pull requests.

---

## Prerequisites

- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) or [Azure PowerShell](https://learn.microsoft.com/en-us/powershell/azure/) for script execution.
- [Bicep CLI](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/install) to compile or deploy Bicep templates directly.
- Appropriate Azure RBAC permissions for the target deployment scope (e.g., Owner or Contributor at the subscription/management group).
- PowerShell 5.1+ or PowerShell 7+ for scripts in the `Azure/` and `Scripts/` directories.

---

## License

MIT License – Copyright © 2021 Tao Yang. See [LICENSE](./LICENSE) for details.