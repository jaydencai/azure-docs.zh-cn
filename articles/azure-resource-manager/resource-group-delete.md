---
title: Azure 资源管理器删除资源组
description: 介绍删除资源组时 Azure 资源管理器如何为资源的删除排序。
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2018
ms.author: tomfitz
ms.openlocfilehash: 8b0711cab07584aa84ab437a2a4efb5aab92f3d1
ms.sourcegitcommit: a08d1236f737915817815da299984461cc2ab07e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2018
ms.locfileid: "52318906"
---
# <a name="azure-resource-manager-resource-group-deletion"></a>Azure 资源管理器资源组的删除

本文介绍在删除资源组时 Azure 资源管理器如何为资源的删除排序。

## <a name="determine-order-of-deletion"></a>确定删除顺序

删除资源组时，资源管理器会确定删除资源的顺序。 采用以下顺序：

1. 删除所有子（嵌套）资源。

2. 接下来，删除管理其他资源的资源。 可以为资源设置 `managedBy` 属性，用于指示管理它的其他资源。 设置此属性后，先删除管理其他资源的资源，再删除受管理的这些资源。

3. 删除前两种类别后，便会删除剩余资源。

## <a name="resource-deletion"></a>资源的删除

确定顺序后，资源管理器为每个资源发出 DELETE 操作。 它先等待所有依赖项均完成操作，再继续。

对于同步操作，预期的成功响应代码为：

* 200
* 204
* 404

对于异步操作，预期的成功响应代码为 202。 资源管理器会跟踪 location 标头或 azure-async operation 标头，以确定异步删除操作的状态。
  
### <a name="errors"></a>错误

如果删除操作返回错误，资源管理器会重试 DELETE 调用。 若状态代码为 5xx、429 和 408，便会重试。 默认情况下，重试的时间段为 15 分钟。

## <a name="after-deletion"></a>删除之后

资源管理器对其尝试删除的每个资源发出 GET 调用。 此 GET 调用的响应应为 404。 当资源管理器获得 404 时，便将删除操作视为成功完成。 资源管理器会从其缓存中删除资源。

但是，如果对资源的 GET 调用返回 200 或 201，资源管理器会重新创建资源。

### <a name="errors"></a>错误

如果 GET 操作返回错误，资源管理器会为以下错误代码重试 GET 调用：

* 小于 100
* 408
* 429
* 大于 500

对于其他错误代码，它会将删除操作视为失败。

## <a name="next-steps"></a>后续步骤

* 若要了解资源管理器概念，请参阅 [Azure 资源管理器概述](resource-group-overview.md)。
* 若要查看资源提供程序的操作，请参阅 [Azure REST API](/rest/api/)。