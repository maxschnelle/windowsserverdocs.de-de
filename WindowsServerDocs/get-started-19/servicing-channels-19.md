---
title: Wartungskanäle
description: 'Erläuterung der Windows Server-Servicekanäle: LTSC und SAC'
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: high
ms.date: 05/21/2019
ms.openlocfilehash: a10cb3b27e3434ab818b41e051edb38ab77626db
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80827133"
---
# <a name="windows-server-servicing-channels-ltsc-and-sac"></a>Windows Server-Wartungskanäle: LTSC und SAC

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)

Windows Server-Kunden stehen zwei primäre Releasekanäle zur Verfügung, der Long-Term Servicing Channel und der halbjährliche Kanal.

Sie können Server im Long-Term Servicing Channel (LTSC) belassen, sie in den halbjährlichen Kanal verschieben oder für einige Server einen von beiden Kanälen verwenden, je nachdem, was für Ihre Anforderungen am besten geeignet ist.

## <a name="long-term-servicing-channel-ltsc"></a>Long-Term Servicing Channel (LTSC)

Sie sind mit diesem Releasemodell bereits vertraut (es wurde früher „Long-Term Servicing *Branch*“ genannt), in dem alle 2 bis 3 Jahre eine neue Hauptversion von Windows Server veröffentlicht wird. Benutzer haben Anspruch auf 5 Jahre Mainstreamsupport und 5 Jahre erweiterten Support. Dieser Kanal eignet sich für Systeme, die eine längere Wartungsoption und funktionale Stabilität erfordern. Bereitstellungen von Windows Server 2016 und frühere Versionen von Windows Server sind von den Releases im neuen Semi-Annual Channel nicht betroffen. Der Long-Term Servicing Channel erhält weiterhin sicherheitsrelevante und nicht sicherheitsrelevante Updates, jedoch keine neuen Features und Funktionen.

> [!Note]  
> **Das aktuelle LTSC-Produkt ist Windows Server 2019**. Wenn Sie diesen Kanal beibehalten möchten, sollten Sie Windows Server 2019 installieren (oder weiterhin nutzen), der im Server Core-Installationsmodus oder als Server mit der Desktopdarstellungs-Installationsoption installiert werden kann.

## <a name="semi-annual-channel"></a>Halbjährlicher Kanal

Der halbjährliche Kanal wurde für Kunden konzipiert, die schnell Neuerungen einführen, um von neuen Betriebssystemfunktionen frühzeitig zu profitieren, sowohl in Anwendungen – insbesondere solchen, die auf Containern und Microservices basieren – als auch in hybriden, softwaredefinierten Rechenzentren. Für Windows Server-Produkte ‫im halbjährlichen Kanal werden zweimal im Jahr neue Versionen bereitgestellt, im Frühjahr und Herbst. Jede Version in diesen Kanal wird nach der ersten Veröffentlichung 18 Monate lang unterstützt.

Die meisten der im halbjährlichen Kanal eingeführten Features werden in der nächsten Long-Term Servicing Channel-Release von Windows Server zusammengefasst. Die Editionen, die Funktionen und die unterstützenden Inhalte können sich je nach Kundenfeedback von Release zu Release unterscheiden.

Der halbjährliche Kanal steht Kunden mit Volumenlizenz mit [Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx) zur Verfügung sowie über den Azure Marketplace oder andere Cloud/Hosting-Dienstanbieter und Treueprogramme wie z.B. Visual Studio-Abonnements.

> [!Note]  
> **Die aktuelle Version des Semi-Annual Channel ist Windows Server, Version 1903**. Wenn Sie Server in diesen Kanal übertragen möchten, sollten Sie die Version 1903 von Windows Server installieren, die im Server Core-Modus oder als Nanoserver in einem Container installiert werden kann. Direkte Upgrades von einer Release aus dem Long-Term Servicing Channel werden nicht unterstützt, da sie sich in **verschiedenen Releasekanälen** befinden. Releases im halbjährlichen Kanal stellen keine Updates dar – bei ihnen handelt es sich um das nächste Release von Windows Server im halbjährlichen Kanal.

