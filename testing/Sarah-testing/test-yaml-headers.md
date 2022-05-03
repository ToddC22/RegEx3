---
title: Operations Guide for Microsoft Teams
author: rmw2890
ms.author: Rowille
audience: admin
manager: serdars
ms.date: 06/11/2019
ms.topic: conceptual
ms.service: msteams
search.appverid: MET150
ms.reviewer: rowille
description: Tasks and activities required for Teams service management, including monitoring service health, and assessing and ensuring network quality and usage.
f1.keywords:
- NOCSH
ms.localizationpriority: medium
ms.collection: 
  - M365-voice
  - M365-collaboration
appliesto: 
  - Microsoft Teams
---

# Acrolinx test

https://dev.azure.com/ceapex/CPS/_workitems/edit/550102
RBAC roles

https://dev.azure.com/ceapex/CPS/_workitems/edit/591238
There are several Azure Quickstart Template available here.

Need to send to add to lexicon: demonstratable, grabbable

CScript

Smartlist

Microsoft 365 Defender

WACTH

If you don't need the resources the script created, use the az group delete command to delete the resource group and all resources it contains, including the Azure Cosmos DB account and database.

## Sample script

This script uses the following commands:

- [az group create](/cli/azure/group#az-group-create) creates a resource group to store all resources.
- [az cosmosdb create](/cli/azure/cosmosdb#az-cosmosdb-create) with the `--capabilities EnableGremlin` parameter creates a Gremlin-enabled Azure Cosmos DB account.
- [az cosmosdb gremlin database create](/cli/azure/cosmosdb/gremlin/database#az-cosmosdb-gremlin-database-create) creates an Azure Cosmos DB Gremlin database.
- [az cosmosdb gremlin graph create](/cli/azure/cosmosdb/gremlin/graph#az-cosmosdb-gremlin-graph-create) with the `--max-throughput` parameter set to minimum `4000` creates an Azure Cosmos DB Gremlin graph with autoscale.

:::code language="azurecli" source="~/azure_cli_scripts/cosmosdb/gremlin/autoscale.sh" id="FullScript":::
