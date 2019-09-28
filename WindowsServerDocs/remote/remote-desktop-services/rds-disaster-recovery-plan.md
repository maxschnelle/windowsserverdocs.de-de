---
title: Erstellen des Notfallwiederherstellungs-Plans
description: Erfahre, wie du einen Notfallwiederherstellungs-Plan für deine RDS-Bereitstellung erstellst.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 05/05/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: e4e9a9ab05e672c72925e3699900218abdf1c682
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404031"
---
# <a name="create-your-disaster-recovery-plan-for-rds"></a>Erstellen des Notfallwiederherstellungs-Plans für RDS

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Du kannst in Azure Site Recovery einen Notfallwiederherstellungs-Plan erstellen, um den Failoverprozess zu automatisieren. Füge alle RDS-Komponenten-VMs dem Wiederherstellungsplan hinzu.

Erstelle deinen Wiederherstellungsplan mit folgenden Schritte in Azure:

1. Öffne den Azure Site Recovery-Tresor im Azure-Portal, und klicke dann auf **Wiederherstellungspläne**.
2. Klicke auf **Erstellen**, und gib einen Namen für den Plan ein.
3. Wähle deine **Quelle** und dein **Ziel** aus. Das Ziel ist entweder ein sekundärer RDS-Standort oder Azure.
4. Wähle die VMs aus, die deine RDS-Komponenten hosten, und klicke dann auf **OK**.

Die folgenden Abschnitte enthalten weitere Informationen zum Erstellen von Wiederherstellungsplänen für die verschiedenen RDS-Bereitstellungstypen.

## <a name="sessions-based-rds-deployment"></a>Sitzungsbasierte RDS-Bereitstellung

Gruppiere die VMs für eine sitzungsbasierte RDS-Bereitstellung, sodass sie nacheinander gestartet werden:

1. Failovergruppe 1: Sitzungshost-VM
2. Failovergruppe 2: Verbindungsbroker-VM
3. Failovergruppe 3: Webzugriff-VM

Dein Plan sieht etwa so aus: 

![Ein Notfallwiederherstellungs-Plan für eine sitzungsbasierte RDS-Bereitstellung](media/rds-asr-session-drplan.png)

## <a name="pooled-desktops-rds-deployment"></a>RDS-Bereitstellung mit in einem Pool zusammengefassten Desktops

Gruppiere die VMs bei einer RDS-Bereitstellung mit in einem Pool zusammengefassten Desktops, sodass sie nacheinander gestartet werden, und füge manuelle Schritte und Skripts hinzu.

1. Failovergruppe 1: RDS-Verbindungsbroker-VM
2. Gruppe 1 manuelle Aktion: DNS aktualisieren

   Führe PowerShell im Modus mit erhöhten Rechten auf der Verbindungsbroker-VM aus. Führe den folgenden Befehl aus, und warte einige Minuten, um sicherzustellen, dass das DNS mit den neuen Wert aktualisiert wird:

   ```
   ipconfig /registerdns
   ```
3. Gruppe 1 Skript: Virtualisierungshosts hinzufügen

   Ändere das folgende Skript, sodass es auf jedem Virtualisierungshost in der Cloud ausgeführt wird. Nachdem du einem Verbindungsbroker einen Virtualisierungshost hinzugefügt hast, musst du in der Regel den Host neu starten. Bevor das Skript ausgeführt wird, stelle sicher, dass bei dem Host kein Neustart aussteht, andernfalls tritt ein Fehler auf.

   ```
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop; 
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com 
   ```
4. Failovergruppe 2: Vorlagen-VM
5. Gruppe 2 Skript 1: Vorlagen-VM deaktivieren
   
   Die Vorlagen-VM wird gestartet, wenn sie am sekundären Standort wiederhergestellt wurde, aber für sie wurde eine Systemvorbereitung mit Sysprep durchgeführt und sie kann nicht vollständig gestartet werden. RDS erfordert auch, dass die VM heruntergefahren wird, um eine Konfiguration für in einem Pool zusammengefasste VMs auf ihrer Basis zu erstellen. Daher müssen wir sie deaktivieren. Wenn du einen einzelnen VMM-Server hast, ist der Name der Vorlagen-VM am primären und sekundären Standort identisch. Aus diesem Grund verwenden wir die VM-ID wie von der *Kontextvariablen* im folgenden Skript festgelegt. Wenn du über mehrere Vorlagen verfügst, deaktiviere alle.

   ```powershell
   ipmo virtualmachinemanager; 
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   } 
   ```
