---
title: Entwickeln von PowerShell-Cmdlets für Nano Server
description: 'Portieren von CIM, .NET-Cmdlets, C++ '
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b4267f0-1c91-4a40-9262-5daf4659f686
author: jaimeo
ms.author: jaimeo
ms.date: 09/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3376d03a2e9f02b20aba608de0228efd7dfddea
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443619"
---
# <a name="developing-powershell-cmdlets-for-nano-server"></a>Entwickeln von PowerShell-Cmdlets für Nano Server

>Gilt für: Windows Server 2016

> [!IMPORTANT]
> Mit dem Beginn von Windows Server, Version 1709 steht Nano Server nur als [Basisimage des Betriebssystems für den Container](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image) zur Verfügung. Sehen Sie sich [Änderungen an Nano Server](nano-in-semi-annual-channel.md) an und erfahren Sie, was dies bedeutet. 
  
## <a name="overview"></a>Übersicht  
PowerShell Core ist standardmäßig in allen Nano Server-Installationen enthalten. PowerShell Core ist eine reduzierte Edition von PowerShell, die auf .Net Core erstellt wird und auf reduzierten Editionen von Windows, wie z.B. Nano Server und Windows IoT Core, ausgeführt wird. PowerShell Core arbeitet genauso wie andere PowerShell-Editionen, wie z.B. Windows PowerShell unter Windows Server 2016. Jedoch bedeutet die reduzierte Version von Nano Server, dass nicht alle PowerShell-Funktionen von Windows Server 2016 in PowerShell Core in Nano Server verfügbar sind.  
  
Wenn Sie über vorhandene PowerShell-Cmdlets verfügen, die Sie auf Nano Server ausführen möchten, oder wenn Sie zu diesem Zweck neue entwickeln, finden Sie in diesem Thema Tipps und Vorschläge, um dies zu vereinfachen.  

## <a name="powershell-editions"></a>PowerShell-Editionen  
  
  
Ab Version 5.1 ist PowerShell in verschiedenen Editionen verfügbar, die unterschiedliche Funktionen mitbringen und zu unterschiedlichen Plattformen kompatibel sind.  
  
- **Desktop-Edition:** Basiert auf .NET Framework und bietet Kompatibilität mit Skripts und Modulen für Versionen von PowerShell, die unter Vollversionen von Windows wie Server Core und Windows-Desktop ausgeführt wird.  
- **Core-Edition:** Basiert auf .NET Core und bietet Kompatibilität mit Skripts und Modulen für Versionen von PowerShell, die unter funktionsreduzierten Versionen von Windows wie Nano Server und Windows IoT ausgeführt wird.  
  
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
Get-Module -ListAvailable | ? CompatiblePSEditions -Contains "Desktop"  
  
    Directory: C:\Program Files\WindowsPowerShell\Modules  
  
  
ModuleType Version    Name                                ExportedCommands  
---------- -------    ----                                ----------------  
Manifest   1.0        ModuleWithPSEditions  
  
Get-Module -ListAvailable | ? CompatiblePSEditions -Contains "Core" | % CompatiblePSEditions  
Desktop  
Core  
  
```  
Skriptautoren können verhindern, dass ein Skript ausgeführt wird, es sei denn, es wird auf einer kompatiblen Edition von PowerShell mithilfe des PSEdition-Parameters auf einer #requires-Anweisung ausgeführt.  
```powershell  
Set-Content C:\script.ps1 -Value "#requires -PSEdition Core  
Get-Process -Name PowerShell"  
Get-Content C:\script.ps1  
#requires -PSEdition Core  
Get-Process -Name PowerShell  
  
C:\script.ps1  
C:\script.ps1 : The script 'script.ps1' cannot be run because it contained a "#requires" statement for PowerShell editions 'Core'. The edition of PowerShell that is required by the script does not match the currently running PowerShell Desktop edition.  
At line:1 char:1  
+ C:\script.ps1  
+ ~~~~~~~~~~~~~  
    + CategoryInfo          : NotSpecified: (script.ps1:String) [], RuntimeException  
    + FullyQualifiedErrorId : ScriptRequiresUnmatchedPSEdition  
