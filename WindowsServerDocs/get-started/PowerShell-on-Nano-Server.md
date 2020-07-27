---
title: PowerShell unter Nano Server
description: Unterschiede in der reduzierten Auswahl von PowerShell-Features unter Nano Server
ms.prod: windows-server
manager: DonGill
ms.technology: server-nano
ms.topic: article
ms.assetid: 9b25b939-1e2c-4bed-a8d3-2a8e8e46b53d
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 6535cb9cc6ad77d4ea5e5e33c2d28e03fd447968
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86963577"
---
# <a name="powershell-on-nano-server"></a>PowerShell unter Nano Server

> Gilt für: Windows Server 2016

> [!IMPORTANT]
> Ab Windows Server, Version 1709, steht Nano Server nur als [Basis-Betriebssystemimage für Container](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image) zur Verfügung. Sieh dir [Änderungen an Nano Server](nano-in-semi-annual-channel.md) an und erfahre, was dies bedeutet.

## <a name="powershell-editions"></a>PowerShell-Editionen

Ab Version 5.1 ist PowerShell in verschiedenen Editionen verfügbar, die unterschiedliche Funktionen mitbringen und zu unterschiedlichen Plattformen kompatibel sind.

- **Desktop-Edition:** Diese Edition basiert auf .NET Framework und bietet Kompatibilität mit PowerShell-Versionen, die auf Skripts und Module abzielen und unter vollwertigen Editionen von Windows ausgeführt werden, z. B. Server Core und Windows Desktop.
- **Core Edition:** Diese Edition basiert auf .NET Core und bietet Kompatibilität mit Skripts und Modulen, die auf PowerShell-Versionen abzielen, die auf reduzierten Editionen von Windows ausgeführt werden, z. B. Nano Server und Windows IoT.

Die ausgeführte Version von PowerShell wird in der PSEdition-Eigenschaft von $PSVersionTable angezeigt.
```powershell
$PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.1.14300.1000
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
CLRVersion                     4.0.30319.42000
BuildVersion                   10.0.14300.1000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

Modulautoren können deklarieren, dass ihre Module mit einer oder mehreren PowerShell-Editionen kompatibel sein sollen, indem Sie den CompatiblePSEditions-Modulmanifestschlüssel verwenden. Dieser Schlüssel wird nur auf PowerShell 5.1 oder höher unterstützt.
```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$moduleInfo = Test-ModuleManifest -Path \TestModuleWithEdition.psd1
$moduleInfo.CompatiblePSEditions
Desktop
Core

$moduleInfo | Get-Member CompatiblePSEditions

   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}

```
Beim Abrufen einer Liste der verfügbaren Module können Sie die Liste nach PowerShell-Edition filtern.
```powershell
Get-Module -ListAvailable | ? CompatiblePSEditions -Contains Desktop

    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions

Get-Module -ListAvailable | ? CompatiblePSEditions -Contains Core | % CompatiblePSEditions
Desktop
Core

```
Skriptautoren können verhindern, dass ein Skript ausgeführt wird, es sei denn, es wird auf einer kompatiblen Edition von PowerShell mithilfe des PSEdition-Parameters auf einer #requires-Anweisung ausgeführt.
```powershell
Set-Content C:\script.ps1 -Value #requires -PSEdition Core
Get-Process -Name PowerShell
Get-Content C:\script.ps1
#requires -PSEdition Core
Get-Process -Name PowerShell

C:\script.ps1
C:\script.ps1 : The script 'script.ps1' cannot be run because it contained a #requires statement for PowerShell editions 'Core'. The edition of PowerShell that is required by the script does not match the currently running PowerShell Desktop edition.
At line:1 char:1
+ C:\script.ps1
+ ~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (script.ps1:String) [], RuntimeException
    + FullyQualifiedErrorId : ScriptRequiresUnmatchedPSEdition
```

## <a name="differences-in-powershell-on-nano-server"></a>Unterschiede in PowerShell unter Nano Server
PowerShell Core ist standardmäßig in allen Nano Server-Installationen enthalten. PowerShell Core ist eine reduzierte Edition von PowerShell, die auf .Net Core erstellt wird und auf reduzierten Editionen von Windows, wie z.B. Nano Server und Windows IoT Core, ausgeführt wird. PowerShell Core arbeitet genauso wie andere PowerShell-Editionen, wie z.B. Windows PowerShell unter Windows Server 2016. Jedoch bedeutet die reduzierte Version von Nano Server, dass nicht alle PowerShell-Funktionen von Windows Server 2016 in PowerShell Core in Nano Server verfügbar sind.


**Windows PowerShell-Funktionen, die nicht in Nano Server enthalten sind**
* ADSI, ADO und WMI-Typadapter
* Enable-PSRemoting, Disable-PSRemoting (PowerShell-Remoting ist standardmäßig aktiviert; siehe Abschnitt „Verwenden von Windows PowerShell-Remoting“ unter [Installieren von Nano Server](Getting-Started-with-Nano-Server.md)).
* Geplante Aufträge und PSScheduledJob-Modul
* Computer-Cmdlets für den Beitritt zu einer Domäne { Add | Remove } (andere Methoden, Nano Server mit einer Domäne zu verknüpfen, finden Sie im Abschnitt „Verknüpfen von Nano Server mit einer Domäne“ unter [Installieren von Nano Server](Getting-Started-with-Nano-Server.md)).
* Reset-ComputerMachinePassword, Test-ComputerSecureChannel
* Profile (Sie können ein Startskript für eingehende Remoteverbindungen mit `Set-PSSessionConfiguration` hinzufügen)
* „Clipboard“-Cmdlets
* EventLog-Cmdlets { Clear | Get | Limit | New | Remove | Show | Write } (Verwenden Sie stattdessen die Cmdlets New-WinEvent and Get-WinEvent).
* Get-PfxCertificate-Cmdlet
* TraceSource-Cmdlets { Get | Set }
* Counter-Cmdlets { Get | Export | Import }
* Einige webbezogene Cmdlets { New-WebServiceProxy, Send-MailMessage, ConvertTo-Html }
* Protokollierung und Ablaufverfolgung mit dem PSDiagnostics-Modul
* Get-HotFix (zum Abrufen und Verwalten von Updates auf Nano Server; Informationen hierzu finden Sie unter [Manage Nano Server (Verwalten von Nano Server)](Manage-Nano-Server.md)).
* Cmdlets für implizites Remoten { Export-PSSession | Import-PSSession }
* New-PSTransportOption
* PowerShell-Transaktionen und Transaktions-Cmdlets { Complete | Get | Start | Undo | Use }
* Infrastruktur, Module und Cmdlets der PowerShell-Workflow
* Out-Printer
* Update-List
* WMIv1-Cmdlets: Get-WmiObject, Invoke-WmiMethod, Register-WmiEvent, Remove-WmiObject, Set-WmiInstance (Verwende stattdessen das CimCmdlets-Modul.)

## <a name="using-windows-powershell-desired-state-configuration-with-nano-server"></a>Verwenden von Windows PowerShell DSC mit Nano Server

Sie können Nano Server als Zielknoten mit Windows PowerShell Desired State Configuration (DSC) verwalten. Derzeit können Sie Knoten unter Nano Server mit DSC nur im Pushmodus verwenden. Allerdings funktionieren nicht alle DSC-Features mit Nano Server.

Ausführliche Informationen finden Sie unter [Using DSC on Nano Server (Verwenden von DSC unter Nano Server)](/powershell/scripting/dsc/getting-started/nanodsc).
