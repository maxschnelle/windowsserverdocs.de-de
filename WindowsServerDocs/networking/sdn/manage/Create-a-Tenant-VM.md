---
title: Erstellen einer VM und Verbinden mit einem virtuellen Mandantennetzwerk oder VLAN
description: In diesem Thema erläutert, wie Sie einen Mandanten-VM erstellen und verbinden Sie es zu einem virtuellen Netzwerk, das Sie mit Hyper-V-Netzwerkvirtualisierung erstellt oder auf einem virtuellen LAN (VLAN).
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c62f533-1815-4f08-96b1-dc271f5a2b36
ms.author: pashort
author: shortpatti
ms.date: 08/24/2018
ms.openlocfilehash: e23e6c020c12dd4900caa368daae0cc6dbeceaf4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856811"
---
# <a name="create-a-vm-and-connect-to-a-tenant-virtual-network-or-vlan"></a>Erstellen einer VM und Verbinden mit einem virtuellen Mandantennetzwerk oder VLAN

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema müssen Sie einen Mandanten-VM erstellen und verbinden Sie es zu einem virtuellen Netzwerk, das Sie mit Hyper-V-Netzwerkvirtualisierung erstellt oder auf einem virtuellen LAN (VLAN). Sie können den Netzwerkcontroller für Windows PowerShell-Cmdlets verwenden, zur Verbindung mit einem virtuellen Netzwerk oder NetworkControllerRESTWrappers für die Verbindung mit einem VLAN.

Verwenden Sie die in diesem Thema beschriebenen Prozesse, um virtuelle Geräte bereitzustellen. Mit einigen zusätzlichen Schritten können Sie Geräte, die zum Verarbeiten, oder überprüfen die Datenpakete, die zu oder von anderen virtuellen Computern im virtuellen Netzwerk fließen konfigurieren.

In den Abschnitten in diesem Thema enthalten die Windows PowerShell-Beispielbefehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie die Beispielwerte in diesen Befehlen durch Werte, die für die Bereitstellung sinnvoll sind ersetzen, bevor Sie diese Befehle ausführen. 


## <a name="prerequisites"></a>Vorraussetzungen

1. Netzwerkadapter eines virtuellen Computers mit statischer MAC-Adressen für die Lebensdauer des virtuellen Computers erstellt.<p>Wenn die MAC-Adresse während der Lebensdauer des virtuellen Computers ändert, kann nicht den Netzwerkcontroller die erforderlichen Richtlinie für den Netzwerkadapter konfigurieren. Konfigurieren die Richtlinie für das Netzwerk nicht verhindert, dass des Netzwerkadapters Verarbeitung des Netzwerkdatenverkehrs, und die gesamte Kommunikation mit dem Netzwerk ein Fehler auftritt.  

2. Wenn der virtuelle Computer mit Netzwerkzugriff beim Start erforderlich ist, starten Sie den virtuellen Computer nicht erst nach dem Festlegen der Schnittstellen-ID, auf dem virtuellen Computer Netzwerkadapters. Wenn Sie den virtuellen Computer starten, bevor Sie die Schnittstellen-ID festlegen und die Netzwerkschnittstelle ist nicht vorhanden, kann nicht der virtuellen Computer im Netzwerk, in dem Netzwerkcontroller und alle angewendeten Richtlinien kommunizieren.

3. Wenn Sie benutzerdefinierte ACLs für diese Schnittstelle benötigen, erstellen Sie die ACL jetzt mithilfe der Anweisungen im Thema [verwenden Zugriffssteuerungslisten (ACLs) zum Verwalten von Datencenter-Netzwerk fließt der Datenverkehr](../../sdn/manage/Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md)

Stellen Sie sicher, dass Sie bereits ein virtuelles Netzwerk erstellt haben, bevor Sie mit dem folgenden Beispielbefehl. Weitere Informationen finden Sie unter [erstellen, löschen oder aktualisieren virtueller Mandantennetzwerke](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create%2c-delete%2c-or-update-tenant-virtual-networks).

## <a name="create-a-vm-and-connect-to-a-virtual-network-by-using-the-windows-powershell-network-controller-cmdlets"></a>Erstellen eines virtuellen Computers und Herstellen von Verbindungen mit einem virtuellen Netzwerk mithilfe von Netzwerkcontroller für Windows PowerShell-cmdlets


