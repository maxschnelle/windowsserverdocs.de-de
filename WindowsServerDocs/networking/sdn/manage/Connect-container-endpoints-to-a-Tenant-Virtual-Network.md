---
title: Verbinden von Containerendpunkten mit einem virtuellen Mandantennetzwerk
description: In diesem Thema erfahren Sie, wie Sie Container Endpunkte mit einem vorhandenen virtuellen Mandanten Netzwerk verbinden, das über Sdn erstellt wurde. Sie verwenden den Netzwerktreiber l2bridge (und optional l2tunnel), der mit dem Windows libnetwork-Plug-in für docker verfügbar ist, um ein Container Netzwerk auf der Mandanten-VM zu erstellen.
manager: grcusanz
ms.topic: article
ms.assetid: f7af1eb6-d035-4f74-a25b-d4b7e4ea9329
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/24/2018
ms.openlocfilehash: fd05441ecc64c05778234dc00fa315bb406dfb40
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970807"
---
# <a name="connect-container-endpoints-to-a-tenant-virtual-network"></a>Verbinden von Containerendpunkten mit einem virtuellen Mandantennetzwerk

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie Container Endpunkte mit einem vorhandenen virtuellen Mandanten Netzwerk verbinden, das über Sdn erstellt wurde. Sie verwenden den Netzwerktreiber *l2bridge* (und optional *l2tunnel*), der mit dem Windows libnetwork-Plug-in für docker verfügbar ist, um ein Container Netzwerk auf der Mandanten-VM zu erstellen.

Im Thema [Container Netzwerktreiber](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/network-drivers-topologies) wurden die verschiedenen Netzwerktreiber erläutert, die über docker unter Windows verfügbar sind. Verwenden Sie für Sdn die Treiber *l2bridge* und *l2tunnel* . Für beide Treiber befindet sich jeder Container Endpunkt im gleichen virtuellen Subnetz wie der virtuelle Computer des Container Hosts (Mandant).

Mit dem Host Netzwerkdienst (HNS) über das Private Cloud-Plug-in werden die IP-Adressen für Container Endpunkte dynamisch zugewiesen. Die Container Endpunkte verfügen über eindeutige IP-Adressen, verwenden jedoch die gleiche Mac-Adresse des virtuellen Computers des Container Hosts (Mandant) aufgrund der Layer-2-Adressübersetzung.

Netzwerk Richtlinien (ACLs, Kapselung und QoS) für diese Container Endpunkte werden auf dem physischen Hyper-V-Host erzwungen, wie er vom Netzwerk Controller empfangen und in Verwaltungssystemen auf der obersten Ebene definiert wurde.

Der Unterschied zwischen den *l2bridge* -und *l2tunnel* -Treibern lautet wie folgt:


|                                                                                                                                                                                                                                                                            l2bridge                                                                                                                                                                                                                                                                            |                                                                                                 l2tunnel                                                                                                  |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Container Endpunkte, die sich auf befinden: <ul><li>Auf demselben virtuellen Container Host Computer und demselben Subnetz wird der gesamte Netzwerk Datenverkehr innerhalb des virtuellen Hyper-V-Switches überbrückt. </li><li>Für verschiedene Container Host-VMS oder in unterschiedlichen Subnetzen wird der Datenverkehr an den physischen Hyper-V-Host weitergeleitet. </li></ul>Die Netzwerk Richtlinie wird nicht erzwungen, da der Netzwerk Datenverkehr zwischen Containern auf demselben Host und im gleichen Subnetz nicht zum physischen Host fließt. Die Netzwerk Richtlinie gilt nur für Host-oder subnetznetzwerkdatenverkehr. | Der *gesamte* Netzwerk Datenverkehr zwischen zwei Container Endpunkten wird unabhängig vom Host oder Subnetz an den physischen Hyper-V-Host weitergeleitet. Die Netzwerk Richtlinie gilt sowohl für den subnetzübergreifenden als auch für den Host übergreifenden Netzwerk Datenverkehr. |

---

>[!NOTE]
>Diese Netzwerk Modi können nicht zum Verbinden von Windows-Container Endpunkten mit einem virtuellen Mandanten Netzwerk in Azure Public Cloud verwendet werden.


## <a name="prerequisites"></a>Voraussetzungen
-  Eine bereitgestellte Sdn-Infrastruktur mit dem Netzwerk Controller.
-  Ein virtuelles Mandanten Netzwerk wurde erstellt.
-  Ein bereitgestellter virtueller Computer für einen Mandanten mit aktiviertem Windows-Container Feature, installiertem docker und aktiviertem Hyper-V-Feature. Das Hyper-V-Feature ist erforderlich, um mehrere Binärdateien für l2bridge-und l2tunnel-Netzwerke zu installieren.

   ```powershell
   # To install HyperV feature without checks for nested virtualization
   dism /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V /All
   ```

>[!Note]
>Die [Genetzte Virtualisierung](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/nesting) und das verfügbar machen von Virtualisierungserweiterungen ist nur erforderlich, wenn Hyper-V-Container verwendet werden


## <a name="workflow"></a>Workflow

