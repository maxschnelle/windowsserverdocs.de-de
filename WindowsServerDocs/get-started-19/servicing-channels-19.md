---
title: Servicing Channels
description: 'Erläuterung der Windows Server-Service-Kanälen: LTSC und SAC'
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
ms.localizationpriority: high
ms.openlocfilehash: c4329339e37acbb0b589e767a570073f4ae1363f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848731"
---
# <a name="windows-server-servicing-channels-ltsc-and-sac"></a>Windows Server wartungskanälen: LTSC und SAC

>Gilt für: Windows Server 2019, Windows Server 2016


**Zwei primäre veröffentlichungskanäle stehen für Windows Server-Kunden, die Long-term Servicing-Kanal und den halbjährlichen Kanal zur Verfügung.** 

Sie können Server im Long-Term Servicing Channel (LTSC) belassen, sie in den neuen Semi-Annual Channel verschieben oder beide Kanäle verwenden, je nachdem, was für Ihre Anforderungen am besten geeignet ist.


## <a name="long-term-servicing-channel-ltsc"></a>Long-Term Servicing Channel (LTSC)
Sie sind mit diesem Freigabemodell bereits vertraut (es wurde früher „Long-Term Servicing *Branch*” genannt). Dabei wird eine neue Hauptversion von Windows Server alle 2 bis 3 Jahre veröffentlicht. Benutzer haben Anspruch auf 5 Jahre Mainstreamsupport und 5 Jahre erweiterten Support. Dieser Kanal eignet sich für Systeme, die eine längere Wartungsoption und funktionale Stabilität erfordern. Bereitstellung von Windows Server 2016 und frühere Versionen von Windows Server werden von den Veröffentlichungen im neuen Semi-Annual Channel nicht beeinflusst. Der Long-Term Servicing Channel erhält weiterhin sicherheitsrelevante und nicht sicherheitsrelevante Updates, jedoch keine neuen Features und Funktionen.

> [!Note]  
> **Das aktuelle LTSC-Produkt ist Windows Server 2019**. Wenn Sie diesen Kanal beibehalten möchten, sollten Sie Windows Server 2019 installieren (oder weiterhin nutzen), der im Server Core-Installationsmodus oder im Server mit Desktopdarstellungsinstallationsoptionen installiert werden kann.

## <a name="semi-annual-channel"></a>Semi-Annual Channel 
Den halbjährlichen Kanal eignet sich ideal für Kunden, die schnell Innovationen werden zum neuen Betriebssystem-Funktionen in kürzerem, sowohl in Anwendungen – insbesondere die integrierten Container und Microservices als auch in die softwaredefinierte nutzen Hybrid-Rechenzentrum. Für Windows Server-Produkte ‫im Semi-Annual Channel werden zweimal im Jahr neue Versionen bereitgestellt, im Frühjahr und Herbst Jede Version in diesen Kanal wird 18 Monate nach der ersten Veröffentlichung unterstützt.

Die meisten der mit dem Semi-Annual Channel eingeführten Features werden mit der nächsten Long-Term Servicing Channel-Version von Windows Server ausgerollt. Die Editionen, Funktionen und Inhalte sind je nach Feedback der Kunden von Version zu Version verschieden.

Semi-Annual Channel stehen für Kunden mit Volumenlizenz zur Verfügung [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx), sowie über den Azure Marketplace oder andere Cloud/Host-Dienstanbieter und Treueprogramme wie z. B. Visual Studio Subscriptions.

> [!Note]  
> **Die aktuelle Version des Semi-Annual Channel ist Windows Server, Version 1809**. Wenn Sie Server in diesen Kanal übertragen möchten, sollten Sie die Version 1809 von Windows Server installieren, die im Server Core-Modus oder als Nano Server in einem Container ausgeführt werden kann. Direkte Upgrades von Windows Server 2016 auf Windows Server der Version 1809 werden nicht unterstützt, da beide zu **unterschiedlichen Kanälen** gehören. Version 1809 von Windows Server ist kein Update für Windows Server 2016, sondern die erste Windows Server-Version in diesem neuen Semi-Annual Channel.



