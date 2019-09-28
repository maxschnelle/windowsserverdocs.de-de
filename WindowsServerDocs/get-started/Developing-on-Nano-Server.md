---
title: Entwickeln für Nano Server
description: PowerShell-Remoting und CIM-Sitzungen
ms.prod: windows-server
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 57079470-a1c1-4fdc-af15-1950d3381860
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 6cf21d9db4221fd6bd76cfd5c362bb9f168d1ce9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360321"
---
# <a name="developing-for-nano-server"></a>Entwickeln für Nano Server

>Gilt für: Windows Server 2016

> [!IMPORTANT]
> Ab Windows Server, Version 1709, steht Nano Server nur als [Basis-Betriebssystemimage für Container](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image) zur Verfügung. Sieh dir die [Änderungen an Nano Server](nano-in-semi-annual-channel.md) an, und erfahre, was dies bedeutet. 

In diesen Themen werden wichtige Unterschiede in PowerShell unter Nano Server erläutert und Unterstützung für die Entwicklung eigener PowerShell-Cmdlets für die Verwendung unter Nano Server geboten.

- [PowerShell unter Nano Server](PowerShell-on-Nano-Server.md)
- [Entwickeln von PowerShell-Cmdlets für Nano Server](Developing-PowerShell-Cmdlets-for-Nano-Server.md)

## <a name="using-windows-powershell-remoting"></a>Verwenden von Windows PowerShell-Remoting  
Um Nano Server mit Windows PowerShell-Remoting zu verwalten, müssen Sie zuerst die IP-Adresse des Nano Servers der Liste vertrauenswürdiger Hosts hinzufügen, die Ihr Verwaltungscomputer besitzt, dann das Konto, das Sie verwenden, zu den Nano Server-Administratoren hinzufügen und schließlich CredSSP aktivieren, wenn Sie dieses Feature verwenden möchten.  

> [!NOTE]
> Wenn sich die Zielinstanz von Nano Server und dein Verwaltungscomputer in derselben AD DS-Gesamtstruktur (oder in Gesamtstrukturen mit einer Vertrauensstellung) befinden, solltest du Nano Server nicht zur Liste der vertrauenswürdigen Hosts hinzufügen. Du kannst eine Verbindung mit Nano Server herstellen, indem du dessen vollständig qualifizierten Domänennamen verwendest, z. B.: PS C:\> Enter-PSSession -ComputerName nanoserver.contoso.com -Credential (Get-Credential).
  
  
Um den Nano Server zu der Liste der vertrauenswürdigen Hosts hinzuzufügen, führen Sie diesen Befehl über eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten aus:  
  
`Set-Item WSMan:\localhost\Client\TrustedHosts "<IP address of Nano Server>"`  
  
Um die Windows PowerShell-Remotesitzung zu starten, initiieren Sie eine lokale Windows PowerShell-Sitzung mit erhöhten Rechten, und führen Sie die folgenden Befehle aus:  
  
  
```  
$ip = "\<IP address of Nano Server>"  
$user = "$ip\Administrator"  
Enter-PSSession -ComputerName $ip -Credential $user  
```  
  
  
Sie können nun wie gewohnt Windows PowerShell-Befehle auf dem Nano Server ausführen.  
  
> [!NOTE]  
> In diesem Release von Nano Server sind nicht alle Windows PowerShell-Befehle verfügbar. Führen Sie `Get-Command -CommandType Cmdlet` aus, um die verfügbaren Befehle anzuzeigen.  
  
Beenden Sie die Remotesitzung mit dem Befehl `Exit-PSSession`.  
  
## <a name="using-windows-powershell-cim-sessions-over-winrm"></a>Verwenden von Windows PowerShell-CIM-Sitzungen über WinRM  
Sie können CIM-Sitzungen und -Instanzen in Windows PowerShell verwenden, um WMI-Befehle über die Windows-Remoteverwaltung (Windows Remote Management, WinRM) auszuführen.  
  
Starten Sie die CIM-Sitzung, indem Sie an einer Windows PowerShell-Eingabeaufforderung diese Befehle ausführen:  
  
  
```  
$ip = "<IP address of the Nano Server\>"  
$ip\Administrator  
$cim = New-CimSession -Credential $user -ComputerName $ip  
```  
  
  
Sobald die Sitzung hergestellt wurde, können Sie verschiedene WMI-Befehle ausführen, wie z.B.:  
  
  
```  
Get-CimInstance -CimSession $cim -ClassName Win32_ComputerSystem | Format-List *  
Get-CimInstance -CimSession $Cim -Query "SELECT * from Win32_Process WHERE name LIKE 'p%'"  
```  
  
  