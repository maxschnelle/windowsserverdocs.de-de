---
title: Optimieren von Windows 10, Version 1909, für eine VDI-Rolle (Virtual Desktop Infrastructure)
description: Empfohlene Einstellungen und Konfiguration zum Minimieren des Mehraufwands für Windows 10-Desktops (Version 1909), die als VDI-Images verwendet werden.
ms.reviewer: robsmi
ms.author: helohr
ms.topic: article
author: heidilohr
manager: lizross
ms.date: 02/19/2020
ms.openlocfilehash: 2caecd2b625de8790ddd0d1ebfeeb9db24d11635
ms.sourcegitcommit: faa5db4cdba4ad2b3a65533b6b49d960080923c9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/06/2020
ms.locfileid: "91752912"
---
# <a name="optimizing-windows-10-version-1909-for-a-virtual-desktop-infrastructure-vdi-role"></a>Optimieren von Windows 10, Version 1909, für eine VDI-Rolle (Virtual Desktop Infrastructure)

Dieser Artikel hilft dir bei der Auswahl von Einstellungen für Windows 10, Version 1909 (Build 18363), die zur besten Leistung in einer VDI-Umgebung (Virtual Desktop Infrastructure) führen sollten. Alle Einstellungen in diesem Handbuch sind Empfehlungen, die berücksichtigt werden sollten, aber keine Anforderungen.

In einer VDI-Umgebung sind die wichtigsten Möglichkeiten zur Optimierung der Leistung von Windows 10, App-Grafikneuzeichnungen und Hintergrundaktivitäten, die keinen großen Nutzen für die VDI-Umgebung haben, zu minimieren und generell laufende Prozesse auf das absolute Minimum zu reduzieren. Ein sekundäres Ziel ist, den Verbrauch von Speicherplatz auf dem Datenträger im Basisimage auf ein Minimum zu reduzieren. Bei VDI-Implementierungen kann die kleinstmögliche Basisimagegröße („goldene“ Imagegröße) die Arbeitsspeicherauslastung auf dem Hypervisor leicht reduzieren und ebenso eine geringfügige Reduzierung der gesamten Netzwerkvorgänge bewirken, die erforderlich sind, um das Desktopimage für den Benutzer bereitzustellen.

> [!NOTE]
> Diese empfohlenen Einstellungen können auf andere Installationen von Windows 10 1909 angewendet werden, auch auf Installationen auf physischen oder anderen virtuellen Computern. Alle Empfehlungen in diesem Artikel sollten von Windows 10 1909 unterstützt werden.

## <a name="vdi-optimization-principles"></a>Prinzipien der VDI-Optimierung

Eine VDI-Umgebung stellt einem Computerbenutzer über ein Netzwerk eine vollständige Desktopsitzung einschließlich Anwendungen zur Verfügung. Der Netzwerkbereitstellungsmechnismus kann ein lokales Netzwerk oder das Internet sein. VDI-Umgebungen sind ein Basis-Betriebssystemimage, das dann die Grundlage für die Desktops bildet, die den Benutzern anschließend bereitgestellt werden. Es gibt verschiedene VDI-Implementierungen wie „Dauerhaft“, „Nicht dauerhaft“ und „Desktopsitzung“. Der dauerhafte Typ bewahrt Änderungen am VDI-Desktopbetriebssystem von einer Sitzung zur nächsten. Der nicht dauerhafte Typ bewahrt keine Änderungen am VDI-Desktopbetriebssystem von einer Sitzung zur nächsten. Für den Benutzer unterscheidet sich dieser Desktop kaum von anderen virtuellen oder physischen Geräten, außer dass über ein Netzwerk auf ihn zugegriffen wird.

Die Optimierungseinstellungen würden auf einem Referenzgerät durchgeführt. Eine VM ist ein idealer Ort, um das Image zu erstellen, da der Status gespeichert und Prüfpunkte sowie Sicherungen erstellt werden können. Auf der Basis-VM wird eine Standardinstallation des Betriebssystems ausgeführt. Diese Basis-VM wird dann durch Entfernen unnötiger Apps, Installieren von Windows-Updates, Installieren anderer Updates, Löschen temporärer Dateien und Anwenden von Einstellungen optimiert.

