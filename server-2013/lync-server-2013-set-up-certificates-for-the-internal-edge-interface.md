﻿---
title: Lync Server 2013：为内部边缘接口设置证书
TOCTitle: 为内部边缘接口设置证书
ms:assetid: a1963cc9-87c5-4935-86c0-6bedc6afd0ac
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg412750(v=OCS.15)
ms:contentKeyID: 49313788
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中为内部边缘接口设置证书

 

_**上一次修改主题：** 2013-11-07_

> [!IMPORTANT]
> 在运行证书向导时，请确保您使用作为组（已为其分配您将使用的证书模板类型的适当权限）的成员的帐户进行登录。默认情况下， Lync Server 2013 证书请求将使用 Web 服务器证书模板。如果您使用作为 RTCUniversalServerAdmins 组的成员的帐户来通过此模板请求证书，请确保已为该组分配使用此模板所需的注册权限。


每台边缘服务器的内部接口都需要一个证书。内部接口的证书可以由内部企业证书颁发机构 (CA) 或公共 CA 颁发。如果组织已部署内部 CA，则通过使用内部 CA 为内部接口颁发证书可以节省使用公用证书的开支。可以使用内部 Windows Server 2008 CA 或 Windows Server 2008 R2 CA 创建这些证书。

有关证书的这一要求以及其他要求的详细信息，请参阅[Lync Server 2013 中外部用户访问的证书要求](lync-server-2013-certificate-requirements-for-external-user-access.md)。

要设置某个站点的内部边缘接口上的证书，请使用本节中的过程执行以下操作：

1.  将内部接口的 CA 证书链下载到每台边缘服务器。

2.  在每台边缘服务器上为内部接口导入 CA 证书链。

3.  在一台边缘服务器（称为第一台边缘服务器）上为内部接口创建证书请求。

4.  在第一台边缘服务器上为内部接口导入证书。

5.  在此站点（或部署在此负载平衡器之后）的其他边缘服务器上导入该证书。

6.  为每台边缘服务器的内部接口分配证书。

如果多个站点都有边缘服务器（即多站点边缘拓扑），或不同组的边缘服务器部署在不同的负载平衡器之后，则需要按照上述步骤对每个有边缘服务器的站点以及每组部署在不同负载平衡器之后的边缘服务器进行操作。

> [!NOTE]  
> 本节中这些过程的步骤是以使用 Windows Server 2008 CA、Windows Server 2008 R2 CA、Windows Server 2012 CA 或 Windows Server 2012 R2 CA 为每台边缘服务器创建证书为前提的。有关任何其他 CA 的分步指南，请参考该 CA 的文档。默认情况下，所有通过身份验证的用户都具有请求证书的适当用户权限。<br />
本节中的过程是以在部署边缘服务器的过程中在边缘服务器上创建证书请求为前提的。可以使用前端服务器创建证书请求。可以在开始部署边缘服务器之前执行此操作，以在规划和部署过程早期完成证书请求。为此，必须确保请求的证书是使用可导出的私钥定义的。<br />
本节中的过程介绍使用 .cer 和 .p7b 文件作为证书。如果使用其他类型的文件，请根据需要修改这些过程。



## 使用 certsrv 网站为内部接口下载 CA 证书链

1.  以 **Administrators** 组的成员身份登录到内部网络中的 Lync Server 2013 服务器（即非边缘服务器）。

2.  在命令提示符下运行以下命令，方法是单击“开始”，再单击“运行”，然后键入以下命令：
    
        https://<name of your Issuing CA Server>/certsrv
    
    例如：
    
        https://ca01.contoso.net/certsrv
    
    > [!NOTE]  
	> 如果您使用的是 Windows Server 2008 或 Windows Server 2008 R2 企业 CA，则必须使用 https，而非 http。
    


3.  在发证 CA 的 certsrv 网页上，在“选择任务”下，单击“下载 CA 证书、证书链或 CRL”。

4.  在“下载 CA 证书、证书链或 CRL”下，单击“下载 CA 证书链”。

5.  在“文件下载”对话框中，单击“保存”。

6.  将 .p7b 文件保存到服务器的硬盘上，然后将其复制到每台边缘服务器的文件夹中。
    
    > [!NOTE]  
	> .p7b 文件包含证书路径中的所有证书。若要查看证书路径，请打开服务器证书，然后单击证书路径。
    


## 使用 MMC 为内部接口下载 CA 证书链

1.  您可以使用 Microsoft 管理控制台 (MMC)从任何加入了域的计算机导出 CA 根证书。单击“开始”，单击“运行”，然后键入 **MMC**。

2.  在 MMC 控制台中，单击“文件”，再单击“添加/删除”。

