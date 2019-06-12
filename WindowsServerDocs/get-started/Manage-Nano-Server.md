---
title: Verwalten von Nano Server
description: Updates, Wartungspakete, Netzwerkablaufverfolgung und Leistungsüberwachung
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 599d6438-a506-4d57-a0ea-1eb7ec19f46e
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: cc535934705878c7f2b7fdc4e655ab5c853e4f96
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443528"
---
# <a name="manage-nano-server"></a>Verwalten von Nano Server

>Gilt für: Windows Server 2016

> [!IMPORTANT]
> Mit dem Beginn von Windows Server, Version 1709 steht Nano Server nur als [Basisimage des Betriebssystems für den Container](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image) zur Verfügung. Sehen Sie sich [Änderungen an Nano Server](nano-in-semi-annual-channel.md) an und erfahren Sie, was dies bedeutet.   

Nano Server wird remote verwaltet. Es besteht weder die Möglichkeit, sich lokal anzumelden, noch werden Terminaldienste unterstützt. Allerdings verfügen Sie über eine Vielzahl von Optionen zur Remoteverwaltung von Nano Server, einschließlich Windows PowerShell, der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI), der Windows-Remoteverwaltung und der Notverwaltungsdienste (Emergency Management Services, EMS).  

Um Remoteverwaltungstools verwenden zu können, müssen Sie wahrscheinlich die IP-Adresse des Nano Servers kennen. Sie können die IP-Adresse z.B. auf folgende Weise ermitteln:  
  
-   Verwenden Sie die Nano-Wiederherstellungskonsole (siehe den Abschnitt „Verwenden der Nano-Wiederherstellungskonsole“ in diesem Thema).  
  
-   Verbinden Sie ein serielles Kabel mit dem Computer, und verwenden Sie EMS.  
  
-   Wenn Sie den Computernamen verwenden, den Sie dem Nano Server während der Konfiguration zugewiesen haben, können Sie die IP-Adresse mit Ping abrufen. Beispiel: `ping NanoServer-PC /4`Hyper-V-Hosts oder Hyper-V-Hostcluster in einem separaten Namespace als verwaltete Hyper-V-Hosts hinzuzufügen.  
  
## <a name="using-windows-powershell-remoting"></a>Verwenden von Windows PowerShell-Remoting  
Um Nano Server mit Windows PowerShell-Remoting zu verwalten, müssen Sie zuerst die IP-Adresse des Nano Servers der Liste vertrauenswürdiger Hosts hinzufügen, die Ihr Verwaltungscomputer besitzt, dann das Konto, das Sie verwenden, zu den Nano Server-Administratoren hinzufügen und schließlich CredSSP aktivieren, wenn Sie dieses Feature verwenden möchten.  

> [!NOTE]
> Wenn die Ziel-Nano Server und Ihr Verwaltungscomputer in derselben AD DS-Gesamtstruktur (oder in Gesamtstrukturen mit einer Vertrauensstellung) sind, sollten Sie nicht der Nano Server-hinzufügen, die Liste der vertrauenswürdigen Hosts können Sie mit dem Nano Server verbinden, mit dessen vollständig qualifizierten Domänennamen Zum Beispiel: PS C:\> Geben Sie-PSSession – ComputerName nanoserver.contoso.com-Credential (Get-Credential)
  
  
Um den Nano Server zu der Liste der vertrauenswürdigen Hosts hinzuzufügen, führen Sie diesen Befehl über eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten aus:  
  
`Set-Item WSMan:\localhost\Client\TrustedHosts "<IP address of Nano Server>"`  
  
Um die Windows PowerShell-Remotesitzung zu starten, initiieren Sie eine lokale Windows PowerShell-Sitzung mit erhöhten Rechten, und führen Sie die folgenden Befehle aus:  
  
  
```  
$ip = "<IP address of Nano Server>"  
$user = "$ip\Administrator"  
Enter-PSSession -ComputerName $ip -Credential $user  
```  
  
  
Sie können nun wie gewohnt Windows PowerShell-Befehle auf dem Nano Server ausführen.  
  
> [!NOTE]  
> In diesem Release von Nano Server sind nicht alle Windows PowerShell-Befehle verfügbar. Führen Sie zum Anzeigen der zur Verfügung stehen. `Get-Command -CommandType Cmdlet`  
  
