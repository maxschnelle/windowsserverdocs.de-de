---
title: Erstellen eines virtuellen Computers und Verbinden mit einem virtuellen Mandantennetzwerk oder VLAN
description: In diesem Thema erfahren Sie, wie Sie eine Mandanten-VM erstellen und mit einem virtuellen Netzwerk verbinden, das Sie mit der Hyper-V-Netzwerkvirtualisierung oder einem virtuellen lokalen Netzwerk (VLAN) erstellt haben.
manager: grcusanz
ms.topic: article
ms.assetid: 3c62f533-1815-4f08-96b1-dc271f5a2b36
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/24/2018
ms.openlocfilehash: 0b82128c703f5f3d1fe357beae90a15481232d5c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970777"
---
# <a name="create-a-vm-and-connect-to-a-tenant-virtual-network-or-vlan"></a>Erstellen eines virtuellen Computers und Verbinden mit einem virtuellen Mandantennetzwerk oder VLAN

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erstellen Sie eine Mandanten-VM und verbinden Sie entweder mit einem virtuellen Netzwerk, das Sie mit der Hyper-V-Netzwerkvirtualisierung oder mit einem virtuellen lokalen Netzwerk (VLAN) erstellt haben. Sie können Windows PowerShell-Cmdlets für Netzwerk Controller verwenden, um eine Verbindung mit einem virtuellen Netzwerk oder networkcontrollerrestwrappern herzustellen, um eine Verbindung mit einem VLAN herzustellen.

Verwenden Sie die in diesem Thema beschriebenen Prozesse, um virtuelle Geräte bereitzustellen. Mit einigen zusätzlichen Schritten können Sie Geräte für die Verarbeitung oder Überprüfung von Datenpaketen konfigurieren, die zu oder von anderen VMS auf dem Virtual Network fließen.

Die Abschnitte in diesem Thema enthalten Beispiele für Windows PowerShell-Befehle, die Beispiel Werte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispiel Werte in diesen Befehlen durch Werte ersetzen, die für die Bereitstellung geeignet sind, bevor Sie diese Befehle ausführen.


## <a name="prerequisites"></a>Voraussetzungen

1. VM-Netzwerkadapter, die für die Lebensdauer des virtuellen Computers mit statischen Mac-Adressen erstellt wurden.<p>Wenn sich die Mac-Adresse während der VM-Lebensdauer ändert, kann der Netzwerk Controller die erforderliche Richtlinie für den Netzwerkadapter nicht konfigurieren. Wenn Sie die Richtlinie für das Netzwerk nicht konfigurieren, wird verhindert, dass der Netzwerkadapter Netzwerk Datenverkehr verarbeitet, und die gesamte Kommunikation mit dem Netzwerk schlägt fehl.

2. Wenn für den virtuellen Computer beim Start Netzwerk Zugriff erforderlich ist, starten Sie den virtuellen Computer erst, nachdem Sie die Schnittstellen-ID auf dem VM-Netzwerkadapter Port festgelegt haben. Wenn Sie den virtuellen Computer vor dem Festlegen der Schnittstellen-ID starten und die Netzwerkschnittstelle nicht vorhanden ist, kann der virtuelle Computer nicht im Netzwerk im Netzwerk Controller kommunizieren, und alle Richtlinien werden angewendet.

3. Wenn Sie benutzerdefinierte ACLs für diese Netzwerkschnittstelle benötigen, erstellen Sie die ACL jetzt mithilfe der Anweisungen im Thema [Verwenden von Access Control Listen (ACLs) zum Verwalten des Netzwerk Datenverkehrs für Daten Center](../../sdn/manage/Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md) .

Stellen Sie sicher, dass Sie bereits eine Virtual Network erstellt haben, bevor Sie diesen Beispiel Befehl verwenden. Weitere Informationen finden Sie unter [erstellen, löschen oder Aktualisieren von virtuellen Mandanten Netzwerken](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create%2c-delete%2c-or-update-tenant-virtual-networks).

## <a name="create-a-vm-and-connect-to-a-virtual-network-by-using-the-windows-powershell-network-controller-cmdlets"></a>Erstellen eines virtuellen Computers und Herstellen einer Verbindung mit einem Virtual Network mithilfe der Windows PowerShell-Cmdlets für Netzwerk Controller


