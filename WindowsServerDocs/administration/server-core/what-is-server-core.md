---
title: Was ist Server Core?
description: Weitere Informationen zur Server Core-Installationsoption in Windows Server
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/20/2018
ms.openlocfilehash: 269be253367ba2bc692a5903e7d519a40f487d8b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383341"
---
# <a name="what-is-the-server-core-installation-option-in-windows-server"></a>Was ist die Server Core-Installationsoption in Windows Server?

> Gilt für: Windows Server 2019, Windows Server 2016 und Windows Server (halbjährlicher Kanal)

Bei der Server Core-Option handelt es sich um eine minimale Installationsoption, die verfügbar ist, wenn Sie die Standard-oder Datacenter Edition von Windows Server bereitstellen. Server Core umfasst die meisten, aber nicht alle Server Rollen. Server Core hat einen geringeren Speicherbedarf und somit eine kleinere Angriffsfläche aufgrund einer geringeren Codebasis. 

## <a name="server-core-vs-server-with-desktop-experience"></a>Server (Core) vs-Server mit Desktop Darstellung 
Wenn Sie Windows Server installieren, installieren Sie nur die von Ihnen ausgewählten Server Rollen. Dies trägt dazu bei, den Gesamtbedarf für Windows Server zu verringern. Bei der Installationsoption Server mit Desktop Darstellung werden jedoch weiterhin viele Dienste und andere Komponenten installiert, die für ein bestimmtes Verwendungs Szenario häufig nicht benötigt werden. 

Dabei kommt Server Core ins Spiel: bei der Server Core-Installation werden alle Dienste und anderen Features eliminiert, die für die Unterstützung bestimmter häufig verwendeter Server Rollen nicht von entscheidender Bedeutung sind. Ein Hyper-v-Server benötigt z. b. keine grafische Benutzeroberfläche (GUI), da Sie praktisch alle Aspekte von Hyper-v entweder über die Befehlszeile mithilfe von Windows PowerShell oder Remote mit dem Hyper-v-Manager verwalten können. 

## <a name="the-server-core-difference---core-capabilities-without-the-frills"></a>Die Server Core-Differenz-Kern-Funktionen ohne die einfaches
Wenn Sie die Installation von Server Core auf einem System abgeschlossen haben und sich zum ersten Mal anmelden, sind Sie etwas überraschend. Der Hauptunterschied zwischen dem Server und der Desktop Darstellung-Installationsoption und Server Core besteht darin, dass Server Core nicht die folgenden GUI-shellpakete umfasst:

- Microsoft-Windows-Server-Shell-Package
- Microsoft-Windows-Server-GUI-Mgmt-Package
- Microsoft-Windows-Server-GUI-RSAT-Package
- Microsoft-Windows-Cortana-PAL-Desktop-Package

Anders ausgedrückt: Es gibt **keinen Desktop** in Server Core. Wenn Sie die für die Unterstützung herkömmlicher Geschäftsanwendungen und rollenbasierten Workloads erforderlichen Funktionen beibehalten, verfügt Server Core nicht über eine herkömmliche Desktop Schnittstelle. Stattdessen ist Server Core für die Remote Verwaltung über die Befehlszeile, PowerShell oder ein GUI-Tool (wie z. [b. RSAT](../../remote/remote-server-administration-tools.md) oder [Windows Admin Center](../../manage/windows-admin-center/overview.md)) konzipiert.

Neben der Benutzeroberfläche unterscheidet sich auch Server Core vom Server mit Desktop Darstellung wie folgt:

- Server Core verfügt über keine Barrierefreiheits Tools
- Keine OOBE (Out-of-Box-Umgebung) für die Einrichtung von Server Core
- Keine Audiounterstützung

In der folgenden Tabelle sind die Anwendungen aufgeführt, die *lokal* auf Server Core vs Server mit Desktop Darstellung verfügbar sind. **Wichtig**: In den meisten Fällen können Anwendungen, die unten als "nicht verfügbar" aufgeführt sind, Remote von einem Windows-Client Computer aus ausgeführt und zum Verwalten der Server Core-Installation verwendet werden.

> [!NOTE]
> Diese Liste ist für kurz Verweise gedacht. Sie ist nicht als umfassende Liste vorgesehen.


