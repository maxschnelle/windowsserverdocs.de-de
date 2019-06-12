---
title: Servicing Channels
description: 'Erläuterung der Windows Server-Service-Kanälen: LTSC und SAC'
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: high
ms.date: 05/21/2019
ms.openlocfilehash: dee19cd5a30b7d913a7faeeaa38368cee8a91895
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442293"
---
# <a name="windows-server-servicing-channels-ltsc-and-sac"></a>Windows Server wartungskanälen: LTSC und SAC

>Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal)

Windows Server-Kunden stehen zwei primäre Veröffentlichungskanäle zur Verfügung, der Long-Term Servicing Channel und der neue Semi-Annual Channel.

Sie können Server im Long-Term Servicing Channel (LTSC) belassen, sie in den neuen Semi-Annual Channel verschieben oder beide Kanäle verwenden, je nachdem, was für Ihre Anforderungen am besten geeignet ist.

## <a name="long-term-servicing-channel-ltsc"></a>Long-Term Servicing Channel (LTSC)

Sie sind mit diesem Freigabemodell bereits vertraut (es wurde früher „Long-Term Servicing *Branch*” genannt). Dabei wird eine neue Hauptversion von Windows Server alle 2 bis 3 Jahre veröffentlicht. Benutzer haben Anspruch auf 5 Jahre Mainstreamsupport und 5 Jahre erweiterten Support. Dieser Kanal eignet sich für Systeme, die eine längere Wartungsoption und funktionale Stabilität erfordern. Bereitstellung von Windows Server 2016 und frühere Versionen von Windows Server werden von den Veröffentlichungen im neuen Semi-Annual Channel nicht beeinflusst. Der Long-Term Servicing Channel erhält weiterhin sicherheitsrelevante und nicht sicherheitsrelevante Updates, jedoch keine neuen Features und Funktionen.

> [!Note]  
> **Das aktuelle LTSC-Produkt ist Windows Server 2019**. Wenn Sie diesen Kanal beibehalten möchten, sollten Sie Windows Server 2019 installieren (oder weiterhin nutzen), der im Server Core-Installationsmodus oder im Server mit Desktopdarstellungsinstallationsoptionen installiert werden kann.

## <a name="semi-annual-channel"></a>Semi-Annual Channel

Den halbjährlichen Kanal eignet sich ideal für Kunden, die schnell Innovationen werden zum neuen Betriebssystem-Funktionen in kürzerem, sowohl in Anwendungen – insbesondere die integrierten Container und Microservices als auch in die softwaredefinierte nutzen Hybrid-Rechenzentrum. Für Windows Server-Produkte ‫im Semi-Annual Channel werden zweimal im Jahr neue Versionen bereitgestellt, im Frühjahr und Herbst Jede Version in diesen Kanal wird 18 Monate nach der ersten Veröffentlichung unterstützt.

Die meisten der mit dem Semi-Annual Channel eingeführten Features werden mit der nächsten Long-Term Servicing Channel-Version von Windows Server ausgerollt. Die Editionen, Funktionen und Inhalte sind je nach Feedback der Kunden von Version zu Version verschieden.

Den halbjährlichen Kanal steht für Kunden mit Volumenlizenzierung lizenzierten [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx)sowie über den Azure Marketplace oder anderen Cloud /-hosting-Dienstanbieter und der Kundentreue Programme z. B. als Visual Studio-Abonnements.

> [!Note]  
> **Die aktuelle Version der Halbjährlicher Kanal ist Windows Server, Version 1903**. Wenn Sie Server in diesem Kanal versetzen möchten, sollten Sie Windows Server, Version 1903 sein, installieren, die in Server Core-Modus oder als Nano Server-Instanz in einem Container ausführen installiert werden kann. Direkte Upgrades von einer Long-term servicing Kanal-Version werden nicht unterstützt, da sie werden **verschiedene veröffentlichungskanäle**. Halbjährlicher Kanal-Versionen werden Updates nicht – es ist die nächste Version von Windows Server im halbjährlichen Kanal.

In diesem neuen Modell werden Windows Server-Versionen je nach Jahr und Monat der Veröffentlichung gekennzeichnet: z. B. wird eine Version des 9. Monats im Jahr 2017 (September) als **Version 1709** gekennzeichnet. Im Semi-Annual Channel werden zweimal pro Jahr neue Versionen von Windows Server bereitgestellt. Der Support Lifecycle für jede Version ist 18 Monate.

