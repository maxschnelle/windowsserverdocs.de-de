---
title: Cluster-zu-Cluster-Speicher Replikat innerhalb derselben Region in Azure
description: Cluster-zu-Cluster-Speicher Replikation innerhalb derselben Region in Azure
keywords: Speicher Replikat, Server-Manager, Windows Server, Azure, Cluster, dieselbe Region
author: arduppal
ms.author: arduppal
ms.date: 04/26/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: 3e620b5597a2d25a7bb02daf80c5812d25f6a987
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950036"
---
# <a name="cluster-to-cluster-storage-replica-within-the-same-region-in-azure"></a>Cluster-zu-Cluster-Speicher Replikat innerhalb derselben Region in Azure

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)

Sie können die Cluster-zu-Cluster-Speicher Replikation innerhalb derselben Region in Azure konfigurieren. In den folgenden Beispielen wird ein Cluster mit zwei Knoten verwendet, aber Cluster-zu-Cluster-Speicher Replikate sind nicht auf einen Cluster mit zwei Knoten beschränkt. Die folgende Abbildung zeigt einen Cluster für direkte Speicherplätze mit zwei Knoten, der miteinander kommunizieren kann, sich in derselben Domäne und innerhalb derselben Region befindet.

Sehen Sie sich die folgenden Videos an, um eine umfassende Exemplarische Vorgehensweise zum Prozess zu finden.

Teil 1
> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE26f2Y]

Teil 2
> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE269Pq]

![Das Architektur Diagramm, das Cluster-zu-Cluster-Speicher Replikate in Azure innerhalb derselben Region zeigt.](media/Cluster-to-cluster-azure-one-region/architecture.png)
> [!IMPORTANT]
> Alle referenzierten Beispiele sind spezifisch für die obige Abbildung.

1. Erstellen Sie eine [Ressourcengruppe](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup) im Azure-Portal in einer Region (**SR-AZ2AZ** in **USA, Westen 2**). 
2. Erstellen Sie in der oben erstellten Ressourcengruppe (**SR-AZ2AZ**) zwei [Verfügbarkeits Gruppen](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM) , eine für jeden Cluster. 
    ein. Verfügbarkeits Gruppe (**az2azAS1**) b. Verfügbarkeits Gruppe (**az2azAS2**)
3. Erstellen Sie ein [virtuelles Netzwerk](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**az2az-vnet**) in der zuvor erstellten Ressourcengruppe (**SR-az2az**) mit mindestens einem Subnetz. 
4. Erstellen Sie eine [Netzwerk Sicherheitsgruppe](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**az2az-NSG**), und fügen Sie eine eingehende Sicherheitsregel für RDP hinzu: 3389. Nachdem Sie die Einrichtung abgeschlossen haben, können Sie diese Regel entfernen. 
5. Erstellen Sie [virtuelle](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM) Windows Server-Computer in der zuvor erstellten Ressourcengruppe (**SR-AZ2AZ**). Verwenden Sie das zuvor erstellte virtuelle Netzwerk (**az2az-vnet**) und die Netzwerk Sicherheitsgruppe (**az2az-NSG**). 
   
   Domänen Controller (**az2azDC**). Sie können auswählen, ob Sie eine dritte Verfügbarkeits Gruppe für Ihren Domänen Controller erstellen oder den Domänen Controller in einer der beiden Verfügbarkeits Gruppen hinzufügen möchten. Wenn Sie dieses der Verfügbarkeits Gruppe hinzufügen, die für die beiden Cluster erstellt wurde, weisen Sie ihm während der Erstellung des virtuellen Computers eine öffentliche IP-Standard Adresse zu. 
   - Installieren Sie Active Directory-Domäne-Dienst.
   - Erstellen einer Domäne (contoso.com)
   - Erstellen eines Benutzers mit Administratorrechten (contosoadmin) 
   - Erstellen Sie zwei virtuelle Computer (**az2az1**, **az2az2**) in der ersten Verfügbarkeits Gruppe (**az2azAS1**). Weisen Sie jedem virtuellen Computer während der Erstellung selbst eine öffentliche Standard-IP-Adresse zu.
   - Hinzufügen von mindestens zwei verwalteten Datenträgern zu jedem Computer
   - Installieren des Failoverclustering-und Speicher Replikat Features
   - Erstellen Sie zwei virtuelle Computer (**az2az3**, **az2az4**) in der zweiten Verfügbarkeits Gruppe (**az2azAS2**). Weisen Sie jedem virtuellen Computer während der Erstellung selbst eine öffentliche Standard-IP-Adresse zu. 
   - Fügen Sie jedem Computer mindestens zwei verwaltete Datenträger hinzu. 
   - Installieren Sie das Feature Failoverclustering und Speicher Replikat. 
   
6. Verbinden Sie alle Knoten mit der Domäne, und stellen Sie dem zuvor erstellten Benutzer Administrator Rechte bereit. 

7. Ändern Sie den DNS-Server des virtuellen Netzwerks in die private IP-Adresse des Domänen Controllers. 
8. In unserem Beispiel hat der Domänen Controller **az2azDC** eine private IP-Adresse (10.3.0.8). Ändern Sie im Virtual Network (**az2az-vnet**) den DNS-Server 10.3.0.8. Verbinden Sie alle Knoten mit "contoso.com", und geben Sie "contosoadmin" Administratorrechte an.
   - Melden Sie sich als "condesoadmin" von allen Knoten an. 
    
9. Erstellen Sie die Cluster (**SRAZC1**, **SRAZC2**). 
   Im folgenden finden Sie die PowerShell-Befehle für unser Beispiel.
   ```PowerShell
    New-Cluster -Name SRAZC1 -Node az2az1,az2az2 –StaticAddress 10.3.0.100
   ```
   ```PowerShell
    New-Cluster -Name SRAZC2 -Node az2az3,az2az4 –StaticAddress 10.3.0.101
   ```