3.  从“添加或删除管理单元”对话框列表中，选择“证书”，然后单击“添加”。系统提示时，选择“计算机帐户”。在“选择计算机”对话框中，选择“本地计算机”。单击“完成”。单击“确定”。

4.  展开“证书(本地计算机)”。展开“受信任的根证书颁发机构”，选择“证书”。

5.  单击由 CA 颁发的根证书。右键单击该证书，选择“所有任务”，选择“导出”。将打开“证书导出向导”。

6.  在“证书导出向导”中，单击“下一步”。

7.  打开“导出文件格式”对话框，选择要导出到的格式。建议选择“加密消息语法标准 – PKCS \#7 证书(.P7B)”。如果选择“加密消息语法标准 – PKCS \#7 证书(.P7B)”，则选择“如果可能，则数据包括证书路径中的所有证书”复选框来导出证书链，包括根 CA 证书和任何中间 CA 证书。单击“下一步”。

8.  在“要导出的文件”对话框的文件名条目中，为导出的证书键入路径和文件名（默认扩展名为 .p7b）。或者，也可以单击“浏览”，找到放置导出的证书的目录并为导出的证书提供名称。单击“保存”。单击“下一步”。

9.  查看操作摘要，然后单击“完成”以完成证书的导出。单击“确定”确认导出成功。

## 为内部接口导入 CA 证书链

1.  在每台边缘服务器上打开 Microsoft 管理控制台 (MMC)，方法是依次单击“开始”、“运行”，在“打开”框中键入 **mmc**，然后单击“确定”。

2.  在“文件”菜单上，单击“添加/删除管理单元”，然后单击“添加”。

3.  在“添加独立管理单元”框中，单击“证书”，然后单击“添加”。

4.  在“证书管理单元”对话框中，单击“计算机帐户”，然后单击“下一步”。

5.  在“选择计算机”对话框中，确保选中“本地计算机: (运行此控制台的计算机)”复选框，然后单击“完成”。

6.  单击“关闭”，然后单击“确定”。

7.  在控制台树中，展开“证书(本地计算机)”，右键单击“受信任的根证书颁发机构”，指向“所有任务”，然后单击“导入”。

8.  在向导的“要导入的文件”中，指定证书的文件名（即在前面过程中为内部接口下载 CA 证书链时指定的名称）。

9.  在每台边缘服务器上重复此过程。

## 为内部接口创建证书申请

1.  在其中一台边缘服务器上启动部署向导，然后单击“步骤 3: 请求、安装或分配证书”旁边的“运行”。
    
    > [!NOTE]  
	> 如果多台边缘服务器位于一个池中的同一个位置，则可以在任意一台边缘服务器上运行证书向导。<br />
    > 首次运行步骤 3 后，按钮会更改为“再次运行”，且只有在请求、安装和分配全部所需证书后，才会显示指示任务成功完成的绿色复选标记。
    


2.  在“可用的证书任务”页上，单击“创建新的证书请求”。

3.  在“证书请求”页上，单击“下一步”。

4.  在“延迟的请求或即时请求”页上，单击“现在准备请求，但稍后发送”。

5.  在“证书请求文件”页上，键入要向其保存请求的完整路径和文件名（例如，**c:\\cert\_internal\_edge.cer**）。

6.  在“指定替代证书模板”页上，要使用除默认 WebServer 模板之外的模板，请选中“使用选定证书颁发机构的备用证书模板”复选框。

7.  在“名称和安全设置”页上，执行以下操作：
    
      - 在“友好名称”中，键入证书的显示名称（例如，内部边缘）。
    
      - 在“位长度”中，指定位长度（通常为默认值“2048”）。
        
        > [!NOTE]  
		> 较高的位长度更为安全，但是会对速度产生负面影响。
        
    
      - 要使证书可以导出，请选中“将证书的私钥标记为可导出”复选框。

8.  在“组织信息”页上，键入组织名称和组织单位 (OU)（例如分部或部门）。

9.  在“地理信息”页上，指定位置信息。

10. 在“使用者名称/使用者替代名称”页上，将显示向导自动填充的信息。

11. 在“配置其他使用者替代名称”页上，指定所需的任何其他使用者替代名称。

12. 在“请求摘要”页上，检查要用于生成请求的证书信息。

13. 完成命令后，请执行以下操作：
    
      - 要查看证书请求的日志，请单击“查看日志”。
    
      - 要完成证书请求，请单击“下一步”。

14. 在“证书请求文件”页上，执行以下操作：
    
      - 要查看生成的证书签名请求 (CSR) 文件，请单击“查看”。
    
      - 要关闭向导，请单击“完成”。

