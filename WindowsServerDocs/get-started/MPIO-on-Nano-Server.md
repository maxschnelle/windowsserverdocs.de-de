---
title: MPIO unter Nano Server
description: Konfigurieren von MPIO unter Nano
ms.prod: windows-server
manager: DonGill
ms.date: 09/06/2017
ms.technology: server-nano
ms.topic: article
ms.assetid: fbef4d91-e18c-4f1b-952f-a9a7ad46cd74
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: fb38976ca6b2297562e74d9ea29510308ad23ff6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826833"
---
# <a name="mpio-on-nano-server"></a>MPIO unter Nano Server

>Gilt für: Windows Server 2016

> [!IMPORTANT]
> Ab Windows Server, Version 1709, steht Nano Server nur als [Basis-Betriebssystemimage für Container](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image) zur Verfügung. Sieh dir [Änderungen an Nano Server](nano-in-semi-annual-channel.md) an und erfahre, was dies bedeutet. 

In diesem Thema wird die Verwendung von MPIO in Nano Server-Installationen von Windows Server 2016 eingeführt. Allgemeine Informationen zu MPIO in Windows Server finden Sie unter [Multipfad-E/A (Übersicht)](https://technet.microsoft.com/library/cc725907.aspx).  

## <a name="using-mpio-on-nano-server"></a>Verwenden von MPIO auf Nano Server  
Sie können MPIO auf Nano Server verwenden, jedoch mit diesen Unterschieden:  
  
-   Nur MSDSM wird unterstützt.  
  
-   Die Lastenausgleichsrichtlinie wird dynamisch ausgewählt und kann nicht geändert werden. Die Richtlinie hat folgende Eigenschaften:  
  
    -   Standard -- RoundRobin (aktiv/aktiv)  
  
    -   SAS HDD -- LeastBlocks  
  
    -   ALUA -- RoundRobin mit Teilmenge  
  
-   Pfad-Status (aktiv/passiv) für ALUA-Arrays werden aus dem Zielarray abgerufen.  
  
-   Speichergeräte werden durch den Bustyp beansprucht (z.B. FC, iSCSI oder SAS). Wenn MPIO auf Nano Server installiert ist, werden Datenträger immer noch als Duplikate verfügbar gemacht (einer pro Pfad verfügbar), bis MPIO so konfiguriert ist, dass es einen Anspruch auf bestimmte Datenträger erhebt und diese verwaltet. Das Beispielskript in diesem Thema wird Ansprüche auf Datenträger für MPIO erheben oder diese abgeben.

- Der iSCSI-Start wird nicht unterstützt.
  
Aktivieren Sie MPIO mit dem folgenden PowerShell-Cmdlet:  
  
`Enable-WindowsOptionalFeature -Online -FeatureName MultiPathIO`  
  
Dieses Beispielskript ermöglicht dem Anrufer das Erheben oder Abgeben von Ansprüchen auf Datenträger für MPIO, indem bestimmte Registrierungsschlüssel geändert werden. Obwohl Sie einen Anspruch auf andere Speichergeräte erheben können, indem Sie sie zu diesen Schlüsseln hinzufügen, empfiehlt es sich nicht, Schlüssel direkt zu bearbeiten.  
  
```  
#  
#  Copyright (c) 2015 Microsoft Corporation.  All rights reserved.  
#    
#  THIS CODE AND INFORMATION IS PROVIDED AS IS WITHOUT WARRANTY   
#  OF ANY KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED   
#  TO THE IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A    
#  PARTICULAR PURPOSE  
#  
  
<#  
.Synopsis  
    This powershell script allows you to enable Multipath-IO support using Microsoft's  
    in-box DSM (MSDSM) for storage devices attached by certain bus types.  
  
    After running this script you will have to either:  
    1. Disable and then re-enable the relevant Host Bus Adapters (HBAs); or  
    2. Reboot the system.  
  
.Description  
  
.Parameter BusType  
    Specifies the bus type for which the claim/unclaim should be done.  
  
    If omitted, this parameter defaults to All.  
  
    All - Will claim/unclaim storage devices attached through Fibre Channel, iSCSI, or SAS.  
  
    FC - Will claim/unclaim storage devices attached through Fibre Channel.  
  
    iSCSI - Will claim/unclaim storage devices attached through iSCSI.  
  
    SAS - Will claim/unclaim storage devices attached through SAS.  
  
.Parameter Server  
    Allows you to specify a remote system, either via computer name or IP address.  
  
    If omitted, this parameter defaults to the local system.  
  
.Parameter Unclaim  
    If specified, the script will unclaim storage devices of the bus type specified by the  
    BusType parameter.  
  
    If omitted, the script will default to claiming storage devices instead.  
  
.Example  
MultipathIoClaim.ps1  
  
Claims all storage devices attached through Fibre Channel, iSCSI, or SAS.    
  
.Example  
MultipathIoClaim.ps1 FC  
  
Claims all storage devices attached through Fibre Channel.  
  
.Example  
MultipathIoClaim.ps1 SAS -Unclaim  
  
Unclaims all storage devices attached through SAS.  
  
.Example  
MultipathIoClaim.ps1 iSCSI 12.34.56.78  
  
Claims all storage devices attached through iSCSI on the remote system with IP address 12.34.56.78.    
  
#>  
[CmdletBinding()]  
param  
(    
    [ValidateSet('all','fc','iscsi','sas')]  
    [string]$BusType='all',  
  
    [string]$Server=127.0.0.1,  
  
    [switch]$Unclaim   
)  
  
#  
# Constants  
#  
$type = [Microsoft.Win32.RegistryHive]::LocalMachine  
[string]$mpioKeyName = SYSTEM\CurrentControlSet\Control\MPDEV  
[string]$mpioValueName = MpioSupportedDeviceList  
[string]$msdsmKeyName = SYSTEM\CurrentControlSet\Services\msdsm\Parameters  
[string]$msdsmValueName = DsmSupportedDeviceList  
  
[string]$fcHwid = MSFT2015FCBusType_0x6     
[string]$sasHwid = MSFT2011SASBusType_0xA    
[string]$iscsiHwid = MSFT2005iSCSIBusType_0x9  
  
#  
# Functions  
#  
  
function AddHardwareId  
{  
    param  
    (  
        [Parameter(Mandatory=$True)]  
        [string]$Hwid,  
  
        [string]$Srv=127.0.0.1,  
  
        [string]$KeyName=SYSTEM\CurrentControlSet\Control\MultipathIoClaimTest,  
  
        [string]$ValueName=DeviceList  
    )  
  
    $regKey = [Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey($type, $Srv)  
    $key = $regKey.OpenSubKey($KeyName, 'true')  
    $val = $key.GetValue($ValueName)  
    $val += $Hwid  
    $key.SetValue($ValueName, [string[]]$val, 'MultiString')  
}  
  
function RemoveHardwareId  
{  
    param  
    (  
        [Parameter(Mandatory=$True)]  
        [string]$Hwid,  
  
        [string]$Srv=127.0.0.1,  
  
        [string]$KeyName=SYSTEM\CurrentControlSet\Control\MultipathIoClaimTest,  
  
        [string]$ValueName=DeviceList  
    )  
  
    [string[]]$newValues = @()  
    $regKey = [Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey($type, $Srv)  
    $key = $regKey.OpenSubKey($KeyName, 'true')  
    $values = $key.GetValue($ValueName)  
    foreach($val in $values)  
    {  
        # Only copy values that don't match the given hardware ID.  
        if ($val -ne $Hwid)  
        {  
            $newValues += $val  
            Write-Debug $($val) will remain in the key.  
        }  
        else  
        {  
            Write-Debug $($val) will be removed from the key.  
        }  
    }  
    $key.SetValue($ValueName, [string[]]$newValues, 'MultiString')  
}  
  
function HardwareIdClaimed  
{  
    param  
    (  
        [Parameter(Mandatory=$True)]  
        [string]$Hwid,  
  
        [string]$Srv=127.0.0.1,  
  
        [string]$KeyName=SYSTEM\CurrentControlSet\Control\MultipathIoClaimTest,  
  
        [string]$ValueName=DeviceList  
    )  
  
    $regKey = [Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey($type, $Srv)  
    $key = $regKey.OpenSubKey($KeyName)  
    $values = $key.GetValue($ValueName)  
    foreach($val in $values)  
    {  
        if ($val -eq $Hwid)  
        {  
            return 'true'  
        }  
    }  
  
    return 'false'  
}  
  
function GetBusTypeName  
{  
    param  
    (  
        [Parameter(Mandatory=$True)]  
        [string]$Hwid  
    )  
  
    if ($Hwid -eq $fcHwid)  
    {  
        return Fibre Channel  
    }  
    elseif ($Hwid -eq $sasHwid)  
    {  
        return SAS  
    }  
    elseif ($Hwid -eq $iscsiHwid)  
    {  
        return iSCSI  
    }  
  
    return Unknown  
}  
  
#  
# Execution starts here.  
#  
  
#  
# Create the list of hardware IDs to claim or unclaim.  
#  
[string[]]$hwids = @()  
  
if ($BusType -eq 'fc')  
{  
    $hwids += $fcHwid  
}  
elseif ($BusType -eq 'iscsi')  
{  
    $hwids += $iscsiHwid  
}  
elseif ($BusType -eq 'sas')  
{  
    $hwids += $sasHwid  
}  
elseif ($BusType -eq 'all')  
{  
    $hwids += $fcHwid  
    $hwids += $sasHwid  
    $hwids += $iscsiHwid  
}  
else  
{  
    Write-Host Please provide a bus type (FC, iSCSI, SAS, or All).  
}  
  
$changed = 'false'  
  
#  
# Attempt to claim or unclaim each of the hardware IDs.  
#  
foreach($hwid in $hwids)  
{      
    $busTypeName = GetBusTypeName $hwid  
  
    #  
    # The device is only considered claimed if it's in both the MPIO and MSDSM lists.  
    #  
    $mpioClaimed = HardwareIdClaimed $hwid $Server $mpioKeyName $mpioValueName  
    $msdsmClaimed = HardwareIdClaimed $hwid $Server $msdsmKeyName $msdsmValueName  
    if ($mpioClaimed -eq 'true' -and $msdsmClaimed -eq 'true')  
    {  
        $claimed = 'true'  
    }  
    else  
    {  
        $claimed = 'false'  
    }  
  
    if ($mpioClaimed -eq 'true')  
    {  
        Write-Debug $($hwid) is in the MPIO list.  
    }  
    else  
    {  
        Write-Debug $($hwid) is NOT in the MPIO list.  
    }  
  
    if ($msdsmClaimed -eq 'true')  
    {  
        Write-Debug $($hwid) is in the MSDSM list.  
    }  
    else  
    {  
        Write-Debug $($hwid) is NOT in the MSDSM list.  
    }  
  
    if ($Unclaim)  
    {  
        #  
        # Unclaim this hardware ID.  
        #   
        if ($claimed -eq 'true')  
        {              
            RemoveHardwareId $hwid $Server $mpioKeyName $mpioValueName  
            RemoveHardwareId $hwid $Server $msdsmKeyName $msdsmValueName  
            $changed = 'true'  
            Write-Host $($busTypeName) devices will not be claimed.  
        }  
        else  
        {  
            Write-Host $($busTypeName) devices are not currently claimed.  
        }  
  
    }  
    else  
    {  
        #  
        # Claim this hardware ID.  
        #       
        if ($claimed -eq 'true')  
        {              
            Write-Host $($busTypeName) devices are already claimed.  
        }  
        else  
        {  
            AddHardwareId $hwid $Server $mpioKeyName $mpioValueName  
            AddHardwareId $hwid $Server $msdsmKeyName $msdsmValueName  
            $changed = 'true'  
            Write-Host $($busTypeName) devices will be claimed.  
        }  
    }  
}  
  
#  
# Finally, if we changed any of the registry keys remind the user to restart.  
#  
if ($changed -eq 'true')  
{  
    Write-Host The system must be restarted for the changes to take effect.  
}  
```  
  