## <a name="should-you-keep-servers-on-the-ltsc-or-move-them-to-the-semi-annual-channel"></a>Sollten Sie Server im LTSC belassen oder in den Semi-Annual Channel verschieben?

Diese wichtigen Unterschiede sind zu berücksichtigen:

- Müssen Sie schnell innovativ sein? Benötigen Sie frühen Zugriff auf die neuesten Windows Server-Features? Müssen Sie in schneller Folge Hybrid-Anwendungen, Dev-Ops und Hyper-V-Fabrics unterstützen? Wenn Sie also sollten **verknüpfen den halbjährlichen Kanal** durch die Installation von **Windows Server, Version 1903**. Wie in diesem Thema beschrieben, erhalten Sie zweimal pro Jahr neue Versionen mit 18 Monaten Mainstreamsupport (produktionsbegleitend) pro Veröffentlichung. Sie erhalten diesen über Volumenlizenzierung, Azure oder Visual Studio Subscriptions. Derzeit erfordern Versionen im Semi-Annual Channel Volumenlizenzierung und Software Assurance, wenn Sie beabsichtigen, das Produkt in der Produktion auszuführen.
- Benötigen Sie Stabilität und Vorhersagbarkeit? Müssen Sie virtuelle Computer und herkömmliche Workloads auf physischen Servern ausführen? Wenn ja, sollten Sie **diese Server im Long-Term Servicing Channel belassen**. Die aktuelle LTSC-Version ist **Windows Server 2019**. Wie in diesem Thema beschrieben, haben Sie alle 2 bis 3 Jahre Zugriff auf neue Versionen, mit 5 Jahren Mainstreamsupport pro Version, auf die 5 Jahre erweiterter Support pro Version folgen. LTSC-Versionen stehen über alle Freigabemechanismen zur Verfügung. Versionen in der LTSC sind für alle Benutzer verfügbar, unabhängig vom verwendeten Lizenzierungsmodell. 

In der folgenden Tabelle sind die wichtigsten Unterschiede zwischen den Kanälen zusammengefasst:


|                       |                                                              Long-Term Servicing Channel (Windows Server 2019)                                                               |                                   Semi-Annual Channel (Windows Server)                                   |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Empfohlene Szenarien | Dateiserver für allgemeine Zwecke, Microsoft und nicht von Microsoft stammende Arbeitslasten, herkömmliche Apps, Infrastruktur-Rollen, Software-definierte Datacenter und hyperkonvergente Infrastruktur | Containerisierte Anwendungen, Container-Hosts und Anwendungsszenarien profitieren von schneller Innovation |
|     Neu erschienen      |                                                                               Alle 2 – 3 Jahre                                                                                |                                              Alle sechs Monate                                              |
|        Support        |                                                       5 Jahre grundlegender Support und 5 Jahre erweiterter Support                                                        |                                                18 Monate                                                 |
|       Editionen        |                                                                    Alle verfügbaren Editionen von Windows Server                                                                     |                                     Standard Edition und Datacenter Edition                                     |
|      Wer kann es verwenden      |                                                                      Alle Kunden über alle Kanäle                                                                      |                               Software Assurance und Cloud nur für Kunden                                |
| Installationsoptions  |                                                                Server Core und Server mit Desktop-Version                                                                |                 Server Core für Container Host und Image und Nano Server-Containerimage                 |

## <a name="device-compatibility"></a>Gerätekompatibilität

Sofern nichts Gegenteiliges kommuniziert wird, sind die Mindestanforderungen zum Ausführen der Semi-Annual Channel-Versionen identisch mit denen der neuesten Long-Term Servicing Channel-Version von Windows Server. Beispiel: **Die aktuelle Long-Term Servicing Channel-Version ist Windows Server 2019**. Die meisten Hardwaretreiber funktionieren auch weiterhin auf diesen Versionen.

## <a name="servicing"></a>Wartung

Sowohl die Long-Term Servicing Channel-Version als auch die Semi-Annual Channel-Version werden mit Sicherheitsupdates und mit nicht sicherheitsrelevanten Updates unterstützt. Der Unterschied ist die Laufzeit, für die die Version unterstützt wird, wie oben beschrieben.

