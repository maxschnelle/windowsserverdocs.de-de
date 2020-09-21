---
title: Welche Art von Installation ist für dich geeignet?
description: In diesem Thema werden die verschiedenen Installationsoptionen für Windows Admin Center beschrieben, einschließlich der Installation auf einem Windows 10-PC oder einem Windows-Server zur Verwendung durch mehrere Administratoren.
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 12/02/2019
ms.openlocfilehash: 403a0f68f559d72dfaa54e4b537a50a66fc3ec6a
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766723"
---
# <a name="what-type-of-installation-is-right-for-you"></a>Welche Art von Installation ist für dich geeignet?

In diesem Thema werden die verschiedenen Installationsoptionen für Windows Admin Center beschrieben, einschließlich der Installation auf einem Windows 10-PC oder einem Windows-Server zur Verwendung durch mehrere Administratoren. Informationen zum Installieren von Windows Admin Center auf einem virtuellen Computer in Azure finden Sie unter [Bereitstellen von Windows Admin Center in Azure](../azure/deploy-wac-in-azure.md).

## <a name="installation-types"></a>Installation: Typen

![img](../media/deployment-options/install-options.PNG)

| Lokaler Client                                | Gatewayserver                                  | Verwalteter Server                               | Failovercluster                           |
|---------------------------------------------|-------------------------------------------------|----------------------------------------------|--------------------------------------------|
| [Installieren](../deploy/install.md) auf einem lokalen Windows 10-Client, der über eine Verbindung mit den verwalteten Servern verfügt.  Hervorragend geeignet für Schnellstart, Tests, Ad-hoc- oder nicht sehr umfangreiche Szenarien. |[Installieren](../deploy/install.md) auf einem bestimmten Gatewayserver und Zugriff von beliebigen Clientbrowsern mit Konnektivität zum Gatewayserver.  Hervorragend geeignet für umfangreiche Szenarien. | Direktes [Installieren](../deploy/install.md) auf einem verwalteten Server, um sich selbst oder einen Cluster, in dem er ein Mitgliedsknoten ist, zu verwalten.  Hervorragend geeignet für verteilte Szenarien. | [Bereitstellung](#high-availability) in einem Failovercluster, um die Hochverfügbarkeit des Gatewaydiensts zu ermöglichen. Hervorragend geeignet für Produktionsumgebungen, um die Resilienz deines Verwaltungsdiensts sicherzustellen. |

## <a name="installation-supported-operating-systems"></a>Installation: Unterstützte Betriebssysteme

Du kannst Windows Admin Center auf den folgenden Windows-Betriebssystemen **installieren**:

| **Plattform**                       | **Installationsmodus** |
| -----------------------------------| --------------------- |
| Windows 10                         | Lokaler Client |
| Windows Server (Halbjährlicher Kanal) | Gatewayserver, verwalteter Server, Failovercluster |
| Windows Server 2016                | Gatewayserver, verwalteter Server, Failovercluster |
| Windows Server 2019                | Gatewayserver, verwalteter Server, Failovercluster |

So wird Windows Admin Center betrieben

- **Im lokalen Clientszenario:** Starte das Windows Admin Center-Gateway über das Startmenü, und stelle über einen Clientwebbrowser eine Verbindung zu ihm her, indem du auf `https://localhost:6516` zugreifst.
- **In anderen Szenarien:** Stelle eine Verbindung mit dem Windows Admin Center-Gateway auf einem anderen Computer über einen Clientbrowser mit dessen URL her, z. B. `https://servername.contoso.com`.

> [!WARNING]
> Die Installation von Windows Admin Center auf einem Domänencontroller wird nicht unterstützt. [Weitere Informationen zu den bewährten Methoden für die Domänencontrollersicherheit](../../../identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack.md).

## <a name="installation-supported-web-browsers"></a>Installation: Unterstützte Webbrowser

Microsoft Edge (einschließlich [Microsoft Edge Insider](https://microsoftedgeinsider.com)) und Google Chrome werden getestet und unter Windows 10 unterstützt. Andere Webbrowser, einschließlich Internet Explorer und Firefox, sind derzeit nicht Bestandteil unserer Testmatrix und werden daher nicht *offiziell* unterstützt. Diese Browser haben möglicherweise Probleme beim Ausführen von Windows Admin Center. Firefox verfügt z. B. über eigene Zertifikatspeicher, daher musst du das `Windows Admin Center Client`-Zertifikat für Firefox zur Verwendung von Windows Admin Center auf Windows 10 importieren. Weitere Informationen findest du unter [Browserspezifische bekannte Probleme](../support/known-issues.md#browser-specific-issues).

## <a name="management-target-supported-operating-systems"></a>Verwaltungsziel: Unterstützte Betriebssysteme

Mit Windows Admin Center kannst du die folgenden Windows-Betriebssysteme **verwalten**:

| Version | Verwalten des *Knotens* über den *Server-Manager* | Verwalten über den *Cluster-Manager* |
| ------------------------- |--------------- | ----- |
| Windows 10 | Ja (über Computerverwaltung) | NICHT ZUTREFFEND |
| Windows Server (Halbjährlicher Kanal) | Ja | Ja |
| Windows Server 2019 | Ja | Ja |
| Windows Server 2016 | Ja | Ja, mit [neuestem kumulativen Update](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) |
| Microsoft Hyper-V Server 2016 | Ja | Ja |
| Windows Server 2012 R2 | Ja | Ja |
| Microsoft Hyper-V Server 2012 R2 | Ja | Ja |
| Windows Server 2012 | Ja | Ja |

> [!NOTE]
> Windows Admin Center erfordert PowerShell-Features, die nicht in Windows Server 2012 und 2012 R2 enthalten sind. Um diese mit Windows Admin Center verwalten zu können, musst du Windows Management Framework (WMF) ab Version 5.1 auf diesen Servern installieren.
>
> Gebe `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder höher installiert ist.
>
> Wenn WMF nicht installiert ist, kann [WMF 5.1 heruntergeladen](https://www.microsoft.com/download/details.aspx?id=54616) werden.

## <a name="high-availability"></a>Hohe Verfügbarkeit

Du kannst die Hochverfügbarkeit des Gatewaydiensts aktivieren, indem du Windows Admin Center in einem Aktiv-Passiv-Modell auf einem Failovercluster bereitstellst. Wenn einer der Knoten im Cluster ausfällt, wechselt Windows Admin Center problemlos zu einem anderen Knoten, sodass die Server in der Umgebung problemlos weiter verwaltet werden können.

[Erfahre, wie Windows Admin Center mit Hochverfügbarkeit bereitgestellt wird.](../deploy/high-availability.md)

> [!Tip]
> Bist du für die Installation von Windows Admin Center bereit? [Jetzt herunterladen](../overview.md)