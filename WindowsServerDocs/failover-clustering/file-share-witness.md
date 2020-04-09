---
title: Bereitstellen eines Dateifreigabe Zeugen in Windows Server 2019
description: Mithilfe von Dateifreigabe Zeugen können Sie eine Dateifreigabe verwenden, die im Cluster Quorum Stimmen soll. In diesem Thema werden Dateifreigabe Zeugen und die neuen Funktionen beschrieben, einschließlich der Verwendung eines USB-Laufwerks, das mit einem Router als Datei frei gaben Zeuge verbunden ist.
ms.prod: windows-server
manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.author: johnmar
ms.date: 01/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 63e016b8e00482529e69aaa12727f854afd51e41
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80827673"
---
# <a name="deploy-a-file-share-witness"></a>Bereitstellen eines Dateifreigabe Zeugen

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ein Dateifreigabe Zeuge ist eine SMB-Freigabe, die der Failovercluster als Stimme im Cluster Quorum verwendet. Dieses Thema bietet einen Überblick über die Technologie und die neuen Funktionen in Windows Server 2019, einschließlich der Verwendung eines USB-Laufwerks, das mit einem Router als Datei frei gaben Zeuge verbunden ist.

Dateifreigabe Zeugen sind in folgenden Situationen nützlich:  

- Ein cloudzeuge kann nicht verwendet werden, da nicht alle Server im Cluster über eine zuverlässige Internet Verbindung verfügen.
- Ein Datenträger Zeuge kann nicht verwendet werden, da keine freigegebenen Laufwerke für einen Datenträger Zeugen verwendet werden. Dabei kann es sich um einen direkte Speicherplätze Cluster, SQL Server Always on Verfügbarkeits Gruppen (AG), eine Exchange-Daten Bank Verfügbarkeits Gruppe (DAG) usw. handeln.  Keiner dieser Cluster Typen verwendet freigegebene Datenträger.

## <a name="file-share-witness-requirements"></a>Anforderungen an den Dateifreigabe Zeugen

Sie können einen Dateifreigabe Zeugen auf einem in die Domäne eingebundenen Windows-Server hosten, oder auf Ihrem Cluster, auf dem Windows Server 2019 ausgeführt wird, auf allen Geräten, auf denen eine Dateifreigabe mit SMB 2 oder höher gehostet werden kann.

|Datei Servertyp                 | Unterstützte Cluster |
|---------------------------------|--------------------|
|Alle Geräte mit einer SMB 2-Dateifreigabe | Windows Server 2019|
|In die Domäne eingebundener Windows Server     | Windows Server 2008 und höher|

Wenn auf dem Cluster Windows Server 2019 ausgeführt wird, gelten die folgenden Anforderungen:

- Eine SMB-Dateifreigabe *auf allen Geräten, die das SMB 2-Protokoll oder das spätere Protokoll verwenden*, einschließlich:
    - NAS-Geräte (Network-Attached Storage)
    - Windows-Computer, die einer Arbeitsgruppe hinzugefügt wurden
    - Router mit lokal verbundener USB-Speicher
- Ein lokales Konto auf dem Gerät zum Authentifizieren des Clusters
- Wenn Sie stattdessen Active Directory zum Authentifizieren des Clusters mit der Dateifreigabe verwenden, muss das Cluster Namen Objekt (CNO) über Schreibberechtigungen für die Freigabe verfügen, und der Server muss sich in derselben Active Directory Gesamtstruktur wie der Cluster befinden.
- Der freie Speicherplatz der Dateifreigabe beträgt 5 MB.

Wenn auf dem Cluster Windows Server 2016 oder eine frühere Version ausgeführt wird, gelten die folgenden Anforderungen:

- SMB-Dateifreigabe *auf einem Windows-Server, der mit derselben Active Directory Gesamtstruktur wie der Cluster* verknüpft ist
- Das Cluster Namen Objekt (CNO) muss über Schreibberechtigungen für die Freigabe verfügen.
- Der freie Speicherplatz der Dateifreigabe beträgt 5 MB.

Weitere Hinweise:
- Wenn Sie einen Dateifreigabe Zeugen verwenden möchten, der von anderen Geräten als einem in die Domäne eingebundenen Windows-Server gehostet wird, müssen Sie derzeit das PowerShell-Cmdlet **Set-Clusterquorum-Credential** verwenden, um den Zeugen festzulegen, wie weiter unten in diesem Thema beschrieben.
- Um Hochverfügbarkeit zu erreichen, können Sie einen Dateifreigabe Zeugen in einem separaten Failovercluster verwenden.
- Die Dateifreigabe kann von mehreren Clustern verwendet werden.
- Die Verwendung einer DFS-Freigabe (verteiltes Dateisystem) oder eines replizierten Speichers wird von keiner Version des Failoverclustering unterstützt.  Diese können eine Split Brain-Situation verursachen, in der gruppierte Server unabhängig voneinander ausgeführt werden und zu einem Datenverlust führen können.

## <a name="creating-a-file-share-witness-on-a-router-with-a-usb-device"></a>Erstellen eines Dateifreigabe Zeugen auf einem Router mit einem USB-Gerät

Bei der [Microsoft Ignite 2018](https://azure.microsoft.com/ignite/)hatte [DataOn Storage](http://www.dataonstorage.com/) einen direkte Speicherplätze Cluster in seinem Kiosk Bereich.  Dieser Cluster wurde mit einem [Netgear](https://www.netgear.com) Nighthawk X4S WiFi-Router über den USB-Anschluss als Datei frei gaben Zeuge verbunden, der diesem ähnelt.

![Netgear-Zeuge](media/File-Share-Witness/FSW1.png)

Die Schritte zum Erstellen eines Dateifreigabe Zeugen mithilfe eines USB-Geräts auf diesem bestimmten Router sind unten aufgeführt.  Beachten Sie, dass die Schritte auf anderen Routern und NAS-Geräten variieren und mit den vom Hersteller bereitgestellten Anweisungen durchgeführt werden sollten.


1. Melden Sie sich beim Router an, wenn das USB-Gerät angeschlossen ist.

   ![Netgear-Schnittstelle](media/File-Share-Witness/FSW2.png)

2. Wählen Sie in der Liste der Optionen den Eintrag "Read-Share" aus. hier können Freigaben erstellt werden.

   ![Netgear-leseryfreigabe](media/File-Share-Witness/FSW3.png)

3. Für einen Dateifreigabe Zeugen ist nur eine einfache Freigabe erforderlich.  Wenn Sie die Schaltfläche Bearbeiten auswählen, wird ein Dialogfeld angezeigt, in dem die Freigabe auf dem USB-Gerät erstellt werden kann.

   ![Netgear-Freigabe Schnittstelle](media/File-Share-Witness/FSW4.png)

4. Nachdem Sie die Schaltfläche anwenden ausgewählt haben, wird die Freigabe erstellt und kann in der Liste angezeigt werden.

   ![Netgear-Freigaben](media/File-Share-Witness/FSW5.png)

5. Nachdem die Freigabe erstellt wurde, wird die Erstellung des Datei frei gaben Zeugen für den Cluster mit PowerShell durchgeführt.

   ```PowerShell
   Set-ClusterQuorum -FileShareWitness \\readyshare\Witness -Credential (Get-Credential)
   ```

   Dadurch wird ein Dialogfeld angezeigt, in dem Sie das lokale Konto auf dem Gerät eingeben können.

Diese ähnlichen Schritte können auch auf anderen Routern mit USB-Funktionen, NAS-Geräten oder anderen Windows-Geräten ausgeführt werden.