In diesem neuen Modell werden Windows Server-Versionen je nach Jahr und Monat der Veröffentlichung gekennzeichnet: z. B. wird eine Version des 9. Monats im Jahr 2017 (September) als **Version 1709** gekennzeichnet. Im Semi-Annual Channel werden zweimal pro Jahr neue Versionen von Windows Server bereitgestellt. Der Support Lifecycle für jede Version ist 18 Monate.

## <a name="should-you-keep-servers-on-the-ltsc-or-move-them-to-the-semi-annual-channel"></a>Sollten Sie Server im LTSC belassen oder in den Semi-Annual Channel verschieben?
Diese wichtigen Unterschiede sind zu berücksichtigen:

- Müssen Sie schnell innovativ sein? Benötigen Sie frühen Zugriff auf die neuesten Windows Server-Features? Müssen Sie in schneller Folge Hybrid-Anwendungen, Dev-Ops und Hyper-V-Fabrics unterstützen? Wenn ja, sollten Sie dem **Semi-Annual Channel beitreten**, indem Sie **Windows Server, Version 1809** installieren. Wie in diesem Thema beschrieben, erhalten Sie zweimal pro Jahr neue Versionen mit 18 Monaten Mainstreamsupport (produktionsbegleitend) pro Veröffentlichung. Sie erhalten diesen über Volumenlizenzierung, Azure oder Visual Studio Subscriptions. Derzeit erfordern Versionen im Semi-Annual Channel Volumenlizenzierung und Software Assurance, wenn Sie beabsichtigen, das Produkt in der Produktion auszuführen.
- Benötigen Sie Stabilität und Vorhersagbarkeit? Müssen Sie virtuelle Computer und herkömmliche Workloads auf physischen Servern ausführen? Wenn ja, sollten Sie **diese Server im Long-Term Servicing Channel belassen**. Die aktuelle LTSC-Version ist **Windows Server 2019**. Wie in diesem Thema beschrieben, haben Sie alle 2 bis 3 Jahre Zugriff auf neue Versionen, mit 5 Jahren Mainstreamsupport pro Version, auf die 5 Jahre erweiterter Support pro Version folgen. LTSC-Versionen stehen über alle Freigabemechanismen zur Verfügung. Versionen in der LTSC sind für alle Benutzer verfügbar, unabhängig vom verwendeten Lizenzierungsmodell. 

In der folgenden Tabelle sind die wichtigsten Unterschiede zwischen den Kanälen zusammengefasst:

|  | Long-Term Servicing Channel (Windows Server 2019) |Semi-Annual Channel (Windows Server) |
| ------------------- | ------------------------------------ | ------------------------------------------------- |
|Empfohlene Szenarien | Dateiserver für allgemeine Zwecke, Microsoft und nicht von Microsoft stammende Arbeitslasten, herkömmliche Apps, Infrastruktur-Rollen, Software-definierte Datacenter und hyperkonvergente Infrastruktur | Containerisierte Anwendungen, Container-Hosts und Anwendungsszenarien profitieren von schneller Innovation |
| Neu erschienen | Alle 2 – 3 Jahre |Alle sechs Monate |
| Support |5 Jahre grundlegender Support und 5 Jahre erweiterter Support | 18 Monate |
| Editionen | Alle verfügbaren Editionen von Windows Server | Standard Edition und Datacenter Edition |
| Wer kann es verwenden | Alle Kunden über alle Kanäle | Software Assurance und Cloud nur für Kunden |
| Installationsoptions | Server Core und Server mit Desktop-Version | Server Core für Container Host und Image und Nano Server-Containerimage |                |