```  
  
  
## <a name="installing-nano-server"></a>Installieren von Nano Server  
Einen Schnellstart sowie detaillierte Schritte zur Installation von Nano Server auf virtuellen oder physischen Computern finden Sie im übergeordneten Thema dieses Themas: [Installieren von Nano Server](Getting-Started-with-Nano-Server.md).  
  
> [!NOTE]  
> Für Entwicklungen auf Nano Server könnte es hilfreich sein, Nano Server zu installieren, indem Sie den Parameter „-Development“ von New-NanoServerImage verwenden. Dadurch wird es möglich, unsignierte Treiber zu installieren, Debugger-Binärdateien zu kopieren, einen Port für das Debuggen zu öffnen, die Testsignierung zu aktivieren und die Installation von AppX-Paketen ohne Entwicklerlizenz zu aktivieren. Zum Beispiel:  
>  
>`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -Development`  
  
## <a name="determining-the-type-of-cmdlet-implementation"></a>Bestimmen des Cmdlet-Implementierungstyps  
PowerShell unterstützt eine Reihe von Implementierungstypen für Cmdlets. Der Typ, den Sie verwendet haben, bestimmt den Prozess und die Tools, die zum Erstellen oder Portieren dieses Typs verwendet werden, damit dieser auf Nano Server funktioniert. Unterstützte Implementierungstypen sind folgende:  
* CIM: besteht aus CDXML-Dateien, die über CIM-Anbieter (WMIv2-Anbieter) geschichtet werden   
* .NET: besteht aus .NET-Assemblys, die verwaltete Cmdlet-Schnittstellen implementieren, die in der Regel in C# geschrieben sind   
* PowerShell-Skript: besteht aus Skriptmodulen (.psm1) oder Skripts (.ps1), die in der PowerShell-Sprache geschrieben sind   
  
Wenn Sie nicht sicher sind, welche Implementierung Sie für vorhandene Cmdlets verwendet haben, die Sie portieren möchten, installieren Sie Ihr Produkt oder Feature und suchen Sie anschließend nach dem PowerShell-Modulordner an einem der folgenden Speicherorten:   
  
* %windir%\system32\WindowsPowerShell\v1.0\Modules   
* %ProgramFiles%\WindowsPowerShell\Modules   
* %UserProfile%\Documents\WindowsPowerShell\Modules   
* \<Speicherort Ihrer Produktinstallation >   
    
  Überprüfen Sie diese Speicherorte auf die folgenden Details:  
  * CIM-Cmdlets haben .cdxml-Dateierweiterungen.  
  * .NET-Cmdlets haben .dll-Dateierweiterungen bzw. haben Assemblys, die in dem GAC installiert werden, der in der PSD1-Datei unter den Feldern „RootModule“, „ModuleToProcess“ oder „NestedModules“ aufgelistet ist.  
* PowerShell-Skript-Cmdlets haben .psm1- oder .ps1-Datei-Erweiterungen.   
  
## <a name="porting-cim-cmdlets"></a>Portieren von CIM-Cmdlets  
Im Allgemeinen sollten diese Cmdlets in Nano Server funktionieren, ohne dass eine Konvertierung erforderlich ist. Sie müssen jedoch den zugrunde liegenden WMIv2-Anbieter so portieren, dass er auf Nano Server ausgeführt wird, falls dies noch nicht geschehen ist.  
  
### <a name="building-c-for-nano-server"></a>Erstellen von C++-Code für Nano Server  
Damit C++-DLLs unter Nano Server funktionieren, kompilieren Sie diese für Nano Server, anstatt für eine spezifische Edition.  
  
Erforderliche Komponenten und eine exemplarische Vorgehensweise zum Entwickeln von C++ unter Nano Server finden Sie im Blogbeitrag [Developing Native Apps on Nano Server (Entwickeln von nativen Apps unter Nano Server)](http://blogs.technet.com/b/nanoserver/archive/2016/04/27/developing-native-apps-on-nano-server.aspx).  
  
  
## <a name="porting-net-cmdlets"></a>Portieren von .NET-Cmdlets  
Die Mehrheit des C#-Codes wird unter Nano Server unterstützt. Sie können [ApiPort](https://github.com/Microsoft/dotnet-apiport) verwenden, um auf inkompatible APIs zu prüfen.  
  
### <a name="powershell-core-sdk"></a>PowerShell Core SDK  
Das Modul „Microsoft.PowerShell.NanoServer.SDK“ ist im [PowerShell-Katalog](https://www.powershellgallery.com/packages/Microsoft.PowerShell.NanoServer.SDK/) verfügbar, um das Entwickeln von .NET-Cmdlets mithilfe von Visual Studio 2015 Update 2 zu vereinfachen, das auf die in Nano Server verfügbaren Versionen von CoreCLR und PowerShell Core ausgerichtet ist. Sie können das Modul mithilfe von PowerShellGet mit dem folgenden Befehl installieren:  
  
`Find-Module Microsoft.PowerShell.NanoServer.SDK -Repository PSGallery | Install-Module -Scope <scope>`  
  
Das PowerShell Core SDK-Modul stellt Cmdlets verfügbar, um die richtigen CoreCLR- und PowerShell Core-Referenzassemblys einzurichten, ein auf diese Referenzassemblys ausgerichtetes C#-Projekt in Visual Studio 2015 zu erstellen und den Remotedebugger auf einem Nano Server-Computer einzurichten, damit Entwickler ihre auf Nano Server ausgeführten .NET-Cmdlets remote in Visual Studio 2015 debuggen können.  
  
Das PowerShell Core SDK-Modul erfordert Visual Studio 2015 Update 2. Wenn Sie Visual Studio 2015 nicht installiert haben, können Sie [Visual Studio Community 2015](https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx) installieren.  
  
Das SDK-Modul hängt auch von den folgenden Funktionen ab, die in Visual Studio 2015 installiert werden müssen:  
  
- Windows- und Webentwicklung -> Entwicklungstools für universelle Windows-Apps -> Tools (1.3.1) und Windows 10 SDK  
  
Überprüfen Sie Ihre Installation von Visual Studio, bevor Sie das SDK-Modul verwenden, um sicherzustellen, dass diese Voraussetzungen erfüllt sind. Stellen Sie sicher, dass Sie die oben genannte Funktion während der Installation von Visual Studio auswählen, oder ändern Sie Ihre vorhandene Visual Studio 2015-Installation, um sie zu installieren.  
  
Das PowerShell Core SDK-Modul enthält die folgenden Cmdlets:  
- New-NanoCSharpProject: Erstellt eine neue Visual Studio C# Projekt auf CoreCLR und PowerShell Core, die in der Windows Server 2016-Release von Nano Server enthalten.  
- Show-SdkSetupReadMe: Öffnet den SDK-Stammordner im Datei-Explorer, und öffnet die Datei "Readme.txt" für das manuelle Setup.  
- Install-RemoteDebugger: Installiert und konfiguriert den Visual Studio-Remotedebugger auf einem Nano Server-Computer.  
- Start-RemoteDebugger: Startet den Remotedebugger auf einem Remotecomputer mit dem Nano Server ausgeführt wird.  
- Stop-RemoteDebugger: Hält den Remotedebugger auf einem Remotecomputer mit dem Nano Server ausgeführt wird.  
  
Ausführliche Informationen zur Verwendung dieser Cmdlets erhalten Sie, indem Sie nach der Installation und der Ausführung des Moduls wie folgt für jedes Cmdlet Get-Help ausführen:  
  
`Get-Command -Module Microsoft.PowerShell.NanoServer.SDK | Get-Help -Full`   
  
  
### <a name="searching-for-compatible-apis"></a>Suchen nach kompatiblen APIs  
  
Sie können im API-Katalog nach .NET Core suchen oder CoreCLR-Referenzassemblys disassemblieren. Weitere Informationen zur Plattformportabilität von .NET-APIs finden Sie unter [Platform Portability (Plattformportabilität)](https://github.com/Microsoft/dotnet-apiport/blob/master/docs/HowTo/PlatformPortability.md).  
  
### <a name="pinvoke"></a>PInvoke  
In CoreCLR, das von Nano Server verwendet wird, wurden einige grundlegende DLLs wie z.B. „kernel32.dll“ und „advapi32.dll“ in zahlreiche API-Sätze aufgeteilt. Sie müssen daher sicherstellen, dass Ihre PInvokes auf die richtige API verweisen. Jede Inkompatibilität äußert sich in einem Laufzeitfehler.  
  
Eine Liste der unter Nano Server unterstützten nativen APIs finden Sie unter [Nano Server APIs (Nano Server-APIs)](https://msdn.microsoft.com/library/mt588480(v=vs.85).aspx).  
  
### <a name="building-c-for-nano-server"></a>Erstellen von C# für Nano Server  
  
Sobald ein C#-Projekt in Visual Studio 2015 mithilfe von `New-NanoCSharpProject` erstellt wird, können Sie es in Visual Studio einfach erstellen, indem Sie auf das Menü **Erstellen** klicken und **Projekt erstellen** oder **Projektmappe erstellen** auswählen. Die generierten Assemblys werden auf die richtigen Versionen von CoreCLR und PowerShell Core ausgerichtet, die in Nano Server enthalten sind, und Sie können die Assemblys einfach auf einen Computer kopieren, auf dem Nano Server ausgeführt wird, und diese verwenden.  
  
### <a name="building-managed-c-cppcli-for-nano-server"></a>Erstellen von verwaltetem C++-Code (CPP/CLI) für Nano Server  
Der verwaltete C++-Code wird für CoreCLR nicht unterstützt. Beim Portieren zu CoreCLR schreiben Sie verwalteten C++-Code in C# um und führen alle nativen Aufrufe über PInvoke durch.  
  
## <a name="porting-powershell-script-cmdlets"></a>Portieren von PowerShell-Skript-Cmdlets  
  
PowerShell Core verfügt über die vollständige PowerShell-Sprachparität mit anderen Editionen von PowerShell, einschließlich der unter Windows Server 2016 und Windows 10 ausgeführten Edition. Beim Portieren von PowerShell-Skript-Cmdlets zu Nano Server sollten Sie jedoch die folgenden Faktoren bedenken:  
* Bestehen Abhängigkeiten von anderen Cmdlets? Sind diese Cmdlets unter Nano Server verfügbar, wenn dies der Fall ist? Informationen dazu, welche nicht verfügbar sind, finden Sie unter [PowerShell on Nano Server (PowerShell unter Nano Server)](PowerShell-on-Nano-Server.md).  
* Funktionieren die Assemblys weiterhin, wenn Abhängigkeiten von Assemblys bestehen, die zur Laufzeit geladen werden?   
* Wie können Sie das Skript remote Debuggen?   
* Wie können Sie von WMI .NET zu MI .NET migrieren?  
  
### <a name="dependency-on-built-in-cmdlets"></a>Abhängigkeit von integrierten Cmdlets  
Nicht alle Cmdlets in Windows Server 2016 sind unter Nano Server verfügbar (siehe [PowerShell on Nano Server (PowerShell unter Nano Server)](PowerShell-on-Nano-Server.md)). Die beste Methode besteht darin, einen virtuellen Nano Server-Computer einzurichten und zu ermitteln, ob die Cmdlets, die Sie benötigen, verfügbar sind. Führen Sie hierzu `Enter-PSSession` aus, um eine Verbindung mit dem Ziel-Nano Server herzustellen, und führen Sie anschließend `Get-Command -CommandType Cmdlet, Function` aus, um die Liste mit verfügbaren Cmdlets abzurufen.  
  
### <a name="consider-using-powershell-classes"></a>Erwägen der Verwendung von PowerShell-Klassen  
Add-Type wird zum Kompilieren von C#-Inlinecode unter Nano Server unterstützt. Wenn Sie neuen Code schreiben oder vorhandenen Code portieren, sollten Sie ebenfalls die Verwendung von PowerShell-Klassen zum Definieren von benutzerdefinierten Typen in Erwägung ziehen. Sie können PowerShell-Klassen sowohl für Eigenschaftenbehälterszenarios als auch für Enumerationen verwenden. Wenn Sie ein PInvoke durchführen müssen, tun Sie dies über C# mithilfe von Add-Type oder in einer vorkompilierten Assembly.  
Im folgenden Beispiel wird die Verwendung von Add-Type dargestellt:  
  
```  
Add-Type -ReferencedAssemblies ([Microsoft.Management.Infrastructure.Ciminstance].Assembly.Location) -TypeDefinition @'  
public class TestNetConnectionResult  
{  
   // The compute name  
   public string ComputerName = null;  
   // The Remote IP address used for connectivity  
   public System.Net.IPAddress RemoteAddress = null;  
}  
'@  
# Create object and set properties  
$result = New-Object TestNetConnectionResult  
$result.ComputerName = "Foo"  
$result.RemoteAddress = 1.1.1.1  
  
