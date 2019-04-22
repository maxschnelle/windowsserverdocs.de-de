---
title: Aktualisieren Ihrer Remotedesktop-Virtualisierungshost auf WindowsServer 2016
description: Dieser Artikel beschreibt, wie Sie Ihre vorhandenen Remote Desktop Services-Bereitstellungen auf Windows Server 2016 aktualisieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5aed8ba7-f541-4416-b01c-4d3b1712e2b1
author: spatnaik
manager: scottman
ms.openlocfilehash: 17bf3a49155d29960684acebea870c0b51f664a4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812031"
---
# <a name="upgrading-your-remote-desktop-virtualization-host-to-windows-server-2016"></a>Aktualisieren Ihrer Remotedesktop-Virtualisierungshost auf WindowsServer 2016

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

## <a name="supported-os-upgrades-with-rds-role-installed"></a>Unterstützt Upgrades des Betriebssystems mit Remotedesktopdienste-Rolle installiert
Upgrades auf Windows Server 2016 werden nur von Windows Server 2012 R2 und Windows Server 2016 TP5 unterstützt.

## <a name="rd-virtualization-host-servers-in-the-deployment-where-vms-are-stored-locally"></a>Remotedesktop-Virtualisierungshostserver in der Bereitstellung, in dem virtuelle Computer lokal gespeichert werden
Diese Server müssen gleichzeitig aktualisiert werden. Führen Sie die folgenden Schritte aus, um ein upgrade aus:

1. Alle Benutzer abmelden.
1. Aktivieren Sie deaktivieren oder speichern Sie alle virtuellen Computer auf jedem Host ein. 
1. Aktualisieren Sie den Server, auf Windows Server 2016. 
1. Alle Auflistungen sollte verfügbar und funktionsfähig sein, nachdem die Upgrades durchgeführt wurden.      

## <a name="rd-virtualization-host-servers-in-the-deployment-where-vms-are-stored-in-cluster-shared-volumes-csv"></a>Remotedesktop-Virtualisierungshostserver in der Bereitstellung, in dem virtuelle Computer in freigegebenen Clustervolumes (CSV) gespeichert werden 

1. Bestimmen einer Aktualisierungsstrategie, in denen einige der RDVH-Server werden aktualisiert, und einige weiterhin das Hosten von VMs unter Windows Server 2012 R2.  
1. Isolieren Sie eine oder mehrere der RDVH-Server, die als Ziel für die erste bewertungsrunde aktualisieren, durch die Migration von allen virtuellen Computern in andere ' nicht noch aktualisiert werden"RDVH-Server, die Teil des ursprünglichen 2012 R2-Clusters bleiben.
    1. Öffnen Sie die Failovercluster-Manager. 
    1. Klicken Sie auf **Rollen**. 
    1. Wählen Sie eine oder mehrere VMs. Mit der rechten Maustaste um das Kontextmenü zu öffnen. 
    1. Klicken Sie auf **verschieben** und wählen Sie entweder **Live** oder **Quick-Migration** verschieben Sie die virtuellen Computer auf eine oder mehrere der Remotedesktop-Virtualisierungshostserver, die nicht Teil des anfänglichen Upgrades sind. Verwendung **Live** oder **schnelle** Migration abhängig von Faktoren wie der Hardwarekompatibilität oder online-Anforderungen. 
1. Entfernen Sie die RDVH-Servern, die für die Aktualisierung, von dem ursprünglichen Cluster vorbereitet. 
1. Aktualisieren Sie die isolierten RDVH-Server. 
1. Nachdem Sie die RDVH-Zielservern wurde erfolgreich aktualisiert wurden, erstellen Sie einen neuen Cluster und CSV-Datei, die auf einem anderen SAN-Volume sein muss.
1. Verknüpfen Sie alle aktualisierten RDVH-Server, mit dem neuen Cluster. 
1. Erstellen Sie eine Ordnerstruktur, in der neuen CSV-Datei, die die Ordnerstruktur in der vorhandenen CSV imitiert. Dazu gehören die Ordner für die Datensammlung und jedes virtuellen Computers Top Level Unterordner. 
1. Kopieren Sie aus den verschiedenen VM-Sammlung Ordnern auf dem ursprünglichen CSV-Datei die /IMGS-Ordner und den Inhalt auf den neuen Ordner für die Datensammlung am gleichen Speicherort auf der neuen CSV-Datei. 
1. Verwenden Sie auf dem Quellcomputer RDVH-Cluster-Manager, um die VM Konfiguration für hohe Verfügbarkeit zu entfernen:
    1. Cluster-Manager zu starten. 
    1. Klicken Sie auf **Rollen**. 
    1. Mit der rechten Maustaste in die VM-Objekte, und klicken Sie dann auf **entfernen**. 
1. Verwenden Sie auf einem der nicht aktualisierten RDVH-Server Hyper-V-Manager, um alle virtuellen Computer auf einen der aktualisierten RDVH-Server und der neuen CSV, Cluster zu verschieben:
    1. Öffnen Sie den Hyper-V-Manager. 
    1. Wählen Sie eine der nicht aktualisierten RDVH-Server. 
    1. Mit der rechten Maustaste eines virtuellen Computers verschoben werden, und klicken Sie dann auf **verschieben**. 
    1. Wählen Sie **den virtuellen Computer verschieben**, und klicken Sie dann auf **Weiter**. 
    1. Geben Sie gezielte aktualisierten RDVH den Namen des Servers, auf die **Zielcomputer angeben** Seite, und klicken Sie dann auf **Weiter**. 
    1. Wählen Sie **verschieben Sie den VM Daten an zentraler Stelle**, und klicken Sie dann auf **Weiter**. 
    1. Navigieren Sie zu den Zielstandort an. 
    > [!IMPORTANT]
    > Stellen Sie sicher, dass dieser Pfad in einen leeren Ordner für den jeweiligen virtuellen Computer ist. 

    > [!NOTE]
    > Wie bereits erwähnt, müssen Sie bereits einen neuen Sub-Zielordner vor diesem Schritt erstellt haben. Das Dialogfeld "Ordner auswählen" lässt nicht zu, dass Sie einen Unterordner in diesem Schritt erstellen. 
    
    Klicken Sie auf **Weiter** und dann auf **Fertig stellen**. 
1. Nachdem die virtuellen Computer verschoben werden, deren hinzufügen als Cluster **Hochverfügbarkeit** Objekte:
    1. Öffnen Sie die Failovercluster-Manager auf einem aktualisierten Remotedesktop-Virtualisierungshostserver. 
    1. Mit der rechten Maustaste die **Rollen** Knoten, und klicken Sie dann auf **Rolle konfigurieren**. Klicken Sie auf **Weiter** auf die **starten** Seite des Assistenten für hohe Verfügbarkeit. 
    1. Wählen Sie **VM** aus der Liste der verfügbaren Rollen, und klicken Sie dann auf **Weiter**. Eine Liste mit VMs, die nicht konfiguriert werden, wird angezeigt werden. 
    1. Wählen Sie alle virtuellen Computer. Klicken Sie auf **Weiter** , und klicken Sie dann auf **Weiter** wieder auf der Seite "Bestätigung", um den Task zu starten.  
1. Nachdem Sie alle virtuellen Computer verschoben haben, aktualisieren Sie die verbleibenden RDVH-Server. Verwenden Sie die oben genannten Schritte für Lastenausgleich der VM-Standorte nach Bedarf.

> [!NOTE]  
> Heterogene Hyper-V-Servern in einem Cluster werden nicht unterstützt. 