### <a name="servicing-tools"></a>Wartungstools

IT-Spezialisten stehen zahlreiche Tools für die Wartung von Windows Server zur Verfügung. Jede Option hat Vor- und Nachteile, die von Funktionen und Steuerung bis hin zu Einfachheit und niedrigem Verwaltungsaufwand reichen. Beispiele für die verfügbaren Wartungstools zur Verwaltung von Wartungs-Updates:

- **Windows Update (eigenständig)** : Diese Option ist nur verfügbar, für den Server, die mit dem Internet verbunden sind und über das Windows Update aktiviert.
- **Windows Server Update Services (WSUS)** bietet umfassende Kontrolle über Updates für Windows 10 sowie Windows Server und ist im Windows Server-Betriebssystem standardmäßig verfügbar. Neben dem Zurückstellen von Updates haben Organisationen auch die Möglichkeit, eine Genehmigungsebene für Updates hinzuzufügen und diese auf bestimmten Computern oder Computergruppen bereitzustellen, sobald sie bereit sind.
- **System Center Konfigurations-Manager** bietet die höchstmögliche Kontrolle über die Wartung. IT-Spezialisten können Updates zurückstellen und genehmigen und verfügen über mehrere Optionen für Bereitstellungszielgruppen und die Verwaltung der Bandbreitenverwendung und Bereitstellungszeiten.

Sie verwenden mindestens eine der folgenden Optionen, basierend auf Ihren Ressourcen, Mitarbeitern und Erfahrungen. Sie können die gleichen Prozesse auch weiterhin mit den Semi-annual Channel-Versionen verwenden: wenn Sie beispielsweise den System Center Konfigurations-Manager bereits zum Verwalten von Updates verwenden, können Sie ihn auch weiterhin verwenden. Ebenso ist die Verwendung von WSUS weiterhin möglich.

## <a name="where-to-obtain-semi-annual-channel-releases"></a>Halbjährlicher Kanal zu erhalten, wo frei

Halbjährlicher Kanal Releases sollte als Neuinstallation installiert werden.

- Volume Licensing Service Center (VLSC): Kunden mit Volumenlizenzierung lizenzierten [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx) können diese Version abrufen, indem Sie auf die [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx) und auf **Anmeldung**. Klicken Sie dann auf **Downloads und SchlüsselKeys** und suchen Sie nach dieser Version. 

- Halbjährlicher Kanal-Versionen sind auch in [Microsoft Azure](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.WindowsServer?tab=Overview).

