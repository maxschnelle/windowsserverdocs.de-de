---
title: Aktualisieren eines direkte Speicherplätze Clusters auf Windows Server 2019
description: So führen Sie ein Upgrade für einen direkte Speicherplätze Cluster auf Windows Server 2019 durch
author: robhindman
ms.author: robhind
manager: eldenc
ms.date: 03/06/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage-spaces
ms.openlocfilehash: 09a1116b7fc1b1d0f8bc144ba9c4cf68fc45697e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402784"
---
# <a name="upgrade-a-storage-spaces-direct-cluster-to-windows-server-2019"></a>Aktualisieren eines direkte Speicherplätze Clusters auf Windows Server 2019

In diesem Thema wird beschrieben, wie ein direkte Speicherplätze-Cluster auf Windows Server 2019 aktualisiert wird. Es gibt vier Möglichkeiten, ein direkte Speicherplätze Cluster von Windows Server 2016 auf Windows Server 2019 zu aktualisieren. dabei wird der parallele [Upgradeprozess für Cluster](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md) Betriebssysteme verwendet – zwei, bei denen die VMs weiterhin ausgeführt werden, und zwei für das Beenden aller VMS. Jeder Ansatz hat unterschiedliche Stärken und Schwächen. Wählen Sie also den Ansatz aus, der den Anforderungen Ihrer Organisation am besten entspricht:

- Direktes Upgrade, während virtuelle Computer auf jedem Server im Cluster ausgeführt werden – diese Option verursacht keine VM-Ausfallzeiten, aber Sie müssen warten, bis Speicher Aufträge (Spiegelung) nach dem Upgrade der einzelnen Server **ausgeführt werden** .

- **Neuinstallation des Betriebssystems während der Ausführung** virtueller Computer auf jedem Server im Cluster – bei dieser Option sind keine VM-Ausfallzeiten aufgetreten, aber Sie müssen warten, bis Speicher Aufträge (Spiegelung) nach dem Upgrade der einzelnen Server vollständig ausgeführt werden, und Sie müssen jeden Server und alle seine Apps und Rollen.

- Direktes Upgrade, während virtuelle Computer auf jedem Server im Cluster **angehalten werden** – diese Option verursacht VM-Ausfallzeiten, aber Sie müssen nicht auf Speicher Aufträge warten (Spiegelung reparieren), sodass es schneller ist.

- **Clean-OS-Installation, während** virtuelle Computer auf jedem Server im Cluster angehalten werden – diese Option verursacht VM-Ausfallzeiten, aber Sie müssen nicht auf Speicher Aufträge warten (Spiegelung reparieren), sodass Sie schneller ist.

## <a name="prerequisites-and-limitations"></a>Voraussetzungen und Einschränkungen

Bevor Sie mit einem Upgrade fortfahren:

- Überprüfen Sie, ob Sie über verwendbare Sicherungen verfügen, falls während des Upgradevorgangs Probleme aufgetreten sind.

- Überprüfen Sie, ob der Hardwarehersteller über ein BIOS, eine Firmware und Treiber für Ihre Server verfügt, die unter Windows Server 2019 unterstützt werden.

Beim Upgradeprozess sind einige Einschränkungen zu beachten:

