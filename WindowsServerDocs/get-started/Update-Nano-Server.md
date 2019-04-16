---
title: Aktualisieren von Nano Server
description: " "
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 7f74b35e93d4ddbe39b955daf7f78c4ef693aa9a
ms.sourcegitcommit: 07ac08dea2b8f2763c2614a999dc7967018aa0b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2018
ms.locfileid: "6121469"
---
# Aktualisieren von Nano Server

> [!IMPORTANT]
> Mit dem Beginn von Windows Server, Version 1709 steht Nano Server nur als [Basisimage des Betriebssystems für den Container](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image) zur Verfügung. Sehen Sie sich [Änderungen an Nano Server](nano-in-semi-annual-channel.md) an und erfahren Sie, was dies bedeutet. 

Sie haben zahlreiche Möglichkeiten, Nano Server zu aktualisieren. Nano Server basiert im Gegensatz zu anderen Installationsoptionen von Windows Server auf einem aktiveren Wartungsmodell, das mit dem von Windows10 vergleichbar ist. Die regelmäßigen Veröffentlichungen werden als **Current Branch for Business (CBB)** bezeichnet. Dieser Ansatz kommt Kunden entgegen, die schneller von Neuerungen profitieren und mit der Geschwindigkeit der Entwicklungslebenszyklen in der Cloud Schritt halten möchten. Weitere Informationen zu CBB finden Sie im [Windows Server-Blog](https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/).

