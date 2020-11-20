---
title: Optimieren von Windows 10 Version 2004 für eine Rolle als virtueller Desktop
description: Empfohlene Einstellungen und Konfiguration zum Minimieren des Mehraufwands für Windows 10-Desktops (Version 2004), die als VDI-Images verwendet werden
ms.prod: windows-server
ms.reviewer: robsmi, timuessi
ms.technology: remote-desktop-services
author: Heidilohr
ms.author: helohr
ms.topic: article
manager: ''
ms.date: 09/24/2020
ms.openlocfilehash: 129bbc8387be655cca563935cb7ff891664da357
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155891"
---
# <a name="optimizing-windows-10-version-2004-for-a-virtual-desktop-infrastructure-vdi-role"></a>Optimieren von Windows 10, Version 2004, für eine VDI-Rolle (Virtual Desktop Infrastructure)

Dieser Artikel enthält Konfigurationsvorschläge für Windows 10 Version 2004, die eine optimale Leistung in virtualisierten Desktopumgebungen wie virtuellen Desktopinfrastrukturen (VDI) und Windows Virtual Desktop ermöglichen sollen. Bei sämtlichen Einstellungen in diesem Leitfaden handelt es sich um empfohlene Optimierungen, nicht um Anforderungen.

Die Informationen in diesem Leitfaden gelten für Windows 10 Version 2004 Build 19041.

Die wichtigsten Prinzipien zur Optimierung der Leistung von Windows 10 in einer virtuellen Desktopumgebung bestehen darin, Grafikneuzeichnungen und -effekte sowie Hintergrundaktivitäten ohne großen Nutzen für die VDI-Umgebung zu minimieren und laufende Prozesse generell auf das absolute Minimum zu reduzieren. Ein sekundäres Ziel ist, den Verbrauch von Speicherplatz auf dem Datenträger im Basisimage auf ein Minimum zu reduzieren. Bei Implementierungen virtueller Desktops kann die kleinstmögliche Basisimagegröße („goldene“ Imagegröße) die Arbeitsspeicherauslastung auf dem Hostsystem leicht reduzieren und ebenso eine geringfügige Reduzierung der gesamten Netzwerkvorgänge bewirken, die erforderlich sind, um das Desktopimage für den Benutzer bereitzustellen.

Optimierungen sollten die Benutzerfreundlichkeit nicht beeinträchtigen. Jede Optimierungseinstellung wurde sorgfältig darauf geprüft, dass die Benutzerfreundlichkeit nicht verringert wird.

> [!NOTE]
> Die Einstellungen in diesem Artikel können auf andere Windows 10-Installationen (z. B. Version 1909), physische Geräte oder andere virtuelle Computer angewendet werden. Keine der Empfehlungen in diesem Artikel wirkt sich auf die Unterstützung von Windows 10 in einer virtuellen Desktopumgebung aus.

## <a name="vdi-optimization-principles"></a>Prinzipien der VDI-Optimierung

Eine vollständige virtuelle Desktopumgebung stellt einem Computerbenutzer über ein Netzwerk eine komplette Desktopsitzung einschließlich Anwendungen zur Verfügung. Der Netzwerkbereitstellungsmechanismus kann ein lokales Netzwerk, das Internet oder beides sein. Einige Implementierungen virtueller Desktopumgebungen verwenden ein Basis-Betriebssystemimage, das dann die Grundlage für die Desktops bildet, die den Benutzern anschließend bereitgestellt werden. Es gibt verschiedene Implementierungen virtueller Desktops wie „Persistent“, „Nicht persistent“ und „Desktopsitzung“. Die persistente Implementierung speichert Änderungen am VDI-Desktopbetriebssystem sitzungsübergreifend. Die nicht persistente Implementierung speichert die Änderungen am VDI-Desktopbetriebssystem nicht, die in einer Sitzung vorgenommen werden. Für den Benutzer unterscheidet sich dieser Desktop kaum von anderen virtuellen oder physischen Geräten, außer dass über ein Netzwerk auf ihn zugegriffen wird.

Die Optimierungseinstellungen können auf einem Referenzcomputer durchgeführt werden. Eine virtueller Computer (VM) ist ein idealer Ort, um die VM zu erstellen, da unter anderem der Status gespeichert und Prüfpunkte sowie Sicherungen erstellt werden können. Auf der Basis-VM wird eine Standardinstallation des Betriebssystems ausgeführt. Diese Basis-VM wird dann unter anderem durch das Entfernen nicht benötigter Apps, das Installieren von Windows-Updates und anderer Updates, das Löschen temporärer Dateien und das Anwenden von Einstellungen optimiert.

