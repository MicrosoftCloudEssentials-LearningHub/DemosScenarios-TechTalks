# Autoscale IOPS for multiple Azure MySQL Flexible Server

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-05-12

----------

> Using [Python 3.7+](https://www.python.org/downloads/source/)

> [!NOTE]
>  Enable Autoscale IOPS via REST API, as now this is the only way to automate enabling Autoscale IOPS since, Azure CLI and PowerShell do not support this setting yet.

> [!IMPORTANT]
> Autoscale IOPS is `only available` for the `General Purpose` and `Business Critical tiers`. `Burstable tier` (B-series) servers (e.g., B1ms) `do not support autoscale IOPS`.

## Pre-requisites

- Install azure-identity with: `py -m pip install azure-identity requests`

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/fa74f47c-bef2-4ad3-8b0f-2ee50813c486" />

-  [Install Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) to work with both Terraform and Azure commands.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/3f552ecc-8e07-453a-9655-8bb5a89e1791" />

## By Resource Group

> - Automatically retrieves your **Azure subscription ID** using the Azure CLI. <br/>
> - Prompts you only for the **resource group name**. <br/>
> - Lists all MySQL Flexible Servers in that resource group. <br/>
> - Sends a `PATCH request`` to enable `autoIoScaling` for each server using the `Azure REST API`

1. Make sure you're logged in: `az login`


## Across a Subscription

> You can also enable autoscale IOPS across an entire subscription, it requires: <br/>
> - Listing all MySQL Flexible Servers in the subscription. <br/>
> - For each server, retrieving its resource group.  <br/>
> - Applying the update if the server is in a supported tier (General Purpose or Business Critical).  <br/>

## Azure CLI Script to Enable Autoscale IOPS 

> [!NOTE]
> The script below will execute: <br/>
> - Using Python 3.13.3  <br/>
> - Checks if Azure CLI is available at the specified path.  <br/>
> - Lists all MySQL Flexible Servers. <br/>
> - Tries to get each server’s resource group. <br/>
> - If the resource group is missing, it prompts you to enter it. <br/>
> - Asks for confirmation before enabling autoscale IOPS. <br/>

```python
import subprocess
import json

# Step 1: Get list of MySQL Flexible Servers
servers_output = subprocess.check_output(
    ["az", "mysql", "flexible-server", "list", "--query", "[].name", "-o", "tsv"],
    text=True
)
servers = servers_output.strip().splitlines()

# Step 2: Loop through each server and enable autoscale IOPS
for server in servers:
    # Get the resource group for the server
    rg_output = subprocess.check_output(
        ["az", "mysql", "flexible-server", "show", "--name", server, "--query", "resourceGroup", "-o", "tsv"],
        text=True
    )
    resource_group = rg_output.strip()

    print(f"Enabling autoscale IOPS for {server} in {resource_group}...")

    # Update the server to enable autoscale IOPS
    subprocess.run([
        "az", "mysql", "flexible-server", "update",
        "--name", server,
        "--resource-group", resource_group,
        "--iops", "Auto"
    ])
```

## How to execute it Azure CLI Script to Enable Autoscale IOPS

1. Download [the script](./enable_autoscale_iops.py) to your local machine or a cloud shell environment.
2. Make sure you're logged in: `az login`
4. Run the script: `py enable_autoscale_iops.py`

> Example: enabling Autoscale IOPS on three different servers, each hosted in a separate resource group but under the same subscription.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/22aa763d-b358-441a-b5b9-aa0197ce680d" />


<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