Es gibt andere Arten von VDI, z. B. Remotedesktopsitzung (RDS) und den kürzlich veröffentlichten [Windows Virtual Desktop](https://azure.microsoft.com/services/virtual-desktop/). Eine ausführliche Erläuterung dieser Technologien sprengt den Rahmen dieses Artikels. Dieser Artikel konzentriert sich auf die Einstellungen des Basisimage, ohne auf andere Faktoren in der Umgebung wie Hostoptimierung zu verweisen.

Sicherheit und Stabilität besitzen für Microsoft höchste Priorität, wenn es um Produkte und Dienste geht. Unternehmenskunden können die integrierte Windows Security nutzen, eine Suite von Diensten, die gut mit und ohne Internet funktioniert. Für VDI-Umgebungen, die nicht mit dem Internet verbunden sind, können die Sicherheitssignaturen mehrmals täglich heruntergeladen werden, da Microsoft möglicherweise mehrere Signaturupdates pro Tag veröffentlicht. Diese Signaturen können dann den VDI-VMs zur Verfügung gestellt und für die Installation während der Produktion geplant werden, und zwar unabhängig davon, ob sie dauerhaft oder nicht dauerhaft sind. Auf diese Weise ist der VM-Schutz so aktuell wie möglich.

Es gibt einige Sicherheitseinstellungen, die nicht auf VDI-Umgebungen anwendbar sind, die nicht mit dem Internet verbunden sind und daher nicht an der cloudfähigen Sicherheit teilnehmen können. Es gibt noch andere Einstellungen, die gängige Windows-Geräte nutzen können, z. B. Cloudoptionen oder den Microsoft Store. Durch das Entfernen des Zugriffs auf nicht verwendete Features werden der Speicherbedarf, die Netzwerkbandbreite und die Angriffsfläche verringert.

In Bezug auf Updates verwendet Windows 10 einen monatlichen Updatealgorithmus, sodass Clients nicht versuchen müssen, Updates auszuführen. In den meisten Fällen steuern die VDI-Administratoren den Updatevorgang durch das Herunterfahren von VMs auf der Basis eines Master- oder Goldimages. Sie entsiegeln dieses schreibgeschützte Image, patchen es, versiegeln es dann erneut und stellen es wieder in der Produktion bereit. Daher ist es nicht erforderlich, dass VDI-VMs Windows Update überprüfen. In bestimmten Fällen (z. B. bei dauerhaften VDI-VMs), finden normale Patchprozeduren nicht statt. Windows Update oder Microsoft Intune können ebenfalls verwendet werden. System Center Configuration Manager kann zum Verarbeiten von Updates und anderen Paketübermittlngen verwendet werden. Es liegt an jeder Organisation, den optimalen Ansatz zum Aktualisieren von VDI zu ermitteln.

> [!TIP]
> Ein Skript, das die in diesem Thema beschriebenen Optimierungen implementiert, sowie eine GPO-Exportdatei, die du mit **LGPO.exe** importieren kannst, sind unter [The Virtual Desktop Team](https://github.com/The-Virtual-Desktop-Team/Virtual-Desktop-Optimization-Tool) auf GitHub verfügbar.

Dieses Skript wurde für Ihre Umgebung und Ihre Anforderungen konzipiert. Der Hauptcode ist PowerShell, und die Arbeit erfolgt mithilfe von Eingabedateien (Nur-Text) und den Exportdateien des Tools des lokalen Gruppenrichtlinienobjekts (LGPO). Diese Dateien enthalten Liste mit den zu entfernenden Apps und den Diensten, die deaktiviert werden sollen. Wenn du nicht möchtest, dass eine bestimmte App entfernt oder ein bestimmter Dienst deaktiviert wird, bearbeitest du die entsprechende Textdatei und entfernst das Element. Schließlich gibt es lokale Richtlinieneinstellungen, die in Ihr Gerät importiert werden können. Es ist besser, einige Einstellungen innerhalb des Basisimages zu verwenden, anstatt die Einstellungen durch die Gruppenrichtlinie anzuwenden, da einige der Einstellungen beim nächsten Neustart wirksam werden oder wenn eine Komponente zum ersten Mal verwendet wird.

### <a name="persistent-vdi"></a>Dauerhafte VDI

Die dauerhafte VDI ist auf der Basisebene eine VM, die den Betriebssystemzustand zwischen Neustarts speichert. Andere Softwareebenen der VDI-Lösung bieten den Benutzern einen einfachen und nahtlosen Zugriff auf die ihnen zugeordneten VMs, oft mit einer Single-Sign-On-Lösung.

Es gibt mehrere verschiedene Implementierungen von dauerhafter VDI:

- Herkömmliche VMs, bei denen die VM über eine eigene virtuelle Festplattendatei verfügt, starten normal und speichern Änderungen von einer Sitzung zur nächsten. Der Unterschied besteht darin, wie der Benutzer auf diese VM zugreift. Möglicherweise gibt es ein Webportal, in dem sich der Benutzer anmeldet und das den Benutzer automatisch zu einer oder mehreren zugewiesenen VDI-VMs leitet.

- Imagebasierter dauerhafter virtueller Computer, optional mit persönlichen virtuellen Datenträgern. In dieser Art der Implementierung ist ein Basis-/Goldimage auf einem oder mehreren Hostservern vorhanden. Eine VM wird erstellt, und ein oder mehrere virtuelle Datenträger werden erstellt und dieser Festplatte zur dauerhaften Speicherung zugewiesen.

    - Wenn der virtuelle Computer gestartet wird, wird eine Kopie des Basisimages in den Arbeitsspeicher dieses virtuellen Computers gelesen. Gleichzeitig wird ein dauerhafter virtueller Datenträger dieser VM zugeordnet, wobei etwaige frühere Betriebssystemänderungen durch einen komplexen Prozess zusammengeführt wurden.

    - Änderungen wie Ereignisprotokollschreiben, Protokollschreiben usw. werden auf den virtuellen Lese-/Schreibdatenträger umgeleitet, der dieser VM zugeordnet ist.

    - Unter diesen Umständen kann die Wartung von Betriebssystem und Apps mit herkömmlicher Wartungssoftware wie Windows Server Update Services oder anderen Verwaltungstechnologien normal funktionieren.

    - Der Unterschied zwischen einem dauerhaften VDI-Computer und einem herkömmlichen virtuellen Computer ist die Beziehung zum Master- bzw. Goldimage. Zu einem bestimmten Zeitpunkt müssen Updates auf den Master angewendet werden. Die Implementierungen entscheiden nun, wie dauerhafte Änderungen des Benutzers behandelt werden. In einigen Fällen wird der Datenträger mit den Änderungen verworfen und/oder zurückgesetzt, wodurch ein neuer Prüfpunkt festgelegt wird. Es kann auch sein, dass die vom Benutzer vorgenommenen Änderungen durch monatliche Qualitätsupdates beibehalten werden, und die Basis wird nach einer Featureaktualisierung zurückgesetzt.

### <a name="non-persistent-vdi"></a>Nicht dauerhafte VDI

Wenn eine nicht dauerhafte VDI-Implementierung auf einem Basis- oder Goldimage basiert, werden die Optimierungen meist im Basisimage und dann über lokale Einstellungen und Richtlinien vorgenommen.

Bei imagebasierten, nicht dauerhaften VDIs ist das Basisimage schreibgeschützt. Wenn eine nicht dauerhafte VM gestartet wird, wird eine Kopie des Basisimages zum virtuellen Computer gestreamt. Aktivitäten, die während des Startvorgangs und danach bis zum nächsten Neustart auftreten, werden an einen temporären Speicherort umgeleitet. Normalerweise werden den Benutzern Netzwerkspeicherorte zur Verfügung gestellt, um ihre Daten zu speichern. In einigen Fällen wird das Profil des Benutzers mit der Standard-VM zusammengeführt, um dem Benutzer deren Einstellungen zur Verfügung zu stellen.

Ein wichtiger Aspekt der nicht dauerhaften VDI, die auf einem einzigen Image basiert, ist die Wartung. Updates des Betriebssystems und Komponenten werden in der Regel ein Mal pro Monat bereitgestellt. Bei der imagebasierten VDI gibt es eine Reihe von Prozessen, die durchgeführt werden müssen, um Aktualisierungen des Image zu erhalten:

- Alle VMs auf einem bestimmten Host, die vom Basisimage abgeleitet sind, müssen heruntergefahren/ausgeschaltet werden. Dies bedeutet, dass die Benutzer auf andere virtuelle Computer umgeleitet werden.

- Das Basisimage wird anschließend geöffnet und gestartet. Alle Wartungsaktivitäten wie z.B. Betriebssystemupdates, .NET-Updates, App-Updates etc. werden dann ausgeführt.

- Alle neuen Einstellungen, die angewendet werden müssen, werden zu diesem Zeitpunkt angewendet.

- Jegliche sonstige Wartung wird zu diesem Zeitpunkt durchgeführt.

- Das Basisimage wird anschließend heruntergefahren.

- Das Basisimage wird versiegelt und so eingestellt, dass es wieder in die Produktion geht.

- Benutzer können sich erneut anmelden.

> [!NOTE]
> Windows 10 führt in regelmäßigen Abständen automatisch eine Reihe von Wartungsaufgaben durch. Eine geplante Aufgabe wird standardmäßig jeden Tag um 3:00 Uhr ausgeführt. Diese geplante Aufgabe führt eine Liste von Aufgaben einschließlich der Windows Update-Bereinigung durch. Du kannst alle Kategorien der Wartung anzeigen, die automatisch mit dem folgenden PowerShell-Befehl ausgeführt werden:
>
>```powershell
>Get-ScheduledTask | Where-Object {$_.Settings.MaintenanceSettings}
>```
>

Eine der Herausforderungen bei nicht dauerhaften VDIs besteht darin, dass beim Abmelden eines Benutzers fast die gesamte Betriebssystemaktivität verworfen wird. Das Profil und/oder der Status des Benutzers können an einem zentralen Ort gespeichert werden, aber die VM selbst verwirft fast alle Änderungen, die seit dem letzten Start vorgenommen wurden. Daher sind Optimierungen, die für einen Windows-Computer bestimmt sind, der den Zustand von einer Sitzung zur nächsten speichert, nicht anwendbar.

Je nach Architektur der VDI-VM sind PreFetch, SuperFetch und Ähnliches von einer Sitzung zur nächsten nicht hilfreich, da alle Optimierungen beim VM-Neustart verworfen werden. Die Indexierung kann eine teilweise Verschwendung von Ressourcen sein, ebenso wie alle Festplattenoptimierungen, z.B. die herkömmliche Defragmentierung.

> [!NOTE]
> Wenn du ein Image mithilfe von Virtualisierung vorbereitest und während der Imageerstellung eine Verbindung mit dem Internet herstellst, solltest du Funktionsupdates bei der ersten Anmeldung aufschieben, indem du zu **Einstellungen** > **Windows Update** wechselst.

### <a name="to-sysprep-or-not-sysprep"></a>Sysprep – ja oder nein?

Windows 10 verfügt über eine integrierte Funktion, das [Systemvorbereitungstool](/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview), häufig als „Sysprep“ (System Preparation) bezeichnet. Mit dem Sysprep-Tool wird ein benutzerdefiniertes Windows 10-Image für die Duplizierung vorbereitet. Der Sysprep-Prozess stellt sicher, dass das resultierende Betriebssystem für den Einsatz in der Produktion eindeutig ist.

Es gibt Gründe, die für und gegen die Ausführung von Sysprep sprechen. Im Falle von VDI möchtest du vielleicht die Möglichkeit haben, das Standardbenutzerprofil anzupassen, das als Profilvorlage für nachfolgende Benutzer verwendet wird, die sich mit diesem Image anmelden. Möglicherweise möchtest du gern einige Apps installieren, aber auch die Möglichkeit haben, die Einstellungen pro App zu steuern.

Die Alternative ist, eine Standard-ISO-Datei für die Installation zu verwenden, möglicherweise unter Verwendung einer Antwortdatei für unbeaufsichtigte Installationen, und eine Aufgabensequenz für die Installation von Anwendungen oder deren Entfernen. Du kannst auch eine Aufgabensequenz verwenden, um lokale Richtlinieneinstellungen im Image festzulegen, vielleicht mit dem Tool [Local Group Policy Object Utility (LGPO)](/archive/blogs/secguide/lgpo-exe-local-group-policy-object-utility-v1-0) (Lokales Gruppenrichtlinienobjekt (Hilfsprogramm)).

### <a name="supportability"></a>Support-Fähigkeit

Immer, wenn Windows-Standardwerte geändert werden, entstehen Fragen bezüglich der Support-Fähigkeit. Sobald ein VDI-Image (VM oder Sitzung) angepasst wird, muss jede am Image vorgenommene Änderung in einem Änderungsprotokoll nachverfolgt werden. Bei der Problembehandlung kann ein Image häufig in einem Pool isoliert und für die Problemanalyse konfiguriert werden. Nachdem ein Problem bis zur Grundursache nachverfolgt wurde, kann diese Änderung zunächst in der Testumgebung und schließlich in der Produktionsarbeitsauslastung ausgeführt werden.

Dieses Dokument vermeidet absichtlich die Themen Systemdienste, Richtlinien oder Tasks, die sich auf die Sicherheit auswirken. Anschließend folgt die Windows-Wartung. Die Möglichkeit, VDI-Images außerhalb von Wartungsfenstern zu warten, wird entfernt, da in Wartungsfenstern die meisten Wartungsereignisse in VDI-Umgebungen stattfinden, *mit Ausnahme von Sicherheitssoftwareupdates*. Microsoft hat Richtlinien für die Windows-Sicherheit in VDI-Umgebungen veröffentlicht. Weitere Informationen findest du im [Bereitstellungsleitfaden für Windows Defender Antivirus in einer VDI-Umgebung (Virtual Desktop Infrastructure)](/windows/security/threat-protection/windows-defender-antivirus/deployment-vdi-windows-defender-antivirus).

Berücksichtige die Support-Fähigkeit, wenn du Windows-Standardeinstellungen änderst. Beim Ändern von Systemdiensten, Richtlinien oder geplanten Tasks (z. B. zur Härtung oder„Erleichterung“) können schwierige Probleme auftreten. Informationen zu den aktuellen bekannten Problemen bezüglich geänderter Standardeinstellungen findest du in der Microsoft Knowledge Base. Die Anleitungen in diesem Dokument und das zugehörige Skript auf GitHub werden im Hinblick auf bekannte Probleme (falls vorhanden) aktualisiert. Darüber hinaus kannst du Probleme auf verschiedene Weise an Microsoft melden.

Sie können Ihre bevorzugte Suchmaschine mit den Begriffen „„Startwert“ site:support.microsoft.com“ verwenden, um bekannte Probleme in Bezug auf die Standardstartwerte für Dienste anzuzeigen.

Möglicherweise wirst du feststellen, dass in diesem Dokument und den zugehörigen Skripts auf GitHub keine Standardberechtigungen geändert werden. Wenn du deine Sicherheitseinstellungen erhöhen möchten, beginnst du mit dem Projekt, das als **AaronLocker** bezeichnet wird. Weitere Informationen finden Sie in der [Übersicht über „AaronLocker“](https://github.com/microsoft/AaronLocker).

#### <a name="vdi-optimization-categories"></a>Kategorien für VDI-Optimierung

- Kategorien globaler Betriebssystemeinstellungen:

    - UWP-App-Bereinigung

    - Bereinigung optionaler Features

    - Lokale Richtlinieneinstellungen

    - Systemdienste

    - Geplante Aufgaben

    - Anwenden von Windows- und anderen Updates

    - Automatische Windows-Ablaufverfolgungen

    - Datenträgerbereinigung vor dem Finalisieren (Versiegeln) des Images

    - Benutzereinstellungen

    - Hypervisor-/Hosteinstellungen

### <a name="universal-windows-platform-uwp-application-cleanup"></a>Anwendungsbereinigung für UWP (Universelle Windows-Plattform)

Ein VDI-Image sollte unter anderem so schlank wie möglich sein. Eine Möglichkeit, die Imagegröße zu reduzieren, besteht darin, UWP-Anwendungen zu entfernen, die nicht in der Umgebung verwendet werden. Unter den UWP-Anwendungen gibt es die wichtigsten, auch als Nutzlast bezeichneten Anwendungsdateien. Im Profil jedes Benutzers ist eine kleine Menge an Daten für anwendungsspezifische Einstellungen gespeichert. Auch im Profil „Alle Benutzer“ ist eine kleine Menge an Daten vorhanden.

Konnektivität und Timing sind wichtige Faktoren, wenn es um die UWP-App-Bereinigung geht. Wenn du dein Basisimage für ein Gerät ohne Netzwerkverbindung bereitstellst, kann Windows 10 keine Verbindung mit Microsoft Store herstellen und Apps herunterladen sowie versuchen, sie zu installieren, während du versuchst, sie zu deinstallieren. Dies ist möglicherweise eine gute Strategie, um dir die Anpassung des Image zu ermöglichen und dann in einer späteren Phase zu aktualisieren, was vom Imageerstellungsprozess verbleibt.

Wenn du deine WIM-Basisdatei änderst, mit der du Windows 10 installierst, und nicht benötigte UWP-Anwendungen vor der Installation aus der WIM-Datei entfernst, werden die Apps nicht von Anfang an installiert, und deine Profilerstellungszeiten werden kürzer. Später in diesem Abschnitt findest du Informationen zum Entfernen von UWP-Apps aus deiner WIM-Installationsdatei.

Eine gute Strategie für VDI ist, die gewünschten Apps im Basisimage bereitzustellen und anschließend den Zugriff auf den Microsoft Store einzuschränken oder zu blockieren. Store-Apps werden auf normalen Computern in regelmäßigen Abständen im Hintergrund aktualisiert. Die UWP-Apps können während des Wartungsfensters aktualisiert werden, wenn andere Updates angewendet werden. Weitere Informationen findest du unter [UWP-Apps (Universelle Windows-Plattform)](https://docs.citrix.com/en-us/citrix-virtual-apps-desktops/manage-deployment/applications-manage/universal-apps.html)

#### <a name="delete-the-payload-of-uwp-apps"></a>Löschen der Nutzlast der UWP-Apps

UWP-Apps, die nicht benötigt werden, sind weiterhin im Dateisystem vorhanden und verbrauchen eine kleine Menge an Speicherplatz. Für Apps, die nie benötigt werden, kann die Nutzlast unerwünschter UWP-Apps mit PowerShell-Befehlen aus dem Basisimage entfernt werden.

Wenn du diese über die später in diesem Abschnitt angegebenen Links aus der Installations-WIM-Datei entfernst, solltest du von Anfang an mit einer sehr schlanken Liste von UWP-Apps beginnen können.

Führe den folgenden Befehl aus, um bereitgestellte UWP-Apps von einem laufenden Betriebssystem auszulisten, wie in dieser verkürzten Beispielausgabe von PowerShell:

```powershell

    Get-AppxProvisionedPackage -Online

    DisplayName  : Microsoft.3DBuilder
    Version      : 13.0.10349.0
    Architecture : neutral
    ResourceId   : \~
    PackageName  : Microsoft.3DBuilder_13.0.10349.0_neutral_\~_8wekyb3d8bbwe
    Regions      :
    ...
```

UWP-Apps, die einem System zur Verfügung gestellt werden, können während der Betriebssysteminstallation im Rahmen einer Aufgabensequenz oder später nach der Installation des Betriebssystems entfernt werden. Dies könnte die bevorzugte Methode sein, da sie den gesamten Prozess der Erstellung oder Wartung eines Images modular gestaltet. Sobald du die Skripts entwickelst, bearbeite ein bestehendes Skript, wenn sich in einem späteren Build etwas ändert, anstatt den Prozess von Grund auf zu wiederholen. Hier sind einige Links zu Informationen zu diesem Thema:

[Removing Windows 10 in-box apps during a task sequence](/archive/blogs/mniehaus/removing-windows-10-in-box-apps-during-a-task-sequence) (Entfernen von mitgelieferten Windows 10-Apps während einer Aufgabensequenz)

[Removing Built-in apps from Windows 10 WIM-File with PowerShell - Version 1.3](https://gallery.technet.microsoft.com/Removing-Built-in-apps-65dc387b) (Entfernen integrierter Apps aus der Windows 10-WIM-Datei mit PowerShell – Version 1.3)

[Windows 10 1607: Keeping apps from coming back when deploying the feature update](/archive/blogs/mniehaus/windows-10-1607-keeping-apps-from-coming-back-when-deploying-the-feature-update) (Windows 10 1607: Verhindern der Rückkehr von Apps bei der Bereitstellung des Featureupdates)

Führe dann den PowerShell-Befehl [Remove-AppxProvisionedPackage](/powershell/module/dism/remove-appxprovisionedpackage?view=win10-ps) aus, um UWP-App-Nutzlasten zu entfernen:

```powershell
Remove-AppxProvisionedPackage -Online -PackageName
```

Jede UWP-App sollte in jeder spezifischen Umgebung auf ihre Anwendbarkeit geprüft werden. Wenn du eine Standardinstallation von Windows 10 1909 durchführst, notiere dir, welche Apps ausgeführt werden und Speicher verbrauchen. Beispielsweise kannst du in Betracht ziehen, Apps zu entfernen, die automatisch starten, oder Apps, die automatisch Informationen wie z. B. Wetter und Nachrichten im Startmenü anzeigen, die in deiner Umgebung möglicherweise nicht nützlich sind.

> [!NOTE]
> Wenn du die Skripts von GitHub verwendest, kannst du leicht steuern, welche Anwendungen entfernt werden, bevor das Skript ausgeführt wird. Suchen Sie nach dem Herunterladen der Skriptdateien die Datei „AppxPackages.json“, bearbeiten Sie diese, und entfernen Sie Einträge für Apps, die Sie behalten möchten, wie den Rechner oder die Kurznotizen. Weitere Informationen finden Sie [im Abschnitt zur Anpassung](https://github.com/TheVDIGuys/Windows_10_VDI_Optimize#customization).

### <a name="manage-windows-optional-features-using-powershell"></a>Verwalten optionaler Windows-Features mit PowerShell

Du kannst optionale Windows-Features mit PowerShell verwalten. Weitere Informationen finden Sie im [Windows Server PowerShell-Forum](/answers/topics/windows-server-powershell.html). Liste die aktuell installierten Windows-Features mit folgendem PowerShell-Befehl auf:

```powershell
Get-WindowsOptionalFeature -Online
```

Du kannst ein bestimmtes optionales Windows-Feature wie im folgenden Beispiel gezeigt aktivieren oder deaktivieren:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName "DirectPlay" -All
```

Du kannst Funktionen im VDI-Image deaktivieren, wie im folgenden Beispiel gezeigt:

```powershell
Disable-WindowsOptionalFeature -Online -FeatureName "WindowsMediaPlayer"
```

Als nächstes möchtest du möglicherweise das Windows Media Player-Paket entfernen. Es gibt zwei Windows Media Player-Pakete in Windows 10 1909:

```powershell
Get-WindowsPackage -Online -PackageName *media*

PackageName       : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.1
Applicable        : True
Copyright        : Copyright (c) Microsoft Corporation. All Rights Reserved
Company         :
CreationTime       :
Description       : Play audio and video files on your local device and on the Internet.
InstallClient      : DISM Package Manager Provider
InstallPackageName    : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.1.mum
InstallTime       : 3/19/2019 6:20:22 AM
...

Features         : {}

PackageName       : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.449
Applicable        : True
Copyright        : Copyright (c) Microsoft Corporation. All Rights Reserved
Company         :
CreationTime       :
Description       : Play audio and video files on your local device and on the Internet.
InstallClient      : UpdateAgentLCU
InstallPackageName    : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.449.mum
InstallTime       : 10/29/2019 5:15:17 AM
...
```

Wenn du das Windows Media Player-Paket entfernen möchtest (um ungefähr 60 MB Speicherplatz auf dem Datenträger freizugeben):

```powershell
 Remove-WindowsPackage -PackageName Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.1 -Online

 Remove-WindowsPackage -PackageName Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.449 -Online
```

#### <a name="enable-or-disable-windows-features-using-dism"></a>Aktivieren oder Deaktivieren von Windows-Features mithilfe von DISM

Mit dem integrierten Tool „Dism.exe“ kannst du optionale Windows-Features auflisten und steuern. Bei einer Tasksequenz zur Installation des Betriebssystems kann ein Skript „Dism.exe“ entwickelt und ausgeführt werden. Die entsprechende Windows-Technologie wird als [Features bei Bedarf](/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities) bezeichnet.

#### <a name="default-user-settings"></a>Standardbenutzereinstellungen

An der Windows-Registrierungsdatei „C:\Benutzer\Default\NTUSER.DAT“ können Anpassungen vorgenommen werden. Alle an dieser Datei vorgenommenen Einstellungen werden auf alle nachfolgenden Benutzerprofile angewendet, die von einem Gerät erstellt werden, auf dem dieses Image ausgeführt wird. Sie können steuern, welche Einstellungen auf das Standardbenutzerprofil angewendet werden sollen, indem Sie die Datei „DefaultUserSettings.txt“ bearbeiten. Eine Einstellung, die du möglicherweise in Erwägung ziehen möchtest, ist eine Einstellung namens **TaskbarSmallIcons**, die in diesen Einstellungsempfehlungen neu ist. Du solltest dich vor der Implementierung dieser Einstellung ggf. mit deiner Benutzerbasis abstimmen. **TaskbarSmallIcons** verkleinert die Windows-Taskleiste und verbraucht weniger Bildschirmfläche, die Symbole werden kompakter, und die Suchschnittstelle wird minimiert. In den folgenden Abbildungen wird das Aussehen vor und nach der Anwendung dargestellt:

Abbildung 1: Normale Taskleiste von Windows 10, Version 1909

![Standardversion der Taskleiste von Windows  10, Version 1909](media/rds-vdi-recommendations-1909/standard-taskbar.png)

Abbildung 2: Taskleiste mit der Einstellung für kleine Symbole

![Taskleiste mit der Einstellung für kleine Symbole](media/rds-vdi-recommendations-1909/taskbar-sm-icons.png)

Um die Übertragung von Bildern über die VDI-Infrastruktur zu reduzieren, kannst du den Standardhintergrund auf eine Volltonfarbe anstatt auf das Windows 10-Standardbild festlegen. Du kannst auch den Anmeldebildschirm auf eine Volltonfarbe festlegen und den nicht transparenten Effekt bei der Anmeldung deaktivieren.

Die folgenden Einstellungen werden auf die standardmäßige Benutzerprofilregistrierungsstruktur angewendet, hauptsächlich, um Animationen zu verringern. Wenn einige oder alle dieser Einstellungen nicht gewünscht werden, löscht du die Einstellungen, die auf der Grundlage dieses Images nicht auf die neuen Benutzerprofile angewendet werden sollen. Das Ziel dieser Einstellungen besteht darin, die folgenden äquivalenten Einstellungen zu aktivieren:

Abbildung 3: Optimierte Systemeigenschaften, Leistungsoptionen

![Optimierte Systemeigenschaften, Leistungsoptionen](media/rds-vdi-recommendations-1909/performance-options.png)

Nachfolgend aufgeführt sind die Optimierungseinstellungen für Windows 10, Version 1909, die zur Leistungsoptimierung auf die Registrierungsstruktur des Profils „Standardbenutzer“ angewendet werden.

```dos
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer" /v ShellState /t REG_BINARY /d 240000003C2800000000000000000000 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v IconsOnly /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v ListviewAlphaSelect /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v ListviewShadow /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v ShowCompColor /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v ShowInfoTip /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v TaskbarAnimations /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects" /v VisualFXSetting /t REG_DWORD /d 3 /f
add "HKLM\Temp\Software\Microsoft\Windows\DWM" /v EnableAeroPeek /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\DWM" /v AlwaysHiberNateThumbnails /t REG_DWORD /d 0 /f
add "HKLM\Temp\Control Panel\Desktop" /v DragFullWindows /t REG_SZ /d 0 /f
add "HKLM\Temp\Control Panel\Desktop" /v FontSmoothing /t REG_SZ /d 2 /f
add "HKLM\Temp\Control Panel\Desktop" /v UserPreferencesMask /t REG_BINARY /d 9032078010000000 /f
add "HKLM\Temp\Control Panel\Desktop\WindowMetrics" /v MinAnimate /t REG_SZ /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\StorageSense\Parameters\StoragePolicy" /v 01 /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" /v SubscribedContent-338393Enabled /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" /v SubscribedContent-353694Enabled /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" /v SubscribedContent-353696Enabled /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" /v SubscribedContent-338388Enabled /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" /v SubscribedContent-338389Enabled /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" /v SystemPaneSuggestionsEnabled /t REG_DWORD /d 0 /f
add "HKLM\Temp\Control Panel\International\User Profile" /v HttpAcceptLanguageOptOut /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\BackgroundAccessApplications\Microsoft.Windows.Photos_8wekyb3d8bbwe" /v Disabled /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\BackgroundAccessApplications\Microsoft.Windows.Photos_8wekyb3d8bbwe" /v DisabledByUser /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\BackgroundAccessApplications\Microsoft.SkypeApp_kzf8qxf38zg5c" /v Disabled /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\BackgroundAccessApplications\Microsoft.SkypeApp_kzf8qxf38zg5c" /v DisabledByUser /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\BackgroundAccessApplications\Microsoft.YourPhone_8wekyb3d8bbwe" /v Disabled /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\BackgroundAccessApplications\Microsoft.YourPhone_8wekyb3d8bbwe" /v DisabledByUser /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\BackgroundAccessApplications\Microsoft.MicrosoftEdge_8wekyb3d8bbwe" /v Disabled /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\BackgroundAccessApplications\Microsoft.MicrosoftEdge_8wekyb3d8bbwe" /v DisabledByUser /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\BackgroundAccessApplications\Microsoft.PPIProjection_cw5n1h2txyewy" /v Disabled /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\BackgroundAccessApplications\Microsoft.PPIProjection_cw5n1h2txyewy" /v DisabledByUser /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\InputPersonalization" /v RestrictImplicitInkCollection /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\InputPersonalization" /v RestrictImplicitTextCollection /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Personalization\Settings" /v AcceptedPrivacyPolicy /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\InputPersonalization\TrainedDataStore" /v HarvestContacts /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\UserProfileEngagement" /v ScoobeSystemSettingEnabled /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\UserProfileEngagement" /v ScoobeSystemSettingEnabled /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\UserProfileEngagement" /v ScoobeSystemSettingEnabled /t REG_DWORD /d 0 /f
add "HKCU\Software\Microsoft\InputPersonalization" /v RestrictImplicitInkCollection /t REG_DWORD /d 1 /f
add "HKCU\Software\Microsoft\InputPersonalization" /v RestrictImplicitTextCollection /t REG_DWORD /d 1 /f
```

In den lokalen Richtlinieneinstellungen möchtest du möglicherweise Bilder für Hintergründe in VDI deaktivieren. Wenn du Bilder verwenden möchtest, kannst du benutzerdefinierte Hintergrundbilder mit reduzierter Farbtiefe erstellen, um die Netzwerkbandbreite für die Übertragung von Bildinformationen einzuschränken. Wenn du in der lokalen Richtlinie kein Hintergrundbild angeben möchtest, solltest du vor dem Festlegen der lokalen Richtlinie die Hintergrundfarbe festlegen, da der Benutzer nach dem Festlegen der Richtlinie keine Möglichkeit mehr hat, die Hintergrundfarbe zu ändern. Es ist möglicherweise besser, „(NULL)“ als Hintergrundbild anzugeben. Im nächsten Abschnitt findest du eine weitere Richtlinieneinstellung, in der der Hintergrund in Remotedesktopprotokoll-Sitzungen nicht verwendet wird.

### <a name="local-policy-settings"></a>Lokale Richtlinieneinstellungen

Zahlreiche Optimierungen für Windows 10 in einer VDI-Umgebung können mit einer Windows-Richtlinie vorgenommen werden. Die in der Tabelle in diesem Abschnitt aufgeführten Einstellungen können lokal auf das Basis-/Goldimage angewendet werden. Wenn die entsprechenden Einstellungen nicht auf andere Weise (z. B. durch eine Gruppenrichtlinie) angegeben werden, würden die Einstellungen weiterhin gelten.

Einige Entscheidungen können auf Besonderheiten der Umgebung basieren, z. B.:

- Darf die VDI-Umgebung auf das Internet zugreifen?

- Ist die VDI-Lösung dauerhaft oder nicht dauerhaft?

Die folgenden Einstellungen wurden ausgewählt, weil sie nicht mit einer Einstellung in Konflikt stehen, die etwas mit der Sicherheit zu tun hat. Diese Einstellungen wurden ausgewählt, um Einstellungen zu entfernen oder Funktionen zu deaktivieren, die möglicherweise nicht auf VDI-Umgebungen anwendbar sind.

| Richtlinieneinstellung | Element | Untergeordnete Element | Mögliche Einstellung und Kommentare|
| -------------- | ---- | -------- | ---------------------------- |
| Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Windows-Einstellungen \\ Sicherheitseinstellungen | | | |
| Netzwerklisten-Manager-Richtlinien | Alle Netzwerkeeigenschaften | Netzwerkadresse | Benutzer kann Adresse nicht ändern |
| Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Systemsteuerung | | | |
| *Systemsteuerung | Onlinetipps zulassen | | Deaktiviert. „Einstellungen“ kontaktiert nicht die Inhaltsdienste von Microsoft zum Abrufen von Tipps und hilfreichen Informationen. |
| *Systemsteuerung\Personalisierung | Der Sperrbildschirm wird nicht angezeigt. | Aktiviert. Diese Einstellung steuert, ob der Sperrbildschirm für Benutzer angezeigt wird. Wenn du diese Richtlinieneinstellung aktivierst, wird Benutzern, die vor der Anmeldung nicht STRG+ALT+ENTF drücken müssen, nach Sperren ihres PCs ihre ausgewählte Kachel angezeigt. |
| *Systemsteuerung\Personalisierung | Ein bestimmtes Standardbild für den Sperr- und Anmeldebildschirm erzwingen | [![Benutzeroberfläche zum Festlegen des Pfads zum Sperrbildschirm](media/lock-screen-image-settings.png)](media/lock-screen-image-settings.png) | Aktiviert. Mit dieser Einstellung kannst du den Standardsperrbildschirm und das Anmeldungsbild angeben, das angezeigt wird, wenn kein Benutzer angemeldet ist, und außerdem legt sie das angegebene Bild als Standard für alle Benutzer fest – es ersetzt das Standardbild.<p>Es wird empfohlen, ein einfaches Bild mit niedriger Auflösung zu verwenden, damit bei jedem Rendern weniger Daten über das Netzwerk übertragen werden. |
| *Systemsteuerung\Regions- und Sprachoptionen\Handschriftanpassung | Automatisches Lernen deaktivieren | | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, wird automatisches Lernen beendet, und alle gespeicherten Daten werden gelöscht. Benutzer können diese Einstellung nicht in der Systemsteuerung konfigurieren. |
| Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Netzwerk | | | |
| Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS) | Verwendung des Windows Branch-Caches durch BITS-Client nicht zulassen |  | Enabled |
| Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS) | Computer darf nicht als BITS-Peercachingclient fungieren |  | Enabled |
| Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS) | Computer darf nicht als BITS-Peercachingserver fungieren |  | Enabled |
| Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS) | BITS-Peercaching zulassen |  | Deaktiviert |
| BranchCache | BranchCache aktivieren |  | Deaktiviert |
| *Schriftarten | Schriftartenanbieter aktivieren |  | Deaktiviert. Windows stellt keine Verbindung mit einem Onlineschriftanbieter her und listet nur lokal installierte Schriftarten auf. |
| Hotspotauthentifizierung | Hotspotauthentifizierung aktivieren |  | Deaktiviert |
| Microsoft Peer-zu-Peer-Netzwerkdienste | Microsoft Peer-zu-Peer-Netzwerkdienste deaktivieren |  | Enabled |
| Netzwerkverbindungs-Statusanzeige | Passive Abrufe angeben. | Passive Abrufe deaktivieren (Kontrollkästchen) | Aktiviert. Verwende diese Einstellung in einem isolierten Netzwerk oder wenn du eine statische IP-Adresse verwendest. |
| Offlinedateien | Offlinedateien zulassen bzw. nicht zulassen. |  | Deaktiviert |
| TCPIP-Einstellungen \\ IPv6-Übergangstechnologien | Teredo-Status festlegen | Deaktivierter Zustand | Aktiviert. Im deaktivierten Zustand sind auf dem Host keine Teredo-Schnittstellen vorhanden. |
| WLAN-Dienst \\ WLAN-Einstellungen | Zulassen, dass Windows automatisch Verbindungen mit vorgeschlagenen öffentlichen Hotspots, mit Netzwerken, die von Kontakten gemeinsam genutzt werden und mit Hotspots herstellt, die kostenpflichtige Dienste anbieten. |  | Deaktiviert. Die Optionen **Mit vorgeschlagenen öffentlichen Hotspots verbinden**, **Mit den von meinen Kontakten freigegebenen Netzen verbinden** und **Kostenpflichtige Dienste aktivieren** werden deaktiviert, Benutzer dieses Geräts können sie jedoch aktivieren. |
| Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Startmenü und Taskleiste |  |  |  |
| *Benachrichtigungen | Netzwerkverwendung für Benachrichtigungen deaktivieren |  | Aktiviert. Wenn du diese Einstellung aktivierst, können Apps und Systemfunktionen keine Benachrichtigungen von WNS über das Netzwerk oder mit Benachrichtigungen abfragenden APIs empfangen. |
| Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ System |  |  |  |
| Geräteinstallation | Keinen Windows-Fehlerbericht senden, wenn ein Standardtreiber für ein Gerät installiert ist |  | Enabled |
| Geräteinstallation | Bei der Installation eines neuen Gerätetreibers keinen Systemwiederherstellungspunkt erstellen. |  | Enabled |
| Geräteinstallation | Abrufen von Gerätemetadaten aus dem Internet verhindern |  | Enabled |
| Geräteinstallation | Verhindern, dass ein Fehlerbericht gesendet wird, wenn ein Gerätetreiber während der Installation zusätzliche Software anfordert |  | Enabled |
| Geräteinstallation | Sprechblasen mit der Meldung **Neue Hardware gefunden** während der Geräteinstallation deaktivieren. |  | Enabled |
| Dateisystem \\ NTFS | Optionen für die Erstellung von Kurznamen | Für alle Volumes deaktiviert | Enabled |
| *Gruppenrichtlinie | Konfigurieren der Verknüpfung zwischen Web und App mit App-URI-Handlern |  | Deaktiviert. Deaktiviert die Verknüpfung zwischen Web und App und HTTP(S). URIs werden im Standardbrowser geöffnet, anstatt die zugehörige App zu starten. |
| *Gruppenrichtlinie | Auf der Oberfläche dieses Geräts weiterarbeiten. |  | Deaktiviert. Das Windows-Gerät ist für andere Geräte nicht erkennbar und wird nicht in geräteübergreifende Oberflächen einbezogen. |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Zugriff auf alle Windows Update-Features deaktivieren |  |Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, werden alle Windows Update-Funktionen entfernt. Dazu gehört das Blockieren des Zugriffs auf die Windows Update-Website unter https://windowsupdate.microsoft.com, über den Windows Update-Hyperlink im Startmenü und auch das Menü „Extras“ im Internet Explorer. Die automatische Aktualisierung von Windows ist ebenfalls deaktiviert. Du wirst weder benachrichtigt, noch erhältst du wichtige Updates von Windows Update. Diese Richtlinieneinstellung verhindert auch, dass der Geräte-Manager automatisch Treiberupdates von der Windows Update-Website installiert. |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Automatisches Update von Stammzertifikaten deaktivieren |  |Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, und dir wird ein Zertifikat angezeigt, das nicht von einer vertrauenswürdigen Stammzertifizierungsstelle ausgestellt wurde, nimmt dein Computer keinen Kontakt mit der Windows Update-Website auf, um festzustellen, ob Microsoft die Zertifizierungsstelle seiner Liste vertrauenswürdiger Zertifizierungsstellen hinzugefügt hat. HINWEIS: Verwende diese Richtlinie nur, wenn du über eine Alternative zur neuesten Zertifikatssperrliste verfügst. |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Events.asp-Links der Ereignisanzeige deaktivieren |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Freigabe von Daten für die Handschriftanpassung deaktivieren |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Handschrifterkennungs-Fehlerberichterstattung deaktivieren |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | „Wussten Sie schon?“-Inhalte im Hilfe- und Supportcenter deaktivieren Inhalt |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Knowledge Base-Suche des Hilfe- und Supportcenters deaktivieren |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Verbindungs-Assistenten deaktivieren, wenn sich die URL-Verbindung auf Microsoft.com bezieht |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Internet-Download für die Assistenten „Webpublishing“ und „Onlinebestellung von Abzügen“ deaktivieren |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Internet-Dateizuordnungsdienst deaktivieren |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Registrierung deaktivieren, wenn sich die URL-Verbindung auf „Microsoft.com“ bezieht |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Aufgabe „Abzüge online bestellen“ für Bilder deaktivieren |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Aufgabe „Im Web veröffentlichen“ für Dateien und Ordner deaktivieren |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Programm zur Verbesserung der Benutzerfreundlichkeit deaktivieren |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Programm zur Verbesserung der Benutzerfreundlichkeit von Windows deaktivieren |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Aktive Tests der Windows-Netzwerkverbindungs-Statusanzeige deaktivieren |  | Aktiviert. Diese Richtlinieneinstellung deaktiviert die aktiven Tests, die von der Windows-Netzwerkverbindungs-Statusanzeige (Windows Network Connectivity Status Indicator, NCSI) durchgeführt werden, um festzustellen, ob dein Computer mit dem Internet oder einem eingeschränkteren Netzwerk verbunden ist. Als Teil der Bestimmung der Verbindungsebene führt der NCSI einen von zwei aktiven Tests durch: Herunterladen einer Seite von einem dedizierten Webserver oder Erstellen einer DNS-Anfrage nach einer dedizierten Adresse. Wenn du diese Richtlinieneinstellung aktivierst, wird einer der beiden aktiven Tests nicht vom NCSI ausgeführt. Dies könnte die Fähigkeit des NCSI und anderer Komponenten, die NCSI verwenden, zur Bestimmung des Internetzugriffs einschränken) HINWEIS: Es gibt andere Richtlinien, die dir ermöglichen, NCSI-Tests auf interne Ressourcen umzuleiten, wenn diese Funktionalität gewünscht wird. |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Fehlerberichterstattung deaktivieren |  | Enabled |
| Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen | Suche nach Gerätetreibern auf Windows Update deaktivieren |  | Enabled |
| Anmelden | Bei der ersten Anmeldung Animation abspielen |  | Deaktiviert |
| Anmelden | Anwendungsbenachrichtigungen auf gesperrtem Bildschirm deaktivieren |  | Enabled |
| Anmelden | Windows-Startsound deaktivieren |  | Enabled |
| Energieverwaltung | Aktiven Energiesparplan auswählen | Hohe Leistung | Enabled |
| Wiederherstellung | Systemwiederherstellung in Standardzustand zulassen |  | Deaktiviert |
| *Speicherintegrität | Herunterladen von Updates auf das Datenträgerfehlermodell ermöglichen |  | Deaktiviert. Updates würden für das Datenträgerfehlermodell nicht heruntergeladen. |
| *Windows-Zeitdienste \\ Zeitanbieter | Windows-NTP-Client aktivieren |  | Deaktiviert. Wenn du diese Richtlinieneinstellung deaktivierst oder nicht konfigurierst, wird die Zeit der Uhr des lokalen Computers nicht mit NTP-Servern synchronisiert. HINWEIS: Überlege dir diese Einstellung sehr sorgfältig. Windows-Geräte, die mit einer Domäne verbunden sind, sollten **NT5DS** verwenden. Für die Verbindung eines DC mit dem DC der übergeordneten Domäne könnte NTP verwendet werden. Die PDCe-Rolle könnte NTP verwenden. Virtuelle Computer verwenden manchmal Erweiterungen oder Integrationsdienste. |
| Problembehandlung und Diagnose \\ Geplante Wartung | Verhalten für geplante Wartung konfigurieren |   | Deaktiviert |
| Problembehandlung und Diagnose \\ Windows-Startleistungsdiagnose | Szenarioausführungsebene konfigurieren |   | Deaktiviert |
| Problembehandlung und Diagnose \\ Windows-Arbeitsspeicherverlust-Diagnose | Szenarioausführungsebene konfigurieren |   | Deaktiviert |
| Problembehandlung und Diagnose \\ Windows-Ressourcenauslastungserkennung und -Konfliktlösung | Szenarioausführungsebene konfigurieren |   | Deaktiviert |
| Problembehandlung und Diagnose \\ Windows-Leistungsdiagnose beim Herunterfahren | Szenarioausführungsebene konfigurieren |   | Deaktiviert |
| Problembehandlung und Diagnose \\ Diagnose für Windows-Standby-/Wiederaufnahmeleistung | Szenarioausführungsebene konfigurieren |   | Deaktiviert |
| Problembehandlung und Diagnose \\ Diagnose der Leistung für Windows-Systemreaktionszeit | Szenarioausführungsebene konfigurieren |   | Deaktiviert |
| *Benutzerprofile | Werbe-ID deaktivieren |   | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, wird die Werbe-ID deaktiviert. Apps können die ID nicht für Benutzeroberflächen in verschiedenen Apps verwenden. |
| Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Windows-Komponenten |  |  |  |
| Features zu Windows 10 hinzufügen | Ausführung des Assistenten verhindern |  | Enabled |
| *App-Datenschutz | Ausführung des Assistenten verhindern |  | Enabled |
| *App-Datenschutz | Windows-App-Zugriff auf Kontoinformationen zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf Kontoinformationen zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf die Anrufliste zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf die Anrufliste zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf Kontakte zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf Kontakte zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf Diagnoseinformationen anderer Apps zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du diese Richtlinieneinstellung deaktivierst oder nicht konfigurierst, können Mitarbeiter in deiner Organisation über „Einstellungen“ > „Datenschutz“ auf dem Gerät festlegen, ob Windows-Apps Diagnoseinformationen über andere Apps erhalten können. |
| *App-Datenschutz | Windows-App-Zugriff auf E-Mails zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Zulassen erzwingen** auswählst, dürfen Windows-Apps auf E-Mails zugreifen, und Mitarbeiter in deinem Unternehmen können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf Standort zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** ausgewählt hast, dürfen Windows-Apps nicht auf den Speicherort zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf Nachrichten zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** ausgewählt hast, dürfen Windows-Apps nicht auf Messaging zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf Bewegungsdaten zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf Bewegungsdaten zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf Benachrichtigungen zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** ausgewählt hast, dürfen Windows-Apps nicht auf Benachrichtigungen zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf Aufgaben zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf Aufgaben zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf Kalender zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** ausgewählt hast, dürfen Windows-Apps nicht auf den Kalender zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf Kamera zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** ausgewählt hast, dürfen Windows-Apps nicht auf die Kamera zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf Mikrofon zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** ausgewählt hast, dürfen Windows-Apps nicht auf das Mikrofon zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf vertrauenswürdige Geräte zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** ausgewählt hast, dürfen Windows-Apps nicht auf vertrauenswürdige Geräte zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Kommunizieren von Windows-Apps mit entkoppelten Geräten zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** ausgewählt hast, dürfen Windows-Apps nicht mit entkoppelten drahtlosen Geräten kommunizieren, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-App-Zugriff auf Radios zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf die Steuerung von Radios zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Windows-Apps Telefonanrufe gestatten | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** ausgewählt hast, dürfen Windows-Apps keine Anrufe ausführen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| *App-Datenschutz | Ausführung von Windows-Apps im Hintergrund zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert. Wenn du die Option **Verweigern erzwingen** ausgewählt hast, dürfen Windows-Apps keine Anrufe ausführen, und Mitarbeiter in deiner Organisation können dies nicht ändern. |
| Richtlinien für die automatische Wiedergabe | Standardverhalten von AutoAusführen festlegen | Keine AutoAusführen-Befehle ausführen | Enabled |
| *Richtlinien für die automatische Wiedergabe | Automatische Wiedergabe deaktivieren |   | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, ist die automatische Wiedergabe auf CD-ROM und Wechselmedienlaufwerken oder auf allen Laufwerken deaktiviert. |
| *Cloudinhalt | Windows-Tipps nicht anzeigen | Aktiviert. Diese Richtlinieneinstellung verhindert, dass Windows-Tipps für Benutzer angezeigt werden. |
| *Cloudinhalt | Microsoft-Anwenderfeatures deaktivieren | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, werden Benutzer keine personalisierten Empfehlungen von Microsoft und keine Benachrichtigungen über ihr Microsoft-Konto mehr angezeigt. |
| *Datenerfassung und Vorabversionen | Telemetrie zulassen | 0 – Sicherheit [nur Enterprise] | Aktiviert. Der Wert 0 kann nur für Geräte festgelegt werden, auf denen die Enterprise-, Education, IoT- oder Windows Server-Editionen ausgeführt werden. |
| *Datenerfassung und Vorabversionen | Feedbackbenachrichtigungen nicht mehr anzeigen |  | Enabled |
| *Datenerfassung und Vorabversionen | Benutzersteuerung für Insider-Builds umstellen  |  | Deaktiviert |
| Übermittlungsoptimierung | Downloadmodus | Downloadmodus: Einfach (99) | 99 = Einfacher Downloadmodus ohne Peering. Die Übermittlungsoptimierung lädt ausschließlich über HTTP herunter und versucht nicht, die Übermittlungsoptimierungs-Cloud-Dienste zu kontaktieren. |
| Desktopfenster-Manager |  Aufruf von Flip-3D nicht zulassen |  | Enabled |
| Desktopfenster-Manager |  Fensteranimationen nicht zulassen |  | Enabled |
| Desktopfenster-Manager |  Volltonfarbe für Starthintergrund verwenden |  | Enabled |
| Rand-UI |  Wischen vom Bildschirmrand zulassen |  | Deaktiviert |
| Rand-UI |  Hilfetipps deaktivieren |  | Enabled |
| Rand-UI | Nachverfolgung der App-Nutzung deaktivieren |  | Enabled |
| *Datei-Explorer |  Windows Defender SmartScreen konfigurieren |  | Deaktiviert. SmartScreen wird für alle Benutzer deaktiviert. Benutzer werden nicht gewarnt, wenn sie versuchen, verdächtige Apps aus dem Internet auszuführen. HINWEIS: Wenn keine Verbindung mit dem Internet besteht, wird so verhindert, dass die Computer versuchen, Microsoft wegen SmartScreen-Informationen zu kontaktieren. |
| Datei-Explorer |  Benachrichtigung **Neue Anwendung installiert** nicht anzeigen |  | Enabled |
| *Mein Gerät suchen |  „Mein Gerät suchen“ aktivieren/deaktivieren |  | Deaktiviert. Wenn „Mein Gerät suchen“ ausgeschaltet ist, werden das Gerät und sein Standort nicht registriert und die Funktion „Mein Gerät suchen“ funktioniert nicht. Der Benutzer kann auf seinem Gerät auch nicht den Ort sehen, an dem sein aktives Digitalisierungsgerät zuletzt genutzt wurde. |
| Datei-Explorer | Zwischenspeicherung von Bildern in Miniaturansicht deaktivieren |  | Enabled |
| Datei-Explorer | Anzeige der letzten Sucheinträge im Datei-Explorer-Suchfeld deaktivieren |  | Enabled |
| Datei-Explorer | Zwischenspeicherung von Miniaturansichten in versteckten thumbs.db-Dateien deaktivieren |  | Enabled |
| Spiel-Explorer | Herunterladen von Spielinformationen deaktivieren |  | Enabled |
| Spiel-Explorer | Spielupdates deaktivieren |  | Enabled |
| Spiel-Explorer | Ablaufverfolgung der letzten Spielzeiten im Ordner „Spiele“ deaktivieren |  | Enabled |
| Heimnetzgruppe | Beitritt des Computers zu einer Heimnetzgruppe verhindern |  | Enabled |
| *Internet Explorer | Für Microsoft-Dienste das Bereitstellen von erweiterten Vorschlägen zulassen, wenn Benutzer Text in die Adressleiste eingeben |  | Deaktiviert. Benutzern werden keine erweiterten Vorschläge angezeigt, sobald sie Text in die Adressleiste eingeben. Außerdem können Benutzer die Einstellung „Vorschläge“ nicht ändern. |
| Internet Explorer | Periodische Überprüfungen auf Internet Explorer-Softwareupdates deaktivieren |  | Enabled |
| Internet Explorer | Anzeigen des Begrüßungsbildschirms deaktivieren |  | Enabled |
| Internet Explorer | Automatisch neue Versionen von Internet Explorer installieren |  | Deaktiviert |
| Internet Explorer | Teilnahme am Programm zur Verbesserung der Benutzerfreundlichkeit verhindern |  | Enabled |
| Internet Explorer | Ausführen des Anpassungs-Assistenten verhindern | Direkt zur Startseite wechseln | Enabled |
| Internet Explorer | Zunahme von Registerkartenprozess festlegen | Low (Niedrig) | Enabled |
| Internet Explorer | Standardverhalten für eine neue Registerkarte festlegen | Neue Registerkartenseite | Enabled |
| Internet Explorer | Benachrichtigungen zur Add-On-Leistung deaktivieren |  | Enabled |
| *Internet Explorer | AutoVervollständigen für Webadressen deaktivieren |  | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, werden dem Benutzer bei der Eingabe von Webadressen keine Übereinstimmungen vorgeschlagen. Der Benutzer kann die automatische Vervollständigung für das Festlegen von Webadressen nicht ändern. |
| *Internet Explorer | Browser-Geolocation deaktivieren |  | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, ist die Geolocationunterstützung im Browser deaktiviert. |
| *Internet Explorer | Erneutes Öffnen der letzten Browsersitzung deaktivieren |  | Enabled |
| Internet Explorer | Erneutes Öffnen der letzten Browsersitzung deaktivieren |  | Enabled |
| *Internet Explorer | „Vorgeschlagene Sites“ aktivieren |  | Deaktiviert. Wenn du diese Richtlinieneinstellung deaktivierst, werden die mit dieser Funktion verbundenen Einstiegspunkte und Funktionen deaktiviert. |
| *Internet Explorer \\ Kompatibilitätsansicht | Kompatibilitätsansicht deaktivieren |  | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, kann der Benutzer weder die Schaltfläche „Kompatibilitätsansicht“ verwenden noch die Liste der Kompatibilitätsansicht-Websites verwalten. |
| *Internet Explorer \\ Internetsystemsteuerung \\ Seite „Erweitert“ | Animationen in Webseiten wiedergeben |  | Deaktiviert |
| *Internet Explorer \\ Internetsystemsteuerung \\ Seite „Erweitert“ | Videos in Webseiten wiedergeben |  | Deaktiviert |
| *Internet Explorer \\ Internetsystemsteuerung \\ Seite „Erweitert“ | Vorblättern mit Seitenvorhersage deaktivieren |  | Aktiviert. Microsoft zeichnet Ihren Browserverlauf auf, um die Funktionsweise des Vorblätterns mit Seitenvorhersage zu verbessern. Dieses Feature ist für Internet Explorer nicht für den Desktop verfügbar. Wenn du diese Richtlinieneinstellung aktivierst, ist das Vorblättern mit Seitenvorhersage deaktiviert, und die nächste Webseite wird nicht im Hintergrund geladen. |
| InternetExplorer \\ Interneteinstellungen \\ Erweiterte Einstellungen \\ Browsen | Finden von Telefonnummern deaktivieren |  | Enabled |
| *Speicherort und Sensoren | Speicherort deaktivieren |  | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, wird die Speicherortfunktion deaktiviert, und alle Programme auf diesem Computer werden daran gehindert, Speicherortinformationen aus der Speicherortfunktion zu verwenden. |
| Speicherort und Sensoren | Sensoren deaktivieren |  | Enabled |
| Speicherorte und Sensoren \\ Windows-Positionssuche | Windows-Positionssuche deaktivieren |  | Enabled |
| *Karten | Automatische Downloads und Updates von Kartendaten deaktivieren |  | Aktiviert. Wenn du diese Einstellung aktivierst, wird das automatische Herunterladen und Aktualisieren von Kartendaten deaktiviert. |
| *Karten | Nicht angeforderten Netzwerk-Datenverkehr auf der Einstellungsseite „Offlinekarten“ deaktivieren |  | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, werden Funktionen, die Netzwerkdatenverkehr auf der Einstellungsseite „Offlinekarten“ erzeugen, deaktiviert. Hinweis: Dies könnte die gesamte Einstellungsseite deaktivieren. |
| *Messaging | Synchronisierung des Nachrichtendiensts mit der Cloud zulassen |  | Deaktiviert. Diese Richtlinieneinstellung ermöglicht das Sichern und Wiederherstellen von SMS an die Microsoft-Clouddienste. |
| *Microsoft Edge | Vorschläge in Dropdownliste der Adressleiste zulassen |  | Deaktiviert |
| *Microsoft Edge | Konfigurationsupdates für die Bibliothek zulassen |  | Deaktiviert. Deaktiviert die Kompatibilitätslisten in Microsoft Edge. |
| *Microsoft Edge | Microsoft-Kompatibilitätsliste zulassen |  | Deaktiviert. Wenn du diese Einstellung deaktivierst, wird die Microsoft-Kompatibilitätsliste während der Browsernavigation nicht verwendet. |
| *Microsoft Edge | Webinhalte auf der Seite „Neuer Tab“ zulassen |  | Deaktiviert. Weist Microsoft Edge an, eine neue Registerkarte ohne Inhalt zu öffnen. |
| *Microsoft Edge | AutoAusfüllen konfigurieren |  | Deaktiviert. Deaktiviert automatisches Ausfüllen der Adressleiste. |
| *Microsoft Edge | DNT konfigurieren |  | Aktiviert. Wenn Sie diese Einstellung aktivieren, werden Do Not Track-Anforderungen (nicht verfolgen) immer an Websites gesendet, die Nachverfolgungsinformationen anfordern. |
| *Microsoft Edge | Kennwort-Manager konfigurieren |  | Deaktiviert. Wenn du diese Einstellung deaktivierst, können Mitarbeiter mithilfe des Kennwort-Managers ihr Kennwort nicht lokal speichern. |
| *Microsoft Edge | Suchvorschläge in Adressleiste konfigurieren |  | Deaktiviert. Benutzer sehen keine Suchvorschläge in der Adressleiste von Microsoft Edge. |
| *Microsoft Edge | Startseiten konfigurieren |  | Aktiviert. Wenn du diese Einstellung aktivierst, kannst du mindestens eine Startseite konfigurieren. Ist diese Einstellung aktiviert, musst du den Seiten auch URLs hinzufügen. Trenne dabei mehrere Seiten durch spitze Klammern, und verwende folgendes Format: <support.contoso.com><support.microsoft.com> Windows 10, Version 1703 oder höher: Wenn du keinen Datenverkehr an Microsoft senden möchtest, kannst du den Wert <about:blank> unabhängig davon verwenden, ob das Gerät mit einer Domäne verbunden ist oder nicht, wenn es die einzige konfigurierte URL ist. |
| *Microsoft Edge | Windows Defender SmartScreen konfigurieren |  | Deaktiviert. Windows Defender SmartScreen ist deaktiviert, und Mitarbeiter können die Einstellung nicht aktivieren. HINWEIS: Berücksichtige diese Einstellung in der Umgebung. Wenn keine Verbindung mit dem Internet besteht, wird so verhindert, dass die Computer versuchen, Microsoft wegen SmartScreen-Informationen zu kontaktieren. |
| *Microsoft Edge | Verhindern, dass die Einrichtungs-Webseite in Microsoft Edge geöffnet wird |  | Aktiviert. Bei aktivierter Einstellung wird den Benutzern die Einrichtungswebseite nicht angezeigt, wenn sie Microsoft Edge zum ersten Mal öffnen. |
| OneDrive | OneDrive davon abhalten, Netzwerkdatenverkehr zu generieren, bis der Benutzer sich auf OneDrive anmeldet |  | Aktiviert. Aktiviere diese Einstellung, um zu verhindern, dass der OneDrive-Synchronisierungsclient (OneDrive.exe) Netzwerkdatenverkehr erzeugt (Suche nach Updates usw.), bis sich der Benutzer bei OneDrive anmeldet oder mit der Synchronisierung von Dateien auf dem lokalen Computer beginnt. |
| *OneDrive | Verwendung von OneDrive für die Dateispeicherung verhindern |  | Aktiviert. Es sei denn, OneDrive wird lokal oder remote verwendet. |
| OneDrive | Dokumente standardmäßig auf OneDrive speichern |  | Deaktiviert. Es sei denn, OneDrive wird lokal oder remote verwendet. |
| RSS-Feeds | Automatische Ermittlung von Feeds und Web Slices verhindern |  | Enabled |
|*RSS-Feeds | Hintergrundsynchronisierung für Feeds und Web Slices deaktivieren |  | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, wird die Möglichkeit, Feeds und Web Slices im Hintergrund zu synchronisieren, deaktiviert. |
|*Suche | Cortana zulassen |  | Deaktiviert. Wenn Cortana deaktiviert ist, können Benutzer immer noch auf dem Gerät suchen. |
|Suchen | Cortana auf Sperrbildschirm zulassen |   | Deaktiviert |
|*Suche | Der Suche und Cortana die Nutzung von Positionsdaten erlauben |  | Deaktiviert |
|Suchen | Websuche nicht zulassen |   | Enabled |
|*Suche | Nicht im Web suchen und keine Webergebnisse in der Suche anzeigen |  | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, werden Abfragen nicht im Web ausgeführt und Webergebnisse nicht angezeigt, wenn ein Benutzer eine Abfrage in der Suche durchführt. |
|Suchen | Hinzufügen von UNC-Speicherorten für die Indizierung in der Systemsteuerung verhindern |  | Enabled |
|Suchen | Indizierung von Dateien im Offlinedateicache verhindern |  | Enabled |
|*Suche | Festlegen der in den anonymen Informationen der Suche freizugebenden Informationen |  | Aktiviert. Nutzungsinformationen teilen, aber nicht Suchverlauf, Microsoft-Kontoinformationen oder bestimmten Standort. |
|*Softwareschutz-Plattform | Online-AVC-Überprüfung des KMS-Clients deaktivieren | Aktiviert. Wenn du diese Einstellung aktivierst, wird verhindert, dass dieser Computer Daten über seinen Aktivierungsstatus an Microsoft sendet. |
|*Spracherkennung | Automatische Aktualisierung von Sprachdaten zulassen |  | Deaktiviert. Wird nicht in regelmäßigen Abständen auf aktualisierte Sprachmodelle überprüft. |
|*Speicher | Automatische Downloads und Installation von Updates deaktivieren |  | Aktiviert. Wenn du diese Einstellung aktivierst, werden der automatische Download und die Installation von App-Updates deaktiviert. |
|*Speicher | Automatische Downloads von Updates auf Win8-Geräten deaktivieren | Aktiviert. Wenn du diese Einstellung aktivierst, wird der automatische Download von App-Updates deaktiviert. |
| Speicher | Deaktivieren des Angebots zum Update auf die aktuelle Version von Windows |  | Enabled |
|*Einstellungen synchronisieren | Nicht synchronisieren | Benutzern das Einschalten der Synchronisierung ermöglichen (nicht ausgewählt) | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, wird „Einstellungen synchronisieren“ deaktiviert und keine der „Einstellungen synchronisieren“-Gruppen auf diesem Gerät synchronisiert. |
| Texteingabe | Freihand- und Eingabeerkennung verbessern |  | Deaktiviert |
| Windows Defender Antivirus \\ MAPS | Microsoft MAPS beitreten |  | Deaktiviert. Wenn du diese Einstellung deaktivierst oder nicht konfigurierst, trittst du Microsoft MAPS nicht bei. |
| Windows Defender Antivirus \\ MAPS | Dateibeispiele senden, wenn eine weitere Analyse erforderlich ist | Nie senden | Aktiviert. Nur dann, wenn MAPS-Diagnosedaten nicht ausgewählt wurden. |
| Windows Defender Antivirus \\ Berichterstellung | Erweiterte Benachrichtigungen deaktivieren |  | Aktiviert. Wenn du diese Einstellung aktivierst, werden erweiterte Benachrichtigungen von Windows Defender Antivirus nicht auf Clients angezeigt. |
| Windows Defender Antivirus \\ Signaturaktualisierungen | Definieren der Reihenfolge der Quellen für das Herunterladen von Definitionsupdates | FileShares | Aktiviert. Wenn du diese Einstellung aktivierst, werden die Quellen für die Definitionsupdates in der angegebenen Reihenfolge kontaktiert. Sobald Definitionsupdates erfolgreich aus einer bestimmten Quelle heruntergeladen wurden, werden die verbleibenden Quellen in der Liste nicht mehr kontaktiert. |
| Windows-Fehlerberichterstattung | Speicherabbild für vom Betriebssystem erstellte Fehlerberichte automatisch senden |  | Deaktiviert |
| Windows-Fehlerberichterstattung | Deaktivieren der Windows-Fehlerberichterstattung |  | Enabled |
| Windows-Spielaufzeichnung und -übertragung | Aktiviert oder deaktiviert die Windows-Spielaufzeichnung und -übertragung | | Deaktiviert |
| Windows Installer | Maximalgröße für den Basisdateicache steuern | 5 | Enabled |
| Windows Installer | Erstellung von Systemwiederherstellungsprüfpunkten deaktivieren |  | Enabled |
| Windows Mail | Communities–Features deaktivieren |  | Enabled |
| Windows Media Player | Dialogfelder für die erste Verwendung nicht anzeigen |  | Enabled |
| Windows Media Player | Medienfreigabe verhindern |  | Enabled |
| Windows-Mobilitätscenter | Windows-Mobilitätscenter deaktivieren |  | Enabled |
| Windows-Zuverlässigkeitsanalyse | WMI-Anbieter für Zuverlässigkeit konfigurieren |  | Deaktiviert |
| Windows Update | Automatische Updates sofort installieren |  | Enabled |
| Windows Update | Keine Verbindungen mit Windows Update-Internetadressen herstellen |  | Aktiviert. Die Aktivierung dieser Richtlinie deaktiviert diese Funktionalität und kann dazu führen, dass die Verbindung mit öffentlichen Diensten wie dem Windows Store nicht mehr funktioniert. HINWEIS: Diese Richtlinie gilt nur, wenn das Gerät so konfiguriert ist, dass es eine Verbindung mit einem internen Updatedienst über die Richtlinie „Internen Pfad für den Microsoft Updatedienst angeben“ herstellt. |
| Windows Update | Zugriff auf alle Windows Update-Funktionen entfernen |   | Enabled |
| Windows Update \\ Windows Update for Business | Vorabversionen verwalten | Lege das Verhalten für den Empfang von Vorabversionen fest: | Aktiviert. Bei Auswahl von „Vorabversionen deaktivieren“ wird verhindert, dass Vorabversionen auf dem Gerät installiert werden. Dies verhindert, dass Benutzer sich über „Einstellungen > Update und Sicherheit“ am Windows-Insider-Programm beteiligen können.<br>Deaktiviert. Deaktiviert Vorabversionen. |
| Windows Update \\ Windows Update for Business | Auswählen, wann Vorabversionen und Featureupdates empfangen werden | Halbjährlicher Kanal<br>Aufschiebung: 365 Tage<br>Start anhalten: jjj-mm-tt. | Aktiviert. Aktiviere diese Richtlinie, um die Ebene der zu empfangenden Vorabversionen oder Featureupdates und den Zeitpunkt anzugeben. |
| Windows Update \\ Windows Update for Business | Beim Empfang von Qualitätsupdates auswählen | 1. 30 Tage<br>2. Qualitätsupdates anhalten ab jjjj-mm-tt | Enabled |
| Windows-Einstellungen für benutzerdefinierte Richtlinie für eingeschränkten Datenverkehr | OneDrive davon abhalten, Netzwerkdatenverkehr zu generieren, bis der Benutzer sich auf OneDrive anmeldet |  | Aktiviert. Aktiviere diese Einstellung, um zu verhindern, dass der OneDrive-Synchronisierungsclient (OneDrive.exe) Netzwerkdatenverkehr erzeugt (Suche nach Updates usw.), bis sich der Benutzer bei OneDrive anmeldet oder mit der Synchronisierung von Dateien auf dem lokalen Computer beginnt. |
| Windows-Einstellungen für benutzerdefinierte Richtlinie für eingeschränkten Datenverkehr | Windows Defender-Benachrichtigungen deaktivieren |  | Aktiviert. Wenn du diese Richtlinieneinstellung aktivierst, sendet Windows Defender keine Benachrichtigungen mit kritischen Informationen über den Zustand und die Sicherheit deines Geräts. |
| Richtlinie für „Lokaler Computer“ \\ Benutzerkonfiguration \\ Administrative Vorlagen  |  |  |
|Systemsteuerung \\ Regions- und Sprachoptionen | Textvorhersagen bei der Eingabe deaktivieren |  | Enabled |
| Desktop | Freigaben von zuletzt geöffneten Dateien nicht in „Netzwerkumgebung“ hinzufügen |  | Enabled |
| Desktop | Aero Shake-Mausbewegung zum Minimieren von Fenstern deaktivieren |  | Enabled |
| Desktop \\ Active Directory | Maximale Suchgröße von Active Directory | 2500 | Enabled |
| Startmenü und Taskleiste | Anheften der Store-App an die Taskleiste nicht zulassen |  | Enabled |
| Startmenü und Taskleiste | Keine Elemente in Sprunglisten von Remotestandorten anzeigen oder nachverfolgen |  | Enabled |
| Startmenü und Taskleiste | Beim Zuordnen von Shellshortcuts nicht die suchbasierte Methode verwenden |  | Aktiviert. Das System führt keine umfassende Laufwerksuche durch. Es wird nur eine Meldung angezeigt, die erklärt, dass die Datei nicht gefunden wurde. |
| Startmenü und Taskleiste | Entfernen der Personenleiste aus der Taskleiste |  | Aktiviert. Das Personensymbol wird aus der Taskleiste entfernt, die entsprechende Einstellungsumschaltung wird von der Einstellungsseite der Taskleiste entfernt, und Benutzer können Personen nicht an die Taskleiste anheften. |
| Startmenü und Taskleiste | Sprechblasenbenachrichtigungen für Featureankündigungen deaktivieren |  | Aktiviert. Benutzer können die Store-App nicht an die Taskleiste anheften. Wenn die Store-App bereits an die Taskleiste angeheftet ist, wird sie beim nächsten Anmelden aus der Taskleiste entfernt. |
| Startmenü und Taskleiste | Benutzerüberwachung deaktivieren |  | Enabled |
| Startmenü und Taskleiste \\ Benachrichtigungen | Popupbenachrichtigungen deaktivieren |  | Enabled |
| Windows-Komponenten \\ Cloud-Inhalt | Features von Windows-Blickpunkt deaktivieren |  | Enabled |

### <a name="notes-about-network-connectivity-status-indicator"></a>Hinweise zur Netzwerkverbindungs-Statusanzeige

Die obigen Einstellungen für Gruppenrichtlinien beinhalten Einstellungen, um die Überprüfung zu deaktivieren, um festzustellen, ob das System mit dem Internet verbunden ist. Wenn deine Umgebung keine Verbindung mit dem Internet herstellt – oder sie indirekt herstellt – kannst du eine Gruppenrichtlinieneinstellung festlegen, um das Netzwerksymbol aus der Taskleiste zu entfernen. Du könntest das Netzwerksymbol aus folgendem Grund aus der Taskleiste entfernen: Wenn du die Prüfungen der Internetverbindung deaktivierst, wird ein gelbes Flag auf dem Netzwerksymbol angezeigt, obwohl das Netzwerk möglicherweise normal funktioniert. Wenn du das Netzwerksymbol als Gruppenrichtlinieneinstellung entfernen möchtest, ist dies hier möglich:

| Richtlinieneinstellung | Element | Untergeordnete Element | Mögliche Einstellung und Kommentare|
| -------------- | ---- | -------- | ---------------------------- |
| Windows Update oder Windows Update for Business | Beim Empfang von Qualitätsupdates auswählen | 1. 30 Tage<br>2. Qualitätsupdates anhalten ab jjjj-mm-tt | Enabled |
| Richtlinie für „Lokaler Computer“ \\ Benutzerkonfiguration \\ Administrative Vorlagen |  |  |  |
| Startmenü und Taskleiste | Netzwerksymbol entfernen |  | Aktiviert. Das Netzwerksymbol wird nicht im Systembenachrichtigungsbereich angezeigt. |

Weitere Informationen zum Netzwerkverbindungs-Statusindikator (NCSI) findest du unter [Verwalten von Verbindungsendpunkten für Windows 10 Enterprise, Version 1903](/windows/privacy/manage-windows-1903-endpoints) und [Verwalten von Verbindungen von Windows 10-Betriebssystemkomponenten mit Microsoft-Diensten](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services).

### <a name="system-services"></a>Systemdienste

Wenn du erwägst, deine Systemdienste zu deaktivieren, um Ressourcen zu schonen, muss unbedingt darauf geachtet werden, dass der betreffende Dienst nicht in irgendeiner Weise Bestandteil eines anderen Diensts ist. Beachten Sie, dass einige Dienste nicht in der Liste enthalten sind, da sie nicht auf eine unterstützte Weise deaktiviert werden können.

Die meisten dieser Empfehlungen spiegeln die Empfehlungen für Windows Server 2016 mit Desktopdarstellung unter [Anleitungen zur Deaktivierung von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung](../../security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server.md) wider.

Viele Dienste, die ggf. als gute Kandidaten zum Deaktivieren erscheinen, sind auf den Starttyp „Manueller Dienst“ festgelegt. Dies bedeutet, dass der Dienst nicht automatisch gestartet wird, sondern erst, wenn ein Prozess oder ein Ereignis eine Anforderung an den zu deaktivierenden Dienst auslöst. Dienste, für die bereits der Starttyp „Manuell“ festgelegt ist, sind hier in der Regel nicht aufgeführt.

> [!NOTE]
> Du kannst aktuell ausgeführte Dienste mit diesem PowerShell-Beispielcode auflisten und dabei nur den Kurznamen des Diensts ausgeben:

```powershell
 Get-Service | Where-Object {$_.Status -eq "Running"} | Select-Object -ExpandProperty Name
 ```

| Windows-Dienst | Element | Kommentare|
| -------------- | ---- | ---------------------------- |
| CDPUserService | Dieser Benutzerdienst wird für Szenarien mit der Plattform für verbundene Geräte verwendet. | Dies ist ein benutzerbezogener Dienst, und daher muss der *Vorlagendienst* deaktiviert sein. |
| Benutzererfahrung und Telemetrie im verbundenen Modus | Ermöglicht Funktionen, die Benutzerfreundlichkeit in Anwendungen und im verbundenen Modus unterstützen. Außerdem verwaltet dieser Dienst die ereignisgesteuerte Sammlung und Übertragung von Diagnose- und Nutzungsdaten (die zur Verbesserung der Benutzerfreundlichkeit und Qualität der Windows-Plattform eingesetzt werden). Dazu müssen die Diagnose- und Nutzungseinstellungen in der Datenschutzoption unter „Feedback und Diagnose“ aktiviert sein. | Im nicht verbundenen Netzwerk Deaktivierung erwägen. |
| Kontaktdaten | Indiziert Kontaktdaten für die schnelle Kontaktsuche. Wenn du diesen Dienst beendest oder deaktivierst, können Kontakte in den Suchergebnissen fehlen. | Dies ist ein benutzerbezogener Dienst, und daher muss der *Vorlagendienst* deaktiviert sein. |
| Diagnoserichtliniendienst | Ermöglicht die Problemerkennung und -lösung für Windows-Komponenten. Wenn dieser Dienst beendet wird, funktioniert die Diagnose nicht mehr. | |
| Manager für heruntergeladene Karten | Windows-Dienst für den Anwendungszugriff auf heruntergeladene Karten. Dieser Dienst wird bedarfsgesteuert je nach der Anwendung gestartet, die auf heruntergeladene Karten zugreift. Wenn der Dienst deaktiviert wird, können Apps nicht auf Karten zugreifen. | |
| Geolocation-Dienst | Überwacht die aktuelle Position des Systems und verwaltet die Geofences | |
| GameDVR und Übertragungsbenutzerdienst | Dieser Benutzerdienst wird für Spielaufzeichnungen und Liveübertragungen verwendet. | Dies ist ein benutzerbezogener Dienst, und daher muss der *Vorlagendienst* deaktiviert sein. |
| MessagingService | Dienst, der SMS und verwandte Funktionen unterstützt. | Dies ist ein benutzerbezogener Dienst, und daher muss der *Vorlagendienst* deaktiviert sein. |
| Laufwerke optimieren | Unterstützt den Computer bei einer effizienteren Ausführung durch das Optimieren von Dateien auf Speicherlaufwerken. | VDI-Lösungen profitieren normalerweise nicht von der Datenträgeroptimierung. Bei diesen „Laufwerken“ handelt es sich nicht um herkömmliche Laufwerke, sondern oft nur um eine temporäre Speicherbelegung. |
| Superfetch | Verwaltet und verbessert die Systemleistung im Zeitablauf. | Verbessert im Allgemeinen nicht die VDI-Leistung, insbesondere nicht dauerhaft, da der Betriebssystemzustand bei jedem Neustart verworfen wird. |
| Dienst für Bildschirmtastatur und Schreibbereich | Aktiviert die Stift- und Freihandfunktionalität der Bildschirmtastatur und des Schreibbereichs. | |
| Windows-Fehlerberichterstattung | Ermöglicht die Berichterstattung von Fehlern bei nicht mehr funktionierenden und reagierenden Programmen und das Angeben von Lösungen. Ermöglicht außerdem das Generieren von Protokollen für Diagnose- und Reparaturdienste. Wenn dieser Dienst beendet wird, funktioniert die Fehlerberichterstattung möglicherweise nicht ordnungsgemäß, und die Ergebnisse von Diagnosediensten und Reparaturen werden möglicherweise nicht angezeigt. | Mit VDI wird die Diagnose oft in einem Offlineszenario und nicht in der Hauptproduktion durchgeführt. Außerdem deaktivieren einige Kunden WER ohnehin. WER benötigt eine winzige Menge an Ressourcen für viele verschiedene Angelegenheiten inklusive Fehler bei der Installation eines Geräts oder bei der Installation eines Updates. |
| Windows Media Player-Netzwerkfreigabedienst | Gibt Windows Media Player-Bibliotheken für andere vernetzte Spieler und Mediengeräte mit universellem Plug & Play frei | Nicht erforderlich, solange Kunden nicht WMP-Bibliotheken im Netzwerk gemeinsam nutzen. |
| Windows-Dienst für mobile Hotspots | Ermöglicht die Freigabe einer Datenverbindung für ein anderes Gerät. | |
| Windows Search | Stellt Inhaltsindizierung, Eigenschaftenzwischenspeicherung und Suchergebnisse für Dateien, E-Mails und andere Inhalte bereit.                                                                    | Wahrscheinlich nicht erforderlich, besonders bei nicht dauerhafter VDI |

#### <a name="per-user-services-in-windows"></a>Benutzerbezogene Dienste in Windows

Benutzerbezogene Dienste werden erstellt, wenn ein Benutzer sich bei Windows oder Windows Server anmeldet, und sie werden beendet und gelöscht, wenn dieser Benutzer sich abmeldet. Diese Dienste werden im Sicherheitskontext des Benutzerkontos ausgeführt – dies bietet eine bessere Ressourcenverwaltung als der bisherige Ansatz, diese Art von Diensten im Explorer auszuführen, verknüpft mit einem vorkonfigurierten Konto oder als Aufgaben.

[Benutzerbezogene Dienste in Windows 10 und Windows Server](/windows/application-management/per-user-services-in-windows)

Wenn Sie beabsichtigen, einen Dienststartwert zu ändern, besteht die bevorzugte Methode darin, eine CMD-Eingabeaufforderung mit erhöhten Rechten zu öffnen und das Dienststeuerungs-Manager-Tool „Sc.exe“ auszuführen. Weitere Informationen zur Verwendung von „Sc.exe“ finden Sie unter [Sc](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc754599(v=ws.11)).

### <a name="scheduled-tasks"></a>Geplante Aufgaben

Stelle wie bei anderen Elementen in Windows sicher, dass ein Element nicht benötigt wird, bevor du es deaktivierst.

Die folgende Liste enthält Aufgaben, die Optimierungen oder Datensammlungen auf Computern durchführen, die ihren Zustand Neustarts übergreifend beibehalten. Wenn eine VDI-VM-Aufgabe neu startet und alle Änderungen seit dem letzten Start verwirft, sind Optimierungen für physische Computer nicht hilfreich.

Du kannst alle aktuellen geplanten Tasks, einschließlich Beschreibungen, mit dem folgenden PowerShell-Code abrufen:

```powershell
 Get-ScheduledTask | Select-Object -Property TaskPath,TaskName,State,Description
```

> [!NOTE]
> Es gibt mehrere Tasks, die nicht über Skripts deaktiviert werden können, auch wenn du mit erhöhten Rechten arbeitest. Es wird empfohlen, keine Tasks zu deaktivieren, die nicht mithilfe eines Skripts deaktiviert werden können.

Name des geplanten Tasks:

- Mobilfunk
- Consolidator
- Diagnose
- FamilySafetyMonitor
- FamilySafetyRefreshTask
- MaintenanceTasks
- MapsToastTask
- Kompatibilität
- Microsoft-Windows-DiskDiagnosticDataCollector
- MNO
- NotificationTask
- PerformRemediation
- ProactiveScan
- ProcessMemoryDiagnosticEvents
- ProgramDataUpdater
- Proxy
- QueueReporting
- RecommendedTroubleshootingScanner
- ReconcileFeatures
- ReconcileLanguageResources
- RefreshCache
- RegIdleBackup
- ResPriStaticDbSync
- RunFullMemoryDiagnostic
- ScanForUpdates
- ScanForUpdatesAsUser
- Geplant
- ScheduledDefrag
- sihpostreboot
- SilentCleanup
- SmartRetry
- SpaceAgentTask
- SpaceManagerTask
- SpeechModelDownloadTask
- Sqm-Tasks
- SR
- StartComponentCleanup
- StartupAppTask
- StorageSense
- SyspartRepair
- Sysprep
- UninstallDeviceTask
- UpdateLibrary
- UpdateModelTask
- UsbCeip
- USB-Benachrichtigungen
- USO_UxBroker
- WLAN
- WIM-Hash-Management
- WindowsActionDialog
- WinSAT
- Ordner
- WsSwapAssessmentTask
- XblGameSaveTask

### <a name="apply-windows-and-other-updates"></a>Anwenden von Windows- und anderen Updates

Ob von Microsoft Update oder deinen internen Ressourcen, wende die verfügbaren Updates einschließlich Windows Defender-Signaturen an. Dies ist ein guter Zeitpunkt, andere verfügbare Updates (einschließlich Updates für Microsoft Office, sofern installiert) und andere Softwareupdates anzuwenden. Wenn PowerShell im Image verbleibt, kannst du die neueste verfügbare Hilfe für PowerShell herunterladen, indem du den Befehl [Update-Help](/powershell/module/microsoft.powershell.core/update-help?view=powershell-7) ausführst.

#### <a name="servicing-the-operating-system-and-apps"></a>Wartung von Betriebssystem und Apps

Irgendwann während des Bildoptimierungsprozesses sollten verfügbare Windows-Updates angewendet werden. Es gibt eine Einstellung in den Windows 10-Updateeinstellungen, mit der zusätzliche Updates bereitgestellt werden können:

![Zusätzliche Updates](media/rds-vdi-recommendations-1909/servicing.png)

Dies wäre eine gute Einstellung, falls du Microsoft-Anwendungen wie Microsoft Office im Basisimage installieren möchtest. Auf diese Weise ist Office auf dem neuesten Stand, wenn das Image in Betrieb genommen wird. Auch .NET-Updates und Updates für bestimmte Drittanbieterkomponenten wie Adobe sind über Windows Update verfügbar.

Ein sehr wichtiger Aspekt für nicht dauerhafte VDI-VMs sind Sicherheitsupdates, einschließlich Definitionsdateien für Sicherheitssoftware. Diese Updates werden möglicherweise mindestens ein Mal pro Tag veröffentlicht. Möglicherweise können diese Updates einschließlich Windows Defender und Drittanbieterkomponenten beibehalten werden.

Für Windows Defender kann es am besten sein, die Updates auch in einer nicht dauerhaften VDI zuzulassen. Die Updates werden in fast jeder Anmeldesitzung angewendet, aber sie sind klein und sollten kein Problem sein. Außerdem gelangt die VM nicht in den Rückstand, da nur die neuesten verfügbaren Updates angewendet werden. Dasselbe gilt möglicherweise für Definitionsdateien von Drittanbietern.

> [!NOTE]
> Store-Apps (UWP-Apps) werden über den Windows Store aktualisiert. Moderne Versionen von Office wie Microsoft 365 werden über ihre eigenen Mechanismen aktualisiert, wenn sie direkt mit dem Internet verbunden sind, oder andernfalls über Management-Technologien.

### <a name="windows-system-startup-event-traces"></a>Ablaufverfolgungen für Ereignisse des Windows-Systemstarts

Windows wird standardmäßig zum Sammeln und Speichern eingeschränkter Diagnosedaten konfiguriert. Dies soll eine Diagnose ermöglichen oder Daten aufzeichnen, falls weitere Problembehandlung erforderlich ist. Automatische Systemablaufverfolgungen findest du am in der folgenden Abbildung gezeigten Speicherort:

![Systemablaufverfolgungen](media/rds-vdi-recommendations-1909/system-traces.png)

Einige der unter **Ereignisablaufverfolgungssitzungen** und **Startereignis-Ereignisablaufverfolgungssitzungen** angezeigten Ablaufverfolgungen können und sollten nicht beendet werden. Andere, z. B. die „WiFiSession“-Ablaufverfolgung, können beendet werden. Zum Beenden einer unter **Ereignisablaufverfolgungssitzungen** ausgeführten Ablaufverfolgung können Sie mit der rechten Maustaste auf diese klicken und dann auf „Beenden“ klicken. Gehe folgendermaßen vor, um zu verhindern, dass die Ablaufverfolgungen automatisch beim Start gestartet werden:

1. Klicke auf den Ordner **Startereignis-Ereignisablaufverfolgungssitzungen**.

2. Suche die gewünschte Ablaufverfolgung, und doppelklicke darauf.

3. Klicke auf die Registerkarte **Ablaufverfolgungssitzung**.

4. Klicke auf das Kontrollkästchen **Aktiviert**, um das Häkchen zu entfernen.

5. Klicken Sie auf **OK**.

Für die folgenden Systemablaufverfolgungen kommt eine Deaktivierung bei der Verwendung von VDI infrage:

| Name                    | Anmerkungen                       |
| ----------------------- | ----------------------------- |
| AppModel | Eine Sammlung von Ablaufverfolgungen, zu denen „phone“ gehört |
| CloudExperienceHostOOBE | |
| DiagLog | |
| NtfsLog | |
| TileStore | |
| UBPM | |
| WiFiDriverIHVSession | Wenn kein WLAN-Gerät verwendet wird |
| WiFiSession | |
| WinPhoneCritical | |

### <a name="windows-defender-optimization-with-vdi"></a>Windows Defender-Optimierung mit VDI

Microsoft hat vor kurzem Dokumentation zu Windows Defender in einer VDI-Umgebung veröffentlicht. Weitere Informationen findest du im [Bereitstellungsleitfaden für Windows Defender Antivirus in einer VDI-Umgebung (Virtual Desktop Infrastructure)](/windows/security/threat-protection/windows-defender-antivirus/deployment-vdi-windows-defender-antivirus).

Der oben genannte Artikel enthält Verfahren zur Wartung des VDI-Goldimages und der VDI-Clients während ihrer Ausführung. Um die Netzwerkbandbreite zu reduzieren, wenn VDI-Computer ihre Windows Defender-Signaturen aktualisieren müssen, staffele Neustarts, und plane sie wenn möglich außerhalb der Geschäftszeiten. Die Signatur-Updates von Windows Defender können intern auf Dateifreigaben enthalten sein, und wenn möglich, sollten sich diese Dateifreigaben in denselben Netzwerksegmenten wie die virtuellen VDI-Computer oder in deren Nähe befinden.

### <a name="client-network-performance-tuning-by-registry-settings"></a>Clientnetzwerk-Leistungsoptimierung durch Registrierungseinstellungen

Es gibt einige Registrierungseinstellungen, mit denen die Netzwerkleistung gesteigert werden kann. Dies ist besonders wichtig in Umgebungen, in denen die VDI oder der Computer eine Workload hat, die hauptsächlich netzwerkbasiert ist. Die Einstellungen in diesem Abschnitt werden empfohlen, um die Leistung zugunsten des Netzwerks zu verzerren, indem sie zusätzliche Pufferung und Zwischenspeicherung von Verzeichniseinträgen usw. festlegen.

> [!NOTE]
> Einige Einstellungen in diesem Abschnitt sind nur registrierungsbasiert und sollten in das Basisimage integriert werden, bevor das Image für die Produktion bereitgestellt wird.

Die folgenden Einstellungen sind in den [Richtlinien zur Optimierung der Leistung für Windows Server 2016](../../administration/performance-tuning/index.md) dokumentiert, die von der Windows-Produktgruppe auf Microsoft.com veröffentlicht wurden.

#### <a name="disablebandwidththrottling"></a>DisableBandwidthThrottling

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableBandwidthThrottling`

Gilt für Windows 10. Der Standardwert ist **0**. Standardmäßig drosselt der SMB-Redirector den Durchsatz für Netzwerkverbindungen mit hoher Latenz. In einigen Fällen besteht das Ziel hierbei darin, netzwerkbezogene Timeouts zu verhindern. Durch das Festlegen dieses Registrierungswerts auf 1 wird diese Art der Drosselung deaktiviert. So wird für Netzwerkverbindungen mit hoher Latenz ein höherer Durchsatz für Dateiübertragungen ermöglicht. Erwäge, diesen Wert auf **1** festzulegen.

#### <a name="fileinfocacheentriesmax"></a>FileInfoCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheEntriesMax` Gilt für Windows 10. Der Standardwert ist **64**, und der gültige Bereich reicht von 1 bis 65.536. Dieser Wert wird verwendet, um die Menge an Dateimetadaten zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf viele Dateien zugegriffen wird. Erwäge, diesen Wert auf **1.024** zu erhöhen.

#### <a name="directorycacheentriesmax"></a>DirectoryCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntriesMax`

Gilt für Windows 10. Der Standardwert ist **16**, und der gültige Bereich reicht von 1 bis 4.096. Dieser Wert wird verwendet, um die Menge von Verzeichnisinformationen zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf große Verzeichnisse zugegriffen wird. Erwäge, diesen Wert auf **1.024** zu erhöhen.

#### <a name="filenotfoundcacheentriesmax"></a>FileNotFoundCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheEntriesMax`

Gilt für Windows 10. Der Standardwert ist **128**, und der gültige Bereich reicht von 1 bis 65.536. Dieser Wert wird verwendet, um die Menge von Dateinameninformationen zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf viele Dateinamen zugegriffen wird. Erwäge, diesen Wert auf **2.048** zu erhöhen.

#### <a name="dormantfilelimit"></a>DormantFileLimit

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantFileLimit`

Gilt für Windows 10. Der Standardwert beträgt **1.023**. Mit diesem Parameter wird die maximale Anzahl von Dateien angegeben, die auf einer freigegebenen Ressource geöffnet bleiben soll, nachdem die Datei von der Anwendung geschlossen wurde. Wenn viele tausend Clients Verbindungen mit SMB-Servern herstellen, solltest du diesen Wert auf **256** reduzieren.

Du kannst viele dieser SMB-Einstellungen mit den Windows PowerShell-Cmdlets [Set-SmbClientConfiguration](/powershell/module/smbshare/set-smbclientconfiguration?view=win10-ps) und [Set-SmbServerConfiguration](/powershell/module/smbshare/set-smbserverconfiguration?view=win10-ps) konfigurieren. Einstellungen nur für die Registrierung auch mit Windows PowerShell konfiguriert werden, wie im folgenden Beispiel gezeigt:

```powershell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" RequireSecuritySignature -Value 0 -Force
```

Zusätzliche Einstellungen aus dem Leitfaden [Windows Restricted Traffic Limited Functionality Baseline](https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services) (Windows-Baseline für eingeschränkten Datenverkehr und begrenzte Funktionalität).

Microsoft hat für Umgebungen, die nicht direkt mit dem Internet verbunden sind oder für die die Menge an Daten reduziert werden soll, die an Microsoft und andere Dienste gesendet werden, eine Baseline veröffentlicht, die mit den gleichen Verfahren wie die [Windows-Sicherheitsbaselines](https://docs.microsoft.com/windows/security/threat-protection/windows-security-baselines) erstellt wurde.

Die Windows Restricted Traffic Limited Functionality Baseline-Einstellungen sind in der Gruppenrichtlinientabelle mit einem Sternchen gekennzeichnet.

#### <a name="disk-cleanup-including-using-the-disk-cleanup-wizard"></a>Datenträgerbereinigung (einschließlich des Datenträgerbereinigungs-Assistenten)

Die Datenträgerbereinigung kann besonders bei Gold-/Masterimage-VDI-Implementierungen hilfreich sein. Nachdem das Image vorbereitet, aktualisiert und konfiguriert wurde, ist eine der letzten durchgeführten Aufgaben die Datenträgerbereinigung. Der integrierte Datenträgerbereinigungs-Assistent kann Ihnen bei der Bereinigung der meisten Bereiche mit potenziellen Speicherplatzeinsparungen helfen. Auf einer VM, auf der nur sehr wenig installiert, die aber vollständig gepatcht wurde, kannst du mit der Datenträgerbereinigung in der Regel ungefähr 4 GB Speicherplatz auf dem Datenträger freigeben.

Hier erhältst du Vorschläge für verschiedene Datenträgerbereinigungsaufgaben. Diese sollten vor der Implementierung alle getestet werden:

1. Führe nach dem Anwenden aller Updates den Datenträgerbereinigungs-Assistenten (mit erhöhten Rechten) aus. Beziehen Sie die Kategorien „Übermittlungsoptimierung“ und „Windows Update-Bereinigung“ mit ein. Dieser Prozess kann mithilfe der Befehlszeile `Cleanmgr.exe` mit der Option `/SAGESET:11` automatisiert werden. Die Option `/SAGESET` legt Registrierungswerte fest, die später zur Automatisierung der Datenträgerbereinigung verwendet werden können, wobei jede verfügbare Option im Datenträgerbereinigungs-Assistenten verwendet wird.

    1. Die Ausführung von `Cleanmgr.exe /SAGESET:11` auf einer Test-VM von einer sauberen Installation aus zeigt, dass standardmäßig nur zwei automatische Optionen für die Datenträgerbereinigung aktiviert sind:

        - Heruntergeladene Programmdateien

        - Temporäre Internetdateien

    2. Wenn du weitere Optionen oder alle Optionen festlegst, werden diese Optionen entsprechend dem im vorherigen Befehl (`Cleanmgr.exe /SAGESET:11`) angegebenen **Indexwert** in der Registrierung gespeichert. In diesem Beispiel verwenden wir den Wert `11` als unseren Index für ein nachfolgend automatisiertes Datenträgerbereinigungsverfahren.

    3. Nach dem Ausführen von `Cleanmgr.exe /SAGESET:11` werden mehrere Kategorien von Datenträgerbereinigungsoptionen angezeigt. Du kannst jede Option aktivieren und dann auf **OK** klicken. Der Datenträgerbereinigungs-Assistent wird ausgeblendet, und die Einstellungen werden in der Registrierung gespeichert.

2. Bereinige deinen Volumeschattenkopie-Speicher, sofern er verwendet wird.

    - Öffne eine Eingabeaufforderung mit erhöhten Rechten, und führe den Befehl `vssadmin list shadows` und dann den Befehl `vssadmin list shadowstorage` aus.

        Wenn die Ausgabe dieser Befehle **Es wurden keine Ergebnisse für die Abfrage gefunden** lautet, wird kein VSS-Speicher verwendet.

3. Bereinige temporäre Dateien und Protokolle. Führe den Befehl `Del C:\*.tmp /s` über eine Eingabeaufforderung mit erhöhten Rechten, den Befehl `Del C:\Windows\Temp\.` und dann den Befehl `Del %temp%\.` aus.

4. Lösche nicht verwendete Profile auf dem System, indem du `wmic path win32_UserProfile where LocalPath="c:\users\<user>" Delete` ausführst.

### <a name="remove-onedrive-components"></a>Entfernen von OneDrive-Komponenten

Das Entfernen von OneDrive umfasst das Entfernen des Pakets und das Deinstallieren und Entfernen der \*.lnk-Dateien. Der folgende PowerShell-Beispielcode kann verwendet werden, um das Entfernen von OneDrive aus dem Image zu unterstützen. Er ist in den GitHub-VDI-Optimierungsskripts enthalten:

```azurecli
Get-Process -Name OneDrive | Stop-Process -Force -Confirm:$false
Get-Process -Name explorer | Stop-Process -Force -Confirm:$false
if (Test-Path "C:\\Windows\\System32\\OneDriveSetup.exe")`
    { Start-Process "C:\\Windows\\System32\\OneDriveSetup.exe"`
        -ArgumentList "/uninstall"`
        -Wait }
if (Test-Path "C:\\Windows\\SysWOW64\\OneDriveSetup.exe")`
    { Start-Process "C:\\Windows\\SysWOW64\\OneDriveSetup.exe"`
        -ArgumentList "/uninstall"`
        -Wait }
Remove-Item -Path "C:\\Windows\\ServiceProfiles\\LocalService\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\OneDrive.lnk" -Force
Remove-Item -Path "C:\\Windows\\ServiceProfiles\\NetworkService\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\OneDrive.lnk" -Force

# Remove the automatic start item for OneDrive from the default user profile registry hive

Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Load HKLM\\Temp C:\\Users\\Default\\NTUSER.DAT" -Wait
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Delete HKLM\\Temp\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run /v OneDriveSetup /f" -Wait
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Unload HKLM\\Temp" -Wait Start-Process -FilePath C:\\Windows\\Explorer.exe -Wait
```

## <a name="turn-windows-update-back-on"></a>Erneutes Aktivieren von Windows Update

Wenn du Windows Update erneut aktivieren möchtest (wie im Fall von dauerhafter VDI), führe die folgenden Schritte aus:

- Erneutes Aktivieren dieser Gruppenrichtlinieneinstellungen:

    - Richtlinie für "Lokaler Computer" \\ Computerkonfiguration \\ Administrative Vorlagen \\ System \\ Internetkommunikationsverwaltung \\ Internetkommunikationseinstellungen

        - Deaktiviere den Zugriff auf alle Windows Update-Features (Änderung aus **Aktiviert** in **Nicht konfiguriert**).

    - Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Windows-Komponenten \\ Windows Update

        - Entfernen des Zugriffs auf alle Windows Update-Features (Änderung aus **Aktiviert** in **Nicht konfigurierte**)

        - Stelle keine Verbindung mit den Windows Update Internetspeicherorten her (Änderung aus **Aktiviert** in **Nicht konfiguriert**).

    - Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Windows-Komponenten \\ Windows Update \\ Windows Update for Business

        - Wählen Sie aus, wann Qualitätsupdates empfangen werden sollen (Änderung von „Aktiviert“ in „Nicht konfiguriert“).

    -   Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Windows-Komponenten \\ Windows Update \\ Windows Update for Business

        - Wähle aus, wann Vorschaubuilds und Featureupdates empfangen werden sollen (Änderung aus **Aktiviert** in **Nicht konfiguriert**).

-  Erneutes Aktivieren von Diensten

    - Aktualisiere den Orchestratordienst (Änderung aus **Deaktiviert** in **Automatisch (verzögerter Start)** ).

    - Bearbeite die folgenden Windows-Registrierungseinstellungen:

        - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UpdatePolicy\PolicyState

            - DeferQualityUpdates (Änderung aus **1** in **0**)

        - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UpdatePolicy\Settings

            - PausedQualityDate (lösche beliebigen vorhandenen Wert)

        - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\WAU

            - Deaktiviert

-  Erneutes Aktivieren von geplanten Aufgaben

    - Aufgabenplanungsbibliothek \\ Microsoft \\ Windows \\ InstallService \\ ScanForUpdates

    - Aufgabenplanungsbibliothek \\ Microsoft \\ Windows \\ InstallService \\ ScanForUpdatesAsUser

Damit alle diese Einstellungen wirksam werden, starte das Gerät neu. Wenn du nicht möchtest, dass dieses Gerät die angebotenen Featureupdates verwendet, navigiere zu Einstellungen \\ Windows Update \\ Erweiterte Optionen \\. Wähle aus, wann Updates installiert werden, und lege dann die Option manuell fest. **Ein Featureupdate enthält neue Funktionen und Verbesserungen. Es kann für diese Anzahl von Tagen für einen Wert ungleich NULL verzögert werden, z. B. 180, 365 usw.**

Für Fragen oder Bedenken bezüglich der in diesem Dokument enthaltenen Informationen wende dich bitte an dein Microsoft-Kontoteam, recherchiere den Microsoft VDI-Blog, poste eine Nachricht in den Microsoft-Foren oder wende dich bei Fragen oder Bedenken an Microsoft.

### <a name="references"></a>Referenzen

- [Was ist VDI (Virtual Desktop Infrastructure)?](https://www.citrix.com/glossary/vdi.html)

- [Sysprep-Fehler nach dem Entfernen oder Aktualisieren von Microsoft Store-Apps, die integrierte Windows-Images enthalten](https://support.microsoft.com/help/2769827/sysprep-fails-after-you-remove-or-update-windows-store-apps-that-inclu).