- Visual Studio-Abonnements: Halbjährlicher Kanal Releases durch Herunterladen von Visual Studio-Abonnenten erhalten die [Downloadseite für Visual Studio-Abonnent](https://my.visualstudio.com/downloads?pid=2347). Wenn Sie nicht bereits ein Abonnent sind, wechseln Sie zu [Visual Studio Subscriptions](https://www.visualstudio.com/subscriptions/), um sich anzumelden, und besuchen Sie anschließend die [Seite zum Herunterladen von Visual Studio-Abonnenten](https://my.visualstudio.com/downloads?pid=2347) wie oben beschrieben. Versionen, die über Visual Studio Subscriptions bereitgestellt werden, dienen nur zur Entwicklung und zum Testen.

- Rufen Sie die Preview-Versionen über das Windows-Insider-Programm: Das Testen der frühen Builds von Windows Server hilft sowohl Microsoft als auch seinen Kunden und bietet die Möglichkeit, potenzielle Probleme vor der Freigabe zu erkennen. Es bietet den Kunden außerdem eine einzigartige Gelegenheit, die Funktion des Produkts direkt zu beeinflussen.   
Microsoft ist auf das Feedback während des Entwicklungsprozesses angewiesen, damit Änderungen so schnell wie möglich gemacht werden können. Ein frühzeitiges Testen und Feedback ist für den schnelleren Versionsrhythmus unabdingbar. Rufen Sie mit der Windows-Insider-Programm finden Sie unter den [Windows Insider-Programm für Server-Dokumentation](https://docs.microsoft.com/windows-insider/at-work/).

## <a name="activating-semi-annual-channel-releases"></a>Aktivieren von Halbjährlicher Kanal releases

- Wenn Sie Microsoft Azure verwenden, sollten diese Version automatisch aktiviert.
- Wenn Sie diese Version aus dem Volume Licensing Service Center oder das Visual Studio-Abonnements erhalten haben, können Sie es mit Ihrer Windows Server 2019 CSVLK in Ihrer Umgebung (Key Management System, KMS) aktivieren. Weitere Informationen finden Sie unter [KMS-clientsetupschlüssel](../get-started/kmsclientkeys.md).

Halbjährlicher Kanal-Versionen, die vor dem Windows Server-2019 veröffentlicht wurden mithilfe der Windows Server 2016-CSVLK.

## <a name="why-do-semi-annual-channel-releases-offer-only-the-server-core-installation-option"></a>Warum bieten Halbjährlicher Kanal-Versionen nur mit die Installationsoption Server Core?

Eine der wichtigsten Schritte bei der Planung jeder Version von Windows Server ist das Kundenfeedback – wie verwenden Sie Windows Server? Welche neuen Features haben die größte Auswirkung auf die Windows Server-Bereitstellungen und ebenfalls auf Ihren täglichen Einsatz? Ihr Feedback zeigt uns, dass die Bereitstellung neuer Innovationen so schnell und effizient wie möglich ein Hauptanliegen ist. Zur gleichen Zeit, für die Kunden Innovationen am schnellsten, Sie haben uns mitgeteilt, dass Sie in erster Linie über die Befehlszeile Skripterstellung mit PowerShell zum Verwalten von Rechenzentren, und daher verfügen nicht über ein sicheres benötigen für die desktop grafische Benutzeroberfläche zur Verfügung, bei der Installation von Windows Server mit Desktopdarstellung, insbesondere jetzt, [Windows Admin Center](../manage/windows-admin-center/overview.md) ist für die Remoteverwaltung Ihrer Server verfügbar.

Durch den Fokus auf die Server Core-Installationsoption können wir diese Innovationen durch weitere Ressourcen gleichzeitig für herkömmliche Windows Server-Plattform-Funktionen und Anwendungskompatibilität entwickeln. Wenn Sie Feedback zu diesem oder anderen Problemen im Zusammenhang mit Windows Server und unseren zukünftigen Versionen haben, können Sie Vorschläge machen und Kommentare über den [Feedback-Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) abgeben.

## <a name="what-about-nano-server"></a>Was ist mit Nano Server?

Nano Server ist als ein Container-Betriebssystem im halbjährlichen Kanal verfügbar. Weitere Details finden Sie unter [Changes to Nano Server in Windows Server Semi-Annual Channel](../get-started/nano-in-semi-annual-channel.md).

## <a name="how-to-tell-whether-a-server-is-running-an-ltsc-or-sac-release"></a>Gewusst wie: feststellen, ob ein Server eine LTSC oder SAC-Version ausgeführt wird

Long-term Servicing Kanal gibt im Allgemeinen frei, wie z. B. Windows Server-2019 werden zur gleichen Zeit wie eine neue Version von den halbjährlichen Kanal, z. B. Windows Server, Version 1809 veröffentlicht. Dadurch ist es ein bisschen schwierig zu bestimmen, ob ein Server die Veröffentlichung im halbjährlichen Kanal ausgeführt wird. Anstatt die Nummer des Builds, müssen Sie den Namen des Produkts anzeigen: Halbjährlicher Kanal-Versionen verwenden, ohne eine Versionsnummer an den Produktnamen "Windows Server Standard" oder "Windows Server Datacenter", während der Long-term Servicing Channel releases enthalten die Versionsnummer, z. B. "Windows Server 2019 Datacenter".

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

## <a name="see-also"></a>Siehe auch

[Änderungen an der Nano Server auf Windows Server Halbjährlicher Kanal](../get-started/nano-in-semi-annual-channel.md)

[Windows Server-Support-Lebenszyklus](https://support.microsoft.com/lifecycle)

[Bestimmt, ob die Server Core ausgeführt wird](https://msdn.microsoft.com/library/hh846315%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)

[GetProductInfo-Funktion](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getproductinfo)

[Cmdlets für die Protokollierung von Software-Inventur](https://docs.microsoft.com/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps)