Es gibt auch andere virtuelle Desktoptechnologien, z. B. Remotedesktopsitzung (RDS) und den kürzlich veröffentlichten [Windows Virtual Desktop](https://azure.microsoft.com/services/virtual-desktop/)-Dienst in Microsoft Azure. Eine ausführliche Erläuterung dieser Technologien sprengt den Rahmen dieses Artikels. Dieser Artikel konzentriert sich auf die Einstellungen des Windows-Basisimages, ohne auf andere Faktoren in der Umgebung wie die Optimierung der Hosthardware zu einzugehen.

Die Sicherheit und Stabilität von Produkten und Diensten zählen für Microsoft zu den höchsten Prioritäten. Die Sicherheit gestaltet sich bei virtuellen Desktops nur geringfügig anders als bei physischen Geräten. Unternehmenskunden können die integrierten Windows-Dienste von Windows-Sicherheit nutzen. Diese App umfasst eine Suite von Diensten, die mit oder ohne Internetverbindung funktionieren. Für virtuelle Desktopumgebungen, die nicht mit dem Internet verbunden sind, können die Sicherheitssignaturen proaktiv mehrmals täglich heruntergeladen werden, da Microsoft möglicherweise mehrere Signaturupdates pro Tag veröffentlicht. Diese Signaturen können dann den virtuellen Desktopgeräten zur Verfügung gestellt und für die Installation während der Produktion geplant werden – unabhängig davon, ob sie persistent oder nicht persistent sind. Auf diese Weise ist der VM-Schutz so aktuell wie möglich.

Es gibt einige Sicherheitseinstellungen, die nicht auf virtuelle Desktopumgebungen anwendbar und nicht mit dem Internet verbunden sind. Daher sind diese nicht für die Cloudsicherheit geeignet. Es gibt noch andere Einstellungen, die gängige Windows-Geräte nutzen können, z. B. Cloudoptionen oder den Microsoft Store. Durch das Entfernen des Zugriffs auf nicht verwendete Features werden der Speicherbedarf, die Netzwerkbandbreite und die Angriffsfläche verringert.

Für Windows 10 gilt ein monatlicher Updaterhythmus. In einigen Fällen steuern die Administratoren virtueller Desktops den Updatevorgang durch das Herunterfahren von VMs auf der Basis eines Master- oder Goldimages. Sie entsiegeln dieses schreibgeschützte Image, patchen es, versiegeln es dann erneut und stellen es wieder in der Produktion bereit. Daher müssen virtuelle Desktopgeräte Windows Update nicht überprüfen. In anderen Fällen erfolgt das Patchen jedoch auch auf gewöhnliche Weise, zum Beispiel bei persistenten persönlichen virtuellen Desktopgeräten. Manchmal kann Windows Update genutzt werden. Manchmal kann Intune genutzt werden. In bestimmten Fällen wird auch Microsoft Endpoint Configuration Manager (früher SCCM) verwendet, um Updates und andere Paketbereitstellungen zu verarbeiten. Die Wahl des geeigneten Updateansatzes für virtuelle Desktopgeräte liegt bei der jeweiligen Organisation. Dieser soll den Verwaltungsaufwand reduzieren.

Die lokalen Richtlinieneinstellungen sowie viele weitere Einstellungen in diesem Leitfaden können mit domänenbasierten Richtlinien überschrieben werden. Es wird empfohlen, die Richtlinieneinstellungen sorgfältig durchzugehen und diejenigen zu entfernen oder nicht zu verwenden, die nicht erwünscht oder nicht für die Umgebung geeignet sind. Durch die in diesem Dokument aufgeführten Einstellungen soll das bestmögliche Gleichgewicht für Leistungsoptimierungen in virtuellen Desktopumgebungen erzielt werden, während die Benutzerfreundlichkeit erhalten bleibt.

> [!NOTE]
> Auf GitHub.com sind Skripts verfügbar, die die hier dokumentierten Aufgaben erledigen. Sie finden die Optimierungsskripts unter [https://github.com/The-Virtual-Desktop-Team/Virtual-Desktop-Optimization-Tool](https://github.com/The-Virtual-Desktop-Team/Virtual-Desktop-Optimization-Tool). Dieses Skript wurde so konzipiert, dass es einfach an Ihre Umgebung und Ihre Anforderungen angepasst werden kann. Der Hauptcode ist in PowerShell, und die Arbeit erfolgt durch das Aufrufen von Eingabedateien (Nur-Text, jetzt JSON) und die Exportdateien des Tools für lokale Gruppenrichtlinienobjekte (LGPO). Diese Textdateien enthalten unter anderem Listen mit den zu entfernenden Apps und den Diensten, die deaktiviert werden sollen. Wenn Sie nicht möchten, dass eine bestimmte App entfernt oder ein bestimmter Dienst deaktiviert wird, können Sie die entsprechende Textdatei bearbeiten und das unerwünschte Element entfernen. Schließlich werden lokale Richtlinieneinstellungen exportiert, die auf die Computer in Ihrer Umgebung importiert werden können. Es wird empfohlen, manche Einstellungen innerhalb des Basisimages zu verwenden, anstatt sie durch die Gruppenrichtlinie anzuwenden, da einige Einstellungen beim nächsten Neustart oder der ersten Verwendung der Komponente wirksam werden.

### <a name="persistent-virtual-desktop-environments"></a>Persistente virtuelle Desktopumgebungen

Die Grundlage bildet ein persistenter virtueller Desktop: ein Gerät, das den Betriebssystemzustand zwischen Neustarts speichert. Andere Softwareschichten der virtuellen Desktoplösung bieten den Benutzern einen einfachen und nahtlosen Zugriff auf die ihnen zugewiesenen VMs, der oft mit einer Single-Sign-On-Lösung erfolgt.

Es gibt mehrere verschiedene Implementierungen von persistenten virtuellen Desktops.

- Herkömmliche VMs, bei denen die VM über eine eigene virtuelle Festplattendatei verfügt, starten normal und speichern Änderungen sitzungsübergreifend. Der Unterschied besteht darin, wie der Benutzer auf diese VM zugreift. Möglicherweise ist ein Webportal vorhanden, bei dem sich der Benutzer anmeldet und dann automatisch zu einem oder mehreren virtuellen Desktopgeräten weitergeleitet wird, die diesem zugewiesen sind.
- Imagebasierte persistente VMs (optional mit persönlichen virtuellen Datenträgern): In dieser Art der Implementierung ist ein Basis-/Goldimage auf einem oder mehreren Hostservern vorhanden. Eine VM wird erstellt, und ein oder mehrere virtuelle Datenträger werden erstellt und dieser Festplatte zur dauerhaften Speicherung zugewiesen.
  - Wenn der virtuelle Computer gestartet wird, wird eine Kopie des Basisimages in den Arbeitsspeicher dieses virtuellen Computers gelesen. Gleichzeitig wird ein persistenter virtueller Datenträger dieser VM zugeordnet, wobei etwaige frühere Betriebssystemveränderungen durch einen komplexen Prozess zusammengeführt werden.
  - Änderungen wie Schreibvorgänge in Protokollen und Ereignisprotokollen werden an den virtuellen Datenträger mit Lese-/Schreibzugriff weitergeleitet, der der VM zugewiesen ist.
  - Unter diesen Umständen kann die Wartung von Betriebssystem und Apps mit herkömmlicher Wartungssoftware wie Windows Server Update Services oder anderen Verwaltungstechnologien normal erfolgen.
- Der Unterschied zwischen einem persistenten virtuellen Desktopgerät und einem herkömmlichen virtuellen Desktopgerät ist die Beziehung zum Master- bzw. Goldimage. Zu einem bestimmten Zeitpunkt müssen Updates auf den Master angewendet werden. An diesem Punkt müssen Organisationen entscheiden, wie persistente Änderungen des Benutzers verarbeitet werden. In einigen Fällen wird der Datenträger mit den Benutzeränderungen verworfen oder zurückgesetzt. Es ist auch möglich, die vom Benutzer vorgenommenen Änderungen durch monatliche Qualitätsupdates beizubehalten und die Basis nach einem Featureupdate zurückzusetzen.

### <a name="non-persistent-virtual-desktop-environments"></a>Nicht persistente virtuelle Desktopumgebungen

Wenn eine nicht persistente Implementierung virtueller Desktops auf einem Basis- oder Goldimage basiert, werden die Optimierungen meist im Basisimage und dann über lokale Einstellungen und Richtlinien vorgenommen.

Bei imagebasierten, nicht persistenten virtuellen Desktopumgebungen ist das Basisimage schreibgeschützt. Wenn ein nicht persistentes virtuelles Desktopgerät gestartet wird, wird eine Kopie des Basisimages zur VM gestreamt. Aktivitäten, die während des Startvorgangs und danach bis zum nächsten Neustart auftreten, werden an einen temporären Speicherort umgeleitet. Normalerweise werden den Benutzern Netzwerkspeicherorte zur Verfügung gestellt, um ihre Daten zu speichern. In einigen Fällen wird das Profil des Benutzers mit der Standard-VM zusammengeführt, um dem Benutzer seine Einstellungen zur Verfügung zu stellen.

Ein wichtiger Aspekt von nicht persistenten virtuellen Desktops, die auf einem einzigen Image basieren, ist die Wartung. Updates für das Betriebssystem und dessen Komponenten werden in der Regel ein Mal pro Monat bereitgestellt. Bei der imagebasierten virtuellen Desktopumgebung muss eine Reihe von Prozessen ausgeführt werden, um Updates auf einem Image zu installieren:

- Alle VMs auf einem bestimmten Host, die vom Basisimage abgeleitet sind, müssen heruntergefahren oder deaktiviert werden. Dies bedeutet, dass die Benutzer auf andere virtuelle Computer umgeleitet werden.

- In einigen Implementierungen wird das als Wartung (Draining) bezeichnet. Wenn die VM oder der Sitzungshost in den Wartungsmodus versetzt wird, werden keine neuen Anforderungen mehr akzeptiert. Benutzer, die derzeit mit dem Gerät verbunden sind, können es jedoch weiterhin nutzen.

- Sobald sich der letzte Benutzer im Wartungsmodus vom Gerät abgemeldet hat, ist das Gerät für Wartungsvorgänge bereit.
- Das Basisimage wird anschließend geöffnet und gestartet. Alle Wartungsaktivitäten wie Betriebssystemupdates, .NET-Updates oder App-Updates werden dann ausgeführt.
- Alle neuen Einstellungen, die angewendet werden müssen, werden zu diesem Zeitpunkt angewendet.
- Jegliche sonstige Wartung wird zu diesem Zeitpunkt durchgeführt.
- Das Basisimage wird anschließend heruntergefahren.
- Das Basisimage wird versiegelt und so eingestellt, dass es wieder in die Produktion geht.
- Benutzer dürfen sich wieder anmelden.

> [!NOTE]
> Windows 10 führt in regelmäßigen Abständen automatisch eine Reihe von Wartungsaufgaben durch. Eine geplante Aufgabe wird standardmäßig jeden Tag um 3:00 Uhr ausgeführt. Diese geplante Aufgabe führt eine Liste von Aufgaben einschließlich der Windows Update-Bereinigung durch. Du kannst alle Kategorien der Wartung anzeigen, die automatisch mit dem folgenden PowerShell-Befehl ausgeführt werden:
>
> ```powershell
> Get-ScheduledTask | Where-Object {$_.Settings.MaintenanceSettings}
> ```

Eine der Herausforderungen bei nicht dauerhaften virtuellen Desktops besteht darin, dass beim Abmelden eines Benutzers fast die gesamte Betriebssystemaktivität verworfen wird. Das Profil und/oder der Status des Benutzers können an einem zentralen Ort gespeichert werden, aber die VM selbst verwirft fast alle Änderungen, die seit dem letzten Start vorgenommen wurden. Daher sind Optimierungen, die für einen Windows-Computer bestimmt sind, der den Zustand von einer Sitzung zur nächsten speichert, nicht anwendbar.

Je nach Architektur des virtuellen Desktopgeräts sind PreFetch, SuperFetch und Ähnliches von einer Sitzung zur nächsten nicht hilfreich, da alle Optimierungen beim Neustart der VM verworfen werden. Die Indizierung kann eine teilweise Verschwendung von Ressourcen sein, ebenso wie alle Festplattenoptimierungen, z. B. die herkömmliche Defragmentierung.

> [!NOTE]
> Wenn Sie ein Image mithilfe von Virtualisierung vorbereiten und während dieses Prozesses eine Internetverbindung besteht, sollten Sie Featureupdates bei der ersten Anmeldung aufschieben, indem Sie zu **Einstellungen** > **Windows Update** navigieren.

### <a name="to-sysprep-or-not-sysprep"></a>Sysprep – ja oder nein?

Windows 10 verfügt über eine integrierte Funktion namens [Systemvorbereitungstool](/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview), die auch als Sysprep bekannt ist. Mit dem Sysprep-Tool wird ein benutzerdefiniertes Windows 10-Image für die Duplizierung vorbereitet. Der Sysprep-Prozess stellt sicher, dass das resultierende Betriebssystem für den Einsatz in der Produktion eindeutig ist.

Es gibt Gründe, die für und gegen die Ausführung von Sysprep sprechen. Bei virtuellen Desktopumgebungen möchten Sie möglicherweise über die Möglichkeit verfügen, das Standardbenutzerprofil anzupassen, das als Profilvorlage für nachfolgende Benutzer verwendet wird, die sich mit diesem Image anmelden. Möglicherweise möchten Sie bestimmte Apps installieren, aber auch dazu in der Lage sein, die Einstellungen pro App zu steuern.

Die Alternative ist, eine Standard-ISO-Datei für die Installation zu verwenden, möglicherweise unter Verwendung einer Antwortdatei für unbeaufsichtigte Installationen, und eine Aufgabensequenz für die Installation von Anwendungen oder deren Entfernen. Du kannst auch eine Aufgabensequenz verwenden, um lokale Richtlinieneinstellungen im Image festzulegen, vielleicht mit dem Tool [Local Group Policy Object Utility (LGPO)](/archive/blogs/secguide/lgpo-exe-local-group-policy-object-utility-v1-0) (Lokales Gruppenrichtlinienobjekt (Hilfsprogramm)).

Weitere Informationen über die Imagevorbereitung finden Sie unter [Vorbereiten einer Windows-VHD oder -VHDX zum Hochladen in Azure](/azure/virtual-machines/windows/prepare-for-upload-vhd-image).

### <a name="supportability"></a>Support-Fähigkeit

Immer, wenn Windows-Standardwerte geändert werden, entstehen Fragen bezüglich der Support-Fähigkeit. Sobald ein Image für einen virtuellen Desktop (VM oder Sitzung) angepasst wird, muss jede am Image vorgenommene Änderung in einem Änderungsprotokoll nachverfolgt werden. Wenn eine Problembehandlung durchgeführt werden muss, kann ein Image oft in einem Pool isoliert und zur Problemanalyse konfiguriert werden. Sobald ein Problem bis zur Grundursache nachverfolgt wurde, kann diese Änderung zunächst in der Testumgebung und schließlich in der Produktionsworkload ausgeführt werden.

Dieses Dokument vermeidet absichtlich die Themen Systemdienste, Richtlinien oder Tasks, die sich auf die Sicherheit auswirken. Anschließend folgt die Windows-Wartung. Die Möglichkeit, Images für virtuelle Desktops außerhalb von Wartungsfenstern zu warten, wird entfernt, da in Wartungsfenstern die meisten Wartungsereignisse in virtuellen Desktopumgebungen stattfinden, mit Ausnahme von Sicherheitssoftwareupdates. Microsoft hat Richtlinien für die Windows-Sicherheit in virtuellen Desktopumgebungen veröffentlicht. Diese finden Sie hier:

**Microsoft:** [Bereitstellungsleitfaden für Windows Defender Antivirus in einer VDI-Umgebung (Virtual Desktop Infrastructure)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/deployment-vdi-windows-defender-antivirus)

Berücksichtigen Sie die Unterstützbarkeit, wenn Sie Änderungen an den Standardeinstellungen von Windows vornehmen. Manchmal treten schwierig zu lösende Probleme auf, wenn Änderungen an Systemdiensten, Richtlinien oder geplanten Aufgaben vorgenommen werden (z. B. für Härtung, „Erleichterung“ und so weiter). Informationen zu den aktuellen bekannten Problemen bezüglich geänderter Standardeinstellungen findest du in der Microsoft Knowledge Base. Die Anleitungen in diesem Dokument und das zugehörige Skript auf GitHub werden im Hinblick auf bekannte Probleme (sofern diese auftreten) aktualisiert. Darüber hinaus stehen Ihnen mehrere Möglichkeiten zur Verfügung, Probleme an Microsoft zu melden.

Sie können die Suchparameter `"start value" site:support.microsoft.com` mit Ihrer bevorzugten Suchmaschine verwenden, um nach bekannten Problemen hinsichtlich der Standardstartwerte für Dienste zu suchen.

Möglicherweise wirst du feststellen, dass in diesem Dokument und den zugehörigen Skripts auf GitHub keine Standardberechtigungen geändert werden. Wenn du deine Sicherheitseinstellungen erhöhen möchten, beginnst du mit dem Projekt, das als **AaronLocker** bezeichnet wird. Weitere Informationen finden Sie in der [Übersicht über „AaronLocker“](https://github.com/microsoft/AaronLocker).

### <a name="virtual-desktop-optimization-categories"></a>Kategorien für die Optimierung von virtuellen Desktops

- UWP-App-Bereinigung (Universal Windows Platform, universelle Windows-Plattform)
- Bereinigung optionaler Features
- Lokale Richtlinieneinstellungen
- Systemdienste
- Geplante Aufgaben
- Anwenden von Windows- und anderen Updates
- Automatische Windows-Ablaufverfolgungen
- Windows Defender-Optimierung mit VDI
- Clientnetzwerk-Leistungsoptimierung durch Registrierungseinstellungen
- Zusätzliche Einstellungen aus dem Leitfaden „Windows Restricted Traffic Limited Functionality Baseline“ (Baseline für die begrenzte Funktionalität des eingeschränkten Windows-Datenverkehrs)
- Datenträgerbereinigung

### <a name="universal-windows-platform-uwp-application-cleanup"></a>Anwendungsbereinigung für UWP (Universelle Windows-Plattform)

Eines der Ziele eines Images für einen virtuellen Desktop besteht darin, in Bezug auf den persistenten Speicher möglichst einfach zu sein. Eine Möglichkeit, die Imagegröße zu reduzieren, besteht darin, UWP-Anwendungen zu entfernen, die nicht in der Umgebung verwendet werden. Unter den UWP-Anwendungen gibt es die wichtigsten, auch als Nutzlast bezeichneten Anwendungsdateien. Im Profil jedes Benutzers wird eine kleine Menge an Daten für anwendungsspezifische Einstellungen gespeichert. Auch im Profil „Alle Benutzer“ ist eine kleine Menge an Daten vorhanden.

Darüber hinaus werden alle UWP-Apps entweder auf Benutzer- oder Computerebene registriert. Dies erfolgt für das Gerät nach dem Start und für den Benutzer nach der Anmeldung. Die UWP-Apps, die das Startmenü und die Windows-Shell enthalten, führen verschiedene Aufgaben während oder nach der Installation durch. Dies geschieht nochmal, wenn ein Benutzer sich zum ersten Mal anmeldet, und in geringerem Umfang bei nachfolgenden Anmeldungen. Für alle UWP-Apps werden gelegentlich Auswertungen durchgeführt, zum Beispiel:

- Muss die App auf die neueste Version aktualisiert werden?
- Für die App stehen möglicherweise Livekacheldaten zum Download zur Verfügung, wenn diese an das Startmenü angeheftet ist.
- Verfügt die App über einen Cache von Daten, der aktualisiert werden muss (z. B. Karten oder Wetter)?
- Verfügt die App über dauerhafte Daten vom Profil des Benutzers, die bei der Anmeldung angezeigt werden müssen (z. B. Kurznotizen)?

Mit einer Standardinstallation von Windows 10 können möglicherweise nicht alle UWP-Apps von einer Organisation verwendet werden. Wenn diese Apps entfernt werden, müssen daher weniger Auswertungen, weniger Zwischenspeicherung und mehr durchgeführt werden. Die zweite Methode hierfür besteht darin, Windows anzuweisen, „Anwenderfeatures“ zu deaktivieren. Dadurch wird die Aktivität des Stores reduziert, die dadurch verursacht wird, dass für jeden Benutzer überprüft werden muss, welche Apps installiert sind, welche Apps verfügbar sind und dass dann einige UWP-Apps heruntergeladen werden. Die Leistungseinsparungen können erheblich sein, wenn es Hunderte oder gar Tausende Benutzer gibt, die alle ungefähr zur selben Zeit Arbeiten oder sogar in verschiedenen Zeitzonen rund um die Uhr mit der Arbeit beginnen.

Konnektivität und Timing sind wichtige Faktoren, wenn es um die UWP-App-Bereinigung geht. Wenn Sie Ihr Basisimage auf einem Gerät ohne Netzwerkverbindung bereitstellen, kann Windows 10 keine Verbindung mit dem Microsoft Store herstellen, Apps herunterladen und diese installieren, während Sie diese deinstallieren. Dies ist möglicherweise eine gute Strategie, um dir die Anpassung des Image zu ermöglichen und dann in einer späteren Phase zu aktualisieren, was vom Imageerstellungsprozess verbleibt.

Wenn Sie die WIM-Basisdatei ändern, die Sie zum Installieren von Windows 10 verwenden, und nicht benötigte UWP-Apps vor der Installation aus der WIM-Datei entfernen, werden die Apps nicht von Anfang an installiert und die erforderliche Zeit für nachfolgende Profilerstellungen ist kürzer. Im späteren Verlauf dieses Abschnitts finden Sie einen Link zu Informationen über das Entfernen von UWP-Apps aus Ihrer WIM-Installationsdatei.

Eine gute Strategie für die virtuelle Desktopumgebung besteht darin, die Apps bereitzustellen, die im Basisimage enthalten sein sollen, und dann den Zugriff auf den Microsoft Store einzuschränken oder zu blockieren. Store-Apps werden auf normalen Computern in regelmäßigen Abständen im Hintergrund aktualisiert. Die UWP-Apps können während des Wartungsfensters aktualisiert werden, wenn andere Updates angewendet werden.

#### <a name="delete-the-payload-of-uwp-apps"></a>Löschen der Nutzlast der UWP-Apps

UWP-Apps, die nicht benötigt werden, sind weiterhin im Dateisystem vorhanden und verbrauchen eine kleine Menge an Speicherplatz. Für Apps, die nie benötigt werden, kann die Nutzlast unerwünschter UWP-Apps mit PowerShell-Befehlen aus dem Basisimage entfernt werden. Wenn Sie mithilfe der später in diesem Abschnitt bereitgestellten Links die Nutzlasten von UWP-Apps aus der WIM-Installationsdatei entfernen, können Sie von Anfang an mit einer sehr kurzen Liste von UWP-Apps beginnen.

Führen Sie den folgenden Befehl aus, um die bereitgestellten UWP-Apps eines aktiven Betriebssystems aufzuführen. Gehen Sie wie in der folgenden gekürzten Beispielausgabe aus PowerShell vor:

```powershell
Get-AppxProvisionedPackage -Online

DisplayName  : Microsoft.3DBuilder
Version      : 13.0.10349.0  
Architecture : neutral
ResourceId   : \~
PackageName  : Microsoft.3DBuilder_13.0.10349.0_neutral_\~_8wekyb3d8bbwe
Regions      :

DisplayName  : Microsoft.Appconnector
Version      : 2015.707.550  
Architecture : neutral
ResourceId   : \~
PackageName  : Microsoft.Appconnector_2015.707.550.0_neutral_\~_8wekyb3d8bbwe
Regions      :
...
```

UWP-Apps, die für ein System bereitgestellt werden, können während der Betriebssysteminstallation im Rahmen einer Tasksequenz entfernt werden. Dies ist auch nach der Installation des Betriebssystems möglich. Hierbei könnte es sich um Ihre bevorzugte Methode handeln, da sie einen modularen Gesamtprozess für die Erstellung oder Wartung eines Images bietet. Sobald du die Skripts entwickelst, bearbeite ein bestehendes Skript, wenn sich in einem späteren Build etwas ändert, anstatt den Prozess von Grund auf zu wiederholen.

Weitere Informationen finden Sie in den folgenden Ressourcen:

- [Removing Windows 10 in-box apps during a task sequence](/archive/blogs/mniehaus/removing-windows-10-in-box-apps-during-a-task-sequence) (Entfernen von mitgelieferten Windows 10-Apps während einer Aufgabensequenz)
- [Entfernen integrierter Apps aus der WIM-Datei für Windows 10 mithilfe von PowerShell Version 1.3](https://gallery.technet.microsoft.com/Removing-Built-in-apps-65dc387b)
- Keeping apps from coming back when deploying the feature update[ (Windows 10 1607: Verhindern der Rückkehr von Apps bei der Bereitstellung des Featureupdates)
- [Removing Windows 10 in-box apps during a task sequence](https://blogs.technet.microsoft.com/mniehaus/2015/11/11/removing-windows-10-in-box-apps-during-a-task-sequence/) (Entfernen von mitgelieferten Windows 10-Apps während einer Aufgabensequenz)

Führen Sie anschließend den folgenden PowerShell-Befehl aus, um Nutzlasten von UWP-Apps zu entfernen:

```powershell
Remove-AppxProvisionedPackage -Online - PackageName MyAppxPackage
```

Zuletzt sollten Sie bei diesem Thema beachten, dass jede UWP-App auf ihre Anwendbarkeit in jeder spezifischen Umgebung geprüft werden sollte. Wenn Sie eine Standardinstallation von Windows 10, Version 2004 durchführen, sollten Sie beachten, welche Apps ausgeführt werden und Arbeitsspeicher verbrauchen. Beispielsweise sollten Sie es in Betracht ziehen, Apps zu entfernen, die automatisch gestartet werden oder automatisch Informationen im Startmenü anzeigen (z. B. Wetter und Nachrichten) und in Ihrer Umgebung nicht nützlich sind.

> [!NOTE]
> Wenn Sie Skripts von GitHub verwenden, können Sie mühelos steuern, welche Apps entfernt werden, bevor das Skript ausgeführt wird. Suchen Sie nach dem Herunterladen der Skriptdateien die Datei „AppxPackages.json“, bearbeiten Sie diese, und entfernen Sie Einträge für Apps, die Sie behalten möchten, wie den Rechner oder die Kurznotizen.

## <a name="windows-optional-features-cleanup"></a>Bereinigung optionaler Features von Windows

### <a name="managing-optional-features-with-powershell"></a>Verwalten optionaler Features mit PowerShell

Microsoft: [Windows 10: Verwalten optionaler Features mit PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/39386.windows-10-managing-optional-features-with-powershell.aspx)

Du kannst optionale Windows-Features mit PowerShell verwalten. Liste die aktuell installierten Windows-Features mit folgendem PowerShell-Befehl auf:

```powershell
Get-WindowsOptionalFeature -Online
```

Mithilfe von PowerShell kann ein aufgelistetes optionales Windows-Feature wie im folgenden Beispiel gezeigt aktiviert oder deaktiviert werden:

```powershell
Enabled-WindowsOptionalFeature -Online -FeatureName "DirectPlay" -All
```

Mit dem folgenden Beispielbefehl wird der Windows Media Player im Image für einen virtuellen Desktop deaktiviert:

```powershell
Disable-WindowsOptionalFeature -Online -FeatureName "WindowsMediaPlayer"
```

Als Nächstes möchten Sie möglicherweise das Windows Media Player-Paket entfernen. Im folgenden Beispielbefehl wird gezeigt, wie Sie dies tun:

```powershell

PS C:\> Get-WindowsPackage -Online -PackageName *media*

PackageName              : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.19041.153
Applicable               : True
Copyright                : Copyright (c) Microsoft Corporation. All Rights Reserved
Company                  :
CreationTime             :
Description              : Play audio and video files on your local machine and on the Internet.
InstallClient            : DISM Package Manager Provider
InstallPackageName       : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.19041.153.mum
InstallTime              : 5/11/2020 5:43:37 AM
LastUpdateTime           :
DisplayName              : Windows Media Player
ProductName              : Microsoft-Windows-MediaPlayer-Package
ProductVersion           :
ReleaseType              : OnDemandPack
RestartRequired          : Possible
SupportInformation       : http://support.microsoft.com/?kbid=777777
PackageState             : Installed
CompletelyOfflineCapable : Undetermined
CapabilityId             : Media.WindowsMediaPlayer~~~~0.0.12.0
Custom Properties        :

Features                 : {}
```

Wenn Sie das Windows Media Player-Paket entfernen möchten (um etwa 60 MB Speicherplatz freizugeben), können Sie den folgenden Befehl ausführen:

```powershell
PS C:\Windows\system32> Remove-WindowsPackage -PackageName Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.19041.153 -Online

Path          :
Online        : True
RestartNeeded : False
```

### <a name="enable-of-disabling-windows-features-using-dism"></a>Aktivieren und Deaktivieren von Windows-Features mit DISM

Mit dem integrierten Tool „Dism.exe“ kannst du optionale Windows-Features auflisten und steuern. Bei einer Tasksequenz zur Installation des Betriebssystems kann ein Skript „Dism.exe“ entwickelt und ausgeführt werden. Die entsprechende Windows-Technologie wird als Features bei Bedarf bezeichnet. Weitere Informationen zu Features bei Bedarf unter Windows finden Sie im folgenden Artikel:

Microsoft: [Features bei Bedarf](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)

### <a name="default-user-settings"></a>Standardbenutzereinstellungen

Sie können die Windows-Registrierungsdatei unter `C:\Users\Default\NTUSER.DAT` anpassen. Jegliche Einstellungsänderungen, die Sie an dieser Datei vornehmen, werden auf jegliche Benutzerprofile angewendet, die anschließend über einen Computer erstellt werden, auf dem dieses Image ausgeführt wird. Sie können steuern, welche Einstellungen Sie auf das Standardbenutzerprofil anwenden möchten, indem Sie die Datei **DefaultUserSettings.txt** bearbeiten.

Sie können eine Volltonfarbe anstelle des Standardhintergrundbilds von Windows 10 als Standardhintergrund festlegen, um die Übertragung von grafischen Daten über die virtuelle Desktopinfrastruktur zu reduzieren. Sie können für den Anmeldebildschirm ebenfalls eine Volltonfarbe festlegen und den undurchsichtigen Unschärfeeffekt bei der Anmeldung deaktivieren.

Die folgenden Einstellungen werden auf die Registrierungsstruktur für das Standardbenutzerprofil angewendet, um hauptsächlich Animationen zu verringern. Wenn einige oder alle dieser Einstellungen unerwünscht sind, löschen Sie die Einstellungen, die nicht auf neue Benutzerprofile angewendet werden sollen mithilfe dieses Bilds. Das Ziel dieser Einstellungen besteht darin, die folgenden äquivalenten Einstellungen zu aktivieren:

- Schatten unter dem Mauszeiger anzeigen
- Schatten unter Fenstern anzeigen
- Glatte Kanten für Schriftarten

![Screenshot: Menü mit Leistungsoptionen mit den relevanten Elementen ausgewählt](media/performance-options.png)

In dieser Version der Einstellungen gibt es eine neue Methode zum Deaktivieren der folgenden zwei Datenschutzeinstellungen für alle Benutzerprofile, die Sie nach der Optimierung erstellt haben:

- „Webseiten den Zugriff auf die eigene Sprachliste gestatten, um die Anzeige lokal relevanter Inhalte zu ermöglichen“
- „Vorgeschlagene Inhalte in der Einstellungs-App anzeigen”

![Screenshot: Fenster „Datenschutzeinstellungen“ Die zwei deaktivierten Einstellungen werden rot hervorgehoben.](media/privacy-settings.png)

Im Folgenden werden die Optimierungseinstellungen aufgeführt, die für die Standardbenutzerprofil-Registrierungsstruktur zum Optimieren der Leistung angewendet wurden. Beachten Sie, dass dieser Vorgang durchgeführt wird, indem zunächst die Registrierungsstruktur des Standardbenutzerprofils (**NTUser.dat**) als kurzlebiger Schlüsselname **Temp** geladen wird und dann die unten aufgeführten Änderungen vorgenommen werden:

```regedit
Load HKLM\Temp C:\Users\Default\NTUSER.DAT
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
add "HKLM\Temp\Software\Microsoft\InputPersonalization" /v RestrictImplicitInkCollection /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\InputPersonalization" /v RestrictImplicitTextCollection /t REG_DWORD /d 1 /f
add "HKLM\Temp\Software\Microsoft\Personalization\Settings" /v AcceptedPrivacyPolicy /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\InputPersonalization\TrainedDataStore" /v HarvestContacts /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\UserProfileEngagement" /v ScoobeSystemSettingEnabled /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\UserProfileEngagement" /v ScoobeSystemSettingEnabled /t REG_DWORD /d 0 /f
add "HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\UserProfileEngagement" /v ScoobeSystemSettingEnabled /t REG_DWORD /d 0 /f
Unload HKLM\Temp
```

Vor kurzem wurde eine weitere Reihe von Standardbenutzereinstellungen hinzugefügt, um mehrere Windows-Apps am Starten und der Ausführung im Hintergrund zu hindern. Dies ist zwar auf einem einzelnen Gerät nicht ausschlaggebend, jedoch startet Windows 10 mehrere Prozesse für jede Benutzersitzung auf einem Gerät (Host). Beispiele hierfür sind die Skype-App und Microsoft Edge. Die enthaltenen Einstellungen verhindern die Ausführung mehrerer Apps im Hintergrund. Wenn Sie diese Funktionalität unverändert beibehalten möchten, löschen Sie einfach die Zeilen aus der Datei „DefaultUserSettings.txt“, die die App-Namen **Windows.Photos**, **SkypeApp**, **YourPhone** und/oder **MicrosoftEdge** enthalten.

### <a name="local-policy-settings"></a>Lokale Richtlinieneinstellungen

Viele Optimierungen für Windows 10 in einer virtuellen Desktopumgebung können mithilfe einer Windows-Richtlinie vorgenommen werden. Die in der Tabelle in diesem Abschnitt aufgeführten Einstellungen können lokal auf das Basis-/Goldimage angewendet werden. Wenn dann die entsprechenden Einstellungen nicht auf andere Weise (z. B. durch eine Gruppenrichtlinie) angegeben werden, würden die Einstellungen weiterhin gelten.

Beachten Sie, dass einige Entscheidungen möglicherweise auf die spezifischen Anforderungen der Umgebung basieren.

- Darf die virtuelle Desktopumgebung auf das Internet zugreifen?
- Ist die virtuelle Desktoplösung dauerhaft oder nicht?

Die folgenden Einstellungen wurden ausgewählt, weil sie nicht mit einer Einstellung in Konflikt stehen, die etwas mit der Sicherheit zu tun hat. Diese Einstellungen wurden ausgewählt, um Einstellungen zu entfernen oder Funktionen zu deaktivieren, die möglicherweise nicht auf virtuelle Desktopumgebungen angewendet werden können.

| Richtlinieneinstellung | Element | Untergeordnete Element | Mögliche Einstellung und Kommentare |
|--------------|----|--------|----------------------------|
| Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Windows-Einstellungen \\ Sicherheitseinstellungen | NICHT ZUTREFFEND | NICHT ZUTREFFEND | NICHT ZUTREFFEND |
| Netzwerklisten-Manager-Richtlinien | Alle Netzwerkeeigenschaften | Netzwerkadresse | **Benutzer kann Ort nicht ändern** (Dies wird festgelegt, um zu verhindern, dass die rechte Seite angezeigt wird, wenn ein neues Netzwerk erkannt wurde.) |
| Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Systemsteuerung | NICHT ZUTREFFEND | NICHT ZUTREFFEND |
| Systemsteuerung | Onlinetipps zulassen | NICHT ZUTREFFEND  | **Deaktiviert** („Einstellungen“ kontaktiert nicht die Inhaltsdienste von Microsoft zum Abrufen von Tipps und hilfreichen Informationen) |
| Systemsteuerung/Personalisierung | Ein bestimmtes Standardbild für den Sperr- und Anmeldebildschirm erzwingen | NICHT ZUTREFFEND | Aktiviert (Diese Einstellung ermöglicht es Ihnen, ein bestimmtes Standardbild für den Sperrbildschirm und die Anmeldung zu erzwingen, indem Sie den Pfad (Speicherort) der Bilddatei eingeben. Dasselbe Bild wird für den Sperr- und den Anmeldebildschirm verwendet. <p>Mit dieser Empfehlung werden die Bytes reduziert, die über das Netzwerk für virtuelle Desktopumgebungen übermittelt werden. Diese Einstellung kann für jede Umgebung entfernt oder angepasst werden.)|
|*Systemsteuerung/Regions- und Sprachoptionen/Handschriftanpassung|Automatisches Lernen deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, wird das automatische Lernen beendet und jegliche gespeicherten Daten werden gelöscht. Benutzer können diese Einstellung nicht in der Systemsteuerung konfigurieren)|
|Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Netzwerk|NICHT ZUTREFFEND|NICHT ZUTREFFEND|NICHT ZUTREFFEND|
|Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)|BITS-Peercaching zulassen| NICHT ZUTREFFEND |**Deaktiviert** (Diese Richtlinie bestimmt, ob das Peercaching des BITS-Diensts (Background Intelligent Transfer Service, Intelligenter Hintergrundübertragungsdienst) auf einem bestimmten Computer aktiviert ist.)|
|Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)|Verwendung des Windows Branch-Caches durch BITS-Client nicht zulassen|NICHT ZUTREFFEND|**Aktiviert** (Wenn diese Richtlinie aktiviert ist, verwendet der BITS-Client nicht den Windows Branch-Cache.)<p>Mit dieser Empfehlung werden virtuelle Desktopgeräte nicht für die Zwischenspeicherung von Inhalten verwendet, und die Geräte dürfen hierzu nicht die Netzwerkbandbreite verwenden.|
|Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)|Computer darf nicht als BITS-Peercachingclient fungieren|NICHT ZUTREFFEND|**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, verwendet der Computer nicht mehr das Peercaching des BITS-Diensts zum Herunterladen von Dateien. Dateien werden dann ausschließlich vom Ursprungsserver heruntergeladen.)|
Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)|Computer darf nicht als BITS-Peercachingserver fungieren|NICHT ZUTREFFEND|**Aktiviert** (Wenn diese Richtlinie aktiviert ist, werden heruntergeladene Dateien nicht mehr zwischengespeichert und Peers angeboten.)|
|BranchCache|BranchCache aktivieren|NICHT ZUTREFFEND|**Deaktiviert** (Wenn diese Option deaktiviert ist, ist BranchCache für alle Clientcomputer deaktiviert, für die die Richtlinie gilt.)|
|*Schriftarten|Schriftartenanbieter aktivieren|NICHT ZUTREFFEND|**Deaktiviert** (Wenn diese Einstellung deaktiviert ist, stellt Windows keine Verbindung mit einem Onlineschriftartenanbieter her und listet nur lokal installierte Schriftarten auf.)|
|Hotspotauthentifizierung|Hotspotauthentifizierung aktivieren| NICHT ZUTREFFEND |**Deaktiviert** (Diese Richtlinieneinstellung definiert, ob bei WLAN-Hotspots überprüft wird, ob das WISPr-Protokoll (Wireless Internet Service Provider roaming) unterstützt wird. Wenn diese Richtlinieneinstellung deaktiviert wird, wird bei WLAN-Hotspots nicht überprüft, ob diese das WISPr-Protokoll unterstützen, und Benutzer können sich nur über einen Webbrowser bei WLAN-Hotspots authentifizieren.)|
|Microsoft Peer-zu-Peer-Netzwerkdienste|Microsoft Peer-zu-Peer-Netzwerkdienste deaktivieren|NICHT ZUTREFFEND|**Aktiviert** (Diese Einstellung deaktiviert alle Microsoft Peer-zu-Peer-Netzwerkdienste, was dazu führt, dass alle abhängigen Anwendungen nicht mehr funktionieren. Wenn Sie diese Einstellung aktivieren, werden Peer-zu-Peer-Protokolle deaktiviert.)|
|Netzwerkverbindungs-Statusanzeige<p>(In diesem Abschnitt gibt es weitere Einstellungen, die in isolierten Netzwerken verwendet werden können.)|Passive Abrufe angeben|Passive Abrufe deaktivieren (**Kontrollkästchen**)|**Aktiviert** (Diese Richtlinieneinstellung ermöglicht es Ihnen, ein Verhalten für passive Abrufe anzugeben. NCSI ruft in einem regelmäßigen Intervall verschiedene Messungen für den Netzwerkstapel ab, um zu bestimmen, ob die Netzwerkkonnektivität unterbrochen wurde. Verwenden Sie die Optionen, um das Verhalten für passive Abrufe zu steuern.)<P>Das Deaktivieren der passiven NCIS-Abrufe kann die CPU-Arbeitsauslastung auf Servern und anderen Computern verbessern, deren Netzwerkkonnektivität statisch ist.|
|Offlinedateien|Die Funktion „Offlinedateien“ zulassen bzw. nicht zulassen|NICHT ZUTREFFEND|**Deaktiviert** (Diese Richtlinieneinstellung bestimmt, ob das Feature „Offlinedateien“ aktiviert ist. „Offlinedateien“ speichert eine Kopie der Netzwerkdateien auf dem Computer des Benutzers zur Verwendung, wenn der Computer nicht mit dem Netzwerk verbunden ist. Wenn diese Richtlinieneinstellung deaktiviert ist, ist das „Offlinedateien“-Feature deaktiviert, und Benutzer können es nicht aktivieren.)|
|*TCPIP-Einstellungen \ IPv6-Übergangstechnologien| Teredo-Status festlegen|Deaktivierter Zustand|**Aktiviert** (Wenn diese Einstellung aktiviert ist und auf „Deaktiviert“ festgelegt wird, sind für den Host keine Teredo-Schnittstellen verfügbar.)|
*WLAN-Dienst \ WLAN-Einstellungen|Zulassen, dass Windows automatisch Verbindungen mit vorgeschlagenen öffentlichen Hotspots, mit Netzwerken, die von Kontakten freigegeben werden und mit Hotspots herstellt, die kostenpflichtige Dienste anbieten.|NICHT ZUTREFFEND|**Deaktiviert** (Diese Richtlinieneinstellung bestimmt, ob Benutzer die folgenden WLAN-Einstellungen aktivieren können: „Mit vorgeschlagenen öffentlichen Hotspots verbinden“, „Mit den von meinen Kontakten freigegebenen Netzen verbinden“ und „Enable paid services“ (Kostenpflichtige Dienste aktivieren). Wenn diese Richtlinieneinstellung deaktiviert ist, werden „Mit vorgeschlagenen öffentlichen Hotspots verbinden“, „Mit den von meinen Kontakten freigegebenen Netzen verbinden“ und „Enable paid services“ (Kostenpflichtige Dienste aktivieren) deaktiviert, und Benutzer auf diesem Gerät werden davon abgehalten, diese Einstellungen zu aktivieren.)|
|WWAN-Dienst \ Mobilfunkdatenzugriff|Windows-Apps den Zugriff auf mobile Daten gestatten|Standard für alle Apps: **Verweigern erzwingen**|**Aktiviert** (Wenn Sie die Option „Verweigern erzwingen“ ausgewählt haben, dürfen Windows-Apps nicht auf Mobilfunkdaten zugreifen, und Benutzer können dies nicht ändern.)|
|Richtlinie für „Lokaler Computer“ \ Computerkonfiguration \ Administrative Vorlagen \ Startmenü und Taskleiste|NICHT ZUTREFFEND|NICHT ZUTREFFEND|
|*Benachrichtigungen|Netzwerkverwendung für Benachrichtigungen deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn Sie diese Richtlinieneinstellung aktivieren, können Anwendungen und Systemfeatures keine Benachrichtigungen von WNS über das Netzwerk oder mit Benachrichtigungen abfragenden APIs empfangen.)|
|Richtlinie für „Lokaler Computer“ \ Computerkonfiguration \ Administrative Vorlagen \ System| NICHT ZUTREFFEND | NICHT ZUTREFFEND |NICHT ZUTREFFEND|
|Geräteinstallation|Keinen Windows-Fehlerbericht senden, wenn ein Standardtreiber für ein Gerät installiert ist| NICHT ZUTREFFEND |**Aktiviert** (Wenn Sie diese Richtlinieneinstellung aktivieren, wird kein Fehlerbericht gesendet, wenn ein allgemeiner Treiber installiert wird.)|
|Geräteinstallation|Bei der Installation eines neuen Gerätetreibers keinen Systemwiederherstellungspunkt erstellen| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, erstellt Windows keinen Systemwiederherstellungspunkt, wenn normalerweise einer erstellt werden würde.)|
|Geräteinstallation|Abrufen von Gerätemetadaten aus dem Internet verhindern| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung ermöglicht es Ihnen, Windows davon abzuhalten, Gerätemetadaten aus dem Internet abzurufen. Wenn diese Richtlinieneinstellung aktiviert ist, ruft Windows keine Gerätemetadaten für installierte Geräte aus dem Internet ab. Diese Richtlinieneinstellung überschreibt die Einstellung im Dialogfeld „Geräteinstallationseinstellungen“ (Systemsteuerung > System und Sicherheit > System > Erweiterte Systemeinstellungen > Registerkarte „Hardware“).)|
|Geräteinstallation|Sprechblasen mit der Meldung „Neue Hardware gefunden“ während der Geräteinstallation deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung ermöglicht es Ihnen, „Neue Hardware gefunden“-Meldungen während der Geräteinstallation zu deaktivieren. Wenn Sie diese Richtlinieneinstellung aktivieren, werden „Neue Hardware gefunden“-Meldungen während Geräteinstallationen nicht angezeigt.)|
|Dateisystem \ NTFS|Optionen für die Erstellung von Kurznamen|Optionen für die Erstellung von Kurznamen Für alle Volumes deaktiviert|**Aktiviert** (Diese Einstellungen bieten Ihnen die Kontrolle darüber, ob Kurznamen bei der Dateierstellung generiert werden oder nicht. Für manche Anwendungen sind Kurznamen aus Kompatibilitätsgründen erforderlich, Kurznamen wirken sich jedoch negativ auf die Leistung des Systems aus. Wenn Kurznamen für alle Volumes deaktiviert werden, werden sie nie erzeugt.)|
|*Gruppenrichtlinie|Auf der Oberfläche dieses Geräts weiterarbeiten| NICHT ZUTREFFEND |**Deaktiviert** (Diese Richtlinieneinstellung bestimmt, ob das Windows-Gerät an geräteübergreifenden Funktionen beteiligt sein darf (Auf der Oberfläche dieses Geräts weiterarbeiten). Wenn Sie diese Richtlinie deaktivieren, kann dieses Gerät von anderen Geräten nicht erkannt werden und kann somit nicht an geräteübergreifenden Funktionen beteiligt sein.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Events.asp-Links der Ereignisanzeige deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung gibt an, ob Events.asp-Links für Ereignisse innerhalb der Ereignisanzeigenanwendung verfügbar sind.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Freigabe von Daten für die Handschriftanpassung deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Deaktiviert die Datenfreigabe für das Handschrifterkennungs-Anpassungstool.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Handschrifterkennungs-Fehlerberichterstattung deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Deaktiviert das Tool für die Fehlermeldung der Handschrifterkennung.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Knowledge Base-Suche des Hilfe- und Supportcenters deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung gibt an, ob Benutzer eine Microsoft Knowledge Base-Suche über das Hilfe- und Supportcenter durchführen können.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Verbindungs-Assistenten deaktivieren, wenn sich die URL-Verbindung auf microsoft.com bezieht| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung gibt an, ob der Assistent für den Internetzugang eine Verbindung zu Microsoft herstellen kann, um eine Liste der Internetdienstanbieter (Internet Service Providers, ISPs) herunterzuladen.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Internet-Download für die Assistenten „Webpublishing“ und „Onlinebestellung von Abzügen“ deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung legt fest, ob Windows eine Liste von Anbietern für die Assistenten zur Webveröffentlichung und Onlinebestellung herunterladen soll.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Internet-Dateizuordnungsdienst deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung legt fest, ob der Microsoft-Webdienst verwendet werden soll, um nach einer Anwendung zum Öffnen einer Datei mit einer unbehandelten Dateizuordnung zu suchen.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Registrierung deaktivieren, wenn sich die URL-Verbindung auf „Microsoft.com“ bezieht| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung legt fest, ob der Assistent für die Windows-Registrierung für die Onlineregistrierung eine Verbindung mit Microsoft.com herstellt.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Deaktivieren des Suchassistenten für Inhaltdateiupdates| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung legt fest, ob der Suchassistent während lokalen Suchvorgängen und Internetsuchvorgängen automatisch Inhaltsupdates herunterladen soll.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Aufgabe „Abzüge online bestellen“ für Bilder deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn Sie diese Richtlinieneinstellung aktivieren, wird die Aufgabe „Order Prints Online“ (Drucke online bestellen) aus den Picture Tasks (Bildaufgaben) in den Ordnern des Datei-Explorers entfernt.)|
Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Aufgabe „Im Web veröffentlichen“ für Dateien und Ordner deaktivieren| NICHT ZUTREFFEND |**Aktiviert* (Diese Richtlinieneinstellung legt fest, ob die Aufgaben „Datei im Web veröffentlichen“, „Ordner im Web veröffentlichen“ und „Ausgewählte Elemente im Web veröffentlichen“ in den Datei- und Ordneraufgaben in Windows-Ordnern verfügbar sind.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Programm zur Verbesserung der Benutzerfreundlichkeit von Windows deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Das Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP) von Windows sammelt Informationen zu Ihrer Hardwarekonfiguration und Ihrer Verwendung unserer Software und Dienste mit dem Ziel, Trends und Verwendungsmuster zu erkennen. Wenn Sie diese Richtlinieneinstellung aktivieren, wird das Programm zur Verbesserung der Benutzerfreundlichkeit für alle Benutzer deaktiviert.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Fehlerberichterstattung deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung steuert, ob Fehler an Microsoft gesendet werden oder nicht. Wenn Sie diese Richtlinieneinstellung deaktivieren, erhalten Benutzer nicht die Option, Fehler zu melden.)|
|Internetkommunikationsverwaltung/Internetkommunikationseinstellungen|Suche nach Gerätetreibern auf Windows Update deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung gibt an, ob Windows nach Windows-Updates für Gerätetreiber sucht, wenn keine lokalen Treiber für ein Gerät vorhanden sind. Wenn Sie diese Richtlinieneinstellung aktivieren, wird nicht nach Windows-Updates gesucht, wenn ein neues Gerät installiert wird.)|
|Anmelden|Willkommensseite für „Erste Schritte“ bei der Anmeldung nicht anzeigen| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Einstellung aktiviert ist, wird die Willkommensseite für den Benutzer ausgeblendet, der sich bei einem Windows-Gerät anmeldet.)|
|Anmelden|Verbundene Benutzer auf Computern, die der Domäne angehören, nicht auflisten| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Einstellung aktiviert ist, werden verbundene Benutzer nicht in der Anmeldebenutzeroberfläche auf mit der Domäne verknüpften Computern aufgeführt.)|
|Anmelden|Lokale Benutzer auf Computern, die der Domäne angehören, auflisten| NICHT ZUTREFFEND |**Deaktiviert** (Wenn diese Einstellung deaktiviert ist, werden lokale Benutzer nicht in der Anmeldebenutzeroberfläche auf mit der Domäne verknüpften Computern aufgeführt.)|
|Anmelden|Show clear logon background (Anmeldehintergrund klar anzeigen)| NICHT ZUTREFFEND |**Aktiviert** (Mit dieser Richtlinieneinstellung wird der Unschärfeeffekt des Anmeldehintergrundbilds deaktiviert. Wenn diese Einstellung aktiviert ist, wird das Hintergrundbild ohne Unschärfe angezeigt.)|
|Anmelden|Bei der ersten Anmeldung Animation abspielen| NICHT ZUTREFFEND |**Deaktiviert** (Mit dieser Richtlinieneinstellung können Sie steuern, ob Benutzern die Animation für die erste Anmeldung beim Computer angezeigt wird. Dies gilt sowohl für den ersten Benutzer des Computers, der die Ersteinrichtung durchführt, als auch für Benutzer, die später zum Computer hinzugefügt werden. Die Einstellung steuert auch, ob Benutzern von Microsoft-Konten bei der ersten Anmeldung die Auswahlaufforderung für Dienste angezeigt wird.<p>Wenn diese Einstellung deaktiviert ist, werden die Animation für die erste Anmeldung und die Auswahlaufforderung für Dienste nicht für Benutzer angezeigt.)|
|Anmelden|Anwendungsbenachrichtigungen auf gesperrtem Bildschirm deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Mit dieser Richtlinieneinstellung können Sie das Anzeigen von App-Benachrichtigungen auf dem Sperrbildschirm verhindern. Wenn diese Einstellung aktiviert ist, werden keine App-Benachrichtigungen auf dem Sperrbildschirm angezeigt.)|
|Energieverwaltung|Aktiven Energiesparplan auswählen|Aktiver Energiesparplan: Hohe Leistung|**Aktiviert** (Wenn Sie diese Richtlinieneinstellung aktivieren, legen Sie einen Energiesparplan über die Liste der Energiesparpläne fest.) <p>Wenn der Dienst „Power“ (Energie) deaktiviert ist, kann die Benutzeroberfläche „Powercfg.cpl“ diese Energieoptionen nicht anzeigen und gibt stattdessen einen RPC-Fehler zurück.|
|Energieverwaltung/Video- und Anzeigeeinstellungen|Diashow für Desktophintergrund aktivieren (Netzbetrieb)| NICHT ZUTREFFEND |**Deaktiviert** (Mit dieser Einstellung können Sie festlegen, ob Windows die Diashow für den Desktophintergrund aktivieren soll.) Wenn diese Einstellung deaktiviert ist, ist die Diashow für den Desktophintergrund deaktiviert. Diese Einstellung hat wahrscheinlich keine Auswirkungen auf VMs.|
|Wiederherstellung|Systemwiederherstellung in Standardzustand zulassen| NICHT ZUTREFFEND |**Deaktiviert** (Wenn diese Einstellung deaktiviert ist, sind die Elemente „Verwenden Sie ein zuvor erstelltes Systemabbild, um den Computer wiederherzustellen.“ und „Windows neu installieren“ (oder „Computer auf die Werkseinstellungen zurücksetzen“) nicht unter „Wiederherstellung“ (in der Systemsteuerung) verfügbar.)|
|*Speicherintegrität|Herunterladen von Updates auf das Datenträgerfehlermodell ermöglichen| NICHT ZUTREFFEND |**Deaktiviert** (Hiermit werden Updates für das Datenträgerfehlermodell nicht heruntergeladen)|
|Systemwiederherstellung|Systemwiederherstellung deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Einstellung aktiviert ist, ist die Systemwiederherstellung deaktiviert, und der Zugriff auf den Assistenten für die Systemwiederherstellung ist nicht verfügbar. Die Option zum Konfigurieren der Systemwiederherstellung oder zum Erstellen eines Wiederherstellungspunkts über den Systemschutz ist ebenfalls deaktiviert.)|
|Problembehandlung und Diagnose/Geplante Wartung|Verhalten für geplante Wartung konfigurieren| NICHT ZUTREFFEND |**Deaktiviert** (Hiermit wird festgelegt, ob die geplante Diagnose ausgeführt wird, um Systemproblem proaktiv zu ermitteln und zu lösen. Wenn diese Richtlinieneinstellung deaktiviert ist, kann Windows Probleme nicht mithilfe eines Zeitplans ermitteln, behandeln oder lösen.)|
|Problembehandlung und Diagnose/Skriptdiagnose|Problembehandlung: Zugriff und Ausführung von Problembehandlungs-Assistenten durch Benutzer zulassen| NICHT ZUTREFFEND |**Disabled** (Wenn diese Einstellung deaktiviert ist, können Benutzer nicht über die Systemsteuerung auf Problembehandlungstools zugreifen bzw. diese ausführen.)|
|Problembehandlung und Diagnose/Skriptdiagnose|Problembehandlung: Ermöglicht Benutzern, über die Systemsteuerung für Problembehandlung auf Onlineinhalte für die Problembehandlung auf Microsoft-Servern zuzugreifen (über den Windows-Problembehandlungs-Onlinedienst).| NICHT ZUTREFFEND |**Deaktiviert** (Wenn diese Einstellung deaktiviert ist, können Benutzer nur auf Problembehandlungsinhalte zugreifen und nach diesen suchen, die lokal auf ihren Computern vorhanden sind, selbst wenn sie mit dem Internet verbunden sind. Sie werden daran gehindert, eine Verbindung zu Microsoft-Servern herzustellen, die den Windows-Problembehandlungs-Onlinedienst hosten.|
|Problembehandlung und Diagnose \ Windows-Startleistungsdiagnose|Szenarioausführungsebene konfigurieren| NICHT ZUTREFFEND |**Deaktiviert** (Bestimmt die Ausführungsebene für die Windows-Startleistungsdiagnose. Wenn Sie diese Richtlinieneinstellung deaktivieren, ist Windows nicht in der Lage, Probleme im Zusammenhang mit der Windows-Startleistung zu erkennen, zu behandeln oder zu lösen, die von DPS verarbeitet werden.)<p>Diese Einstellung kann sehr hilfreich während Entwurfs-, Test-, Entwicklungs- oder Wartungsphasen sein. Diese Einstellung könnte auf einer isolierten VM oder einem isolierten Sitzungshost aktiviert werden. Messungen werden genommen und die Ergebnisse in den Ereignisprotokollen unter folgenden Pfad geschrieben: „Microsoft-Windows-Diagnostics-Performance/Operational“ Quelle: Diagnostics-Performance, Taskkategorie: „Startleistungsüberwachung“.<p>**ZUSÄTZLICH GILT:** Wenn der DPS-Dienst deaktiviert ist, hat diese Einstellung keinerlei Auswirkungen, da Windows keine Leistungsdaten protokolliert.|
|Problembehandlung und Diagnose \ Windows-Arbeitsspeicherverlust-Diagnose|Szenarioausführungsebene konfigurieren| NICHT ZUTREFFEND |**Deaktiviert** (Diese Richtlinieneinstellung bestimmt, ob der Diagnoserichtliniendienst (DPS) Arbeitsspeicherverlustprobleme diagnostiziert. Wenn diese Einstellung deaktiviert ist, kann der DPS keine Arbeitsspeicherverlustprobleme diagnostizieren.) <p>Viele Diagnosemodi können aktiviert und Tools wie WPT verwendet werden, obwohl dies in der Regel in Verwaltungs-, Test- oder Wartungsszenarios erfolgt. Auf Produktions-VMs oder in entsprechenden Sitzungen werden sie nicht aktiviert und verwendet.|
|Problembehandlung und Diagnose \ Windows-Leistungsnachverfolgungsmodul|PerfTrack aktivieren/deaktivieren| NICHT ZUTREFFEND |**Deaktiviert** (Diese Richtlinieneinstellung bestimmt, ob die Nachverfolgung von Ereignissen zur Reaktionszeit aktiviert oder deaktiviert wird. Wenn diese Einstellung deaktiviert wird, werden Ereignisse zur Reaktionszeit nicht verarbeitet.)|
|Problembehandlung und Diagnose \ Windows-Ressourcenauslastungserkennung und -Konfliktlösung|Szenarioausführungsebene konfigurieren| NICHT ZUTREFFEND |**Deaktiviert** (Bestimmt die Ausführungsebene für Windows-Ressourcenauslastungserkennung und -Konfliktlösung. Wenn Sie diese Einstellung deaktivieren, kann Windows Probleme der Windows-Ressourcenauslastung, die vom DPS verarbeitet werden, nicht erkennen, behandeln oder lösen.)|
|Problembehandlung und Diagnose \ Windows-Leistungsdiagnose beim Herunterfahren|Szenarioausführungsebene konfigurieren| NICHT ZUTREFFEND |**Deaktiviert** (Bestimmt die Ausführungsebene für die Windows-Herunterfahr-Leistungsdiagnose. Wenn Sie diese Einstellung deaktivieren, kann Windows Probleme der Windows-Herunterfahr-Leistung, die vom DPS verarbeitet werden, nicht erkennen, behandeln oder lösen.)|
|Problembehandlung und Diagnose \ Diagnose für Windows-Standby-/Wiederaufnahmeleistung|Szenarioausführungsebene konfigurieren| NICHT ZUTREFFEND |**Deaktiviert** (Bestimmt die Ausführungsebene für die Diagnose für Windows-Standby-/Wiederaufnahmeleistung. Wenn Sie diese Einstellung deaktivieren, kann Windows Probleme der Windows-Standby-/Wiederaufnahmeleistung, die vom DPS verarbeitet werden, nicht erkennen, behandeln oder lösen.)|
|Problembehandlung und Diagnose \ Diagnose der Leistung für Windows-Systemreaktionszeit|Szenarioausführungsebene konfigurieren| NICHT ZUTREFFEND |**Deaktiviert** (Bestimmt die Ausführungsebene für die Diagnose der Leistung für Windows-Systemreaktionszeit. Wenn Sie diese Einstellung deaktivieren, kann Windows Leistungsprobleme für Windows-Systemreaktionszeiten, die vom DPS verarbeitet werden, nicht erkennen, behandeln oder lösen.)|
*Benutzerprofile|Werbe-ID deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Einstellung aktiviert ist, ist die Werbe-ID deaktiviert. Apps können die ID nicht für Benutzeroberflächen in verschiedenen Apps verwenden.)|
|Richtlinie für „Lokaler Computer“ \ Computerkonfiguration \ Administrative Vorlagen \ Windows-Komponenten| NICHT ZUTREFFEND | NICHT ZUTREFFEND | NICHT ZUTREFFEND |
|*App-Datenschutz|Windows-App-Zugriff auf Diagnoseinformationen anderer Apps zulassen|Standard für alle Apps: Verweigern erzwingen|**Aktiviert** (Wenn diese Einstellung aktiviert ist und die Option „Verweigern erzwingen“ verwendet wird, können Windows-Apps keine Diagnoseinformationen zu anderen Apps abrufen, und Angestellte in Ihrer Organisation können dies nicht ändern.)|
|*App-Datenschutz|Windows-App-Zugriff auf Standort zulassen|Standard für alle Apps: Verweigern erzwingen|**Aktiviert** (Wenn Sie diese Einstellung aktivieren und die Option „Verweigern erzwingen“ verwendet wird, können Windows-Apps nicht auf den Standort zugreifen, und Benutzer können diese Einstellung nicht ändern.)|
|*App-Datenschutz|Windows-App-Zugriff auf Bewegungsdaten zulassen|Standard für alle Apps: Verweigern erzwingen|**Aktiviert** (Wenn Sie diese Einstellung aktivieren und die Option „Verweigern erzwingen“ verwendet wird, können Windows-Apps nicht auf Bewegungsdaten zugreifen, und Benutzer können diese Einstellung nicht ändern.)|
|*App-Datenschutz|Windows-App-Zugriff auf Benachrichtigungen zulassen|Standard für alle Apps: Verweigern erzwingen|**Aktiviert** (Wenn Sie diese Einstellung aktivieren und die Option „Verweigern erzwingen“ verwendet wird, können Windows-Apps nicht auf Benachrichtigungen zugreifen, und Benutzer können diese Einstellung nicht ändern.)|
|*App-Datenschutz|Sprachaktivierung für Apps aktivieren|Standard für alle Apps: Verweigern erzwingen|**Aktiviert** (Mit dieser Richtlinieneinstellung wird angegeben, ob Windows-Apps per Sprache aktiviert werden können.)|
|*App-Datenschutz|Sprachaktivierung für Apps auf Sperrbildschirm aktivieren|Standard für alle Apps: Verweigern erzwingen|**Aktiviert** (Mit dieser Richtlinieneinstellung wird angegeben, ob Windows-Apps per Sprache aktiviert werden können, während das System gesperrt ist.)|
|*App-Datenschutz|Let Windows apps control radios|Standard für alle Apps: Verweigern erzwingen|**Aktiviert** (Wenn Sie die Option „Verweigern erzwingen“ gewählt haben, dürfen Windows-Apps nicht auf die Steuerung von Radios zugreifen, und Mitarbeiter in Ihrer Organisation können dies nicht ändern.)|
|Anwendungskompatibilität|Inventory Collector deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung steuert den Status des Inventory Collectors. Der Inventory Collector inventarisiert Anwendungen, Dateien, Geräte und Treiber auf dem System und sendet die Informationen an Microsoft. Wenn Sie diese Richtlinieneinstellung aktivieren, wird der Inventory Collector deaktiviert, und es werden keine Daten an Microsoft gesendet. Die Erfassung von Installationsdaten über den Programmkompatibilitäts-Assistenten ist ebenfalls deaktiviert.)|
|Richtlinien für die automatische Wiedergabe|Standardverhalten von AutoAusführen festlegen|Keine AutoAusführen-Befehle ausführen|**Aktiviert** (Diese Richtlinieneinstellung legt das Standardverhalten für AutoAusführen-Befehle fest.)|
|*Richtlinien für die automatische Wiedergabe|Automatische Wiedergabe deaktivieren|Alle Laufwerke|**Aktiviert** (Wenn Sie diese Richtlinieneinstellung aktivieren, wird die automatische Wiedergabe auf allen Laufwerken deaktiviert.)|
|*Cloudinhalt|Windows-Tipps nicht anzeigen| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung verhindert, dass Windows-Tipps für Benutzer angezeigt werden.)|
|*Cloudinhalt|Microsoft-Anwenderfeatures deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Ist diese Richtlinieneinstellung aktiviert, werden Benutzern keine personalisierten Empfehlungen von Microsoft und keine Benachrichtigungen über ihr Microsoft-Konto mehr angezeigt.)|
|*Datenerfassung und Vorabversionen|Telemetrie zulassen|0 – Sicherheit [nur Enterprise]|**Aktiviert** (Wird der Wert 0 (Null) festgelegt, gilt dies für Geräte, auf denen ausschließlich Enterprise-, Education-, IoT- oder Windows Server-Editionen ausgeführt werden. Zudem wird die gesendete Telemetrie hierdurch auf die niedrigste unterstützte Ebene reduziert.)|
|Datensammlung und Vorabversionen|Configure collection of browsing data for Desktop Analytics (Sammlung von Browserdaten für Desktop Analytics konfigurieren)|Configure telemetry collection: (Telemetriesammlung konfigurieren:) Do not allow sending intranet or internet history (Senden des Intra- oder Internetverlaufs nicht zulassen)|**Aktiviert** (Sie können Microsoft Edge so konfigurieren, dass nur der Intranetverlauf, nur der Internetverlauf oder beides von Unternehmensgeräten mit einer konfigurierten kommerziellen ID an Desktop Analytics gesendet wird. Ist diese Option deaktiviert oder nicht konfiguriert, sendet Microsoft Edge keine Browserverlaufsdaten an Desktop Analytics.)|
|*Datenerfassung und Vorabversionen|Feedbackbenachrichtigungen nicht mehr anzeigen| NICHT ZUTREFFEND |**Aktiviert** (Mit dieser Richtlinieneinstellung können Organisationen verhindern, dass die Geräte der Organisation Feedbackfragen von Microsoft anzeigen.)|
|Übermittlungsoptimierung|Downloadmodus|Downloadmodus: Einfach (99)|**Aktiviert** (99 = Einfacher Downloadmodus ohne Peering. Die Übermittlungsoptimierung lädt ausschließlich über HTTP herunter und versucht nicht, die Clouddienste der Übermittlungsoptimierung zu kontaktieren)|
|Desktopfenster-Manager|Fensteranimationen nicht zulassen| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung steuert die Darstellung von Fensteranimationen wie diejenigen Animationen, die beim Wiederherstellen, Minimieren und Maximieren von Fenstern angezeigt werden. Ist diese Richtlinieneinstellung aktiviert, werden Fensteranimationen deaktiviert.)|
|Desktopfenster-Manager|Volltonfarbe für Starthintergrund verwenden| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung steuert die Darstellung des Starthintergrunds. Ist diese Richtlinieneinstellung aktiviert, wird für den Starthintergrund eine Volltonfarbe verwendet.)|
|Rand-UI|Wischen vom Bildschirmrand zulassen| NICHT ZUTREFFEND |**Deaktiviert** (Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer keine Systembenutzeroberfläche durch Wischen vom Bildschirmrand weg aufrufen.)|
|Rand-UI|Hilfetipps deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Ist diese Einstellung aktiviert, zeigt Windows dem Benutzer keine Hilfetipps an.)|
|Datei-Explorer|Benachrichtigung „Neue Anwendung installiert“ nicht anzeigen| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinie entfernt die Benachrichtigung für Endbenutzer zu neuen Anwendungszuweisungen. Diese Zuweisungen basieren auf Dateitypen (z. B. TXT-Dateien) oder Protokollen (z. B. HTTP). Ist diese Richtlinie aktiviert, werden dem Endbenutzer keine Benachrichtigungen angezeigt.)|
|Dateiversionsverlauf|Dateiversionsverlauf deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Ist diese Richtlinieneinstellung aktiviert, kann der Dateiverlauf nicht aktiviert werden, um reguläre, automatische Sicherungen zu erstellen.)|
|*Mein Gerät suchen|„Mein Gerät suchen“ aktivieren/deaktivieren| NICHT ZUTREFFEND |**Deaktiviert** (Ist „Mein Gerät suchen“ ausgeschaltet, werden das Gerät und sein Standort nicht registriert und das Feature „Mein Gerät suchen“ funktioniert nicht. Der Benutzer kann auf seinem Gerät auch nicht den Ort sehen, an dem sein aktives Digitalisierungsgerät zuletzt genutzt wurde.)|
|Heimnetzgruppe|Beitritt des Computers zu einer Heimnetzgruppe verhindern| NICHT ZUTREFFEND |**Aktiviert** (Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer keine Computer zu Heimnetzgruppen hinzufügen. Diese Richtlinieneinstellung wirkt sich nicht auf andere Netzwerkfreigabefeatures aus.)|
|*Internet Explorer|Für Microsoft-Dienste das Bereitstellen von erweiterten Vorschlägen zulassen, wenn Benutzer Text in die Adressleiste eingeben| NICHT ZUTREFFEND |**Deaktiviert** (Benutzern werden keine erweiterten Vorschläge angezeigt, sobald sie Text in die Adressleiste eingeben. Außerdem können Benutzer die Einstellung „Vorschläge“ nicht ändern.)|
|Internet Explorer|Periodische Überprüfungen auf Internet Explorer-Softwareupdates deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Verhindert, dass Internet Explorer überprüft, ob eine neue Browserversion verfügbar ist.)|
|Internet Explorer|Anzeigen des Begrüßungsbildschirms deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Verhindert, dass der Begrüßungsbildschirm von Internet Explorers angezeigt wird, wenn Benutzer den Browser starten.)|
|Internet Explorer|Automatisch neue Versionen von Internet Explorer installieren| NICHT ZUTREFFEND |**Deaktiviert** (Diese Richtlinieneinstellung konfiguriert Internet Explorer so, dass automatisch neuere Versionen von Internet Explorer installiert werden, wenn diese verfügbar sind.)|
|Internet Explorer|Teilnahme am Programm zur Verbesserung der Benutzerfreundlichkeit verhindern| NICHT ZUTREFFEND |**Aktiviert** (Diese Einstellung verhindert, dass Benutzer am Programm zur Verbesserung der Benutzerfreundlichkeit teilnehmen.)|
|Internet Explorer|Ausführen des Anpassungs-Assistenten verhindern|Direkt zur Startseite wechseln|**Aktiviert** (Diese Richtlinieneinstellung verhindert, dass Internet Explorer den Anpassungs-Assistenten ausführt, wenn ein Benutzer den Browser nach der Installation von Internet Explorer oder Windows zum ersten Mal startet.)|
|Internet Explorer|Zunahme von Registerkartenprozess festlegen|Low (Niedrig)|**Aktiviert** (Mit dieser Richtlinieneinstellung können Sie die Häufigkeit festlegen, mit der Internet Explorer neue Registerkartenprozesse erstellt.)|
|Internet Explorer|Benachrichtigungen zur Add-On-Leistung deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung verhindert, dass Internet Explorer eine Benachrichtigung anzeigt, wenn die durchschnittliche Ladezeit für alle aktivierten Add-Ons eines Benutzers den Schwellenwert überschreitet.)|
|Internet Explorer|Automatische Wiederherstellung nach Systemabsturz deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Mit dieser Richtlinieneinstellung wird die automatische Wiederherstellung nach Systemabstürzen deaktiviert. Ist diese Richtlinieneinstellung aktiviert, wird der Benutzer von der automatischen Wiederherstellung nach Systemabstürzen nicht aufgefordert, seine Daten wiederherzustellen, nachdem ein Programm nicht mehr reagiert.)|
|*Internet Explorer|Browser-Geolocation deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, wird die Geolocationunterstützung im Browser deaktiviert.)|
|*Internet Explorer|„Vorgeschlagene Sites“ aktivieren| NICHT ZUTREFFEND |**Deaktiviert** (Wenn diese Richtlinieneinstellung deaktiviert ist, werden die mit diesem Feature verbundenen Einstiegspunkte und Funktionen deaktiviert.)|
|Internet Explorer\Internetsystemsteuerung\Seite „Erweitert“|Animationen in Webseiten wiedergeben| NICHT ZUTREFFEND |**Deaktiviert** (Mithilfe dieser Richtlinieneinstellung können Sie verwalten, ob im Internet Explorer animierte Bilder aus Webinhalten angezeigt werden. Diese Einstellung wirkt sich in der Regel nur auf animierte GIF-Dateien aus. Aktive Webinhalte wie Java-Applets werden nicht beeinträchtigt.)|
|Internet Explorer\Internetsystemsteuerung\Seite „Erweitert“|Abspielen von Sounds auf Webseiten| NICHT ZUTREFFEND |**Deaktiviert** (Wenn diese Richtlinieneinstellung deaktiviert ist, spielt der Internet Explorer Sounds in Webinhalten weder ab noch lädt er sie herunter, und Hilfeseiten werden schneller angezeigt.)|
|Internet Explorer\Internetsystemsteuerung\Seite „Erweitert“|Videos in Webseiten wiedergeben| NICHT ZUTREFFEND |**Deaktiviert** (Wenn Sie diese Richtlinieneinstellung deaktivieren, spielt der Internet Explorer Videos weder ab noch lädt er sie herunter, und Hilfeseiten werden schneller angezeigt.)|
|Internet Explorer\Internetsystemsteuerung\Seite „Erweitert“|Laden von Websites und Inhalten im Hintergrund zur Optimierung der Leistung deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, lädt der Internet Explorer keine Websites oder Inhalte im Hintergrund.)|
|*Internet Explorer\Internetsystemsteuerung\Seite „Erweitert“|Vorblättern mit Seitenvorhersage deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Microsoft zeichnet Ihren Browserverlauf auf, um die Funktionsweise des Vorblätterns mit Seitenvorhersage zu verbessern. Wenn du diese Richtlinieneinstellung aktivierst, ist das Vorblättern mit Seitenvorhersage deaktiviert, und die nächste Webseite wird nicht im Hintergrund geladen.)|
|Internet Explorer\Interneteinstellungen\Erweiterte Einstellungen\Browsen|Finden von Telefonnummern deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung bestimmt, ob Telefonnummern erkannt und in Hyperlinks umgewandelt werden, mit denen die Standardtelefonanwendung des Systems aufgerufen werden kann. Wenn Sie diese Richtlinieneinstellung deaktivieren, ist das Finden von Telefonnummern aktiviert. Diese Einstellung kann von Benutzern nicht geändert werden.)|
|Internetinformationsdienste|IIS-Installation verhindern| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, können keine IIS installiert werden, und Sie können keine Windows-Komponenten oder Anwendungen installieren, für die IIS erforderlich sind.)|
|*Speicherort und Sensoren|Speicherort deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, wird das Speicherortfeature deaktiviert, und alle Programme auf diesem Gerät werden daran gehindert, Speicherortinformationen aus dem Speicherortfeature zu verwenden.)|
|Speicherort und Sensoren|Sensoren deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung deaktiviert das Sensorfeature für dieses Gerät. Wenn diese Richtlinieneinstellung aktiviert ist, ist das Sensorfeature deaktiviert, und keins der Programme auf diesem Computer kann das Sensorfeature verwenden.)|
|Speicherorte und Sensoren / Windows-Positionssuche|Windows-Positionssuche deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung deaktiviert die Windows-Positionssuche für dieses Gerät.)|
|*Karten|Automatische Downloads und Updates von Kartendaten deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Einstellung aktiviert ist, wird das automatische Herunterladen und Aktualisieren von Kartendaten deaktiviert.)|
|*Karten|Nicht angeforderten Netzwerk-Datenverkehr auf der Einstellungsseite „Offlinekarten“ deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, werden Features deaktiviert, die Netzwerkdatenverkehr auf der Einstellungsseite „Offlinekarten“ erzeugen. Hinweis: Dies könnte die gesamte Einstellungsseite deaktivieren.)|
|*Messaging|Synchronisierung des Nachrichtendiensts mit der Cloud zulassen| NICHT ZUTREFFEND |**Deaktiviert** (Diese Richtlinieneinstellung ermöglicht die Sicherung und Wiederherstellung von SMS in den Cloud-Diensten von Microsoft.)|
|*Microsoft Edge|Konfigurationsupdates für die Bibliothek zulassen| NICHT ZUTREFFEND |**Deaktiviert** (Wenn diese Einstellung deaktiviert ist, werden die aktualisierten Konfigurationsdaten für die Bibliothek von Microsoft Edge nicht automatisch heruntergeladen.)|
|*Microsoft Edge|Erweiterte Telemetrie für die Registerkarte „Bücher“ zulassen| NICHT ZUTREFFEND |**Deaktiviert** (Wenn diese Einstellung deaktiviert ist, sendet Microsoft Edge je nach Gerätekonfiguration nur grundlegende Telemetriedaten.)|
|Microsoft Edge|Microsoft Edge einen Vorabstart beim Windows-Start ermöglichen, wenn sich das System im Leerlauf befindet und wenn Microsoft Edge geschlossen wird|Vorabstart konfigurieren: Vorabstart verhindern|**Aktiviert** (Wenn diese Einstellung aktiviert und konfiguriert wurde, um einen Vorabstart zu verhindern, wird Microsoft Edge bei der Windows-Anmeldung nicht vorab gestartet, wenn sich das System im Leerlauf befindet oder wenn Microsoft Edge geschlossen wird.)|
|Microsoft Edge|Zulassen, dass Microsoft Edge beim Starten von Windows und bei jedem Schließen von Microsoft Edge die Seiten „Start“ und „Neue Registerkarte“ startet und lädt|Vorabladen von Registerkarten konfigurieren: Vorabladen von Registerkarten verhindern|**Aktiviert** (Mithilfe dieser Richtlinieneinstellung können Sie entscheiden, ob Microsoft Edge während der Windows-Anmeldung – und wenn Microsoft Edge geschlossen wird – die Seiten „Start“ und „Neue Registerkarte“ laden kann. Standardmäßig lässt diese Einstellung das Vorabladen zu. Wenn das Vorabladen deaktiviert ist, lädt Microsoft Edge die Seiten „Start“ oder „Neue Registerkarte“ nicht während der Windows-Anmeldung und wenn Microsoft Edge geschlossen wird.)|
|Microsoft Edge|Webinhalte auf der Seite „Neuer Tab“ zulassen| NICHT ZUTREFFEND |**Deaktiviert** (Wenn diese Einstellung deaktiviert ist, öffnet Microsoft Edge eine neue Registerkarte mit einer leeren Seite. Wenn diese Einstellung konfiguriert ist, können Benutzer die Einstellung nicht ändern.)|
|*Microsoft Edge|Verhindern, dass die Einrichtungs-Webseite in Microsoft Edge geöffnet wird| NICHT ZUTREFFEND |**Aktiviert** (Bei aktivierter Einstellung wird den Benutzern die Seite „First Run“ (Erste Ausführung) nicht angezeigt, wenn sie Microsoft Edge zum ersten Mal öffnen.)|
|OneDrive|OneDrive davon abhalten, Netzwerkdatenverkehr zu generieren, bis der Benutzer sich auf OneDrive anmeldet| NICHT ZUTREFFEND |**Aktiviert** (Aktivieren Sie diese Einstellung, um zu verhindern, dass der OneDrive-Synchronisierungsclient (OneDrive.exe) Netzwerkdatenverkehr erzeugt (Suche nach Updates usw.), bis sich der Benutzer bei OneDrive anmeldet oder mit der Synchronisierung von Dateien auf dem lokalen Computer beginnt.)|
|Onlineunterstützung|Aktive Hilfe deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, werden aktive Links zu Inhalten nicht gerendert. Der Text wird zwar angezeigt, aber es gibt keine Links für diese Elemente, auf die geklickt werden kann.)|
|OOBE|Oberfläche für Datenschutzeinstellung bei Benutzeranmeldung nicht starten| NICHT ZUTREFFEND |**Aktiviert** (Wenn ein Benutzer sich zum ersten Mal oder nach einem Upgrade in bestimmten Szenarien bei einem neuen Benutzerkonto anmeldet, werden dem Benutzer ein Bildschirm oder eine Reihe von Bildschirmen angezeigt, die ihn dazu auffordern, die Datenschutzeinstellungen für sein Konto zu wählen. Aktiviere diese Richtlinie, um zu verhindern, dass diese Oberfläche gestartet wird.)|
|RSS-Feeds|Automatische Ermittlung von Feeds und Web Slices verhindern| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung verhindert, dass Benutzer Internet Explorer verwenden, um automatisch zu ermitteln, ob ein Feed oder Web Slice für eine zugeordnete Webseite verfügbar ist.)|
|*RSS-Feeds|Hintergrundsynchronisierung für Feeds und Web Slices deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, können Feeds und Web Slices nicht im Hintergrund synchronisiert werden.)|
|*Suche|Cortana zulassen| NICHT ZUTREFFEND |**Deaktiviert** (Diese Richtlinieneinstellung gibt an, ob Cortana auf dem Gerät zugelassen ist. Wenn Cortana ausgeschaltet ist, können Benutzer mithilfe der Suchfunktion trotzdem Informationen auf dem Gerät suchen.)|
|Suchen|Cortana auf Sperrbildschirm zulassen| NICHT ZUTREFFEND |**Deaktiviert** (Diese Richtlinieneinstellung bestimmt, ob der Benutzer mittels Sprache mit Cortana interagieren kann, während das System gesperrt ist.)|
|*Suche|Der Suche und Cortana die Nutzung von Positionsdaten erlauben| NICHT ZUTREFFEND |**Deaktiviert** (Diese Richtlinieneinstellung gibt an, ob von der Suche und Cortana standortabhängige Such- und Cortana-Ergebnisse bereitgestellt werden können.)|
|Suchen|Umfassende Vorschau für Anlagen steuern|Umfassende Vorschau für Anlagen steuern: **.docx;.xlsx;.txt;.xls**|**Aktiviert** (Das Aktivieren dieser Richtlinie definiert eine durch Semikolons getrennte Liste der Dateierweiterungen, für die eine umfassende Vorschau zugelassen wird.)<p>**HINWEIS**: Mit dieser Einstellung können die Anhangstypen eingeschränkt werden, für die eine Vorschau angezeigt werden kann. Hiermit lässt sich auch die automatische Anzeige einer Vorschau potenziell gefährlicher Inhaltstypen verhindern.|
|Suchen|Websuche nicht zulassen| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinie aktiviert ist, wird die Option zum Durchsuchen des Webs aus der Windows-Desktopsuche entfernt.)|
|*Suche|Nicht im Web suchen und keine Webergebnisse in der Suche anzeigen| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, werden keine Abfragen im Web durchgeführt, und es werden keine Webergebnisse angezeigt, wenn ein Benutzer in der Suche eine Abfrage durchführt.)|
|Suchen|Indizierung von nicht zwischengespeicherten Exchange-Ordnern aktivieren| NICHT ZUTREFFEND |**Deaktiviert** (Das Aktivieren dieser Richtlinie ermöglicht die Indizierung von E-Mail-Elementen auf einem Microsoft Exchange-Server, wenn Microsoft Outlook nicht im Cachemodus ausgeführt wird. Beim Standardsuchverhalten werden nicht zwischengespeicherte Exchange-Ordner nicht indiziert. Durch Deaktivieren dieser Richtlinie wird die gesamte Indizierung nicht zwischengespeicherter Exchange-Ordner blockiert.)|
|Suchen|Indizierung von Dateien im Offlinedateicache verhindern| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinie aktiviert ist, werden Dateien auf Netzwerkfreigaben, die offline zur Verfügung stehen, nicht indiziert. Andernfalls werden diese Dateien indiziert. Standardmäßig deaktiviert.)|
|*Suche|Festlegen der in der Suche freizugebenden Informationen|Anonyme Informationen|**Aktiviert** (Anonyme Informationen: Freigabe von Nutzungsinformationen, aber keine Freigabe des Suchverlaufs, der Microsoft-Kontoinformationen oder des genauen Standorts.)|
|Suchen|Indizierung bei eingeschränktem Festplatten-Speicherplatz beenden|Limit (MB): **5000**|**Aktiviert** (Bei aktivierter Richtlinie wird die Fortsetzung der Indizierung verhindert, wenn weniger als die angegebene Menge Speicherplatz auf dem Laufwerk verfügbar ist, auf dem der Index gespeichert ist. Leg einen Wert zwischen 0 und 2147483647 MB fest.)|
|Softwareschutz-Plattform|AVS-Onlineüberprüfung für KMS-Client ausschalten| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Einstellung aktiviert ist, sendet das Gerät keine Daten zum Aktivierungszustand an Microsoft.)|
|*Spracherkennung|Automatische Aktualisierung von Sprachdaten zulassen| NICHT ZUTREFFEND |**Deaktiviert** (Gibt an, ob das Gerät Updates für die Spracherkennungs- und Sprachsynthesemodelle erhält.)|
|Speicher|Deaktivieren des Angebots zum Update auf die aktuelle Version von Windows| NICHT ZUTREFFEND |**Aktiviert** (Aktiviert bzw. deaktiviert das Store-Angebot zum Update auf die aktuelle Version von Windows. Wenn du diese Einstellung aktivierst, bietet die Store-Anwendung kein Update auf die jeweils aktuelle Windows-Version an.)|
|Texteingabe|Freihand- und Eingabeerkennung verbessern| NICHT ZUTREFFEND |**Deaktiviert** (Diese Richtlinieneinstellung bestimmt, ob Freihand- und Eingabedaten an Microsoft gesendet werden können, um die Funktionen für Spracherkennung und Vorschläge zu verbessern, die Apps und Dienste unter Windows nutzen.)|
|Windows-Fehlerberichterstattung|Deaktivieren der Windows-Fehlerberichterstattung| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, sendet die Windows-Fehlerberichterstattung keine Probleminformationen an Microsoft. Darüber hinaus sind in der Systemsteuerung unter „Sicherheit und Wartung“ auch keine Informationen zur Problemlösung verfügbar.)|
|Windows-Spielaufzeichnung und -übertragung|Aktiviert oder deaktiviert die Windows-Spielaufzeichnung und -übertragung| NICHT ZUTREFFEND |**Deaktiviert** (Wenn diese Einstellung deaktiviert ist, ist die Windows-Spielaufzeichnung nicht zulässig.)|
|Windows Ink-Arbeitsbereich|Windows Ink-Arbeitsbereich zulassen|Wähle eine der folgenden Aktionen aus: Deaktiviert|**Aktiviert** (Wenn diese Einstellung aktiviert und die untergeordnete Einstellung deaktiviert ist, sind die Funktionen des Windows Ink-Arbeitsbereichs nicht verfügbar.)|
|Windows Installer|Maximalgröße für den Basisdateicache steuern|5|**Aktiviert** (Diese Richtlinie steuert den Prozentsatz des Speicherplatzes, der dem Basisdateicache von Windows Installer zur Verfügung steht. Wenn diese Richtlinie aktiviert ist, kannst du die maximale Größe des Basisdateicache für Windows Installer ändern.)|
|Windows Installer|Erstellung von Systemwiederherstellungsprüfpunkten deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinie aktiviert ist, generiert Windows Installer bei der Installation von Anwendungen keine Prüfpunkte für die Systemwiederherstellung.)|
|Windows-Mobilitätscenter|Windows-Mobilitätscenter deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert wird, kann der Benutzer das Windows-Mobilitätscenter nicht aufrufen. Die Benutzeroberfläche des Windows-Mobilitätscenters wird von allen Shelleinsprungpunkten entfernt und kann mithilfe der EXE-Datei nicht mehr gestartet werden.)|
|Windows-Zuverlässigkeitsanalyse|WMI-Anbieter für Zuverlässigkeit konfigurieren| NICHT ZUTREFFEND |**Deaktiviert** (Wenn diese Richtlinieneinstellung deaktiviert ist, werden keine Informationen zur Systemzuverlässigkeit von der Zuverlässigkeitsüberwachung angezeigt, und WMI-fähige Anwendungen sind nicht in der Lage, auf Zuverlässigkeitsinformationen der aufgelisteten Anbieter zuzugreifen.)|
|Windows-Sicherheit \ Benachrichtigungen|Nicht kritische Benachrichtigungen ausblenden| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Einstellung aktiviert ist, werden lokalen Benutzern nur kritische Benachrichtigung aus Windows-Sicherheit angezeigt. Andere Benachrichtigungstypen wie reguläre Informationen zur Integrität von PCs oder Geräten werden nicht angezeigt.)|
|Windows Update|Softwarebenachrichtigungen aktivieren| NICHT ZUTREFFEND |**Deaktiviert** (Mit dieser Richtlinieneinstellung kannst du steuern, ob Benutzer ausführliche erweiterte Benachrichtigungen über vom Microsoft Update-Dienst vorgestellte Software erhalten. Optimierte Benachrichtigungen vermitteln den Nutzen und fördern die Installation und Verwendung von optionaler Software. Diese Richtlinieneinstellung eignet sich für locker verwaltete Umgebungen, in denen Endbenutzern Zugriff auf den Microsoft Update-Dienst gewährt wird.)|
|*Windows Update \ Windows Update für Unternehmen|Vorabversionen verwalten|Lege das Verhalten für den Empfang von Vorabversionen fest: **Vorabversionen deaktivieren**|**Aktiviert** (Bei Auswahl von „Vorabversionen deaktivieren“ werden keine Vorabversionen auf dem Gerät installiert. Dadurch wird verhindert, dass Benutzer über „Einstellungen“ > „Update und Sicherheit“ am Windows-Insider-Programm teilnehmen.)|
|*Windows Update \ Windows Update für Unternehmen|Auswählen, wann Vorabversionen und Featureupdates empfangen werden|Wähle die Windows-Bereitschaftsstufe für die Updates aus, die empfangen werden sollen:<p>Halbjährlicher Kanal:<p>Nach Veröffentlichung eines Vorschaubuilds oder eines Featureupdates kann der Empfang für die folgende Anzahl von Tagen zurückgestellt werden: **365**<p>Vorschaubuilds oder Featureupdates ab diesem Datum pausieren: **jjjj-mm-tt**|**Aktiviert** (Aktiviere diese Richtlinie, um die Stufe der zu empfangenden Vorschaubuilds oder Featureupdates und den Zeitpunkt anzugeben. Halbjährlicher Kanal: Hiermit werden Featureupdates sofort empfangen, wenn sie für die allgemeine Öffentlichkeit freigegeben werden.<p> Bei Auswahl des halbjährlichen Kanals gilt Folgendes:<p>– Du kannst den Empfang von Featureupdates bis zu 365 Tage zurückstellen.<p>– Um zu verhindern, dass Featureupdates zum geplanten Zeitpunkt empfangen werden, kannst du sie vorübergehend pausieren. Die Pause ist ab der angegebenen Startzeit 35 Tage gültig.<p> – Um den Empfang pausierter Featureupdates wieder aufzunehmen, lösche den Eintrag im Startdatumsfeld.)|
|*Windows Update \ Windows Update für Unternehmen|Beim Empfang von Qualitätsupdates auswählen|Nach Veröffentlichung eines Qualitätsupdates kann der Empfang für die folgende Anzahl von Tagen zurückgestellt werden: **30**<p>Qualitätsupdates ab diesem Datum pausieren: jjjj-mm-tt|**Aktiviert** (Aktiviere diese Richtlinie, um anzugeben, wann du Qualitätsupdates empfangen möchtest.<p>Du kannst den Empfang von Qualitätsupdates maximal 30 Tage zurückstellen.<p>Um den Empfang von Qualitätsupdates zum geplanten Zeitpunkt zu verhindern, kannst du sie vorübergehend pausieren. Die Pause gilt für 35 Tage oder bis du das Datum aus dem Feld „Startdatum“ löschst.<p>Um pausierte Qualitätsupdates wieder zu empfangen, lösche das Datum aus dem Startdatumsfeld.)<p>Mit dieser Empfehlung kannst du steuern, wann Updates angewendet werden, und sicherstellen, dass Updates nicht unerwartet angeboten und installiert werden.|
|Richtlinie für Lokaler Computer \ Benutzerkonfiguration \ Administrative Vorlagen| NICHT ZUTREFFEND | NICHT ZUTREFFEND | NICHT ZUTREFFEND |
|Systemsteuerung \ Regions- und Sprachoptionen|Textvorhersagen bei der Eingabe deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinie deaktiviert die Option für Textvorhersagen bei der Eingabe. Dadurch wird allerdings nicht verhindert, dass der Benutzer oder eine Anwendung die Einstellung programmgesteuert ändert. Wenn diese Richtlinieneinstellung aktiviert ist, wird die Option so festgelegt, dass keine Textvorhersagen angezeigt werden.)|
|Desktop|Freigaben von zuletzt geöffneten Dateien nicht in „Netzwerkumgebung“ hinzufügen| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Einstellung aktiviert ist, werden freigegebene Ordner nicht automatisch zu Netzwerkspeicherorten hinzugefügt, wenn ein Dokument im freigegebenen Ordner geöffnet wird.)|
|Desktop|Aero Shake-Mausbewegung zum Minimieren von Fenstern deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Verhindert, dass Fenster minimiert oder wiederhergestellt werden, wenn im aktiven Fenster eine Schüttelbewegung mit der Maus ausgeführt wird. Wenn diese Richtlinie aktiviert ist, werden Anwendungsfenster nicht Fenster minimiert oder wiederhergestellt, wenn im aktiven Fenster eine Schüttelbewegung mit der Maus ausgeführt wird.)|
|Desktop  Active Directory|Maximale Suchgröße von Active Directory|Anzahl der zurückgegebenen Objekte: **1500**|**Aktiviert** (Gibt die maximale Anzahl von Objekten an, die das System als Antwort auf einen Befehl anzeigt, in Active Directory zu suchen. Diese Einstellung wirkt sich auf alle Suchanzeigen für Active Directory aus, z. B. auf die in „Lokale Benutzer und Gruppen“, „Active Directory-Benutzer und -Computer“ und in Dialogfeldern, in denen die Berechtigungen für Benutzer- und Gruppenobjekte von Active Directory festgelegt werden.)|
|Startmenü und Taskleiste|Keine Elemente in Sprunglisten von Remotestandorten anzeigen oder nachverfolgen| NICHT ZUTREFFEND |**Aktiviert** (Mit dieser Richtlinieneinstellung kannst du die Anzeige oder Nachverfolgung von Elementen in Sprunglisten von Remotestandorten steuern.)|
|Startmenü und Taskleiste|Nicht im Internet suchen| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, wird im Feld „Suchen“ des Startmenüs nicht im Internetverlauf oder in den Favoriten gesucht.)|
|Startmenü und Taskleiste|Beim Zuordnen von Shellshortcuts nicht die suchbasierte Methode verwenden| NICHT ZUTREFFEND |**Aktiviert** (Mit dieser Richtlinieneinstellung wird verhindert, dass das System zum Auflösen einer Verknüpfung eine umfassende Suche auf dem Ziellaufwerk ausführt.)|
|Startmenü und Taskleiste|Alle Sprechblasenbenachrichtigungen deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, werden keine Sprechblasenbenachrichtigungen für Benutzer angezeigt.)
|Startmenü und Taskleiste|Sprechblasenbenachrichtigungen für Featureankündigungen deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, werden bestimmte, als Featureankündigungen markierte Sprechblasenbenachrichtigungen nicht angezeigt.)|
|Startmenü und Taskleiste|Benutzerüberwachung deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, werden die vom Benutzer ausgeführten Programme nicht vom System nachverfolgt und häufig verwendete Programme nicht im Startmenü angezeigt.)|
|*Startmenü und Taskleiste \ Benachrichtigungen|Popupbenachrichtigungen deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, können Anwendungen keine Popupbenachrichtigungen auslösen.)|
|*Startmenü und Taskleiste \ Benachrichtigungen|Popupbenachrichtigungen auf Sperrbildschirm deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, können Anwendungen keine Popupbenachrichtigungen auf dem Sperrbildschirm auslösen.)|
|Lokale Computerrichtlinie / Benutzerkonfiguration| NICHT ZUTREFFEND | NICHT ZUTREFFEND | NICHT ZUTREFFEND |
|*Windows-Komponenten / Cloudinhalt|Windows-Blickpunkt auf Sperrbildschirm konfigurieren| NICHT ZUTREFFEND |**Deaktiviert** (Wenn diese Richtlinie deaktiviert ist, wird der Windows-Blickpunkt deaktiviert, und Benutzer können diesen nicht mehr als Sperrbildschirm auswählen. Benutzer sehen das Standardbild des Sperrbildschirms und können ein anderes Bild auswählen, sofern die Richtlinie „Ändern des Sperrbildschirmbilds verhindern“ nicht aktiviert ist.)|
|*Windows-Komponenten / Cloudinhalt|Keine Inhalte von Drittanbietern in Windows-Blickpunkt vorschlagen| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinie aktiviert ist, werden durch Windows-Blickpunktfeatures wie den Blickpunkt auf dem Sperrbildschirm, vorgeschlagene Apps im Startmenü oder Windows-Tipps keine Apps und Inhalte von Softwaredrittanbietern mehr vorgeschlagen. Benutzer sehen möglicherweise weiterhin Vorschläge und Tipps, damit sie mit Features und Apps von Microsoft produktiver arbeiten können.)|
|*Windows-Komponenten / Cloudinhalt|Keine Diagnosedaten für maßgeschneiderte Oberflächen verwenden| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, verwendet Windows keine Diagnosedaten (beispielsweise zur Nutzung von Browser, Apps und Features, je nach Wert der Einstellung „Diagnosedaten“) von diesem Gerät, um Inhalte des Sperrbildschirms, Windows-Tipps, Microsoft-Verbraucherprodukte und andere ähnliche Features anzupassen.)|
|*Windows-Komponenten / Cloudinhalt|Features von Windows-Blickpunkt deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Windows-Blickpunkt auf dem Sperrbildschirm, Windows-Tipps, Microsoft-Verbraucherprodukte und andere ähnliche Features werden deaktiviert. Diese Richtlinieneinstellung sollte aktiviert werden, wenn der Netzwerkdatenverkehr von Zielgeräten minimiert werden soll.)|
|Rand-UI|Nachverfolgung der App-Nutzung deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Diese Richtlinieneinstellung hindert Windows daran, die am häufigsten verwendeten und gesuchten Apps nachzuverfolgen. Wenn diese Richtlinieneinstellung aktiviert ist, werden die Apps in folgenden Rubriken alphabetisch sortiert:<p> – Suchergebnisse<p> – Bereiche „Suchen“ und „Gemeinsam nutzen“<p> – Dropdownliste der Apps in der Auswahl)|
|Datei-Explorer|Zwischenspeicherung von Bildern in Miniaturansicht deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, werden Miniaturansichten nicht zwischengespeichert.)|
|Datei-Explorer|Gängige Steuerungs- und Fensteranimationen deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Durch Deaktivieren von Animationen lässt sich die Benutzerfreundlichkeit für Benutzer mit visuellen Einschränkungen sowie die Leistung und die Akkulebensdauer in einigen Szenarien verbessern.)|
|Datei-Explorer|Anzeige der letzten Sucheinträge im Datei-Explorer-Suchfeld deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Deaktiviert den Vorschlag der letzten Abfragen für das Suchfeld und verhindert, dass Einträge im Suchfeld in der Registrierung zur späteren Verwendung gespeichert werden.)|
|Datei-Explorer|Zwischenspeicherung von Miniaturansichten in versteckten thumbs.db-Dateien deaktivieren| NICHT ZUTREFFEND |**Aktiviert** (Wenn diese Richtlinieneinstellung aktiviert ist, kann der Datei-Explorer keine thumbs.db-Dateien erstellen, lesen oder darin schreiben.)|