## <a name="device-compatibility"></a>Gerätekompatibilität
Sofern nichts Gegenteiliges kommuniziert wird, sind die Mindestanforderungen zum Ausführen der Semi-Annual Channel-Versionen identisch mit denen der neuesten Long-Term Servicing Channel-Version von Windows Server. Beispiel: **Die aktuelle Long-Term Servicing Channel-Version ist Windows Server 2019**. Die meisten Hardwaretreiber funktionieren auch weiterhin auf diesen Versionen.

## <a name="servicing"></a>Wartung
Sowohl die Long-Term Servicing Channel-Version als auch die Semi-Annual Channel-Version werden mit Sicherheitsupdates und mit nicht sicherheitsrelevanten Updates unterstützt. Der Unterschied ist die Laufzeit, für die die Version unterstützt wird, wie oben beschrieben.

### <a name="servicing-tools"></a>Wartungstools
IT-Spezialisten stehen zahlreiche Tools für die Wartung von Windows Server zur Verfügung. Jede Option hat Vor- und Nachteile, die von Funktionen und Steuerung bis hin zu Einfachheit und niedrigem Verwaltungsaufwand reichen. Beispiele für die verfügbaren Wartungstools zur Verwaltung von Wartungs-Updates:

- **Windows Update (eigenständig)**: Diese Option ist nur verfügbar, für den Server, die mit dem Internet verbunden sind und über das Windows Update aktiviert.
- **Windows Server Update Services (WSUS)** bietet umfassende Kontrolle über Updates für Windows 10 sowie Windows Server und ist im Windows Server-Betriebssystem standardmäßig verfügbar. Neben dem Zurückstellen von Updates haben Organisationen auch die Möglichkeit, eine Genehmigungsebene für Updates hinzuzufügen und diese auf bestimmten Computern oder Computergruppen bereitzustellen, sobald sie bereit sind.
- **System Center Konfigurations-Manager** bietet die höchstmögliche Kontrolle über die Wartung. IT-Spezialisten können Updates zurückstellen und genehmigen und verfügen über mehrere Optionen für Bereitstellungszielgruppen und die Verwaltung der Bandbreitenverwendung und Bereitstellungszeiten.

Sie verwenden mindestens eine der folgenden Optionen, basierend auf Ihren Ressourcen, Mitarbeitern und Erfahrungen. Sie können die gleichen Prozesse auch weiterhin mit den Semi-annual Channel-Versionen verwenden: wenn Sie beispielsweise den System Center Konfigurations-Manager bereits zum Verwalten von Updates verwenden, können Sie ihn auch weiterhin verwenden. Ebenso ist die Verwendung von WSUS weiterhin möglich.

## <a name="obtain-preview-releases-through-the-windows-insider-program"></a>Vorabversionen über das Windows-Insider-Programm erhalten
Das Testen der frühen Builds von Windows Server hilft sowohl Microsoft als auch seinen Kunden und bietet die Möglichkeit, potenzielle Probleme vor der Freigabe zu erkennen. Es bietet den Kunden außerdem eine einzigartige Gelegenheit, die Funktion des Produkts direkt zu beeinflussen. 

Microsoft ist auf das Feedback während des Entwicklungsprozesses angewiesen, damit Änderungen so schnell wie möglich gemacht werden können. Ein frühzeitiges Testen und Feedback ist für den schnelleren Versionsrhythmus unabdingbar.

