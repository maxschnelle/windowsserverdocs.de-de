---
title: Verbinden von Containerendpunkten mit einem virtuellen Mandantennetzwerk
description: In diesem Thema erfahren Sie, wie zur Verbindung mit eines vorhandenen virtuellen Netzwerks von Mandanten erstellt, die über SDN containerendpunkte. Verwenden Sie die l2bridge (und optional l2tunnel) Netzwerktreiber verfügbar, mit der Windows Libnetwork-Plug-In für Docker, um ein containernetzwerk für den Mandanten-VM zu erstellen.
manager: ravirao
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7af1eb6-d035-4f74-a25b-d4b7e4ea9329
ms.author: pashort
author: jmesser81
ms.date: 08/24/2018
ms.openlocfilehash: 1968a4db9231459fe5858d9a0f3ba5e8f317ed1b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872741"
---
# <a name="connect-container-endpoints-to-a-tenant-virtual-network"></a>Verbinden von Containerendpunkten mit einem virtuellen Mandantennetzwerk

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema erfahren Sie, wie zur Verbindung mit eines vorhandenen virtuellen Netzwerks von Mandanten erstellt, die über SDN containerendpunkte. Sie verwenden die *l2bridge* (und optional *l2tunnel*) Netzwerktreiber verfügbar, mit der Windows Libnetwork-Plug-In für Docker, um ein containernetzwerk für den Mandanten-VM zu erstellen.

In der [Container Netzwerktreiber](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/network-drivers-topologies) Thema erläutert die mehrere Netzwerktreiber sind über Docker unter Windows verfügbar. Verwenden Sie für SDN, das *l2bridge* und *l2tunnel* Treiber. Ist für beide Treiber jeder containerendpunkt im gleichen virtuellen Subnetz wie der Container-Host (Mandant) virtuelle Computer. 

Der Host Networking Service (HNS), über die private Cloud-Plug-in, wird die IP-Adressen für den containerendpunkte dynamisch zugewiesen. Den containerendpunkte über eindeutige IP-Adressen, aber dieselbe MAC-Adresse des Container-Host (Mandant) virtuellen Computers aufgrund der Layer-2-Adressübersetzung. 

Netzwerkrichtlinie (ACLs, Kapselung und QoS) für diesen containerendpunkten werden auf dem physischen Hyper-V-Host erzwungen wird, wie durch den Netzwerkcontroller empfangen und in Verwaltungssystemen auf höherer Ebene definiert. 

Der Unterschied zwischen der *l2bridge* und *l2tunnel* Treiber sind:

| l2bridge | l2tunnel |
| --- | --- |
|Containerendpunkte, die sich befinden: <ul><li>Der gleiche Container Hosten virtueller Computer und im gleichen Subnetz gesamten Netzwerkdatenverkehr innerhalb des virtuellen Hyper-V-Switches überbrückt. </li><li>Verschiedene Container Hosten von virtuellen Computern oder in unterschiedlichen Subnetzen müssen den Datenverkehr weitergeleitet wird, auf dem physischen Hyper-V-Host. </li></ul>Netzwerkrichtlinie wird nicht erzwungen zu erhalten, da der Netzwerkdatenverkehr zwischen Containern auf dem gleichen Host und im gleichen Subnetz werden erst übernommen, auf dem physischen Host. Netzwerkrichtlinie gilt nur auf Cross-Host oder subnetzübergreifende Container des Netzwerkdatenverkehrs. | *ALLE* Netzwerkdatenverkehr zwischen zwei containerendpunkte auf dem physischen Hyper-V-Host unabhängig vom Host oder das Subnetz weitergeleitet wird. Netzwerkrichtlinie gilt für sowohl subnetzübergreifende und Cross-Host Netzwerkdatenverkehr. |
---

>[!NOTE]
>Diese Netzwerkmodi funktionieren nicht für die eine Verbindung herstellen Windows Container-Endpunkten in einem virtuellen mandantennetzwerk in öffentlichen Azure-Cloud.


## <a name="prerequisites"></a>Vorraussetzungen
-  Eine bereitgestellte SDN-Infrastruktur, mit dem Netzwerkcontroller.
-  Einem virtuellen mandantennetzwerk wurde erstellt.
-  Ein bereitgestellter Mandant virtuellen Computer mit dem Windows-containerfeature aktiviert Docker installiert und Hyper-V-Feature aktiviert. Das Hyper-V-Feature ist erforderlich, um mehrere Binärdateien für l2bridge und l2tunnel Netzwerke zu installieren.

   ```powershell
   # To install HyperV feature without checks for nested virtualization
   dism /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V /All 
   ```

