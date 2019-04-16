---
title: Verwalten von Failoverclustern mit Windows Admin Center
description: Verwalten von Failoverclustern mit Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 63f5fca8e7ef63200e01cfc6e00a979e7f045b51
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296672"
---
# Verwalten von Failoverclustern mit Windows Admin Center

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../understand/windows-admin-center.md) oder [jetzt herunterladen](https://aka.ms/windowsadmincenter).

## Verwalten von Failoverclustern
[Failover-Clusterunterstützung](https://docs.microsoft.com/windows-server/failover-clustering/failover-clustering-overview) ist ein Windows Server-Feature, das Ihnen ermöglicht, mehrere Server zu einem fehlertoleranten Cluster zur Steigerung der Verfügbarkeit und Skalierbarkeit von Anwendungen und Dienste, z. B. Scale-Out-Dateiserver, Hyper-V zu gruppieren und Microsoft SQL Server.

Während Sie Failover-Clusterknoten als einzelne Server sie als [Server-Verbindungen](manage-servers.md) im Windows Admin Center hinzufügen verwalten können, können Sie auch diese hinzufügen wie zum Anzeigen und Verwalten von Clusterressourcen, Speicher, Netzwerk, Knoten, Rollen, virtuelle für Failovercluster Computer und virtuelle Switches.

![Failover Cluster (Übersicht) Bildschirm](../media/manage-failover-clusters/fcm-overview.png)

## Hinzufügen eines Failoverclusters zu Windows Admin Center
So fügen Sie einen Cluster in Windows Admin Center hinzu:

1. Klicken Sie unter alle Verbindungen auf **+ Hinzufügen** .
2. Wählen Sie zum Hinzufügen einer **Failover-Verbindung**.
3. Geben Sie den Namen des Clusters und, wenn Sie dazu aufgefordert werden, die Anmeldeinformationen zu verwenden.
4. Sie haben die Möglichkeit, die Clusterknoten als einzelne Server-Verbindungen im Windows Admin Center hinzufügen.
5. Klicken Sie auf **übermitteln** zum Abschließen.

Cluster wird zur Verbindungsliste, auf der Seite "Übersicht" hinzugefügt. Klicken Sie auf die Verbindung mit dem Cluster.

> [!NOTE]
> Sie können auch zusammengeführte verwalten durch Hinzufügen des Clusters als [Hyper-converged Cluster-Verbindung](manage-hyper-converged.md) in Windows Admin Center gruppiert.

## Tools

Die folgenden Tools sind für failoverclusterverbindungen verfügbar:

| Tool | Beschreibung |
| ---- | ----------- |
| Übersicht | Zeigen Sie Failover Cluster Details an und Verwalten von Clusterressourcen |
| Datenträger | Anzeigen von freigegebenen Datenträgern und volumes |
| Netzwerke | Netzwerke im Cluster anzeigen |
| Knoten | Zeigen Sie an und Verwalten von Clusterknoten |
| Rollen | Verwalten von clusterrollen oder eine leere Rolle erstellen |
| Updates | Verwalten von Cluster-Aware Updates (erfordert [CredSSP](../understand/faq.md#does-windows-admin-center-use-credssp)) |
| [Virtuelle Computer](manage-virtual-machines.md) | Zeigen Sie an und Verwalten von virtuellen Computern |
| Virtuelle Switches | Zeigen Sie an und verwalten Sie virtuelle switches |

## Weitere kommen

Failovercluster-Verwaltung in Windows Admin Center ist aktiv in der Entwicklung, und neue Features in naher Zukunft hinzugefügt werden. Sie können den Status und die Zustimmung zum Features in UserVoice anzeigen:

|Feature-Anforderung|
|-------|
| [Mehr gruppierten Datenträger Informationen anzeigen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31740424--cluster-more-disk-info-in-failover-cluster-manag) |
| [Maßnahmen zur Unterstützung zusätzlicher cluster](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/33558076--fcm-full-csv-management-cycle-in-one-place) |
| [Unterstützen Sie zusammengeführte Cluster mit Hyper-V und Dateiserver mit horizontaler Skalierung auf verschiedene Cluster](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31729741--cluster-support-for-converged-architecture) |
| [Ansicht CSV-Block-cache](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31669477--cluster-csv-block-cache) |
| [Alle oder neues Feature vorschlagen](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bcluster%5D) |