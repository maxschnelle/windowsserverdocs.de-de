---
title: Cluster-zu-Cluster Storage Replica cross-Bereich in Azure
description: Regions übergreifender Cluster-zu-Cluster-Speicher Replikation in Azure
keywords: Speicher Replikat, Server-Manager, Windows Server, Azure, Cluster, Regions übergreifend, unterschiedliche Regionen
author: arduppal
ms.author: arduppal
ms.date: 12/19/2018
ms.topic: article
ms.prod: windows-server
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: 806857d5de067c0f4640344ed80338b474dd758e
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950062"
---
# <a name="cluster-to-cluster-storage-replica-cross-region-in-azure"></a>Cluster-zu-Cluster Storage Replica cross-Bereich in Azure

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)

Sie können Cluster-zu-Cluster-Speicher Replikate für Regions übergreifende Anwendungen in Azure konfigurieren. In den folgenden Beispielen wird ein Cluster mit zwei Knoten verwendet, aber Cluster-zu-Cluster-Speicher Replikate sind nicht auf einen Cluster mit zwei Knoten beschränkt. Die folgende Abbildung zeigt einen Cluster für direkte Speicherplätze mit zwei Knoten, der miteinander kommunizieren kann, sich in derselben Domäne befindet und Regions übergreifend ist.