- Um direkte Speicherplätze mit Windows Server 2019-Builds vor 176693,292 zu aktivieren, müssen Kunden ggf. den Microsoft-Support für Registrierungsschlüssel kontaktieren, die direkte Speicherplätze und Software definierte Netzwerkfunktionen ermöglichen. Weitere Informationen finden Sie im Microsoft Knowledge Base- [Artikel 4464776](https://support.microsoft.com/help/4464776/software-defined-data-center-and-software-defined-networking).

- Beim Aktualisieren eines Clusters mit Refs-Volumes gibt es einige Einschränkungen:

- Das Upgrade wird auf Refs-Volumes vollständig unterstützt. aktualisierte Volumes profitieren jedoch nicht von den Refs-Erweiterungen in Windows Server 2019. Diese Vorteile, z. b. eine bessere Leistung für eine Spiegel beschleunigte Parität, erfordern ein neu erstelltes Windows Server 2019 Refs-Volume. Anders ausgedrückt: Sie müssen mithilfe des `New-Volume` Cmdlets oder Server-Manager neue Volumes erstellen. Im folgenden finden Sie einige der Refs-Erweiterungen, die neue Volumes erhalten würden:

    - **Map Log-Bypass**: eine Leistungsverbesserung in Refs, die nur für gruppierte Systeme (direkte Speicherplätze) gilt und nicht für eigenständige Speicherpools gilt.

    - Verbesserungen der Effizienz der **Kompatibilität** in Windows Server 2019, die für Volumes mit mehreren robusten Volumes spezifisch sind.

- Vor dem Upgrade eines Windows Server 2016 direkte Speicherplätze-Cluster Servers empfiehlt es sich, den Server in den Speicher Wartungsmodus zu versetzen. Weitere Informationen finden Sie im Abschnitt Ereignis 5120 unter Problembehandlung [direkte Speicherplätze](troubleshooting-storage-spaces.md). Obwohl dieses Problem in Windows Server 2016 behoben wurde, empfiehlt es sich, jeden direkte Speicherplätze Server während des Upgrades in den Speicher Wartungsmodus zu versetzen.

- Es gibt ein bekanntes Problem mit Software definierten Netzwerkumgebungen, in denen Set Switches verwendet werden. Dieses Problem umfasst Hyper-V-VM-Live Migrationen von Windows Server 2019 zu Windows Server 2016 (Live Migration zu einem früheren Betriebssystem). Um erfolgreiche Live Migrationen sicherzustellen, empfiehlt es sich, eine VM-Netzwerk Einstellung auf VMS zu ändern, die von Windows Server 2019 zu Windows Server 2016 migriert werden. Dieses Problem wurde für Windows Server 2019 im Hotfixrollup-Paket 2019-01D (Build 17763,292) behoben. Weitere Informationen finden Sie im Microsoft Knowledge Base- [Artikel 4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976).

Aufgrund der oben genannten bekannten Probleme können einige Kunden in Erwägung gezogen werden, einen neuen Windows Server 2019-Cluster zu entwickeln und Daten aus dem alten Cluster zu kopieren, anstatt Ihre Windows Server 2016-Cluster mit einem der vier unten beschriebenen Verfahren zu aktualisieren.

## <a name="performing-an-in-place-upgrade-while-vms-are-running"></a>Ausführen eines direkten Upgrades, während virtuelle Computer ausgeführt werden

Diese Option verursacht keine VM-Ausfallzeiten, aber Sie müssen warten, bis Speicher Aufträge (Spiegelung) nach dem Upgrade der einzelnen Server fertiggestellt werden. Obwohl einzelne Server während des Upgradevorgangs nacheinander neu gestartet werden, werden die restlichen Server im Cluster sowie alle VMs weiterhin ausgeführt.

1. Überprüfen Sie, ob auf allen Servern im Cluster die neuesten Windows-Updates installiert sind. Weitere Informationen finden Sie unter [Windows 10 und Windows Server 2016 Update History](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history). Installieren Sie mindestens den Microsoft Knowledge Base- [Artikel 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (19. Februar 2019). Die Buildnummer ( `ver` siehe Befehl) sollte 14393,2828 oder höher lauten.

2. Wenn Sie ein Software definiertes Netzwerk mit Set Switches verwenden, öffnen Sie eine PowerShell-Sitzung mit erhöhten Rechten, und führen Sie den folgenden Befehl aus, um die Überprüfung der Live Migration von virtuellen Computern auf allen virtuellen Computern im Cluster

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. Führen Sie die folgenden Schritte auf einem Cluster Server gleichzeitig aus:

   1. Verwenden Sie die Hyper-V-VM-Live Migration, um virtuelle Computer auf dem Server zu verschieben, den Sie gerade aktualisieren möchten.

   2. Halten Sie den Cluster Server mit dem folgenden PowerShell-Befehl an – beachten Sie, dass einige interne Gruppen ausgeblendet sind. Dieser Schritt wird als Vorsicht empfohlen – wenn Sie noch keine Live Migration von VMS aus dem Server durchführen, wird dieses Cmdlet dies für Sie tun, sodass Sie den vorherigen Schritt bei Bedarf überspringen können.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. Platzieren Sie den Server im Speicher Wartungsmodus, indem Sie die folgenden PowerShell-Befehle ausführen:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. Führen Sie das folgende Cmdlet aus, um zu überprüfen, ob sich der Wert **OperationalStatus** **im Wartungsmodus**befindet:

       ```PowerShell
       Get-PhysicalDisk
       ```

   5. Führen Sie eine Upgradeinstallation von Windows Server 2019 auf dem Server aus, indem Sie die Datei " **Setup. exe** " ausführen und die Option "persönliche Dateien und apps aufbewahren" verwenden. Nach Abschluss der Installation verbleibt der Server im Cluster, und der Cluster Dienst wird automatisch gestartet.

   6. Überprüfen Sie, ob der neu aktualisierte Server über die neuesten Windows Server 2019-Updates verfügt. Weitere Informationen finden Sie unter [Windows 10 und Windows Server 2019 Update History](https://support.microsoft.com/help/4464619/windows-10-update-history). Die Buildnummer ( `ver` siehe Befehl) sollte 17763,292 oder höher lauten.

   7. Entfernen Sie den Server aus dem Speicher Wartungsmodus mit dem folgenden PowerShell-Befehl:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   8. Verwenden Sie den folgenden PowerShell-Befehl, um den Server fortzusetzen:

       ```PowerShell
       Resume-ClusterNode
       ```

   9. Warten Sie, bis Speicher Reparaturaufträge abgeschlossen sind und alle Datenträger in einen fehlerfreien Status zurückversetzt werden. Dies kann je nach Anzahl der virtuellen Computer, die während des Server Upgrades ausgeführt werden, viel Zeit in Anspruch nehmen. Die folgenden Befehle müssen ausgeführt werden:

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. Aktualisieren Sie den nächsten Server im Cluster.

5. Nachdem alle Server auf Windows Server 2019 aktualisiert wurden, verwenden Sie das folgende PowerShell-Cmdlet, um die Cluster Funktionsebene zu aktualisieren.

   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > Es wird empfohlen, die Cluster Funktionsebene so bald wie möglich zu aktualisieren, obwohl Sie technisch gesehen bis zu vier Wochen dauern müssen.

6. Nachdem die Cluster Funktionsebene aktualisiert wurde, verwenden Sie das folgende Cmdlet, um den Speicherpool zu aktualisieren. An diesem Punkt sind neue Cmdlets wie z `Get-ClusterPerf` . b. auf jedem Server im Cluster voll funktionsfähig.

   ```PowerShell
   Update-StoragePool
   ```

7. Aktualisieren Sie optional VM-Konfigurationsebenen, indem Sie jeden virtuellen `Update-VMVersion` Computer mit dem Cmdlet beenden und dann die VMs erneut starten.

8. Verwenden Sie das folgende Cmdlet, um die Überprüfung der Überprüfung von virtuellen Computern zu aktivieren, wenn Sie Software-Defined Networking mit Set Switches und deaktivierte Live Migrations Prüfungen für virtuelle Computer verwenden, wie oben beschrieben.

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter  SkipMigrationDestinationCheck -Value 0
   ```

9. Überprüfen Sie, ob der aktualisierte Cluster wie erwartet funktioniert. Für Rollen sollte ein Failover ordnungsgemäß durchgeführt werden. wenn die VM-Live Migration auf dem Cluster verwendet wird, sollten die virtuellen Computer erfolgreich migriert werden

10. Überprüfen Sie den Cluster, indem Sie`Test-Cluster`die Cluster Überprüfung ausführen () und den Cluster Validierungsbericht untersuchen.

## <a name="performing-a-clean-os-installation-while-vms-are-running"></a>Ausführen einer Neuinstallation des Betriebssystems während der Ausführung virtueller Computer

Diese Option verursacht keine VM-Ausfallzeiten, aber Sie müssen warten, bis Speicher Aufträge (Spiegelung) nach dem Upgrade der einzelnen Server fertiggestellt werden. Obwohl einzelne Server während des Upgradevorgangs nacheinander neu gestartet werden, werden die restlichen Server im Cluster sowie alle VMs weiterhin ausgeführt.

1. Überprüfen Sie, ob auf allen Servern im Cluster die neuesten Updates ausgeführt werden. Weitere Informationen finden Sie unter [Windows 10 und Windows Server 2016 Update History](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history). Installieren Sie mindestens den Microsoft Knowledge Base- [Artikel 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (19. Februar 2019). Die Buildnummer ( `ver` siehe Befehl) sollte 14393,2828 oder höher lauten.

2. Wenn Sie ein Software definiertes Netzwerk mit Set Switches verwenden, öffnen Sie eine PowerShell-Sitzung mit erhöhten Rechten, und führen Sie den folgenden Befehl aus, um die Überprüfung der Live Migration von virtuellen Computern auf allen virtuellen Computern im Cluster

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. Führen Sie die folgenden Schritte auf einem Cluster Server gleichzeitig aus:

   1. Verwenden Sie die Hyper-V-VM-Live Migration, um virtuelle Computer auf dem Server zu verschieben, den Sie gerade aktualisieren möchten.

   2. Halten Sie den Cluster Server mit dem folgenden PowerShell-Befehl an – beachten Sie, dass einige interne Gruppen ausgeblendet sind. Dieser Schritt wird als Vorsicht empfohlen – wenn Sie noch keine Live Migration von VMS aus dem Server durchführen, wird dieses Cmdlet dies für Sie tun, sodass Sie den vorherigen Schritt bei Bedarf überspringen können.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. Platzieren Sie den Server im Speicher Wartungsmodus, indem Sie die folgenden PowerShell-Befehle ausführen:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. Führen Sie das folgende Cmdlet aus, um zu überprüfen, ob sich der Wert **OperationalStatus** **im Wartungsmodus**befindet:

       ```PowerShell
       Get-PhysicalDisk
       ```

   3.  Entfernen Sie den Server aus dem Cluster, indem Sie den folgenden PowerShell-Befehl ausführen:  

       ```PowerShell
       Remove-ClusterNode <ServerName>
       ```

   4. Führen Sie eine Neuinstallation von Windows Server 2019 auf dem Server aus: Formatieren Sie das Systemlaufwerk, führen Sie " **Setup. exe** " aus, und verwenden Sie die Option "Nothing". Sie müssen die Server Identität, Rollen, Features und Anwendungen konfigurieren, nachdem das Setup abgeschlossen und der Server neu gestartet wurde.

   5. Installieren Sie die Hyper-V-Rolle und das Failoverclustering-Feature auf dem Server ( `Install-WindowsFeature` Sie können das Cmdlet verwenden).

   6. Installieren Sie die neuesten Speicher-und Netzwerktreiber für Ihre Hardware, die von Ihrem Serverhersteller für die Verwendung mit direkte Speicherplätze genehmigt werden.

   7. Überprüfen Sie, ob der neu aktualisierte Server über die neuesten Windows Server 2019-Updates verfügt. Weitere Informationen finden Sie unter [Windows 10 und Windows Server 2019 Update History](https://support.microsoft.com/help/4464619/windows-10-update-history). Die Buildnummer ( `ver` siehe Befehl) sollte 17763,292 oder höher lauten.

   8. Fügen Sie den Server mit dem folgenden PowerShell-Befehl dem Cluster erneut hinzu:

       ```PowerShell
       Add-ClusterNode
       ```

   9. Entfernen Sie den Server aus dem Speicher Wartungsmodus mithilfe der folgenden PowerShell-Befehle:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   10. Warten Sie, bis Speicher Reparaturaufträge abgeschlossen sind und alle Datenträger in einen fehlerfreien Status zurückversetzt werden. Dies kann je nach Anzahl der virtuellen Computer, die während des Server Upgrades ausgeführt werden, viel Zeit in Anspruch nehmen. Die folgenden Befehle müssen ausgeführt werden:

        ```PowerShell
        Get-StorageJob
        Get-VirtualDisk
        ```

4. Aktualisieren Sie den nächsten Server im Cluster.

5. Nachdem alle Server auf Windows Server 2019 aktualisiert wurden, verwenden Sie das folgende PowerShell-Cmdlet, um die Cluster Funktionsebene zu aktualisieren.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > Es wird empfohlen, die Cluster Funktionsebene so bald wie möglich zu aktualisieren, obwohl Sie technisch gesehen bis zu vier Wochen dauern müssen.

6. Nachdem die Cluster Funktionsebene aktualisiert wurde, verwenden Sie das folgende Cmdlet, um den Speicherpool zu aktualisieren. An diesem Punkt sind neue Cmdlets wie z `Get-ClusterPerf` . b. auf jedem Server im Cluster voll funktionsfähig.

   ```PowerShell
   Update-StoragePool
   ```

7. Aktualisieren Sie optional VM-Konfigurationsebenen, indem Sie jeden virtuellen `Update-VMVersion` Computer beenden und das Cmdlet verwenden, und starten Sie die VMs dann erneut.

8. Verwenden Sie das folgende Cmdlet, um die Überprüfung der Überprüfung von virtuellen Computern zu aktivieren, wenn Sie Software-Defined Networking mit Set Switches und deaktivierte Live Migrations Prüfungen für virtuelle Computer verwenden, wie oben beschrieben.

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" | 
   Set-ClusterParameter SkipMigrationDestinationCheck -Value 0
   ```

9. Überprüfen Sie, ob der aktualisierte Cluster wie erwartet funktioniert. Für Rollen sollte ein Failover ordnungsgemäß durchgeführt werden. wenn die VM-Live Migration auf dem Cluster verwendet wird, sollten die virtuellen Computer erfolgreich migriert werden

10. Überprüfen Sie den Cluster, indem Sie`Test-Cluster`die Cluster Überprüfung ausführen () und den Cluster Validierungsbericht untersuchen.

## <a name="performing-an-in-place-upgrade-while-vms-are-stopped"></a>Ausführen eines direkten Upgrades, während virtuelle Computer angehalten werden

Diese Option verursacht VM-Ausfallzeiten, kann jedoch weniger Zeit in Anspruch nehmen, als wenn Sie die virtuellen Computer während des Upgrades beibehalten haben, da Sie nicht warten müssen, bis Speicher Aufträge (Spiegelungs Reparatur) nach jedem Upgrade des Servers ausgeführt werden. Obwohl die einzelnen Server während des Upgradevorgangs nacheinander neu gestartet werden, werden die verbleibenden Server im Cluster weiterhin ausgeführt.

1. Überprüfen Sie, ob auf allen Servern im Cluster die neuesten Updates ausgeführt werden. Weitere Informationen finden Sie unter [Windows 10 und Windows Server 2016 Update History](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history). Installieren Sie mindestens den Microsoft Knowledge Base- [Artikel 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (19. Februar 2019). Die Buildnummer ( `ver` siehe Befehl) sollte 14393,2828 oder höher lauten.

2. Beendet die virtuellen Computer, die im Cluster ausgeführt werden.

3. Führen Sie die folgenden Schritte auf einem Cluster Server gleichzeitig aus:

   1. Halten Sie den Cluster Server mit dem folgenden PowerShell-Befehl an – beachten Sie, dass einige interne Gruppen ausgeblendet sind. Es wird empfohlen, diesen Schritt vorsichtig zu machen.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   2. Platzieren Sie den Server im Speicher Wartungsmodus, indem Sie die folgenden PowerShell-Befehle ausführen:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   3. Führen Sie das folgende Cmdlet aus, um zu überprüfen, ob sich der Wert **OperationalStatus** **im Wartungsmodus**befindet:

       ```PowerShell
       Get-PhysicalDisk
       ```

   4. Führen Sie eine Upgradeinstallation von Windows Server 2019 auf dem Server aus, indem Sie die Datei " **Setup. exe** " ausführen und die Option "persönliche Dateien und apps aufbewahren" verwenden.  
   Nach Abschluss der Installation verbleibt der Server im Cluster, und der Cluster Dienst wird automatisch gestartet.

   5.  Überprüfen Sie, ob der neu aktualisierte Server über die neuesten Windows Server 2019-Updates verfügt.  
   Weitere Informationen finden Sie unter [Windows 10 und Windows Server 2019 Update History](https://support.microsoft.com/help/4464619/windows-10-update-history).
   Die Buildnummer ( `ver` siehe Befehl) sollte 17763,292 oder höher lauten.

   6.  Entfernen Sie den Server aus dem Speicher Wartungsmodus mithilfe der folgenden PowerShell-Befehle:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   7.  Verwenden Sie den folgenden PowerShell-Befehl, um den Server fortzusetzen:

       ```PowerShell
       Resume-ClusterNode
       ```

   8.  Warten Sie, bis Speicher Reparaturaufträge abgeschlossen sind und alle Datenträger in einen fehlerfreien Status zurückversetzt werden.  
   Dies sollte relativ schnell sein, da VMS nicht ausgeführt werden. Die folgenden Befehle müssen ausgeführt werden:

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. Aktualisieren Sie den nächsten Server im Cluster.
5. Nachdem alle Server auf Windows Server 2019 aktualisiert wurden, verwenden Sie das folgende PowerShell-Cmdlet, um die Cluster Funktionsebene zu aktualisieren.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   Es wird empfohlen, die Cluster Funktionsebene so bald wie möglich zu aktualisieren, obwohl Sie technisch gesehen bis zu vier Wochen dauern müssen.

6. Nachdem die Cluster Funktionsebene aktualisiert wurde, verwenden Sie das folgende Cmdlet, um den Speicherpool zu aktualisieren.  
   An diesem Punkt sind neue Cmdlets wie z `Get-ClusterPerf` . b. auf jedem Server im Cluster voll funktionsfähig.

   ```PowerShell
   Update-StoragePool
   ```

7. Starten Sie die virtuellen Computer im Cluster, und überprüfen Sie, ob Sie ordnungsgemäß ausgeführt werden.

8. Aktualisieren Sie optional VM-Konfigurationsebenen, indem Sie jeden virtuellen `Update-VMVersion` Computer beenden und das Cmdlet verwenden, und starten Sie die VMs dann erneut.

9. Überprüfen Sie, ob der aktualisierte Cluster wie erwartet funktioniert.  
   Für Rollen sollte ein Failover ordnungsgemäß durchgeführt werden. wenn die VM-Live Migration auf dem Cluster verwendet wird, sollten die virtuellen Computer erfolgreich migriert werden

10. Überprüfen Sie den Cluster, indem Sie`Test-Cluster`die Cluster Überprüfung ausführen () und den Cluster Validierungsbericht untersuchen.

## <a name="performing-a-clean-os-installation-while-vms-are-stopped"></a>Ausführen einer Neuinstallation des Betriebssystems, während virtuelle Computer angehalten werden

Diese Option verursacht VM-Ausfallzeiten, kann jedoch weniger Zeit in Anspruch nehmen, als wenn Sie die virtuellen Computer während des Upgrades beibehalten haben, da Sie nicht warten müssen, bis Speicher Aufträge (Spiegelungs Reparatur) nach jedem Upgrade des Servers ausgeführt werden. Obwohl die einzelnen Server während des Upgradevorgangs nacheinander neu gestartet werden, werden die verbleibenden Server im Cluster weiterhin ausgeführt.

1. Überprüfen Sie, ob auf allen Servern im Cluster die neuesten Updates ausgeführt werden.  
   Weitere Informationen finden Sie unter [Windows 10 und Windows Server 2016 Update History](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history).
   Installieren Sie mindestens den Microsoft Knowledge Base- [Artikel 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (19. Februar 2019). Die Buildnummer ( `ver` siehe Befehl) sollte 14393,2828 oder höher lauten.

2. Beendet die virtuellen Computer, die im Cluster ausgeführt werden.

3. Führen Sie die folgenden Schritte auf einem Cluster Server gleichzeitig aus:

   2. Halten Sie den Cluster Server mit dem folgenden PowerShell-Befehl an – beachten Sie, dass einige interne Gruppen ausgeblendet sind.  
      Es wird empfohlen, diesen Schritt vorsichtig zu machen.

       ```PowerShell
      Suspend-ClusterNode -Drain
      ```

   3. Platzieren Sie den Server im Speicher Wartungsmodus, indem Sie die folgenden PowerShell-Befehle ausführen:

      ```PowerShell
      Get-StorageFaultDomain -type StorageScaleUnit | 
      Where FriendlyName -Eq <ServerName> | 
      Enable-StorageMaintenanceMode
      ```

   4. Führen Sie das folgende Cmdlet aus, um zu überprüfen, ob sich der Wert **OperationalStatus** **im Wartungsmodus**befindet:

      ```PowerShell
      Get-PhysicalDisk
      ```

   5. Entfernen Sie den Server aus dem Cluster, indem Sie den folgenden PowerShell-Befehl ausführen:  
    
      ```PowerShell
      Remove-ClusterNode <ServerName>
      ```

   6. Führen Sie eine Neuinstallation von Windows Server 2019 auf dem Server aus: Formatieren Sie das Systemlaufwerk, führen Sie " **Setup. exe** " aus, und verwenden Sie die Option "Nothing".  
      Sie müssen die Server Identität, Rollen, Features und Anwendungen konfigurieren, nachdem das Setup abgeschlossen und der Server neu gestartet wurde.

   7. Installieren Sie die Hyper-V-Rolle und das Failoverclustering-Feature auf dem Server ( `Install-WindowsFeature` Sie können das Cmdlet verwenden).

   8. Installieren Sie die neuesten Speicher-und Netzwerktreiber für Ihre Hardware, die von Ihrem Serverhersteller für die Verwendung mit direkte Speicherplätze genehmigt werden.

   9. Überprüfen Sie, ob der neu aktualisierte Server über die neuesten Windows Server 2019-Updates verfügt.  
      Weitere Informationen finden Sie unter [Windows 10 und Windows Server 2019 Update History](https://support.microsoft.com/help/4464619/windows-10-update-history).
      Die Buildnummer ( `ver` siehe Befehl) sollte 17763,292 oder höher lauten.

   10. Fügen Sie den Server mit dem folgenden PowerShell-Befehl dem Cluster erneut hinzu:

      ```PowerShell
      Add-ClusterNode
      ```

   11. Entfernen Sie den Server aus dem Speicher Wartungsmodus mit dem folgenden PowerShell-Befehl:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   12. Warten Sie, bis Speicher Reparaturaufträge abgeschlossen sind und alle Datenträger in einen fehlerfreien Status zurückversetzt werden.  
       Dies kann je nach Anzahl der virtuellen Computer, die während des Server Upgrades ausgeführt werden, viel Zeit in Anspruch nehmen. Die folgenden Befehle müssen ausgeführt werden:

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. Aktualisieren Sie den nächsten Server im Cluster.

5. Nachdem alle Server auf Windows Server 2019 aktualisiert wurden, verwenden Sie das folgende PowerShell-Cmdlet, um die Cluster Funktionsebene zu aktualisieren.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   Es wird empfohlen, die Cluster Funktionsebene so bald wie möglich zu aktualisieren, obwohl Sie technisch gesehen bis zu vier Wochen dauern müssen.

6. Nachdem die Cluster Funktionsebene aktualisiert wurde, verwenden Sie das folgende Cmdlet, um den Speicherpool zu aktualisieren.  
   An diesem Punkt sind neue Cmdlets wie z `Get-ClusterPerf` . b. auf jedem Server im Cluster voll funktionsfähig.

   ```PowerShell
   Update-StoragePool
   ```

7. Starten Sie die virtuellen Computer im Cluster, und überprüfen Sie, ob Sie ordnungsgemäß ausgeführt werden.

8. Aktualisieren Sie optional VM-Konfigurationsebenen, indem Sie jeden virtuellen `Update-VMVersion` Computer beenden und das Cmdlet verwenden, und starten Sie die VMs dann erneut.

9. Überprüfen Sie, ob der aktualisierte Cluster wie erwartet funktioniert.  
   Für Rollen sollte ein Failover ordnungsgemäß durchgeführt werden. wenn die VM-Live Migration auf dem Cluster verwendet wird, sollten die virtuellen Computer erfolgreich migriert werden

10. Überprüfen Sie den Cluster, indem Sie`Test-Cluster`die Cluster Überprüfung ausführen () und den Cluster Validierungsbericht untersuchen.
