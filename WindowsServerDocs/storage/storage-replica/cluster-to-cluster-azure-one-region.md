---
title: Cluster-zu-Cluster Storage Replica innerhalb desselben Bereichs in Azure
description: Cluster-zu-Cluster-Speicherreplikation innerhalb derselben Region in Azure
keywords: Funktion "Speicherreplikat", Server-Manager, Windows Server, Azure, Cluster, der gleichen region
author: arduppal
ms.author: arduppal
ms.date: 12/19/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: 8dbfab96404f5c98b9861476c0bc654af1bda775
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829141"
---
# <a name="cluster-to-cluster-storage-replica-within-the-same-region-in-azure"></a>Cluster-zu-Cluster Storage Replica innerhalb desselben Bereichs in Azure
Sie können die Cluster-zu-Cluster von Speicherreplikaten in derselben Region in Azure konfigurieren. Klicken Sie in den folgenden Beispielen verwenden wir einen Cluster mit zwei Knoten, aber Cluster-zu-Cluster-Funktion "speicherreplikat" ist nicht auf einen Cluster mit zwei Knoten beschränkt. In der folgenden Abbildung ist ein Storage Space Direct Cluster mit zwei Knoten, die miteinander kommunizieren können sind Sie in der gleichen Domäne, und klicken Sie in der gleichen Region.

Sehen Sie sich die Videos unten für eine vollständige Exemplarische Vorgehensweise des Prozesses.

Teil 1
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE26f2Y]

Teil 2
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE269Pq]

![Das Architekturdiagramm mit der Funktion "Speicherreplikat" Cluster-zu-Cluster in Azure innerhalb derselben Region.](media\Cluster-to-cluster-azure-one-region\architecture.png)
> [!IMPORTANT]
> Alle referenzierten Beispiele sind spezifisch für die obige Abbildung.

1. Erstellen Sie eine [Ressourcengruppe](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup) im Azure-Portal in einer Region (**SR-AZ2AZ** in **USA, Westen 2**). 
2. Erstellen Sie zwei [Verfügbarkeitsgruppen](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM) in der Ressourcengruppe (**SR-AZ2AZ**) weiter oben erstellten eine für jeden Cluster. 
    a. Verfügbarkeitsgruppe (**az2azAS1**) b. Verfügbarkeitsgruppe (**az2azAS2**)
3. Erstellen Sie eine [virtuelles Netzwerk](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**az2az-Vnet**) in der zuvor erstellten Ressourcengruppe (**SR-AZ2AZ**), müssen mindestens ein Subnetz. 
4. Erstellen Sie eine [Netzwerksicherheitsgruppe](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**az2az-NSG**), und fügen Sie eine Sicherheitsregel für eingehenden Datenverkehr für RDP:3389 hinzu. Sie können diese Regel zu entfernen, wenn Sie das Setup abgeschlossen haben. 
5. Erstellen von Windows Server [VMs](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM) in der zuvor erstellten Ressourcengruppe (**SR-AZ2AZ**). Verwenden Sie das zuvor erstellte virtuelle Netzwerk (**az2az-Vnet**) und Netzwerk-Sicherheitsgruppe (**az2az-NSG**). 
   
   Domain Controller (**az2azDC**). Sie können auswählen, zum Erstellen einer dritten verfügbarkeitsgruppe für Ihre Domänencontroller oder der Domänencontroller in einem der zwei Verfügbarkeitsgruppen hinzufügen. Wenn Sie dies für die verfügbarkeitsgruppe erstellt haben, für die zwei Cluster hinzufügen, weisen sie eine öffentliche Standard-IP-Adresse während der Erstellung des virtuellen Computers an. 
   - Installieren Sie Active Directory Domain Services.
   - Erstellen Sie eine Domäne (Contoso.com)
   - Erstellen Sie einen Benutzer mit Administratorrechten (Contosoadmin) 
   - Erstellen Sie zwei virtuelle Computer (**az2az1**, **az2az2**) in der primären verfügbarkeitsgruppe festgelegt (**az2azAS1**). Weisen Sie eine standardmäßige öffentliche IP-Adresse für jeden virtuellen Computer während der Erstellung selbst.
   - Fügen Sie mindestens 2 verwaltete Datenträger für jeden Computer hinzu.
   - Installieren des Failoverclusterings und die Funktion "Speicherreplikat"-Funktion
   - Erstellen Sie zwei virtuelle Computer (**az2az3**, **az2az4**) in der zweiten verfügbarkeitsgruppe festgelegt (**az2azAS2**). Weisen Sie standardmäßige öffentliche IP-Adresse für jeden virtuellen Computer während der Erstellung selbst. 
   - Fügen Sie mindestens 2 verwaltete Datenträger für jeden Computer hinzu. 
   - Failoverclustering und die Funktion "Speicherreplikat"-Feature installieren. 
   
6. Verbinden Sie alle Knoten mit der Domäne ein, und geben Sie über Administratorrechte für den zuvor erstellten Benutzer. 

7. Ändern Sie den DNS-Server im virtuellen Netzwerk, in der privaten IP-Adresse des Domänencontrollers. 
8. In unserem Beispiel der Domänencontroller **az2azDC** verfügt über private IP-Adresse (10.3.0.8). Im Virtuellenetzwerk (**az2az-Vnet**) ändern Sie die DNS-Server 10.3.0.8 verwiesen. Verbinden Sie alle Knoten auf "Contoso.com", und geben Sie Administratorrechte besitzen, um "Contosoadmin".
   - Melden Sie sich als Contosoadmin von allen Knoten. 
    
