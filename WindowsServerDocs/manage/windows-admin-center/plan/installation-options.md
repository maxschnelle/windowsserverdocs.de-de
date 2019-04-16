---
title: Welche Art von Installation für Sie geeignet ist.
description: Dieses Thema beschreibt die verschiedenen Optionen für Windows Admin Center, einschließlich der Installation auf einem Windows 10-PC oder einem Windows-Server für die Verwendung durch mehrere Administratoren.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 04/12/2019
ms.openlocfilehash: cc6f9e6c2f2572618c1c5fdae00047d24fbeb3cf
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296662"
---
# Welche Art von Installation ist für Sie geeignet?

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Dieses Thema beschreibt die verschiedenen Optionen für Windows Admin Center, einschließlich der Installation auf einem Windows 10-PC oder einem Windows-Server für die Verwendung durch mehrere Administratoren. Zum Installieren von Windows Admin Center auf einem virtuellen Computer in Azure finden Sie unter " [Bereitstellen von Windows Admin Center in Azure](../azure/deploy-wac-in-azure.md)".

## Unterstützte Betriebssysteme: Installation

Sie können Windows Admin Center auf den folgenden Windows-Betriebssystemen **Installieren** :

| **Version** | **Installationsmodus** |
|-------------|-----------------------|
|Windows 10, Version 1709 oder höher | Desktopmodus |
|Windows Server (Semi-Annual Channel) | Gatewaymodus |
|Windows Server 2016 | Gatewaymodus |
|Windows Server 2019 | Gatewaymodus |

**Desktopmodus:** Starten Sie aus dem Menü "Start", und Verbinden mit dem Windows Admin Center-Gateway über denselben Computer, auf dem es installiert ist (d. h. `https://localhost:6516`)

**Gatewaymodus:** Verbinden mit dem Windows Admin Center-Gateway von einem Clientbrowser auf einem anderen Computer (d. h. `https://servername.contoso.com`) 

> [!WARNING]
> Installieren von Windows Admin Center auf einem Domänencontroller wird nicht unterstützt. [Weitere Informationen zu Domain Controller Bewährte Sicherheitsmethoden lesen](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack). 

> [!IMPORTANT]
> Sie können Internet Explorer Windows Admin Center verwalten – Sie müssen stattdessen eine [unterstützte Browser](../understand/faq.md#which-web-browsers-are-supported-by-windows-admin-center
)verwenden.  Wenn Sie Windows Admin Center auf Windows Server installieren, wird empfohlen, über eine Remoteverbindung mit Windows 10 und Edge verwalten.  Alternativ können Sie lokal auf Windows Server verwalten, wenn Sie einen unterstützten Browser installiert haben.

## Unterstützte Betriebssysteme: Management

Sie können den folgenden Windows-Betriebssystemen mithilfe von Windows Admin Center **Verwalten** :

| Version | Verwalten von *Knoten* über *Server-Manager* | Verwalten von *Cluster* über *Failovercluster-Manager* | Verwalten von *HCI* über *HCI Cluster-Manager*|
|-------------------------|---------------|-----|------------------------|
| Windows 10, Version 1709 oder höher | Ja (über Computermanagement) | n.a. | n.a. |
| Windows Server (Semi-Annual Channel) | Ja | Ja | – |
| Windows Server 2019 | Ja | Ja | Ja |
| Windows Server 2016 | Ja | Ja | Ja, mit den [neuesten kumulativen update](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) |
| Microsoft Hyper-V Server 2016 | Ja | Ja | – |
| Windows Server2012 R2 | Ja | Ja | – |
| Microsoft Hyper-V Server 2012 R2 | Ja | Ja | n.v. |
| Windows Server 2012 | Ja | Ja | – |
| Windows Server 2008 R2 | Ja, eingeschränkte Funktionen | n.a. | n.a. |

> [!NOTE]
> Windows Admin Center erfordert PowerShell-Features, die nicht in Windows Server 2008 R2, 2012 und 2012 R2 enthalten sind. Wenn Sie diese mit Windows Admin Center verwalten zu können, müssen Sie Windows Management Framework (WMF) Version 5.1 oder höher auf diesen Servern installieren.

>Geben Sie `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder einen neuere Version installiert ist. 

>Wenn WMF nicht installiert ist, können Sie [WMF 5.1 herunterladen](https://www.microsoft.com/en-us/download/details.aspx?id=54616).

## Bereitstellungsoptionen

| ![IMG](../media/deployment-options/W10.png) | ![IMG](../media/deployment-options/gateway.png) | ![IMG](../media/deployment-options/node.png) | ![IMG](../media/deployment-options/HA.png) |
|---|---|---|---|

| Lokalen Client | Gateway-Server | Verwaltete Server | Failovercluster |
| --- | --- | --- | --- |
| Installieren Sie auf einem lokalen Windows 10-Client, der mit den verwalteten Servern verbunden ist.  Ideal für Schnellstart-Ad-hoc- oder kleinen Skalierung Szenarien testen. |Installieren auf einem designierten Gateway-Server und den Zugriff auf dem Gateway-Server mit Konnektivität über alle Clientbrowser.  Gut für umfassende Szenarien. | Installieren Sie direkt auf einen verwalteten Server zum Verwalten von sich selbst oder einem Cluster, in dem sie eine Memberknoten ist.  Gut für verteilte Szenarien. | In einem Failovercluster zu ermöglichen von hoher Verfügbarkeit des Diensts Gateway bereitstellen. Hervorragend für produktionsumgebungen geeignet, um sicherzustellen, dass Ihre Management-Service-resilienz. |

## Hohe Verfügbarkeit

Sie können die hohen Verfügbarkeit des Diensts Gateway aktivieren, durch die Bereitstellung von Windows Admin Center in einem Aktiv / Passiv-Modell auf einem Failovercluster. Wenn einer der Knoten im Cluster ausfällt, Failover Windows Admin Center problemlos auf einen anderen Knoten abgemeldet nahtlos, die Server in Ihrer Umgebung zu verwalten.

[Enthält Informationen zum Bereitstellen von Windows Admin Center mit hoher Verfügbarkeit.](../deploy/high-availability.md)

> [!Tip]
> Sind Sie bereit zum Installieren von Windows Admin Center? [Jetzt herunterladen](https://aka.ms/windowsadmincenter)