In diesem neuen Modell werden Windows Server-Versionen je nach Jahr und Monat der Veröffentlichung gekennzeichnet: z.B. wird eine Version aus dem 9. Monat im Jahr 2017 (September) als **Version 1709** bezeichnet. Im halbjährlichen Kanal werden zweimal pro Jahr neue Versionen von Windows Server bereitgestellt. Der Supportlebenszyklus für jede Version beträgt 18 Monate.

## <a name="should-you-keep-servers-on-the-ltsc-or-move-them-to-the-semi-annual-channel"></a>Sollten Sie Server im LTSC belassen oder in den halbjährlichen Kanal verschieben?

Diese wichtigen Unterschiede sind zu berücksichtigen:

- Müssen Sie schnell innovativ sein? Benötigen Sie frühzeitig Zugriff auf die neuesten Windows Server-Features? Müssen Sie in schneller Folge Hybrid-Anwendungen, Dev-Ops und Hyper-V-Fabrics unterstützen? Wenn ja, sollten Sie dem **Halbjährlichen Kanal beitreten**, indem Sie **Windows Server, Version 1903** installieren. Wie in diesem Thema beschrieben, erhalten Sie zweimal pro Jahr neue Versionen mit 18 Monaten Mainstream-Support für Produktionsumgebungen pro Release. Sie erhalten diese über Volumenlizenzierung, Azure oder Visual Studio-Abonnementdienste. Derzeit erfordern Versionen im halbjährlichen Kanal Volumenlizenzierung und Software Assurance, wenn Sie beabsichtigen, das Produkt in Produktionsumgebungen einzusetzen.
- Benötigen Sie Stabilität und Vorhersagbarkeit? Müssen Sie virtuelle Computer und herkömmliche Workloads auf physischen Servern ausführen? Wenn ja, sollten Sie **diese Server im Long-Term Servicing Channel belassen**. Die aktuelle LTSC-Version ist **Windows Server 2019**. Wie in diesem Thema beschrieben, haben Sie alle 2 bis 3 Jahre Zugriff auf neue Versionen, mit 5 Jahren Mainstream-Support, auf die 5 Jahre erweiterter Support pro Version folgen. LTSC-Versionen stehen über alle Releasemechanismen zur Verfügung. Versionen im LTSC sind für alle Benutzer verfügbar, unabhängig vom verwendeten Lizenzierungsmodell. 

In der folgenden Tabelle sind die wichtigsten Unterschiede zwischen den Kanälen zusammengefasst:


|                       |                                                              Long-Term Servicing Channel (Windows Server 2019)                                                               |                                   Halbjährlicher Kanal (Windows Server)                                   |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Empfohlene Szenarien | Dateiserver für allgemeine Zwecke, von Microsoft und nicht von Microsoft stammende Workloads, herkömmliche Apps, Infrastruktur-Rollen, softwaredefinierte Rechenzentren und hyperkonvergente Infrastruktur | Anwendungen in Containern, Container-Hosts und Anwendungsszenarien, die von schneller Innovation profitieren |
|     Neue Versionen      |                                                                               Alle 2–3 Jahre                                                                                |                                              Alle 6 Monate                                              |
|        Support        |                                                       5 Jahre grundlegender Support und 5 Jahre erweiterter Support                                                        |                                                18 Monate                                                 |
|       Editionen        |                                                                    Alle verfügbaren Editionen von Windows Server                                                                     |                                     Standard Edition und Datacenter Edition                                     |
|      Für wen nutzbar      |                                                                      Alle Kunden über alle Kanäle                                                                      |                               Nur Software Assurance- und Cloud-Kunden                                |
| Installationsoptions  |                                                                Server Core und Server mit Desktopdarstellung                                                                |                 Server Core für Container-Hosts und Images und Nano Server-Containerimage                 |