9. Erstellen Sie die Cluster (**SRAZC1**, **SRAZC2**). Im folgenden finden Sie in unserem Beispiel die PowerShell-Befehle
```PowerShell
    New-Cluster -Name SRAZC1 -Node az2az1,az2az2 – StaticAddress 10.3.0.100
```
```PowerShell
    New-Cluster -Name SRAZC2 -Node az2az3,az2az4 – StaticAddress 10.3.0.101
```
10. Aktivieren von "direkte Speicherplätze"
```PowerShell
    Enable-clusterS2D
```   
   
   Erstellen Sie für jeden Cluster die virtuellen Datenträger und Volumes. Eine für die Daten und eine für das Protokoll. 
   
11. Erstellen Sie eine interne Standard-SKU [Load Balancer](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM) für jeden Cluster (**azlbr1**,**azlbr2**). 
   
   Geben Sie die Cluster-IP-Adresse als statische private IP-Adresse an, für den Load Balancer.
   - azlbr1 = > Front-End-IP: 10.3.0.100 (Wählen Sie eine nicht verwendete IP-Adresse aus dem virtuellen Netzwerk (**az2az-Vnet**) Subnetz)
   - Erstellen Sie für jeden Load Balancer-Back-End-Pool ein. Fügen Sie den zugehörigen Clusterknoten hinzu.
   - Erstellen eines Integritätstests: Port 59999
   - Erstellen Sie Load Balance-Regel: Ermöglichen Sie hochverfügbarkeitsports mit aktivierter Floating-IP ein. 
   
   Geben Sie die Cluster-IP-Adresse als statische private IP-Adresse an, für den Load Balancer.
   - azlbr2 = > Front-End-IP: 10.3.0.101 (Wählen Sie eine nicht verwendete IP-Adresse aus dem virtuellen Netzwerk (**az2az-Vnet**) Subnetz)
   - Erstellen Sie für jeden Load Balancer-Back-End-Pool ein. Fügen Sie den zugehörigen Clusterknoten hinzu.
   - Erstellen eines Integritätstests: Port 59999
   - Erstellen Sie Load Balance-Regel: Ermöglichen Sie hochverfügbarkeitsports mit aktivierter Floating-IP ein. 
   
12. Öffnen Sie auf jedem Clusterknoten Port 59999 (Integritätstest) aus. 
   
    Führen Sie den folgenden Befehl auf jedem Knoten aus:
```PowerShell
netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
```   
13. Weisen Sie den Cluster für Integritätstest auf Port 59999-Nachrichten zu Lauschen und reagieren, die über den Knoten, der derzeit diese Ressource besitzt. Führen Sie es einmal, von jedem Knoten des Clusters für jeden Cluster. 
    
    Stellen Sie in unserem Beispiel "ILBIP" gemäß Ihrer Konfigurationswerte zu ändern. Führen den folgenden Befehl aus einem Knoten **az2az1**/**az2az2**:

    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}
    ```

14. Führen den folgenden Befehl aus einem Knoten **az2az3**/**az2az4**. 

    ```PowerShell
    $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
    $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
    $ILBIP = "10.3.0.101" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
    [int]$ProbePort = 59999
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
    ```   
   Stellen Sie sicher, dass beide Cluster eine Verbindung herstellen / miteinander kommunizieren können. 

   Entweder "Verbindung zum Cluster"-Funktion im Failovercluster-Manager verwenden, um eine Verbindung herstellen, auf die anderen Cluster, oder Überprüfen Sie, dass die anderen Cluster aus einem der Knoten des aktuellen Clusters reagiert.  
   
   ```PowerShell
     Get-Cluster -Name SRAZC1 (ran from az2az3)
   ```
   ```PowerShell
     Get-Cluster -Name SRAZC2 (ran from az2az1)
   ```   

15. Cloud-Zeugen für beide Cluster zu erstellen. Erstellen Sie zwei [Speicherkonten](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) (**az2azcw**, **az2azcw2**) in Azure zu für jeden Cluster in derselben Ressourcengruppe befinden (**SR-AZ2AZ**).

    - Kopieren Sie den speicherkontonamen und Schlüssel aus "Zugriffsschlüssel"
    - Erstellen Sie des cloudzeugen über "Failovercluster-Manager", und verwenden Sie die oben genannten Namen und den Schlüssel um zu erstellen.

16. Führen Sie [Clustervalidierungstests](../../failover-clustering/create-failover-cluster.md#validate-the-configuration) bevor Sie mit dem nächsten Schritt fortfahren.

17. Starten Sie Windows PowerShell, und überprüfen Sie mithilfe des Cmdlets [Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps), ob alle Anforderungen für das Speicherreplikatfeature erfüllt sind. Sie können das Cmdlet eine Anforderungen nur im Modus für einen schnellen Test sowie eine lang andauernde Leistung-auswertungsmodus verwenden.

18. Konfigurieren Sie die Funktion "Speicherreplikat" Cluster-zu-Cluster.
   
   Gewähren des Zugriffs über einen Cluster mit einem anderen Cluster in beide Richtungen:

   In unserem Beispiel:

   ```PowerShell
      Grant-SRAccess -ComputerName az2az1 -Cluster SRAZC2
   ```
Wenn Sie diesen Befehl auch Ausführen von Windows Server 2016 verwenden:

   ```PowerShell
      Grant-SRAccess -ComputerName az2az3 -Cluster SRAZC1
   ```   
   
19. SRPartnership für den Cluster zu erstellen:</ol>

 - Für Cluster **SRAZC1**.
   - Volume-Speicherort:-c:\ClusterStorage\DataDisk1
   - Protokollspeicherort:-g:
 - Für Cluster **SRAZC2**
    - Volume-Speicherort:-c:\ClusterStorage\DataDisk2
    - Protokollspeicherort:-g:

Führen Sie den folgenden Befehl aus:

```PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName **SRAZC2** -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDisk2 -DestinationLogVolumeName  g:
```