1. Erstellen eines virtuellen Computers mit einem VM-Netzwerkadapter, der über eine statische MAC-Adresse verfügt. 

   ```PowerShell    
   New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch" 
    
   Set-VM -Name "MyVM" -ProcessorCount 4
    
   Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55" 
   ```

2. Rufen Sie das virtuelle Netzwerk mit dem Subnetz aus, das Sie den Netzwerkadapter eine Verbindung herstellen möchten.

   ```Powershell 
   $vnet = get-networkcontrollervirtualnetwork -connectionuri $uri -ResourceId “Contoso_WebTier”
   ```

3. Erstellen Sie eine Netzwerkschnittstellenobjekt im Netzwerkcontroller.

   >[!TIP]
   >In diesem Schritt verwenden Sie die benutzerdefinierte ACL an.

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
   $ipconfiguration.properties.PrivateIPAddress = “24.30.1.101”
   $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"
    
   $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
   $ipconfiguration.properties.subnet.ResourceRef = $vnet.Properties.Subnets[0].ResourceRef
    
   $vmnicproperties.IpConfigurations = @($ipconfiguration)
   New-NetworkControllerNetworkInterface –ResourceID “MyVM_Ethernet1” –Properties $vmnicproperties –ConnectionUri $uri
   ```

4. Rufen Sie die Instanz-ID für die Netzwerkschnittstelle, vom Netzwerkcontroller.

   ```PowerShell 
    $nic = Get-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId "MyVM-Ethernet1"
   ```

5. Legen Sie die Schnittstellen-ID für die Hyper-V-VM-Netzwerkadapters ab.

   >[!NOTE]
   >Sie müssen diese Befehle auf dem Hyper-V-Host ausführen, in der virtuellen Computer installiert ist.

   ```PowerShell 
   #Do not change the hardcoded IDs in this section, because they are fixed values and must not change.
    
   $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"
    
   $vmNics = Get-VMNetworkAdapter -VMName “MyVM”
    
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
    Get-VM -Name “MyVM” | Start-VM 
   ```

Sie haben erfolgreich eine virtuelle Maschine erstellt, den virtuellen Computer zu einem virtuellen Netzwerk des Mandanten verbunden, und den virtuelle Computer gestartet, sodass mandantenworkloads verarbeitet werden kann.

## <a name="create-a-vm-and-connect-to-a-vlan-by-using-networkcontrollerrestwrappers"></a>Erstellen eines virtuellen Computers und Herstellen von Verbindungen mit einem VLAN mithilfe von NetworkControllerRESTWrappers


1. Erstellen Sie des virtuellen Computers, und weisen Sie eine statische MAC-Adresse des virtuellen Computers.

   ```PowerShell
   New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch" 

   Set-VM -Name "MyVM" -ProcessorCount 4

   Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55" 
   ```

2. Legen Sie die VLAN-ID für den VM-Netzwerkadapter an.

   ```PowerShell
   Set-VMNetworkAdapterIsolation –VMName “MyVM” -AllowUntaggedTraffic $true -IsolationMode VLAN -DefaultIsolationId 123
   ```

3. Rufen Sie das logische Netzwerk-Subnetz aus, und erstellen Sie die Netzwerkschnittstelle. 

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
    $ipconfiguration.properties.PrivateIPAddress = “10.127.132.177”
    $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"

    $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $ipconfiguration.properties.subnet.ResourceRef = $logicalnet.Properties.Subnets[0].ResourceRef

    $vmnicproperties.IpConfigurations = @($ipconfiguration)
    $vnic = New-NetworkControllerNetworkInterface –ResourceID “MyVM_Ethernet1” –Properties $vmnicproperties –ConnectionUri $uri

    $vnic.InstanceId
   ```

4. Legen Sie die Instanz-ID, auf dem Hyper-V-Port.

   ```PowerShell  
   #The hardcoded Ids in this section are fixed values and must not change.
   $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"

   $vmNics = Get-VMNetworkAdapter -VMName “MyVM”

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
   Get-VM -Name “MyVM” | Start-VM 
   ```

Sie haben erfolgreich eine virtuelle Maschine erstellt, den virtuellen Computer mit einem VLAN verbunden und den virtuelle Computer gestartet, sodass mandantenworkloads verarbeitet werden kann.

  

