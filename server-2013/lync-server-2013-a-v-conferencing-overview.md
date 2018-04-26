﻿---
title: Lync Server 2013 中的 A/V 会议概述
TOCTitle: Lync Server 2013 中的 A/V 会议概述
ms:assetid: 9583de87-4618-4a99-a47a-45e8cc4cc221
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ619186(v=OCS.15)
ms:contentKeyID: 49313640
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 A/V 会议概述

 

_**上一次修改主题：** 2016-12-08_

A/V 会议支持用户之间的实时音频和视频通信。在部署会议时，可以选择同时启用并使用 Web 会议和 A/V 会议，也可以仅启用并使用 Web 会议。

要规划 A/V 会议，需了解组织所需会议媒体类型要求的网络带宽。这包含音频、视频和全景视频。

允许用户参加 A/V 会议之前，请确保网络可以处理生成的负载。如果网络带宽不足，用户体验可能大打折扣。您可以使用呼叫允许控制 (CAC) 管理 A/V 会议使用的网络带宽。这对受限网络（例如中央站点和分支站点之间的受限带宽链接）很重要。有关详细信息，请参阅 [Lync Server 2013 中的呼叫允许控制概述](lync-server-2013-overview-of-call-admission-control.md)。有关媒体带宽要求的详细信息，请参阅[Lync Server 2013 中的媒体流量的网络带宽要求](lync-server-2013-network-bandwidth-requirements-for-media-traffic.md)。

如果在网络中部署音频会议，则用户需要使用诸如耳麦之类的音频设备才能参加音频会议。如果部署视频会议，则需要部署诸如用户网络摄像机之类的视频设备。建议您使用由 Microsoft 针对所有设备类型认证的统一通信 (UC) 设备，以确保达到最佳的用户体验。有关 UC 认证的设备的详细信息，请参阅“适用于 Lync 的电话和设备”，网址为 [http://go.microsoft.com/fwlink/?linkid=263861\&clcid=0x804](http://go.microsoft.com/fwlink/?linkid=263861%26clcid=0x804)。对于音频或视频设备，设备部署和用户培训是要考虑和规划的重要步骤。

以下几节介绍了音频和视频会议的功能，其中包括有关管理带宽和选择适当的客户端的信息。

## 音频会议功能

Lync Server 2013 提供了可用于配置用户音频会议体验的几项功能，其中包括：

  - **受众静音**   演示者可使用此设置将会议中的所有音频参与者静音，并将会议置于某种状态以使非演示者无法自行取消静音。

  - **会议进入/退出通知**   如果已启用电话拨入式会议，演示者可使用此设置打开或关闭进入/退出通知以最大程度地减小会议进行中受到的干扰。

  - **通过拨出添加用户**   授予了权限的演示者和与会者可将 PSTN 号码添加到会议中并使会议拨出到这些号码。

## 视频会议功能

Lync Server 2013 提供了可用于配置用户视频会议体验的几项功能，其中包括：

  - **库视图**   在超过两名与会者的视频会议中，用户会自动看到会议中的每一名与会者。如果与会者超过五名，那么最活跃与会者的视频将显示在最上面一行，并仅对其他与会者显示照片。默认情况下，已启用多方视频。有关配置或禁用多方视频的详细信息，请参阅[在 Lync Server 2013 中配置视频带宽](lync-server-2013-configuring-video-bandwidth.md)。

  - **全景视频**   如果在会议室中安装了 RoundTable 视频会议设备，则此功能可提供会议室的 360 度全景。全景视频带只能用于 RoundTable 设备。

  - **仅演示者视频模式**   演示者可以对会议进行配置，以仅显示来自演示者的视频。如果提供了多个视频流并锁定到不同的源，这可阻止大型会议受到干扰。此模式还适用于由 RoundTable 设备捕获和提供的视频。

  - **高清视频**   用户可在双方呼叫和多方会议中体验最高为高清 1080P 的分辨率。

  - **视频聚焦**   演示者可以对会议进行配置，以使会议中的其他参与者仅看到由作为视频源的选定参与者提供的视频。此模式还适用于由 RoundTable 设备针对全景视频捕获和提供的视频。
