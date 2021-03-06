---
author: msmbaldwin
ms.service: key-vault
ms.topic: include
ms.date: 01/31/2019
ms.author: mbaldwin
ms.openlocfilehash: d8e33113ca9f0886a4cef1c8f9acb855b32c2973
ms.sourcegitcommit: 3aa0fbfdde618656d66edf7e469e543c2aa29a57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2019
ms.locfileid: "58114714"
---
## <a name="preventative"></a>预防

| 安全属性 | Yes/No | 说明 |
|---|---|--|
| 静态加密：<ul><li>服务器端加密</li><li>使用客户托管密钥的服务器端加密</li><li>其他加密功能（例如客户端、始终加密等）</ul>| 是 |  |
| 传输中加密：<ul><li>快速路由加密</li><li>Vnet 中加密</li><li>VNet-VNet 加密</ul>| 是 | 支持标准的 HTTPS/TLS 机制。  传输到服务之前，用户还可以加密数据。 |
| 加密密钥处理（CMK、BYOK 等）| 是 | 请参阅[使用 Azure Key Vault 中客户托管密钥的存储服务加密](../articles/storage/common/storage-service-encryption-customer-managed-keys.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)。|
| 列级加密（Azure 数据服务）| 不适用 |  |
| 加密的 API 调用| 是 |  |

## <a name="network-segmentation"></a>网络分段

| 安全属性 | Yes/No | 说明 |
|---|---|--|
| 服务终结点支持| 是 |  |
| vNET 注入支持| 不适用 |  |
| 网络隔离/防火墙支持| 是 | |
| 支持强制隧道 | 不适用 |  |

## <a name="detection"></a>检测

| 安全属性 | Yes/No | 说明|
|---|---|--|
| Azure 监视支持（Log Analytics、App Insights 等）| 是 | 可用的 azure Monitor 指标现在，可以记录开始预览 |

## <a name="iam-support"></a>IAM 支持

| 安全属性 | Yes/No | 说明|
|---|---|--|
| 访问管理 - 身份验证| 是 | Azure Active Directory、 共享密钥、 共享访问令牌。 |
| 访问管理 - 授权| 是 | 支持通过 RBAC、 POSIX Acl 和 SAS 令牌的授权 |


## <a name="audit-trail"></a>审核线索

| 安全属性 | Yes/No | 说明|
|---|---|--|
| 控制/管理计划日志记录和审核 | 是 | Azure 资源管理器活动日志 |
| 数据平面日志记录和审核| 是 | 服务诊断日志和 Azure Monitor 日志记录开始预览  |

## <a name="configuration-management"></a>配置管理

| 安全特性 | Yes/No | 说明|
|---|---|--|
| 配置管理支持（配置的版本控制等）| 是 | 支持通过 Azure 资源管理器 Api 的资源提供程序版本控制 |