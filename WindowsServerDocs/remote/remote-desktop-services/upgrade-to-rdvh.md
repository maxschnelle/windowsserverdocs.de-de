---
title: Aktualisieren deines Remotedesktop-Virtualisierungshosts auf Windows Server 2016
description: In diesem Artikel wird beschrieben, wie du deine vorhandenen Bereitstellungen der Remotedesktopdienste auf Windows Server 2016 aktualisierst.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 08/01/2016
ms.topic: article
ms.assetid: 5aed8ba7-f541-4416-b01c-4d3b1712e2b1
author: spatnaik
manager: scottman
ms.openlocfilehash: 7bbf5f6a81a18303d4f9f4b02a1b8dead3c9a53a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857113"
---
# <a name="upgrading-your-remote-desktop-virtualization-host-to-windows-server-2016"></a>Aktualisieren deines Remotedesktop-Virtualisierungshosts auf Windows Server 2016

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

## <a name="supported-os-upgrades-with-rds-role-installed"></a>Unterstützte Betriebssystemupgrades mit installierter RDS-Rolle
Upgrades auf Windows Server 2016 werden nur von Windows Server 2012 R2 und Windows Server 2016 TP5 unterstützt.

## <a name="rd-virtualization-host-servers-in-the-deployment-where-vms-are-stored-locally"></a>RD-Virtualisierungshostserver in der Bereitstellung, wo virtuelle Computer lokal gespeichert werden
Diese Server müssen gleichzeitig aktualisiert werden. Führe die folgenden Schritte zum Aktualisieren aus:

1. Melde alle Benutzer ab.
1. Schalte alle virtuellen Computer auf allen Hosts aus, oder speichere sie. 
1. Aktualisiere die Server auf Windows Server 2016. 
1. Alle Sammlungen sollten verfügbar und funktionsfähig sein, nachdem die Upgrades durchgeführt wurden.      

## <a name="rd-virtualization-host-servers-in-the-deployment-where-vms-are-stored-in-cluster-shared-volumes-csv"></a>RD-Virtualisierungshostserver in der Bereitstellung, wo virtuelle Computer in freigegebenen Clustervolumes (Cluster Shared Volumes, CSV) gespeichert werden 

1. Lege eine Upgradestrategie fest, bei der einige der RDVH-Server aktualisiert werden und andere weiterhin VMs auf Windows Server 2012 R2 hosten.  
2. Isoliere einen oder mehrere der RDVH-Server, die für die erste Upgraderunde vorgesehen sind, indem du alle VMs auf andere, noch nicht zu aktualisierende RDVH-Server migrierst, die Teil des ursprünglichen 2012 R2-Clusters bleiben.
    1. Öffne den Failovercluster-Manager 
    1. Klicken Sie auf **Rollen**. 
    1. Wähle eine oder mehrere VMs aus. Klicke mit der rechten Maustaste, um das Kontextmenü zu öffnen. 
    1. Klicke auf **Verschieben**, und wähle entweder **Livemigration** oder **Schnellmigration** aus, um die VMs auf einen oder mehrere der RD-Virtualisierungshostserver zu verschieben, die nicht Teil des ersten Upgrades sind. Verwende **Livemigration** oder **Schnellmigration** abhängig von Faktoren wie Hardwarekompatibilität oder Onlineanforderungen. 
3. Entferne die für das Upgrade vorbereiteten RDVH-Server aus dem ursprünglichen Cluster. 
4. Aktualisiere die isolierten RDVH-Server. 
5. Nachdem die vorgesehenen RDVH-Server erfolgreich aktualisiert wurden, erstelle einen neuen Cluster und neue CSVs, was auf einem ganz anderen SAN-Volume erfolgen muss.
6. Verknüpfe alle aktualisierten RDVH-Server mit dem neuen Cluster. 
7. Erstelle eine Ordnerstruktur im neuen CSV, die die Ordnerstruktur im vorhandenen CSV imitiert. Dazu gehören die Sammlungsordner und die Unterordner auf höchster Ebene jedes virtuellen Computers. 
8. Kopiere aus den verschiedenen VM-Sammlungsordnern des ursprünglichen CSV den Ordner „/IMGS“ und dessen Inhalt in die neuen Sammlungsordner an den gleichen Speicherorten des neuen CSV. 
9. Entferne auf dem Quell-RDVH-Computer mit dem Cluster-Manager die Konfiguration der VM für Hochverfügbarkeit:
    1. Starte den Cluster-Manager. 
    1. Klicken Sie auf **Rollen**. 
    1. Klicke mit der rechten Maustaste auf die VM-Objekte, und klicke dann auf **Entfernen**. 
10. Verschiebe auf einem der nicht aktualisierten RDVH-Server mit dem Hyper-V-Manager alle VMs auf einen der aktualisierten RDVH-Server und das neue Cluster-CSV:
    1. Öffnen Sie den Hyper-V-Manager. 
    2. Wähle einen der nicht aktualisierten RDVH-Server aus. 
    3. Klicke mit der rechten Maustaste auf eine der zu verschiebenden VMs, und klicke dann auf **Verschieben**. 
    4. Wähle **Virtuellen Computer verschieben** aus, und klicke dann auf **Weiter**. 
    5. Gib den Namen des vorgesehenen aktualisierten RDVH-Servers auf der Seite **Zielcomputer angeben** ein, und klicke dann auf **Weiter**. 
    6. Wähle**Daten des virtuellen Computers in einen einzelnen Speicherort verschieben** aus, und klicke dann auf **Weiter**. 
    7. Navigiere zum Zielspeicherort. 
       > [!IMPORTANT]
       > Stelle sicher, dass dieser Pfad für die jeweilige VM zu einem leeren Ordner führt. 

       > [!NOTE]
       > Wie bereits erwähnt, musst du bereits vor diesem Schritt einen neuen Zielunterordner erstellt haben. Das Dialogfeld „Ordner auswählen“ lässt in diesem Schritt nicht zu, einen Unterordner zu erstellen. 
    
       Klicken Sie auf **Weiter**und dann auf **Fertig stellen**. 
11. Nachdem die virtuellen Computer verschoben sind, füge sie als Clusterobjekte mit **Hoher Verfügbarkeit** hinzu:
     1. Öffne den Failovercluster-Manager auf einem aktualisierten Remotedesktop-Virtualisierungshostserver. 
     1. Klicke mit der rechten Maustaste auf den Knoten **Rollen**, und klicke dann auf **Rolle konfigurieren**. Klicke auf der Seite **Start** des Assistenten für hohe Verfügbarkeit auf **Weiter**. 
     1. Wähle**VM** in der Liste der verfügbaren Rollen aus, und klicke dann auf **Weiter**. Eine Liste der nicht konfigurierten VMs wird angezeigt. 
     1. Wähle alle virtuellen Computer aus. Klicke auf **Weiter** und dann auf der Bestätigungsseite erneut auf **Weiter**, um die Konfigurationsaufgabe zu starten.  
12. Nachdem du alle virtuellen Computer verschoben hast, aktualisiere die verbleibenden RDVH-Server. Schaffe mit den oben genannten Schritten eine angemessene Ausgewogenheit der VM-Speicherorte.

> [!NOTE]  
> Heterogene Hyper-V-Server in einem Cluster werden nicht unterstützt. 
