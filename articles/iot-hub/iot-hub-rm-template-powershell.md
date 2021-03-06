---
title: 使用模板创建 Azure IoT 中心 (PowerShell) | Microsoft Docs
description: 如何使用 Azure 资源管理器模板和 PowerShell 创建 IoT 中心。
author: robinsh
manager: philmea
ms.author: robinsh
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 08/08/2017
ms.openlocfilehash: fcc9af9e614b0a1b7977ba18f3147fddab8b7b7d
ms.sourcegitcommit: 8313d5bf28fb32e8531cdd4a3054065fa7315bfd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2019
ms.locfileid: "59045042"
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>使用 Azure 资源管理器模板创建 IoT 中心 (PowerShell)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

可以使用 Azure 资源管理器以编程方式创建和管理 Azure IoT 中心。 本教程介绍如何将 Azure 资源管理器模板与 PowerShell 配合使用来创建 IoT 中心。

> [!NOTE]
> Azure 具有用于创建和处理资源的两个不同部署模型：[Azure 资源管理器部署模型和经典部署模型](../azure-resource-manager/resource-manager-deployment-model.md)。 本文介绍了如何使用 Azure 资源管理器部署模型。

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

要完成本教程，需要具备以下先决条件：

* 有效的 Azure 帐户。 <br/>如果没有帐户，只需几分钟即可创建一个[免费帐户][lnk-free-trial]。
* [Azure PowerShell 1.0][lnk-powershell-install] 或更高版本。

> [!TIP]
> [将 Azure PowerShell 与 Azure 资源管理器配合使用][lnk-powershell-arm]一文提供了有关如何使用 PowerShell 和 Azure 资源管理器模板创建 Azure 资源的详细信息。

## <a name="connect-to-your-azure-subscription"></a>连接到 Azure 订阅

在 PowerShell 命令提示符中，输入以下命令以登录 Azure 订阅：

```powershell
Connect-AzAccount
```

如果有多个 Azure 订阅，则访问 Azure 即有权访问与凭据关联的所有 Azure 订阅。 使用以下命令，列出可供使用的 Azure 订阅：

```powershell
Get-AzSubscription
```

使用以下命令，选择想要用于运行命令以创建 IoT 中心的订阅。 可使用上一命令输出中的订阅名称或 ID：

```powershell
Select-AzSubscription `
    -SubscriptionName "{your subscription name}"
```

可以使用以下命令来发现可部署 IoT 中心的位置和当前支持的 API 版本：

```powershell
((Get-AzResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

在 IoT 中心支持的位置之一，使用以下命令创建资源组来包含 IoT 中心。 本示例将创建一个名为 **MyIoTRG1** 的资源组：

```powershell
New-AzResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-to-create-an-iot-hub"></a>提交模板以创建 IoT 中心

使用 JSON 模板在资源组中创建 IoT 中心。 还可以使用 Azure 资源管理器模板更改现有 IoT 中心。

1. 使用文本编辑器创建名为 **template.json** 的 Azure 资源管理器模板，并指定以下资源定义来创建新的标准 IoT 中心。 此示例在**美国东部**区域中添加 IoT 中心，在事件中心兼容的终结点上创建两个使用者组（**cg1** 和 **cg2**），并使用 **2016-02-03** API 版本。 此模板还要求以名为 **hubName** 的参数的形式传入 IoT 中心名称。 有关支持 IoT 中心的位置的最新列表，请参阅 [Azure 状态][lnk-status]：

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. 将 Azure 资源管理器模板文件保存到本地计算机。 本示例假设将它保存在名为 **c:\templates** 的文件夹中。

3. 运行以下命令部署新的 IoT 中心，并传递 IoT 中心的名称作为参数。 在此示例中，IoT 中心的名称是 `abcmyiothub`。 IoT 中心的名称必须全局唯一：

    ```powershell
    New-AzResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. 输出会显示你创建的 IoT 中心的密钥。

5. 若要验证应用程序是否添加了新的 IoT 中心，请访问 [Azure 门户][lnk-azure-portal]并查看资源列表。 另外，也可以使用 **Get-AzResource** PowerShell cmdlet。

> [!NOTE]
> 本示例应用程序将添加用于对你计费的 S1 标准 IoT 中心。 在完成任务后，可以通过 [Azure 门户][lnk-azure-portal] 或者使用 **Remove-AzResource** PowerShell cmdlet 删除该 IoT 中心。

## <a name="next-steps"></a>后续步骤

现在，已使用 Azure 资源管理器模板和 PowerShell 部署了一个 IoT 中心，接下来可以进一步进行探索：

* 阅读了解 [IoT 中心资源提供程序 REST API][lnk-rest-api] 的相关功能。
* 有关 Azure 资源管理器功能的详细信息，请参阅 [Azure 资源管理器概述][lnk-azure-rm-overview]。
* 有关要在模板中使用的 JSON 语法和属性，请参阅 [Microsoft.Devices 资源类型](/azure/templates/microsoft.devices/iothub-allversions)。

若要详细了解如何开发 IoT 中心，请参阅以下文章：

* [C SDK 简介][lnk-c-sdk]
* [Azure IoT SDK][lnk-sdks]

若要进一步探索 IoT 中心的功能，请参阅：

* [使用 Azure IoT Edge 将 AI 部署到边缘设备][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-Az-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/manage-resources-powershell.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: ../iot-edge/tutorial-simulate-device-linux.md