1. Erstellen Sie einen virtuellen Computer mit einem VM-Netzwerkadapter, der über eine statische MAC-Adresse verfügt.

   ```PowerShell
   New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch"

   Set-VM -Name "MyVM" -ProcessorCount 4

   Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55"
   ```

2. Holen Sie sich das virtuelle Netzwerk, das das Subnetz enthält, mit dem Sie den Netzwerkadapter verbinden möchten.

   ```Powershell
   $vnet = get-networkcontrollervirtualnetwork -connectionuri $uri -ResourceId "Contoso_WebTier"
   ```

3. Erstellen Sie ein Netzwerkschnittstellen Objekt im Netzwerk Controller.

   >[!TIP]
   >In diesem Schritt verwenden Sie die benutzerdefinierte ACL.

   ```PowerShell
   $vmnicproperties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceProperties
   $vmnicproperties.PrivateMacAddress = "001122334455"
   $vmnicproperties.PrivateMacAllocationMethod = "Static"
   $vmnicproperties.IsPrimary = $true

   $vmnicproperties.DnsSettings = new-object Microsoft.Windows.NetworkController.NetworkInterfaceDnsSettings
   $vmnicproperties.DnsSettings.DnsServers = @("24.30.1.11", "24.30.1.12")

   $ipconfiguration = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
   $ipconfiguration.resourceid = "MyVM_IP1"
   $ipconfiguration.properties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties
   $ipconfiguration.properties.PrivateIPAddress = "24.30.1.101"
   $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"

   $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
   $ipconfiguration.properties.subnet.ResourceRef = $vnet.Properties.Subnets[0].ResourceRef

   $vmnicproperties.IpConfigurations = @($ipconfiguration)
   New-NetworkControllerNetworkInterface –ResourceID "MyVM_Ethernet1" –Properties $vmnicproperties –ConnectionUri $uri
   ```

4. Holen Sie sich die InstanceId für die Netzwerkschnittstelle vom Netzwerk Controller.

   ```PowerShell
    $nic = Get-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId "MyVM-Ethernet1"
   ```

5. Legen Sie die Schnittstellen-ID auf dem Hyper-V-VM-Netzwerkadapter Port fest.

   >[!NOTE]
   >Sie müssen diese Befehle auf dem Hyper-V-Host ausführen, auf dem die VM installiert ist.

   ```PowerShell
   #Do not change the hardcoded IDs in this section, because they are fixed values and must not change.

   $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"

   $vmNics = Get-VMNetworkAdapter -VMName "MyVM"

   $CurrentFeature = Get-VMSwitchExtensionPortFeature -FeatureId $FeatureId -VMNetworkAdapter $vmNics

   if ($CurrentFeature -eq $null)
   {
   $Feature = Get-VMSystemSwitchExtensionPortFeature -FeatureId $FeatureId

   $Feature.SettingData.ProfileId = "{$($nic.InstanceId)}"
   $Feature.SettingData.NetCfgInstanceId = "{56785678-a0e5-4a26-bc9b-c0cba27311a3}"
   $Feature.SettingData.CdnLabelString = "TestCdn"
   $Feature.SettingData.CdnLabelId = 1111
   $Feature.SettingData.ProfileName = "Testprofile"
   $Feature.SettingData.VendorId = "{1FA41B39-B444-4E43-B35A-E1F7985FD548}"
   $Feature.SettingData.VendorName = "NetworkController"
   $Feature.SettingData.ProfileData = 1

   Add-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature  $Feature -VMNetworkAdapter $vmNics
   }
   else
   {
   $CurrentFeature.SettingData.ProfileId = "{$($nic.InstanceId)}"
   $CurrentFeature.SettingData.ProfileData = 1

   Set-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature $CurrentFeature  -VMNetworkAdapter $vmNic
   }
   ```

6. Starten Sie den virtuellen Computer.

   ```PowerShell
    Get-VM -Name "MyVM" | Start-VM
   ```

Sie haben erfolgreich einen virtuellen Computer erstellt, den virtuellen Computer mit einem Mandanten Virtual Network verbunden und den virtuellen Computer gestartet, damit er workerworkloads verarbeiten kann.