| Application                     | Server Core     | Server mit Desktopdarstellung |
|------------------------------------|-----------------|--------------------------------|
| Eingabeaufforderung                     | verfügbar       | verfügbar                      |
| Windows PowerShell/Microsoft .net | verfügbar       | verfügbar                      |
| Perfmon. exe                        | nicht verfügbar  | verfügbar                      |
| WinDbg (GUI)                         | unterstützt       | unterstützt                      |
| Resmon. exe                         | nicht verfügbar   | verfügbar                      |
| Regedit                            | verfügbar       | verfügbar                      |
| "F. exe"                         | verfügbar       | verfügbar                      |
| Disksnapshot. exe                   | nicht verfügbar   | verfügbar                      |
| Diskpart.exe                       | verfügbar       | verfügbar                      |
| Diskmgmt. msc                       | nicht verfügbar   | verfügbar                      |
| Devmgmt. msc                        | nicht verfügbar   | verfügbar                      |
| Server-Manager                     | nicht verfügbar  | verfügbar                      |
| "MMC. exe"                            | nicht verfügbar   | verfügbar                      |
| Eventvwr                           | nicht verfügbar  | verfügbar                      |
| Wevtutil (Ereignis Abfragen)           | verfügbar       | verfügbar                      |
| Services. msc                       | nicht verfügbar   | verfügbar                      |
| Systemsteuerung                      | nicht verfügbar   | verfügbar                      |
| Windows Update (GUI)                 | nicht verfügbar | verfügbar                      |
| Windows-Explorer                   | nicht verfügbar   | verfügbar                      |
| Taskleiste                            | nicht verfügbar   | verfügbar                      |
| Task leisten Benachrichtigungen              | nicht verfügbar   | verfügbar                      |
| Von "taskmgr                            | verfügbar       | verfügbar                      |
| Internet Explorer oder Microsoft Edge          | nicht verfügbar   | verfügbar                      |
| Integriertes Hilfesystem               | nicht verfügbar   | verfügbar                      |
| Windows 10 Shell                   | nicht verfügbar   | verfügbar                      |
| Windows Media Player               | nicht verfügbar   | verfügbar                      |
| PowerShell                         | verfügbar       | verfügbar                      |
| PowerShell ISE                     | nicht verfügbar   | verfügbar                      |
| PowerShell-IME                     | verfügbar       | verfügbar                      |
| Mstsc. exe                          | nicht verfügbar   | verfügbar                      |
| Remotedesktopdienste            | verfügbar       | verfügbar                      |
| Hyper-V-Manager                    | nicht verfügbar  | verfügbar                      |


Weitere Informationen zu den Funktionen von Server Core finden Sie unter [Rollen, Rollen Dienste und Features, die in Windows Server-Server Core enthalten](server-core-roles-and-services.md) *sind.* Informationen dazu, was nicht in Server Core enthalten *ist* , finden Sie unter [Rollen, Rollen Dienste und Features, die nicht in Server Core enthalten](server-core-removed-roles.md) sind.

## <a name="get-started-using-server-core"></a>Einstieg in die Verwendung von Server Core
Verwenden Sie die folgenden Informationen, um die Server Core-Installationsoption von Windows Server zu installieren, zu konfigurieren und zu verwalten.

Server Core-Installation: 
- [Rollen, Rollen Dienste und Features, die in Server Core enthalten sind](server-core-roles-and-services.md)
- [Rollen, Rollen Dienste und Features, die nicht in Server Core enthalten sind](server-core-removed-roles.md)
- [Installieren der Server Core-Installationsoption](../../get-started/getting-started-with-server-core.md)
- [Konfigurieren von Server Core mit dem SCONFIG-Tool](../../get-started/sconfig-on-ws2016.md)

Verwenden von Server Core:
- [Grundlegende Server Core-Verwaltungsaufgaben mithilfe von Windows PowerShell oder der Befehlszeile](server-core-administer.md)
- [Verwalten von Server Core](server-core-manage.md)
- [Patchen von Server Core](server-core-servicing.md)
- [Konfigurieren von Speicherabbilddateien](server-core-memory-dump.md)