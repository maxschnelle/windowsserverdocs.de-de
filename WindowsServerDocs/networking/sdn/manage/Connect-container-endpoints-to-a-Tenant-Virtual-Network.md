---
title: Container mit einem virtuellen Netzwerk verbinden
description: Dieses Thema ist Teil der Software Defined Networking-Anleitung für zum Verwalten von Mandantenworkloads und virtuellen Netzwerken in Windows Server2016.
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
ms.openlocfilehash: 801cf4b8f71935eb72d820d47e523a310fa64562
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="connect-container-endpoints-to-a-tenant-virtual-network"></a>Verbinden von containerendpunkten mit einem virtuellen mandantennetzwerk

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema erfahren Sie eine vorhandene virtuelle Netzwerk des Mandanten über den Microsoft Software Defined Networking (SDN)-Stapel erstellt containerendpunkte Verbindung. Wir verwenden die *l2bridge* (und optional *l2tunnel*) Treiber mit der Windows Libnetwork-Plug-In für Docker zum Erstellen eines Containernetzwerks auf dem Container-Host (Mandanten) virtuellen Computer verfügbar.

Gemäß der [Container Netzwerk](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/management/container_networking) auf der MSDN-Thema mehrere Netzwerktreiber sind über Docker unter Windows verfügbar. Die am besten geeigneten für SDN Treiber sind *l2bridge* und *l2tunnel*. Für beide Treiber ist jeder containerendpunkt im gleichen virtuellen Subnetz wie der Container-Host (Mandanten) virtuelle Computer. Die IP-Adressen für containerendpunkte werden durch den Host Networking Service (HNS) über die private Cloud-Plug-In dynamisch zugewiesen. Die containerendpunkte über eindeutige IP-Adressen, aber dieselbe MAC-Adresse des Container-Host (Mandanten) virtuellen Computers aufgrund der Layer-2-Adressübersetzung. Netzwerk-Richtlinie (z.B.: ACLs, Kapselung und QoS) für diesen containerendpunkten auf dem physischen Hyper-V-Host erzwungen wird, wie vom Netzwerkcontroller empfangen und höheren Schicht-Systemen definiert werden. Es ist eine geringfügige Unterschiede zwischen der *l2bridge* und *l2tunnel* Treiber, die nachfolgend erläutert wird.

- **L2-Brücke** -containerendpunkte, die auf demselben virtuellen containerhostcomputer befinden und im gleichen Subnetz verfügen alle Netzwerkdatenverkehr innerhalb der Hyper-V-Switch. Containerendpunkte, die auf verschiedene Container-Host virtuelle Maschinen befinden oder sind in unterschiedlichen Subnetzen, haben den Datenverkehr auf dem physischen Hyper-V-Host weitergeleitet. Da der Netzwerkverkehr zwischen Containern auf demselben Host und im gleichen Subnetz nicht auf dem physischen Host fließen, wird keine Netzwerkrichtlinie erzwungen. Richtlinie gilt nur für den Container Cross-Host oder subnetzübergreifende Netzwerkdatenverkehr.  
 
- **L2-Tunnel** - *alle* Netzwerkdatenverkehr zwischen zwei containerendpunkte auf dem physischen Hyper-V-Host unabhängig von der Host oder Subnetz weitergeleitet wird. Netzwerkrichtlinie wird für subnetzübergreifende und Cross-Host des Netzwerkdatenverkehrs erzwungen.   

>[!NOTE]
>Diese Netzwerkmodi funktionieren nicht für verbinden Windows Container-Endpunkte in eine virtuelle Netzwerk des Mandanten in Azure öffentliche Cloud

## <a name="prerequistes"></a>Prerequistes
 * Eine SDN-Infrastruktur mit Netzwerkcontroller bereitgestellt wurde
 * Ein virtuelle Netzwerk des Mandanten wurde erstellt
 * Ein Mandant virtuellen Computer wurde bereitgestellt, mit der Windows-Container-Feature aktiviert, Docker installiert und Hyper-V-Feature aktiviert

