---
title: Create a container in Azure Cosmos DB for Gremlin
description: Learn how to create a container in Azure Cosmos DB for Gremlin by using Azure portal, .NET, and other SDKs.
ms.service: azure-cosmos-db
ms.subservice: apache-gremlin
ms.topic: how-to
ms.date: 10/16/2020
author: manishmsfte
ms.author: mansha
ms.devlang: csharp
ms.custom: devx-track-csharp, devx-track-azurecli, devx-track-dotnet
---

# Create a container in Azure Cosmos DB for Gremlin
[!INCLUDE[Gremlin](../includes/appliesto-gremlin.md)]

This article explains the different ways to create a container in Azure Cosmos DB for Gremlin. It shows how to create a container using Azure portal, Azure CLI, PowerShell, or supported software development kits (SDKs). This article demonstrates how to create a container, specify the partition key, and provision throughput.

This article explains the different ways to create a container in Azure Cosmos DB for Gremlin. If you're using a different API, see [API for MongoDB](../mongodb/how-to-create-container.md), [API for Cassandra](../cassandra/how-to-create-container.md), [API for Table](../table/how-to-create-container.md), and [API for NoSQL](../how-to-create-container.md) articles to create the container.

> [!NOTE]
> When creating containers, make sure you don’t create two containers with the same name but different casing. That’s because some parts of the Azure platform aren't case-sensitive, and this can result in confusion/collision of telemetry and actions on containers with such names.

## <a id="portal-gremlin"></a>Create using Azure portal

1. Sign in to the [Azure portal](https://portal.azure.com/).

1. [Create a new Azure Cosmos DB account](quickstart-dotnet.md), or select an existing account.

1. Open the **Data Explorer** pane, and select **New Graph**. Next, provide the following details:

   * Indicate whether you're creating a new database, or using an existing one.
   * Enter a Graph ID.
   * Select **Unlimited** storage capacity.
   * Enter a partition key for vertices.
   * Enter a throughput to be provisioned (for example, 1000 RUs).
   * Select **OK**.

    :::image type="content" source="../media/how-to-create-container/partitioned-collection-create-gremlin.png" alt-text="Screenshot of API for Gremlin, Add Graph dialog box":::

## <a id="dotnet-sql-graph"></a>Create using .NET SDK

If you encounter timeout exception when creating a collection, do a read operation to validate if the collection was created successfully. The read operation throws an exception until the collection create operation is successful. For the list of status codes supported by the create operation see the [HTTP Status Codes for Azure Cosmos DB](/rest/api/cosmos-db/http-status-codes-for-cosmosdb) article.

```csharp
// Create a container with a partition key and provision 1000 RU/s throughput.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "myContainerName";
myCollection.PartitionKey.Paths.Add("/myPartitionKey");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("myDatabaseName"),
    myCollection,
    new RequestOptions { OfferThroughput = 1000 });
```

## Next steps

* [Partitioning in Azure Cosmos DB](../partitioning-overview.md)
* [Request Units in Azure Cosmos DB](../request-units.md)
* [Provision throughput on containers and databases](../set-throughput.md)
* [Work with Azure Cosmos DB account](../resource-model.md)
