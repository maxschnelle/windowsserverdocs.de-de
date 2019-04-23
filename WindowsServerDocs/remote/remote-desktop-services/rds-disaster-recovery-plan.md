---
title: Erstellen des Wiederherstellungsplans
description: Erfahren Sie, wie Sie einen Notfallwiederherstellungsplan für Ihre RDS-Bereitstellung zu erstellen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 05/05/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 8ad759a73e4a0ce1dc28f2b8e8d80f4365895430
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879501"
---
# <a name="create-your-disaster-recovery-plan-for-rds"></a>Erstellen Sie Ihres Plans zur notfallwiederherstellung für RDS

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können einen Notfallwiederherstellungsplan erstellen, in Azure Site Recovery, um den Failoverprozess zu automatisieren. Fügen Sie dem Wiederherstellungsplan alle virtuellen Computer RDS-Komponente hinzu.

Verwenden Sie die folgenden Schritte in Azure, um Ihren Wiederherstellungsplan zu erstellen:

1. Öffnen Sie Azure Site Recovery-Tresor im Azure-Portal aus, und klicken Sie dann auf **Wiederherstellungspläne**.
2. Klicken Sie auf **erstellen** , und geben Sie einen Namen für den Plan.
3. Wählen Sie Ihre **Quelle** und **Ziel**. Das Ziel ist eine sekundäre RDS-Website oder Azure.
4. Wählen Sie die VMs, die Ihre RDS-Komponenten zu hosten, und klicken Sie dann auf **OK**.

Die folgenden Abschnitte enthalten weitere Informationen zum Erstellen von Wiederherstellungsplänen für die verschiedenen Typen von RDS-Bereitstellung.

## <a name="sessions-based-rds-deployment"></a>Sitzungen basierende RDS-Bereitstellung

Gruppieren Sie die VMs für eine Bereitstellung mit RDS-Sitzungen damit diese nacheinander kommen:

1. Failovergruppe 1: Session Host-VM
2. Failovergruppe 2: Broker-VM-Verbindung
3. Failovergruppe 3 – Web Access-VM

Ihr Plan wird wie folgt aussehen: 

![Einen Notfallwiederherstellungsplan für eine sitzungsbasierte RDS-Bereitstellung](media/rds-asr-session-drplan.png)

## <a name="pooled-desktops-rds-deployment"></a>In einem Pool zusammengefasste Desktops RDS-Bereitstellung

Gruppieren Sie die VMs für eine RDS-Bereitstellung bei gepoolten Desktops damit sie in der Sequenz ist, Hinzufügen von manuellen Schritte und Skripts kommen.

1. Failovergruppe 1: RDS Connection Broker-VM
2. Gruppe 1 manuelle Aktion - Update DNS

   Führen Sie PowerShell im erweiterten Modus, auf dem virtuellen Computer Verbindung-Broker. Führen Sie den folgenden Befehl aus, und warten Sie einige Minuten, um sicherzustellen, dass das DNS mit den neuen Wert aktualisiert wird:

   ```
   ipconfig /registerdns
   ```
3. Gruppe 1-Skript – hinzufügen Virtualisierungshosts

   Ändern Sie das folgende Skript auf jedem Virtualisierungshost in der Cloud ausführen. Nachdem Sie einen Virtualisierungshost Verbindungsbrokers hinzugefügt haben, müssen Sie in der Regel den Host neu starten. Stellen Sie sicher, dass der Host verfügt nicht über einen ausstehenden Neustart, bevor Sie das Skript ausgeführt, sonst wird fehlerhaft sein.

   ```
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop; 
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com 
   ```
4. Failovergruppe 2 - Vorlagen-VM
5. Gruppe 2 Skript 1: Aktivieren Sie off-VM-Vorlage
   
   Der Vorlagen-VM beim Wiederherstellen der an den sekundären Standort wird gestartet, aber es ist ein mit Sysprep vorbereitete virtuelle Computer und kann nicht vollständig gestartet. RDS erfordert auch, dass die VM Herunterfahren auf, um eine in einem Pool zusammengefasste VM-Konfiguration erstellen können. Daher müssen wir diese Funktion zu deaktivieren. Wenn Sie einen einzelnen VMM-Server verfügen, ist der VM-Vorlagenname auf dem primären Replikat identisch und der sekundären Datenbank. Aus diesem Grund verwenden wir die VM-ID gemäß der *Kontext* Variable im Skript unten. Wenn Sie mehrere Vorlagen verfügen, deaktivieren sie alle.

   ```powershell
   ipmo virtualmachinemanager; 
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   } 
   ```
