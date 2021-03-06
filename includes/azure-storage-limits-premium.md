---
title: include 文件
description: include 文件
services: storage
author: roygara
ms.service: storage
ms.topic: include
ms.date: 03/23/2019
ms.author: rogarana
ms.custom: include file
ms.openlocfilehash: e3d2466f05028a963256dbcc052c46650857836d
ms.sourcegitcommit: 49c8204824c4f7b067cd35dbd0d44352f7e1f95e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58372707"
---
### <a name="premium-performance-block-blob-storage"></a>高级性能数据块 blob 存储

高级性能块 blob 存储帐户是使用较小，千字节范围，对象的应用程序进行了优化。 它非常适合于需要非常高事务率或一致的低延迟存储的应用程序。 高级性能数据块 blob 存储被设计为与你的应用程序扩展。 如果你打算部署需要数以百计的千位每秒的请求或千万亿字节的存储容量的应用程序，请与我们联系通过提交支持请求[Azure 门户](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。

### <a name="premium-performance-page-blob-storage"></a>高级性能页 blob 存储

高级的性能，常规用途 v1 或 v2 存储帐户有以下可伸缩性目标：

| 总帐户容量                            | 本地冗余存储帐户的总带宽                     |
| ------------------------------------------------- | --------------------------------------------------------------------------- |
| 磁盘容量：35 TB <br>快照容量：10 TB | 为入站<sup>1</sup> 和出站<sup>2</sup> 流量提供最高 50 Gbps 的带宽 |

<sup>1</sup> 发送到存储帐户的所有数据（请求）

<sup>2</sup> 从存储帐户接收的所有数据（响应）

如果要对非托管磁盘使用高级性能存储帐户和你的应用程序超过了单个存储帐户的可伸缩性目标，你可能想要迁移到托管磁盘。 如果不想要迁移到托管磁盘，请将应用程序构建为使用多个存储帐户。 然后，将数据分布到这些存储帐户中。 例如，如果要将 51-TB 的磁盘附加到多个 VM，请将这些磁盘分散在两个存储帐户中。 35 TB 是单个高级存储帐户的限制。 请确保单个高级性能存储帐户永远不会具有超过 35 TB 的预配的磁盘。