---
title: Upgrade von "direkte Speicherplätze"-Clustern auf Windows Server-2019
description: Informationen zum upgrade von "direkte Speicherplätze"-Clustern auf Windows Server 2019 – entweder gleichzeitig ausgeführten virtuellen Computer oder während sie angehalten sind.
author: robhindman
ms.author: robhind
manager: eldenc
ms.date: 03/06/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-spaces
ms.openlocfilehash: 9db92aa33cde9b2beed11149dae06bb3af2b5a03
ms.sourcegitcommit: fe621b72d45d0259bac1d5b9031deed3dcbed29d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2019
ms.locfileid: "66455410"
---
# <a name="upgrade-a-storage-spaces-direct-cluster-to-windows-server-2019"></a>Upgrade von "direkte Speicherplätze"-Clustern auf Windows Server-2019

In diesem Thema wird beschrieben, wie Sie einen "direkte Speicherplätze"-Cluster auf Windows Server-2019 aktualisieren. Es gibt vier Möglichkeiten für die Aktualisierung von "direkte Speicherplätze"-Cluster von Windows Server 2016 zu WindowsServer 2019, mit der [cluster OS rolling Upgrade Process](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md) – zwei, bei denen die ausgeführten virtuellen Computer beibehalten und zwei, bei denen Beenden alle virtuellen Computer. Jeder Ansatz hat jeweils eigene Stärken und Schwächen, also, dass ein auswählen, die die Anforderungen Ihrer Organisation am besten entspricht:

- **Direktes Upgrade während der virtuelle Computer ausgeführt werden** auf jedem Server im Cluster – diese Option fallen keine VM-Ausfallzeiten, aber Sie müssen warten, bis speicheraufträge (Spiegel reparieren) abschließen, nachdem Sie jeden Server aktualisiert wird.

- **Bereinigung-OS-Installation während der virtuelle Computer ausgeführt werden** auf jedem Server im Cluster – diese Option fallen keine VM-Ausfallzeit, aber Sie müssen warten, speicheraufträge (Spiegel reparieren) abschließen, nachdem Sie jeden Server wird aktualisiert, und Sie müssen Festlegen von jedem Server und alle die apps und die Rollen noch mal.

- **Direktes Upgrade während der virtuelle Computer beendet wurden** auf jedem Server im Cluster – diese Option kommt es zu VM-Ausfällen, aber Sie müssen nicht warten, Speicher (Spiegel reparieren), Aufträge, sodass es schneller ist.

- **Bereinigen und Betriebssystem zu installieren, während der virtuelle Computer beendet wurden** auf jedem Server im Cluster – diese Option kommt es zu VM-Ausfällen, aber Sie müssen nicht warten, Speicher (Spiegel reparieren) Aufträge, sodass es schneller ist.

## <a name="prerequisites-and-limitations"></a>Voraussetzungen und Einschränkungen

Bevor Sie ein Upgrade fortsetzen:

- Überprüfen Sie, dass Sie verwendet werden, Backups verfügen, für den Fall, dass während des Upgradevorgangs Probleme vorliegen.

- Überprüfen, ob Ihre Hardwarehersteller enthält ein BIOS, Firmware und Treiber für Ihre Server, die sie auf Windows Server-2019 unterstützt.

Es gibt einige Einschränkungen bei der Upgradevorgang zu beachten:

- Um "direkte Speicherplätze" mit Windows Server-2019 Builds vor 176693.292 zu aktivieren, müssen Kunden den Microsoft-Support für Registrierungsschlüssel, die "direkte Speicherplätze" und Software Defined Networking-Funktionalität zu aktivieren. Weitere Informationen finden Sie im Microsoft Knowledge Base [Artikel 4464776](https://support.microsoft.com/help/4464776/software-defined-data-center-and-software-defined-networking).

- Wenn Sie einen Cluster mit ReFS-Volumes zu aktualisieren, gibt es jedoch einige Einschränkungen:

- Upgrade wird vollständig auf ReFS-Volumes unterstützt, die aktualisierten Volumes wird nicht profitieren jedoch von ReFS-Verbesserungen in Windows Server-2019. Diese Vorteile, z. B. verbessert die Leistung bei Parität Mirror-Beschleunigung, erfordern eine neu erstellte Windows Server 2019 ReFS-Volume. Das heißt, müssen Sie das Erstellen neuer Volumes, die mit der `New-Volume` Cmdlet oder Server-Manager. Hier sind einige der ReFS-Verbesserungen, die neuen Volumes erhalten würden:

    - **MAP-Log-Umgehung**: eine leistungsverbesserung in ReFS, die gilt nur für Clustersystemen (Storage Spaces Direct) und gilt nicht für eigenständige Speicherpools.

    - **Komprimierung** Effizienz-Verbesserungen in Windows Server-2019, die auf mehreren robuste Volumes spezifisch sind.

- Es wird empfohlen, vor dem Upgrade von eines Windows Server 2016 "direkte Speicherplätze"-Cluster-Servers, platzieren den Server in den Wartungsmodus für Speicher. Weitere Informationen finden Sie im Abschnitt Ereignis 5120 [Problembehandlung für "direkte Speicherplätze"](troubleshooting-storage-spaces.md). Obwohl dieses Problem in Windows Server 2016 behoben wurde, wird empfohlen, Sie jedes "direkte Speicherplätze"-Server während des Upgrades als bewährte Methode in den speicherwartungsmodus einsetzen.

- Es gibt ein bekanntes Problem mit der Software Defined Networking-Umgebungen, die SET-Schalter verwenden. Dieses Problem umfasst die Hyper-V-VM live-Migrationen von Windows Server-2019 auf Windows Server 2016 (live Migration zu einem früheren Betriebssystem). Es wird empfohlen, um sicherzustellen, dass erfolgreiche livemigrationen, Ändern einer Einstellung des VM-Netzwerk auf virtuellen Computern, die live-Migration von Windows Server-2019 auf Windows Server 2016. Dieses Problem wurde im 2019-01-D-Hotfix Rollup Package für Windows Server-2019 behoben, auch bekannt als 17763.292 zu erstellen. Weitere Informationen finden Sie im Microsoft Knowledge Base [Artikel 4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976).

Aufgrund der oben genannten bekannten Problemen sollten einige Kunden, erstellen einen neuen 2019 für Windows Server-Cluster, und Kopieren von Daten aus dem alten Cluster, anstelle eines Upgrade ihrer Windows Server 2016-Cluster mithilfe einer der vier nachfolgend beschriebenen Prozesse.

## <a name="performing-an-in-place-upgrade-while-vms-are-running"></a>Ein direktes Upgrade ausführen, während die virtuellen Computer ausgeführt werden

Diese Option fallen keine VM-Ausfallzeiten, aber Sie müssen warten, bis speicheraufträge (Spiegel reparieren) abschließen, nachdem Sie jeden Server aktualisiert wird. Obwohl einzelne Server nacheinander während des Upgrades neu gestartet werden, werden die verbleibenden Server im Cluster sowie alle VMs weiterhin ausgeführt.

1. Überprüfen Sie, dass alle Server im Cluster die neuesten Windows-Updates installiert haben. Weitere Informationen finden Sie unter [Windows 10- und Windows Server 2016-Updateverlauf](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history). Installieren Sie mindestens die Microsoft Knowledge Base [Artikel 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (19. Februar 2019). Die Nummer des Builds (finden Sie unter `ver` Befehl) 14393.2828 oder höher sein.

2. Wenn Sie Software Defined Networking mit SET-Optionen verwenden, öffnen Sie eine PowerShell-Sitzung mit erhöhten Rechten, und führen Sie den folgenden Befehl zum Deaktivieren von Überprüfungen der Livemigration auf allen virtuellen Computern im Cluster virtuelle Computer:

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. Führen Sie die folgenden Schritte auf einem Clusterserver zu einem Zeitpunkt:

   1. Verwenden Sie Hyper-V-VM-Livemigration zum Verschieben von ausgeführten virtuellen Computer vom Server an, das Sie aktualisieren möchten.

   2. Halten Sie den Clusterserver mit dem folgenden PowerShell-Befehl – Beachten Sie, dass einige interne Gruppen ausgeblendet sind. Es wird empfohlen, diesen Schritt, vorsichtig zu sein, wenn Sie nicht bereits Online geschaltete Migrieren von VMs aus dem Server, die mit diesem Cmdlet tun, also können Sie den vorherigen Schritt übergehen können nach Wunsch.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. Platzieren Sie den Server in den Wartungsmodus für Speicher, durch die folgenden PowerShell-Befehle ausführen:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. Führen Sie das folgende Cmdlet aus, um zu überprüfen, die die **OperationalStatus** Wert **im Wartungsmodus**:

       ```PowerShell
       Get-PhysicalDisk
       ```

   5. Führen Sie eine Upgrade-Installation von Windows Server-2019 auf dem Server mit **setup.exe** und mit der Option "Bleiben persönlichen Dateien und apps". Nachdem die Installation abgeschlossen ist,-Dienst verbleibt der Server in den Cluster und den Cluster automatisch gestartet wird.

   6. Überprüfen Sie, dass der neu aktualisierte Server die neuesten Updates für Windows Server-2019 verfügt. Weitere Informationen finden Sie unter [Windows 10- und Windows Server-2019 Updateverlauf](https://support.microsoft.com/help/4464619/windows-10-update-history). Die Nummer des Builds (finden Sie unter `ver` Befehl) 17763.292 oder höher sein.

   7. Entfernen Sie den Server aus dem Wartungsmodus von Speicher mithilfe des folgenden PowerShell-Befehl:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   8. Fortsetzen Sie den Server mit dem folgenden PowerShell-Befehl:

       ```PowerShell
       Resume-ClusterNode
       ```

   9. Warten Sie, für die Reparatur speicheraufträge abgeschlossen und für alle Datenträger in einen fehlerfreien Status wiederherzustellen. Dies kann sehr viel Zeit abhängig von der Anzahl von virtuellen Computern dauern, während der serveraktualisierung ausgeführt wird. Hier sind die auszuführenden Befehle an:

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. Aktualisieren Sie den nächsten Server im Cluster.

5. Nachdem alle Server auf Windows Server-2019 aktualisiert wurden, verwenden Sie das folgende PowerShell-Cmdlet, um Funktionsebene des Clusters aktualisieren.

   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > Obwohl technisch bis zu vier Wochen haben dazu sollten so bald wie möglich, Funktionsebene des Clusters zu aktualisieren.

6. Nach der Funktionsebene des Clusters aktualisiert wurde, verwenden Sie das folgende Cmdlet aus, um den Speicherpool zu aktualisieren. Nun, neue Cmdlets, z. B. `Get-ClusterPerf` werden auf einem beliebigen Server im Cluster voll funktionsfähig.

   ```PowerShell
   Update-StoragePool
   ```

7. Optional ein upgrade auf VM-Konfigurationsebenen durch das Beenden von jedem virtuellen Computer mithilfe der `Update-VMVersion` -Cmdlet, und klicken Sie dann die virtuellen Computer neu zu starten.

8. Wenn Sie Software Defined Networking mit SET-Switches und deaktivierte Überprüfungen der VM-live-Migration wie an weiter oben beschrieben das folgende Cmdlet verwenden um Überprüfungen der Live-VM erneut zu aktivieren:

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter  SkipMigrationDestinationCheck -Value 0
   ```

9. Stellen Sie sicher, dass die aktualisierte Cluster wie erwartet funktioniert. Rollen sollten Failover ordnungsgemäß, und wenn live Migration von virtuellen Computern im Cluster verwendet wird, sollte erfolgreich live-VMs migrieren.

10. Überprüfen des Clusters durch Ausführen der Clusterüberprüfung (`Test-Cluster`) und untersuchen den Bericht der clustervalidierung.

## <a name="performing-a-clean-os-installation-while-vms-are-running"></a>Eine Neuinstallation des Betriebssystems ausführen, während die virtuellen Computer ausgeführt werden

Diese Option fallen keine VM-Ausfallzeiten, aber Sie müssen warten, bis speicheraufträge (Spiegel reparieren) abschließen, nachdem Sie jeden Server aktualisiert wird. Obwohl einzelne Server nacheinander während des Upgrades neu gestartet werden, werden die verbleibenden Server im Cluster sowie alle VMs weiterhin ausgeführt.

1. Überprüfen Sie, dass alle Server im Cluster die neuesten Updates ausgeführt werden. Weitere Informationen finden Sie unter [Windows 10- und Windows Server 2016-Updateverlauf](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history). Installieren Sie mindestens die Microsoft Knowledge Base [Artikel 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (19. Februar 2019). Die Nummer des Builds (finden Sie unter `ver` Befehl) 14393.2828 oder höher sein.

2. Wenn Sie Software Defined Networking mit SET-Optionen verwenden, öffnen Sie eine PowerShell-Sitzung mit erhöhten Rechten, und führen Sie den folgenden Befehl zum Deaktivieren von Überprüfungen der Livemigration auf allen virtuellen Computern im Cluster virtuelle Computer:

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. Führen Sie die folgenden Schritte auf einem Clusterserver zu einem Zeitpunkt:

   1. Verwenden Sie Hyper-V-VM-Livemigration zum Verschieben von ausgeführten virtuellen Computer vom Server an, das Sie aktualisieren möchten.

   2. Halten Sie den Clusterserver mit dem folgenden PowerShell-Befehl – Beachten Sie, dass einige interne Gruppen ausgeblendet sind. Es wird empfohlen, diesen Schritt, vorsichtig zu sein, wenn Sie nicht bereits Online geschaltete Migrieren von VMs aus dem Server, die mit diesem Cmdlet tun, also können Sie den vorherigen Schritt übergehen können nach Wunsch.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. Platzieren Sie den Server in den Wartungsmodus für Speicher, durch die folgenden PowerShell-Befehle ausführen:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. Führen Sie das folgende Cmdlet aus, um zu überprüfen, die die **OperationalStatus** Wert **im Wartungsmodus**:

       ```PowerShell
       Get-PhysicalDisk
       ```

   3.  Entfernen Sie den Server aus dem Cluster, durch den folgenden PowerShell-Befehl ausführen:  

       ```PowerShell
       Remove-ClusterNode <ServerName>
       ```

   4. Führen Sie auf dem Server eine Neuinstallation von Windows Server-2019: Format das Systemlaufwerk ausführen **setup.exe** und verwenden Sie den Text "Nothing" Option. Sie müssen die Identität des Servers, Rollen, Features und Anwendungen, die nach Abschluss der Installation und Neustart des Servers zu konfigurieren.

   5. Installieren der Hyper-V-Rolle und Feature Failoverclustering auf dem Server (Sie können die `Install-WindowsFeature` Cmdlet).

   6. Installieren Sie die neuesten Speicher- und Netzwerkressourcen Treiber für Ihre Hardware, die durch den Serverhersteller Ihres für die Verwendung mit "direkte Speicherplätze" genehmigt werden.

   7. Überprüfen Sie, dass der neu aktualisierte Server die neuesten Updates für Windows Server-2019 verfügt. Weitere Informationen finden Sie unter [Windows 10- und Windows Server-2019 Updateverlauf](https://support.microsoft.com/help/4464619/windows-10-update-history). Die Nummer des Builds (finden Sie unter `ver` Befehl) 17763.292 oder höher sein.

   8. Eingebunden Sie den Server mit dem Cluster wieder werden, mithilfe des folgenden PowerShell-Befehl:

       ```PowerShell
       Add-ClusterNode
       ```

   9. Entfernen Sie den Server aus dem speicherwartungsmodus mithilfe des folgenden PowerShell-Befehle ein:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   10. Warten Sie, für die Reparatur speicheraufträge abgeschlossen und für alle Datenträger in einen fehlerfreien Status wiederherzustellen. Dies kann sehr viel Zeit abhängig von der Anzahl von virtuellen Computern dauern, während der serveraktualisierung ausgeführt wird. Hier sind die auszuführenden Befehle an:

        ```PowerShell
        Get-StorageJob
        Get-VirtualDisk
        ```

4. Aktualisieren Sie den nächsten Server im Cluster.

5. Nachdem alle Server auf Windows Server-2019 aktualisiert wurden, verwenden Sie das folgende PowerShell-Cmdlet, um Funktionsebene des Clusters aktualisieren.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > Obwohl technisch bis zu vier Wochen haben dazu sollten so bald wie möglich, Funktionsebene des Clusters zu aktualisieren.

6. Nach der Funktionsebene des Clusters aktualisiert wurde, verwenden Sie das folgende Cmdlet aus, um den Speicherpool zu aktualisieren. Nun, neue Cmdlets, z. B. `Get-ClusterPerf` werden auf einem beliebigen Server im Cluster voll funktionsfähig.

   ```PowerShell
   Update-StoragePool
   ```

7. Ebenen der VM-Konfiguration bei Bedarf aktualisieren, indem Sie jeden virtuellen Computer beenden und die `Update-VMVersion` -Cmdlet, und klicken Sie dann die virtuellen Computer neu zu starten.

8. Wenn Sie Software Defined Networking mit SET-Switches und deaktivierte Überprüfungen der VM-live-Migration wie an weiter oben beschrieben das folgende Cmdlet verwenden um Überprüfungen der Live-VM erneut zu aktivieren:

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" | 
   Set-ClusterParameter SkipMigrationDestinationCheck -Value 0
   ```

9. Stellen Sie sicher, dass die aktualisierte Cluster wie erwartet funktioniert. Rollen sollten Failover ordnungsgemäß, und wenn live Migration von virtuellen Computern im Cluster verwendet wird, sollte erfolgreich live-VMs migrieren.

10. Überprüfen des Clusters durch Ausführen der Clusterüberprüfung (`Test-Cluster`) und untersuchen den Bericht der clustervalidierung.

## <a name="performing-an-in-place-upgrade-while-vms-are-stopped"></a>Ein direktes Upgrade ausführen, während der virtuelle Computer beendet wurden

Diese Option kann kommt es zu Ausfällen der virtuellen Computer jedoch weniger Zeit als beibehalten, wenn Sie die virtuellen Computer während des Upgrades ausgeführt werden, da Sie keine speicheraufträge (Spiegel reparieren) abschließen, nachdem das Upgrade der einzelnen Server warten müssen. Obwohl einzelne Server nacheinander während des Upgrades neu gestartet werden, weiterhin die verbleibenden Server im Cluster ausgeführt wird.

1. Überprüfen Sie, dass alle Server im Cluster die neuesten Updates ausgeführt werden. Weitere Informationen finden Sie unter [Windows 10- und Windows Server 2016-Updateverlauf](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history). Installieren Sie mindestens die Microsoft Knowledge Base [Artikel 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (19. Februar 2019). Die Nummer des Builds (finden Sie unter `ver` Befehl) 14393.2828 oder höher sein.

2. Beenden Sie die virtuellen Computern im Cluster ausgeführt.

3. Führen Sie die folgenden Schritte auf einem Clusterserver zu einem Zeitpunkt:

   1. Halten Sie den Clusterserver mit dem folgenden PowerShell-Befehl – Beachten Sie, dass einige interne Gruppen ausgeblendet sind. Es wird empfohlen, diesen Schritt, vorsichtig zu sein.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   2. Platzieren Sie den Server in den Wartungsmodus für Speicher, durch die folgenden PowerShell-Befehle ausführen:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   3. Führen Sie das folgende Cmdlet aus, um zu überprüfen, die die **OperationalStatus** Wert **im Wartungsmodus**:

       ```PowerShell
       Get-PhysicalDisk
       ```

   4. Führen Sie eine Upgrade-Installation von Windows Server-2019 auf dem Server mit **setup.exe** und mit der Option "Bleiben persönlichen Dateien und apps".  
   Nachdem die Installation abgeschlossen ist,-Dienst verbleibt der Server in den Cluster und den Cluster automatisch gestartet wird.

   5.  Überprüfen Sie, dass der neu aktualisierte Server die neuesten Updates für Windows Server-2019 verfügt.  
   Weitere Informationen finden Sie unter [Windows 10- und Windows Server-2019 Updateverlauf](https://support.microsoft.com/help/4464619/windows-10-update-history).
   Die Nummer des Builds (finden Sie unter `ver` Befehl) 17763.292 oder höher sein.

   6.  Entfernen Sie den Server aus dem speicherwartungsmodus mithilfe des folgenden PowerShell-Befehle ein:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   7.  Fortsetzen Sie den Server mit dem folgenden PowerShell-Befehl:

       ```PowerShell
       Resume-ClusterNode
       ```

   8.  Warten Sie, für die Reparatur speicheraufträge abgeschlossen und für alle Datenträger in einen fehlerfreien Status wiederherzustellen.  
   Dies sollte relativ schnell, da die virtuellen Computer nicht ausgeführt werden. Hier sind die auszuführenden Befehle an:

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. Aktualisieren Sie den nächsten Server im Cluster.
5. Nachdem alle Server auf Windows Server-2019 aktualisiert wurden, verwenden Sie das folgende PowerShell-Cmdlet, um Funktionsebene des Clusters aktualisieren.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   Obwohl technisch bis zu vier Wochen haben dazu sollten so bald wie möglich, Funktionsebene des Clusters zu aktualisieren.

6. Nach der Funktionsebene des Clusters aktualisiert wurde, verwenden Sie das folgende Cmdlet aus, um den Speicherpool zu aktualisieren.  
   Nun, neue Cmdlets, z. B. `Get-ClusterPerf` werden auf einem beliebigen Server im Cluster voll funktionsfähig.

   ```PowerShell
   Update-StoragePool
   ```

7. Starten Sie die virtuellen Computern im Cluster, und überprüfen Sie, dass sie ordnungsgemäß arbeiten.

8. Ebenen der VM-Konfiguration bei Bedarf aktualisieren, indem Sie jeden virtuellen Computer beenden und die `Update-VMVersion` -Cmdlet, und klicken Sie dann die virtuellen Computer neu zu starten.

9. Stellen Sie sicher, dass die aktualisierte Cluster wie erwartet funktioniert.  
   Rollen sollten Failover ordnungsgemäß, und wenn live Migration von virtuellen Computern im Cluster verwendet wird, sollte erfolgreich live-VMs migrieren.

10. Überprüfen des Clusters durch Ausführen der Clusterüberprüfung (`Test-Cluster`) und untersuchen den Bericht der clustervalidierung.

## <a name="performing-a-clean-os-installation-while-vms-are-stopped"></a>Eine Neuinstallation des Betriebssystems ausführen, während der virtuelle Computer beendet wurden

Diese Option kann kommt es zu Ausfällen der virtuellen Computer jedoch weniger Zeit als beibehalten, wenn Sie die virtuellen Computer während des Upgrades ausgeführt werden, da Sie keine speicheraufträge (Spiegel reparieren) abschließen, nachdem das Upgrade der einzelnen Server warten müssen. Obwohl einzelne Server nacheinander während des Upgrades neu gestartet werden, weiterhin die verbleibenden Server im Cluster ausgeführt wird.

1. Überprüfen Sie, dass alle Server im Cluster die neuesten Updates ausgeführt werden.  
   Weitere Informationen finden Sie unter [Windows 10- und Windows Server 2016-Updateverlauf](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history).
   Installieren Sie mindestens die Microsoft Knowledge Base [Artikel 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (19. Februar 2019). Die Nummer des Builds (finden Sie unter `ver` Befehl) 14393.2828 oder höher sein.

2. Beenden Sie die virtuellen Computern im Cluster ausgeführt.

3. Führen Sie die folgenden Schritte auf einem Clusterserver zu einem Zeitpunkt:

   2. Halten Sie den Clusterserver mit dem folgenden PowerShell-Befehl – Beachten Sie, dass einige interne Gruppen ausgeblendet sind.  
      Es wird empfohlen, diesen Schritt, vorsichtig zu sein.

       ```PowerShell
      Suspend-ClusterNode -Drain
      ```

   3. Platzieren Sie den Server in den Wartungsmodus für Speicher, durch die folgenden PowerShell-Befehle ausführen:

      ```PowerShell
      Get-StorageFaultDomain -type StorageScaleUnit | 
      Where FriendlyName -Eq <ServerName> | 
      Enable-StorageMaintenanceMode
      ```

   4. Führen Sie das folgende Cmdlet aus, um zu überprüfen, die die **OperationalStatus** Wert **im Wartungsmodus**:

      ```PowerShell
      Get-PhysicalDisk
      ```

   5. Entfernen Sie den Server aus dem Cluster, durch den folgenden PowerShell-Befehl ausführen:  
    
      ```PowerShell
      Remove-ClusterNode <ServerName>
      ```

   6. Führen Sie auf dem Server eine Neuinstallation von Windows Server-2019: Format das Systemlaufwerk ausführen **setup.exe** und verwenden Sie den Text "Nothing" Option.  
      Sie müssen die Identität des Servers, Rollen, Features und Anwendungen, die nach Abschluss der Installation und Neustart des Servers zu konfigurieren.

   7. Installieren der Hyper-V-Rolle und Feature Failoverclustering auf dem Server (Sie können die `Install-WindowsFeature` Cmdlet).

   8. Installieren Sie die neuesten Speicher- und Netzwerkressourcen Treiber für Ihre Hardware, die durch den Serverhersteller Ihres für die Verwendung mit "direkte Speicherplätze" genehmigt werden.

   9. Überprüfen Sie, dass der neu aktualisierte Server die neuesten Updates für Windows Server-2019 verfügt.  
      Weitere Informationen finden Sie unter [Windows 10- und Windows Server-2019 Updateverlauf](https://support.microsoft.com/help/4464619/windows-10-update-history).
      Die Nummer des Builds (finden Sie unter `ver` Befehl) 17763.292 oder höher sein.

   10. Eingebunden Sie den Server mit dem Cluster wieder werden, mithilfe des folgenden PowerShell-Befehl:

      ```PowerShell
      Add-ClusterNode
      ```

   11. Entfernen Sie den Server aus dem Wartungsmodus von Speicher mithilfe des folgenden PowerShell-Befehl:

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   12. Warten Sie, für die Reparatur speicheraufträge abgeschlossen und für alle Datenträger in einen fehlerfreien Status wiederherzustellen.  
       Dies kann sehr viel Zeit abhängig von der Anzahl von virtuellen Computern dauern, während der serveraktualisierung ausgeführt wird. Hier sind die auszuführenden Befehle an:

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. Aktualisieren Sie den nächsten Server im Cluster.

5. Nachdem alle Server auf Windows Server-2019 aktualisiert wurden, verwenden Sie das folgende PowerShell-Cmdlet, um Funktionsebene des Clusters aktualisieren.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   Obwohl technisch bis zu vier Wochen haben dazu sollten so bald wie möglich, Funktionsebene des Clusters zu aktualisieren.

6. Nach der Funktionsebene des Clusters aktualisiert wurde, verwenden Sie das folgende Cmdlet aus, um den Speicherpool zu aktualisieren.  
   Nun, neue Cmdlets, z. B. `Get-ClusterPerf` werden auf einem beliebigen Server im Cluster voll funktionsfähig.

   ```PowerShell
   Update-StoragePool
   ```

7. Starten Sie die virtuellen Computern im Cluster, und überprüfen Sie, dass sie ordnungsgemäß arbeiten.

8. Ebenen der VM-Konfiguration bei Bedarf aktualisieren, indem Sie jeden virtuellen Computer beenden und die `Update-VMVersion` -Cmdlet, und klicken Sie dann die virtuellen Computer neu zu starten.

9. Stellen Sie sicher, dass die aktualisierte Cluster wie erwartet funktioniert.  
   Rollen sollten Failover ordnungsgemäß, und wenn live Migration von virtuellen Computern im Cluster verwendet wird, sollte erfolgreich live-VMs migrieren.

10. Überprüfen des Clusters durch Ausführen der Clusterüberprüfung (`Test-Cluster`) und untersuchen den Bericht der clustervalidierung.