6. Gruppe 2 Skript 2: Entfernen Sie vorhandene in einem Pool zusammengefasste virtuelle Computer

   Sie müssen die in einem Pool zusammengefasste virtuelle Computer, auf dem primären Standort aus der Verbindungsbroker entfernen, damit neue virtuelle Computer am sekundären Standort erstellt werden können. In diesem Fall müssen Sie den genauen Host für die Erstellung den in einem Pool zusammengefasste virtuelle Computer angeben. Beachten Sie, dass dies die virtuellen Computer aus der Auflistung gelöscht werden.

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName Win8Desktops; 
   Foreach($vm in $desktops){
      Remove-RDVirtualDesktopFromCollection -CollectionName Win8Desktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }
   ```
7. Gruppe 2 manuelle Aktion: neue Vorlage zuweisen

   Sie müssen den Verbindungsbroker für die Auflistung die neue Vorlage zuweisen, sodass Sie neue in einem Pool zusammengefasste virtuelle Computer am Wiederherstellungsstandort erstellen können. Wechseln Sie zu der RDS-Verbindungsbroker und bestimmen Sie die Auflistung. Bearbeiten Sie die Eigenschaften, und geben Sie ein neues VM-Image, als der Vorlage.
8. Gruppe 2 Skript 3: Erstellen Sie alle in einem Pool zusammengefasste virtuelle Computer neu.

   Erstellen Sie die in einem Pool zusammengefasste virtuelle Computer am Wiederherstellungsstandort über den Verbindungsbroker neu. In diesem Fall müssen Sie den genauen Host für die Erstellung den in einem Pool zusammengefasste virtuelle Computer angeben.

   In einem Pool zusammengefasste VM-Name muss mit dem Präfix und Suffix eindeutig sein. Wenn Sie der VM-Namen bereits vorhanden ist, wird das Skript fehl. Auch wenn der primären Seite virtuelle Computer von 1 bis 5, nummeriert werden wird die Site Recovery Nummerierung aus 6 fortgesetzt.

   ```powershell
   ipmo RemoteDesktop; 
   Add-RDVirtualDesktopToCollection -CollectionName Win8Desktops -VirtualDesktopAllocation @{"RDVH1.contoso.com" = 1} 
   ```
9. Failovergruppe 3 – Web Access und Gateway-Server-VM

Der Wiederherstellungsplan wird wie folgt aussehen:

![Einen Notfallwiederherstellungsplan für eine RDS-Bereitstellung, bei gepoolten desktops](media/rds-asr-pooled-drplan.png)

## <a name="personal-desktops-rds-deployment"></a>Für persönliche Desktops RDS-Bereitstellung

Gruppieren Sie die VMs, damit sie in der Sequenz ist, Hinzufügen von manuellen Schritte und Skripts kommen, für eine RDS-Bereitstellung mit persönliche Desktops.

1. Failovergruppe 1: RDS Connection Broker-VM
2. Gruppe 1 manuelle Aktion - Update DNS

   Führen Sie PowerShell im erweiterten Modus, auf dem virtuellen Computer Verbindung-Broker. Führen Sie den folgenden Befehl aus, und warten Sie einige Minuten, um sicherzustellen, dass das DNS mit den neuen Wert aktualisiert wird:

   ```
   ipconfig /registerdns
   ```
3. Gruppe 1-Skript: Hinzufügen von Virtualisierungshosts
      
   Ändern Sie das folgende Skript auf jedem Virtualisierungshost in der Cloud ausführen. Nachdem Sie einen Virtualisierungshost Verbindungsbrokers hinzugefügt haben, müssen Sie in der Regel den Host neu starten. Stellen Sie sicher, dass der Host verfügt nicht über einen ausstehenden Neustart, bevor Sie das Skript ausgeführt, sonst wird fehlerhaft sein.

   ```powershell
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop; 
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com 
   ```
4. Failovergruppe 2 - Vorlagen-VM
5. Gruppe 2 Skript 1: Aktivieren Sie aus der VM-Vorlage
   
   Der Vorlagen-VM beim Wiederherstellen der an den sekundären Standort wird gestartet, aber es ist ein mit Sysprep vorbereitete virtuelle Computer und kann nicht vollständig gestartet. RDS erfordert auch, dass die VM Herunterfahren auf, um eine in einem Pool zusammengefasste VM-Konfiguration erstellen können. Daher müssen wir diese Funktion zu deaktivieren. Wenn Sie einen einzelnen VMM-Server verfügen, ist der VM-Vorlagenname auf dem primären Replikat identisch und der sekundären Datenbank. Aus diesem Grund verwenden wir die VM-ID gemäß der *Kontext* Variable im Skript unten. Wenn Sie mehrere Vorlagen verfügen, deaktivieren sie alle.

   ```powershell
   ipmo virtualmachinemanager; 
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   } 
   ```
6. Gruppe 3: Persönliche virtuelle Computer für Failover
7. 3 Skript 1: Entfernen Sie vorhandene persönliche virtuelle Computer, und fügen Sie

   Entfernen Sie die persönliche virtuelle Computer, auf dem primären Standort aus der Verbindungsbroker ein, damit neue virtuelle Computer am sekundären Standort erstellt werden können. Sie müssen die VMs Zuweisungen zu extrahieren und die virtuellen Computer erneut an den Broker für die Verbindung mit dem Hashwert der Zuweisungen hinzufügen. Nur die persönliche virtuelle Computer aus der Auflistung entfernt und erneut hinzufügen. Die Zuordnung für persönliche Desktops exportiert und importiert in der Auflistung.

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName CEODesktops; 
   Export-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com 

   Foreach($vm in $desktops){
     Remove-RDVirtualDesktopFromCollection -CollectionName CEODesktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }
   
   Import-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com 
   ```
8. Failovergruppe 3 – Web Access und Gateway-Server-VM

Ihr Plan wird wie folgt aussehen: 

![Einen Notfallwiederherstellungsplan für eine persönliche Desktops RDS-Bereitstellung](media/rds-asr-personal-desktops-drplan.png)