## <a name="device-compatibility"></a>Gerätekompatibilität

Sofern nichts Gegenteiliges kommuniziert wird, sind die Mindestanforderungen zum Ausführen der Releases im halbjährlichen Kanal identisch mit denen des neuesten Release von Windows Server im Long-Term Servicing Channel. Beispiel: **Die aktuelle Version im Long-Term Servicing Channel ist Windows Server 2019**. Die meisten Hardwaretreiber funktionieren auch weiterhin in diesen Versionen.

## <a name="servicing"></a>Wird gewartet

Sowohl die Releases im Long-Term Servicing Channel als auch die im halbjährlichen Kanal werden mit Sicherheitsupdates und mit nicht sicherheitsrelevanten Updates unterstützt. Der Unterschied liegt in der Dauer der Unterstützung für das Release, wie oben beschrieben.

### <a name="servicing-tools"></a>Wartungstools

Es gibt viele Tools, mit denen IT-Experten Windows Server warten können. Jede Option hat Vor- und Nachteile, die von Funktionen und Steuerung bis hin zu Einfachheit und niedrigem Verwaltungsaufwand reichen. Beispiele für die verfügbaren Wartungstools zur Verwaltung von Wartungsupdates:

- **Windows Update (eigenständig)** : Diese Option steht nur für Server zur Verfügung, die mit dem Internet verbunden sind und Windows Update aktiviert haben.
- **Windows Server Update Services (WSUS)** bietet umfassende Kontrolle über Updates für Windows 10 sowie Windows Server und ist im Windows Server-Betriebssystem standardmäßig verfügbar. Neben dem Zurückstellen von Updates haben Organisationen auch die Möglichkeit, eine Genehmigungsebene für Updates hinzuzufügen und diese auf bestimmten Computern oder Computergruppen bereitzustellen, sobald sie bereit sind.
- **Microsoft Endpoint Configuration Manager** bietet die höchstmögliche Kontrolle über die Wartung. IT-Spezialisten können Updates zurückstellen und genehmigen und verfügen über mehrere Optionen für Bereitstellungszielgruppen und die Verwaltung der Bandbreitenverwendung und Bereitstellungszeiten.

Sie haben sich auf der Grundlage Ihrer Ressourcen, Ihrer Mitarbeiter und Ihrer Erfahrung vermutlich bereits für mindestens eine dieser Optionen entschieden. Sie können das gleiche Verfahren für Releases im halbjährlichen Kanal auch weiterhin verwenden: Wenn Sie beispielsweise bereits Configuration Manager zum Verwalten von Updates verwenden, können Sie damit fortfahren. Ebenso ist die Verwendung von WSUS weiterhin möglich.

## <a name="where-to-obtain-semi-annual-channel-releases"></a>Bezug von Releases im halbjährlichen Kanal

Releases im halbjährlichen Kanal sollten als Neuinstallation installiert werden.

- Volume Licensing Service Center (VLSC) Volumenlizenz-Kunden mit [Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx) können dieses Release erhalten, indem sie im [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx) auf **Anmeldung** klicken. Klicken Sie dann auf **Downloads und Schlüssel**, und suchen Sie nach diesem Release. 

- Releases im halbjährlichen Kanal sind auch in [Microsoft Azure](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WindowsServer?tab=Overview) verfügbar.

