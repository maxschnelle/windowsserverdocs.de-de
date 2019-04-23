---
title: Was ist Server Core?
description: Erfahren Sie mehr über die Server Core-Installationsoption in Windows Server
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/20/2018
ms.openlocfilehash: 08229e458d0aa0c8e8397f0f053f37a207a1aea5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885601"
---
# <a name="what-is-the-server-core-installation-option-in-windows-server"></a>Was ist der Server Core-Installationsoption in Windows Server?

> Gilt für: WindowsServer (Halbjährlicher Kanal) und WindowsServer 2016

Die Server Core-Option ist eine Minimalinstallation aus, die verfügbar ist, wenn Sie die Standard oder Datacenter Edition von Windows Server bereitstellen. Server Core umfasst die meisten, aber nicht alle Serverrollen. Server Core verfügt über einen geringeren Speicherbedarf für die Datenträger, und daher eine kleinere Angriffsfläche aufgrund einer kleinere Codebasis. 

## <a name="server-core-vs-server-with-desktop-experience"></a>Server-(Core) oder Server mit Desktopdarstellung 
Wenn Sie Windows Server installieren, installieren Sie nur die Serverrollen, die Sie auswählen – Dadurch wird den gesamten Speicherbedarf für Windows Server zu reduzieren. Der Server mit der Installationsoption "Desktopdarstellung" installiert jedoch noch viele Dienste und andere Komponenten, die für ein bestimmtes Einsatzszenario zugängig häufig nicht erforderlich sind. 

Hier kommt Server Core ins Spiel: Server Core-Installation beseitigt, Dienste und andere Funktionen, die nicht häufig wichtig für die Unterstützung bestimmter sind verwendet Server-Rollen. Hyper-V-Server z. B. erforderlich keine grafische Benutzeroberfläche (GUI), da Sie fast alle Aspekte von Hyper-V entweder über die Befehlszeile mithilfe von Windows PowerShell oder mithilfe von Hyper-V-Manager verwalten können. 

## <a name="the-server-core-difference---core-capabilities-without-the-frills"></a>Der Unterschied für Server Core - Kernfunktionen, ohne die frills
Wenn Sie die Installation von Server Core auf einem System und melden Sie sich zum ersten Mal abgeschlossen haben, haben Sie für etwas überrascht. Der Hauptunterschied zwischen dem Server mit der Installationsoption "Desktopdarstellung" und die Server Core ist, dass Server Core nicht die folgenden Pakete des GUI-Shell enthält:

- Microsoft-Windows-Server-Shell-Package
- Microsoft-Windows-Server-Gui-Mgmt-Package
- Microsoft-Windows-Server-Gui-RSAT-Package
- Microsoft-Windows-Cortana-PAL-Desktop-Package

Das heißt, es gibt **kein Desktop** in Server Core beabsichtigt. Und gleichzeitig die Funktionen zur Unterstützung von traditionellen Geschäftsanwendungen und rollenbasierte Workloads erforderlich sind, muss die Server Core keine herkömmliche desktop-Benutzeroberfläche. Stattdessen dient Server Core über die Befehlszeile, über PowerShell oder ein GUI-Tool im Remotemodus verwaltet werden (z. B. [RSAT](../../remote/remote-server-administration-tools.md) oder [Windows Admin Center](../../manage/windows-admin-center/overview.md)).

Zusätzlich zur keine Benutzeroberfläche unterscheidet sich Server Core auch vom Server mit Desktopdarstellung auf folgende Weise:

- Server Core hat keinen Zugriff auf tools
- Keine OOBE (Out-of-Box-Experience) für die Einrichtung von Server Core
- Keine audiounterstützung

Die folgende Tabelle zeigt, welche Anwendungen verfügbar sind *lokal* in Server Core und Server mit Desktopdarstellung. **Wichtig**: In den meisten Fällen, Anwendungen, die als "nicht verfügbar" unter Remote von einem Windows-Clientcomputer ausgeführt werden kann aufgelistet und verwendet, um die Server Core-Installation zu verwalten.

