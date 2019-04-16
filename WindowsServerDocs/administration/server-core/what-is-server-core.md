---
title: Was ist die Server Core?
description: Erfahren Sie mehr über die Server Core-Installationsoption von Windows Server
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/20/2018
ms.openlocfilehash: 08229e458d0aa0c8e8397f0f053f37a207a1aea5
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1718534"
---
# <a name="what-is-the-server-core-installation-option-in-windows-server"></a>Was ist die Server Core-Installationsoption von Windows Server?

> Betrifft: WindowsServer (Semikolons jährlichen Channel) und WindowsServer 2016

Die Server Core-Option ist eine minimale Installation-Option, die verfügbar ist, wenn Sie die Standard oder Datacenter Edition von Windows Server bereitstellen. Server Core enthält die meisten, jedoch nicht alle Serverrollen. Server Core verfügt über einen kleineren Datenträger Speicherbedarf und somit eine kleinere Angriffsfläche aufgrund einer kleineren Codebasis. 

## <a name="server-core-vs-server-with-desktop-experience"></a>Server (Core) Vs Server mit Desktopdarstellung 
Bei der Installation von Windows Server installieren Sie nur die Serverrollen, die Sie auswählen – Dadurch kann der allgemeine Speicherbedarf für Windows Server reduziert. Der Server mit Desktop Experience Installationsoption installiert jedoch noch viele Dienste und anderer Komponenten, die für einen bestimmten Verwendungsszenario häufig nicht benötigt werden. 

Hier kommt Server Core ins Spiel: die Server Core-Installation entfällt alle Dienste und andere Features, die nicht häufig entscheidend für die Unterstützung bestimmter sind verwendet Serverrollen. Beispielsweise kein Hyper-V Server graphical User Interface (GUI), nicht erforderlich, da Sie nahezu alle Aspekte von Hyper-V entweder über die Befehlszeile mithilfe von Windows PowerShell oder Remote über den Hyper-V-Manager verwalten können. 

## <a name="the-server-core-difference---core-capabilities-without-the-frills"></a>Die Server Core-Differenz - Kernfunktionen, ohne die frills
Sie nach Abschluss der Installation von Server Core auf einem System und melden Sie sich zum ersten Mal können Sie für eine plötzlich auszudrücken. Der Hauptunterschied zwischen dem Server mit Desktop Experience Installationsoption und Server Core ist, dass die Server Core nicht in den folgenden GUI Shell-Paketen enthalten ist:

- Microsoft Windows-Server-Verwaltungsshell-Paket
- Microsoft-Windows-Server-Gui-Mgmt-Package
- Microsoft-Windows-Server-Gui-RSAT-Package
- Microsoft-Windows-Cortana-PAL-Desktop-Package

Anders ausgedrückt, wird es **keine Desktop** in Server Core, Verhalten ist erwünscht. Beibehaltung der Funktionen zur Unterstützung von herkömmlichen Geschäftsanwendungen und rollenbasierte Arbeitslasten erforderlich ist Server Core eine herkömmliche desktop-Schnittstelle nicht vorhanden. Server Core soll stattdessen über die Befehlszeile, PowerShell oder ein GUI-Tool (wie [Remoteserver-Verwaltungstools](../../remote/remote-server-administration-tools.md) oder [Windows Admin Center](../../manage/windows-admin-center/overview.md)) remote verwaltet werden.

Zusätzlich zur keine Benutzeroberfläche unterscheidet Server Core auch auf dem Server mit Desktopdarstellung auf folgende Weise:

- Server Core hat keine Eingabehilfen
- Keine OOBE (Out-of-Box-Experience) für das Einrichten von Server Core
- Kein audio-Unterstützung

Die folgende Tabelle zeigt, welche Anwendungen verfügbar *lokal* auf Server Core Vs Server mit Desktopdarstellung sind. **Wichtig**: In den meisten Fällen Programmen, die als "nicht verfügbar" unter Remote von einem Windows-Client-Computer ausgeführt werden kann aufgeführt und zur Verwaltung Ihrer Server Core-Installations verwendet werden.

