---
title: Bereitstellen Sie ein Dateifreigabezeugen auf WindowsServer 2019
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/24/2019
description: Dateifreigabezeugen können Sie eine Dateifreigabe zu verwenden, um im Clusterquorum abstimmen. Dieses Thema beschreibt dateifreigabezeugen und die neuen Funktionen, einschließlich der Verwendung von einem USB-Laufwerk an einen Router als einen Dateifreigabenzeugen verbunden.
ms.localizationpriority: medium
ms.openlocfilehash: 1888142f96208800a0417c9caeea89e8a0472e88
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831751"
---
# <a name="deploy-a-file-share-witness"></a>Bereitstellen Sie ein dateifreigabezeugen

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ein Dateifreigabenzeuge ist eine SMB-Freigabe, die Failover-Cluster als eine Stimme in das Clusterquorum verwendet. Dieses Thema enthält eine Übersicht über die Technologie und die neuen Funktionen in Windows Server-2019, einschließlich der Verwendung von einem USB-Laufwerk an einen Router als einen Dateifreigabenzeugen verbunden.

Dateifreigabezeugen sind in den folgenden Situationen nützlich:  

- Ein cloudzeugen kann nicht verwendet werden, da nicht alle Server im Cluster eine zuverlässige Internetverbindung verfügen.
- Ein datenträgerzeuge kann nicht verwendet werden, da es sind keine freigegebenen Laufwerke, die für einen datenträgerzeugen verwendet. Dies ist möglicherweise ein "direkte Speicherplätze"-Cluster, SQL Server Always On Availability Gruppen (-Verfügbarkeitsgruppen), Exchange Database Availability Group (DAG), usw.  Keinem dieser Typen von Clustern verwenden freigegebener Datenträger vorhanden.

## <a name="file-share-witness-requirements"></a>File Share Witness Anforderungen

Sie können einen dateifreigabezeugen auf eine Domäne eingebundenen Windows-Server hosten, oder wenn Ihr Cluster Windows Server 2019, jedem Gerät ausgeführt wird Host einer SMB-2 oder höher Datei freigeben.

|Dateiservertyp                 | Unterstützte Cluster |
|---------------------------------|--------------------|
|Alle Geräte w/einen SMB 2-Dateifreigabe | Windows Server 2019|
|Domäne eingebundenen WindowsServer     | WindowsServer 2008 und höher|

Wenn der Cluster Windows Server-2019 ausgeführt wird, sind hier die Anforderungen:

- SMB-Dateifreigabe *auf jedes Gerät, das SMB 2 oder höher-Protokoll verwendet*, einschließlich:
    - Geräte Network-attached Storage (NAS)
    - Windows-Computer zu einer Arbeitsgruppe gehört
    - Router mit dem lokal verbundenen USB-Speicher
- Ein lokales Konto auf dem Gerät für die Authentifizierung des Clusters
- Wenn Sie stattdessen Active Directory zum Authentifizieren des Clusters mit der Dateifreigabe verwenden, die Cluster-Name-Objekt (CNO) muss über Schreibberechtigungen für die Freigabe verfügen, und der Server muss in derselben Active Directory-Gesamtstruktur wie der Cluster.
- Die Dateifreigabe verfügt über mindestens 5 MB freier Speicherplatz

Wenn der Cluster WindowsServer 2016 oder früher ausgeführt wird, sind hier die Anforderungen:

- SMB-Dateifreigabe *auf einem Windows-Server in derselben Active Directory-Gesamtstruktur wie der Cluster eingebunden*
- Die Cluster-Name-Objekt (CNO) muss Schreibberechtigungen für die Freigabe verfügen.
- Die Dateifreigabe verfügt über mindestens 5 MB freier Speicherplatz

Weitere Hinweise:
- Verwendung von File Share Witness von Geräte als eine Domäne eingebundenen Windows-Server gehostet wird, derzeit müssen Sie verwenden die **Set-ClusterQuorum-Anmeldeinformationen** PowerShell-Cmdlet, um den Zeugen festlegen, wie weiter unten in diesem Thema beschrieben.
- Für hohe Verfügbarkeit können Sie einen dateifreigabezeugen auf einem separaten Failovercluster verwenden.
- Die Dateifreigabe kann von mehreren Clustern verwendet werden
- Die Verwendung eines verteilten Dateisystems (Distributed File System, DFS)-Dateifreigabe oder repliziertem Speicher wird mit jeder Version der Failover-Clusterunterstützung nicht unterstützt.  Diese kann eine Split-Brain-Situation, in dem geclusterte Servern werden unabhängig voneinander ausgeführt und können zu Datenverlust führen.

## <a name="creating-a-file-share-witness-on-a-router-with-a-usb-device"></a>Erstellen einen dateifreigabezeugen auf einem Router mit einem USB-Gerät

Am [Microsoft Ignite 2018](https://azure.microsoft.com/ignite/), [Spitzengruppe Storage](http://www.dataonstorage.com/) mussten Sie einem Cluster für direkte Speicherplätze in ihrer Region Kioskmodus.  Dieser Cluster verbunden war, eine [NetGear](https://www.netgear.com) Nighthawk X4S WiFi-Router mithilfe des USB-Ports als Datei Dateifreigabenzeugen ähnelt.

![NetGear Zeugen](media\File-Share-Witness\FSW1.png)

Die Schritte zum Erstellen eines Dateifreigabenzeugen mithilfe eines USB-Geräts auf diesem bestimmten Router sind unten aufgeführt.  Erfahren Sie, wie bereitgestellt, beachten Sie, dass die Schritte, die von anderen Routern und NAS-Geräte variieren und mithilfe von Anbieter durchgeführt werden soll.


1. Melden Sie sich den Router, mit dem USB-Gerät angeschlossen.

   ![NetGear-Schnittstelle](media\File-Share-Witness\FSW2.png)

2. Wählen Sie aus der Liste der Optionen ReadySHARE handelt es sich, in denen Freigaben erstellt werden können.

   ![NetGear ReadySHARE](media\File-Share-Witness\FSW3.png)

3. Für einen Dateifreigabenzeugen ist eine einfache Freigabe alles, die was erforderlich ist.  Die Schaltfläche "Bearbeiten" auswählen, wird ein Dialogfeld angezeigt, in dem die Freigabe auf dem USB-Gerät erstellt werden kann.

   ![NetGear-Freigabe-Schnittstelle](media\File-Share-Witness\FSW4.png)

4. Nach der Schaltfläche "anwenden" auswählen, wird die Freigabe wird erstellt und in der Liste angezeigt werden kann.

   ![NetGear Freigaben](media\File-Share-Witness\FSW5.png)

5. Sobald die Freigabe erstellt wurde, ist der Dateifreigabenzeuge für Cluster mit PowerShell erstellt.

   ```PowerShell
   Set-ClusterQuorum -FileShareWitness \\readyshare\Witness -Credential (Get-Credential)
   ```

   Dies zeigt ein Dialogfeld zum Eingeben des lokalen Kontos auf dem Gerät.

Die gleichen ähnliche Schritte können auf andere Router mit USB-Funktionen, NAS-Geräten oder anderen Windows-Geräten erfolgen.