\* Stammt aus der [Windows Restricted Traffic Limited Functionality Baseline](https://go.microsoft.com/fwlink/?linkid=828887).

### <a name="system-services"></a>Systemdienste

Wenn du Systemdienste deaktivieren möchtest, um Ressourcen zu sparen, muss sichergestellt sein, dass der betreffende Dienst keine Komponente eines anderen Diensts ist. Im vorliegenden Dokument sowie in den verfügbaren GitHub-Skripts sind einige Dienste nicht in der Liste enthalten, weil sie nicht auf eine unterstützte Weise deaktiviert werden können.

Die meisten dieser Empfehlungen entsprechen den Empfehlungen für Windows Server 2016 mit Desktopdarstellung und basieren auf den [Anleitungen zur Deaktivierung von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung](../../security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server.md).

Viele Dienste, die möglicherweise deaktiviert werden können, sind auf den Typ „Manueller Start“ festgelegt. Ein Dienst dieses Typs wird nicht automatisch gestartet, sondern erst dann, wenn ein Prozess oder Ereignis eine Anforderung an den Dienst auslöst. Dienste, die bereits auf den manuellen Starttyp eingestellt sind, werden hier in der Regel nicht aufgeführt.

> [!NOTE]
> Du kannst aktuell ausgeführte Dienste mit diesem PowerShell-Beispielcode auflisten und dabei nur den Kurznamen des Diensts ausgeben:
>
> ```powershell
> Get-Service | Where-Object {$_.Status -eq 'Running'} | Select-Object -ExpandProperty Name
> ```

Die folgende Tabelle enthält einige Dienste, die in virtuellen Desktopumgebungen möglicherweise deaktiviert werden können:

| Windows-Dienst | Dienstname | Element | Anmerkungen|
| --------------- | ------------ | ---- | ------ |
|Mobilfunkzeit|autotimesvc|Dieser Dienst legt die Zeit auf der Grundlage der NITZ-Meldungen eines Mobilfunknetzes fest.|Möglicherweise sind solche Geräte in virtuellen Desktopumgebungen nicht verfügbar. <p>Weitere Informationen findest du in [diesem Artikel](/windows-hardware/drivers/network/mb-nitz-support). |
|GameDVR und Übertragungsbenutzerdienst|BcastDVRUserService|Dieser (benutzerbezogene) Dienst wird für Spielaufzeichnungen und Liveübertragungen verwendet.|HINWEIS: Dies ist ein benutzerbezogener Dienst, daher muss der Vorlagendienst deaktiviert sein. Dieser Benutzerdienst wird für Spielaufzeichnungen und Liveübertragungen verwendet.<p>Weitere Informationen findest du in [diesem Artikel](/windows-hardware/drivers/network/mb-nitz-support). |
|CaptureService|CaptureService|Aktiviert optionale Bildschirmerfassungsfunktionen für Anwendungen, die die Windows.Graphics.Capture-API aufrufen.|OneCore-Erfassungsdienst: Aktiviert optionale Bildschirmerfassungsfunktionen für Anwendungen, die die Windows.Graphics.Capture-API aufrufen.<p> Weitere Informationen finden Sie in [diesem Artikel](/uwp/api/windows.graphics.capture?view=winrt-19041&preserve-view=true).|
|Plattformdienst für verbundene Geräte|CDPSvc|Dieser Benutzerdienst wird für Szenarien mit der Plattform für verbundene Geräte verwendet.|Plattformdienst für verbundene Geräte <p> Weitere Informationen findest du in [diesem Artikel](/openspecs/windows_protocols/ms-cdp/929c2238-6d49-4ba4-a36a-37e732c4f736).|
|CDP-Benutzerdienst|CDPUserSvc| NICHT ZUTREFFEND |Benutzerdienst für Plattform für verbundene Geräte. Weitere Informationen findest du in [diesem Artikel](/openspecs/windows_protocols/ms-cdp/f5a15c56-ac3a-48f9-8c51-07b2eadbe9b4).<p> Dieser Benutzerdienst wird für Szenarien mit der Plattform für verbundene Geräte verwendet. <br><br>Dies ist ein benutzerbezogener Dienst, daher muss der Vorlagendienst deaktiviert sein (CDPUserSvc).|
|Laufwerke optimieren|defragsvc|Unterstützt den Computer bei einer effizienteren Ausführung durch das Optimieren von Dateien auf Speicherlaufwerken.|Virtuelle Desktoplösungen profitieren in der Regel nicht von der Datenträgeroptimierung. Diese „Laufwerke“ sind keine herkömmlichen Laufwerke, sondern häufig nur eine temporäre Speicherzuordnung.|
|Diagnoseausführungsdienst|DiagSvc|Führt Diagnoseaktionen zur Unterstützung bei der Problembehandlung aus.|Das Deaktivieren dieses Diensts unterbindet die Ausführung des Diagnoseausführungsdiensts der Windows-Diagnose.|
|Benutzererfahrung und Telemetrie im verbundenen Modus|DiagTrack|Dieser Dienst aktiviert Funktionen, die Benutzerfreundlichkeit in Anwendungen und im verbundenen Modus unterstützen. Außerdem verwaltet dieser Dienst die ereignisgesteuerte Sammlung und Übertragung von Diagnose- und Nutzungsdaten (die zur Verbesserung der Benutzerfreundlichkeit und Qualität der Windows-Plattform eingesetzt werden). Dazu müssen die Diagnose- und Nutzungseinstellungen in der Datenschutzoption unter „Feedback und Diagnose“ aktiviert sein.|Im nicht verbundenen Netzwerk Deaktivierung erwägen. Weitere Informationen findest du in [diesem Artikel](/windows/privacy/configure-windows-diagnostic-data-in-your-organization).|
|Diagnoserichtliniendienst|DPS|Der Diagnoserichtliniendienst ermöglicht die Problemerkennung, Problembehandlung und Lösung für Windows-Komponenten. Wenn dieser Dienst beendet wird, funktioniert die Diagnose nicht mehr.|Das Deaktivieren dieses Diensts unterbindet die Ausführung der Windows-Diagnose. Weitere Informationen finden Sie in [diesem Artikel](/uwp/api/Windows.System.Diagnostics?view=winrt-19041&preserve-view=true).|
|Geräteinstallations-Manager|DsmSvc|Ermöglicht die Erkennung, den Download und die Installation von gerätebezogener Software. |Wenn dieser Dienst deaktiviert wird, werden die Geräte ggf. mit veralteter Software konfiguriert und funktionieren unter Umständen nicht richtig. <p>Virtuelle Desktopumgebungen kontrollieren sehr genau, welche Software installiert wird, und sorgen für Konsistenz in der gesamten Umgebung.|
|Datennutzungsdienst|DusmSvc|Nutzung von Netzwerkdaten, Datenlimit, Einschränkung von Hintergrunddaten, getaktete Netzwerke.| Weitere Informationen finden Sie in [diesem Artikel](/uwp/schemas/mobilebroadbandschema/dusm/schema-root). |
|Windows-Dienst für mobile Hotspots|icssvc|Ermöglicht die Freigabe einer Datenverbindung für ein anderes Gerät.|Weitere Informationen findest du in [diesem Artikel](/uwp/api/Windows.Networking.NetworkOperators.NetworkOperatorTetheringAccessPointConfiguration?view=winrt-19041&preserve-view=true).|
|Microsoft Store-Installationsdienst|InstallService|Stellt Infrastrukturunterstützung für den Microsoft Store bereit. |Der Dienst wird bei Bedarf gestartet. Wenn der Dienst deaktiviert ist, funktionieren Installationen nicht ordnungsgemäß.<p>Es empfiehlt sich, diesen Dienst auf nicht persistenten virtuellen Desktops zu deaktivieren und auf persistenten virtuellen Desktops unverändert beizubehalten.|
|Geolocation-Dienst|Lfsvc|Überwacht den aktuellen Standort des Systems und verwaltet Geofences (geografische Standorte mit zugeordneten Ereignissen). |Wenn du diesen Dienst deaktivierst, sind Anwendungen nicht in der Lage, Benachrichtigungen zu Geolocations oder Geofences zu nutzen oder zu empfangen. Weitere Informationen findest du in [diesem Artikel](/uwp/api/Windows.Devices.Geolocation?view=winrt-19041&preserve-view=true).|
|Manager für heruntergeladene Karten|MapsBroker|Windows-Dienst für den Anwendungszugriff auf heruntergeladene Karten. Dieser Dienst wird bedarfsgesteuert je nach der Anwendung gestartet, die auf heruntergeladene Karten zugreift.|Wenn der Dienst deaktiviert wird, können Apps nicht auf Karten zugreifen. Weitere Informationen findest du in [diesem Artikel](/uwp/api/Windows.Services.Maps?view=winrt-19041&preserve-view=true).|
|MessagingService|MessagingService|Dienst, der SMS und verwandte Funktionen unterstützt.|Dies ist ein benutzerbezogener Dienst, daher muss der Vorlagendienst deaktiviert sein.|
|Synchronisierungshost|OneSyncSvc|Dieser Dienst synchronisiert E-Mail-, Kontakt-, Kalender- und verschiedene andere Benutzerdaten. |Wenn dieser Dienst nicht ausgeführt wird, funktionieren E-Mail-Programme und andere Anwendungen (UWP), die von dieser Funktionalität abhängig sind, nicht ordnungsgemäß. <p>Dies ist ein benutzerbezogener Dienst, daher muss der Vorlagendienst deaktiviert sein.|
|Kontaktdaten|PimIndexMaintenanceSvc|Indiziert Kontaktdaten für die schnelle Kontaktsuche. Wenn du diesen Dienst beendest oder deaktivierst, können Kontakte in den Suchergebnissen fehlen.|Dies ist ein benutzerbezogener Dienst, daher muss der Vorlagendienst deaktiviert sein.|
|Leistung|Leistung|Verwaltet die Energierichtlinie und die Zustellung der Energierichtlinienbenachrichtigung.|Virtueller Computer haben praktisch keinen Einfluss auf Energieeigenschaften. Wenn dieser Dienst deaktiviert ist, sind die Energieverwaltung und die entsprechende Berichterstellung nicht verfügbar. Weitere Informationen findest du in [diesem Artikel](/windows-hardware/drivers/powermeter/user-mode-power-service).|
|Zahlungs- und NFC/SE-Manager|SEMgrSvc|Verwaltet Zahlungen und sichere Elemente, die auf NFC (Near Field Communication) basieren.|In einer Unternehmensumgebung ist dieser Dienst für Zahlungen möglicherweise nicht erforderlich.|
|Microsoft Windows SMS-Routerdienst|SmsRouter|Leitet Nachrichten regelbasiert an die entsprechenden Clients weiter.|Dieser Dienst ist möglicherweise nicht erforderlich, wenn für das Messaging andere Tools wie z. B. Teams, Skype oder ähnliches verwendet werden. Weitere Informationen findest du in [diesem Artikel](/dotnet/framework/wcf/feature-details/routing-service).|.
|Superfetch (SysMain)|SysMain|Verwaltet und verbessert die Systemleistung im Zeitablauf.|Superfetch verbessert die Leistung in virtuellen Desktopumgebungen in der Regel aus verschiedenen Gründen nicht. Der zugrunde liegende Speicher ist häufig virtualisiert und möglicherweise per Striping auf mehrere Laufwerke verteilt. In einigen virtuellen Desktoplösungen wird der kumulierte Benutzerzustand verworfen, wenn der Benutzer sich abmeldet. Das SysMain-Feature sollte für jede Umgebung bewertet werden.|
|Dienst für Bildschirmtastatur und Schreibbereich|TabletInputService|Aktiviert die Stift- und Freihandfunktionalität der Bildschirmtastatur und des Schreibbereichs.|Nicht erforderlich, es sei denn, es wird ein aktiver Touchscreen oder ein Gerät für die handschriftliche Eingabe verwendet.|
|Update-Orchestrator-Dienst|UsoSvc|Verwaltet Windows-Updates. Falls beendet, können die neuesten Updates nicht auf Geräte heruntergeladen und dort installiert werden.|Virtuelle Desktopgeräte werden im Hinblick auf Updates meist sorgfältig verwaltet. Die Wartung erfolgt in der Regel innerhalb von Wartungsfenstern. In einigen Fällen kann ein Updateclient verwendet werden, z. B. SCCM. Eine Ausnahme hiervon sind Updates für Sicherheitssignaturen. Diese werden jederzeit auf jedem virtuellen Desktopgerät angewendet, damit die Signaturen immer aktuell sind. Wenn du diesen Dienst deaktivierst, führe einen Test aus, um sicherzustellen, dass Sicherheitssignaturen weiterhin installiert werden können.|
|Volumeschattenkopie|VSS|Verwaltet und implementiert Volumeschattenkopien, die zu Sicherungs- und anderen Zwecken verwendet werden. |Wenn dieser Dienst beendet wird, sind keine Schattenkopien für Sicherungen verfügbar, und die Sicherung kann eventuell fehlschlagen. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. Weitere Informationen findest du in [diesem Artikel](../../../WindowsServerDocs/storage/file-server/volume-shadow-copy-service.md).|
|Diagnosesystemhost|WdiSystemHost|Der Diagnosesystemhost wird vom Diagnoserichtliniendienst verwendet, um Diagnosen zu hosten, die für einen lokalen Dienst durchgeführt werden müssen. Wird dieser Dienst beendet, funktionieren alle davon abhängigen Diagnosen nicht mehr ordnungsgemäß.|Das Deaktivieren dieses Diensts unterbindet die Ausführung der Windows-Diagnose.
|Windows-Fehlerberichterstattung|WerSvc|Ermöglicht die Berichterstattung von Fehlern bei nicht mehr funktionierenden und reagierenden Programmen und das Angeben von Lösungen. Ermöglicht außerdem das Generieren von Protokollen für Diagnose- und Reparaturdienste. Wenn dieser Dienst beendet wird, funktioniert die Fehlerberichterstattung möglicherweise nicht ordnungsgemäß, und die Ergebnisse von Diagnosediensten und Reparaturen werden möglicherweise nicht angezeigt.|In virtuellen Desktopumgebungen wird die Diagnose oft in einem Offlineszenario und nicht in der Hauptproduktion durchgeführt. Außerdem deaktivieren einige Kunden WER ohnehin. WER benötigt eine winzige Menge an Ressourcen für viele verschiedene Angelegenheiten inklusive Fehler bei der Installation eines Geräts oder bei der Installation eines Updates. Weitere Informationen finden Sie in [diesem Artikel](/windows/win32/wer/windows-error-reporting).|
|Windows Search|WSearch|Stellt Inhaltsindizierung, Eigenschaftenzwischenspeicherung und Suchergebnisse für Dateien, E-Mails und andere Inhalte bereit.|Ein Deaktivieren dieses Diensts verhindert die Indizierung von E-Mails und anderen Elementen. Führen Sie Tests durch, bevor Sie diesen Dienst deaktivieren. Weitere Informationen finden Sie in [diesem Artikel](/windows/win32/search/-search-3x-wds-overview#windows-search-service). |
|Xbox Live Authentifizierungs-Manager|XblAuthManager|Stellt Authentifizierungs- und Autorisierungsservices für Xbox Live bereit. |Wenn dieser Dienst beendet wird, funktionieren einige Anwendungen möglicherweise nicht korrekt.
|Xbox Live-Spiele speichern|XblGameSave|Dieser Dienst synchronisiert für Xbox Live-Spiele gespeicherte Daten. |Wenn der Dienst beendet wird, werden die gespeicherten Spieldaten für Xbox Live nicht hochgeladen bzw. heruntergeladen.
|Xbox-Zubehörverwaltungsdienst|XboxGipSvc|Dieser Dienst verwaltet verbundenes Xbox Zubehör.| NICHT ZUTREFFEND |
|Xbox Live-Netzwerkservice|XboxNetApiSvc|Dieser Dienst unterstützt die Anwendungsprogrammierschnittstelle Windows.Networking.XboxLive.| NICHT ZUTREFFEND |

#### <a name="per-user-services-in-windows"></a>Benutzerbezogene Dienste in Windows

Benutzerbezogene Dienste werden erstellt, wenn ein Benutzer sich bei Windows oder Windows Server anmeldet, und sie werden beendet und gelöscht, wenn dieser Benutzer sich abmeldet. Diese Dienste werden im Sicherheitskontext des Benutzerkontos ausgeführt – dies bietet eine bessere Ressourcenverwaltung als der bisherige Ansatz, diese Art von Diensten im Explorer auszuführen, verknüpft mit einem vorkonfigurierten Konto oder als Aufgaben. Weitere Informationen finden Sie unter [Benutzerspezifische Dienste unter Windows](/windows/application-management/per-user-services-in-windows).

Wenn Sie beabsichtigen, einen Dienststartwert zu ändern, besteht die bevorzugte Methode darin, eine CMD-Eingabeaufforderung mit erhöhten Rechten zu öffnen und das Dienststeuerungs-Manager-Tool `SC.EXE` auszuführen. Weitere Informationen finden Sie unter [SC](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc754599(v=ws.11)).

### <a name="scheduled-tasks"></a>Geplante Aufgaben

Stellen Sie wie bei anderen Elementen in Windows sicher, dass ein Element nicht benötigt wird, bevor Sie eine geplante Aufgabe deaktivieren. Manche Aufgaben in virtuellen Desktopumgebungen, z. B. **StartComponentCleanup**, sollten möglicherweise nicht in der Produktion ausgeführt werden, eignen sich jedoch möglicherweise gut für die Ausführung während eines Wartungsfensters des „Golden Image“ (Referenzimage).

Die folgende Liste enthält Aufgaben, die Optimierungen oder Datensammlungen auf Computern durchführen, die ihren Status Neustarts übergreifend beibehalten. Wenn ein virtuelles Desktopgerät neu startet und alle Änderungen seit dem letzten Start verwirft, sind Optimierungen für physische Computer nicht hilfreich.

Du kannst alle aktuellen geplanten Tasks, einschließlich Beschreibungen, mit dem folgenden PowerShell-Code abrufen:

```powershell
  Get-ScheduledTask | Select-Object -Property TaskPath,TaskName,State,Description
```

> [!NOTE]
> Es gibt mehrere Aufgaben, die mit einem Skript nicht deaktiviert werden können, selbst wenn dieses über eine Eingabeaufforderung mit erhöhten Rechten ausgeführt wird. Die Empfehlungen hier sowie die GitHub-Skripts versuchen nicht, Aufgaben zu deaktivieren, die mit einem Skript nicht deaktiviert werden können.

|Name der geplanten Aufgabe|Beschreibung|
|-------------------|-----------|
|MNO|Metadatenparser für Darstellung eines mobilen Breitbandkontos|
|AnalyzeSystem|Diese Aufgabe analysiert das System auf Bedingungen, die einen hohen Energieverbrauch verursachen könnten.|
|Mobilfunk|Betrifft Mobilgeräte.|
|Kompatibilität|Sammelt Telemetrieinformationen bei Registrierung für das Programm zur Verbesserung der Benutzerfreundlichkeit von Microsoft.|
|Consolidator|Wenn der Benutzer zugestimmt hat, am Programm zur Verbesserung der Benutzerfreundlichkeit von Windows teilzunehmen, sammelt dieser Auftrag Nutzungsdaten und sendet diese an Microsoft.|
|Diagnose|(DiskFootprint im Aufgabenpfad). „DiskFootprint“ ist der kombinierte Beitrag aller Prozesse, die Speicher-E/A in Form von Speicherlesevorgängen, entsprechenden Schreibvorgängen und Leerungen generieren.|
|FamilySafetyMonitor|Initialisiert Überwachung und Erzwingung im Rahmen von Family Safety.|
|FamilySafetyRefreshTask|Synchronisiert die aktuellen Einstellungen mit dem Dienst für Microsoft Family-Features.|
|MapsToastTask|Diese Aufgabe zeigt verschiedene Popupbenachrichtigungen zur Karte.|
|Microsoft-Windows-DiskDiagnosticDataCollector|Die Windows-Datenträgerdiagnose meldet allgemeine Informationen zu Datenträger und System für Benutzer an Microsoft, die am Programm zur Verbesserung der Benutzerfreundlichkeit teilnehmen.|
|NotificationTask|Hintergrundaufgabe für das Durchführen von benutzerspezifischen Interaktionen und Webinteraktionen.|
|ProcessMemoryDiagnosticEvents|Plant eine Arbeitsspeicherdiagnose als Reaktion auf Systemereignisse.|
|Proxy|Diese Aufgabe sammelt autochk-SQM-Daten bei Registrierung für das Programm zur Verbesserung der Benutzerfreundlichkeit von Microsoft.|
|QueueReporting|Aufgabe der Windows-Fehlerberichterstattung zum Verarbeiten von Berichten in der Warteschlange.|
|RecommendedTroubleshootingScanner|Überprüfung auf von Microsoft empfohlene Problembehandlung.|
|RegIdleBackup|Aufgabe zur Registrierung einer Leerlaufsicherung|
|RunFullMemoryDiagnostic|Erkennt und behebt Probleme des physischen Speichers (RAM).|
|Geplant|Die von Windows geplante Wartungsaufgabe führt eine regelmäßige Wartung des Computersystems durch, indem Probleme automatisch behoben werden, oder sie werden über „Sicherheit und Wartung“ gemeldet.|
|ScheduledDefrag|Diese Aufgabe optimiert lokale Speicherlaufwerke.|
|SilentCleanup|Vom System zum Starten einer automatischen Datenträgerbereinigung im Hintergrund verwendete Wartungsaufgabe bei knappem Speicherplatz auf dem Datenträger.|
|SpeechModelDownloadTask|
|Sqm-Tasks|Diese Aufgabe sammelt Informationen zum Trusted Platform Module (TPM), zum sicheren Start und zum kontrollierten Start.|
|SR|Diese Aufgabe erstellt normale Systemschutzpunkte.|
|StartComponentCleanup|Wartungsaufgabe, die besser während Wartungsfenstern durchgeführt werden sollte.|
|StartupAppTask|Scannt Starteinträge und löst Benachrichtigungen für den Benutzer aus, wenn es zu viele Starteinträge gibt.|
|SyspartRepair|
|WindowsActionDialog|Benachrichtigung zum Speicherort|
|WinSAT|Misst die Leistung und Funktionen eines Systems|
|XblGameSaveTask|Xbox Live-Standbytask zum Speichern des Spiels|

### <a name="apply-windows-and-other-updates"></a>Anwenden von Windows- und anderen Updates

Ob von Microsoft Update oder deinen internen Ressourcen, wende verfügbare Updates einschließlich Windows Defender-Signaturen an. Dies ist ein guter Zeitpunkt, andere verfügbare Updates (einschließlich Updates für Microsoft Office, sofern installiert) und andere Softwareupdates anzuwenden. Wenn PowerShell im Image verbleibt, kannst du die neueste verfügbare Hilfe für PowerShell herunterladen, indem du den Befehl `Update-Help`Update-Help ausführst.

#### <a name="servicing-os-and-apps"></a>Wartung von Betriebssystem und Apps

Irgendwann während des Bildoptimierungsprozesses sollten verfügbare Windows-Updates angewendet werden. In den Windows 10-Updateeinstellungen ist eine Einstellung vorhanden, mit der zusätzliche Updates bereitgestellt werden können: Diese finden Sie unter **Einstellungen** > **Erweiterte Optionen**. Legen Sie dort **Updates für andere Microsoft-Produkte bereitstellen, wenn ein Windows-Update ausgeführt wird** auf **Ein** fest.

![Screenshot: Menü „Erweiterte Optionen“ mit aktivierter Einstellung „Updates für andere Microsoft-Produkte bereitstellen“](media/rds-vdi-recommendations-1909/servicing.png)

Dies wäre eine gute Einstellung, falls du Microsoft-Anwendungen wie Microsoft Office im Basisimage installieren möchtest. Auf diese Weise ist Office auf dem neuesten Stand, wenn das Image in Betrieb genommen wird. Auch .NET-Updates und Updates für bestimmte Drittanbieterkomponenten wie Adobe sind über Windows Update verfügbar.

Ein sehr wichtiger Aspekt für nicht persistente virtuelle Desktopgeräte sind Sicherheitsupdates, einschließlich Definitionsdateien für Sicherheitssoftware. Diese Updates werden möglicherweise mehrmals täglich veröffentlicht.

Für Windows Defender empfiehlt es sich, Updates auch in nicht persistenten virtuellen Desktopumgebungen zuzulassen. Die Updates werden bei fast jeder Anmeldung angewendet, sind jedoch klein und sollten kein Problem darstellen. Außerdem gelangt das Gerät nicht in den Rückstand, da nur die neuesten verfügbaren Updates angewendet werden. Dasselbe kann für Definitionsdateien von Drittanbietern gelten.

>[!NOTE]
> Store-Apps (UWP-Apps) werden über den Windows Store aktualisiert. Moderne Versionen von Office wie Office 365 werden über ihre eigenen Mechanismen aktualisiert, wenn sie direkt mit dem Internet verbunden sind, oder andernfalls über Verwaltungstechnologien.

#### <a name="windows-system-startup-event-traces-autologgers"></a>Ablaufverfolgungen für Ereignisse beim Windows-Systemstart (AutoLoggers)

Windows ist standardmäßig darauf konfiguriert, Diagnosedaten zu sammeln und zu speichern. Dies soll eine Diagnose ermöglichen oder Daten aufzeichnen, falls weitere Problembehandlung erforderlich ist. Die automatische Systemablaufverfolgungen befindet sich am auf der folgenden Abbildung gezeigten Ort:

![Screenshot: App „Computerverwaltung“, in der der Ordner „Ereignisablaufverfolgungssitzungen“ geöffnet und die Datei „WiFiSession“ ausgewählt ist](media/rds-vdi-recommendations-1909/system-traces.png)

Einige der unter **Ereignisablaufverfolgungssitzungen** und **Startereignis-Ereignisablaufverfolgungssitzungen** angezeigten Ablaufverfolgungen können und sollten nicht beendet werden. Andere, z. B. die WiFiSession-Ablaufverfolgung, können beendet werden. Zum Beenden einer unter **Ereignisablaufverfolgungssitzungen** ausgeführten Ablaufverfolgung können Sie mit der rechten Maustaste klicken und dann **Beenden** auswählen. Gehe folgendermaßen vor, um zu verhindern, dass die Ablaufverfolgungen automatisch beim Start gestartet werden:

1. Wählen Sie den Ordner **Startereignis-Ereignisablaufverfolgungssitzungen** aus.

2. Suchen Sie die relevante Ablaufverfolgungsdatei, und klicken Sie auf diese, um sie zu öffnen.

3. Wähle die Registerkarte **Ablaufverfolgungssitzung** aus.

4. Deaktivieren Sie das Kontrollkästchen **Aktiviert**.

5. Klicken Sie auf **OK**.

In der folgenden Tabelle werden einige Systemablaufverfolgungen aufgelistet, die Sie in Ihren virtuellen Desktopumgebungen deaktivieren sollten:

|Name|Anmerkungen|
|---|--------|
|Cellcore|[https://docs.microsoft.com/windows-hardware/drivers/network/cellular-architecture-and-driver-model](/windows-hardware/drivers/network/cellular-architecture-and-driver-model)|
|CloudExperienceHostOOBE|Die Dokumentation finden Sie [hier](/windows/security/identity-protection/hello-for-business/hello-how-it-works-technology#cloud-experience-host).|
|DiagLog|Ein vom Diagnoserichtliniendienst generiertes Protokoll, die Dokumentation finden Sie [hier](/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server).|
|RadioMgr|Die Dokumentation finden Sie [hier](/windows-hardware/drivers/nfc/what-s-new-in-nfc-device-drivers).|
|ReadyBoot|Die Dokumentation finden Sie [hier](/previous-versions/windows/desktop/xperf/readyboot-analysis).|
|WDIContextLog|Schnittstelle für WLAN-Gerätetreiber, die Dokumentation finden Sie hier. |
|WiFiDriverIHVSession|Die Dokumentation finden Sie [hier](/windows-hardware/drivers/network/user-initiated-feedback-normal-mode).|
|WiFiSession|Diagnoseprotokoll für WLAN-Technologie – diese Protokollierung wird nur benötigt, wenn WLAN implementiert ist.|
|WinPhoneCritical|Diagnoseprotokoll für Smartphones (Windows) – diese Protokollierung wird nur benötigt, wenn Smartphones verwendet werden.|

#### <a name="windows-defender-optimization-in-the-virtual-desktop-environment"></a>Windows Defender-Optimierung in der virtuellen Desktopumgebung

Weitere Informationen zur Optimierung von Windows Defender in einer virtuellen Desktopumgebung finden Sie unter [Bereitstellungshandbuch für Microsoft Defender Antivirus in einer VDI-Umgebung (Virtual Desktop Infrastructure)](/windows/security/threat-protection/windows-defender-antivirus/deployment-vdi-windows-defender-antivirus).

Der oben genannte Artikel enthält Verfahren zur Wartung des Goldimages für virtuelle Desktops und der virtuellen Desktopclients während ihrer Ausführung. Wenn virtuelle Desktopgeräte ihre Windows Defender-Signaturen aktualisieren müssen, sollten Sie Neustarts staffeln und nach Möglichkeit außerhalb der Geschäftszeiten planen, um die Netzwerkbandbreite zu reduzieren. Die Signaturupdates von Windows Defender können intern auf Dateifreigaben enthalten sein. Wenn möglich, sollten sich diese Dateifreigaben in denselben oder nahegelegenen Netzwerksegmenten wie die virtuellen Desktopgeräte befinden.

#### <a name="client-network-performance-tuning-by-registry-settings"></a>Clientnetzwerk-Leistungsoptimierung durch Registrierungseinstellungen

Es gibt einige Registrierungseinstellungen, mit denen die Netzwerkleistung gesteigert werden kann. Das ist besonders in Umgebungen wichtig, in denen das virtuelle Desktopgerät oder der physische Computer eine primär netzwerkbasierte Arbeitsauslastung besitzt. Die Einstellungen in diesem Abschnitt werden empfohlen, um die Leistung zugunsten des Arbeitsauslastungsprofils des Netzwerks zu optimieren, indem zusätzliche Pufferung und Zwischenspeicherung von Verzeichniseinträgen usw. festgelegt werden.

> [!NOTE]
> Einige Einstellungen in diesem Abschnitt sind nur registrierungsbasiert und sollten in das Basisimage integriert werden, bevor das Image für die Produktion bereitgestellt wird.

Die folgenden Einstellungen sind unter [Richtlinien zur Optimierung der Leistung für Windows Server 2016](../../administration/performance-tuning/index.md) dokumentiert.

#### <a name="disablebandwidththrottling"></a>DisableBandwidthThrottling

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableBandwidthThrottling`

Gilt für Windows 10. Der Standardwert ist **0**. Standardmäßig drosselt der SMB-Redirector den Durchsatz für Netzwerkverbindungen mit hoher Latenz. In einigen Fällen besteht das Ziel hierbei darin, netzwerkbezogene Timeouts zu verhindern. Durch das Festlegen dieses Registrierungswerts auf **1** wird diese Art der Drosselung deaktiviert. So wird für Netzwerkverbindungen mit hoher Latenz ein höherer Durchsatz für Dateiübertragungen ermöglicht. Erwäge, diesen Wert auf **1** festzulegen.

#### <a name="fileinfocacheentriesmax"></a>FileInfoCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheEntriesMax`

Gilt für Windows 10. Der Standardwert ist **64**, und der gültige Bereich reicht von 1 bis 65.536. Dieser Wert wird verwendet, um die Menge an Dateimetadaten zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf viele Dateien zugegriffen wird. Erwäge, diesen Wert auf **1.024** zu erhöhen.

#### <a name="directorycacheentriesmax"></a>DirectoryCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntriesMax`

Gilt für Windows 10. Der Standardwert ist **16**, und der gültige Bereich reicht von 1 bis 4.096. Dieser Wert wird verwendet, um die Menge von Verzeichnisinformationen zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf große Verzeichnisse zugegriffen wird. Erwäge, diesen Wert auf **1.024** zu erhöhen.

#### <a name="filenotfoundcacheentriesmax"></a>FileNotFoundCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheEntriesMax`

Gilt für Windows 10. Der Standardwert ist **128**, und der gültige Bereich reicht von 1 bis 65.536. Dieser Wert wird verwendet, um die Menge von Dateinameninformationen zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf viele Dateinamen zugegriffen wird. Erwäge, diesen Wert auf **2.048** zu erhöhen.

#### <a name="dormantfilelimit"></a>DormantFileLimit

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantFileLimit`

Gilt für Windows 10. Der Standardwert beträgt **1.023**. Mit diesem Parameter wird die maximale Anzahl von Dateien angegeben, die auf einer freigegebenen Ressource geöffnet bleiben soll, nachdem die Datei von der Anwendung geschlossen wurde. Wenn viele tausend Clients Verbindungen mit SMB-Servern herstellen, solltest du diesen Wert auf **256** reduzieren.

Du kannst viele dieser SMB-Einstellungen mit den Windows PowerShell-Cmdlets [Set-SmbClientConfiguration](/powershell/module/smbshare/set-smbclientconfiguration?view=win10-ps&preserve-view=true) und [Set-SmbServerConfiguration](/powershell/module/smbshare/set-smbserverconfiguration?view=win10-ps&preserve-view=true) konfigurieren. Einstellungen nur für die Registrierung auch mit Windows PowerShell konfiguriert werden, wie im folgenden Beispiel gezeigt:

```powershell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" RequireSecuritySignature -Value 0 -Force
```

#### <a name="additional-settings-from-the-windows-restricted-traffic-limited-functionality-baseline-guidance"></a>Zusätzliche Einstellungen aus dem Leitfaden „Windows Restricted Traffic Limited Functionality Baseline“.

Microsoft hat für Umgebungen, die nicht direkt mit dem Internet verbunden sind oder für die die Menge an Daten reduziert werden soll, die an Microsoft und andere Dienste gesendet werden, eine Baseline veröffentlicht, die mit den gleichen Verfahren wie die [Windows-Sicherheitsbaselines](/windows/device-security/windows-security-baselines) erstellt wurde.

Die [Windows Restricted Traffic Limited Functionality Baseline](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services)-Einstellungen sind in der Gruppenrichtlinientabelle mit einem Sternchen gekennzeichnet.

#### <a name="disk-cleanup-including-using-the-disk-cleanup-wizard"></a>Datenträgerbereinigung (einschließlich des Datenträgerbereinigungs-Assistenten)

Die Datenträgerbereinigung kann besonders bei Gold-/Masterimageimplementierungen virtueller Desktops hilfreich sein. Nachdem das Gold-/Masterimage vorbereitet, aktualisiert und konfiguriert wurde, besteht eine der letzten Aufgaben in der Datenträgerbereinigung. Die Optimierungsskripts auf GitHub.com enthalten PowerShell-Code für gängige Datenträgerbereinigungstasks.

> [!NOTE]
> Die Einstellungen für die Datenträgerbereinigung finden Sie unter „Einstellungen > System > Speicher“. Standardmäßig wird Speicheroptimierung ausgeführt, wenn der Schwellenwert für niedrigen freien Speicherplatz erreicht wird.
>
> Weitere Informationen zur Verwendung von Speicheroptimierung mit benutzerdefiniert Azure-VHD-Images finden Sie unter [Vorbereiten und Anpassen eines VHD-Masterimages](/azure/virtual-desktop/set-up-customize-master-image).
>
> Für Windows Virtual Desktop-Sitzungshosts, für die Windows 10 Enterprise oder Windows 10 Enterprise (mehrere Sitzungen) verwendet wird, empfehlen wir die Deaktivierung der Speicheroptimierung. Sie können Speicheroptimierung in den Einstellungen unter **Speicher** deaktivieren.

Hier erhältst du Vorschläge für verschiedene Datenträgerbereinigungsaufgaben. Diese sollten vor der Implementierung alle getestet werden:

1. Speicheroptimierung kann manuell oder automatisch verwendet werden. Weitere Informationen zu Speicheroptimierung finden Sie in diesem Artikel: Verwenden von OneDrive und Speicheroptimierung in Windows 10 zum Verwalten von Speicherplatz
2. Bereinigen Sie temporäre Dateien und Protokolle manuell. Führe an einer Eingabeaufforderung mit erhöhten Rechten diese Befehle aus:

   1. `Del C:\*.tmp /s`
   2. `C:\*.etl /s`
   3. `C:\*.evtx /s`

   ```powershell
   Get-ChildItem -Path c:\ -Include *.tmp, *.dmp, *.etl, *.evtx, thumbcache*.db, *.log -File -Recurse -Force -ErrorAction SilentlyContinue | Remove-Item -ErrorAction SilentlyContinue

   Remove-Item -Path $env:ProgramData\Microsoft\Windows\WER\Temp\* -Recurse -Force -ErrorAction SilentlyContinue

   Remove-Item -Path $env:ProgramData\Microsoft\Windows\WER\ReportArchive\* -Recurse -Force -ErrorAction SilentlyContinue

   Remove-Item -Path $env:ProgramData\Microsoft\Windows\WER\ReportQueue\* -Recurse -Force -ErrorAction SilentlyContinue

   Clear-RecycleBin -Force -ErrorAction SilentlyContinue

   Clear-BCCache -Force -ErrorAction SilentlyContinue
   ```

3. Löschen Sie nicht verwendete Profile auf dem System, indem Sie den folgenden Befehl ausführen:

    `wmic path win32_UserProfile where LocalPath="C:\\users\\<users>" Delete`

Wenn Sie Fragen oder Bedenken bezüglich der in diesem Dokument enthaltenen Informationen haben, wenden Sie sich an Ihr Microsoft-Kundenteam, lesen Sie den [Expertenblog zu virtuellen Windows-Desktops](https://community.windows.com/stories/virtual-desktop-windows-10), veröffentlichen Sie einen Beitrag im [Windows Virtual Desktop-Forum](https://techcommunity.microsoft.com/t5/windows-virtual-desktop/bd-p/WindowsVirtualDesktop), oder kontaktieren Sie [Microsoft](https://support.microsoft.com/contactus/).

### <a name="re-enable-windows-update"></a>Erneutes Aktivieren von Windows Update

Wenn Sie Windows Updates nach der Deaktivierung wieder aktivieren möchten (z. B. für persistente virtuelle Desktops), befolgen Sie diese Schritte:

1. Aktivieren Sie Gruppenrichtlinieneinstellungen erneut:

   - Navigieren Sie zu **Lokale Computerrichtlinie** > **Computerkonfiguration** > **Administrative Vorlagen** > **System** > **Internetkommunikationsverwaltung** > **Internetkommunikationseinstellungen**.
     - Deaktivieren Sie den Zugriff auf alle Windows Update-Features, indem Sie die Einstellung von **Aktiviert** in **Nicht konfiguriert** ändern.
   - Navigieren Sie zu **Lokale Computerrichtlinie** > **Computerkonfiguration** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update**.
     - Entfernen Sie den Zugriff auf alle Windows Update-Features, indem Sie die Einstellung von **Aktiviert** in **Nicht konfiguriert** ändern.
     - Unterbinden Sie die Verbindungsherstellung mit Windows Update-Internetseiten, indem Sie die Einstellung von **Aktiviert** in **Nicht konfiguriert** ändern.
   - Navigieren Sie zu **Lokale Computerrichtlinie** > **Computerkonfiguration** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update** > **Windows Update for Business**.
     - Wählen Sie aus, wann Qualitätsupdates empfangen werden sollen (Änderung von **Aktiviert** in **Nicht konfiguriert**).
   - Navigieren Sie zu **Lokale Computerrichtlinie** > **Computerkonfiguration** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Update** > **Windows Update for Business**.
     - Wähle aus, wann Vorschaubuilds und Featureupdates empfangen werden sollen (Änderung aus **Aktiviert** in **Nicht konfiguriert**).

2. Erneutes Aktivieren von Diensten:

   - Ändern Sie den **Orchestratordienst** von **Deaktiviert** in **Automatisch (verzögerter Start)** .

3. Bearbeiten Sie die Windows-Registrierung. Gehen Sie dabei vorsichtig vor.

   - Wechseln Sie zu `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UpdatePolicy\PolicyState`.
     - Ändern Sie **DeferQualityUpdates** von 1 in 0.
   - `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UpdatePolicy\Settings`
     - Löschen Sie sämtliche vorhandenen Werte für **PausedQualityDate**.
   - Wechseln Sie zu `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\WAU`.
     - Legen Sie **Deaktiviert** fest.

4. Erneutes Aktivieren von geplanten Aufgaben:

   - Navigieren Sie zu **Aufgabenplanungsbibliothek** > **Microsoft** > **Windows** > **InstallService** > **ScanForUpdates**.
   - Navigieren Sie zu **Aufgabenplanungsbibliothek** > **Microsoft** > **Windows** > **InstallService** > **ScanForUpdatesAsUser**.

5. Starten Sie das Gerät neu, damit diese Einstellungen wirksam werden.

6. Wenn Sie die auf dem Gerät angebotenen Featureupdates nicht nutzen möchten, können Sie unter **Einstellungen** > **Windows Update** > **Erweiterte Optionen** > **Installationszeitpunkt für Updates auswählen** die Option **Ein Funktionsupdate enthält neue Funktionen und Verbesserungen und kann für die folgende Anzahl von Tagen verzögert werden:** manuell auf einen Wert ungleich null (z. B. 180 oder 365) festlegen.

## <a name="additional-information"></a>Weitere Informationen

In der [Windows Virtual Desktop-Dokumentation](https://azure.microsoft.com/services/virtual-desktop/) erfahren Sie mehr über die VDI-Architektur von Microsoft.

Wenn Sie bei der Problembehandlung von Sysprep zusätzliche Hilfe benötigen, sollten Sie den Artikel [Sysprep-Fehler nach dem Entfernen oder Aktualisieren von Microsoft Store-Apps, die integrierte Windows-Images enthalten](https://support.microsoft.com/help/2769827/sysprep-fails-after-you-remove-or-update-windows-store-apps-that-inclu) lesen.
