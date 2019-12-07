---
title: Welche Art der Installation ist für Sie geeignet?
description: In diesem Thema werden die verschiedenen Installationsoptionen für Windows Admin Center beschrieben, einschließlich der Installation von auf einem Windows 10-PC oder Windows Server für die Verwendung durch mehrere Administratoren.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 12/02/2019
ms.openlocfilehash: d4046cc10a5e0fdc12cfb9587eef10d4263c2ddd
ms.sourcegitcommit: 7c7fc443ecd0a81bff6ed6dbeeaf4f24582ba339
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2019
ms.locfileid: "74904023"
---
# <a name="what-type-of-installation-is-right-for-you"></a>Welche Art von Installation ist für Sie geeignet?

In diesem Thema werden die verschiedenen Installationsoptionen für Windows Admin Center beschrieben, einschließlich der Installation von auf einem Windows 10-PC oder Windows Server für die Verwendung durch mehrere Administratoren. Informationen zum Installieren des Windows Admin Centers auf einem virtuellen Computer in Azure finden Sie unter Bereitstellen [des Windows Admin Centers in Azure](../azure/deploy-wac-in-azure.md).

## <a name="installation-types"></a>Installation: Typen

![img](../media/deployment-options/install-options.PNG)

| Lokaler Client                                | Gatewayserver                                  | Verwalteter Server                               | Failovercluster                           |
|---------------------------------------------|-------------------------------------------------|----------------------------------------------|--------------------------------------------|
| [Installieren](../deploy/install.md) Sie auf einem lokalen Windows 10-Client, der über Konnektivität zu den verwalteten Servern verfügt.  Hervorragend geeignet für Schnellstart-, Test-, Ad-hoc-oder kleine Skalierungs Szenarien. |[Installieren](../deploy/install.md) Sie auf einem bestimmten Gatewayserver, und greifen Sie von einem beliebigen Client Browser aus mit Verbindung zum Gatewayserver darauf zu.  Ideal für umfangreiche Szenarien. | [Installieren](../deploy/install.md) Sie direkt auf einem verwalteten Server, um sich selbst oder einen Cluster zu verwalten, in dem es sich um einen Mitglieds Knoten handelt.  Hervorragend für verteilte Szenarien. | Stellen [Sie in einem](#high-availability) Failovercluster bereit, um die Hochverfügbarkeit des Gatewaydiensts zu ermöglichen. Hervorragend für Produktionsumgebungen, um die Resilienz Ihres Verwaltungs Dienstanbieter sicherzustellen. |

## <a name="installation-supported-operating-systems"></a>Installation: Unterstützte Betriebssysteme

Sie können Windows Admin Center unter den folgenden Windows-Betriebssystemen **Installieren** :

| **Platform**                       | **Installationsmodus** |
| -----------------------------------| --------------------- |
| Windows 10                         | Lokaler Client |
| Windows Server (Semi-Annual Channel) | Gatewayserver, verwalteter Server, Failovercluster |
| Windows Server 2016                | Gatewayserver, verwalteter Server, Failovercluster |
| Windows Server 2019                | Gatewayserver, verwalteter Server, Failovercluster |

So betreiben Sie Windows Admin Center:

- **In lokalem Client Szenario:** Starten Sie das Windows Admin Center-Gateway über das Startmenü, und stellen Sie über einen Client Webbrowser eine Verbindung mit ihm her, indem Sie auf `https://localhost:6516`zugreifen.
- **In anderen Szenarien:** Stellen Sie eine Verbindung mit dem Windows Admin Center-Gateway auf einem anderen Computer her, von einem Client Browser über die URL, z. b. `https://servername.contoso.com`

> [!WARNING]
> Die Installation von Windows Admin Center auf einem Domänen Controller wird nicht unterstützt. [Weitere Informationen finden Sie unter Bewährte Sicherheitsmethoden für Domänen Controller](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack).

## <a name="installation-supported-web-browsers"></a>Installation: Unterstützte Webbrowser

Microsoft Edge (einschließlich [Microsoft Edge Insider](https://microsoftedgeinsider.com)) und Google Chrome werden getestet und unter Windows 10 unterstützt. Andere Webbrowser – einschließlich Internet Explorer und Firefox – sind zurzeit nicht Teil unserer Test Matrix und werden daher nicht *offiziell* unterstützt. Diese Browser haben möglicherweise Probleme beim Ausführen des Windows Admin Centers. Firefox verfügt beispielsweise über einen eigenen Zertifikat Speicher, sodass Sie das `Windows Admin Center Client` Zertifikat in Firefox importieren müssen, damit Windows Admin Center unter Windows 10 verwendet werden kann. Weitere Informationen finden Sie unter [browserspezifische bekannte Probleme](../support/known-issues.md#browser-specific-issues).

## <a name="management-target-supported-operating-systems"></a>Verwaltungs Ziel: Unterstützte Betriebssysteme

Mithilfe des Windows Admin Centers können Sie die folgenden Windows-Betriebssysteme **Verwalten** :

| Version | *Knoten* "verwalten" über *Server-Manager* | Verwalten über den *Cluster-Manager* |
| ------------------------- |--------------- | ----- |
| Windows 10 | Ja (über Computer Verwaltung) | n. v. |
| Windows Server (Semi-Annual Channel) | „Ja“ | „Ja“ |
| Windows Server 2019 | „Ja“ | „Ja“ |
| Windows Server 2016 | „Ja“ | Ja, mit dem [aktuellen kumulativen Update](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) |
| Microsoft Hyper-V Server 2016 | „Ja“ | „Ja“ |
| Windows Server 2012 R2 | „Ja“ | „Ja“ |
| Microsoft Hyper-V Server 2012 R2 | „Ja“ | „Ja“ |
| WindowsServer 2012 | „Ja“ | „Ja“ |
| Windows Server 2008 R2 | Ja, eingeschränkte Funktionalität | n. v. |

> [!NOTE]
> Windows Admin Center erfordert PowerShell-Features, die nicht in Windows Server 2008 R2, 2012 und 2012 R2 enthalten sind. Wenn Sie diese mit dem Windows Admin Center verwalten, müssen Sie Windows Management Framework (WMF) Version 5,1 oder höher auf diesen Servern installieren.
> 
> Geben Sie `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder einen neuere Version installiert ist. 
> 
> Wenn WMF nicht installiert ist, können Sie [WMF 5,1 herunterladen](https://www.microsoft.com/en-us/download/details.aspx?id=54616).

## <a name="high-availability"></a>Hohe Verfügbarkeit

Sie können die Hochverfügbarkeit des Gatewaydiensts aktivieren, indem Sie das Windows Admin Center in einem aktiv/passiv-Modell auf einem Failovercluster bereitstellen. Wenn einer der Knoten im Cluster ausfällt, führt das Windows Admin Center ein ordnungsgemäßes Failover zu einem anderen Knoten durch, sodass Sie die Server in Ihrer Umgebung nahtlos weiter verwalten können.

[Erfahren Sie, wie Sie das Windows Admin Center mit hoher Verfügbarkeit bereitstellen.](../deploy/high-availability.md)

> [!Tip]
> Bist du für die Installation von Windows Admin Center bereit? [Jetzt herunterladen](https://aka.ms/windowsadmincenter)