[1. Fügen Sie mithilfe des Netzwerk Controllers (Hyper-V-Host) 2 mehrere IP-Konfigurationen zu einer vorhandenen VM-NIC-Ressource hinzu](#1-add-multiple-ip-configurations). 
 [ Aktivieren Sie den Netzwerk Proxy auf dem Host, um ca-IP-Adressen für Container Endpunkte (Hyper-V-Host)](#2-enable-the-network-proxy) 
 [3 zuzuordnen. Installieren Sie das Private Cloud-Plug-in, um den Container Endpunkten (Container Host-VM) 4 Zertifizierungsstellen-IP-Adressen zuzuweisen](#3-install-the-private-cloud-plug-in) 
 [. Erstellen eines *l2bridge* -oder *l2tunnel* -Netzwerks mithilfe von docker (Container Host-VM)](#4-create-an-l2bridge-container-network)

>[!NOTE]
>Mehrere IP-Konfigurationen werden für VM-NIC-Ressourcen nicht unterstützt, die über System Center Virtual Machine Manager erstellt wurden Für diese Bereitstellungs Typen wird empfohlen, dass Sie die VM-NIC-Ressource mithilfe der Netzwerk Controller-PowerShell out-of-Band erstellen.

### <a name="1-add-multiple-ip-configurations"></a>1. Hinzufügen von mehreren IP-Konfigurationen
In diesem Schritt wird davon ausgegangen, dass die VM-NIC des virtuellen Mandanten Computers über eine IP-Konfiguration mit der IP-Adresse 192.168.1.9 verfügt und an die vnet-Ressourcen-ID "VNet1" und die VM-subnetzressource "Subnet1" im IP-Subnetz 192.168.1.0/24 angefügt ist. Wir fügen 10 IP-Adressen für Container aus 192.168.1.101-192.168.1.110 hinzu.

```powershell
Import-Module NetworkController

# Specify Network Controller REST IP or FQDN
$uri = "<NC REST IP or FQDN>"
$vnetResourceId = "VNet1"
$vsubnetResourceId = "Subnet1"

$vmnic= Get-NetworkControllerNetworkInterface -ConnectionUri $uri | where {$_.properties.IpConfigurations.Properties.PrivateIPAddress -eq "192.168.1.9" }
$vmsubnet = Get-NetworkControllerVirtualSubnet -VirtualNetworkId $vnetResourceId -ResourceId $vsubnetResourceId -ConnectionUri $uri

# For this demo, we will assume an ACL has already been defined; any ACL can be applied here
$allowallacl = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"


foreach ($i in 1..10)
{
    $newipconfig = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
    $props = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties

    $resourceid = "IP_192_168_1_1"
    if ($i -eq 10)
    {
        $resourceid += "10"
        $ipstr = "192.168.1.110"
    }
    else
    {
        $resourceid += "0$i"
        $ipstr = "192.168.1.10$i"
    }

    $newipconfig.ResourceId = $resourceid
    $props.PrivateIPAddress = $ipstr

    $props.PrivateIPAllocationMethod = "Static"
    $props.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $props.Subnet.ResourceRef = $vmsubnet.ResourceRef
    $props.AccessControlList = new-object Microsoft.Windows.NetworkController.AccessControlList
    $props.AccessControlList.ResourceRef = $allowallacl.ResourceRef

    $newipconfig.Properties = $props
    $vmnic.Properties.IpConfigurations += $newipconfig
}

New-NetworkControllerNetworkInterface -ResourceId $vmnic.ResourceId -Properties $vmnic.Properties -ConnectionUri $uri
```

### <a name="2-enable-the-network-proxy"></a>2. Aktivieren des Netzwerk Proxys
In diesem Schritt aktivieren Sie den Netzwerk Proxy, um mehrere IP-Adressen für den virtuellen Container Host Computer zuzuweisen.

Um den Netzwerk Proxy zu aktivieren, führen Sie das [ConfigureMCNP.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/ConfigureMCNP.ps1) Skript auf dem **Hyper-V-Host** aus, der den virtuellen Computer des Container Hosts (Mandant) hostet.

```powershell
PS C:\> ConfigureMCNP.ps1
```

### <a name="3-install-the-private-cloud-plug-in"></a>3. Installieren Sie das Private Cloud-Plug-in.
In diesem Schritt installieren Sie ein Plug-in, um dem HNS die Kommunikation mit dem Netzwerk Proxy auf dem Hyper-V-Host zu ermöglichen.

Um das Plug-in zu installieren, führen Sie das [InstallPrivateCloudPlugin.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/InstallPrivateCloudPlugin.ps1) Skript auf dem **virtuellen Computer des Container Hosts (Mandant)** aus.


```powershell
PS C:\> InstallPrivateCloudPlugin.ps1
```

### <a name="4-create-an-l2bridge-container-network"></a>4. Erstellen eines *l2bridge* -Container Netzwerks
In diesem Schritt verwenden Sie den `docker network create` Befehl auf dem **virtuellen Computer des Container Hosts (Tenant)** , um ein l2bridge-Netzwerk zu erstellen.

```powershell
# Create the container network
C:\> docker network create -d l2bridge --subnet="192.168.1.0/24" --gateway="192.168.1.1" MyContainerOverlayNetwork

# Attach a container to the MyContainerOverlayNetwork
C:\> docker run -it --network=MyContainerOverlayNetwork <image> <cmd>
```

>[!NOTE]
>Die statische IP-Zuweisung wird bei Verwendung mit dem Microsoft Sdn-Stapel nicht mit *l2bridge* -oder *l2tunnel* -Container Netzwerken unterstützt.

## <a name="more-information"></a>Weitere Informationen
Weitere Informationen zum Bereitstellen einer Sdn-Infrastruktur finden Sie unter Bereitstellen [einer Software definierten Netzwerkinfrastruktur](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure).

