﻿---
title: Lync Server 2013 企业语音
TOCTitle: 企业语音
ms:assetid: c9da8099-6f4f-4346-ac67-f041bb96072c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg417163(v=OCS.15)
ms:contentKeyID: 49314230
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的企业语音

 

_**上一次修改主题：** 2015-04-08_

通过企业语音， Lync Server 可提供用于增强或替代传统 PBX 系统的独立 IP 语音 (VoIP) 服务。企业语音用户可以呼叫组织的 VoIP 网络或 PBX 中的同事，也可以呼叫组织外的传统电话号码。企业语音解决方案包括常见呼叫功能，如应答、转接、转移、保持、释放和寄存，以及增强型 9-1-1 呼叫。（增强型 9-1-1 仅限在美国使用。）企业语音还支持各种当前和以前型号的 IP 和 USB 设备。

## 发起和接收呼叫

使用 Lync，用户可以通过在键盘上键入名称或电话号码或者使用屏幕中显示的拨号盘来发起呼叫。用户还可以直接从联系人列表中发起呼叫。您也可以部署 Lync Phone Edition 设备，即由 Microsoft 合作伙伴提供的独立 IP 电话设备。

用户可以在 Lync Server 中注册多个电话设备，并可以轻松地在这些设备之间进行切换。

来电时将同时在用户的所有设备上通知用户，IP 电话设备上将播放可自定义的铃声，PC 上将显示类似即时消息的通知。

用户还可以设置与桌面电话、PC 和移动电话连接的单个电话号码，以便能够随时随地接听电话。

## 基本呼叫功能

在通话过程中，用户可以应答其他传入呼叫或发起传出呼叫，现有的活动呼叫将自动置于保持状态。可以直接或在第一个用户与第二个用户私下通话后，将呼叫从一个用户转接至另一个用户。用户还可以将呼叫转接至其他设备；例如，用户在办公室外接听电话时可以将活动呼叫转接至移动电话。

## 更丰富的通信

使用 Lync 与其他用户通话时，用户可以轻松地在呼叫中添加文本、视频或桌面共享。在 Lync 中，状态设置集成了“请勿打扰”功能。

使用 Exchange 统一消息 (UM)，Lync 和 Lync Server 与 Microsoft Exchange Server 2013 和 Microsoft Outlook 2013 集成。用户可以在 Lync 窗口和电子邮件中查看他们是否有新的语音邮件。在电子邮件中，用户可以通过单击播放电子邮件中的语音邮件音频，或查看语音邮件的脚本。

## 高级呼叫功能

企业语音还包括多个高级呼叫功能，如委派、团队呼叫、组内呼叫应答和响应组。

通过委派，用户可以委派一个或多个助理来处理呼叫。代理人可以代表用户执行多项呼叫任务，包括筛选呼叫、发起呼叫和发起会议。

通过团队呼叫，用户可以让来电同时进入队友的电话，以便团队中的任何人都可以应答该呼叫。

组内呼叫应答是 2013 年 2 月版 Lync Server 2013 累积更新中的一项新功能，它允许用户从其自己的电话接听打给其同事的电话。组内呼叫应答本质上不同于团队呼叫，因为来电仅进入预期接听人的电话，但任何其他用户均可通过拨打应答分组号码来选择接听该来电。

可以对响应组进行设置，以便将呼叫排队并智能路由至指定的代理。常见用途包括 IT 技术支持、人力资源热线和其他内部联络中心。

## 企业语音管理

Lync Server 使用标准和发布的接口与现有基础结构进行互操作。它支持用于与 IP PBX 系统和 PSTN 网络进行互联的网关和 SIP 选项（如 SIP 中继），以便以后可以将用户迁移至企业语音，同时最大限度地减少中断。 Lync Server 支持用于与传统 VoIP 解决方案进行互操作的传统编解码器，如 G.711、G.722 和 G.723.1。

通过呼叫允许控制 (CAC)，管理员可以限制受限网络链接中的 Lync Server 语音和视频流量，并指定在新呼叫超出限制时将采取的操作。这些操作包括使用备用路径路由或拒绝呼叫。

Lync Server 与第三方 Survivable Branch Appliance 相互协作，在中央站点中发生 WAN 故障时为分支机构提供本地呼叫服务和 PSTN 连接。