Sehen Sie sich das Video unten an, um eine umfassende Exemplarische Vorgehensweise zum Prozess zu finden.
> [!video https://www.microsoft.com/videoplayer/embed/RE26xeW]

![Das Architektur Diagramm, in dem sich die in Azure in Azure mit der gleichen Region ausstellt.](media/Cluster-to-cluster-azure-cross-region/architecture.png)
> [!IMPORTANT]
> Alle referenzierten Beispiele sind spezifisch für die obige Abbildung.


1. Erstellen Sie in der Azure-Portal [Ressourcengruppen](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup) in zwei verschiedenen Regionen.

    Beispielsweise **SR-AZ2AZ** in " **USA, Westen 2** " und " **SR-azcross** " in " **USA, Westen**-Mitte", wie oben gezeigt.

2. Erstellen Sie zwei [Verfügbarkeits Gruppen](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM), eine in jeder Ressourcengruppe für jeden Cluster.
    - Verfügbarkeits Gruppe (**az2azAS1**) in (**SR-AZ2AZ**)
    - Verfügbarkeits Gruppe (**azcross-as**) in (**SR-azcross**)

3. Erstellen zweier virtueller Netzwerke
   - Erstellen Sie das [virtuelle Netzwerk](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**az2az-vnet**) in der ersten Ressourcengruppe (**SR-az2az**) mit einem Subnetz und einem gatewaysubnetz.
   - Erstellen Sie das [virtuelle Netzwerk](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**azcross-vnet**) in der zweiten Ressourcengruppe (**SR-azcross**) mit einem Subnetz und einem gatewaysubnetz.

4. Erstellen von zwei Netzwerk Sicherheitsgruppen
   - Erstellen Sie die [Netzwerk Sicherheitsgruppe](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**az2az-NSG**) in der ersten Ressourcengruppe (**SR-az2az**).
   - Erstellen Sie die [Netzwerk Sicherheitsgruppe](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**azcross-NSG**) in der zweiten Ressourcengruppe (**SR-azcross**).

   Fügen Sie eine eingehende Sicherheitsregel für RDP: 3389 zu beiden Netzwerk Sicherheitsgruppen hinzu. Nachdem Sie die Einrichtung abgeschlossen haben, können Sie diese Regel entfernen.

5. Erstellen Sie [virtuelle](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM) Windows Server-Computer in den zuvor erstellten Ressourcengruppen.

   Domänen Controller (**az2azDC**). Sie können auswählen, ob Sie eine Dritt-Verfügbarkeits Gruppe für Ihren Domänen Controller erstellen oder den Domänen Controller in einer der beiden Verfügbarkeits Gruppen hinzufügen möchten. Wenn Sie dieses der Verfügbarkeits Gruppe hinzufügen, die für die beiden Cluster erstellt wurde, weisen Sie ihm während der Erstellung des virtuellen Computers eine öffentliche IP-Standard Adresse zu.
      - Installieren Sie Active Directory-Domäne-Dienst.
      - Erstellen einer Domäne (contoso.com)
      - Erstellen eines Benutzers mit Administratorrechten (contosoadmin)

   Erstellen Sie zwei virtuelle Computer **(az2az1**, **az2az2**) in der Ressourcengruppe **(SR-AZ2AZ**) mithilfe des virtuellen Netzwerks (**AZ2AZ-vnet**) und der Netzwerk Sicherheitsgruppe (**AZ2AZ-NSG**) in der Verfügbarkeits Gruppe (**az2azAS1**). Weisen Sie jedem virtuellen Computer während der Erstellung selbst eine öffentliche Standard-IP-Adresse zu.
      - Hinzufügen von mindestens zwei verwalteten Datenträgern zu jedem Computer
      - Installieren des Failoverclustering und des Speicher Replikat Features

   Erstellen Sie zwei virtuelle Computer **(azcross1**, **azcross2**) in der Ressourcengruppe **(SR-azcross**) mithilfe des virtuellen Netzwerks (**azcross-vnet**) und der Netzwerk Sicherheitsgruppe (**azcross-NSG**) in der Verfügbarkeits Gruppe (**azcross-as**). Zuweisen einer öffentlichen Standard-IP-Adresse zu jedem virtuellen Computer während der Erstellung
      - Hinzufügen von mindestens zwei verwalteten Datenträgern zu jedem Computer
      - Installieren des Failoverclustering und des Speicher Replikat Features

   Verbinden Sie alle Knoten mit der Domäne, und stellen Sie dem zuvor erstellten Benutzer Administratorrechte bereit.

   Ändern Sie den DNS-Server des virtuellen Netzwerks in die private IP-Adresse des Domänen Controllers.
   - Im Beispiel verfügt der Domänen Controller **az2azDC** über eine private IP-Adresse (10.3.0.8). Ändern Sie im Virtual Network (**az2az-vnet** und **azcross-vnet**) den DNS-Server 10.3.0.8. 

     Verbinden Sie in diesem Beispiel alle Knoten mit "contoso.com", und stellen Sie "contosoadmin" Administratorrechte bereit.
   - Melden Sie sich als "condesoadmin" von allen Knoten an. 
 
6. Erstellen Sie die Cluster (**SRAZC1**, **srazcross**).

   Im folgenden finden Sie die PowerShell-Befehle für das Beispiel.
   ```powershell
      New-Cluster -Name SRAZC1 -Node az2az1,az2az2 –StaticAddress 10.3.0.100
   ```
   ```powershell
      New-Cluster -Name SRAZCross -Node azcross1,azcross2 –StaticAddress 10.0.0.10
   ```

7. Aktivieren Sie "direkte Speicherplätze".

   ```powershell
      Enable-clusterS2D
   ```

   > [!NOTE]
   > Erstellen Sie für jeden Cluster eine virtuelle Festplatte und ein Volume. Einer für die Daten und ein anderer für das Protokoll.

8. Erstellen Sie einen internen Standard-SKU- [Load Balancer](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM) für jeden Cluster (**azlbr1**, **azlbazcross**).

   Geben Sie die Cluster-IP-Adresse als statische private IP-Adresse für den Load Balancer an.
      - azlbr1 = > Front-End-IP: 10.3.0.100 (übernehmen Sie eine nicht verwendete IP-Adresse aus dem Subnetz des virtuellen Netzwerks (**az2az-vnet**))
      - Erstellen Sie einen Back-End-Pool für jeden Load Balancer. Fügen Sie die zugeordneten Cluster Knoten hinzu.
      - Erstellen eines Integritätstests: Port 59999
      - Lasten Ausgleichs Regel erstellen: hochverfügbarkeitsports mit aktivierter Floating IP zulassen.

   Geben Sie die Cluster-IP-Adresse als statische private IP-Adresse für den Load Balancer an. 
      - azlbazcross = > Front-End-IP: 10.0.0.10 (übernehmen Sie eine nicht verwendete IP-Adresse aus dem virtuellen Netzwerk (**azcross-vnet**) Subnetz)
      - Erstellen Sie einen Back-End-Pool für jeden Load Balancer. Fügen Sie die zugeordneten Cluster Knoten hinzu.
      - Erstellen eines Integritätstests: Port 59999
      - Lasten Ausgleichs Regel erstellen: hochverfügbarkeitsports mit aktivierter Floating IP zulassen. 

9. Erstellen Sie ein [virtuelles Netzwerk Gateway](https://ms.portal.azure.com/#create/Microsoft.VirtualNetworkGateway-ARM) für die vnet-zu-vnet-Konnektivität.

   - Erstellen des ersten virtuellen Netzwerk Gateways (**az2az-vnetgateway**) in der ersten Ressourcengruppe (**SR-az2az**)
   - Gatewaytyp = VPN und VPN-Typ: Routen basiert

   - Erstellen des zweiten virtuellen Netzwerk Gateways (**azcross-vnetgateway**) in der zweiten Ressourcengruppe (**SR-azcross**)
   - Gatewaytyp = VPN und VPN-Typ: Routen basiert

   - Erstellen Sie eine vnet-zu-vnet-Verbindung zwischen dem ersten virtuellen Netzwerk Gateway und dem zweiten virtuellen Netzwerk Gateway. Angeben eines gemeinsam verwendeten Schlüssels

   - Erstellen Sie eine vnet-zu-vnet-Verbindung zwischen dem zweiten virtuellen Netzwerk Gateway und dem ersten virtuellen Netzwerk Gateway. Geben Sie den gleichen gemeinsam verwendeten Schlüssel wie im obigen Schritt an. 

10. Öffnen Sie auf jedem Cluster Knoten Port 59999 (Integritätstest).

    Führen Sie den folgenden Befehl auf jedem Knoten aus:

    ```powershell
      netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
    ```

11. Weisen Sie den Cluster an, auf dem Port 59999 auf Integritätstest Nachrichten zu lauschen und von dem Knoten zu antworten, der derzeit diese Ressource besitzt.

    Führen Sie es für jeden Cluster einmal von einem beliebigen Knoten des Clusters aus. 
    
    Stellen Sie in unserem Beispiel sicher, dass Sie das "ilbip" entsprechend ihren Konfigurations Werten ändern. Führen Sie den folgenden Befehl von einem beliebigen Knoten aus **az2az1**/**az2az2**

    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
    ```

12. Führen Sie den folgenden Befehl von einem beliebigen Knoten aus **azcross1**/**azcross2**
    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.0.0.10" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
    ```

    Stellen Sie sicher, dass beide Cluster eine Verbindung herstellen und miteinander kommunizieren können.

    Verwenden Sie entweder die Funktion "mit Cluster verbinden" im Failovercluster-Manager, um eine Verbindung mit dem anderen Cluster herzustellen, oder überprüfen Sie, ob andere Cluster von einem der Knoten des aktuellen Clusters antwortet.

    Aus dem Beispiel, das wir verwendet haben:
    ```powershell
      Get-Cluster -Name SRAZC1 (ran from azcross1)
    ```
    ```powershell
      Get-Cluster -Name SRAZCross (ran from az2az1) 
    ```

13. Erstellen Sie einen cloudzeugen für beide Cluster. Erstellen Sie zwei [Speicher Konten](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) (**az2azcw**,**azcrosssa**) in Azure, eine für jeden Cluster in jeder Ressourcengruppe (**SR-AZ2AZ**, **SR-azcross**).
   
    - Kopieren Sie den Speicherkonto Namen und den Schlüssel aus "Zugriffs Schlüsseln".
    - Erstellen Sie den cloudzeugen aus "Failovercluster-Manager", und verwenden Sie den obigen Kontonamen und-Schlüssel, um ihn zu erstellen. 

14. Ausführen von [Cluster Validierungstests](../../failover-clustering/create-failover-cluster.md#validate-the-configuration) , bevor mit dem nächsten Schritt fortfahren

15. Starten Sie Windows PowerShell, und überprüfen Sie mithilfe des Cmdlets [Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps), ob alle Anforderungen für das Speicherreplikatfeature erfüllt sind. Für einen schnellen Test können Sie das Cmdlet in einem Modus zur ausschließlichen Überprüfung der Anforderungen ausführen, oder Sie wählen einen Modus mit langer Ausführungsdauer, um die Leistung auszuwerten.
 
16. Konfigurieren Sie das Cluster-zu-Cluster-Speicher Replikat.
    Gewähren des Zugriffs von einem Cluster auf einen anderen Cluster in beide Richtungen:

    Aus unserem Beispiel:
    ```powershell
     Grant-SRAccess -ComputerName az2az1 -Cluster SRAZCross
    ```
    Wenn Sie Windows Server 2016 verwenden, führen Sie auch den folgenden Befehl aus:

    ```powershell
     Grant-SRAccess -ComputerName azcross1 -Cluster SRAZC1
    ```

17. Erstellen Sie SR-Partnerschaft für die beiden Cluster:</ol>

    - Für Cluster **SRAZC1**
      - Volumespeicherort:-c:\clusterstorage\datadisk1
      - Protokoll Speicherort:-g:
    - Für Cluster **srazcross**
      - Volumespeicherort:-c:\clusterstorage\datadiskcross
      - Protokoll Speicherort:-g:

Führen Sie den Befehl aus:

```powershell
PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName SRAZCross -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDiskCross -DestinationLogVolumeName  g:
```