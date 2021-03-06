---
title: 教程：Azure Active Directory 与 Tableau Online 集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 和 Tableau Online 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: bd5e3087c21908600be9cd369a15f3036e5acb2f
ms.sourcegitcommit: a60a55278f645f5d6cda95bcf9895441ade04629
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2019
ms.locfileid: "58884697"
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a>教程：Azure Active Directory 与 Tableau Online 集成

在本教程中，了解如何将 Tableau Online 与 Azure Active Directory (Azure AD) 集成。

将 Tableau Online 与 Azure AD 集成提供以下优势：

- 可在 Azure AD 中控制谁有权访问 Tableau Online
- 可以让用户使用其 Azure AD 帐户自动登录到 Tableau Online（单一登录）
- 可以在一个中心位置（即 Azure 门户）管理帐户

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>必备组件

若要配置 Azure AD 与 Tableau Online 的集成，需要以下项：

- Azure AD 订阅
- 已启用 Tableau Online 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以在[此处](https://azure.microsoft.com/pricing/free-trial/)获取一个月的试用版。

## <a name="scenario-description"></a>方案描述
在本教程中，会在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 Tableau Online
1. 配置和测试 Azure AD 单一登录

## <a name="adding-tableau-online-from-the-gallery"></a>从库中添加 Tableau Online
要配置 Tableau Online 与 Azure AD 的集成，需要从库中将 Tableau Online 添加到托管 SaaS 应用列表。

**若要从库中添加 Tableau Online，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![Active Directory][1]

1. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![应用程序][2]
    
1. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![应用程序][3]

1. 在搜索框中，键入“Tableau Online”。

    ![创建 Azure AD 测试用户](./media/tableauonline-tutorial/tutorial_tableauonline_search.png)

1. 在结果面板中，选择“Tableau Online”，然后单击“添加”按钮添加该应用程序。

    ![创建 Azure AD 测试用户](./media/tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录
在本部分中，将基于名为“Britta Simon”的测试用户配置和测试 Tableau Online 的 Azure AD 单一登录。

若要运行单一登录，Azure AD 需要知道与 Azure AD 用户相对应的 Tableau Online 用户。 换句话说，需要在 Azure AD 用户与 Tableau Online 中相关用户之间建立链接关系。

可通过将 Azure AD 中“用户名”的值指定为 Tableau Online 中“用户名”的值来建立此链接关系。

若要配置和测试 Tableau Online 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configuring-azure-ad-single-sign-on)** - 让用户使用此功能。
1. **[创建 Azure AD 测试用户](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
1. **[创建 Tableau Online 测试用户](#creating-a-tableau-online-test-user)** - 在 Tableau Online 中创建 Britta Simon 的对应用户，并将其链接到该用户的 Azure AD 表示形式。
1. **[分配 Azure AD 测试用户](#assigning-the-azure-ad-test-user)** - 让 Britta Simon 使用 Azure AD 单一登录。
1. **[测试单一登录](#testing-single-sign-on)** - 验证配置是否正常工作。

### <a name="configuring-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录，并在 Tableau Online 应用程序中配置单一登录。

**若要配置 Azure AD 单一登录 Tableau Online，请执行以下步骤：**

1. 在 Azure 门户中的“Tableau Online”应用程序集成页上，单击“单一登录”。

    ![配置单一登录][4]

1. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。
 
    ![配置单一登录](./media/tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

1. 在“Tableau Online 域和 URL”部分中，执行以下步骤：

    ![配置单一登录](./media/tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    a. 在“登录 URL”文本框中，键入 URL： `https://sso.online.tableau.com`

    b. 在“标识符”文本框中，键入 URL： `https://sso.online.tableau.com/public/sp/metadata?alias=<entityid>`

1. 在“SAML 签名证书”部分中，单击“元数据 XML”，并在计算机上保存元数据文件。

    ![配置单一登录](./media/tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

1. 单击“保存”按钮。

    ![配置单一登录](./media/tableauonline-tutorial/tutorial_general_400.png)

1. 在另一个浏览器窗口中，登录 Tableau Online 应用程序。 转到“设置”，然后到“身份验证”。
   
    ![配置单一登录](./media/tableauonline-tutorial/tutorial_tableauonline_09.png)
    
1. 若要启用 SAML，请在“身份验证类型”部分下， 选中“使用 SAML 单一登录”复选框。
   
    ![配置单一登录](./media/tableauonline-tutorial/tutorial_tableauonline_12.png)

1. 向下滚动到“将元数据文件导入 Tableau Online”部分。  单击“浏览”并导入已从 Azure AD 下载的元数据文件。 然后，单击“应用”。
   
   ![配置单一登录](./media/tableauonline-tutorial/tutorial_tableauonline_13.png)

1. 在“匹配断言”部分中，为**电子邮件地址**、**名字**和**姓氏**插入相应的标识提供者断言名称。 若要从 Azure AD 中获取此信息，请执行以下操作： 
  
    a. 在 Azure 门户中，转到“Tableau Online”应用程序集成页。
    
    b. 在“属性”部分中，选中“查看和编辑所有其他用户属性”复选框。 
    
   ![配置单一登录](./media/tableauonline-tutorial/attributesection.png)
      
    c. 通过执行以下步骤复制以下属性的命名空间值：givenname、email 和 surname：

   ![Azure AD 单一登录](./media/tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    d. 单击“user.givenname”值 
    
    e. 从“命名空间”文本框复制值。

   ![配置单一登录](./media/tableauonline-tutorial/attributesection2.png)

    f. 若要复制 email 和 surname 的命名空间值，请按照前面的步骤进行操作。

    g. 切换到 Tableau Online 应用程序，然后设置“Tableau Online 属性”部分，如下所示：
     * 电子邮件：**mail** 或 **userprincipalname**
     * 名字：**givenname**
     * 姓氏：**surname**
   
   ![配置单一登录](./media/tableauonline-tutorial/tutorial_tableauonline_14.png)

### <a name="creating-an-azure-ad-test-user"></a>创建 Azure AD 测试用户
本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

![创建 Azure AD 用户][100]

**若要在 Azure AD 中创建的测试用户，请执行以下步骤：**

1. 在 **Azure 门户**的左侧导航窗格中，单击“Azure Active Directory”图标。

    ![创建 Azure AD 测试用户](./media/tableauonline-tutorial/create_aaduser_01.png) 

1. 若要显示用户列表，请转到“用户和组”，单击“所有用户”。
    
    ![创建 Azure AD 测试用户](./media/tableauonline-tutorial/create_aaduser_02.png) 

1. 若要打开“用户”对话框，请在对话框顶部单击“添加”。
 
    ![创建 Azure AD 测试用户](./media/tableauonline-tutorial/create_aaduser_03.png) 

1. 在“用户”对话框页上，执行以下步骤：
 
    ![创建 Azure AD 测试用户](./media/tableauonline-tutorial/create_aaduser_04.png) 

    a. 在“名称”文本框中，键入 **BrittaSimon**。

    b. 在“用户名”文本框中，键入 BrittaSimon 的“电子邮件地址”。

    c. 选择“显示密码”并记下“密码”的值。

    d. 单击“创建”。
 
### <a name="creating-a-tableau-online-test-user"></a>创建 Tableau Online 测试用户

在本部分中，会在 Tableau Online 中创建一个名为“Britta Simon”的用户。

1. 在“Tableau Online”上，单击“设置”，然后单击“身份验证”部分。 向下滚动到“选择用户”部分。 依次单击“添加用户”、“输入电子邮件地址”。
   
    ![创建 Azure AD 测试用户](./media/tableauonline-tutorial/tutorial_tableauonline_15.png)
1. 选择“添加要进行单一登录(SSO)身份验证的用户”。 在“输入电子邮件地址”文本框中添加 britta.simon@contoso.com
   
    ![创建 Azure AD 测试用户](./media/tableauonline-tutorial/tutorial_tableauonline_11.png)
1. 单击“创建”。

### <a name="assigning-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过授予 Britta Simon 访问 Tableau Online 的权限，允许她使用 Azure 单一登录。

![分配用户][200] 

**若要将 Britta Simon 分配到 Tableau Online，请执行以下步骤：**

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201] 

1. 在应用程序列表中，选择“Tableau Online”。

    ![配置单一登录](./media/tableauonline-tutorial/tutorial_tableauonline_app.png) 

1. 在左侧菜单中，单击“用户和组”。

    ![分配用户][202] 

1. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![分配用户][203]

1. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

1. 在“用户和组”对话框中单击“选择”按钮。

1. 在“添加分配”对话框中单击“分配”按钮。
    
### <a name="testing-single-sign-on"></a>测试单一登录

本部分旨在使用“访问面板”测试 Azure AD SSO 配置。

单击访问面板中的“Tableau Online”磁贴时，用户应自动登录到 Tableau Online 应用程序。

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [Azure Active Directory 的应用程序访问与单一登录是什么？](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/tableauonline-tutorial/tutorial_general_203.png
