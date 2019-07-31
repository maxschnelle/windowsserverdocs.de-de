---
title: Welche Art der Installation ist für Sie geeignet?
description: In diesem Thema werden die verschiedenen Installationsoptionen für Windows Admin Center beschrieben, einschließlich der Installation von auf einem Windows 10-PC oder Windows Server für die Verwendung durch mehrere Administratoren.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 06/07/2019
ms.openlocfilehash: 36c9dfcb38ef417df56206cdb18633cc877183c4
ms.sourcegitcommit: af80963a1d16c0b836da31efd9c5caaaf6708133
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2019
ms.locfileid: "68658897"
---
# <a name="what-type-of-installation-is-right-for-you"></a>Welche Art von Installation ist für Sie geeignet?

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

In diesem Thema werden die verschiedenen Installationsoptionen für Windows Admin Center beschrieben, einschließlich der Installation von auf einem Windows 10-PC oder Windows Server für die Verwendung durch mehrere Administratoren. Informationen zum Installieren des Windows Admin Centers auf einem virtuellen Computer in Azure finden Sie unter Bereitstellen [des Windows Admin Centers in Azure](../azure/deploy-wac-in-azure.md).

## <a name="installation-types"></a>Install Typen

| Lokaler Client                                | Gatewayserver                                  | Verwalteter Server                               | Failovercluster                           |
|---------------------------------------------|-------------------------------------------------|----------------------------------------------|--------------------------------------------|
| ![IMG](../media/deployment-options/W10.PNG) | ![IMG](../media/deployment-options/gateway.PNG) | ![IMG](../media/deployment-options/node.PNG) | ![IMG](../media/deployment-options/HA.png) |
| Installieren Sie auf einem lokalen Windows 10-Client, der über Konnektivität zu den verwalteten Servern verfügt.  Hervorragend geeignet für Schnellstart-, Test-, Ad-hoc-oder kleine Skalierungs Szenarien. |Installieren Sie auf einem bestimmten Gatewayserver, und greifen Sie von einem beliebigen Client Browser aus mit Verbindung zum Gatewayserver darauf zu.  Ideal für umfangreiche Szenarien. | Installieren Sie direkt auf einem verwalteten Server, um sich selbst oder einen Cluster zu verwalten, in dem es sich um einen Mitglieds Knoten handelt.  Hervorragend für verteilte Szenarien. | Stellen Sie in einem Failovercluster bereit, um die Hochverfügbarkeit des Gatewaydiensts zu ermöglichen. Hervorragend für Produktionsumgebungen, um die Resilienz Ihres Verwaltungs Dienstanbieter sicherzustellen. |

## <a name="installation-supported-operating-systems"></a>Install Unterstützte Betriebssysteme

Sie können Windows Admin Center unter den folgenden Windows-Betriebssystemen **Installieren** :

| **Plattform**                       | **Installationsmodus** |
| -----------------------------------| --------------------- |
| Windows 10, Version 1709 oder höher  | Lokaler Client |
| Windows Server (Semi-Annual Channel) | Gatewayserver, verwalteter Server, Failovercluster |
| Windows Server 2016                | Gatewayserver, verwalteter Server, Failovercluster |
| Windows Server 2019                | Gatewayserver, verwalteter Server, Failovercluster |

So betreiben Sie Windows Admin Center:

- **In lokalem Client Szenario:** Starten Sie das Windows Admin Center-Gateway über das Startmenü, und stellen Sie über einen Client Webbrowser eine `https://localhost:6516`Verbindung dazu her, indem Sie auf zugreifen.
- **In anderen Szenarien:** Herstellen einer Verbindung mit dem Windows Admin Center-Gateway auf einem anderen Computer als einem Client Browser über die URL, z. b.`https://servername.contoso.com`

> [!WARNING]
> Die Installation von Windows Admin Center auf einem Domänen Controller wird nicht unterstützt. [Weitere Informationen finden Sie unter Bewährte Sicherheitsmethoden für Domänen Controller](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack). 

## <a name="installation-supported-web-browsers"></a>Install Unterstützte Webbrowser

Microsoft Edge und Google Chrome werden auf Windows 10 getestet und unterstützt. Andere Webbrowser – einschließlich Internet Explorer und Firefox – sind zurzeit nicht Teil unserer Test Matrix und werden daher nicht *offiziell* unterstützt. Diese Browser haben möglicherweise Probleme beim Ausführen des Windows Admin Centers. Firefox verfügt beispielsweise über einen eigenen Zertifikat Speicher, sodass Sie das `Windows Admin Center Client` Zertifikat in Firefox importieren müssen, damit Windows Admin Center unter Windows 10 verwendet werden kann. Weitere Informationen finden Sie unter [browserspezifische bekannte Probleme](../support/known-issues.md#browser-specific-issues).

## <a name="management-target-supported-operating-systems"></a>Verwaltungs Ziel: Unterstützte Betriebssysteme

Mithilfe des Windows Admin Centers können Sie die folgenden Windows-Betriebssysteme **Verwalten** :

| Version | *Knoten* "verwalten" über *Server-Manager* | *Cluster* über *Failovercluster-Manager* verwalten | Verwalten von *HCI* über den *HCI-Cluster-Manager* |
| ------------------------- |--------------- | ----- | ------------------------ |
| Windows 10, Version 1709 oder höher | Ja (über Computer Verwaltung) | Nicht zutreffend | Nicht zutreffend |
| Windows Server (Semi-Annual Channel) | Ja | Ja | Nicht zutreffend |
| Windows Server 2019 | Ja | Ja | Ja |
| Windows Server 2016 | Ja | Ja | Ja, mit dem [aktuellen kumulativen Update](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) |
| Microsoft Hyper-V Server 2016 | Ja | Ja | Nicht zutreffend |
| Windows Server 2012 R2 | Ja | Ja | Nicht zutreffend |
| Microsoft Hyper-V Server 2012 R2 | Ja | Ja | Nicht zutreffend |
| Windows Server 2012 | Ja | Ja | Nicht zutreffend |
| Windows Server 2008 R2 | Ja, eingeschränkte Funktionalität | Nicht zutreffend | Nicht zutreffend |

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
> Sind Sie bereit zum Installieren von Windows Admin Center? [Jetzt herunterladen](https://aka.ms/windowsadmincenter)