10. Aktivieren von "direkte Speicherplätze"
    ```PowerShell
    Enable-clusterS2D
    ```   
   
    Erstellen Sie für jeden Cluster eine virtuelle Festplatte und ein Volume. Einer für die Daten und ein anderer für das Protokoll. 
   
11. Erstellen Sie für jeden Cluster einen internen Standard-SKU- [Load Balancer](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM) (**azlbr1**,**azlbr2**). 
   
    Geben Sie die Cluster-IP-Adresse als statische private IP-Adresse für den Load Balancer an.
    - azlbr1 = > Front-End-IP: 10.3.0.100 (übernehmen Sie eine nicht verwendete IP-Adresse aus dem Subnetz des virtuellen Netzwerks (**az2az-vnet**))
    - Erstellen Sie einen Back-End-Pool für jeden Load Balancer. Fügen Sie die zugeordneten Cluster Knoten hinzu.
    - Erstellen eines Integritätstests: Port 59999
    - Lasten Ausgleichs Regel erstellen: hochverfügbarkeitsports mit aktivierter Floating IP zulassen. 
   
    Geben Sie die Cluster-IP-Adresse als statische private IP-Adresse für den Load Balancer an.
    - azlbr2 = > Front-End-IP: 10.3.0.101 (übernehmen Sie eine nicht verwendete IP-Adresse aus dem Subnetz des virtuellen Netzwerks (**az2az-vnet**))
    - Erstellen Sie einen Back-End-Pool für jeden Load Balancer. Fügen Sie die zugeordneten Cluster Knoten hinzu.
    - Erstellen eines Integritätstests: Port 59999
    - Lasten Ausgleichs Regel erstellen: hochverfügbarkeitsports mit aktivierter Floating IP zulassen. 
   
12. Öffnen Sie auf jedem Cluster Knoten Port 59999 (Integritätstest). 
   
    Führen Sie den folgenden Befehl auf jedem Knoten aus:
    ```PowerShell
    netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
    ```   
13. Weisen Sie den Cluster an, auf dem Port 59999 auf Integritätstest Nachrichten zu lauschen und von dem Knoten zu antworten, der derzeit diese Ressource besitzt. 
    Führen Sie es für jeden Cluster einmal von einem beliebigen Knoten des Clusters aus. 
    
    Stellen Sie in unserem Beispiel sicher, dass Sie das "ilbip" entsprechend ihren Konfigurations Werten ändern. Führen Sie den folgenden Befehl von einem beliebigen Knoten aus **az2az1**/**az2az2**:

    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}
    ```

14. Führen Sie den folgenden Befehl von einem beliebigen Knoten aus **az2az3**/**az2az4**. 

    ```PowerShell
    $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
    $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
    $ILBIP = "10.3.0.101" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
    [int]$ProbePort = 59999
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
    ```   
    Stellen Sie sicher, dass beide Cluster eine Verbindung herstellen und miteinander kommunizieren können. 

    Verwenden Sie entweder die Funktion "mit Cluster verbinden" im Failovercluster-Manager, um eine Verbindung mit dem anderen Cluster herzustellen, oder überprüfen Sie, ob andere Cluster von einem der Knoten des aktuellen Clusters antwortet.  
   
    ```PowerShell
     Get-Cluster -Name SRAZC1 (ran from az2az3)
    ```
    ```PowerShell
     Get-Cluster -Name SRAZC2 (ran from az2az1)
    ```   

15. Erstellen Sie cloudzeugen für beide Cluster. Erstellen Sie zwei [Speicher Konten](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) (**az2azcw**, **az2azcw2**) in Azure für jeden Cluster in derselben Ressourcengruppe (**SR-AZ2AZ**).

    - Kopieren Sie den Speicherkonto Namen und den Schlüssel aus "Zugriffs Schlüsseln".
    - Erstellen Sie den cloudzeugen aus "Failovercluster-Manager", und verwenden Sie den obigen Kontonamen und-Schlüssel, um ihn zu erstellen.

16. Führen Sie [Cluster Validierungstests](../../failover-clustering/create-failover-cluster.md#validate-the-configuration) aus, bevor Sie mit dem nächsten Schritt fortfahren.

17. Starten Sie Windows PowerShell, und überprüfen Sie mithilfe des Cmdlets [Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps), ob alle Anforderungen für das Speicherreplikatfeature erfüllt sind. Sie können das Cmdlet in einem reinen Anforderungs Modus für einen Schnelltest und einen Leistungs Bewertungsmodus mit langer Ausführungszeit verwenden.

18. Konfigurieren Sie das Cluster-zu-Cluster-Speicher Replikat.
   
    Gewähren des Zugriffs von einem Cluster auf einen anderen Cluster in beide Richtungen:

    In unserem Beispiel:

    ```PowerShell
      Grant-SRAccess -ComputerName az2az1 -Cluster SRAZC2
    ```
    Wenn Sie Windows Server 2016 verwenden, führen Sie auch den folgenden Befehl aus:

    ```PowerShell
      Grant-SRAccess -ComputerName az2az3 -Cluster SRAZC1
    ```   
   
19. Erstellen Sie eine srpartnership für die Cluster:</ol>

    - Für Cluster **SRAZC1**.
    - Volumespeicherort:-c:\clusterstorage\datadisk1
    - Protokoll Speicherort:-g:
    - Für Cluster **SRAZC2**
    - Volumespeicherort:-c:\clusterstorage\datadisk2
    - Protokoll Speicherort:-g:

Führen Sie den folgenden Befehl aus:

```PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName **SRAZC2** -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDisk2 -DestinationLogVolumeName  g:
```