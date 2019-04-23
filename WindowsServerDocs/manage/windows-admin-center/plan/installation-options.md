---
title: Welche Art von Installation für Sie geeignet ist.
description: Welche Art von Installation für Sie Windows Admin Center (Projekt Honolulu) geeignet ist. Installieren Sie auf einem Failovercluster für hohe Verfügbarkeit und resilienz.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fae0305e454cdd10109219c6182ff612f539e9c9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868011"
---
# <a name="what-type-of-installation-is-right-for-you"></a>Welche Art von Installation ist für Sie geeignet?

>Gilt für: Windows Admin Center, Windows Admin Center Preview

## <a name="supported-operating-systems-installation"></a>Unterstützte Betriebssysteme: Installation

Sie können **installieren** Windows Admin Center auf den folgenden Windows-Betriebssystemen unterstützt:

| **Version** | **Installationsmodus** |
|-------------|-----------------------|
|Windows 10, Version 1709 oder höher | Desktopmodus |
|Windows Server (Semi-Annual Channel) | Gatewaymodus |
|Windows Server 2016 | Gatewaymodus |
|Windows Server 2019 | Gatewaymodus |

**Desktop-Modus:** Über das Startmenü starten und eine Verbindung des Gateways Windows Admin Center aus dem gleichen Computer, auf dem er installiert ist (d. h. `https://localhost:6516`)

**Gateway-Modus:** Ein Browser auf einem anderen Computer eine Verbindung mit dem Gateway Windows Admin Center (d. h. `https://servername.contoso.com`) 

> [!WARNING]
> Installieren von Windows Admin Center auf einem Domänencontroller wird nicht unterstützt. [Erfahren Sie mehr über die Sicherheit des Domänencontrollers, bewährte Methoden](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack). 

> [!IMPORTANT]
> Nicht möglich, verwenden Sie Internet Explorer zum Verwalten von Windows Admin Center – stattdessen müssen Sie verwenden eine [unterstützten Browser](../understand/faq.md#which-web-browsers-are-supported-by-windows-admin-center
).  Bei der Installation von Windows Admin Center unter Windows Server wird empfohlen, beim Herstellen einer Remoteverbindung mit Windows 10 und Edge verwalten.  Alternativ können Sie lokal unter Windows Server verwalten, wenn Sie einen unterstützten Browser installiert haben.

## <a name="supported-operating-systems-management"></a>Unterstützte Betriebssysteme: Management

Sie können **verwalten** die folgenden Windows-Betriebssysteme mit Windows Admin Center:

| Version | Verwalten von *Knoten* über *Server-Manager* | Verwalten von *Cluster* über *Failovercluster-Manager* | Verwalten von *HCI* über *HCI-Cluster-Manager*|
|-------------------------|---------------|-----|------------------------|
| Windows 10, Version 1709 oder höher | Ja (über die Computerverwaltung) | Nicht zutreffend | Nicht zutreffend |
| Windows Server (Semi-Annual Channel) | Ja | Ja | Nicht zutreffend |
| Windows Server 2019 | Ja | Ja | Ja |
| Windows Server 2016 | Ja | Ja | Ja, mit [– neuestes Kumulatives Update](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) |
| Microsoft Hyper-V Server 2016 | Ja | Ja | Nicht zutreffend |
| Windows Server 2012 R2 | Ja | Ja | Nicht zutreffend |
| Microsoft Hyper-V Server 2012 R2 | Ja | Ja | Nicht zutreffend |
| Windows Server 2012 | Ja | Ja | Nicht zutreffend |
| Windows Server 2008 R2 | Ja, begrenzte Funktionalität | Nicht zutreffend | Nicht zutreffend |

> [!NOTE]
> Windows Admin Center erfordert PowerShell-Funktionen, die nicht in Windows Server 2008 R2, 2012 und 2012 R2 enthalten sind. Wenn Sie diese mit Windows Admin Center verwalten, müssen Sie Windows Management Framework (WMF) Version 5.1 oder höher auf diesen Servern installieren.

>Geben Sie `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder einen neuere Version installiert ist. 

>Wenn WMF nicht installiert ist, können Sie [Herunterladen von WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616).

## <a name="deployment-options"></a>Bereitstellungsoptionen

| ![img](../media/deployment-options/W10.png) | ![img](../media/deployment-options/gateway.png) | ![img](../media/deployment-options/node.png) | ![img](../media/deployment-options/HA.png) |
|---|---|---|---|

| Lokaler Client | Gatewayserver | Verwalteter Server | Failovercluster |
| --- | --- | --- | --- |
| Installieren Sie auf einem lokalen Windows 10-Client, der eine Verbindung mit den verwalteten Servern verfügt.  Hervorragend geeignet für den schnellen Einstieg und Ad-hoc- oder kleinen Szenarien testen. |Auf einem designierten Gateway-Server installieren und über einen beliebigen Clientbrowser mit der Konnektivität mit dem Gatewayserver zugreifen.  Hervorragend geeignet für umfangreiche Szenarien. | Installieren Sie direkt auf einem verwalteten Server zum Verwalten von sich selbst oder auf einem Cluster, in dem ein Elementknoten ist.  Hervorragend geeignet für verteilten Szenarien. | Bereitstellen Sie in einem Failovercluster, um hohe Verfügbarkeit des Gateway-Diensts zu aktivieren. Hervorragend geeignet für produktionsumgebungen auf die Gewährleistung der resilienz von den Management-Dienst. |

## <a name="high-availability"></a>Hohe Verfügbarkeit

Sie können die hohe Verfügbarkeit des Gatewaydiensts aktivieren, durch die Bereitstellung von Windows Admin Center in einem Aktiv / Passiv-Modell in einem Failovercluster installieren. Wenn einer der Knoten im Cluster ausfällt, ein Windows Admin Center ordnungsgemäß Failover auf einen anderen Knoten können Sie weiterhin die Server in Ihrer Umgebung problemlos verwalten.

[Erfahren Sie, wie Windows Admin Center mit hochverfügbarkeit bereitstellen.](../deploy/high-availability.md)

> [!Tip]
> Sind Sie bereit zum Installieren von Windows Admin Center? [Jetzt herunterladen](https://aka.ms/windowsadmincenter)