>[!Note]
>[Geschachtelte Virtualisierung](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/nesting) und Verfügbarmachen von Virtualisierungserweiterungen ist nicht erforderlich, es sei denn, mithilfe von Hyper-V-Container. 


## <a name="workflow"></a>Workflow

[1. Hinzufügen mehrerer IP-Konfigurationen einer vorhandenen VM-NIC-Ressource über den Netzwerkcontroller (Hyper-V-Host)](#1-add-multiple-ip-configurations)
[2. Aktivieren den Netzwerk-Proxy auf dem Host zuweisen KA-IP-Adressen für den containerendpunkte (Hyper-V-Host) ](#2-enable-the-network-proxy) 
 [3. Installieren Sie die private Cloud-Plug-in den containerendpunkte (Containerhost-VM) KA-IP-Adressen zuweisen ](#3-install-the-private-cloud-plug-in) 
 [4. Erstellen Sie eine *l2bridge* oder *l2tunnel* Netzwerk mithilfe von Docker (Container-Host-VM) ](#4-create-an-l2bridge-container-network)
 
>[!NOTE]
>Mehrere IP-Konfigurationen wird nicht unterstützt, auf der VM-NIC-Ressourcen, die über System Center Virtual Machine Manager erstellt. Es wird für solche Bereitstellungen empfohlen, die Erstellung der VM-NIC-Ressource Out-of-Band-mithilfe Netzwerks Controller PowerShell.

### <a name="1-add-multiple-ip-configurations"></a>1. Fügen Sie mehrerer IP-Konfigurationen hinzu
In diesem Schritt gehen wir davon aus, die VM-NIC der VM-Mandanten verfügt über eine IP-Konfiguration mit IP-Adresse des 192.168.1.9 und eine VNet-Ressourcen-ID von "VNet1" und VM-Subnetz-Ressource von "Subnet1" angefügt ist, in dem 192.168.1.0/24 IP-Subnetz. Wir 10 IP-Adressen für Container hinzufügen, aus 192.168.1.101 - 192.168.1.110 zu.

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

### <a name="2-enable-the-network-proxy"></a>2. Aktivieren des Netzwerk-Proxys
In diesem Schritt können Sie den Netzwerkproxy für den Container-Host virtuellen Computer mehrere IP-Adressen zuweisen. 

Um den Netzwerkproxy zu aktivieren, führen Sie die [ConfigureMCNP.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/ConfigureMCNP.ps1) Beispielskript auf die **Hyper-V-Host** den Container Host (Mandant) virtuellen Computer hostet.

```powershell
PS C:\> ConfigureMCNP.ps1
```

### <a name="3-install-the-private-cloud-plug-in"></a>3. Installieren Sie die Private Cloud-Plug-in
In diesem Schritt installieren Sie ein plug-in, um die HNS für die Kommunikation mit dem Netzwerkproxy auf dem Hyper-V-Host zu ermöglichen.

Um das plug-in installieren, führen die [InstallPrivateCloudPlugin.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/InstallPrivateCloudPlugin.ps1) Skript innerhalb der **(Mandant) virtuellen containerhostcomputer**.


```powershell
PS C:\> InstallPrivateCloudPlugin.ps1
```

### <a name="4-create-an-l2bridge-container-network"></a>4. Erstellen Sie eine *l2bridge* Containernetzwerk
In diesem Schritt verwenden Sie die `docker network create` Befehl die **(Mandant) virtuellen containerhostcomputer** ein l2bridge-Netzwerks zu erstellen. 

```powershell
# Create the container network
C:\> docker network create -d l2bridge --subnet="192.168.1.0/24" --gateway="192.168.1.1" MyContainerOverlayNetwork

# Attach a container to the MyContainerOverlayNetwork 
C:\> docker run -it --network=MyContainerOverlayNetwork <image> <cmd>
```

>[!NOTE]
>Statische IP-Adresszuweisung wird nicht unterstützt, mit *l2bridge* oder *l2tunnel* Container Netzwerke bei der Verwendung mit den Microsoft-SDN-Stapel.

## <a name="more-information"></a>Weitere Informationen
Weitere Informationen zu eine SDN-Infrastruktur bereitstellen, finden Sie unter [Bereitstellen einer Software definierten Netzwerkinfrastruktur](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure).

