---
title: Cluster-zu-Cluster Storage Replica cross-Bereich in Azure
description: Cluster-zu-Cluster-Speicherreplikation cross-Region in Azure
keywords: Funktion "Speicherreplikat", Server-Manager, Windows Server, Azure-Cluster regionsübergreifend anderen region
author: arduppal
ms.author: arduppal
ms.date: 12/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: 41f435c3d537cbfd204dfa869d750b22200deb33
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891131"
---
# <a name="cluster-to-cluster-storage-replica-cross-region-in-azure"></a>Cluster-zu-Cluster Storage Replica cross-Bereich in Azure
Sie können die Cluster-zu-Cluster Speicherreplikate für regionsübergreifende Anwendungen in Azure konfigurieren. Klicken Sie in den folgenden Beispielen verwenden wir einen Cluster mit zwei Knoten, aber Cluster-zu-Cluster-Funktion "speicherreplikat" ist nicht auf einen Cluster mit zwei Knoten beschränkt. In der folgenden Abbildung ist ein Storage Space Direct Cluster mit zwei Knoten, der miteinander kommunizieren kann, befinden sich in derselben Domäne und regionsübergreifenden.

Sehen Sie sich das Video unten für eine vollständige Exemplarische Vorgehensweise des Prozesses.
> [!video https://www.microsoft.com/en-us/videoplayer/embed/RE26xeW]

![Die Architektur in einem Diagramm mit C2C SR in Azure innerhalb derselben Region.](media\Cluster-to-cluster-azure-cross-region\architecture.png)
> [!IMPORTANT]
> Alle referenzierten Beispiele sind spezifisch für die obige Abbildung.


1. Erstellen Sie im Azure-Portal, [Ressourcengruppen](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup) in zwei verschiedenen Regionen.

    Z. B. **SR-AZ2AZ** in **USA, Westen 2** und **SR-AZCROSS** in **USA, Westen Mitte**, wie oben gezeigt.

2. Erstellen Sie zwei [Verfügbarkeitsgruppen](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM), eine in jeder Ressourcengruppe für jeden Cluster
    - Verfügbarkeitsgruppe (**az2azAS1**) in (**SR-AZ2AZ**)
    - Verfügbarkeitsgruppe (**Azcross-AS**) in (**SR-AZCROSS**)

3. Erstellen Sie zwei virtuelle Netzwerke
   - Erstellen der [virtuelles Netzwerk](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**az2az-Vnet**) in der ersten Ressourcengruppe (**SR-AZ2AZ**), müssen ein Subnetz und ein gatewaysubnetz.
   - Erstellen der [virtuelles Netzwerk](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**Azcross-VNET**) in die zweite Ressourcengruppe (**SR-AZCROSS**), müssen ein Subnetz und ein gatewaysubnetz.

4. Erstellen Sie zwei netzwerksicherheitsgruppen
   - Erstellen der [Netzwerksicherheitsgruppe](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**az2az-NSG**) in der ersten Ressourcengruppe (**SR-AZ2AZ**).
   - Erstellen der [Netzwerksicherheitsgruppe](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**Azcross-NSG**) in die zweite Ressourcengruppe (**SR-AZCROSS**). 

   Fügen Sie eine Sicherheitsregel für eingehenden Datenverkehr für RDP:3389 auf beiden Netzwerksicherheitsgruppen hinzu. Sie können diese Regel zu entfernen, wenn Sie das Setup abgeschlossen haben.

5. Erstellen von Windows Server [VMs](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM) in den zuvor erstellten Ressourcengruppen.

   Domain Controller (**az2azDC**). Sie können auch eine 3. verfügbarkeitsgruppe für Ihre Domänencontroller erstellen, oder die Domänencontroller in einer der beiden verfügbarkeitsgruppe hinzufügen. Wenn Sie dies für die verfügbarkeitsgruppe erstellt haben, für die zwei Cluster hinzufügen, weisen sie eine öffentliche Standard-IP-Adresse während der Erstellung des virtuellen Computers an.
      - Installieren Sie Active Directory Domain Services.
      - Erstellen Sie eine Domäne (contoso.com)
      - Erstellen Sie einen Benutzer mit Administratorrechten (Contosoadmin)

   Erstellen Sie zwei virtuelle Computer (**az2az1**, **az2az2**) in der Ressourcengruppe (**SR-AZ2AZ**) mithilfe des virtuellen Netzwerks (**az2az-Vnet**) und Netzwerksicherheitsgruppe (**az2az-NSG**) legen Sie bei der Verfügbarkeit (**az2azAS1**). Weisen Sie eine öffentliche standard-IP-Adresse für jeden virtuellen Computer während der Erstellung selbst.
      - Fügen Sie mindestens zwei Datenträger für jeden Computer
      - Installieren des Failoverclusterings und die Funktion "Speicherreplikat"-Funktion

   Erstellen Sie zwei virtuelle Computer (**azcross1**, **azcross2**) in der Ressourcengruppe (**SR-AZCROSS**) mithilfe des virtuellen Netzwerks (**Azcross-VNET**) und Netzwerk-Sicherheitsgruppe (**Azcross-NSG**) legen Sie bei der Verfügbarkeit (**Azcross-AS**). Weisen Sie die standardmäßige öffentliche IP-Adresse für jeden virtuellen Computer während der Erstellung selbst
      - Fügen Sie mindestens zwei Datenträger für jeden Computer
      - Installieren des Failoverclusterings und die Funktion "Speicherreplikat"-Funktion

   Verbinden Sie alle Knoten mit der Domäne ein, und geben Sie über Administratorrechte für den zuvor erstellten Benutzer.

   Ändern Sie den DNS-Server im virtuellen Netzwerk, in der privaten IP-Adresse des Domänencontrollers.
   - Im Beispiel ist der Domänencontroller **az2azDC** verfügt über private IP-Adresse (10.3.0.8). Im Virtuellenetzwerk (**az2az-Vnet** und **Azcross-VNET**) ändern Sie die DNS-Server 10.3.0.8 verwiesen. 

    Klicken Sie im Beispiel verbinden Sie alle Knoten auf "contoso.com", und geben Sie Administratorrechte besitzen, um "Contosoadmin".
   - Melden Sie sich als Contosoadmin von allen Knoten. 
 
6. Erstellen Sie die Cluster (**SRAZC1**, **SRAZCross**).

   Im folgenden finden Sie die PowerShell-Befehle für das Beispiel
   ```powershell
      New-Cluster -Name SRAZC1 -Node az2az1,az2az2 – StaticAddress 10.3.0.100
   ```
   ```powershell
      New-Cluster -Name SRAZCross -Node azcross1,azcross2 – StaticAddress 10.0.0.10
   ```

7. Aktivieren Sie "direkte Speicherplätze".

   ```powershell
      Enable-clusterS2D
   ```

   > [!NOTE]
   > Erstellen Sie für jeden Cluster die virtuellen Datenträger und Volumes. Eine für die Daten und eine für das Protokoll.

8. Erstellen Sie eine interne Standard-SKU [Load Balancer](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM) für jeden Cluster (**azlbr1**, **Azlbazcross**).

   Geben Sie die Cluster-IP-Adresse als statische private IP-Adresse an, für den Load Balancer.
      - azlbr1 = > Front-End-IP: 10.3.0.100 (Wählen Sie eine nicht verwendete IP-Adresse aus dem virtuellen Netzwerk (**az2az-Vnet**) Subnetz)
      - Erstellen Sie für jeden Load Balancer-Back-End-Pool ein. Fügen Sie den zugehörigen Clusterknoten hinzu.
      - Erstellen eines Integritätstests: Port 59999
      - Erstellen Sie Load Balance-Regel: Ermöglichen Sie hochverfügbarkeitsports mit aktivierter Floating-IP ein.

   Geben Sie die Cluster-IP-Adresse als statische private IP-Adresse an, für den Load Balancer. 
      - Azlbazcross = > Frontend IP: 10.0.0.10 (Wählen Sie eine nicht verwendete IP-Adresse aus dem virtuellen Netzwerk (**Azcross-VNET**) Subnetz)
      - Erstellen Sie für jeden Load Balancer-Back-End-Pool ein. Fügen Sie den zugehörigen Clusterknoten hinzu.
      - Erstellen eines Integritätstests: Port 59999
      - Erstellen Sie Load Balance-Regel: Ermöglichen Sie hochverfügbarkeitsports mit aktivierter Floating-IP ein. 

9. Erstellen Sie [Gateway des virtuellen Netzwerks](https://ms.portal.azure.com/#create/Microsoft.VirtualNetworkGateway-ARM) für Vnet-zu-Vnet-Verbindungen.

 - Erstellen Sie das Gateway des ersten virtuellen Netzwerks (**az2az-VNetGateway**) in der ersten Ressourcengruppe (**SR-AZ2AZ**)
 - Gatewaytyp = VPN- und VPN-Typ = routenbasiert

 - Erstellen der zweite Gateway des virtuellen Netzwerks (**Azcross-VNetGateway**) in die zweite Ressourcengruppe (**SR-AZCROSS**)
 - Gatewaytyp = VPN- und VPN-Typ = routenbasiert

 - Erstellen Sie eine Vnet-zu-Vnet-Verbindung vom ersten Gateway für virtuelle Netzwerke, die zweite Gateway des virtuellen Netzwerks. Geben Sie einen gemeinsam verwendeten Schlüssel

 - Erstellen Sie eine Vnet-zu-Vnet-Verbindung aus der zweiten Gateway für virtuelle Netzwerke auf dem ersten Gateway für virtuelle Netzwerke. Geben Sie den gleichen gemeinsam verwendeten Schlüssel an, wie im vorherigen Schritt angegeben. 

10. Öffnen Sie auf jedem Clusterknoten Port 59999 (Integritätstest) aus.

   Führen Sie den folgenden Befehl auf jedem Knoten aus:

   ```powershell
      netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
   ```

11. Weisen Sie den Cluster für Integritätstest auf Port 59999-Nachrichten zu Lauschen und reagieren, die über den Knoten, der derzeit diese Ressource besitzt.

   Führen Sie es einmal, von jedem Knoten des Clusters für jeden Cluster. 
    
   Stellen Sie in unserem Beispiel "ILBIP" gemäß Ihrer Konfigurationswerte zu ändern. Führen den folgenden Befehl aus einem Knoten **az2az1**/**az2az2**

   ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
   ```

12. Führen den folgenden Befehl aus einem Knoten **azcross1**/**azcross2**
   ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.0.0.10" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
   ```

   Stellen Sie sicher, dass beide Cluster eine Verbindung herstellen / miteinander kommunizieren können.

   Entweder "Verbindung zum Cluster"-Funktion im Failovercluster-Manager verwenden, um eine Verbindung herstellen, auf die anderen Cluster, oder Überprüfen Sie, dass die anderen Cluster aus einem der Knoten des aktuellen Clusters reagiert.

   Im Beispiel haben wir verwendet:
   ```powershell
      Get-Cluster -Name SRAZC1 (ran from azcross1)
   ```
   ```powershell
      Get-Cluster -Name SRAZCross (ran from az2az1) 
   ```

13. Cloudzeugen für beide Cluster zu erstellen. Erstellen Sie zwei [Speicherkonten](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) (**az2azcw**,**Azcrosssa**) in Azure, eine für jeden Cluster in jeder Ressourcengruppe (**SR-AZ2AZ**,  **SR-AZCROSS**).
   
   - Kopieren Sie den speicherkontonamen und Schlüssel aus "Zugriffsschlüssel"
   - Erstellen Sie des cloudzeugen über "Failovercluster-Manager", und verwenden Sie die oben genannten Namen und den Schlüssel um zu erstellen. 

14. Führen Sie [Clustervalidierungstests](../../failover-clustering/create-failover-cluster.md#validate-the-configuration) bevor Sie mit dem nächsten Schritt fortfahren

15. Starten Sie Windows PowerShell, und überprüfen Sie mithilfe des Cmdlets [Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps), ob alle Anforderungen für das Speicherreplikatfeature erfüllt sind. Für einen schnellen Test können Sie das Cmdlet in einem Modus zur ausschließlichen Überprüfung der Anforderungen ausführen, oder Sie wählen einen Modus mit langer Ausführungsdauer, um die Leistung auszuwerten.
 
16. Konfigurieren Sie die Cluster-zu-Cluster-Funktion "speicherreplikat".
Gewähren des Zugriffs über einen Cluster mit einem anderen Cluster in beide Richtungen:

   Aus unserem Beispiel:
   ```powershell
     Grant-SRAccess -ComputerName az2az1 -Cluster SRAZCross
   ```
Wenn Sie diesen Befehl auch Ausführen von Windows Server 2016 verwenden:

   ```powershell
     Grant-SRAccess -ComputerName azcross1 -Cluster SRAZC1
   ```

17. Erstellen Sie SR-Partnerschaft für die zwei Cluster:</ol>

   - Für Cluster **SRAZC1**
      - Volume-Speicherort:-c:\ClusterStorage\DataDisk1
      - Protokollspeicherort:-g:
   - Für Cluster **SRAZCross**
      - Volume-Speicherort:-c:\ClusterStorage\DataDiskCross
      - Protokollspeicherort:-g:

Führen Sie den Befehl ein:

```powershell
PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName SRAZCross -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDiskCross -DestinationLogVolumeName  g:
```