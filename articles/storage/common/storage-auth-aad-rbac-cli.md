---
title: 使用 Azure CLI 管理 Azure AD 对使用 RBAC 的 Azure 存储的 blob 和队列数据的访问权限
description: 使用 Azure CLI 授予对容器和队列使用基于角色的访问控制 (RBAC) 访问权限。 Azure 存储支持通过 Azure AD 进行身份验证的内置和自定义 RBAC 角色。
services: storage
author: tamram
ms.service: storage
ms.topic: article
ms.date: 03/21/2019
ms.author: tamram
ms.subservice: common
ms.openlocfilehash: de8cb99ae5db93c2438a9ea982ad1c6c9324b47f
ms.sourcegitcommit: f0f21b9b6f2b820bd3736f4ec5c04b65bdbf4236
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2019
ms.locfileid: "58449951"
---
# <a name="grant-access-to-azure-blob-and-queue-data-with-rbac-using-azure-cli"></a>授予对 Azure blob 和队列数据与使用 Azure CLI 的 RBAC 访问权限

Azure Active Directory (Azure AD) 通过[基于角色的访问控制 (RBAC)](../../role-based-access-control/overview.md) 授权访问受保护的资源。 Azure 存储定义包含常见的用来访问 blob 或队列数据的权限集的内置 RBAC 角色的一组。 

RBAC 角色分配到 Azure AD 安全主体，Azure 授予访问这些资源时为该安全主体。 可以将访问权限限定于订阅、资源组、存储帐户、单个容器或队列级别。 Azure AD 安全主体可能是用户、 组、 应用程序服务主体，或[管理 Azure 资源的标识](../../active-directory/managed-identities-azure-resources/overview.md)。

本文介绍如何使用 Azure CLI 列出内置 RBAC 角色，并将其分配给用户。 有关使用 Azure CLI 的详细信息，请参阅[Azure 命令行接口 (CLI)](https://docs.microsoft.com/cli/azure)。

## <a name="rbac-roles-for-blobs-and-queues"></a>Blob 和队列的 RBAC 角色

[!INCLUDE [storage-auth-rbac-roles-include](../../../includes/storage-auth-rbac-roles-include.md)]

## <a name="determine-resource-scope"></a>确定资源范围 

[!INCLUDE [storage-auth-resource-scope-include](../../../includes/storage-auth-resource-scope-include.md)]

## <a name="list-available-rbac-roles"></a>列出可用的 RBAC 角色

若要列出可用 Azure CLI 的内置 RBAC 角色，请使用[az 角色定义列表](/cli/azure/role/definition#az-role-definition-list)命令：

```azurecli-interactive
az role definition list --out table
```

你将看到列出，以及其他内置角色适用于 Azure 内置的 Azure 存储数据角色：

```Example
Storage Blob Data Contributor             Allows for read, write and delete access to Azure Storage blob containers and data
Storage Blob Data Owner                   Allows for full access to Azure Storage blob containers and data, including assigning POSIX access control.
Storage Blob Data Reader                  Allows for read access to Azure Storage blob containers and data
Storage Queue Data Contributor            Allows for read, write, and delete access to Azure Storage queues and queue messages
Storage Queue Data Message Processor      Allows for peek, receive, and delete access to Azure Storage queue messages
Storage Queue Data Message Sender         Allows for sending of Azure Storage queue messages
Storage Queue Data Reader                 Allows for read access to Azure Storage queues and queue messages
```

## <a name="assign-an-rbac-role-to-a-user"></a>向用户分配有 RBAC 角色

若要将 RBAC 角色分配给用户，请使用[az 角色分配创建](/cli/azure/role/assignment#az-role-assignment-create)命令。 该命令的格式可能不同基于分配的范围。 以下示例演示如何将角色分配给不同范围内的用户。

### <a name="container-scope"></a>容器作用域

若要将分配到容器作用域的角色，请指定一个包含容器的作用域字符串`--scope`参数。 容器的作用域是在窗体中：

```
/subscriptions/<subscription>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/<storage-account>/blobServices/default/containers/<container-name>
```

以下示例将分配**存储 Blob 数据参与者**到用户，应用范围限定为一个名为容器角色*示例容器*。 请确保将示例值和中括号内的占位符值替换为你自己的值： 

```azurecli-interactive
az role assignment create \
    --role "Storage Blob Data Contributor" \
    --assignee <email> \
    --scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/<storage-account>/blobServices/default/containers/sample-container"
```

### <a name="queue-scope"></a>队列范围

若要将分配到的队列作用域的角色，请指定一个包含有关队列的作用域字符串`--scope`参数。 队列的作用域是在窗体中：

```
/subscriptions/<subscription>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/<storage-account>/queueServices/default/queues/<queue-name>
```

以下示例将分配**存储队列数据参与者**到名为的队列为作用域的用户角色*示例队列*。 请确保将示例值和中括号内的占位符值替换为你自己的值： 

```azurecli-interactive
az role assignment create \
    --role "Storage Queue Data Contributor" \
    --assignee <email> \
    --scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/<storage-account>/queueServices/default/queues/sample-queue"
```

### <a name="storage-account-scope"></a>存储帐户范围

若要将分配到存储帐户作用域的角色，请指定的存储帐户资源的作用域`--scope`参数。 存储帐户的作用域是在窗体中：

```
/subscriptions/<subscription>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/<storage-account>
```

下面的示例演示如何将分配**存储 Blob 数据读取器**到存储帐户级别的用户角色。 请确保将示例值替换为你自己的值： 

```azurecli-interactive
az role assignment create \
    --role "Storage Blob Data Reader" \
    --assignee <email> \
    --scope "/subscriptions/<subscription-id>/resourceGroups/sample-resource-group/providers/Microsoft.Storage/storageAccounts/storagesamples"
```

### <a name="resource-group-scope"></a>资源组范围内

若要将分配到资源组作用域的角色，请指定资源组名称或 ID`--resource-group`参数。 以下示例将分配**存储队列数据读取器**到资源组级别的用户角色。 请确保将示例值和括号中的占位符值替换为你自己的值： 

```azurecli-interactive
az role assignment create \
    --role "Storage Queue Data Reader" \
    --assignee <email> \
    --resource-group sample-resource-group
```

### <a name="subscription-scope"></a>订阅范围内

若要将分配到订阅作用域的角色，请指定的订阅的作用域`--scope`参数。 订阅的作用域是在窗体中：

```
/subscriptions/<subscription>
```

下面的示例演示如何将分配**存储 Blob 数据读取器**到存储帐户级别的用户角色。 请确保将示例值替换为你自己的值： 

```azurecli-interactive
az role assignment create \
    --role "Storage Blob Data Reader" \
    --assignee <email> \
    --scope "/subscriptions/<subscription-id>"
```

## <a name="next-steps"></a>后续步骤

- [使用 RBAC 和 Azure PowerShell 管理对 Azure 资源的访问权限](../../role-based-access-control/role-assignments-powershell.md)
- [授予对 Azure blob 和队列数据与使用 Azure PowerShell 的 RBAC 访问权限](storage-auth-aad-rbac-powershell.md)
- [授予对 Azure blob 和队列数据使用 RBAC 在 Azure 门户中访问权限](storage-auth-aad-rbac-portal.md)
