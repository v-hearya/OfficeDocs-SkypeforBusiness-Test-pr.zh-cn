﻿---
title: 创建新的 Web 服务配置设置
TOCTitle: 创建新的 Web 服务配置设置
ms:assetid: f3f04d81-8a1f-427f-bd0f-fb659024e096
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg182605(v=OCS.15)
ms:contentKeyID: 49314731
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 创建新的 Web 服务配置设置

 

_**上一次修改主题：** 2012-11-01_

可以使用“Web 服务”页配置用于访问与 Lync Server 2013 相关的 Web 服务器和 Web 服务的身份验证方法。

按照以下步骤创建新的 Web 服务策略。

## 创建 Web 服务策略

1.  使用 RTCUniversalServerAdmins 组成员（或具有同等用户权限）的用户帐户，或分配给 CsServerAdministrator 或 CsAdministrator 角色的用户帐户，登录到网络中部署了 Lync Server 2013 的任何计算机。

2.  打开浏览器窗口，然后输入管理 URL 以打开 Lync Server 控制面板。有关可以用于启动 Lync Server 控制面板的不同方法的详细信息，请参阅[打开 Lync Server 管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左侧导航栏中，单击“安全性”，然后单击“Web 服务”。

4.  在“Web 服务”页上，单击“新建”，然后执行下列操作之一：
    
      - 要配置站点的 Web 服务，请单击“站点配置”。在“选择站点”中，单击将应用此 Web 服务策略的站点，然后单击“确定”。
    
      - 要配置池的 Web 服务，请单击“池配置”。在“选择服务”中，单击将应用此 Web 服务策略的服务，然后单击“确定”。

5.  在“新建 Web 服务设置”的“集成的 Windows 身份验证”中，选择“协商”、“集成的 Windows 身份验证”或“无”。

6.  根据环境中的客户端功能和支持情况，选择下列一项或多项：
    
      - **启用 PIN 身份验证**，允许使用 PIN 号对客户端进行身份验证。
    
      - **启用证书身份验证**，可使池中的服务器向客户端颁发证书。
    
      - **启用证书链下载**，让具有身份验证证书的服务器下载该证书的证书链。

7.  单击“提交”。

