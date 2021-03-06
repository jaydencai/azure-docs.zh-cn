---
title: 查看模型详细信息 - 自定义翻译
titleSuffix: Azure Cognitive Services
description: 任何项目下的“模型”选项卡会显示每个模型的详细信息，例如模型名称、模型状态、BLEU 评分、训练、优化、测试句子计数。
author: rajdeep-in
manager: christw
ms.service: cognitive-services
ms.subservice: translator-text
ms.date: 02/21/2019
ms.author: v-rada
ms.topic: conceptual
ms.openlocfilehash: 13f3d88ad69d2acc64b9a6469415eceaf22fa491
ms.sourcegitcommit: 5fbca3354f47d936e46582e76ff49b77a989f299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2019
ms.locfileid: "57764382"
---
# <a name="view-model-details"></a>查看模型详细信息

项目下的“模型”选项卡显示该项目中的所有模型。 为该项目训练的所有模型列在此选项卡中。

在项目中每个模型，显示了这些详细信息。

1.  模型名称：显示给定模型的模型名称。

2.  状态：显示给定模型的状态。 新的训练在接受之前一直显示为“已提交”状态。 在服务评估文档的内容时，状态将更改为“正在处理数据”。 文档评估完成时，状态将更改为“正在运行”，此时可以查看训练中包含的句子数，包括系统自动创建的优化和测试集。 下面是描述模型状态的模型状态列表。

    -  已提交：指定后端正在处理该模型的文档。

    -  训练已排队：指定训练正在该模型的 MT 系统中排队。

    -  正在运行：指定训练正在该模型的 MT 系统中运行。

    -  成功：指定训练在 MT 系统中成功，并且模型可用。 处于此状态时，将显示该模型的 BLEU 评分。

    -  已部署：指定已将成功训练的模型提交到 MT 系统进行部署。

    -  正在取消部署：指定正在取消部署已部署的模型。

    -  已取消部署：指定已成功完成模型的取消部署过程。

    -  训练失败：指定训练已失败。 如果发生训练失败，请重试训练作业。 如果错误持续出现，请联系我们。 请勿删除失败的模型。

    - 数据处理失败：指定属于模型的一个或多个文档的数据处理失败。

    - 部署失败：指定模型部署已失败。

    - 迁移草稿：指定模型在从中心迁移到自定义翻译后处于草稿状态。

4.  BLEU 评分：显示模型的 BLEU（双语评估辅助）评分，指示翻译系统的质量。 此评分告知翻译系统在此次训练后提供的翻译，与测试数据集中的参考句子之间的近似程度。 如果训练成功完成，则会显示 BLEU 评分。 如果训练未完成/失败，则不会显示任何 BLEU 评分。

5.  训练句子计数：显示用作训练集的句子总数。

6.  优化句子计数：显示用作优化集的句子总数。

7.  训练句子计数：显示用作测试集的句子总数。

8.  单语句子计数：显示用作单语集的句子总数。

9.  部署操作按钮：对于成功训练的但尚未部署的模型，将显示“部署”按钮。 如果模型已部署，则会显示“取消部署”按钮。

10. 删除：使用此按钮可以删除模型。 删除某个模型不会删除用于创建该模型的任何文档。

    ![查看模型详细信息](media/how-to/how-to-view-model-details.png)

>[!Note]
>若要比较相同系统的连续训练，必须将优化集和测试集保持恒定。

## <a name="view-model-training-details"></a>查看模型训练详细信息

训练完成后，可在“详细信息”页中查看有关该训练的详细信息。 选择一个项目，找到并选择“模型”选项卡，然后选择一个模型。

模型页面有两个选项卡：“训练详细信息”和“测试”。

1.  **训练详细信息：** 此选项卡显示训练中使用的文档列表：

    -  文档名称：此字段显示文档的名称

    -  文档类型：此字段显示此文档是并行还是单语的。

    -  源语言中的句子计数：此字段显示源语言中包含的句子数量。

    -  目标语言中的句子计数：此字段显示目标语言中包含的句子数量。

    -  对齐的句子数：此字段显示自定义翻译在对齐过程中对齐的句子数。

    -  使用的句子数：此字段显示自定义翻译在此训练过程中使用的句子数。

    ![模型训练详细信息](media/how-to/how-to-model-training-details.png)

2.  **测试：** 此选项卡显示成功训练的测试详细信息。

## <a name="next-steps"></a>后续步骤

- 查看[测试结果](how-to-view-system-test-results.md)并分析训练结果。