Beenden Sie die Remotesitzung mit dem Befehl `Exit-PSSession`  
  
## <a name="using-windows-powershell-cim-sessions-over-winrm"></a>Verwenden von Windows PowerShell-CIM-Sitzungen über WinRM  
Sie können CIM-Sitzungen und -Instanzen in Windows PowerShell verwenden, um WMI-Befehle über die Windows-Remoteverwaltung (Windows Remote Management, WinRM) auszuführen.  
  
Starten Sie die CIM-Sitzung, indem Sie an einer Windows PowerShell-Eingabeaufforderung diese Befehle ausführen:  
  
  
```  
$ip = "<IP address of the Nano Server\>"  
$user = $ip\Administrator  
$cim = New-CimSession -Credential $user -ComputerName $ip  
```  
  
  
Sobald die Sitzung hergestellt wurde, können Sie verschiedene WMI-Befehle ausführen, wie z.B.:  
  
  
```  
Get-CimInstance -CimSession $cim -ClassName Win32_ComputerSystem | Format-List *  
Get-CimInstance -CimSession $Cim -Query "SELECT * from Win32_Process WHERE name LIKE 'p%'"  
```  
  
  
## <a name="windows-remote-management"></a>Windows-Remoteverwaltung  
Sie können Programme auf dem Nano Server mit der Windows-Remoteverwaltung (WinRM) remote ausführen. Konfigurieren Sie zum Verwenden von WinRM zuerst den Dienst, und richten Sie die Codepage mit den folgenden Befehlen über eine Eingabeaufforderung mit erhöhten Rechten ein:  
  
```
winrm quickconfig
winrm set winrm/config/client @{TrustedHosts="<ip address of Nano Server>"}
chcp 65001
```
  
Sie können die Befehle jetzt auf dem Nano Server remote ausführen. Zum Beispiel:  

```
winrs -r:<IP address of Nano Server> -u:Administrator -p:<Nano Server administrator password> ipconfig
```
  