**Zwischen den CBB-Veröffentlichungen** sorgen eine Reihe *kumulativer Updates* dafür, dass Nano Server immer auf dem neuesten Stand ist. Das erste kumulative Update für Nano Server wurde beispielsweise am 26. September 2016 mit [KB4093120](https://support.microsoft.com/help/4093120/windows-10-update-kb4093120)veröffentlicht. Dieses und nachfolgende kumulative Updates können auf verschiedene Weisen unter Nano Server installiert werden. In diesem Artikel veranschaulichen wir anhand von Update KB3192366, wie Sie kumulative Updates erhalten und auf Nano Server anwenden. Weitere Informationen zum Modell für kumulative Updates finden Sie im [Microsoft Update-Blog](https://blogs.technet.microsoft.com/mu/2016/10/25/patching-with-windows-server-2016/).

> [!NOTE]
> Wenn Sie ein optionales Nano Server-Paket von Medien oder aus dem Onlinerepository installieren, sind keine aktuellen Sicherheitsfixes enthalten. Um einen Versionskonflikt zwischen dem optionalen Paketen und der Basisbetriebssystemversion zu vermeiden sollten Sie das das neueste kumulative Update unmittelbar nach der Installation der optionalen Pakete und **vor** dem Neustart des Servers installieren.

Bei Verwendung des kumulativen Updates für Windows Server2016 vom 26.September2016 ([KB3192366](https://support.microsoft.com/en-us/kb/3192366)) muss zunächst das neueste Bereitstellungsstapelupdate für Windows10, Version 1607, vom 23.August2016 ([KB3176936](https://support.microsoft.com/en-us/kb/3176936)) als Voraussetzung installiert werden. Bei den meisten nachfolgend genannten Optionen benötigen Sie die MSU-Dateien, die die CAB-Updatepakete enthalten. Im Microsoft Update-Katalog können Sie die einzelnen Updatepakete herunterladen:
- [https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3192366](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3192366)
- [https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3176936](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3176936)

Nachdem Sie die MSU-Dateien aus dem Microsoft Update-Katalog heruntergeladen haben, speichern Sie diese auf einer Netzwerkfreigabe oder in einem lokalen Verzeichnis z.B. „C:\ServicingPackages“. Sie können die MSU-Dateien nach ihrer KB-Nummer umbenennen. Wir sind so verfahren, damit sie leichter identifiziert werden können. Extrahieren Sie dann die CAB-Dateien mit dem Hilfsprogramm EXPAND aus den MSU-Dateien in separate Verzeichnisse, und kopieren Sie die CAB-Dateien in einen einzelnen Ordner.

```code
    mkdir C:\ServicingPackages_expanded
    mkdir C:\ServicingPackages_expanded\KB3176936
    mkdir C:\ServicingPackages_expanded\KB3192366
    Expand C:\ServicingPackages\KB3176936.msu -F:* C:\ServicingPackages_expanded\KB3176936
    Expand C:\ServicingPackages\KB3192366.msu -F:* C:\ServicingPackages_expanded\KB3192366
    mkdir C:\ServicingPackages_cabs
    copy C:\ServicingPackages_expanded\KB3176936\Windows10.0-KB3176936-x64.cab C:\ServicingPackages_cabs
    copy C:\ServicingPackages_expanded\KB3192366\Windows10.0-KB3192366-x64.cab C:\ServicingPackages_cabs
```

Jetzt haben Sie je nach Bedarf unterschiedliche Möglichkeiten, die Updates mithilfe der extrahierten CAB-Dateien auf ein Nano Server-Image anzuwenden. Bei der Auflistung der folgenden Optionen wurde keine bestimmte Rangfolge beachtet. Verwenden Sie die Option, die für Ihre Umgebung am besten geeignet ist.

> [!NOTE]
> Wenn Sie zur Wartung von Nano Server die DISM-Tools verwenden, muss die DISM-Version mit der gewarteten Nano Server-Version identisch oder aber höher sein. Dazu können Sie DISM unter einer entsprechenden Windows-Version ausführen, eine entsprechende Version des [Windows Asssessment and Deployment Kits (ADK)](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit) installieren oder DISM unter Nano Server selbst ausführen.

## Option 1: Integrieren eines kumulativen Updates in ein neues Image
Wenn Sie ein neues Nano Server-Image erstellen, können Sie das aktuelle kumulative Update direkt in das Image integrieren, sodass es beim ersten Start vollständig gepatcht wird.

```powershell
New-NanoServerImage -ServicingPackagePath 'C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab', 'C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab' -<other parameters>
```

## Option 2: Integrieren eines kumulativen Updates in ein vorhandenes Image
Wenn Sie bereits über ein Nano Server-Image verfügen, das Sie als Basis zum Erstellen bestimmter Nano Server-Instanzen verwenden, können Sie das aktuelle kumulative Update direkt in Ihr vorhandenes Basisimage integrieren, sodass Computer, die mit dem Image erstellt werden, beim ersten Start vollständig gepatcht werden.

```powershell
Edit-NanoServerImage -ServicingPackagePath 'C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab', 'C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab' -TargetPath .\NanoServer.wim
```

## Option 3: Anwenden des kumulativen Updates auf eine vorhandene Offline-VHD oder -VHDX
Wenn Sie über eine virtuelle Festplatte (VHD oder VHDX) verfügen, können Sie das Update mithilfe der DISM-Tools auf die virtuelle Festplatte anwenden. Sie müssen sicherstellen, dass der Datenträger nicht verwendet wird, indem Sie entweder alle virtuellen Computer herunterfahren, die den Datenträger verwenden, oder die Bereitstellung der Datei für die virtuelle Festplatte aufheben.

- Mithilfe von PowerShell

   ```powershell
   Mount-WindowsImage -ImagePath .\NanoServer.vhdx -Path .\MountDir -Index 1
   Add-WindowsPackage -Path .\MountDir -PackagePath  C:\ServicingPackages_cabs
   Dismount-WindowsImage -Path .\MountDir -Save
   ```

- Mithilfe von „dism.exe“

   ```code
   dism.exe /Mount-Image /ImageFile:C:\NanoServer.vhdx /Index:1 /MountDir:C:\MountDir
   dism.exe /Image:C:\MountDir /Add-Package /PackagePath:C:\ServicingPackages_cabs
   dism.exe /Unmount-Image /MountDir:C:\MountDir /Commit
   ```

## Option 4: Anwenden des kumulativen Updates auf ein laufendes Nano Server-System
Wenn Sie über einen laufenden virtuellen Computer oder physischen Host unter Nano Server verfügen und die CAB-Datei für das Update heruntergeladen haben, können Sie das Update mit den DISM-Tools anwenden, während das Betriebssystem online ist. Sie müssen die CAB-Datei lokal auf das Nano Server-System oder an einen verfügbaren Speicherort im Netzwerk kopieren. Wenn Sie ein Bereitstellungsstapelupdate anwenden, müssen Sie den Server neu starten, nachdem Sie das Bereitstellungsstapelupdate angewendet haben, bevor Sie weitere Updates installieren.

> [!NOTE]
> Wenn Sie das Nano Server-VHD- oder -VHDX-Image mithilfe des New-NanoServerImage-Cmdlets erstellt haben, ohne für die Datei für die virtuelle Festplatte MaxSize anzugeben, reicht die Standardgröße von 4GB nicht aus, um das kumulative Update anzuwenden. Vor der Installation des Updates vergrößern Sie die virtuelle Festplatte und das Systemvolume mit dem Hyper-V-Manager, der Datenträgerverwaltung, PowerShell oder einem anderen Tool auf mindestens 10GB. Alternativ können Sie den ScratchDir-Parameter in den DISM-Tools verwenden, um das Scratchverzeichnis auf ein Volume mit mindestens 10GB freiem Speicherplatz festzulegen.

```powershell
$s = New-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
Copy-Item -ToSession $s -Path C:\ServicingPackages_cabs -Destination C:\ServicingPackages_cabs -Recurse
Enter-PSSession $s
```

- Mithilfe von PowerShell

   ```powershell
   # Apply the servicing stack update first and then restart
   Add-WindowsPackage -Online -PackagePath C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab
   Restart-Computer; exit

   # After restarting, apply the cumulative update and then restart
   Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
   Add-WindowsPackage -Online -PackagePath C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab
   Restart-Computer; exit
   ```

- Mithilfe von „dism.exe“
   ```powershell
   # Apply the servicing stack update first and then restart
   dism.exe /Online /Add-Package /PackagePath:C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab
   
   # After the operation completes successfully and you are prompted to restart, it's safe to
   # press Ctrl+C to cancel the pipeline and return to the prompt
   Restart-Computer; exit

   # After restarting, apply the cumulative update and then restart
   Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
   dism.exe /Online /Add-Package /PackagePath:C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab
   Restart-Computer; exit
   ```

## Option 5: Herunterladen und Installieren des kumulativen Updates auf einem laufenden Nano Server-System

Wenn Sie über einen laufenden virtuellen Computer oder physischen Host unter Nano Server verfügen, können Sie den WMI-Anbieter von Windows Update verwenden, um das Update herunterzuladen und zu installieren, während das Betriebssystem online ist. Bei dieser Methode müssen Sie die MSU-Datei nicht separat aus dem Microsoft Update-Katalog herunterladen. Der WMI-Anbieter kann alle verfügbaren Updates auf einmal erkennen, herunterladen und installieren.

```powershell
Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
```

- Suchen nach verfügbaren Updates
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  
   $result = $ci | Invoke-CimMethod -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=0";OnlineScan=$true}
   $result.Updates
   ```

- Installieren aller verfügbaren Updates
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession
   Invoke-CimMethod -InputObject $ci -MethodName ApplyApplicableUpdates
   Restart-Computer; exit
   ```

- Abrufen einer Liste installierter Updates
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession
   $result = $ci | Invoke-CimMethod -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=1";OnlineScan=$true}
   $result.Updates
   ```
   
## Weitere Optionen
Weitere Methoden zum Aktualisieren von Nano Server können sich mit den oben angegebenen Optionen überschneiden oder diese ergänzen. Diese Optionen umfassen Windows Server Update Services (WSUS), System Center Virtual Machine Manager (VMM), die Aufgabenplanung oder eine Lösung, die nicht von Microsoft stammt.
- [Konfigurieren von Windows Update für WSUS](https://msdn.microsoft.com/en-us/library/dd939844(v=ws.10).aspx) durch Festlegen der folgenden Registrierungsschlüssel:
  - WUServer
  - WUStatusServer (verwendet in der Regel den gleichen Wert wie WUServer)
  - UseWUServer
  - AUOptions
- [Verwalten von Fabric-Updates in VMM](https://technet.microsoft.com/library/gg675084(v=sc.12).aspx)
- [Registrieren einer geplanten Aufgabe](https://technet.microsoft.com/library/jj649811.aspx)