>[!Note]
>[Geschachtelte Virtualisierung](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/nesting) und Verfügbarmachen von Virtualisierungserweiterungen ist nicht erforderlich, es sei denn, Sie mit Hyper-V-Container der Hyper-v-Feature, installieren mehrere Binärdateien für l2bridge und l2tunnel Netzwerke erforderlich ist

```powershell
# To install HyperV feature without checks for nested virtualization
dism /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V /All 
```

 

## <a name="workflow"></a>Workflow

1. [Fügen Sie mehrere IP-Konfigurationen auf eine vorhandene VM-NIC-Ressource über Netzwerkcontroller](#Add) (Hyper-V-Host)
2. [Aktivieren den Netzwerk-Proxy auf dem Host zuweisen KA-IP-Adressen für containerendpunkte](#Enable) (Hyper-V-Host) 
3. [Installieren Sie die private Cloud-Plug-In containerendpunkte KA-IP-Adressen zuweisen](#Install) (Container-Host-VM) 
4. [Erstellen einer *l2bridge* oder *l2tunnel* Netzwerk mithilfe von Docker](#Create) (Container-Host-VM) 
 
>[!NOTE]
>Mehrere IP-Konfigurationen wird nicht unterstützt, auf VM-NIC-Ressourcen, die über System Center Virtual Machine Manager erstellt. Für diese Typen Bereitstellungen ist empfohlen, dass Sie die VM-NIC-Ressource Out of Band mithilfe von Netzwerk-Controller PowerShell erstellen.

### <a name="Add"></a>1. Fügen Sie 1. mehrere IP-Konfigurationen

In diesem Beispiel wird davon ausgegangen, dass die VM-NIC des virtuellen Computers an Mandanten bereits eine IP-Konfiguration mit IP-Adresse des 192.168.1.9 und -VNet Ressourcen-ID 'VNet1' und "Subnet1" VM-Subnetzressource im 192.168.1.0/24 IP-Subnetz verbunden ist. Wir werden 10 IP-Adressen für Container von 192.168.1.101 - 192.168.1.110 zu hinzugefügt.

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

### <a name="Enable"></a>2. Aktivieren des Netzwerk-Proxys

[ConfigureMCNP.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/ConfigureMCNP.ps1>)

Führen Sie dieses Skript auf den **Hyper-V-Host** die dient als Host für den Container Host (Mandanten) virtuellen Computer zum Aktivieren des Netzwerk-Proxys für die Container-Host virtuelle Maschine mehrere IP-Adressen zugewiesen werden.

```powershell
PS C:\> ConfigureMCNP.ps1
```

### <a name="Install"></a>3. Installieren Sie die Private Cloud-Plug-In

[InstallPrivateCloudPlugin.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/InstallPrivateCloudPlugin.ps1)

Führen Sie dieses Skript innerhalb der **(Mandanten) virtuellen containerhostcomputer** auf dem Host Networking Service (HNS) für die Kommunikation mit dem Netzwerkproxy auf dem Hyper-V-Host zulassen.

```powershell
PS C:\> InstallPrivateCloudPlugin.ps1
```

### <a name="Create"></a>4. erstellen Sie eine *l2bridge* Containernetzwerk

Auf der **(Mandanten) virtuellen containerhostcomputer** verwenden Sie die `docker network create`Befehl zum Erstellen eines l2bridge-Netzwerks

```powershell
# Create the container network
C:\> docker network create -d l2bridge --subnet="192.168.1.0/24" --gateway="192.168.1.1" MyContainerOverlayNetwork

# Attach a container to the MyContainerOverlayNetwork 
C:\> docker run -it --network=MyContainerOverlayNetwork <image> <cmd>
```

>[!NOTE]
>Statische IP-Adresszuweisung wird nicht unterstützt, mit *l2bridge* oder *l2tunnel* Container-Netzwerke mit dem Microsoft-SDN-Stapels verwendet.

## <a name="more-information"></a>Weitere Informationen
Weitere Infortation zur Bereitstellung einer SDN-Infrastruktur, finden Sie unter [Bereitstellen einer Software definiert Netzwerkinfrastruktur](https://technet.microsoft.com/en-us/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure).

