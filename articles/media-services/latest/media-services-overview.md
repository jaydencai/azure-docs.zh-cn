---
title: Azure 媒体服务 v3 概述 | Microsoft Docs
description: 本文提供媒体服务的高级概述和包含详细信息的相关文章的链接。
services: media-services
documentationcenter: na
author: Juliako
manager: femila
editor: ''
tags: ''
keywords: azure 媒体服务, 流, 广播, 实时, 脱机
ms.service: media-services
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: media
ms.date: 03/20/2019
ms.author: juliako
ms.custom: mvc
ms.openlocfilehash: 88113fee64251344bd84085caedc9dfccfa10933
ms.sourcegitcommit: 87bd7bf35c469f84d6ca6599ac3f5ea5545159c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58351450"
---
# <a name="what-is-azure-media-services-v3"></a>什么是 Azure 媒体服务 v3？

Azure 媒体服务是一个基于云的平台，用于生成解决方案，以便实现广播质量的视频流、增强可访问性和分发、分析内容，等等。 无论你是应用程序开发者、呼叫中心、政府机构还是娱乐公司，媒体服务都能帮助你创建应用程序，通过当今最热门的移动设备和浏览器向广大受众提供品质卓越的媒体体验。 

> [!NOTE]
> 目前，无法使用 Azure 门户来管理 v3 资源。 请使用 [REST API](https://aka.ms/ams-v3-rest-ref)、[CLI](https://aka.ms/ams-v3-cli-ref) 或支持的 [SDK](developers-guide.md) 之一。

## <a name="what-can-i-do-with-media-services"></a>媒体服务的功能是什么？

通过媒体服务，可以在云中生成各种媒体工作流，以下是媒体服务功能的一些示例。  

* 提供各种格式的视频，以便通过各种浏览器和设备播放视频。 对于面向多种客户端（移动设备、电视、电脑等）的按需和实时流式传输交付，需要对视频和音频进行适当的编码和打包。 要了解如何交付和流式传输此类内容，请参阅[快速入门：编码和流式传输文件](stream-files-dotnet-quickstart.md)。
* 向大量在线观众流式传输实时体育赛事，例如足球、棒球、大学和高中体育运动等等。 
* 广播公共会议和活动，例如市政厅、市议会和立法机构。
* 分析录制的视频或音频内容。 例如，为了实现更高的客户满意度，组织可以提取语音转文本并生成搜索索引和仪表板。 然后，他们可以提取围绕常见的投诉、投诉原因以及其他相关数据的情报。
* 当客户（例如电影工作室）需要限制对版权所有作品的访问和使用时，创建订阅视频服务并流式传输受 DRM 保护的内容。
* 提供脱机内容，以便在飞机、火车和汽车上播放。 如果客户希望断开网络连接，可能需要将内容下载到手机或平板电脑上播放。
* 使用 Azure 媒体服务和 [Azure 认知服务 API](https://docs.microsoft.com/azure/#pivot=products&panel=ai) 实现教育在线学习视频平台，提供语音转文本字幕，多种语言翻译等等。 
* 将 Azure 媒体服务与 [Azure 认知服务 API](https://docs.microsoft.com/azure/#pivot=products&panel=ai) 配合使用来为视频添加字幕和描述文字，满足更多受众的需求（例如，听力障碍人士或想用不同语言阅读的人）。
* 启用 Azure CDN 实现大幅度缩放，更好地处理即时高负载（例如在产品发布活动开始时）。 

## <a name="v3-capabilities"></a>v3 功能

v3 基于一个统一的 API 接口，该接口公开了基于 Azure 资源管理器构建的管理和操作功能。 

该版本提供以下功能：  

* “转换”有助于定义媒体处理或分析任务的简单工作流。 “转换”是处理视频和音频文件的一种方法。 可以通过将作业提交到“转换”，重复应用“转换”来处理内容库中的所有文件。
* “作业”用于处理（编码或分析）视频。 可以使用 HTTPS、URL、SAS URL 或位于 Azure Blob 存储中的文件路径，在作业上指定输入内容。 目前，AMS v3 不支持基于 HTTPS URL 的块传输编码。
* “通知”用于监视作业进度或状态，或实时事件启动/停止和错误事件。 “通知”与 Azure 事件网格通知系统集成。 在 Azure 媒体服务中可以轻松订阅多个资源的事件。 
* **Azure 资源管理**模板可用于创建和部署转换、流式处理终结点、实时事件等等。
* 可在资源级别设置**基于角色的访问控制**，从而锁定对特定资源（如转换、实时事件等）的访问。
* 多种语言的客户端 SDK：.NET、.NET core、Python、Go、Java 和 Node.js。

## <a name="naming-conventions"></a>命名约定

Azure 媒体服务 v3 资源名称（例如，资产、作业、转换）需遵循 Azure 资源管理器命名约束。 根据 Azure 资源管理器的要求，资源名称始终必须唯一。 因此，可以为资源名称使用任何唯一的标识符字符串（例如，GUID）。 

媒体服务资源名称不能包含“<”、“>”、“%”、“&”、“:”、“&#92;”、“?”、“/”、“*”、“+”、“.”、单引号或任何控制字符。 允许其他所有字符。 资源名称的最大长度为 260 个字符。 

有关 Azure 资源管理器命名的详细信息，请参阅：[命名需求](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/resource-api-reference.md#arguments-for-crud-on-resource)和[命名约定](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。

## <a name="v3-api-design-principles"></a>v3 API 设计原则

V3 API 的主要设计原则之一是使 API 更安全。 v3 API 不在 **Get** 或 **List** 操作中返回机密或凭据。 在响应中，密钥始终为 null、空值或进行了净化。 你需要调用单独的操作方法来获取机密或凭据。 当某些 API 会检索/显示机密而另一些 API 不会这样做时，可以使用单独的操作设置不同的 RBAC 安全权限。 有关如何使用 RBAC 管理访问权限的信息，请参阅[使用 RBAC 管理访问权限](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-rest)。

此类示例包括 

* 不在 StreamingLocator 的 Get 中返回 ContentKey 值， 
* 不在 ContentKeyPolicy 的 Get 中返回限制密钥， 
* 不返回作业的 HTTP 输入 URL 的查询字符串部分（删除签名）。

请参阅[获取内容密钥策略 - .NET](get-content-key-policy-dotnet-howto.md) 示例。

## <a name="next-steps"></a>后续步骤

如何开始使用 v3？ 

> [!div class="nextstepaction"]
> [了解基本概念](concepts-overview.md)<br/>
> [通过 SDK 使用媒体服务 v3 API 进行开发](developers-guide.md) 