15. 将此文件提交给 CA（通过电子邮件或组织对企业 CA 支持的其他方法），并在收到回复文件时将新证书复制到此计算机，以使该证书可供导入。

## 为内部接口导入证书

1.  以本地 Administrators 组成员的身份登录到在其上创建了证书请求的边缘服务器。

2.  在部署向导中，单击“步骤 3: 请求、安装或分配证书”旁边的“再次运行”。
    
    首次运行步骤 3 后，按钮会更改为“再次运行”，但只有在请求、安装和分配所有所需证书后，才会显示绿色复选标记（指示任务成功完成）。

3.  在“可用的证书任务”页上，单击“从 .P7b, .pfx 或 .cer 文件导入证书”。

4.  在“导入证书”页上，键入为此边缘服务器的内部接口请求并接收的证书的完整路径和文件名（或单击“浏览”找到并选择该证书）。

5.  如果要为池中的其他成员导入证书，且证书包含私钥，请选中“证书文件包含证书的私钥”复选框并指定密码。

## 为池中的边缘服务器导出包含私钥的证书

1.  以 Administrators 组成员的身份登录到导入了证书的同一台边缘服务器。

2.  依次单击“开始”和“运行”，再键入 **MMC**。

3.  从 MMC 控制台中，单击“文件”，再单击“添加/删除管理单元”。

4.  从“添加或删除管理单元”页中，单击“证书”，再单击“添加”。

5.  在“证书管理单元”对话框中，选择“计算机帐户”。单击“下一步”。在“选择计算机”中，选择“本地计算机: (运行此控制台的计算机)”。单击“完成”。单击“确定”完成对 MMC 控制台的配置。

6.  双击“证书(本地计算机)”扩展证书存储。双击“个人”，然后双击“证书”。
    
    > [!IMPORTANT]
    > 如果本地计算机的证书个人存储中没有证书，则表示未导入与证书关联的私钥。请检查请求和导入步骤。如果问题仍然存在，请联系您的证书颁发机构管理员或提供商。


7.  在本地计算机的证书个人存储中，右键单击要导出的证书。单击“所有任务”，再单击“导出”。

8.  在证书导出向导中，单击“下一步”。选择“是，导出私钥”。单击“下一步”。
    
    > [!NOTE]  
	> 如果“是，导出私钥”选择不可用，则没有将与该证书关联的私钥标记为导出。您将需要再次请求该证书，并确保该证书已标记为允许导出私钥，然后您才能继续导出操作。请与您的证书颁发机构管理员或提供商联系。
    


9.  在“导出文件格式”对话框中，选择“个人信息交换 - PKCS \#12 (.PFX)”，然后选择以下选项：
    
      - 如果可能，则数据包括证书路径中的所有证书
    
      - 导出所有扩展属性
        
        > [!WARNING]  
		> 从边缘服务器导出证书时，请勿选择“如果导出成功，删除私钥”。如果选择此选项，您将需要将证书和私钥导入到此边缘服务器。
    
    单击“下一步”继续。

10. 如果要分配密码以保护私钥，则键入私钥的密码。重新输入该密码以进行确认。单击“下一步”。

11. 为导出的证书键入路径和文件名，并使用文件扩展名 .pfx。该路径必须可由池中的所有其他边缘服务器访问，或者可通过可移动媒体（例如，USB 闪存驱动器）传输。单击“下一步”。

12. 查看“正在完成证书导出向导”对话框中的摘要。单击“完成”。

13. 在成功导出对话框中单击“确定”。

14. 按照 [为 Lync Server 2013 的外部边缘接口设置证书](lync-server-2013-set-up-certificates-for-the-external-edge-interface.md)过程中所述的步骤进行操作，将导出的证书文件导入其他边缘服务器中。

## 在边缘服务器上分配内部证书

1.  对于每台边缘服务器，在部署向导中，单击“步骤 3: 请求、安装或分配证书”旁边的“再次运行”。

2.  在“可用的证书任务”页上，单击“分配现有证书”。

3.  在“证书分配”页上，选择列表中的“边缘内部”。

4.  在“证书存储”页上，选择为内部边缘导入的证书（在前面过程中）。

5.  在“证书分配摘要”页上，检查设置，然后单击“下一步”以分配证书。

6.  在向导完成页上，单击“完成”。

7.  使用此过程分配内部边缘证书后，在每台服务器上打开“证书”管理单元，依次展开“证书(本地计算机)”、“个人”，单击“证书”，然后确认详细信息窗格中是否列出了内部边缘证书。

8.  如果部署中包含多台边缘服务器，请对每台边缘服务器重复此过程。