> [!NOTE]
> Diese Liste erhebt Kurzübersicht – es soll eine vollständige Liste ist nicht.


| Application                     | Server Core     | Server mit Desktopdarstellung |
|------------------------------------|-----------------|--------------------------------|
| Eingabeaufforderung                     | verfügbar       | verfügbar                      |
| Windows PowerShell/ Microsoft .NET | verfügbar       | verfügbar                      |
| Perfmon.exe                        | nicht verfügbar  | verfügbar                      |
| Windbg (GUI)                         | unterstützt       | unterstützt                      |
| Resmon.exe                         | nicht verfügbar   | verfügbar                      |
| "Regedit"                            | verfügbar       | verfügbar                      |
| Fsutil.exe                         | verfügbar       | verfügbar                      |
| Disksnapshot.exe                   | nicht verfügbar   | verfügbar                      |
| Diskpart.exe                       | verfügbar       | verfügbar                      |
| Diskmgmt.msc                       | nicht verfügbar   | verfügbar                      |
| Devmgmt.msc                        | nicht verfügbar   | verfügbar                      |
| Server-Manager                     | nicht verfügbar  | verfügbar                      |
| Mmc.exe                            | nicht verfügbar   | verfügbar                      |
| Eventvwr                           | nicht verfügbar  | verfügbar                      |
| Wevtutil (Ereignis-Abfragen)           | verfügbar       | verfügbar                      |
| Services.msc                       | nicht verfügbar   | verfügbar                      |
| Systemsteuerung                      | nicht verfügbar   | verfügbar                      |
| Windows Update (GUI)                 | nicht verfügbar | verfügbar                      |
| Windows-Explorer                   | nicht verfügbar   | verfügbar                      |
| Taskleiste                            | nicht verfügbar   | verfügbar                      |
| Benachrichtigungen der Taskleiste              | nicht verfügbar   | verfügbar                      |
| taskmgr                            | verfügbar       | verfügbar                      |
| InternetExplorer oder Edge          | nicht verfügbar   | verfügbar                      |
| Integriertes Hilfesystem               | nicht verfügbar   | verfügbar                      |
| Windows 10 Shell                   | nicht verfügbar   | verfügbar                      |
| Windows Media Player               | nicht verfügbar   | verfügbar                      |
| PowerShell                         | verfügbar       | verfügbar                      |
| PowerShell ISE                     | nicht verfügbar   | verfügbar                      |
| PowerShell-IME                     | verfügbar       | verfügbar                      |
| Mstsc.exe                          | nicht verfügbar   | verfügbar                      |
| Remotedesktopdienste            | verfügbar       | verfügbar                      |
| Hyper-V-Manager                    | nicht verfügbar  | verfügbar                      |


Weitere Informationen darüber, was *ist* finden Sie in Server Core enthalten, [Rollen, Rollendienste und Features in Windows Server - Server Core enthalten](server-core-roles-and-services.md). Informationen darüber, was *nicht* finden Sie in Server Core enthalten, [Rollen, Rollendienste und Features im Server Core nicht enthalten.](server-core-removed-roles.md)

## <a name="get-started-using-server-core"></a>Erste Schritte mit Server Core
Verwenden Sie die folgende Informationen zum Installieren, konfigurieren und verwalten die Server Core-Installationsoption von Windows Server.

Server Core-Installation: 
- [Rollen, Rollendienste und Features im Server Core enthalten](server-core-roles-and-services.md)
- [Rollen, Rollendienste und Features nicht in Server Core](server-core-removed-roles.md)
- [Installieren Sie die Server Core-Installationsoption](../../get-started/getting-started-with-server-core.md)
- [Konfigurieren von Server Core mithilfe des SConfig-Tools](../../get-started/sconfig-on-ws2016.md)

Verwendung von Server Core:
- [Grundlegende Verwaltungsaufgaben für Server Core mit Windows PowerShell oder über die Befehlszeile](server-core-administer.md)
- [Verwalten von Server Core](server-core-manage.md)
- [Patchen von Server Core](server-core-servicing.md)
- [Konfigurieren von Speicherabbilddateien](server-core-memory-dump.md)