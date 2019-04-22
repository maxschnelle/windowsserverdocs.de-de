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
ms.openlocfilehash: f7e14581f7f6b14b0cf39308de236b68a07e8c9f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824071"
---
# <a name="manage-failover-clusters-with-windows-admin-center"></a>Verwalten von Failoverclustern mit Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center Preview

> [!Tip]
> Neu bei Windows Admin Center?
> [Erfahren Sie mehr über Windows Admin Center](../understand/windows-admin-center.md) oder [jetzt herunterladen](https://aka.ms/windowsadmincenter).

## <a name="managing-failover-clusters"></a>Verwalten von Failoverclustern
[Failover-Clusterunterstützung](https://docs.microsoft.com/windows-server/failover-clustering/failover-clustering-overview) ist ein Windows Server-Feature, das Ihnen ermöglicht, mehrere Server in einem fehlertoleranten Cluster Erhöhen der Verfügbarkeit und Skalierbarkeit von Anwendungen und Dienste wie z. B. Scale-Out File Server, Hyper-V gruppieren und Microsoft SQL Server.

Während Sie Failoverclusterknoten als einzelne Server verwalten können, indem Sie sie als hinzufügen [serververbindungen](manage-servers.md) in Windows Admin Center, Sie können auch beliebig sie zum Anzeigen und Verwalten von Clusterressourcen, Speicher, Netzwerk, Knoten für Failovercluster Rollen, virtuelle Computer und virtuelle Switches.

![Bildschirm "Systemübersicht" der Failover-cluster](../media/manage-failover-clusters/fcm-overview.png)

## <a name="adding-a-failover-cluster-to-windows-admin-center"></a>Hinzufügen eines Failoverclusters auf Windows Admin Center
So fügen Sie einen Cluster Windows Admin Center hinzu

1. Klicken Sie auf **+ hinzufügen** unter alle Verbindungen.
2. Hinzufügen einer **Failoververbindung**.
3. Geben Sie den Namen des Clusters und, wenn Sie dazu aufgefordert werden, die zu verwendenden Anmeldeinformationen.
4. Sie haben die Möglichkeit, die die Clusterknoten als einzelne Server-Verbindungen in Windows Admin Center hinzufügen.
5. Klicken Sie auf **senden** um den Vorgang abzuschließen.

Ihre Liste der auf der Seite "Übersicht" wird der Cluster hinzugefügt werden. Klicken Sie darauf, eine Verbindung mit dem Cluster herstellen.

> [!NOTE]
> Sie können auch verwalten hyperkonvergenten gruppiert nach Hinzufügen des Clusters als eine [Hyper-Converged Clusterverbindung](manage-hyper-converged.md) in Windows Admin Center.

## <a name="tools"></a>Tools

Die folgenden Tools sind verfügbar für Failover Cluster-Verbindungen:

| Tool | Beschreibung |
| ---- | ----------- |
| Übersicht | Failover-Cluster-Details anzeigen und Verwalten von Clusterressourcen |
| „Datenträger“, | Ansicht freigegebene Datenträger und volumes |
| „Netzwerke“ | Anzeigen von Netzwerken im cluster |
| Knoten | Anzeigen und Verwalten von Clusterknoten |
| Rollen | Verwalten von clusterrollen oder eine leere Rolle erstellen |
| Updates | Verwalten von Cluster-Aware Updates |
| [Virtuelle Computer](manage-virtual-machines.md) | Anzeigen und Verwalten von virtuellen Computern |
| Virtuelle Switches | Anzeigen und Verwalten von virtuellen switches |

## <a name="more-coming"></a>Weitere folgen

Failover-Clusterverwaltung in Windows Admin Center wird aktiv weiterentwickelt, und werden in naher Zukunft neue Funktionen hinzugefügt werden. Sie können den Status und stimmen Sie für Funktionen in UserVoice anzeigen:

|Die Anforderung zur|
|-------|
| [Weitere Datenträgerinformationen die gruppierten anzeigen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31740424--cluster-more-disk-info-in-failover-cluster-manag) |
| [Unterstützung für zusätzliche clusteraktionen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/33558076--fcm-full-csv-management-cycle-in-one-place) |
| [Zusammengeführte Clustern, die unter Hyper-V und den Scale-Out File Server auf verschiedenen Clustern zu unterstützen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31729741--cluster-support-for-converged-architecture) |
| [CSV-blockcache anzeigen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31669477--cluster-csv-block-cache) |
| [Alle anzeigen oder neues Feature vorschlagen](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bcluster%5D) |