6. Gruppe 2 Skript 2: vorhandene in einem Pool zusammengefasste virtuelle Computer entfernen

   Du musst die in einem Pool zusammengefassten VMs am primären Standort aus dem Verbindungsbroker entfernen, damit am sekundären Standort neue VMs erstellt werden können. In diesem Fall musst du den genauen Host angeben, auf dem die in einem Pool zusammengefassten virtuellen Computer erstellt werden sollen. Beachte, dass die virtuellen Computer damit nur aus der Sammlung gelöscht werden.

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName Win8Desktops; 
   Foreach($vm in $desktops){
      Remove-RDVirtualDesktopFromCollection -CollectionName Win8Desktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }
   ```
7. Gruppe 2 manuelle Aktion: neue Vorlage zuweisen

   Du musst die neue Vorlage dem Verbindungsbroker für die Sammlung zuordnen, damit du neue in einem Pool zusammengefasste VMs am Wiederherstellungsstandort erstellen kannst. Wechsele zum RDS-Verbindungsbroker, und bestimme die Sammlung. Bearbeite die Eigenschaften, und gib ein neues VM-Image als Vorlage an.
8. Gruppe 2 Skript 3: alle in einem Pool zusammengefassten virtuellen Computer neu erstellen

   Erstelle die in einem Pool zusammengefassten virtuellen Computer am Wiederherstellungsstandort über den Verbindungsbroker neu. In diesem Fall musst du den genauen Host angeben, auf dem die in einem Pool zusammengefassten virtuellen Computer erstellt werden sollen.

   Die Namen der in einem Pool zusammengefassten VMs müssen unter Verwendung von Präfix und Suffix eindeutig sein. Wenn der VM-Name bereits vorhanden ist, tritt bei der Skriptausführung ein Fehler auf. Außerdem: Wenn die VMs am primären Standort von 1-5 nummeriert sind, wird die Nummerierung am Wiederherstellungsstandort mit 6 fortgesetzt.

   ```powershell
   ipmo RemoteDesktop; 
   Add-RDVirtualDesktopToCollection -CollectionName Win8Desktops -VirtualDesktopAllocation @{"RDVH1.contoso.com" = 1} 
   ```
9. Failovergruppe 3: Webzugriff und Gatewayserver-VM

Der Wiederherstellungsplan wird wie folgt aussehen:

![Ein Notfallwiederherstellungs-Plan für eine RDS-Bereitstellung mit in einem Pool zusammengefassten Desktops](media/rds-asr-pooled-drplan.png)

## <a name="personal-desktops-rds-deployment"></a>RDS-Bereitstellung mit persönlichen Desktops

Gruppiere die VMs bei einer RDS-Bereitstellung mit persönlichen Desktops, sodass sie nacheinander gestartet werden, und füge manuelle Schritte und Skripts hinzu.

1. Failovergruppe 1: RDS-Verbindungsbroker-VM
2. Gruppe 1 manuelle Aktion: DNS aktualisieren

   Führe PowerShell im Modus mit erhöhten Rechten auf der Verbindungsbroker-VM aus. Führe den folgenden Befehl aus, und warte einige Minuten, um sicherzustellen, dass das DNS mit den neuen Wert aktualisiert wird:

   ```
   ipconfig /registerdns
   ```
3. Gruppe 1 Skript: Virtualisierungshosts hinzufügen
      
   Ändere das folgende Skript, sodass es auf jedem Virtualisierungshost in der Cloud ausgeführt wird. Nachdem du einem Verbindungsbroker einen Virtualisierungshost hinzugefügt hast, musst du in der Regel den Host neu starten. Bevor das Skript ausgeführt wird, stelle sicher, dass bei dem Host kein Neustart aussteht, andernfalls tritt ein Fehler auf.

   ```powershell
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop; 
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com 
   ```
4. Failovergruppe 2: Vorlagen-VM
5. Gruppe 2 Skript 1: Vorlagen-VM deaktivieren
   
   Die Vorlagen-VM wird gestartet, wenn sie am sekundären Standort wiederhergestellt wurde, aber für sie wurde eine Systemvorbereitung mit Sysprep durchgeführt und sie kann nicht vollständig gestartet werden. RDS erfordert auch, dass die VM heruntergefahren wird, um eine Konfiguration für in einem Pool zusammengefasste VMs auf ihrer Basis zu erstellen. Daher müssen wir sie deaktivieren. Wenn du einen einzelnen VMM-Server hast, ist der Name der Vorlagen-VM am primären und sekundären Standort identisch. Aus diesem Grund verwenden wir die VM-ID wie von der *Kontextvariablen* im folgenden Skript festgelegt. Wenn du über mehrere Vorlagen verfügst, deaktiviere alle.

   ```powershell
   ipmo virtualmachinemanager; 
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   } 
   ```
6. Failovergruppe 3: Persönliche virtuelle Computer
7. Gruppe 3 Skript 1: vorhandene persönliche virtuelle Computer entfernen und hinzufügen

   Entferne die persönlichen VMs am primären Standort aus dem Verbindungsbroker, damit am sekundären Standort neue VMs erstellt werden können. Du musst die Zuweisungen der VMs extrahieren und die virtuellen Computer mit dem Zuweisungenhash erneut dem Verbindungsbroker hinzufügen. Damit werden nur die persönlichen virtuellen Computer aus der Sammlung entfernt und erneut hinzugefügt. Die Zuordnung des persönlichen Desktops wird exportiert und wieder in die Sammlung importiert.

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName CEODesktops; 
   Export-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com 

   Foreach($vm in $desktops){
     Remove-RDVirtualDesktopFromCollection -CollectionName CEODesktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }
   
   Import-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com 
   ```
8. Failovergruppe 3: Webzugriff und Gatewayserver-VM

Dein Plan sieht etwa so aus: 

![Ein Notfallwiederherstellungs-Plan für eine RDS-Bereitstellung mit persönlichen Desktops](media/rds-asr-personal-desktops-drplan.png)