> [!NOTE]
> Diese Liste ist für die Kurzübersicht - vorgesehen es ist keine vollständige Liste werden soll.


| Application                     | Server Core     | Server mit Desktopdarstellung |
|------------------------------------|-----------------|--------------------------------|
| Befehlszeile                     | verfügbar       | verfügbar                      |
| Windows PowerShell / Microsoft .NET | verfügbar       | verfügbar                      |
| Perfmon.exe                        | nicht verfügbar  | verfügbar                      |
| WinDbg (GUI)                         | unterstützt       | unterstützt                      |
| Resmon.exe                         | nicht verfügbar   | verfügbar                      |
| Regedit ein.                            | verfügbar       | verfügbar                      |
| Fsutil.exe                         | verfügbar       | verfügbar                      |
| Disksnapshot.exe                   | nicht verfügbar   | verfügbar                      |
| Diskpart.exe                       | verfügbar       | verfügbar                      |
| Diskmgmt.msc                       | nicht verfügbar   | verfügbar                      |
| Devmgmt.msc                        | nicht verfügbar   | verfügbar                      |
| Server-Manager                     | nicht verfügbar  | verfügbar                      |
| MMC.exe                            | nicht verfügbar   | verfügbar                      |
| Eventvwr                           | nicht verfügbar  | verfügbar                      |
| Wevtutil (Ereignisabfragen)           | verfügbar       | verfügbar                      |
| Services.msc                       | nicht verfügbar   | verfügbar                      |
| Systemsteuerung                      | nicht verfügbar   | verfügbar                      |
| Windows Update (GUI)                 | nicht verfügbar | verfügbar                      |
| Windows-Explorer                   | nicht verfügbar   | verfügbar                      |
| Taskleiste                            | nicht verfügbar   | verfügbar                      |
| Taskleiste              | nicht verfügbar   | verfügbar                      |
| Taskmgr                            | verfügbar       | verfügbar                      |
| InternetExplorer oder Edge          | nicht verfügbar   | verfügbar                      |
| Integrierte Hilfesystem               | nicht verfügbar   | verfügbar                      |
| Windows-10-Shell                   | nicht verfügbar   | verfügbar                      |
| Windows Media Player               | nicht verfügbar   | verfügbar                      |
| PowerShell                         | verfügbar       | verfügbar                      |
| PowerShell ISE                     | nicht verfügbar   | verfügbar                      |
| PowerShell-IME                     | verfügbar       | verfügbar                      |
| Mstsc.exe                          | nicht verfügbar   | verfügbar                      |
| Remotedesktopdienste            | verfügbar       | verfügbar                      |
| Hyper-V-Manager                    | nicht verfügbar  | verfügbar                      |


Weitere Informationen dazu, welche *ist* in Server Core enthalten finden Sie unter [Rollen, Rollendienste und Features in Windows Server - Server Core enthalten](server-core-roles-and-services.md). Und Informationen dazu, welche *ist nicht* in Server Core enthalten, finden Sie unter [Rollen, Rollendienste und Features in Server Core nicht enthalten](server-core-removed-roles.md)

## <a name="get-started-using-server-core"></a>Erste Schritte mit der Server Core
Verwenden Sie die folgende Informationen zum Installieren, konfigurieren und verwalten die Server Core-Installationsoption von Windows Server.

Server Core-Installation: 
- [Rollen, Rollendienste und Features in Server Core enthalten](server-core-roles-and-services.md)
- [Rollen, Rollendienste und Features nicht in Server Core](server-core-removed-roles.md)
- [Installieren Sie die Server Core-Installationsoption](../../get-started/getting-started-with-server-core.md)
- [Konfigurieren von Server Core mit dem Tool SConfig](../../get-started/sconfig-on-ws2016.md)

Verwenden von Server Core:
- [Grundlegende Server Core-Verwaltungsaufgaben mithilfe von Windows PowerShell oder der Befehlszeile](server-core-administer.md)
- [Server Core verwalten](server-core-manage.md)
- [Patchen von Server Core](server-core-servicing.md)
- [Konfigurieren von Speicherabbilddateien](server-core-memory-dump.md)