## <a name="create-a-vm-and-connect-to-a-vlan-by-using-networkcontrollerrestwrappers"></a>Erstellen eines virtuellen Computers und Herstellen einer Verbindung mit einem VLAN mithilfe von networkcontrollerrestwrapper


1. Erstellen Sie den virtuellen Computer, und weisen Sie dem virtuellen Computer eine statische MAC-Adresse zu.

   ```PowerShell
   New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch"

   Set-VM -Name "MyVM" -ProcessorCount 4

   Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55"
   ```

2. Legen Sie die VLAN-ID auf dem VM-Netzwerkadapter fest.

   ```PowerShell
   Set-VMNetworkAdapterIsolation –VMName "MyVM" -AllowUntaggedTraffic $true -IsolationMode VLAN -DefaultIsolationId 123
   ```

3. Rufen Sie das logische Netzwerksubnetz ab, und erstellen Sie die Netzwerkschnittstelle.

   ```PowerShell
    $logicalnet = get-networkcontrollerLogicalNetwork -connectionuri $uri -ResourceId "00000000-2222-1111-9999-000000000002"

    $vmnicproperties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceProperties
    $vmnicproperties.PrivateMacAddress = "00-1D-C8-B7-01-02"
    $vmnicproperties.PrivateMacAllocationMethod = "Static"
    $vmnicproperties.IsPrimary = $true

    $vmnicproperties.DnsSettings = new-object Microsoft.Windows.NetworkController.NetworkInterfaceDnsSettings
    $vmnicproperties.DnsSettings.DnsServers = $logicalnet.Properties.Subnets[0].DNSServers

    $ipconfiguration = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
    $ipconfiguration.resourceid = "MyVM_Ip1"
    $ipconfiguration.properties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties
    $ipconfiguration.properties.PrivateIPAddress = "10.127.132.177"
    $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"

    $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $ipconfiguration.properties.subnet.ResourceRef = $logicalnet.Properties.Subnets[0].ResourceRef

    $vmnicproperties.IpConfigurations = @($ipconfiguration)
    $vnic = New-NetworkControllerNetworkInterface –ResourceID "MyVM_Ethernet1" –Properties $vmnicproperties –ConnectionUri $uri

    $vnic.InstanceId
   ```

4. Legen Sie die InstanceId auf dem Hyper-V-Port fest.

   ```PowerShell
   #The hardcoded Ids in this section are fixed values and must not change.
   $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"

   $vmNics = Get-VMNetworkAdapter -VMName "MyVM"

   $CurrentFeature = Get-VMSwitchExtensionPortFeature -FeatureId $FeatureId -VMNetworkAdapter $vmNic

   if ($CurrentFeature -eq $null)
   {
       $Feature = Get-VMSystemSwitchExtensionFeature -FeatureId $FeatureId

       $Feature.SettingData.ProfileId = "{$InstanceId}"
       $Feature.SettingData.NetCfgInstanceId = "{56785678-a0e5-4a26-bc9b-c0cba27311a3}"
       $Feature.SettingData.CdnLabelString = "TestCdn"
       $Feature.SettingData.CdnLabelId = 1111
       $Feature.SettingData.ProfileName = "Testprofile"
       $Feature.SettingData.VendorId = "{1FA41B39-B444-4E43-B35A-E1F7985FD548}"
       $Feature.SettingData.VendorName = "NetworkController"
       $Feature.SettingData.ProfileData = 1

       Add-VMSwitchExtensionFeature -VMSwitchExtensionFeature  $Feature -VMNetworkAdapter $vmNic
   }
   else
   {
       $CurrentFeature.SettingData.ProfileId = "{$InstanceId}"
       $CurrentFeature.SettingData.ProfileData = 1

       Set-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature $CurrentFeature  -VMNetworkAdapter $vmNic
   }
   ```

5. Starten Sie den virtuellen Computer.

   ```PowerShell
   Get-VM -Name "MyVM" | Start-VM
   ```

Sie haben erfolgreich einen virtuellen Computer erstellt, den virtuellen Computer mit einem VLAN verbunden und den virtuellen Computer gestartet, damit er workerworkloads verarbeiten kann.



