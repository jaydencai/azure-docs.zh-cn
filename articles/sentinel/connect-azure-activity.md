---
title: 收集 Azure Sentinel 预览版中的 Azure 活动数据 |Microsoft Docs
description: 了解如何收集 Azure 活动数据在 Azure Sentinel。
services: sentinel
documentationcenter: na
author: rkarlin
manager: barbkess
editor: ''
ms.assetid: 8c25baa8-b93b-41da-9e6c-15bb7b5c5511
ms.service: sentinel
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 2/28/2019
ms.author: rkarlin
ms.openlocfilehash: 42ce8d06489cfacf7ba9bb3de1425224b5df95e7
ms.sourcegitcommit: ad019f9b57c7f99652ee665b25b8fef5cd54054d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2019
ms.locfileid: "57240569"
---
# <a name="collect-data-from-azure-activity-log"></a>从 Azure 活动日志中收集数据

> [!IMPORTANT]
> Azure Sentinel 目前处于公共预览状态。
> 此预览版在提供时没有附带服务级别协议，不建议将其用于生产工作负荷。 某些功能可能不受支持或者受限。 有关详细信息，请参阅 [Microsoft Azure 预览版补充使用条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)。

可以从日志流式传输[Azure 活动日志](../azure-monitor/platform/activity-logs-overview.md)到 Azure Sentinel 单击一次。 活动日志是一种深入了解 Azure 中发生的订阅级别事件的订阅日志。 这包括从 Azure 资源管理器操作数据到服务运行状况事件更新的一系列数据。 使用活动日志，您可以确定 ' 什么，谁，以及何时的任何写入操作 (PUT、 POST、 DELETE) 在订阅中的资源执行的。 还可以了解该操作和其他相关属性的状态。 活动日志不包括读取 (GET) 操作或使用经典的资源的操作 /"RDFE"模型。 


## <a name="prerequisites"></a>必备组件

- 具有全局管理员或安全管理员权限的用户


## <a name="connect-to-azure-activity-log"></a>连接到 Azure 活动日志

1. 在 Azure Sentinel，选择**数据收集**，然后单击**Azure 活动日志**磁贴。

2. 在 Azure 活动日志窗格中，选择你想要流式传输到 Azure Sentinel 的订阅。 

3. 单击“连接”。

4. 若要使用 Log Analytics 中的 Azure 活动警报相关的架构，搜索**AzureActivity**。


 

## <a name="next-steps"></a>后续步骤
在本文档中，您学习了如何将 Azure 活动日志连接到 Azure Sentinel。 若要了解有关 Azure Sentinel 的详细信息，请参阅以下文章：
- 了解如何[来了解一下你的数据和潜在威胁](quickstart-get-visibility.md)。
- 开始[检测威胁 Azure Sentinel](tutorial-detect-threats.md)。