Weitere Informationen zur Teilnahme am Windows-Insider-Programm finden Sie unter [Windows-Insider-Programm für Serverdokumente](https://docs.microsoft.com/windows-insider/at-work/).

## <a name="to-identify-windows-server-2019-and-windows-server-version-1809"></a>Identifizieren von Windows Server 2019 und Windows Server, Version 1809

>[!Note]  
> Die folgende Anleitung soll nur dazu beitragen, LTSC und SAC zu identifizieren bzw. zwischen Lebenszyklus und allgemeiner Bestandsaufnahme zu unterscheiden.  Sie ist nicht für die Anwendungskompatibilität oder zur Darstellung einer bestimmten API-Oberfläche gedacht.  App-Entwickler sollten andere Anleitungen verwenden, um die Kompatibilität zu gewährleisten, da Komponenten, APIs und Funktionen über die Lebensdauer eines Systems hinzugefügt werden können bzw. noch fehlen. Die [Version des Betriebssystems](https://docs.microsoft.com/windows/desktop/SysInfo/operating-system-version) ist ein besserer Ausgangspunkt für App-Entwickler.

Öffnen Sie PowerShell, und verwenden Sie das Cmdlet Get-ItemProperty oder das Cmdlet Get-ComputerInfo, um diese Eigenschaften in der Registrierung zu überprüfen.  Zusammen mit der Buildnummer bezeichnet diese Angabe LTSC oder SAC durch das Vorhandensein oder Fehlen des Markenjahres (2019).  LTSC enthält sie, SAC nicht.  Zurückgegeben wird mit ReleaseId oder WindowsVersion auch das Timing der Version (1809), und ob es sich bei der Installation um Server Core oder Server mit Desktop Experience handelt. 

**Windows Server 2019 Datacenter Edition (LTSC) mit Desktop Experience-Beispiel:**

````PowerShell
Get-ItemProperty -Path "HKLM:\Software\Microsoft\Windows NT\CurrentVersion" | Select ProductName, ReleaseId, InstallationType, CurrentMajorVersionNumber,CurrentMinorVersionNumber,CurrentBuild
````

````
ProductName               : Windows Server 2019 Datacenter
ReleaseId                 : 1809
InstallationType          : Server
CurrentMajorVersionNumber : 10
CurrentMinorVersionNumber : 0
CurrentBuild              : 17763
````

**Windows Server, Version 1809 (, SAC) Standard Edition-Server-Core-Beispiel:**

````PowerShell
Get-ItemProperty -Path "HKLM:\Software\Microsoft\Windows NT\CurrentVersion" | Select ProductName, ReleaseId, InstallationType, CurrentMajorVersionNumber,CurrentMinorVersionNumber,CurrentBuild
````

````
ProductName               : Windows Server Standard
ReleaseId                 : 1809
InstallationType          : Server Core
CurrentMajorVersionNumber : 10
CurrentMinorVersionNumber : 0
CurrentBuild              : 17763
````

**Windows Server 2019 Standard Edition (LTSC) Server Core-Beispiel:**


````PowerShell
Get-ComputerInfo | Select WindowsProductName, WindowsVersion, WindowsInstallationType, OsServerLevel, OsVersion, OsHardwareAbstractionLayer
````

````
WindowsProductName            : Windows Server 2019 Standard
WindowsVersion                : 1809
WindowsInstallationType       : Server Core
OsServerLevel                 : ServerCore
OsVersion                     : 10.0.17763
OsHardwareAbstractionLayer    : 10.0.17763.107
````

Um abzufragen, ob das neue [Server Core App Compatibility FOD](https://docs.microsoft.com/windows-server/get-started-19/install-fod-19) auf einem Server vorhanden ist, verwenden Sie das Cmdlet [Get-WindowsCapability](https://docs.microsoft.com/powershell/module/dism/get-windowscapability?view=win10-ps) und suchen nach:
````
Name    :     ServerCore.AppCompatibility~~~~0.0.1.0
State   :     Installed
````

# <a name="related-topics"></a>Verwandte Themen
[Änderungen an der Nano Server auf Windows Server Halbjährlicher Kanal](../get-started/nano-in-semi-annual-channel.md)

[Windows Server-Support-Lebenszyklus](https://support.microsoft.com/lifecycle)

[Bestimmt, ob die Server Core ausgeführt wird](https://msdn.microsoft.com/library/hh846315%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)

[GetProductInfo-Funktion](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getproductinfo)

[Cmdlets für die Protokollierung von Software-Inventur](https://docs.microsoft.com/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps)