- Visual Studio-Abonnements: Visual Studio-Abonnenten können Releases im halbjährlichen Kanal erhalten, indem sie sie von der [Downloadseite für Visual Studio-Abonnenten](https://my.visualstudio.com/downloads?pid=2347) herunterladen. Wenn Sie noch kein Abonnent sind, navigieren Sie zu [Visual Studio-Abonnements](https://www.visualstudio.com/subscriptions/), um sich zu registrieren, und besuchen Sie dann die [Downloadseite für Visual Studio-Abonnenten](https://my.visualstudio.com/downloads?pid=2347), wie oben beschrieben. Releases, die über Visual Studio-Abonnements bezogen werden, sind nur zu Entwicklungs- und Testzwecken bestimmt.

- Vorschauversionen können Sie über das Windows-Insider-Programm erhalten: Aufgrund der Möglichkeit zum Aufspüren potenzieller Probleme vor der Veröffentlichung hilft das frühzeitige Testen von Builds von Windows Server sowohl Microsoft als auch dessen Kunden. Dies gibt Kunden auch eine einzigartige Gelegenheit, direkt auf die im Produkt enthaltenen Funktionen Einfluss zu nehmen.   
Microsoft ist auf Feedback während des Entwicklungsprozesses angewiesen, damit Anpassungen so schnell wie möglich gemacht werden können. Frühzeitiges Testen und Feedback sind für das Modell schneller Releases unabdingbar. Informationen zur Teilnahme am Windows-Insider-Programm finden Sie unter [Windows-Insider-Programm für Serverdokumente](https://docs.microsoft.com/windows-insider/at-work/).

## <a name="activating-semi-annual-channel-releases"></a>Aktivieren von Releases im halbjährlichen Kanal

- Wenn Sie Microsoft Azure verwenden, sollte das Release automatisch aktiviert werden.
- Wenn Sie dieses Release über das Volume Licensing Service Center oder Visual Studio-Abonnements erhalten haben, können Sie es mithilfe Ihres Windows Server 2019-CSVLKs in Verbindung mit Ihrem Key Management System (KMS) aktivieren. Weitere Informationen finden Sie unter [KMS-Clientsetupschlüssel](../get-started/kmsclientkeys.md).

Releases im halbjährlichen Kanal, die vor Windows Server 2019 veröffentlicht wurden, verwenden den Windows Server 2016-CSVLK.

## <a name="why-do-semi-annual-channel-releases-offer-only-the-server-core-installation-option"></a>Warum bieten Releases im halbjährlichen Kanal nur die Server Core-Installationsoption?

Einer der wichtigsten Schritte, die wir bei der Planung der einzelnen Releases von Windows Server ausführen, ist die Einbeziehung von Kundenfeedback: Wie nutzen Sie Windows Server? Welche neuen Funktionen haben die größte Auswirkung auf Ihre Windows Server-Bereitstellungen und damit auch auf Ihr Tagesgeschäft? Ihr Feedback zeigt uns, dass die möglichst schnelle und effiziente Bereitstellung von Innovationen ein Hauptanliegen ist. Zugleich haben uns Kunden, die Innovationen besonders schnell einführen, mitgeteilt, dass sie in erster Linie Befehlszeilenskripts mit PowerShell für die Verwaltung ihrer Rechenzentren verwenden und daher nicht unbedingt die Desktop-GUI benötigen, die in der Installation von Windows Server mit Desktopdarstellung verfügbar ist, vor allem, da jetzt das [Windows Admin Center](../manage/windows-admin-center/overview.md) für die Remoteverwaltung von Servern erhältlich ist.

Durch die Konzentration auf die Server Core-Installationsoption können wir den Innovationen mehr Ressourcen widmen und zugleich die traditionelle Funktionalität und Anwendungskompatibilität der Windows Server-Plattform beibehalten. Wenn Sie Feedback zu diesem Thema oder zu anderen Problemen im Hinblick auf Windows Server und unsere künftigen Releases haben, können Sie über den [Feedback-Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) Vorschläge machen und Kommentare abgeben.

## <a name="what-about-nano-server"></a>Was ist mit Nano Server?

Nano Server ist als Containerbetriebssystem im halbjährlichen Kanal verfügbar. Weitere Details finden Sie unter [Änderungen bei Nano Server im halbjährlichen Kanal von Windows Server](../get-started/nano-in-semi-annual-channel.md).

## <a name="how-to-tell-whether-a-server-is-running-an-ltsc-or-sac-release"></a>Feststellen, ob auf einem Server ein LTSC- oder ein SAC-Release ausgeführt wird

Im Allgemeinen werden Releases im Long-Term Servicing Channel, wie etwa Windows Server 2019, zum gleichen Zeitpunkt wie die neue Version des halbjährlichen Kanals veröffentlicht, beispielsweise Windows Server, Version 1809. Dadurch kann die Bestimmung, ob ein Server ein Release des halbjährlichen Kanals ausführt, etwas schwieriger werden. Statt auf die Buildnummer müssen Sie auf den Produktnamen achten: Für Releases im halbjährlichen Kanal werden die Produktnamen „Windows Server Standard“ oder „Windows Server Datacenter“ ohne Versionsnummer verwendet, während Releases im Long-Term Servicing Channel die Versionsnummer enthalten, z. B. „Windows Server 2019 Datacenter“.

>[!Note]  
> Die folgende Anleitung ist nur dazu vorgesehen, die Bestimmung von LTSC und SAC zur allgemeinen Bestandsaufnahme zu erleichtern.  Sie ist nicht zur Bestimmung der Anwendungskompatibilität oder zur Darstellung einer bestimmten API-Oberfläche vorgesehen.  App-Entwickler sollten andere Anleitungen verwenden, um die Kompatibilität zu gewährleisten, da Komponenten, APIs und Funktionen über die Lebensdauer eines Systems hinzugefügt werden bzw. noch fehlen können. [Betriebssystemversion](https://docs.microsoft.com/windows/desktop/SysInfo/operating-system-version) ist ein besserer Ausgangspunkt für Anwendungsentwickler.

Öffnen Sie PowerShell, und verwenden Sie das Cmdlet „Get-ItemProperty“ oder das Cmdlet „Get-ComputerInfo“, um diese Eigenschaften in der Registrierung zu überprüfen.  Zusammen mit der Buildnummer macht diese Angabe LTSC oder SAC durch das Vorhandensein oder Fehlen des Markenjahres (2019) kenntlich.  LTSC enthält sie, SAC nicht.  Zusammen mit „ReleaseId“ oder „WindowsVersion“ wird auch der Zeitpunkt des Releases zurückgegeben, d.h. 1809, und die Information, ob es sich bei der Installation um Server Core oder Server mit Desktop-Benutzeroberfläche handelt. 

**Beispiel für Windows Server 2019 Datacenter Edition (LTSC) mit Desktopdarstellung :**

````PowerShell
Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows NT\CurrentVersion | Select ProductName, ReleaseId, InstallationType, CurrentMajorVersionNumber,CurrentMinorVersionNumber,CurrentBuild
````

````
ProductName               : Windows Server 2019 Datacenter
ReleaseId                 : 1809
InstallationType          : Server
CurrentMajorVersionNumber : 10
CurrentMinorVersionNumber : 0
CurrentBuild              : 17763
````

**Beispiel für Windows Server, Version 1809 (SAC), Standard Edition Server Core:**

````PowerShell
Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows NT\CurrentVersion | Select ProductName, ReleaseId, InstallationType, CurrentMajorVersionNumber,CurrentMinorVersionNumber,CurrentBuild
````

````
ProductName               : Windows Server Standard
ReleaseId                 : 1809
InstallationType          : Server Core
CurrentMajorVersionNumber : 10
CurrentMinorVersionNumber : 0
CurrentBuild              : 17763
````

**Beispiel für Windows Server 2019 Standard Edition (LTSC) Server Core:**


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

[Änderungen bei Nano Server in Windows Server Semi-Annual Channel](../get-started/nano-in-semi-annual-channel.md)

[Supportlebenszyklus für Windows Server](https://support.microsoft.com/lifecycle)

[Ermitteln, ob Server Core ausgeführt wird](https://msdn.microsoft.com/library/hh846315%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)

[GetProductInfo-Funktion](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getproductinfo)

[Cmdlets zur Protokollierung des Softwarebestands](https://docs.microsoft.com/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps)
