---
title: Bereitstellen Sie einen Dateifreigabe-Zeugen in WindowsServer 2019
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/24/2019
description: Datei Freigabe Zeugen können Sie eine Dateifreigabe verwenden, um in Clusterquorum abstimmen. Dieses Thema beschreibt die Datei Freigabe Zeugen und die neuen Funktionen, einschließlich der Verwendung von einem USB-Laufwerk mit einem Router als eine Dateifreigabe-Zeugen verbunden.
ms.localizationpriority: medium
ms.openlocfilehash: 1888142f96208800a0417c9caeea89e8a0472e88
ms.sourcegitcommit: d622f7af181ed0063d716b30278d41887a57db19
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2019
ms.locfileid: "9150890"
---
# Bereitstellen eines Dateifreigabezeugen

> Gilt für: WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

Ein Dateifreigabe-Zeugen, ist eine SMB-Freigabe, die Failovercluster als eine Stimme in das Clusterquorum verwendet. Dieses Thema enthält eine Übersicht über die Technologie und die neuen Funktionen in Windows Server 2019, einschließlich der Verwendung von einem USB-Laufwerk mit einem Router als eine Dateifreigabe-Zeugen verbunden.

Datei Freigabe Zeugen sind praktisch in folgenden Fällen:  

- Eine cloudzeugen kann nicht verwendet werden, da nicht alle Server im Cluster eine zuverlässige Verbindung zum Internet haben
- Zeuge Datenträger kann nicht verwendet werden, weil es keine freigegebenen Laufwerke für Zeuge Datenträger verwenden. Dies ist möglicherweise eine direkte Speicherplätze-Cluster, SQL Server immer auf Verfügbarkeit Gruppen (AG), Exchange Datenbank Verfügbarkeit Gruppe (so), usw..  Dieser Typen von Clustern verwendet werden freigegebene Datenträgern.

## Datei Freigabe Zeugen Anforderungen

Sie können einen Dateifreigabe-Zeugen, auf einem Windows-Server Domäne hosten, oder wenn im Cluster Windows Server 2019 jedem Gerät ausgeführt wird kann Host eine SMB-2 oder höher Datei zu teilen.

|Server-Dateityp                 | Unterstützte Cluster |
|---------------------------------|--------------------|
|Alle Geräte w/eine SMB-2-Dateifreigabe | Windows Server 2019|
|Domäne WindowsServer     | WindowsServer 2008 und höher|

Wenn der Cluster Windows Server 2019 ausgeführt wird, sind hier die Anforderungen:

- SMB-Dateifreigabe *auf jedem Gerät, das die SMB-2 oder höher Protokoll verwendet*, einschließlich:
    - Network attached Storage (NAS)-Geräte
    - Windows-Computern, die Mitglied einer Arbeitsgruppe
    - Router mit lokal verbundene USB-Speicher
- Ein lokales Konto auf dem Gerät für die Authentifizierung des Clusters
- Wenn Sie Active Directory für die Authentifizierung des Clusters mit der Dateifreigabe stattdessen verwenden, muss das Cluster Name Objekt (Clusternamenobjekt) Schreibberechtigungen für die Freigabe, und der Server muss in derselben Active Directory-Gesamtstruktur als Cluster sein
- Die Dateifreigabe wurde mindestens 5 MB freiem Speicherplatz

Wenn der Cluster WindowsServer 2016 oder einer früheren Version ausgeführt wird, sind hier die Anforderungen:

- SMB-Dateifreigabe *auf einem Windows-Server, die Active Directory-Gesamtstruktur als Cluster beigetreten sind*
- Das Cluster Name Objekt (Clusternamenobjekt) müssen Schreibberechtigungen für die Freigabe vorhanden sein.
- Die Dateifreigabe wurde mindestens 5 MB freiem Speicherplatz

Weitere Hinweise:
- Um eine Dateifreigabe-Zeugen von Geräten als eine Domäne eingebunden Windows-Server gehostet zu verwenden, derzeit müssen Sie anhand der **Set-ClusterQuorum-Credential** PowerShell-Cmdlet Zeugen, festlegen, wie weiter unten in diesem Thema beschrieben.
- Für eine hohe Verfügbarkeit können Sie einen Dateifreigabe-Zeugen, auf einem separaten Failovercluster verwenden.
- Die Dateifreigabe kann durch mehrere Cluster verwendet werden
- Die Verwendung einer Freigabe (Distributed File System, DFS) oder eines replizierten Speichers wird mit einer beliebigen Version der Failover-Clusterunterstützung nicht unterstützt.  Diese kann eine Split Brain-Situation, in dem Cluster-Servern unabhängig voneinander ausgeführt werden, und können zu Datenverlust führen.

## Erstellen einen Dateifreigabe-Zeugen, auf einem Router mit einem USB-Gerät

Bei [Microsoft Ignite 2018](https://azure.microsoft.com/ignite/)mussten [DataOn Speicher](http://www.dataonstorage.com/) ein Storage Spaces Direct-Cluster in ihrem Kiosk.  Diese Cluster wurde mit einem [NetGear](https://www.netgear.com) Nighthawk X4S WiFi Router verwenden den USB-Anschluss als eine Dateifreigabe-Zeugen, ähnlich wie folgt verbunden.

![NetGear Zeuge](media\File-Share-Witness\FSW1.png)

Die Schritte zum Erstellen eines Dateifreigabe-Zeugen, verwenden ein USB-Gerät auf diesem bestimmten Router sind unten aufgeführt.  Beachten Sie, dass die Schritte auf anderen Routern und NAS-Geräte variiert und sollte mit der Anbieter ausgeführt werden bereitgestellt, erfahren Sie, wie.


1. Melden Sie sich bei der Router, mit dem USB-Gerät angeschlossen.

   ![NetGear-Schnittstelle](media\File-Share-Witness\FSW2.png)

2. Wählen Sie aus der Liste der Optionen ReadySHARE die ist, in denen Freigaben erstellt werden kann.

   ![NetGear ReadySHARE](media\File-Share-Witness\FSW3.png)

3. Für eine Dateifreigabe-Zeugen ist eine einfache Freigabe alles, die was erforderlich ist.  Auswählen der Schaltfläche "Bearbeiten" wird ein Dialogfeld angezeigt, in denen die Freigabe auf dem USB-Gerät erstellt werden kann.

   ![NetGear Freigabe-Schnittstelle](media\File-Share-Witness\FSW4.png)

4. Nachdem die Schaltfläche Übernehmen auswählen, wird die Freigabe wird erstellt und werden dann in der Liste angezeigt.

   ![NetGear-Freigaben](media\File-Share-Witness\FSW5.png)

5. Nachdem die Bereitstellungsfreigabe erstellt wurde, wird den Dateifreigabe-Zeugen für Cluster mit PowerShell erstellt.

   ```PowerShell
   Set-ClusterQuorum -FileShareWitness \\readyshare\Witness -Credential (Get-Credential)
   ```

   Geben Sie das lokale Konto auf dem Gerät ein Dialogfeld angezeigt.

Dieselben ähnliche Schritte können für andere Router mit USB-Funktionen, NAS-Geräte oder anderen Windows-Geräten ausgeführt werden.