```  
 Dieses Beispiel zeigt die Verwendung von PowerShell-Klassen unter Nano Server:  
   
```  
class TestNetConnectionResult    
{    
   # The compute name  
  [string] $ComputerName    
  
  #The Remote IP address used for connectivity    
  [System.Net.IPAddress] $RemoteAddress  
}  
# Create object and set properties  
$result = [TestNetConnectionResult]::new()  
$result.ComputerName = "Foo"  
$result.RemoteAddress = 1.1.1.1  
  
```  
  
### <a name="remotely-debugging-scripts"></a>Remotedebuggen von Skripts  
  
Stellen Sie eine Verbindung mit dem Remotecomputer her, indem Sie `Enter-PSsession` aus PowerShell ISE verwenden, um ein Skript remote zu debuggen. Sie können `psedit <file_path>` einmal innerhalb der Sitzung ausführen, und eine Kopie der Datei wird in Ihrer lokalen PowerShell ISE geöffnet. Anschließend können Sie das Skript debuggen, als ob es lokal ausgeführt würde, indem Sie Haltepunkte festlegen. Darüber hinaus werden alle Änderungen, die Sie an dieser Datei vornehmen, in der Remoteversion gespeichert.   
  
### <a name="migrating-from-wmi-net-to-mi-net"></a>Migrieren von WMI .NET zu MI .NET  
  
[WMI .NET](https://msdn.microsoft.com/library/mt481551(v=vs.110).aspx) wird nicht unterstützt, sodass alle Cmdlets, die mit der alten API für die unterstützten WMI-API migrieren müssen: [MI. .NET](https://msdn.microsoft.com/library/dn387184(v=vs.85).aspx). Sie können direkt über C# oder die Cmdlets im CimCmdlets-Modul auf MI . NET zugreifen.   
  
### <a name="cimcmdlets-module"></a>CimCmdlets-Module  
  
Die WMIv1-Cmdlets (z.B. Get-WmiObject) werden unter Nano Server nicht unterstützt. Die CIM-Cmdlets (z.B. Get-CimInstance) im CimCmdlets-Modul werden jedoch unterstützt. Die CIM-Cmdlets sind ziemlich eng an die WMIv1-Cmdlets angelehnt. Beispielsweise stimmt Get-WmiObject mit Get-CimInstance überein, das sehr ähnliche Parameter verwendet. Die Methodenaufrufsyntax weicht leicht ab, ist jedoch über Invoke-CimMethod gut dokumentiert. Seien Sie vorsichtig bei der Parametereingabe. MI .NET hat strengere Anforderungen hinsichtlich Methodenparametertypen.  
  
### <a name="c-api"></a>C#-API  
  
WMI .NET umschließt die WMIv1-Schnittstelle, während MI .NET die WMIv2-Schnittstelle (CIM-Schnittstelle) umschließt. Die zur Verfügung gestellten Klassen können abweichen, die zugrundeliegenden Vorgänge sind jedoch sehr ähnlich. Sie listen Instanzen von Objekten auf oder rufen diese ab und rufen Vorgänge für diese auf, um Aufgaben zu erfüllen.   
  
  


