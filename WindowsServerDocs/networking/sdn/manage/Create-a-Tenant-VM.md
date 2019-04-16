---
title: Erstellen einer virtuellen Maschine und Verbinden mit einem virtuellen Mandantennetzwerk oder VLAN
description: Dieses Thema ist Teil der Software Defined Networking-Anleitung für zum Verwalten von Mandantenworkloads und virtuellen Netzwerken in Windows Server2016.
manager: brianlic
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
ms.openlocfilehash: 001eb3efa073e4ffbdfad41f88949303159a7274
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-a-vm-and-connect-to-a-tenant-virtual-network-or-vlan"></a>Erstellen einer virtuellen Maschine und Verbinden mit einem virtuellen Mandantennetzwerk oder VLAN

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema erstellen Sie ein Mandant virtuellen Computer \(VM\) und verbinden Sie den virtuellen Computer zu einem virtuellen Netzwerk, die Sie mit Hyper-V-Netzwerkvirtualisierung erstellt oder auf einem virtuellen lokalen Netzwerks \(VLAN\). 

Dieses Thema enthält die folgenden Abschnitte.

- [Erstellen einer virtuellen Maschine und Verbinden mit einem virtuellen Netzwerk mit den Netzwerkcontroller für Windows PowerShell-Cmdlets](#bkmk_vn)
- [Erstellen einer virtuellen Maschine und Verbinden mit einem VLAN mithilfe von NetworkControllerRESTWrappers](#bkmk_vlan)

## <a name="requirements"></a>Anforderungen
Beachten Sie vor dem Ausführen der Verfahrens in den folgenden Abschnitten, die folgenden Anforderungen.

1. Sie müssen Netzwerkadapter eines virtuellen Computers mit statischen Media Zugriffskontrolle erstellen \(MAC\) Adressen, damit die MAC-Adresse des virtuellen Computers nicht während der Lebensdauer des virtuellen Computers geändert wird. 
>[!NOTE]
>Wenn die VM-MAC-Adresse während der Lebensdauer des virtuellen Computers geändert wird, kann nicht Netzwerkcontroller die erforderliche Richtlinie für den Netzwerkadapter konfigurieren. Wenn die Richtlinie für den Netzwerkadapter nicht konfiguriert ist, der Netzwerkadapter wird für die Verarbeitung des Netzwerkdatenverkehrs verhindert, und die gesamte Kommunikation mit dem Netzwerk ein Fehler auftritt. 

2. Wenn der virtuelle Computer Zugriff auf das Netzwerk beim Start erforderlich ist, ist es wichtig, dass Sie den virtuellen Computer erst nach der letzte Konfigurationsschritt - Schnittstellen-ID festlegen, auf dem virtuellen Computer Netzwerkport Adapter nicht starten. Wenn Sie den virtuellen Computer starten, bevor Sie diesen Schrittabgeschlossen haben, kann nicht die virtuelle Maschine erst kommunizieren, im Netzwerk erstellt die Netzwerkschnittstelle in Netzwerk-Controller und der Domänencontroller verfügt über alle anwendbaren Richtlinien - Richtlinie für virtuelle Netzwerke, angewendet Access Control lists, \(ACLs\) und die Qualität des Diensts \(QoS\).

Sie können auch die Prozesse, die in diesem Thema für die Bereitstellung von virtuelle Appliances beschrieben werden. Mit einigen zusätzlichen Schrittenkönnen Sie Geräte zum Verarbeiten oder Datenpakete, die an oder von anderen virtuellen Maschinen auf dem virtuellen Netzwerk fließen überprüfen konfigurieren.

>[!IMPORTANT]
>Die folgenden Abschnitte enthalten, wird Windows PowerShell-Befehle, die Beispielwerte für viele Parameter enthalten. Stellen Sie sicher, dass Sie in diesen Befehlen Beispielwerte durch Werte, die für Ihre Bereitstellung geeignet sind ersetzen, bevor Sie diese Befehle ausführen.  

## <a name="bkmk_vn"></a>Erstellen einer virtuellen Maschine und Verbinden mit einem virtuellen Netzwerk mit den Netzwerkcontroller für Windows PowerShell-Cmdlets

Dieser Abschnitt enthält die folgenden Themen.

1.  [Erstellen eines virtuellen Computers mit einem VM-Netzwerkadapter, der eine statische MAC-Adresse verfügt.](#bkmk_create)
2.  [Rufen Sie das virtuelle Netzwerk, das das Subnetz enthält, das Sie den Netzwerkadapter eine Verbindung herstellen möchten](#bkmk_getvn)
3.  [Erstellen Sie ein Objekt für die Netzwerkschnittstelle in Netzwerk-Controller](#bkmk_object)
4.  [Holen Sie sich die InstanceId für die Netzwerkschnittstelle aus Netzwerkcontroller](#bkmk_getinstance)
5.  [Legen Sie die Schnittstellen-ID auf dem virtuellen Hyper-V-Computer Netzwerkport-Adapter](#bkmk_setinstance)
6.  [Starten Sie den virtuellen Computer](#bkmk_start)

### <a name="bkmk_create"></a>Erstellen eines virtuellen Computers mit einem VM-Netzwerkadapter, der eine statische MAC-Adresse verfügt.

Verwenden Sie zum Erstellen einer virtuellen Maschine mit einem Netzwerkadapter, die eine statische MAC-Adresse hat Befehl im folgenden Beispiel.

    
    New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch" 
    
    Set-VM -Name "MyVM" -ProcessorCount 4
    
    Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55" 
    

### <a name="bkmk_getvn"></a>Rufen Sie das virtuelle Netzwerk, das das Subnetz enthält, das Sie den Netzwerkadapter eine Verbindung herstellen möchten
Stellen Sie sicher, dass Sie bereits ein virtuelles Netzwerk erstellt haben, bevor Sie mit diesem Befehl wird. Weitere Informationen finden Sie unter [erstellen, löschen oder aktualisieren virtueller Mandantennetzwerke](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create%2c-delete%2c-or-update-tenant-virtual-networks).

Um das virtuelle Netzwerk zu erhalten, verwenden Sie den folgenden Befehl werden beispielsweise.

    
    $vnet = get-networkcontrollervirtualnetwork -connectionuri $uri -ResourceId “Contoso_WebTier”
    

>[!NOTE]
>Wenn Sie benutzerdefinierte ACLs für diese Netzwerkschnittstelle benötigen, klicken Sie dann die ACL jetzt erstellen mithilfe der Anweisungen im Thema [verwenden Zugriffssteuerungslisten (ACLs) zum Verwalten von Netzwerkdatenverkehrsflusses](../../sdn/manage/Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md)

### <a name="bkmk_object"></a>Erstellen Sie ein Objekt für die Netzwerkschnittstelle in Netzwerk-Controller

Um ein Objekt für die Netzwerkschnittstelle in Netzwerk-Controller zu erstellen, verwenden Sie den folgenden Befehl werden beispielsweise.

>[!NOTE]
>Wenn Sie eine benutzerdefinierte ACL nach dem vorherigen Schritterstellt haben, können Sie es jetzt verwenden.

    
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
    

### <a name="bkmk_getinstance"></a>Holen Sie sich die InstanceId für die Netzwerkschnittstelle aus Netzwerkcontroller
Verwenden Sie zum Abrufen der InstanceId für die Netzwerkschnittstelle aus Netzwerkcontroller Befehl im folgenden Beispiel.

    
    $nic = Get-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId "MyVM-Ethernet1"
    

### <a name="bkmk_setinstance"></a>Legen Sie die Schnittstellen-ID auf dem virtuellen Hyper-V-Computer Netzwerkport-Adapter
Um die Schnittstellen-ID auf dem virtuellen Hyper-V-Computer Adapter Netzwerkport festzulegen, verwenden Sie den folgenden Befehl werden beispielsweise.

>[!NOTE]
>Sie müssen diese Befehle auf dem Hyper-V-Host ausführen, auf dem der virtuelle Computer installiert ist.

    
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
    

### <a name="bkmk_start"></a>Starten Sie den virtuellen Computer
Verwenden Sie zum Starten des virtuellen Computers Befehl im folgenden Beispiel.

    
    Get-VM -Name “MyVM” | Start-VM 
    
Sie haben jetzt erfolgreich erstellt eine virtuelle Maschine, die virtuelle Maschine zu einem Mandanten virtuelle Netzwerk verbunden und des virtuellen Computers gestartet, sodass mandantenworkloads verarbeitet werden können.

## <a name="bkmk_vlan"></a>Erstellen einer virtuellen Maschine und Verbinden mit einem VLAN mithilfe von NetworkControllerRESTWrappers

Dieser Abschnitt enthält die folgenden Themen.

1. [Erstellen Sie des virtuellen Computers, und weisen Sie eine statische MAC-Adresse](#bkmk_mac)
2. [Legen Sie die VLAN-ID auf dem VM-Netzwerkadapter](#bkmk_vid)
3. [Rufen Sie das logische Netzwerk-Subnetz und erstellen Sie die Netzwerkschnittstelle](#bkmk_subnet)
4. [Legen Sie die InstanceId auf dem Hyper-V-Port](#bkmk_instance)
5. [Starten Sie den virtuellen Computer](#bkmk_startvlan)


###<a name="bkmk_mac"></a>Erstellen Sie des virtuellen Computers, und weisen Sie eine statische MAC-Adresse
Zum Erstellen eines virtuellen Computers und Zuweisen einer statischen Media \(MAC\)-Adresse des virtuellen Computers, können Sie die folgenden Beispielbefehle verwenden.

    New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch" 

    Set-VM -Name "MyVM" -ProcessorCount 4

    Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55" 

###<a name="bkmk_vid"></a>Legen Sie die VLAN-ID auf dem VM-Netzwerkadapter
Um die VLAN-ID auf dem Netzwerkadapter festzulegen, können Sie den folgenden Befehl werden beispielsweise.


    Set-VMNetworkAdapterIsolation –VMName “MyVM” -AllowUntaggedTraffic $true -IsolationMode VLAN -DefaultIsolationId 123


###<a name="bkmk_subnet"></a>Rufen Sie das logische Netzwerk-Subnetz und erstellen Sie die Netzwerkschnittstelle

Um das logische Netzwerk-Subnetz zu erhalten, und erstellen die Netzwerkschnittstelle, die mit dem logischen Netzwerk-Subnetz, können Sie die folgenden Beispielbefehle verwenden.


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
    

###<a name="bkmk_instance"></a>Legen Sie die InstanceId auf dem Hyper-V-Port
Um die InstanceId auf dem Hyper-V-Port festzulegen, können Sie die folgenden Beispielbefehle auf dem Hyper-V-Host, wo sich die virtuelle Maschine befindet.

  
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


###<a name="bkmk_startvlan"></a>Starten Sie den virtuellen Computer
Um den virtuellen Computer zu starten, können Sie den folgenden Befehl werden beispielsweise.


    Get-VM -Name “MyVM” | Start-VM 

Sie haben jetzt erfolgreich erstellt eine virtuelle Maschine, die virtuelle Maschine mit einem VLAN verbunden und des virtuellen Computers gestartet, sodass mandantenworkloads verarbeitet werden können.

  