Weitere Informationen zur Windows-Remoteverwaltung finden Sie unter [Übersicht über die Windows-Remoteverwaltung (Windows Remote Management, WinRM)](https://technet.microsoft.com/library/dn265971.aspx).  
   
   
  
## <a name="running-a-network-trace-on-nano-server"></a>Ausführen einer Netzwerkablaufverfolgung unter Nano-Server  
 Die Netsh-Ablaufverfolgung, Tracelog.exe und Logman.exe sind für Nano Server nicht verfügbar. Um Netzwerkpakete zu erfassen, können Sie diese Windows PowerShell-Cmdlets verwenden:  
   
   
```  
New-NetEventSession [-Name]  
Add-NetEventPacketCaptureProvider -SessionName  
Start-NetEventSession [-Name]  
Stop-NetEventSession [-Name]  
```  
Diese Cmdlets finden Sie unter [Network Event Packet Capture Cmdlets in Windows PowerShell (Windows PowerShell-Cmdlets zum Erfassen von Netzwerkereignispaketen)](https://technet.microsoft.com/library/dn268520(v=wps.630).aspx) detailliert dokumentiert.  

## <a name="installing-servicing-packages"></a>Installieren von Wartungspaketen  
Wenn Sie ein Wartungspaket installieren möchten, verwenden Sie den Parameter „-ServicingPackagePath“ (Sie können ein Array von Pfaden an CAB-Dateien übergeben):  
  
`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -ServicingPackagePath \\path\to\kb123456.cab`  
  
Häufig wird ein Wartungspaket oder Hotfix als KB-Artikel, der eine CAB-Datei enthält, heruntergeladen. Befolgen Sie diese Schritte, um die CAB-Datei zu extrahieren, den Sie anschließend mit dem Parameter „-ServicingPackagePath“ installieren können:  
  
1.  Laden Sie das Wartungspaket aus dem zugehörigen Knowledge Base-Artikel oder dem [Microsoft Update-Katalog](https://catalog.update.microsoft.com/v7/site/home.aspx) herunter. Speichern Sie es z. B. auf einem lokalen Verzeichnis oder einer Netzwerkfreigabe: C:\ServicingPackages  
2.  Erstellen Sie einen Ordner, in dem Sie das extrahierte Wartungspaket speichern.  Beispiel: C:\KB3157663_expanded  
3.  Öffnen Sie eine Windows PowerShell-Konsole, und verwenden Sie den `Expand`-Befehl, um den Pfad zur MSU-Datei des Wartungspakets anzugeben, einschließlich des `-f:*`-Parameters und des Pfads, in den das Wartungspaket extrahiert werden soll.  Zum Beispiel:  `Expand "C:\ServicingPackages\Windows10.0-KB3157663-x64.msu" -f:* "C:\KB3157663_expanded"`  
  
    Die erweiterten Dateien sollten dem folgenden Beispiel ähneln:  
C:>dir C:\KB3157663_expanded   
Volume in drive C is OS  
Volume Serial Number is B05B-CC3D  
   
      Directory of C:\KB3157663_expanded  
   
      04/19/2016  01:17 PM    \<DIR>          .  
      04/19/2016  01:17 PM    \<DIR&gt;          .  
        04/17/2016  12:31 AM               517 Windows10.0-KB3157663-x64-pkgProperties.txt  
04/17/2016  12:30 AM        93,886,347 Windows10.0-KB3157663-x64.cab  
04/17/2016  12:31 AM               454 Windows10.0-KB3157663-x64.xml  
04/17/2016  12:36 AM           185,818 WSUSSCAN.cab  
               4 File(s)     94,073,136 bytes  
               2 Dir(s)  328,559,427,584 bytes free  
4.  Führen Sie `New-NanoServerImage` mit dem "- servicingpackagepath"-Parameter, die auf die CAB-Datei in diesem Verzeichnis, beispielsweise: `New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -ServicingPackagePath C:\KB3157663_expanded\Windows10.0-KB3157663-x64.cab`  

## <a name="managing-updates-in-nano-server"></a>Verwalten von Updates in Nano Server

Derzeit können Sie den Windows Update-Anbieter für die Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) verwenden, um die Liste der anwendbaren Updates zu suchen und anschließend alle oder einen Teil der Updates zu installieren. Wenn Sie Windows Server Update Services (WSUS) verwenden, können Sie Nano Server dazu konfigurieren, den WSUS-Server für Updates aufzurufen.  

In jedem Fall müssen Sie zuerst eine Windows PowerShell-Remotesitzung zu dem Nano Server-Computer aufbauen. Diese Beispiele verwenden *$sess* für die Sitzung. Wenn Sie ein anderes Element verwenden, ersetzen Sie es nach Bedarf.  


### <a name="view-all-available-updates"></a>Anzeigen aller verfügbaren Updates  
---  
Rufen Sie mithilfe dieser Befehle die vollständige Liste der anwendbaren Updates ab:  
```  
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=0";OnlineScan=$true}  
```  
**Hinweis**:  
Wenn keine Updates verfügbar sind, gibt dieser Befehl den folgenden Fehler zurück:  
```  
Invoke-CimMethod : A general error occurred that is not covered by a more specific error code.  

At line:1 char:16  

+ ... anResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUp ...  

+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~  

    + CategoryInfo          : NotSpecified: (MSFT_WUOperatio...-5b842a3dd45d")  

   :CimInstance) [Invoke-CimMethod], CimException  

    + FullyQualifiedErrorId : MI RESULT 1,Microsoft.Management.Infrastructure.  

   CimCmdlets.InvokeCimMethodCommand  
```  

### <a name="install-all-available-updates"></a>Installieren aller verfügbaren Updates  
---  
Sie können **alle** verfügbaren Updates gleichzeitig mit folgenden Befehlen erkennen, herunterladen und installieren:  

```  
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ApplyApplicableUpdates  

Restart-Computer  
```  
**Hinweis**:  
Windows Defender verhindert die Installation von Updates. Um dies zu umgehen, deinstallieren Sie Windows Defender, installieren Sie die Updates, und installieren Sie Windows Defender erneut. Alternativ können Sie Updates auf einen anderen Computer herunterladen, auf den Nano-Server kopieren und diese mit „DISM.exe“ anwenden.  


### <a name="verify-installation-of-updates"></a>Überprüfen der Updateinstallation  
---  
Verwenden Sie diese Befehle, um eine Liste der installierten Updates zu erhalten:  
```  
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=1";OnlineScan=$true}  
```  

**Hinweis**:  
Diese Befehle listen die installierten Updates auf, markieren sie in der Ausgabe jedoch nicht speziell als „installiert“. Wenn Sie möchten, dass dies in der Ausgabe angegeben wird, z.B. für einen Bericht, führen Sie Folgendes aus:  
```  
Get-WindowsPackage--Online  
```  

### <a name="using-wsus"></a>Verwenden von WSUS  
---  
Die oben aufgeführten Befehle fragen den Windows Update und Microsoft Update-Dienst online ab, um Updates zu suchen und herunterzuladen. Wenn Sie WSUS verwenden, können Sie die Registrierungsschlüssel auf dem Nano Server so anpassen, dass stattdessen Ihr WSUS-Server verwendet wird.  
  
Informationen hierzu finden Sie in der Tabelle „Windows Update Agent Environment Options Registry Keys“ (Registrierungsschlüssel der Optionen der Windows Update-Agent-Umgebung) unter [Configure Automatic Updates in a Non–Active Directory Environment (Konfigurieren von automatischen Updates in einer nicht auf Active Directory basierenden Umgebung)](https://technet.microsoft.com/library/cc708449(v=ws.10).aspx).  
  
Sie sollten mindestens die Registrierungsschlüssel **WUServer** und **WUStatusServer** festlegen, allerdings könnten je nach Ihrer WSUS-Implementierung andere Werte erforderlich sein. Sie können diese Einstellungen immer überprüfen, indem Sie einen anderen Windows Server in der gleichen Umgebung untersuchen.  

Nachdem diese Werte für WSUS festlegt wurden, fragen die Befehle im vorherigen Abschnitt diesen Server nach Updates ab und verwenden ihn als Downloadquelle.  

### <a name="automatic-updates"></a>Automatische Updates  
---  
Derzeit besteht der Weg, die Updateinstallation zu automatisieren, darin, die oben beschriebenen Schritte in ein lokales Windows PowerShell-Skript zu konvertieren, und anschließend einen geplanten Task zu erstellen, diesen auszuführen und das System Ihrem Zeitplan entsprechend erneut zu starten.


## <a name="performance-and-event-monitoring-on-nano-server"></a>Leistung und Ereignisüberwachung unter Nano Server
[comment]: # (von Venkat Yalla.)
Nano Server unterstützt die [Ereignisablaufverfolgung für Windows](https://aka.ms/u2pa0i) (Event Tracing for Windows, ETW) vollständig, allerdings sind derzeit einige bekannte Tools zur Verwaltung von Protokollierung und Leistungsindikatoren nicht für Nano Server verfügbar. Nano Server verfügt jedoch über Tools und Cmdlets für die üblichen Leistungsanalyse-Szenarios.

Der allgemeine Workflow bleibt der gleiche, wie bei jeder Windows Server-Installation. Die Ablaufverfolgung mit geringem Mehraufwand wird auf dem Zielcomputer (Nano Server) ausgeführt, und die sich ergebenden Ablaufverfolgungsdateien und/oder Protokolle werden offline auf einem separaten Computer mithilfe von Tools wie [Windows Performance Analyzer](https://msdn.microsoft.com/library/windows/hardware/hh448170.aspx), der [Nachrichtenanalyse](https://www.microsoft.com/download/details.aspx?id=44226) usw. nachbearbeitet.

> [!NOTE]
> Ein Auffrischung zur Übertragung von Dateien mithilfe von PowerShell-Remoting finden Sie unter [How to copy files to and from Nano Server (So kopieren Sie Dateien aus und in Nano Server)](https://aka.ms/nri9c8).

In den folgenden Abschnitten werden die am häufigsten verwendeten Aktivitäten zur Sammlung von Leistungsdaten sowie ein unterstützter Weg dargestellt, dies unter Nano Server auszuführen.

### <a name="query-available-event-providers"></a>Abfragen von verfügbaren Ereignisanbietern
[Windows Performance Recorder](https://msdn.microsoft.com/en-us/library/hh448229.aspx) ist ein Tool, mit dem Sie verfügbare Ereignisanbieter wie folgt abfragen können:
```
wpr.exe -providers
```

Sie können die Ausgabe nach den Ereignistypen filtern, die von Interesse sind. Zum Beispiel:
```
PS C:\> wpr.exe -providers | select-string "Storage"

       595f33ea-d4af-4f4d-b4dd-9dacdd17fc6e                              : Microsoft-Windows-StorageManagement-WSP-Host
       595f7f52-c90a-4026-a125-8eb5e083f15e                              : Microsoft-Windows-StorageSpaces-Driver
       69c8ca7e-1adf-472b-ba4c-a0485986b9f6                              : Microsoft-Windows-StorageSpaces-SpaceManager
       7e58e69a-e361-4f06-b880-ad2f4b64c944                              : Microsoft-Windows-StorageManagement
       88c09888-118d-48fc-8863-e1c6d39ca4df                              : Microsoft-Windows-StorageManagement-WSP-Spaces
```

### <a name="record-traces-from-a-single-etw-provider"></a>Aufzeichnen von Ablaufverfolgungen von einem einzigen ETW-Anbieter
Hierzu können Sie neue [Cmdlets für die Verwaltung der Ereignisablaufverfolgung (in englischer Sprache)](https://technet.microsoft.com/library/dn919247.aspx) verwenden. Dies ist ein Beispielworkflow:

Erstellen Sie eine Ablaufverfolgung, starten Sie sie, und geben Sie dabei einen Dateinamen zum Speichern der Ereignisse an.
```
PS C:\> New-EtwTraceSession -Name "ExampleTrace" -LocalFilePath c:\etrace.etl
```

Fügen Sie der Ablaufverfolgung eine Anbieter-GUID hinzu. Verwenden Sie ```wpr.exe -providers``` für die Übersetzung des Anbieternamens in GUID. 
```
PS C:\> wpr.exe -providers | select-string "Kernel-Memory"

       d1d93ef7-e1f2-4f45-9943-03d245fe6c00                              : Microsoft-Windows-Kernel-Memory

PS C:\> Add-EtwTraceProvider -Guid "{d1d93ef7-e1f2-4f45-9943-03d245fe6c00}" -SessionName "ExampleTrace"
```

Entfernen Sie die Ablaufverfolgung. Dies beendet die Ablaufverfolgungssitzung, und Ereignisse werden an die zugehörige Protokolldatei weitergeleitet.
```
PS C:\> Remove-EtwTraceSession -Name "ExampleTrace"

PS C:\> dir .\etrace.etl

    Directory: C:\

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/14/2016  11:17 AM       16515072 etrace.etl
```
> [!NOTE]
> In diesem Beispiel wird ein einziger Ablaufverfolgungsanbieter zu der Sitzung hinzugefügt. Sie können allerdings auch das Cmdlet ```Add-EtwTraceProvider``` mehrmals für eine Ablaufverfolgungssitzung mit verschiedenen Anbieter-GUIDs verwenden, um die Ablaufverfolgung aus mehreren Quellen zu aktivieren. Eine weitere Alternative ist die Verwendung von ```wpr.exe```-Profilen wie nachfolgend beschriebenen.

### <a name="record-traces-from-multiple-etw-providers"></a>Aufzeichnen von Ablaufverfolgungen von mehreren ETW-Anbietern
Die Option ```-profiles``` von [Windows Performance Recorder](https://msdn.microsoft.com/library/hh448229.aspx) ermöglicht die Ablaufverfolgung von mehreren Anbietern zur gleichen Zeit. Es steht eine Reihe integrierter Profile wie CPU, Netzwerk und DiskIO zur Auswahl:
```
PS C:\Users\Administrator\Documents> wpr.exe -profiles 

Microsoft Windows Performance Recorder Version 10.0.14393 (CoreSystem)
Copyright (c) 2015 Microsoft Corporation. All rights reserved.

        GeneralProfile              First level triage
        CPU                         CPU usage
        DiskIO                      Disk I/O activity
        FileIO                      File I/O activity
        Registry                    Registry I/O activity
        Network                     Networking I/O activity
        Heap                        Heap usage
        Pool                        Pool usage
        VirtualAllocation           VirtualAlloc usage
        Audio                       Audio glitches
        Video                       Video glitches
        Power                       Power usage
        InternetExplorer            Internet Explorer
        EdgeBrowser                 Edge Browser
        Minifilter                  Minifilter I/O activity
        GPU                         GPU activity
        Handle                      Handle usage
        XAMLActivity                XAML activity
        HTMLActivity                HTML activity
        DesktopComposition          Desktop composition activity
        XAMLAppResponsiveness       XAML App Responsiveness analysis
        HTMLResponsiveness          HTML Responsiveness analysis
        ReferenceSet                Reference Set analysis
        ResidentSet                 Resident Set analysis
        XAMLHTMLAppMemoryAnalysis   XAML/HTML application memory analysis
        UTC                         UTC Scenarios
        DotNET                      .NET Activity
        WdfTraceLoggingProvider     WDF Driver Activity
```

Eine ausführliche Anleitung zum Erstellen benutzerdefinierter Profile finden Sie in der [WPR.exe-Dokumentation](https://msdn.microsoft.com/library/windows/hardware/hh448223.aspx).

### <a name="record-etw-traces-during-operating-system-boot-time"></a>Aufzeichnen von ETW-Ablaufverfolgungen beim Neustart des Betriebssystems
Verwenden Sie das Cmdlet ```New-AutologgerConfig``` zum Sammeln von Ereignissen während des Systemstarts. Die Verwendung ähnelt der des Cmdlets ```New-EtwTraceSession```, allerdings werden die zu der AutoLogger-Konfiguration hinzugefügten Anbieter erst beim nächsten Neustart aktiviert. Der gesamte Workflow sieht folgendermaßen aus:

Erstellen Sie zunächst eine neue AutoLogger-Konfiguration.
```
PS C:\> New-AutologgerConfig -Name "BootPnpLog" -LocalFilePath c:\bootpnp.etl 
```

Fügen Sie der Konfiguration einen ETW-Anbieter hinzu. Dieses Beispiel verwendet die Kernel-Plug & Play-Anbieter. Rufen Sie ```Add-EtwTraceProvider``` erneut auf, und geben Sie denselben AutoLogger-Namen, jedoch eine andere GUID an, um die Sammlung von Startablaufdaten aus mehreren Quellen zu aktivieren.
```
Add-EtwTraceProvider -Guid "{9c205a39-1250-487d-abd7-e831c6290539}" -AutologgerName BootPnpLog
```

Dies startet nicht unmittelbar eine ETW-Sitzung, sondern stattdessen konfigurieren eine, damit sie beim nächsten Neustart gestartet wird. Nach dem Neustart wird eine neue ETW-Sitzung mit dem Konfigurationsnamen „AutoLogger“ automatisch gestartet, wobei die hinzugefügten Ablaufverfolgungsanbieter aktiviert sind. Nachdem Nano Server neu startet, beendet der folgende Befehl die Ablaufverfolgungssitzung, nachdem die protokollierten Ereignisse an die zugewiesene Datei Ablaufverfolgungsdatei weitergeleitet wurden:
```
PS C:\> Remove-EtwTraceSession -Name BootPnpLog
```

Um zu verhindern, dass eine andere Ablaufverfolgungssitzung beim nächsten Neustart automatisch erstellt wird, entfernen Sie die AutoLogger-Konfiguration wie folgt:
```
PS C:\> Remove-AutologgerConfig -Name BootPnpLog
```

Ziehen Sie die Verwendung der [Sammlung von Setup- und Startereignissen](../administration/get-started-with-setup-and-boot-event-collection.md) in Betracht, um Neustart- und Setupablaufverfolgungen in einer Reihe von Systemen oder auf einem datenträgerlosen System zu sammeln.

### <a name="capture-performance-counter-data"></a>Erfassen von Leistungsindikatordaten
In der Regel überwachen Sie Leistungsindikatordaten mit der GUI „Perfmon.exe“. Verwenden Sie unter Nano Server die Entsprechung der ```Typeperf.exe```-Befehlszeilen. Zum Beispiel:

Verfügbare Leistungsindikatoren: Sie können die Ausgabe filtern, um für Sie interessante Daten leichter zu finden.
```
PS C:\> typeperf.exe -q | Select-String "UDPv6"

\UDPv6\Datagrams/sec
\UDPv6\Datagrams Received/sec
\UDPv6\Datagrams No Port/sec
\UDPv6\Datagrams Received Errors
\UDPv6\Datagrams Sent/sec
```

Mithilfe der Optionen können Sie die Häufigkeit und das Intervall angeben, mit denen Leistungsindikatordaten gesammelt werden. Im folgenden Beispiel wird der Prozessorleerlauf 5 Mal alle 3 Sekunden erfasst.
```
PS C:\> typeperf.exe "\Processor Information(0,0)\% Idle Time" -si 3 -sc 5

"(PDH-CSV 4.0)","\\ns-g2\Processor Information(0,0)\% Idle Time"
"09/15/2016 09:20:56.002","99.982990"
"09/15/2016 09:20:59.002","99.469634"
"09/15/2016 09:21:02.003","99.990081"
"09/15/2016 09:21:05.003","99.990454"
"09/15/2016 09:21:08.003","99.998577"
Exiting, please wait...
The command completed successfully.
```

Mithilfe weiterer Befehlszeilenoptionen können Sie die für Sie wichtigen Leistungsindikatornamen in einer Konfigurationsdatei angeben und so die Ausgabe u.a. in eine Protokolldatei umleiten. Weitere Informationen finden Sie in der [typeperf.exe-Dokumentation](https://technet.microsoft.com/library/bb490960.aspx).

Sie können auch die grafische Oberfläche von „Perfmon.exe“ remote mit Nano Server-Zielen verwenden. Wenn Sie der Ansicht Leistungsindikatoren hinzufügen, müssen Sie als Computername den Nano Server anstatt des *<Local computer>* angeben.

### <a name="interact-with-the-windows-event-log"></a>Interagieren mit dem Windows-Ereignisprotokoll

Nano Server unterstützt das Cmdlet ```Get-WinEvent```, das Filter- und Abfragefunktionen für das Windows-Ereignisprotokoll bereitstellt, sowohl lokal als auch auf einem Remotecomputer. Ausführlichere Informationen zu den Optionen und Beispiele finden Sie unter der [Dokumentationsseite von Get-WinEvent (in englischer Sprache)](https://technet.microsoft.com/library/hh849682.aspx). In diesem einfachen Beispiel wird der *Fehler* abgerufen, der im *Systemprotokoll* während der vergangenen zwei Tage notiert wurden.
```
PS C:\> $StartTime = (Get-Date) - (New-TimeSpan -Day 2)
PS C:\> Get-WinEvent -FilterHashTable @{LogName='System'; Level=2; StartTime=$StartTime} | select TimeCreated, Message

TimeCreated           Message
-----------           -------
9/15/2016 11:31:19 AM Task Scheduler service failed to start Task Compatibility module. Tasks may not be able to reg...
9/15/2016 11:31:16 AM The Virtualization Based Security enablement policy check at phase 6 failed with status: {File...
9/15/2016 11:31:16 AM The Virtualization Based Security enablement policy check at phase 0 failed with status: {File...
```

Nano Server unterstützt außerdem ```wevtutil.exe```, womit Sie Informationen über Ereignisprotokolle und Herausgeber abrufen können. Weitere Informationen finden Sie unter [Wevtutil.exe-Dokumentation](https://aka.ms/qvod7p). 

### <a name="graphical-interface-tools"></a>Tools für die grafische Oberfläche
[Web-basierte Server-Verwaltungstools](https://blogs.technet.microsoft.com/servermanagement/2016/08/17/deploy-setup-server-management-tools/) können zur Remoteverwaltung der Nano Server-Ziele verwendet werden und stellen ein Nano Server-Ereignisprotokoll mithilfe eines Webbrowsers bereit. Schließlich kann auch das MMC-Snap-In „Ereignisanzeige“ (eventvwr.msc) dazu verwendet werden, Protokolle anzuzeigen. Öffnen Sie es einfach auf einem Computer mit einem Desktop, und verweisen Sie es an einen Nano Remoteserver.




## <a name="using-windows-powershell-desired-state-configuration-with-nano-server"></a>Verwenden von Windows PowerShell DSC mit Nano Server  
  
Sie können Nano Server als Zielknoten mit Windows PowerShell Desired State Configuration (DSC) verwalten. Derzeit können Sie Knoten unter Nano Server mit DSC nur im Pushmodus verwenden. Allerdings funktionieren nicht alle DSC-Features mit Nano Server.  
  
Ausführliche Informationen finden Sie unter [Using DSC on Nano Server (Verwenden von DSC unter Nano Server)](https://msdn.microsoft.com/powershell/dsc/nanoDsc).  
