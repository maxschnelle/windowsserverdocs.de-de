---
title: Serverrollenupgrade und Migrationsmatrix für Windows Server 2016
description: Zeigt, welche Serverrollen zu Windows Server 2016 aktualisiert oder migriert werden können.
ms.prod: windows-server
ms.date: 10/05/2016
ms.technology: server-general
ms.topic: article
ms.assetid: 7e031a64-b1e6-4cf6-994a-e7c575835f6a
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 4e1b783c43eb435e61c7caaccaf842a0137b5eec
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826523"
---
# <a name="server-role-upgrade-and-migration-matrix-for-windows-server-2016"></a>Serverrollenupgrade und Migrationsmatrix für Windows Server 2016

>Gilt für: Windows Server 2016

Das Raster auf dieser Seite veranschaulicht Ihre Optionen für Serverrollenupgrades und die Migration speziell für den Wechsel zu Windows Server 2016. Einzelne Migrationshandbücher finden Sie unter [Migrieren von Rollen und Features in Windows Server](https://docs.microsoft.com/windows-server/get-started/migrate-roles-and-features). Weitere Informationen zu Installation und Upgrades finden Sie unter [Windows Server Installation, Upgrade, and Migration (Windows Server-Installation, -Upgrade und -Migration)](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade).

|Serverrolle|Upgrade von Windows Server 2012 R2 möglich?|Upgrade von Windows Server 2012 möglich?|Wird die Migration unterstützt?|Kann die Migration ohne Downtime abgeschlossen werden?|  
|-------------------|----------|--------------|--------------|----------|  
|Active Directory-Zertifikatdienste|    Ja|    Ja|    Ja|    Nein|
|Active Directory-Domänendienste (AD DS)|    Ja|    Ja|    Ja|    Ja|
|Active Directory-Verbunddienste|    Nein|    Nein|    Ja|    Nein (neue Knoten müssen zur Farm hinzugefügt werden)|
|Active Directory Lightweight Directory Services|    Ja|    Ja|    Ja|    Ja|
|Active Directory-Rechteverwaltungsdienste|    Ja|    Ja|    Ja|    Nein|
|DHCP-Server|    Ja|    Ja|    Ja|    Ja|
|DNS-Server|    Ja|    Ja|    Ja|    Nein|
|Failovercluster|Ja mit dem Prozess [Cluster OS Rolling Upgrade](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade), der Pause-Drain und Evict von Knoten, Upgrade auf Windows Server 2016 und das wieder Zusammenführen von Knoten zu einem ursprünglichen Cluster umfasst. Ja, wenn der Server für ein Upgrade vom Cluster entfernt und dann zu einem anderen Cluster hinzugefügt wird.|Nicht wenn der Server Teil eines Clusters ist. Ja, wenn der Server für ein Upgrade vom Cluster entfernt und dann zu einem anderen Cluster hinzugefügt wird.    |Ja|Nicht für Windows Server 2012-Failovercluster. Ja, für Windows Server 2012 R2-Failovercluster mit virtuellen Hyper-V Computern, oder für Windows Server 2012 R2-Failovercluster, die die Rolle des Dateiservers mit horizontaler Skalierung ausführen. Weitere Informationen finden Sie unter [Cluster OS Rolling Upgrade](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade).|
|Datei- und Speicherdienste|    Ja|    Ja|    Variiert je nach Sub-Feature|    Nein|
|Hyper-V| Ja. (Wenn der Host Teil eines Clusters mit dem Prozess Cluster OS Rolling Upgrade ist, der Pause-Drain und Evict von Knoten, Upgrade auf Windows Server 2016 und das wieder Zusammenführen von Knoten zu einem ursprünglichen Cluster umfasst.)|  Nein|   Ja|  Nicht für Windows Server 2012-Failovercluster. Ja, für Windows Server 2012 R2-Failovercluster mit virtuellen Hyper-V Computern, oder für Windows Server 2012 R2-Failovercluster, die die Rolle des Dateiservers mit horizontaler Skalierung ausführen. Weitere Informationen finden Sie unter [Cluster OS Rolling Upgrade](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade).| 
|Druck- und Faxdienste|    Nein|    Nein|    Ja (Printbrm.exe)|    Nein|
|Remotedesktopdienste|    Ja, für alle untergeordneten Rollen. Die Farm im gemischten Modus wird jedoch nicht unterstützt|    Ja, für alle untergeordneten Rollen. Die Farm im gemischten Modus wird jedoch nicht unterstützt|    Ja|    Nein|
|Webserver (IIS)|    Ja|    Ja|    Ja|    Nein|
|Windows Server Essentials Experience|    Ja|    N/V – neues Feature|    Ja|    Nein|
|Windows Server Update Services|    Ja|    Ja|    Ja|    Nein|
|Arbeitsordner|    Ja|    Ja|    Ja|    Ja, vom Cluster WS 2012 R2, wenn [Cluster OS Rolling Upgrade](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) ausgeführt wird.|

