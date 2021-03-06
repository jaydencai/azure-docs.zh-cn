---
title: Azure 数据工厂映射数据流有条件拆分转换
description: Azure 数据工厂数据流有条件拆分转换
author: kromerm
ms.author: makromer
ms.reviewer: douglasl
ms.service: data-factory
ms.topic: conceptual
ms.date: 02/03/2019
ms.openlocfilehash: a4ea79e05165dfae4f79aa6473a07151ba7c00fc
ms.sourcegitcommit: 90c6b63552f6b7f8efac7f5c375e77526841a678
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56727802"
---
# <a name="azure-data-factory-mapping-data-flow-conditional-split-transformation"></a>Azure 数据工厂映射数据流有条件拆分转换

[!INCLUDE [notes](../../includes/data-factory-data-flow-preview.md)]

有条件拆分转换可以将数据行路由到不同的流，具体取决于数据的内容。 有条件拆分转换的实现类似于编程语言中的 CASE 决策结构。 转换计算表达式，并根据结果将数据行定向到指定的流。 此转换还提供默认输出，因此，如果某行与任何表达式都不匹配，它会被定向到默认输出。

![有条件拆分](media/data-flow/cd1.png "有条件拆分")

若要添加附加条件，请在底部配置窗格中选择“添加流”，并单击“表达式生成器”文本框来生成表达式。
