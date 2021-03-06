---
title: 教程：Azure Active Directory 与 InsideView 的集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 和 InsideView 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 845ab85ae10a9d57bf3e263d49532675f60cd84f
ms.sourcegitcommit: 6da4959d3a1ffcd8a781b709578668471ec6bf1b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58517838"
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a>教程：Azure Active Directory 与 InsideView 的集成

本教程介绍如何将 InsideView 与 Azure Active Directory (Azure AD) 集成。

将 InsideView 与 Azure AD 集成具有以下优势：

- 可在 Azure AD 中控制谁有权访问 InsideView
- 可以让用户使用其 Azure AD 帐户自动登录到 InsideView（单一登录）
- 可以在一个中心位置（即 Azure 门户）管理帐户

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>必备组件

若要配置 Azure AD 与 InsideView 的集成，需要以下各项：

- Azure AD 订阅
- InsideView 单一登录已启用的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以在[此处](https://azure.microsoft.com/pricing/free-trial/)获取一个月的试用版。

## <a name="scenario-description"></a>方案描述
在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 InsideView
1. 配置和测试 Azure AD 单一登录

## <a name="adding-insideview-from-the-gallery"></a>从库中添加 InsideView
若要配置 InsideView 与 Azure AD 的集成，需要从库中将 InsideView 添加到托管 SaaS 应用列表。

若要从库中添加 InsideView，请执行以下步骤：

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![Active Directory][1]

1. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![应用程序][2]
    
1. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![应用程序][3]

1. 在搜索框中，键入“InsideView”。

    ![创建 Azure AD 测试用户](./media/insideview-tutorial/tutorial_insideview_search.png)

1. 在结果窗格中，选择“InsideView”，然后单击“添加”按钮添加该应用程序。

    ![创建 Azure AD 测试用户](./media/insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录
在本部分中，基于名为 Britta Simon 的测试用户配置和测试 InsideView 的 Azure AD 单一登录。

若要运行单一登录，Azure AD 需要知道与 Azure AD 用户相对应的 InsideView 用户。 换句话说，需要建立 Azure AD 用户与 InsideView 中相关用户之间的链接关系。

可通过将 Azure AD 中“用户名”的值指定为 InsideView 中“用户名”的值来建立此链接关系。

若要配置和测试 InsideView 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configuring-azure-ad-single-sign-on)** - 让用户使用此功能。
1. **[创建 Azure AD 测试用户](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
1. **[创建 InsideView 测试用户](#creating-an-insideview-test-user)** -Britta Simon 的对应在 InsideView 链接到用户的 Azure AD 表示形式。
1. **[分配 Azure AD 测试用户](#assigning-the-azure-ad-test-user)** - 让 Britta Simon 使用 Azure AD 单一登录。
1. **[测试单一登录](#testing-single-sign-on)** - 验证配置是否正常工作。

### <a name="configuring-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，在 Azure 门户中启用 Azure AD 单一登录，并在 InsideView 应用程序中配置单一登录。

若要配置 InsideView 的 Azure AD 单一登录，请执行以下步骤：

1. 在 Azure 门户中的 InsideView 应用程序集成页上，单击“单一登录”。

    ![配置单一登录][4]

1. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。
 
    ![配置单一登录](./media/insideview-tutorial/tutorial_insideview_samlbase.png)

1. 在“InsideView 域和 URL”部分中，执行以下步骤：

    ![配置单一登录](./media/insideview-tutorial/tutorial_insideview_url.png)
    
    在 **“回复 URL”** 文本框中，使用以下模式键入 URL：`https://my.insideview.com/iv/<STS Name>/login.iv`

    > [!NOTE] 
    > 此值不是真实值。 请使用实际回复 URL 更新此值。 请联系[InsideView 支持团队](mailto:support@insideview.com)获取此值。
 
1. 在“SAML 签名证书”部分中，单击“证书(原始)”，并在计算机上保存证书文件。

    ![配置单一登录](./media/insideview-tutorial/tutorial_insideview_certificate.png) 

1. 单击“保存”按钮。

    ![配置单一登录](./media/insideview-tutorial/tutorial_general_400.png)

1. 在“InsideView 配置”部分中，单击“配置 InsideView”打开“配置登录”窗口。 从“快速参考”部分中复制“SAML 单一登录服务 URL”

    ![配置单一登录](./media/insideview-tutorial/tutorial_insideview_configure.png) 

1. 在另一个 Web 浏览器窗口中，以管理员身份登录到 InsideView 公司站点。

1. 在顶部工具栏中，依次单击“管理”、“单一登录设置”、“添加 SAML”。
   
   ![SAML 单一登录设置](./media/insideview-tutorial/ic794135.png "SAML Single Sign On Settings")

1. 在“添加新 SAML”部分中，执行以下步骤：

    ![添加新 SAML](./media/insideview-tutorial/ic794136.png "Add a New SAML")
   
    a. 在“STS 名称”文本框中，键入配置名称。

    b. 在“SamlP/WS-Fed 未经请求的终结点”文本框中，粘贴从 Azure 门户复制的“SAML 单一登录服务 URL”值 ****。
    
    c. 打开从 Azure 门户中下载的 base-64 编码证书，将其内容复制到剪贴板，然后再粘贴到“STS 证书”文本框中。

    d. 在“Crm 用户 ID 映射”文本框中，键入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。
        
    e. 在“Crm 电子邮件映射”文本框中，键入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。

    f. 在“Crm 名字映射”文本框中，键入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`。
    
    g. 在“Crm 姓氏映射”文本框中，键入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`。  

    h.如果该值不存在，请单击“添加行”。 单击“保存” 。

> [!TIP]
> 之后在设置应用时，就可以在 [Azure 门户](https://portal.azure.com)中阅读这些说明的简明版本了！  从“Active Directory”>“企业应用程序”部分添加此应用后，只需单击“单一登录”选项卡，即可通过底部的“配置”部分访问嵌入式文档。 可在此处阅读有关嵌入式文档功能的详细信息：[Azure AD 嵌入式文档]( https://go.microsoft.com/fwlink/?linkid=845985)
> 
 
### <a name="creating-an-azure-ad-test-user"></a>创建 Azure AD 测试用户
本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

![创建 Azure AD 用户][100]

**若要在 Azure AD 中创建测试用户，请执行以下步骤：**

1. 在 **Azure 门户**的左侧导航窗格中，单击“Azure Active Directory”图标。

    ![创建 Azure AD 测试用户](./media/insideview-tutorial/create_aaduser_01.png) 

1. 若要显示用户列表，请转到“用户和组”，单击“所有用户”。
    
    ![创建 Azure AD 测试用户](./media/insideview-tutorial/create_aaduser_02.png) 

1. 若要打开“用户”对话框，请在对话框顶部单击“添加”。
 
    ![创建 Azure AD 测试用户](./media/insideview-tutorial/create_aaduser_03.png) 

1. 在“用户”对话框页上，执行以下步骤：
 
    ![创建 Azure AD 测试用户](./media/insideview-tutorial/create_aaduser_04.png) 

    a. 在“名称”文本框中，键入 **BrittaSimon**。

    b. 在“用户名”文本框中，键入 BrittaSimon 的“电子邮件地址”。

    c. 选择“显示密码”并记下“密码”的值。

    d. 单击**创建**。
 
### <a name="creating-an-insideview-test-user"></a>创建 InsideView 测试用户

要使 Azure AD 用户能够登录 InsideView，必须将这些用户预配到 InsideView 中。 对于 InsideView，预配是一项手动任务。

若要获取在 InsideView 中创建的用户或联系人，请联系 [InsideView 支持团队](mailto:support@insideview.com)。

>[!NOTE]
>可以使用 InsideView 提供的任何其他 InsideView 用户帐户创建工具或 API 来预配 Azure AD 用户帐户。

### <a name="assigning-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过授予 Britta Simon 访问 InsideView 的权限，允许其使用 Azure 单一登录。

![分配用户][200] 

若要将 Britta Simon 分配到 InsideView，请执行以下步骤：

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201] 

1. 在应用程序列表中，选择“InsideView”。

    ![配置单一登录](./media/insideview-tutorial/tutorial_insideview_app.png) 

1. 在左侧菜单中，单击“用户和组”。

    ![分配用户][202] 

1. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![分配用户][203]

1. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

1. 在“用户和组”对话框中单击“选择”按钮。

1. 在“添加分配”对话框中单击“分配”按钮。
    
### <a name="testing-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

单击访问面板中的 InsideView 磁贴时，用户自动登录到 InsideView 应用程序。

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [Azure Active Directory 的应用程序访问与单一登录是什么？](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/insideview-tutorial/tutorial_general_01.png
[2]: ./media/insideview-tutorial/tutorial_general_02.png
[3]: ./media/insideview-tutorial/tutorial_general_03.png
[4]: ./media/insideview-tutorial/tutorial_general_04.png

[100]: ./media/insideview-tutorial/tutorial_general_100.png

[200]: ./media/insideview-tutorial/tutorial_general_200.png
[201]: ./media/insideview-tutorial/tutorial_general_201.png
[202]: ./media/insideview-tutorial/tutorial_general_202.png
[203]: ./media/insideview-tutorial/tutorial_general_203.png
