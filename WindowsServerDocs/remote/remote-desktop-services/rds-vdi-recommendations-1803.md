---
title: Optimieren von Windows 10, Version 1803, für eine VDI-Rolle (Virtuelle Desktopinfrastruktur)
description: Empfohlene Einstellungen und Konfiguration zum Minimieren des Mehraufwands für Windows 10-1803-Desktops, die als VDI-Images verwendet werden
ms.author: robsmi
ms.topic: article
author: jaimeo
ms.openlocfilehash: 4ba432e13785694844229a41f2966eb7cf65fa7e
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078637"
---
# <a name="optimizing-windows-10-version-1803-for-a-virtual-desktop-infrastructure-vdi-role"></a>Optimieren von Windows 10, Version 1803, für eine VDI-Rolle (Virtuelle Desktopinfrastruktur)

Dieser Artikel hilft dir bei der Auswahl von Einstellungen für Windows 10, Version 1803 (Build 17134), die zur besten Leistung in einer VDI-Umgebung (Virtuelle Desktopinfrastruktur) führen sollten. Alle Einstellungen in diesem Handbuch sind *Empfehlungen, die berücksichtigt werden sollten*, und keine Anforderungen.

In einer VDI-Umgebung sind die wichtigsten Möglichkeiten zur Optimierung der Leistung von Windows 10, App-Grafikneuzeichnungen und Hintergrundaktivitäten, die keinen großen Nutzen für die VDI-Umgebung haben, zu minimieren und generell laufende Prozesse auf das absolute Minimum zu reduzieren. Ein sekundäres Ziel ist, den Verbrauch von Speicherplatz auf dem Datenträger im Basisimage auf ein Minimum zu reduzieren. Bei VDI-Implementierungen kann die kleinstmögliche Basisimagegröße („goldene“ Imagegröße) die Speicherauslastung auf dem Hypervisor leicht reduzieren und ebenso eine kleine Reduzierung der gesamten Netzwerkoperationen bewirken, die erforderlich sind, um das Desktopimage für den Verbraucher bereitzustellen.

> [!NOTE]
> Die hier empfohlenen Einstellungen können auf andere Installationen von Windows 10, Version 1803 auf physischen wie virtuellen Geräten angewendet werden. Alle Empfehlungen in diesem Thema sollten von Windows 10, Version 1803 unterstützt werden.

> [!TIP]
> Ein Skript, das die in diesem Thema beschriebenen Optimierungen implementiert, sowie eine GPO-Exportdatei, die du mit **LGPO.exe** importieren kannst, sind unter [TheVDIGuys](https://github.com//TheVDIGuys) auf GitHub verfügbar.

## <a name="vdi-optimization-principles"></a>Prinzipien der VDI-Optimierung

Eine VDI-Umgebung stellt einem Computerbenutzer über ein Netzwerk eine vollständige Desktopsitzung einschließlich Anwendungen zur Verfügung. VDI-Umgebungen verwenden in der Regel ein Basis-Betriebssystemimage, das dann die Grundlage für die Desktops bildet, die den Benutzern anschließend zur Arbeit präsentiert werden. Es gibt verschiedene VDI-Implementierungen wie „dauerhaft“, „nicht dauerhaft“ und „Desktopsitzung“. Der dauerhafte Typ bewahrt Änderungen am VDI-Desktopbetriebssystem von einer Sitzung zur nächsten. Der nicht dauerhaft Typ bewahrt Änderungen am VDI-Desktopbetriebssystem nicht von einer Sitzung zur nächsten. Für den Benutzer unterscheidet sich dieser Desktop kaum von anderen virtuellen oder physischen Geräten, außer dass über ein Netzwerk auf ihn zugegriffen wird.

Die Optimierungseinstellungen würden auf einem Referenzgerät durchgeführt. Eine VM ist ein idealer Ort, um das Image zu erstellen, da du den Status speichern, Prüfpunkte und Backups erstellen und andere nützliche Aufgaben erledigen kannst. Beginne mit der Installation des Standardbetriebssystems auf der Basis-VM, und optimiere dann die Basis-VM für die VDI-Nutzung, indem du nicht benötigte Apps entfernst, Windows- und andere Updates installierst, temporäre Dateien löschst, Einstellungen anwendest usw.

Es gibt andere Arten von VDI, z.B. dauerhafte und Remotedesktopdienste (Remote Desktop Services, RDS). Eine eingehende Diskussion über diese Technologien ist nicht Gegenstand dieses Themas, das sich auf die Windows-Basisimageeinstellungen in Bezug auf andere Faktoren in der Umgebung wie die Hostoptimierung konzentriert.

### <a name="persistent-vdi"></a>Dauerhafte VDI

Dauerhafte VDI ist auf der Basisebene eine VM, die den Betriebssystemzustand zwischen Neustarts speichert. Andere Softwareebenen der VDI-Lösung bieten den Benutzern einen einfachen und nahtlosen Zugriff auf die ihnen zugeordneten VMs, oft mit einer Single-Sign-On-Lösung.

Es gibt mehrere verschiedene Implementierungen von dauerhafter VDI:

- Herkömmliche VMs, bei denen die VM über eine eigene virtuelle Festplattendatei verfügt, starten normal, speichern Änderungen von einer Sitzung zur nächsten und sind im Wesentlichen nur eine normale VM. Der Unterschied besteht darin, wie der Benutzer auf diese VM zugreift. Möglicherweise gibt es ein Webportal, in dem sich der Benutzer anmeldet und das den Benutzer automatisch zu einer oder mehreren zugewiesenen VDI-VMs leitet.

- Imagebasierter dauerhafter virtueller Computer mit persönlichen virtuellen Datenträgern. In dieser Art der Implementierung ist ein Basis-/Goldimage auf einem oder mehreren Hostservern vorhanden. Eine VM wird erstellt, und ein oder mehrere virtuelle Datenträger werden erstellt und dieser Festplatte zur dauerhaften Speicherung zugewiesen.

    - Wenn der virtuelle Computer gestartet wird, wird eine Kopie des Basisimages in den Arbeitsspeicher des virtuellen Computers gelesen. Gleichzeitig wird ein dauerhafter virtueller Datenträger dieser VM zugeordnet, wobei etwaige frühere Betriebssystemänderungen durch einen komplexen Prozess zusammengeführt wurden.

    - Änderungen wie Ereignisprotokollschreiben, Protokollschreiben usw. werden auf den virtuellen Lese-/Schreibdatenträger umgeleitet, der dieser VM zugeordnet ist.

    - Unter diesen Umständen kann die Wartung von Betriebssystem und Apps mit herkömmlicher Wartungssoftware wie Windows Server Update Services oder anderen Verwaltungstechnologien normal funktionieren.

### <a name="non-persistent-vdi"></a>Nicht dauerhafte VDI

Wenn eine nicht dauerhafte VDI-Implementierung auf einem Basis- oder „Gold“-Image basiert, werden die Optimierungen meist im Basisimage und dann über lokale Einstellungen und lokale Richtlinien durchgeführt.

Bei imagebasierten, nicht dauerhaften VDIs ist das Basisimage schreibgeschützt. Wenn eine nicht dauerhafte VDI-VM gestartet wird, wird eine Kopie des Basisimages zum virtuellen Computer gestreamt. Aktivitäten, die während des Startvorgangs und danach bis zum nächsten Neustart auftreten, werden an einen temporären Speicherort umgeleitet. Normalerweise werden den Benutzern Netzwerkspeicherorte zur Verfügung gestellt, um ihre Daten zu speichern. In einigen Fällen wird das Profil des Benutzers mit der Standard-VM zusammengeführt, um dem Benutzer seine Einstellungen zur Verfügung zu stellen.

Ein wichtiger Aspekt der nicht dauerhaften VDI, die auf einem einzigen Image basiert, ist die Wartung. Updates des Betriebssystems werden in der Regel einmal pro Monat bereitgestellt.
Bei der imagebasierten VDI gibt es eine Reihe von Prozessen, die durchgeführt werden müssen, um Aktualisierungen des Images zu erhalten:

- Alle VMs auf einem bestimmten Host, die vom Basisimage abgeleitet sind, müssen heruntergefahren oder ausgeschaltet werden. Dies bedeutet, dass die Benutzer auf andere virtuelle Computer umgeleitet werden.

- Das Basisimage wird anschließend geöffnet und gestartet. Alle Wartungsaktivitäten wie z.B. Betriebssystemupdates, .NET-Updates, App-Updates etc. werden dann ausgeführt.

- Alle neuen Einstellungen, die angewendet werden müssen, werden zu diesem Zeitpunkt angewendet.

- Jegliche sonstige Wartung wird zu diesem Zeitpunkt durchgeführt.

- Das Basisimage wird anschließend heruntergefahren.

- Das Basisimage wird versiegelt und so eingestellt, dass es wieder in die Produktion geht.

Benutzer dürfen sich wieder anmelden.

> [!NOTE]
> Windows 10 führt in regelmäßigen Abständen automatisch eine Reihe von Wartungsaufgaben durch. Eine geplante Aufgabe wird standardmäßig jeden Tag um 3:00 Uhr Ortszeit ausgeführt. Diese geplante Aufgabe führt eine Liste von Aufgaben einschließlich der Windows Update-Bereinigung durch. Du kannst alle Kategorien der Wartung anzeigen, die automatisch mit dem folgenden PowerShell-Befehl ausgeführt werden:
>
>```powershell
>Get-ScheduledTask | ? {$_.Settings.MaintenanceSettings}
>```
>

Eine der Herausforderungen bei nicht dauerhaften VDIs besteht darin, dass beim Abmelden eines Benutzers fast die gesamte Betriebssystemaktivität verworfen wird. Das Profil und/oder der Status des Benutzers können gespeichert werden, aber die VM selbst verwirft fast alle Änderungen, die seit dem letzten Start vorgenommen wurden. Daher sind Optimierungen, die für einen Windows-Computer bestimmt sind, der den Zustand von einer Sitzung zur nächsten speichert, nicht anwendbar.

Je nach Architektur der VDI-VM sind PreFetch, SuperFetch und Ähnliches von einer Sitzung zur nächsten nicht hilfreich, da alle Optimierungen beim VM-Neustart verworfen werden. Die Indexierung kann eine teilweise Verschwendung von Ressourcen sein, ebenso wie alle Festplattenoptimierungen, z.B. die herkömmliche Defragmentierung.

### <a name="to-sysprep-or-not-sysprep"></a>Sysprep – ja oder nein?

Windows 10 verfügt über eine integrierte Funktion, das [Systemvorbereitungstool](/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview), häufig als „Sysprep“ (System Preparation) bezeichnet. Mit dem Sysprep-Tool wird ein benutzerdefiniertes Windows 10-Image für die Duplizierung vorbereitet. Der Sysprep-Prozess stellt sicher, dass das resultierende Betriebssystem für den Einsatz in der Produktion eindeutig ist.
Es gibt Gründe, die für und gegen die Ausführung von Sysprep sprechen. Im Falle von VDI möchtest du vielleicht die Möglichkeit haben, das Standardbenutzerprofil anzupassen, das als Profilvorlage für nachfolgende Benutzer verwendet wird, die sich mit diesem Image anmelden. Möglicherweise möchtest du gern einige Apps installieren, aber auch die Möglichkeit haben, die Einstellungen pro App zu steuern.

Die Alternative ist, eine Standard-ISO-Datei für die Installation zu verwenden, möglicherweise unter Verwendung einer Antwortdatei für unbeaufsichtigte Installationen, und eine Aufgabensequenz für die Installation von Anwendungen oder deren Entfernen. Du kannst auch eine Aufgabensequenz verwenden, um lokale Richtlinieneinstellungen im Image festzulegen, vielleicht mit dem Tool [Local Group Policy Object Utility (LGPO)](/archive/blogs/secguide/lgpo-exe-local-group-policy-object-utility-v1-0) (Lokales Gruppenrichtlinienobjekt (Hilfsprogramm)).

#### <a name="vdi-optimization-categories"></a>Kategorien für VDI-Optimierung

- Globale Betriebssystemeinstellungen

    - UWP-App-Bereinigung

    - Bereinigung optionaler Features

    - Lokale Richtlinieneinstellungen

    - Systemdienste

    -   Geplante Aufgaben

    -   Anwenden von Windows-Updates

    -   Automatische Windows-Ablaufverfolgungen

    -   Datenträgerbereinigung vor dem Finalisieren (Versiegeln) des Images

-   Benutzereinstellungen

-   Hypervisor-/Hosteinstellungen

- [Optimieren der Netzwerkleistung von Windows 10 mit Registrierungseinstellungen](#tuning-windows-10-network-performance-by-using-registry-settings)

- Zusätzliche Einstellungen aus dem Leitfaden [Windows Restricted Traffic Limited Functionality Baseline](https://go.microsoft.com/fwlink/?linkid=828887) (Windows-Baseline für eingeschränkten Datenverkehr und begrenzte Funktionalität).

- [Datenträgerbereinigung](#disk-cleanup-including-using-the-disk-cleanup-wizard)

### <a name="universal-windows-platform-app-cleanup"></a>UWP-App-Bereinigung

Ein VDI-Image sollte unter anderem so klein wie möglich sein. Eine Möglichkeit, die Imagegröße zu reduzieren, besteht darin, UWP-Anwendungen zu entfernen, die nicht in der Umgebung verwendet werden. Unter den UWP-Anwendungen gibt es die wichtigsten, auch als Nutzlast bezeichneten Anwendungsdateien. Im Profil jedes Benutzers ist eine kleine Menge an Daten für anwendungsspezifische Einstellungen gespeichert. Auch im Profil „Alle Benutzer“ ist eine kleine Menge an Daten vorhanden.

Konnektivität und Timing sind alles, wenn es um die UWP-App-Bereinigung geht. Wenn du dein Basisimage für ein Gerät ohne Netzwerkverbindung bereitstellst, kann Windows 10 keine Verbindung mit Microsoft Store herstellen und Apps herunterladen sowie versuchen, sie zu installieren, während du versuchst, sie zu deinstallieren.

Wenn du deine Basis-WIM-Datei ändern, mit der du Windows 10 installierst, und nicht benötigte UWP-Anwendungen vor der Installation aus der WIM-Datei entfernst, werden die Apps nicht von Anfang an installiert und deine Profilerstellungszeiten sollten kürzer sein. Später in diesem Abschnitt findest du Informationen zum Entfernen von UWP-Apps aus deiner Installations-WIM-Datei.

Eine gute Strategie für VDI ist, die gewünschten Apps im Basisimage bereitzustellen und anschließend den Zugriff auf den Microsoft Store einzuschränken oder zu blockieren. Store-Apps werden auf normalen Computern in regelmäßigen Abständen im Hintergrund aktualisiert. Die UWP-Apps können während des Wartungsfensters aktualisiert werden, wenn andere Updates angewendet werden.

#### <a name="delete-the-payload-of-uwp-apps"></a>Löschen der Nutzlast der UWP-Apps

UWP-Apps, die nicht benötigt werden, sind weiterhin im Dateisystem vorhanden und verbrauchen eine kleine Menge an Speicherplatz. Für Apps, die nie benötigt werden, kann die Nutzlast unerwünschter UWP-Apps mit PowerShell-Befehlen aus dem Basisimage entfernt werden.

Wenn du diese über die später in diesem Abschnitt angegebenen Links aus der Installations-WIM-Datei entfernst, solltest du von Anfang an mit einer sehr schlanken Liste von UWP-Apps beginnen können.

Führe den folgenden Befehl aus, um bereitgestellte UWP-Apps von einem laufenden Windows 10-Betriebssystem auszulisten, wie in dieser verkürzten Beispielausgabe von PowerShell:

```powershell

    Get-AppxProvisionedPackage -Online

    DisplayName  : Microsoft.3DBuilder
    Version      : 13.0.10349.0
    Architecture : neutral
    ResourceId   : \~
    PackageName  : Microsoft.3DBuilder_13.0.10349.0_neutral_\~_8wekyb3d8bbwe
    Regions      :
```

UWP-Apps, die einem System zur Verfügung gestellt werden, können während der Betriebssysteminstallation im Rahmen einer Aufgabensequenz oder später nach der Installation des Betriebssystems entfernt werden. Dies könnte die bevorzugte Methode sein, da sie den gesamten Prozess der Erstellung oder Wartung eines Images modular gestaltet. Sobald du die Skripts entwickelst, bearbeite ein bestehendes Skript, wenn sich in einem späteren Build etwas ändert, anstatt den Prozess von Grund auf zu wiederholen. Hier sind einige Links zu Informationen zu diesem Thema:

[Removing Windows 10 in-box apps during a task sequence](/archive/blogs/mniehaus/removing-windows-10-in-box-apps-during-a-task-sequence) (Entfernen von mitgelieferten Windows 10-Apps während einer Aufgabensequenz)

[Removing Built-in apps from Windows 10 WIM-File with PowerShell - Version 1.3](https://gallery.technet.microsoft.com/Removing-Built-in-apps-65dc387b) (Entfernen integrierter Apps aus der Windows 10-WIM-Datei mit PowerShell – Version 1.3)

[Windows 10 1607: Keeping apps from coming back when deploying the feature update](/archive/blogs/mniehaus/windows-10-1607-keeping-apps-from-coming-back-when-deploying-the-feature-update) (Windows 10 1607: Verhindern der Rückkehr von Apps bei der Bereitstellung des Featureupdates)

Führe dann den PowerShell-Befehl [Remove-AppxProvisionedPackage](/powershell/module/dism/remove-appxprovisionedpackage?view=win10-ps) aus, um UWP-App-Nutzlasten zu entfernen:

```powershell
Remove-AppxProvisionedPackage -Online -PackageName
```

Jede UWP-App sollte in jeder spezifischen Umgebung auf ihre Anwendbarkeit geprüft werden. Wenn du eine Standardinstallation von Windows 10, Version 1803 durchführst, notiere dir, welche Apps ausgeführt werden und Speicher verbrauchen. Beispielsweise kannst du in Betracht ziehen, Apps zu entfernen, die automatisch starten, oder Apps, die automatisch Informationen wie z.B. Wetter und Nachrichten im Startmenü anzeigen, die in deiner Umgebung möglicherweise nicht nützlich sind.

Eine der „mitgelieferten“ UWP-Apps namens „Photos“ hat eine Standardeinstellung **Benachrichtigung anzeigen, wenn neue Alben verfügbar sind**.  Die Photos-App kann ca. 145MB Speicherplatz belegen, insbesondere privaten Arbeitssatzspeicher, auch wenn er nicht verwendet wird.  Das Ändern der Einstellung **Benachrichtigung anzeigen, wenn neue Alben verfügbar sind** für alle Benutzer ist zu diesem Zeitpunkt nicht sinnvoll, daher die Empfehlung, die Photos-App zu entfernen, wenn sie nicht benötigt oder gewünscht wird.

### <a name="clean-up-optional-features"></a>Bereinigung optionaler Features

#### <a name="managing-optional-features-with-powershell"></a>Verwalten optionaler Features mit PowerShell

 Liste die aktuell installierten Windows-Features mit diesem PowerShell-Befehl auf:

```powershell
Get-WindowsOptionalFeature -Online
```

Du kannst ein bestimmtes optionales Windows-Feature wie im folgenden Beispiel aktivieren oder deaktivieren:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName "DirectPlay"
```

Weitere Informationen hierzu finden Sie im [Windows PowerShell-Forum](/answers/topics/windows-server-powershell.ht).

#### <a name="enable-or-disable-windows-features-by-using-dism"></a>Aktivieren oder Deaktivieren von Windows-Features mit DISM

Mit dem integrierten **Dism.exe**-Tool kannst du optionale Windows-Features auflisten und steuern. Du kannst ein Dism.exe-Skript einrichten, das während einer Aufgabensequenz ausgeführt wird, die das Betriebssystem installiert.

### <a name="local-policy-settings"></a>Lokale Richtlinieneinstellungen

Zahlreiche Optimierungen für Windows 10 in einer VDI-Umgebung können mit einer Windows-Richtlinie vorgenommen werden. Die hier aufgeführten Einstellungen können lokal auf das Basisimage angewendet werden. Wenn die entsprechenden Einstellungen nicht auf andere Weise wie z.B. durch eine Gruppenrichtlinie angegeben werden, würden die Einstellungen weiterhin gelten.

Einige Entscheidungen können auf Besonderheiten der Umgebung basieren, z.B.:

-   Darf die VDI-Umgebung auf das Internet zugreifen?

-   Ist die VDI-Lösung dauerhaft oder nicht dauerhaft?

Die folgenden Einstellungen stehen nicht mit einer Einstellung in Konflikt, die etwas mit der Sicherheit zu tun hat. Diese Einstellungen wurden ausgewählt, um Einstellungen zu entfernen, die möglicherweise nicht auf VDI-Umgebungen anwendbar sind.

> [!NOTE]
> In dieser Tabelle der Gruppenrichtlinieneinstellungen stammen die mit einem Sternchen gekennzeichneten Elemente aus der [Windows Restricted Traffic Limited Functionality Baseline](https://go.microsoft.com/fwlink/?linkid=828887).

| Richtlinieneinstellung | Element | Untergeordnete Element | Mögliche Einstellung und Kommentare |
|--|--|--|--|
| **Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Windows-Einstellungen \\ Sicherheitseinstellungen** |  |  |  |
| **Netzwerklisten-Manager-Richtlinien** | Alle Netzwerkeeigenschaften | Netzwerkadresse | Benutzer kann Ort nicht ändern. |
| **Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Systemsteuerung** |  |  |  |
| \***Systemsteuerung** | Onlinetipps zulassen |  | Deaktiviert („Einstellungen“ kontaktiert nicht die Inhaltsdienste von Microsoft zum Abrufen von Tipps und hilfreichen Informationen) |
| **\*Systemsteuerung**\\ Personalisierung | Sperrbildschirm nicht anzeigen |  | Aktiviert (Diese Richtlinieneinstellung steuert ob der Sperrbildschirm für Benutzer angezeigt wird. Wenn du diese Richtlinieneinstellung aktivierst, wird Benutzern, die vor der Anmeldung nicht STRG+ALT+ENTF drücken müssen, nach Sperren ihres PCs ihre ausgewählte Kachel angezeigt.) |
| **\*Systemsteuerung**\\ Personalisierung | Ein bestimmtes Standardbild für den Sperr- und Anmeldebildschirm erzwingen | [![Abbildung der Benutzeroberfläche zum Festlegen des Pfads zum Sperrbildschirmbild](media/lock-screen-image-settings.png)](media/lock-screen-image-settings.png) | Aktiviert (Mit dieser Einstellung kannst du den Standardsperrbildschirm und das Anmeldungsbild angeben, das angezeigt wird, wenn kein Benutzer angemeldet ist, und außerdem legt sie das angegebene Bild als Standard für alle Benutzer fest – es ersetzt das Standardbild.) Für ein einfaches Bild mit niedriger Auflösung würden bei jedem Rendern weniger Daten über das Netzwerk übertragen. |
| **\*Systemsteuerung**\\ Regions- und Sprachoptionen\\Handschriftanpassung | Automatisches Lernen deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, wird automatisches Lernen beendet, und alle gespeicherten Daten werden gelöscht. Benutzer können diese Einstellung nicht in der Systemsteuerung konfigurieren) |
| **Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Netzwerk** |  |  |  |
| **BITS (Background Intelligent Transfer Service, Intelligenter Hintergrundübertragungsdienst)** | Verwendung des Windows Branch-Caches durch BITS-Client nicht zulassen |  | Enabled |
| **BITS (Background Intelligent Transfer Service, Intelligenter Hintergrundübertragungsdienst)** | Computer darf nicht als BITS-Peercachingclient fungieren |  | Enabled |
| **BITS (Background Intelligent Transfer Service, Intelligenter Hintergrundübertragungsdienst)** | Computer darf nicht als BITS-Peercachingserver fungieren |  | Enabled |
| **BITS (Background Intelligent Transfer Service, Intelligenter Hintergrundübertragungsdienst)** | BITS-Peercaching zulassen |  | Deaktiviert |
| **BranchCache** | BranchCache aktivieren |  | Deaktiviert |
| \***Schriftarten** | Schriftartenanbieter aktivieren |  | Deaktiviert (Windows stellt keine Verbindung mit einem Onlineschriftanbieter her und listet nur lokal installierte Schriftarten auf.) |
| **Hotspotauthentifizierung** | Hotspotauthentifizierung aktivieren |  | Deaktiviert |
| **Microsoft Peer-zu-Peer-Netzwerkdienste** | Microsoft Peer-zu-Peer-Netzwerkdienste deaktivieren |  | Enabled |
| **Netzwerkverbindungs-Statusanzeige** (Beachte, dass es in diesem Abschnitt weitere Einstellungen gibt, die in isolierten Netzwerken verwendet werden können) | Passive Abrufe angeben | Passive Abrufe deaktivieren (Kontrollkästchen) | Aktiviert (Verwende diese Einstellung in einem isolierten Netzwerk, oder wenn du statische IP-Adressen verwendest.) |
| **Offlinedateien** | Die Funktion „Offlinedateien“ zulassen bzw. nicht zulassen |  | Deaktiviert |
| **\*TCPIP-Einstellungen**\\ IPv6-Übergangstechnologien | Teredo-Status festlegen | Deaktivierter Zustand | Aktiviert (Im deaktivierten Zustand sind auf dem Host keine Teredo-Schnittstellen vorhanden.) |
| **\*WLAN-Dienst**\\ WLAN-Einstellungen | Zulassen, dass Windows automatisch Verbindungen mit vorgeschlagenen öffentlichen Hotspots, mit Netzwerken, die von Kontakten gemeinsam genutzt werden und mit Hotspots herstellt, die kostenpflichtige Dienste anbieten |  | Deaktiviert (**Mit vorgeschlagenen öffentlichen Hotspots verbinden**, **Mit den von meinen Kontakten freigegebenen Netzen verbinden** und **Kostenpflichtige Dienste aktivieren** werden deaktiviert, und Benutzer dieses Geräts können sie nicht aktivieren.) |
| **Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Startmenü und Taskleiste** |  |  |  |
| \***Benachrichtigungen** | Netzwerkverwendung für Benachrichtigungen deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, können Anwendungen und Systemfunktionen keine Benachrichtigungen von WNS über das Netzwerk oder mit Benachrichtigungen abfragenden APIs empfangen.) |
| **Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ System** |  |  |  |
| **Geräteinstallation** | Keinen Windows-Fehlerbericht senden, wenn ein Standardtreiber für ein Gerät installiert ist |  | Enabled |
| **Geräteinstallation** | Bei der Installation eines neuen Gerätetreibers keinen Systemwiederherstellungspunkt erstellen |  | Enabled |
| **Geräteinstallation** | Abrufen von Gerätemetadaten aus dem Internet verhindern |  | Enabled |
| **Geräteinstallation** | Verhindern, dass ein Fehlerbericht gesendet wird, wenn ein Gerätetreiber während der Installation zusätzliche Software anfordert |  | Enabled |
| **Geräteinstallation** | Sprechblasen mit der Meldung **Neue Hardware gefunden** während der Geräteinstallation deaktivieren |  | Enabled |
| **Dateisystem**\\NTFS | Optionen für die Erstellung von Kurznamen | Für alle Volumes deaktiviert | Enabled |
| \***Gruppenrichtlinie** | Konfigurieren der Verknüpfung zwischen Web und App mit App-URI-Handlern |  | Deaktiviert (Deaktiviert die Verknüpfung zwischen Web und App und HTTP(S); URIs werden im Standardbrowser geöffnet, anstatt die zugehörige App zu starten.) |
| \***Gruppenrichtlinie** | Auf der Oberfläche dieses Geräts weiterarbeiten |  | Deaktiviert (Das Windows-Gerät ist für andere Geräte nicht erkennbar und wird nicht in geräteübergreifende Oberflächen einbezogen.) |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Zugriff auf alle Windows Update-Features deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, werden alle Windows Update-Funktionen entfernt. Dazu gehört das Blockieren des Zugriffs auf die Windows Update-Website unter https://windowsupdate.microsoft.com, über den Windows Update-Hyperlink im Startmenü und auch das Menü „Extras“ im Internet Explorer. Die automatische Aktualisierung von Windows ist ebenfalls deaktiviert; du wirst weder benachrichtigt, noch erhältst du wichtige Updates von Windows Update. Diese Richtlinieneinstellung verhindert auch, dass der Geräte-Manager automatisch Treiberupdates von der Windows Update-Website installiert.) |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Automatisches Update von Stammzertifikaten deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, und dir wird ein Zertifikat angezeigt, das nicht von einer vertrauenswürdigen Stammzertifizierungsstelle ausgestellt wurde, nimmt dein Computer keinen Kontakt mit der Windows Update-Website auf, um festzustellen, ob Microsoft die Zertifizierungsstelle seiner Liste vertrauenswürdiger Zertifizierungsstellen hinzugefügt hat.)    **HINWEIS:** Verwende diese Richtlinie nur, wenn du über eine Alternative zur neuesten Zertifikatssperrliste verfügst. |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Events.asp-Links der Ereignisanzeige deaktivieren |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Freigabe von Daten für die Handschriftanpassung deaktivieren |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Handschrifterkennungs-Fehlerberichterstattung deaktivieren |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | „Wussten Sie schon?“-Inhalte im Hilfe- und Supportcenter deaktivieren Inhalt |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Knowledge Base-Suche des Hilfe- und Supportcenters deaktivieren |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Verbindungs-Assistenten deaktivieren, wenn sich die URL-Verbindung auf Microsoft.com bezieht |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Internet-Download für die Assistenten „Webpublishing“ und „Onlinebestellung von Abzügen“ deaktivieren |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Internet-Dateizuordnungsdienst deaktivieren |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Registrierung deaktivieren, wenn sich die URL-Verbindung auf „Microsoft.com“ bezieht |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Aufgabe „Abzüge online bestellen“ für Bilder deaktivieren |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Aufgabe „Im Web veröffentlichen“ für Dateien und Ordner deaktivieren |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Programm zur Verbesserung der Benutzerfreundlichkeit deaktivieren |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Programm zur Verbesserung der Benutzerfreundlichkeit von Windows deaktivieren |  | Enabled |
| **\*Internetkommunikationsverwaltung**\\ Internetkommunikationseinstellungen | Aktive Tests der Windows-Netzwerkverbindungs-Statusanzeige deaktivieren |  | Aktiviert (Diese Richtlinieneinstellung deaktiviert die aktiven Tests, die von der Windows-Netzwerkverbindungs-Statusanzeige (Windows Network Connectivity Status Indicator, NCSI) durchgeführt werden, um festzustellen, ob dein Computer mit dem Internet oder einem eingeschränkteren Netzwerk verbunden ist. Als Teil der Bestimmung der Verbindungsebene führt der NCSI einen von zwei aktiven Tests durch: Herunterladen einer Seite von einem dedizierten Webserver oder Erstellen einer DNS-Anfrage nach einer dedizierten Adresse. Wenn du diese Richtlinieneinstellung aktivierst, wird einer der beiden aktiven Tests nicht vom NCSI ausgeführt. Dies könnte die Fähigkeit des NCSI und anderer Komponenten, die NCSI verwenden, zur Bestimmung des Internetzugriffs einschränken) HINWEIS: Es gibt andere Richtlinien, die dir ermöglichen, NCSI-Tests auf interne Ressourcen umzuleiten, wenn diese Funktionalität gewünscht wird. |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Fehlerberichterstattung deaktivieren |  | Enabled |
| **Internetkommunikationsverwaltung**\\Internetkommunikationseinstellungen | Suche nach Gerätetreibern auf Windows Update deaktivieren |  | Enabled |
| **Anmelden** | Bei der ersten Anmeldung Animation abspielen |  | Deaktiviert |
| **Anmelden** | Anwendungsbenachrichtigungen auf gesperrtem Bildschirm deaktivieren |  | Enabled |
| **Anmelden** | Windows-Startsound deaktivieren |  | Enabled |
| **Energieverwaltung** | Aktiven Energiesparplan auswählen | Hohe Leistung | Enabled |
| **Wiederherstellung** | Systemwiederherstellung in Standardzustand zulassen |  | Deaktiviert |
| \***Speicherintegrität** | Herunterladen von Updates auf das Datenträgerfehlermodell ermöglichen |  | Deaktiviert (Updates würden für das Datenträgerfehlermodell nicht heruntergeladen) |
| \***Windows-Zeitdienste**\\ Zeitanbieter | Windows-NTP-Client aktivieren |  | Deaktiviert (Wenn du diese Richtlinieneinstellung deaktivierst oder nicht konfigurierst, wird die Zeit der Uhr des lokalen Computers nicht mit NTP-Servern synchronisiert) **HINWEIS**: *Überlege dir diese Einstellung sehr gründlich*. Windows-Geräte, die mit einer Domäne verbunden sind, sollten **NT5DS** verwenden. Für die Verbindung eines DC mit dem DC der übergeordneten Domäne könnte NTP verwendet werden. Die PDCe-Rolle könnte NTP verwenden. Virtuelle Computer verwenden manchmal „Erweiterungen“ oder „Integrationsdienste“. |
| **Problembehandlung und Diagnose**\\ Geplante Wartung | Verhalten für geplante Wartung konfigurieren |  | Deaktiviert |
| **Problembehandlung und Diagnose**\\ Windows-Startleistungsdiagnose | Szenarioausführungsebene konfigurieren |  | Deaktiviert |
| **Problembehandlung und Diagnose**\\ Windows-Arbeitsspeicherverlust-Diagnose | Szenarioausführungsebene konfigurieren |  | Deaktiviert |
| **Problembehandlung und Diagnose**\\ Windows-Ressourcenauslastungserkennung und -Konfliktlösung | Szenarioausführungsebene konfigurieren |  | Deaktiviert |
| **Problembehandlung und Diagnose**\\ Windows-Herunterfahr-Leistungsdiagnose | Szenarioausführungsebene konfigurieren |  | Deaktiviert |
| **Problembehandlung und Diagnose**\\ Diagnose für Windows-Standby-/Wiederaufnahmeleistung | Szenarioausführungsebene konfigurieren |  | Deaktiviert |
| **Problembehandlung und Diagnose**\\ Diagnose der Leistung für Windows-Systemreaktionszeit | Szenarioausführungsebene konfigurieren |  | Deaktiviert |
| \***Benutzerprofile** | Werbe-ID deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, wird die Werbe-ID deaktiviert. Apps können die ID nicht für Benutzeroberflächen in verschiedenen Apps verwenden.) |
| **Richtlinie für „Lokaler Computer“ \\ Computerkonfiguration \\ Administrative Vorlagen \\ Windows-Komponenten** |  |  |  |
| **Features zu Windows 10 hinzufügen** | Ausführung des Assistenten verhindern |  | Enabled |
| \***App-Datenschutz** | Windows-App-Zugriff auf Kontoinformationen zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf Kontoinformationen zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf die Anrufliste zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf die Anrufliste zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf Kontakte zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf Kontakte zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf Diagnoseinformationen anderer Apps zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du diese Richtlinieneinstellung deaktivierst oder nicht konfigurierst, können Mitarbeiter in deiner Organisation über „Einstellungen“ \> „Datenschutz“ auf dem Gerät festlegen, ob Windows-Apps Diagnoseinformationen über andere Apps erhalten können.) |
| \***App-Datenschutz** | Windows-App-Zugriff auf E-Mails zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option „Zulassen erzwingen“ wählst, dürfen Windows-Apps auf E-Mails zugreifen, und Mitarbeiter in deinem Unternehmen können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf Standort zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf den Speicherort zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf Nachrichten zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf den Speicherort zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf Bewegungsdaten zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf Bewegungsdaten zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf Benachrichtigungen zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf Benachrichtigungen zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf Aufgaben zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf Aufgaben zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf Kalender zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf den Kalender zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf Kamera zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf die Kamera zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf Mikrofon zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf das Mikrofon zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Windows-App-Zugriff auf vertrauenswürdige Geräte zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf vertrauenswürdige Geräte zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| \***App-Datenschutz** | Kommunizieren von Windows-Apps mit entkoppelten Geräten zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht mit entkoppelten drahtlosen Geräten kommunizieren, und Mitarbeiter in deiner Organisation können dies nicht ändern.) |
| \***App-Datenschutz** | Windows-App-Zugriff auf Radios zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht auf die Steuerung von Radios zugreifen, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| **App-Datenschutz** | Windows-Apps Telefonanrufe gestatten | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Windows-Anwendungen dürfen keine Anrufe tätigen, und Mitarbeiter in deiner Organisation können dies nicht ändern.) |
| \***App-Datenschutz** | Ausführung von Windows-Apps im Hintergrund zulassen | Standard für alle Apps: Verweigern erzwingen | Aktiviert (Wenn du die Option **Verweigern erzwingen** gewählt hast, dürfen Windows-Apps nicht im Hintergrund ausgeführt werden, und Mitarbeiter in deiner Organisation können dies nicht ändern) |
| **Richtlinien für die automatische Wiedergabe** | Standardverhalten von AutoAusführen festlegen | Keine AutoAusführen-Befehle ausführen | Enabled |
| \***Richtlinien für die automatische Wiedergabe** | Automatische Wiedergabe deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, ist die automatische Wiedergabe auf CD-ROM und Wechselmedienlaufwerken oder auf allen Laufwerken deaktiviert.) |
| \***Cloudinhalt** | Windows-Tipps nicht anzeigen |  | Aktiviert (Diese Richtlinieneinstellung verhindert, dass Windows-Tipps für Benutzer angezeigt werden.) |
| \***Cloudinhalt** | Microsoft-Anwenderfeatures deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, werden Benutzer keine personalisierten Empfehlungen von Microsoft und keine Benachrichtigungen über ihr Microsoft-Konto mehr angezeigt.) |
| \***Datensammlung und Vorabversionen** | Telemetrie zulassen | 0 – Sicherheit [nur Enterprise] | Aktiviert (Der Wert 0 kann nur für Geräte festgelegt werden, auf denen die Enterprise-, Education, IoT- oder Windows Server-Editionen ausgeführt werden.) |
| \***Datensammlung und Vorabversionen** | Feedbackbenachrichtigungen nicht mehr anzeigen |  | Enabled |
| \***Datensammlung und Vorabversionen** | Benutzersteuerung für Insider-Builds umstellen |  | Deaktiviert |
| **Übermittlungsoptimierung** | Downloadmodus | Downloadmodus: Einfach (99) | 99 = Einfacher Downloadmodus ohne Peering. Die Übermittlungsoptimierung lädt ausschließlich über HTTP herunter und versucht nicht, die Übermittlungsoptimierungs-Cloud-Dienste zu kontaktieren. |
| **Desktopfenster-Manager** | Aufruf von Flip-3D nicht zulassen |  | Enabled |
| **Desktopfenster-Manager** | Fensteranimationen nicht zulassen |  | Enabled |
| **Desktopfenster-Manager** | Volltonfarbe für Starthintergrund verwenden |  | Enabled |
| **Rand-UI** | Wischen vom Bildschirmrand zulassen |  | Deaktivieren |
| **Rand-UI** | Hilfetipps deaktivieren |  | Enabled |
| \***Datei-Explorer** | Windows Defender SmartScreen konfigurieren |  | Deaktiviert (SmartScreen wird für alle Benutzer deaktiviert. Benutzer werden nicht gewarnt, wenn sie versuchen, verdächtige Apps aus dem Internet auszuführen.) |
|  |  |  | **HINWEIS**: Wenn keine Verbindung mit dem Internet besteht, wird so verhindert, dass die Computer versuchen, Microsoft wegen SmartScreen-Informationen zu kontaktieren. |
| **Datei-Explorer** | Benachrichtigung **Neue Anwendung installiert** nicht anzeigen |  | Enabled |
| \***Mein Gerät suchen** | „Mein Gerät suchen“ aktivieren/deaktivieren |  | Deaktiviert (Wenn „Mein Gerät suchen“ ausgeschaltet ist, werden das Gerät und sein Standort nicht registriert und die Funktion „Mein Gerät suchen“ funktioniert nicht. Der Benutzer kann auf seinem Gerät auch nicht den Ort sehen, an dem sein aktives Digitalisierungsgerät zuletzt genutzt wurde.) |
| **Spiel-Explorer** | Herunterladen von Spielinformationen deaktivieren |  | Enabled |
| **Spiel-Explorer** | Spielupdates deaktivieren |  | Enabled |
| **Spiel-Explorer** | Ablaufverfolgung der letzten Spielzeiten im Ordner „Spiele“ deaktivieren |  | Enabled |
| **Heimnetzgruppe** | Beitritt des Computers zu einer Heimnetzgruppe verhindern |  | Enabled |
| \***Internet Explorer** | Für Microsoft-Dienste das Bereitstellen von erweiterten Vorschlägen zulassen, wenn Benutzer Text in die Adressleiste eingeben |  | Deaktiviert (Benutzern werden keine erweiterten Vorschläge angezeigt, sobald sie Text in die Adressleiste eingeben. Außerdem können Benutzer die Einstellung „Vorschläge“ nicht ändern.) |
| **Internet Explorer** | Periodische Überprüfungen auf Internet Explorer-Softwareupdates deaktivieren |  | Enabled |
| **Internet Explorer** | Anzeigen des Begrüßungsbildschirms deaktivieren |  | Enabled |
| **Internet Explorer** | Automatisch neue Versionen von Internet Explorer installieren |  | Deaktiviert |
| **Internet Explorer** | Teilnahme am Programm zur Verbesserung der Benutzerfreundlichkeit verhindern |  | Enabled |
| **Internet Explorer** | Ausführen des Anpassungs-Assistenten verhindern | Direkt zur Startseite wechseln | Enabled |
| **Internet Explorer** | Zunahme von Registerkartenprozess festlegen | Low (Niedrig) | Enabled |
| **Internet Explorer** | Standardverhalten für eine neue Registerkarte festlegen | Neue Registerkartenseite | Enabled |
| **Internet Explorer** | Benachrichtigungen zur Add-On-Leistung deaktivieren |  | Enabled |
| \***Internet Explorer** | AutoVervollständigen für Webadressen deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, werden dem Benutzer bei der Eingabe von Webadressen keine Übereinstimmungen vorgeschlagen. Der Benutzer kann die automatische Vervollständigung für das Festlegen von Webadressen nicht ändern.) |
| \***Internet Explorer** | Browser-Geolocation deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, ist die Geolocationunterstützung im Browser deaktiviert.) |
| **Internet Explorer** | Erneutes Öffnen der letzten Browsersitzung deaktivieren |  | Enabled |
| \***Internet Explorer** | „Vorgeschlagene Sites“ aktivieren |  | Deaktiviert (Wenn du diese Richtlinieneinstellung deaktivierst, werden die mit dieser Funktion verbundenen Einstiegspunkte und Funktionen deaktiviert.) |
| **\*Internet Explorer**\\ Kompatibilitätsansicht | Kompatibilitätsansicht deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, kann der Benutzer weder die Schaltfläche „Kompatibilitätsansicht“ verwenden noch die Liste der Kompatibilitätsansicht-Websites verwalten.) |
| **Internet Explorer**\\ Internetsystemsteuerung<strong>\\</strong> Seite „Erweitert“ | Animationen in Webseiten wiedergeben |  | Deaktiviert |
| **Internet Explorer**\\ Internetsystemsteuerung\\ Seite „Erweitert“ | Videos in Webseiten wiedergeben |  | Deaktiviert |
| **\*Internet Explorer**\\ Internetsystemsteuerung\\ Seite „Erweitert“ | Vorblättern mit Seitenvorhersage deaktivieren |  | Aktiviert (Microsoft zeichnet deinen Browserverlauf auf, um die Funktionsweise des Vorblätterns mit Seitenvorhersage zu verbessern. Dieses Feature ist für Internet Explorer nicht für den Desktop verfügbar. Wenn du diese Richtlinieneinstellung aktivierst, ist das Vorblättern mit Seitenvorhersage deaktiviert, und die nächste Webseite wird nicht im Hintergrund geladen.) |
| **InternetExplorer**\\ Interneteinstellungen\\ Erweiterte Einstellungen\\ Browsen | Finden von Telefonnummern deaktivieren |  | Enabled |
| **InternetExplorer**\\ Interneteinstellungen\\ Erweiterte Einstellungen\\ Multimedia | Internet Explorer erlauben Mediendateien wiederzugeben, die alternative Codecs verwenden |  | Deaktiviert |
| \***Speicherort und Sensoren** | Speicherort deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, wird die Speicherortfunktion deaktiviert, und alle Programme auf diesem Computer werden daran gehindert, Speicherortinformationen aus der Speicherortfunktion zu verwenden.) |
| **Speicherort und Sensoren** | Sensoren deaktivieren |  | Enabled |
| **Speicherorte und Sensoren /** Windows-Positionssuche | Windows-Positionssuche deaktivieren |  | Enabled |
| \***Karten** | Automatische Downloads und Updates von Kartendaten deaktivieren |  | Aktiviert (Wenn du diese Einstellung aktivierst, wird das automatische Herunterladen und Aktualisieren von Kartendaten deaktiviert.) |
| \***Karten** | Nicht angeforderten Netzwerk-Datenverkehr auf der Einstellungsseite „Offlinekarten“ deaktivieren |  | Aktiviert (Wenn du diese Richtlinieneinstellung aktivierst, werden Funktionen, die Netzwerkdatenverkehr auf der Einstellungsseite „Offlinekarten“ erzeugen, deaktiviert. Hinweis: Dies könnte die gesamte Einstellungsseite deaktivieren.) |
| \***Nachrichten** | Synchronisierung des Nachrichtendiensts mit der Cloud zulassen |  | Deaktiviert (Diese Richtlinieneinstellung ermöglicht die Sicherung und Wiederherstellung von Mobilfunktextnachrichten in den Cloud-Diensten von Microsoft.) |
| \***Microsoft Edge** | Vorschläge in Dropdownliste der Adressleiste zulassen |  | Deaktiviert |
| \***Microsoft Edge** | Konfigurationsupdates für die Bibliothek zulassen |  | Deaktiviert (Deaktiviert die Kompatibilitätslisten in Microsoft Edge.) |
| \***Microsoft Edge** | Microsoft-Kompatibilitätsliste zulassen |  | Deaktiviert (Wenn du diese Einstellung deaktivierst, wird die Microsoft-Kompatibilitätsliste während der Browsernavigation nicht verwendet.) |
| \***Microsoft Edge** | Webinhalte auf der Seite „Neuer Tab“ zulassen |  | Deaktiviert (Weist Edge an, eine neue Registerkarte ohne Inhalt zu öffnen.) |
| \***Microsoft Edge** | AutoAusfüllen konfigurieren |  | Deaktiviert (Deaktiviert automatisches Ausfüllen der Adressleiste.) |
| \***Microsoft Edge** | DNT konfigurieren |  | Aktiviert (Wenn du diese Einstellung aktivierst, werden Do Not Track-Anforderungen (nicht verfolgen) immer an Websites gesendet, die Nachverfolgungsinformationen anfordern.) |
| \***Microsoft Edge** | Kennwort-Manager konfigurieren |  | Deaktiviert (Wenn du diese Einstellung deaktivierst, können Mitarbeiter ihre Kennwörter nicht mithilfe des Kennwort-Managers lokal speichern.) |
| \***Microsoft Edge** | Suchvorschläge in Adressleiste konfigurieren |  | Deaktiviert (Besucher sehen keine Suchvorschläge in der Adressleiste von Microsoft Edge.) |
| \***Microsoft Edge** | Startseiten konfigurieren |  | Aktiviert (Wenn du diese Einstellung aktivierst, kannst du mindestens eine Startseite konfigurieren. Ist diese Einstellung aktiviert, müssen Sie auch URLs zu den Seiten hinzufügen. Trennen Sie dabei mehrere Seiten durch spitze Klammern, und verwenden Sie folgendes Format: \<support.contoso.com\>\<support.microsoft.com\>Windows 10 Version 1703 oder höher: Wenn du keinen Datenverkehr an Microsoft senden möchtest, kannst du den Wert \<about:blank\> unabhängig davon verwenden, ob das Gerät mit einer Domäne verbunden ist oder nicht, wenn es die einzige konfigurierte URL ist. |
| \***Microsoft Edge** | Windows Defender SmartScreen konfigurieren |  | Deaktiviert (Windows Defender SmartScreen ist deaktiviert, und Mitarbeiter können die Einstellung nicht aktivieren.) |
|  |  |  | **HINWEIS**: Berücksichtige diese Einstellung in der Umgebung. Wenn keine Verbindung mit dem Internet besteht, wird so verhindert, dass die Computer versuchen, Microsoft wegen SmartScreen-Informationen zu kontaktieren. |
| \***Microsoft Edge** | Verhindern, dass die Einrichtungs-Webseite in Microsoft Edge geöffnet wird |  | **Aktiviert** (Bei aktivierter Einstellung wird den Benutzern die Einrichtungswebseite nicht angezeigt, wenn sie Microsoft Edge zum ersten Mal öffnen.) |
| **OneDrive** | OneDrive davon abhalten, Netzwerkdatenverkehr zu generieren, bis der Benutzer sich auf OneDrive anmeldet |  | **Aktiviert** (Aktiviere diese Einstellung, um zu verhindern, dass der OneDrive-Synchronisierungsclient (OneDrive.exe) Netzwerkdatenverkehr erzeugt (Suche nach Updates usw.), bis sich der Benutzer bei OneDrive anmeldet oder mit der Synchronisierung von Dateien auf dem lokalen Computer beginnt.) |
| \***OneDrive** | Verwendung von OneDrive für die Dateispeicherung verhindern |  | **Aktiviert** (es sei denn, OneDrive wird lokal oder remote verwendet.) |
| **OneDrive** | Dokumente standardmäßig auf OneDrive speichern |  | **Deaktiviert** (es sei denn, OneDrive wird lokal oder remote verwendet.) |
| **RSS-Feeds** | Automatische Ermittlung von Feeds und Web Slices verhindern |  | **Aktiviert** |
| \***RSS-Feeds** | Hintergrundsynchronisierung für Feeds und Web Slices deaktivieren |  | **Aktiviert** (Wenn du diese Richtlinieneinstellung aktivierst, wird die Möglichkeit, Feeds und Web Slices im Hintergrund zu synchronisieren, deaktiviert.) |
| \***Suche** | Cortana zulassen |  | **Deaktiviert** (Wenn Cortana deaktiviert ist, können Benutzer immer noch auf dem Gerät suchen.) |
| **Suche** | Cortana auf Sperrbildschirm zulassen |  | **Deaktiviert** |
| \***Suche** | Der Suche und Cortana die Nutzung von Positionsdaten erlauben |  | **Deaktiviert** |
| **Suche** | Websuche nicht zulassen |  | **Aktiviert** |
| \***Suche** | Nicht im Web suchen und keine Webergebnisse in der Suche anzeigen |  | **Aktiviert** (Wenn du diese Richtlinieneinstellung aktivierst, werden Abfragen nicht im Web ausgeführt und Webergebnisse nicht angezeigt, wenn ein Benutzer eine Abfrage in der Suche durchführt.) |
| **Suche** | Hinzufügen von UNC-Speicherorten für die Indizierung in der Systemsteuerung verhindern |  | **Aktiviert** |
| **Suche** | Indizierung von Dateien im Offlinedateicache verhindern |  | **Aktiviert** |
| \***Suche** | Festlegen der in der Suche freizugebenden Informationen | Anonyme Informationen | **Aktiviert** (Nutzungsinformationen teilen, aber nicht Suchverlauf, Microsoft-Kontoinformationen oder bestimmten Standort.) |
| \***Softwareschutz-Plattform** | Online-AVC-Überprüfung des KMS-Clients deaktivieren |  | **Aktiviert** (Wenn du diese Einstellung aktivierst, wird verhindert, dass dieser Computer Daten über seinen Aktivierungsstatus an Microsoft sendet.) |
| \***Spracherkennung** | Automatische Aktualisierung von Sprachdaten zulassen |  | **Deaktiviert** (wird nicht in regelmäßigen Abständen auf aktualisierte Sprachmodelle überprüft) |
| \***Speicher** | Automatische Downloads und Installation von Updates deaktivieren |  | **Aktiviert** (Wenn du diese Einstellung aktivierst, werden der automatische Download und die Installation von App-Updates deaktiviert.) |
| \***Speicher** | Automatische Downloads von Updates auf Win8-Geräten deaktivieren |  | **Aktiviert** (Wenn du diese Einstellung aktivierst, wird der automatische Download von App-Updates deaktiviert.) |
| **Speicher** | Deaktivieren des Angebots zum Update auf die aktuelle Version von Windows |  | **Aktiviert** |
| \***Einstellungen synchronisieren** | Nicht synchronisieren | Benutzern das Einschalten der Synchronisierung ermöglichen (nicht ausgewählt) | **Aktiviert** (Wenn du diese Richtlinieneinstellung aktivierst, wird „Einstellungen synchronisieren“ deaktiviert und keine der „Einstellungen synchronisieren“-Gruppen auf diesem Gerät synchronisiert. |
| **Texteingabe** | Freihand- und Eingabeerkennung verbessern |  | **Deaktiviert** |
| **Windows Defender Antivirus**\\ MAPS | Microsoft MAPS beitreten |  | **Deaktiviert** (Wenn du diese Einstellung deaktivierst oder nicht konfigurierst, trittst du Microsoft MAPS nicht bei.) |
| **Windows Defender Antivirus**\\ MAPS | Dateibeispiele senden, wenn eine weitere Analyse erforderlich ist | Nie senden | **Aktiviert** (nur, wenn MAPS-Diagnosedaten nicht gewählt wurden) |
| **Windows Defender Antivirus**\\ Berichterstellung | Erweiterte Benachrichtigungen deaktivieren |  | **Aktiviert** (Wenn du diese Einstellung aktivierst, werden erweiterte Benachrichtigungen von Windows Defender Antivirus nicht auf Clients angezeigt.) |
| **Windows Defender Antivirus**\\ Signaturaktualisierungen | Definieren der Reihenfolge der Quellen für das Herunterladen von Definitionsupdates | FileShares | **Aktiviert** (Wenn du diese Einstellung aktivierst, werden die Quellen für die Definitionsupdates in der angegebenen Reihenfolge kontaktiert. Sobald Definitionsupdates erfolgreich aus einer bestimmten Quelle heruntergeladen wurden, werden die verbleibenden Quellen in der Liste nicht mehr kontaktiert.) |
| **Windows-Fehlerberichterstattung** | Speicherabbild für vom Betriebssystem erstellte Fehlerberichte automatisch senden |  | **Deaktiviert** |
| **Windows-Fehlerberichterstattung** | Deaktivieren der Windows-Fehlerberichterstattung |  | **Aktiviert** |
| **Windows-Spielaufzeichnung und -übertragung** | Aktiviert oder deaktiviert die Windows-Spielaufzeichnung und -übertragung |  | **Deaktiviert** |
| **Windows Installer** | Maximalgröße für den Basisdateicache steuern | 5 | **Aktiviert** |
| **Windows Installer** | Erstellung von Systemwiederherstellungsprüfpunkten deaktivieren |  | **Aktiviert** |
| **Windows Mail** | Communities–Features deaktivieren |  | **Aktiviert** |
| **Windows Media Player** | Dialogfelder für die erste Verwendung nicht anzeigen |  | **Aktiviert** |
| **Windows Media Player** | Medienfreigabe verhindern |  | **Aktiviert** |
| **Windows-Mobilitätscenter** | Windows-Mobilitätscenter deaktivieren |  | **Aktiviert** |
| **Windows-Zuverlässigkeitsanalyse** | WMI-Anbieter für Zuverlässigkeit konfigurieren |  | **Deaktiviert** |
| **Windows Update** | Automatische Updates sofort installieren |  | **Aktiviert** |
| **Windows Update** | Keine Verbindungen mit Windows Update-Internetadressen herstellen |  | **Aktiviert** (Die Aktivierung dieser Richtlinie deaktiviert diese Funktionalität und kann dazu führen, dass die Verbindung mit öffentlichen Diensten wie dem Windows Store nicht mehr funktioniert. **Hinweis:** Diese Richtlinie gilt nur, wenn das Gerät so konfiguriert ist, dass es eine Verbindung mit einem internen Updatedienst über die Richtlinie „Internen Pfad für den Microsoft Updatedienst angeben“ herstellt. |
| **Windows Update** | Zugriff auf alle Windows Update-Funktionen entfernen |  | **Aktiviert** |
| **\*Windows Update**\\ Windows Update for Business | Vorabversionen verwalten | Lege das Verhalten für den Empfang von Vorabversionen fest: | **Aktiviert** (Bei Auswahl von **Vorabversionen deaktivieren** wird verhindert, dass Vorabversionen auf dem Gerät installiert werden. Dies verhindert, dass Benutzer sich über „Einstellungen -\> Update und Sicherheit“ an dem Windows-Insider-Programm beteiligen können.) |
|  |  | Vorabversionen deaktivieren |  |
| **\*Windows Update**\\ Windows Update for Business | Auswählen, wann Vorabversionen und Featureupdates empfangen werden | Halbjährlicher Kanal | **Aktiviert** (Aktiviere diese Richtlinie, um die Ebene der zu empfangenden Vorabversionen oder Featureupdates und den Zeitpunkt anzugeben.) |
|  |  | Aufschiebung: 365 Tage, |  |
|  |  | Start anhalten: jjjj-mm-tt |  |
| **Windows Update**\\ Windows Update for Business | Beim Empfang von Qualitätsupdates auswählen | 1. 30 Tage 2. Qualitätsupdates anhalten ab jjjj-mm-tt | **Aktiviert** |
| **Windows-Einstellungen für benutzerdefinierte Richtlinie für eingeschränkten Datenverkehr** | OneDrive davon abhalten, Netzwerkdatenverkehr zu generieren, bis der Benutzer sich auf OneDrive anmeldet |  | **Aktiviert** (Aktiviere diese Einstellung, um zu verhindern, dass der OneDrive-Synchronisierungsclient (OneDrive.exe) Netzwerkdatenverkehr erzeugt (Suche nach Updates usw.), bis sich der Benutzer bei OneDrive anmeldet oder mit der Synchronisierung von Dateien auf dem lokalen Computer beginnt.) |
| **Windows-Einstellungen für benutzerdefinierte Richtlinie für eingeschränkten Datenverkehr** | Windows Defender-Benachrichtigungen deaktivieren |  | **Aktiviert** (Wenn du diese Richtlinieneinstellung aktivierst, sendet Windows Defender keine Benachrichtigungen mit kritischen Informationen über den Zustand und die Sicherheit deines Geräts.) |
| **Richtlinie für „Lokaler Computer“ \\ Benutzerkonfiguration \\ Administrative Vorlagen** |  |  |  |
| **Systemsteuerung**\\ Regions- und Sprachoptionen | Textvorhersagen bei der Eingabe deaktivieren |  | **Aktiviert** |
| **Desktop** | Freigaben von zuletzt geöffneten Dateien nicht in „Netzwerkumgebung“ hinzufügen |  | **Aktiviert** |
| **Desktop** | Aero Shake-Mausbewegung zum Minimieren von Fenstern deaktivieren |  | **Aktiviert** |
| **Desktop**/Active Directory | Maximale Suchgröße von Active Directory | 2\.500 | **Aktiviert** |
| **Startmenü und Taskleiste** | Anheften der Store-App an die Taskleiste nicht zulassen |  | **Aktiviert** |
| **Startmenü und Taskleiste** | Keine Elemente in Sprunglisten von Remotestandorten anzeigen oder nachverfolgen |  | **Aktiviert** |
| **Startmenü und Taskleiste** | Beim Zuordnen von Shellshortcuts nicht die suchbasierte Methode verwenden |  | **Aktiviert** (Das System führt keine umfassende Laufwerksuche durch. Es wird nur eine Meldung angezeigt, die erklärt, dass die Datei nicht gefunden wurde.) |
| **Startmenü und Taskleiste** | Entfernen der Personenleiste aus der Taskleiste |  | **Aktiviert** (Das Personensymbol wird aus der Taskleiste entfernt, die entsprechende Einstellungsumschaltung wird von der Einstellungsseite der Taskleiste entfernt, und Benutzer können Personen nicht an die Taskleiste anheften.) |
| **Startmenü und Taskleiste** | Sprechblasenbenachrichtigungen für Featureankündigungen deaktivieren |  | **Aktiviert** (Benutzer können die Store-App nicht an die Taskleiste anheften. Wenn die Store-App bereits an die Taskleiste angeheftet ist, wird sie beim nächsten Anmelden aus der Taskleiste entfernt.) |
| **Startmenü und Taskleiste** | Benutzerüberwachung deaktivieren |  | **Aktiviert** |
| **Startmenü und Taskleiste**/Benachrichtigungen | Popupbenachrichtigungen deaktivieren |  | **Aktiviert** |
| **Windows-Komponenten**/Cloud-Inhalt | Features von Windows-Blickpunkt deaktivieren |  | **Aktiviert** |
| **Rand-UI** | Nachverfolgung der App-Nutzung deaktivieren |  | **Aktiviert** |
| **Datei-Explorer** | Zwischenspeicherung von Bildern in Miniaturansicht deaktivieren |  | **Aktiviert** |
| **Datei-Explorer** | Anzeige der letzten Sucheinträge im Datei-Explorer-Suchfeld deaktivieren |  | **Aktiviert** |
| **Datei-Explorer** | Zwischenspeicherung von Miniaturansichten in versteckten thumbs.db-Dateien deaktivieren |  | **Aktiviert** ||

### <a name="notes-about-network-connectivity-status-indicator"></a>Hinweise zur Netzwerkverbindungs-Statusanzeige

Die obigen Einstellungen für Gruppenrichtlinien beinhalten Einstellungen, um die Überprüfung zu deaktivieren, um festzustellen, ob das System mit dem Internet verbunden ist. Wenn deine Umgebung keine Verbindung mit dem Internet herstellt – oder sie indirekt herstellt – kannst du eine Gruppenrichtlinieneinstellung festlegen, um das Netzwerksymbol aus der Taskleiste zu entfernen. Du könntest das Netzwerksymbol aus folgendem Grund aus der Taskleiste entfernen: Wenn du die Prüfungen der Internetverbindung deaktivierst, wird ein gelbes Flag auf dem Netzwerksymbol angezeigt, obwohl das Netzwerk möglicherweise normal funktioniert. Wenn du das Netzwerksymbol als Gruppenrichtlinieneinstellung entfernen möchtest, ist dies hier möglich:

| Windows Update oder Windows Update for Business | Beim Empfang von Qualitätsupdates auswählen | 1. 30 Tage 2. Qualitätsupdates anhalten ab jjjj-mm-tt | Enabled |
|--|--|--|--|
| **Richtlinie für „Lokaler Computer“ \\ Benutzerkonfiguration \\ Administrative Vorlagen** |  |  |  |
| **Startmenü und Taskleiste** | Netzwerksymbol entfernen |  | **Aktiviert** (Das Netzwerksymbol wird nicht im Systembenachrichtigungsbereich angezeigt.) |

Weitere Informationen zur Netzwerkverbindungs-Statusanzeige (Network Connection Status Indicator, NCSI) findest du unter: [The Network Connection Status icon](https://techcommunity.microsoft.com/t5/networking-blog/bg-p/NetworkingBlog) (Das Symbol für den Netzwerkverbindungsstatus)

### <a name="system-services"></a>Systemdienste

Wenn du erwägst, Systemdienste zu deaktivieren, um Ressourcen zu schonen, achte sehr darauf, dass der betreffende Dienst nicht in irgendeiner Weise Bestandteil eines anderen Diensts ist.

Die meisten dieser Empfehlungen spiegeln auch die Empfehlungen für Windows Server 2016 mit Desktopdarstellung wider; weitere Informationen findest du unter [Anleitungen zur Deaktivierung von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung](../../security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server.md).

Beachte, dass viele Dienste, die als gute Kandidaten zum Deaktivieren erscheinen könnten, auf den Starttyp „Manueller Dienst“ eingestellt sind. Dies bedeutet, dass der Dienst nicht automatisch gestartet wird, sondern erst, wenn eine bestimmte Anwendung oder ein bestimmter Dienst eine Anforderung an den zu deaktivierenden Dienst auslöst. Dienste, die bereits auf den manuellen Starttyp eingestellt sind, werden hier in der Regel nicht aufgeführt.

| Windows-Dienst | Element | Anmerkungen |
|--|--|--|
| CDPUserService | Dieser Benutzerdienst wird für Szenarien mit der Plattform für verbundene Geräte verwendet. | HINWEIS: Dies ist ein benutzerbezogener Dienst, und daher muss der *Vorlagendienst* deaktiviert sein. |
| Benutzererfahrung und Telemetrie im verbundenen Modus | Ermöglicht Funktionen, die Benutzerfreundlichkeit in Anwendungen und im verbundenen Modus unterstützen. Außerdem verwaltet dieser Dienst die ereignisgesteuerte Sammlung und Übertragung von Diagnose- und Nutzungsdaten (die zur Verbesserung der Benutzerfreundlichkeit und Qualität der Windows-Plattform eingesetzt werden). Dazu müssen die Diagnose- und Nutzungseinstellungen in der Datenschutzoption unter „Feedback und Diagnose“ aktiviert sein. | Im nicht verbundenen Netzwerk Deaktivieren erwägen |
| Kontaktdaten | Indiziert Kontaktdaten für die schnelle Kontaktsuche. Wenn du diesen Dienst beendest oder deaktivierst, können Kontakte in den Suchergebnissen fehlen. | (PimIndexMaintenanceSvc) HINWEIS: Dies ist ein benutzerbezogener Dienst, und daher muss der *Vorlagendienst* deaktiviert sein. |
| Diagnoserichtliniendienst | Ermöglicht die Problemerkennung und -lösung für Windows-Komponenten. Wenn dieser Dienst beendet wird, funktioniert die Diagnose nicht mehr. |  |
| Manager für heruntergeladene Karten | Windows-Dienst für den Anwendungszugriff auf heruntergeladene Karten. Dieser Dienst wird bedarfsgesteuert je nach der Anwendung gestartet, die auf heruntergeladene Karten zugreift. Wenn der Dienst deaktiviert wird, können Apps nicht auf Karten zugreifen. |  |
| Geolocation-Dienst | Überwacht die aktuelle Position des Systems und verwaltet die Geofences |  |
| GameDVR und Übertragungsbenutzerdienst | Dieser Benutzerdienst wird für Spielaufzeichnungen und Liveübertragungen verwendet. | HINWEIS: Dies ist ein benutzerbezogener Dienst, und daher muss der Vorlagendienst deaktiviert sein. |
| MessagingService | Dienst, der SMS und verwandte Funktionen unterstützt. | HINWEIS: Dies ist ein benutzerbezogener Dienst, und daher muss der *Vorlagendienst* deaktiviert sein. |
| Laufwerke optimieren | Unterstützt den Computer bei einer effizienteren Ausführung durch das Optimieren von Dateien auf Speicherlaufwerken. | VDI-Lösungen profitieren normalerweise nicht von der Datenträgeroptimierung. Diese „Laufwerke“ sind keine herkömmlichen Laufwerke und oft nur eine temporäre Speicherbelegung. |
| Superfetch | Verwaltet und verbessert die Systemleistung im Zeitablauf. | Verbessert im Allgemeinen nicht die VDI-Leistung, insbesondere nicht dauerhaft, da der Betriebssystemzustand bei jedem Neustart verworfen wird. |
| Dienst für Bildschirmtastatur und Schreibbereich | Aktiviert die Stift- und Freihandfunktionalität der Bildschirmtastatur und des Schreibbereichs. |  |
| Windows-Fehlerberichterstattung | Ermöglicht die Berichterstattung von Fehlern bei nicht mehr funktionierenden und reagierenden Programmen und das Angeben von Lösungen. Ermöglicht außerdem das Generieren von Protokollen für Diagnose- und Reparaturdienste. Wenn dieser Dienst beendet wird, funktioniert die Fehlerberichterstattung möglicherweise nicht ordnungsgemäß, und die Ergebnisse von Diagnosediensten und Reparaturen werden möglicherweise nicht angezeigt. | Mit VDI wird die Diagnose oft in einem Offlineszenario und nicht in der Hauptproduktion durchgeführt. Außerdem deaktivieren einige Kunden WER ohnehin. WER benötigt eine winzige Menge an Ressourcen für viele verschiedene Angelegenheiten inklusive Fehler bei der Installation eines Geräts oder bei der Installation eines Updates. |
| Windows Media Player-Netzwerkfreigabedienst | Gibt Windows Media Player-Bibliotheken für andere vernetzte Spieler und Mediengeräte mit universellem Plug & Play frei | Nicht erforderlich, solange Kunden nicht WMP-Bibliotheken im Netzwerk gemeinsam nutzen. |
| Windows-Dienst für mobile Hotspots | Ermöglicht die Freigabe einer Datenverbindung für ein anderes Gerät. |  |
| Windows Search | Stellt Inhaltsindizierung, Eigenschaftenzwischenspeicherung und Suchergebnisse für Dateien, E-Mails und andere Inhalte bereit. | Wahrscheinlich nicht erforderlich, besonders bei nicht dauerhafter VDI |

#### <a name="per-user-services-in-windows"></a>Benutzerbezogene Dienste in Windows

[Benutzerbezogene Dienste](/windows/application-management/per-user-services-in-windows) werden erstellt, wenn ein Benutzer sich bei Windows oder Windows Server anmeldet, und werden beendet und gelöscht, wenn dieser Benutzer sich abmeldet. Diese Dienste werden im Sicherheitskontext des Benutzerkontos ausgeführt – dies bietet eine bessere Ressourcenverwaltung als der bisherige Ansatz, diese Art von Diensten im Explorer auszuführen, verknüpft mit einem vorkonfigurierten Konto oder als Aufgaben.

### <a name="scheduled-tasks"></a>Geplante Aufgaben

Stelle wie bei anderen Elementen in Windows sicher, dass ein Element nicht benötigt wird, bevor du es deaktivierst.

Die folgende Liste enthält Aufgaben, die Optimierungen oder Datensammlungen auf Computern durchführen, die ihren Zustand Neustarts übergreifend beibehalten. Wenn eine VDI-VM-Aufgabe neu startet und alle Änderungen seit dem letzten Start verwirft, sind Optimierungen für physische Computer nicht hilfreich.

Du kannst alle aktuellen geplanten Aufgaben, einschließlich Beschreibungen, mit dem folgenden PowerShell-Code abrufen:

`Get-ScheduledTask | Select-Object -Property TaskPath,TaskName,State,Description |Export-CSV -Path C:\Temp\W10_1803_SchTasks.csv -NoTypeInformation`

Gültige Werte für **Name der geplanten Aufgabe**  sind:

- OneDrive Standalone Update Task v2
- Microsoft Compatibility Appraiser
- ProgramDataUpdater
- StartupAppTask
- CleanupTemporaryState
- Proxy
- UninstallDeviceTask
- ProactiveScan
- Consolidator
- UsbCeip
- Datenintegritätsüberprüfung
- Datenintegritätsüberprüfung für die Wiederherstellung nach Systemabsturz
- ScheduledDefrag
- SilentCleanup
- Microsoft-Windows-DiskDiagnosticDataCollector
- Diagnose
- StorageSense
- DmClient
- DmClientOnScenarioDownload
- Dateiversionsverlauf (Wartungsmodus)
- ScanForUpdates
- ScanForUpdatesAsUser
- SmartRetry
- Benachrichtigungen
- WindowsActionDialog
- WinSAT Mobilfunk
- MapsToastTask
- ProcessMemoryDiagnosticEvents
- RunFullMemoryDiagnostic
- MNO-Metadatenparser
- LPRemove
- GatherNetworkInfo
- WiFiTask
- Sqm-Tasks
- AnalyzeSystem
- MobilityManager
- VerifyWinRE
- RegIdleBackup
- FamilySafetyMonitor
- FamilySafetyRefreshTask
- IndexerAutomaticMaintenance
- SpaceAgentTask
- SpaceManagerTask
- HeadsetButtonPress
- SpeechModelDownloadTask
- ResPriStaticDbSync
- WsSwapAssessmentTask
- SR
- SynchronizeTimeZone
- USB-Benachrichtigungen
- QueueReporting
- UpdateLibrary
- Geplanter Start
- sih
- XblGameSaveTask

### <a name="apply-windows-and-other-updates"></a>Anwenden von Windows- und anderen -Updates

Ob von Microsoft Update oder deinen internen Ressourcen, wende verfügbare Updates einschließlich Windows Defender-Signaturen an. Dies ist ein guter Zeitpunkt, andere verfügbare Updates einschließlich der für Microsoft Office (sofern installiert) anzuwenden.

### <a name="automatic-windows-traces"></a>Automatische Windows-Ablaufverfolgungen

Windows wird standardmäßig zum Sammeln und Speichern eingeschränkter Diagnosedaten konfiguriert. Dies soll eine Diagnose ermöglichen oder Daten aufzeichnen, falls eine weitere Fehlersuche erforderlich ist. Um automatische Systemablaufverfolgungen zu finden, startest du die Computerverwaltung-App, erweiterst **Systemprogramme**, **Leistung**, **Datensammlersätze** und wählst dann **Ereignisablaufverfolgungssitzungen** aus.

Einige der unter **Ereignisablaufverfolgungssitzungen** und **Startereignis-Ereignisablaufverfolgungssitzungen** angezeigten Ablaufverfolgungen können und sollten nicht gestoppt werden. Andere, z.B. die **WiFiSession**-Ablaufverfolgung, können beendet werden. Zum Beenden einer unter **Ereignisablaufverfolgungssitzungen** ausgeführten Ablaufverfolgung klicke mit der rechten Maustaste, und wähle dann **Beenden** aus. Um zu verhindern, dass die Ablaufverfolgungen automatisch beim Start gestartet werden, gehe folgendermaßen vor:

1.  Wähle den Ordner **Startereignis-Ereignisablaufverfolgungssitzungen** aus.

2.  Suche die gewünschte Ablaufverfolgung, und doppelklicke darauf.

3.  Wähle die Registerkarte **Ablaufverfolgungssitzung** aus.

4.  Deaktiviere das Kontrollkästchen **Aktiviert**.

5.  Wählen Sie **OK** aus.

Hier sind einige Systemablaufverfolgungen, deren Deaktivierung bei der Verwendung von VDI infrage kommt:

| Name | Anmerkungen |
|--|--|
| AppModel | Eine Sammlung von Ablaufverfolgungen, zu denen „phone“ gehört |
| CloudExperienceHostOOBE |  |
| DiagLog |  |
| NtfsLog |  |
| TileStore |  |
| UBPM |  |
| WiFiDriverIHVSession | Wenn kein WLAN-Gerät verwendet wird |
| WiFiSession |  |

#### <a name="servicing-the-operating-system-and-apps"></a>Wartung von Betriebssystem und Apps

Irgendwann während des Bildoptimierungsprozesses sollten verfügbare Windows-Updates angewendet werden. Du kannst Windows Update so einstellen, dass Updates für andere Microsoft-Produkte und Windows installiert werden. Um dies einzustellen, öffne **Windows-Einstellungen**, und wähle dann **Update und Sicherheit** und **Erweiterte Optionen** aus. Wähle **Updates für andere Microsoft-Produkte bereitstellen, wenn ein Windows-Update ausgeführt wird** aus und setze die Option auf **Ein**.

Dies wäre eine gute Einstellung, falls du Microsoft-Anwendungen wie Microsoft Office im Basisimage installieren möchtest. Auf diese Weise ist Office auf dem neuesten Stand, wenn das Image in Betrieb genommen wird. Auch .NET-Updates und Updates für bestimmte Nicht-Microsoft-Komponenten wie Adobe sind über Windows Update verfügbar.

Ein sehr wichtiger Aspekt für nicht dauerhafte VDI-VMs sind Sicherheitsupdates, einschließlich Definitionsdateien für Sicherheitssoftware. Diese Updates werden möglicherweise mindestens einmal pro Tag veröffentlicht. Möglicherweise können diese Updates einschließlich Windows Defender und Nicht-Microsoft-Komponenten beibehalten werden.

Für Windows Defender kann es am besten sein, die Updates auch in einer nicht dauerhaften VDI zuzulassen. Die Updates werden in fast jeder Anmeldesitzung angewendet, aber sie sind klein und sollten kein Problem sein. Außerdem gelangen die VMs bei Updates nicht in Rückstand, da nur die neuesten verfügbaren Versionen verwendet werden. Dasselbe gilt möglicherweise für Nicht-Microsoft-Definitionsdateien.

> [!NOTE]
> Store-Apps (UWP-Apps) werden über den Windows Store aktualisiert. Moderne Versionen von Office wie Microsoft 365 werden über ihre eigenen Mechanismen aktualisiert, wenn sie direkt mit dem Internet verbunden sind, oder andernfalls über Management-Technologien.

### <a name="windows-defender-optimization-with-vdi"></a>Windows Defender-Optimierung mit VDI

Microsoft hat vor kurzem Dokumentation zu Windows Defender in einer VDI-Umgebung veröffentlicht. Weitere Informationen findest du im [Bereitstellungshandbuch für Windows Defender Antivirus in einer VDI-Umgebung (Virtual Desktop Infrastructure)](/windows/security/threat-protection/windows-defender-antivirus/deployment-vdi-windows-defender-antivirus).

Der oben genannte Artikel enthält Verfahren zur Wartung des VDI-Goldimages und der VDI-Clients während ihrer Ausführung. Um die Netzwerkbandbreite zu reduzieren, wenn VDI-Computer ihre Windows Defender-Signaturen aktualisieren müssen, staffele Neustarts, und plane sie wenn möglich außerhalb der Geschäftszeiten. Die Signatur-Updates von Windows Defender können intern auf Dateifreigaben enthalten sein, und wenn möglich, sollten sich diese Dateifreigaben in denselben Netzwerksegmenten wie die virtuellen VDI-Computer oder in deren Nähe befinden.

Weitere Informationen zur Optimierung von Windows Defender mit VDI findest du in dem am Anfang dieses Abschnitts aufgeführten Dokument.

### <a name="tuning-windows-10-network-performance-by-using-registry-settings"></a>Optimieren der Netzwerkleistung von Windows 10 mit Registrierungseinstellungen

Dies ist besonders wichtig in Umgebungen, in denen die VDI oder der physische Computer eine Workload hat, die hauptsächlich netzwerkbasiert ist. Die Einstellungen in diesem Abschnitt verzerren die Leistung zugunsten des Netzwerks, indem sie zusätzliche Pufferung und Zwischenspeicherung von Verzeichniseinträgen usw. festlegen.

Beachte, dass einige Einstellungen in diesem Abschnitt *nur registrierungsbasiert* sind und in das Basisimage integriert werden sollten, bevor das Image für die Produktion bereitgestellt wird.

Die folgenden Einstellungen sind in den [Richtlinien zur Optimierung der Leistung für Windows Server 2016](/windows-server/administration/performance-tuning/) dokumentiert, die von der Windows-Produktgruppe auf Microsoft.com veröffentlicht wurden.

#### <a name="disablebandwidththrottling"></a>DisableBandwidthThrottling

HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\DisableBandwidthThrottling

Gilt für Windows 10. Der Standardwert ist **0**. Standardmäßig drosselt der SMB-Redirector den Durchsatz für Netzwerkverbindungen mit hoher Latenz. In einigen Fällen besteht das Ziel hierbei darin, netzwerkbezogene Timeouts zu verhindern. Durch das Festlegen dieses Registrierungswerts auf **1** wird diese Art der Drosselung deaktiviert. Da so für Netzwerkverbindungen mit hoher Latenz ein höherer Durchsatz für Dateiübertragungen ermöglicht wird, solltest du diese Einstellung in Erwägung ziehen.

#### <a name="fileinfocacheentriesmax"></a>FileInfoCacheEntriesMax

HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\FileInfoCacheEntriesMax

Gilt für Windows 10. Der Standardwert ist **64**, und der gültige Bereich reicht von 1 bis 65.536. Dieser Wert wird verwendet, um die Menge an Dateimetadaten zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf viele Dateien zugegriffen wird. Erwäge, diesen Wert auf **1.024** zu erhöhen.

#### <a name="directorycacheentriesmax"></a>DirectoryCacheEntriesMax

HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\DirectoryCacheEntriesMax

Gilt für Windows 10. Der Standardwert ist **16**, und der gültige Bereich reicht von 1 bis 4.096. Dieser Wert wird verwendet, um die Menge von Verzeichnisinformationen zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf große Verzeichnisse zugegriffen wird. Erwäge, diesen Wert auf **1.024** zu erhöhen.

#### <a name="filenotfoundcacheentriesmax"></a>FileNotFoundCacheEntriesMax

HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\FileNotFoundCacheEntriesMax

Gilt für Windows 10. Der Standardwert ist **128**, und der gültige Bereich reicht von 1 bis 65.536. Dieser Wert wird verwendet, um die Menge von Dateinameninformationen zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf viele Dateinamen zugegriffen wird. Erwäge, diesen Wert auf **2.048** zu erhöhen.

#### <a name="dormantfilelimit"></a>DormantFileLimit

HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\DormantFileLimit

Gilt für Windows 10. Der Standardwert beträgt **1.023**. Mit diesem Parameter wird die maximale Anzahl von Dateien angegeben, die auf einer freigegebenen Ressource geöffnet bleiben soll, nachdem die Datei von der Anwendung geschlossen wurde. Wenn viele tausend Clients Verbindungen mit SMB-Servern herstellen, solltest du diesen Wert auf **256** reduzieren.

Du kannst viele dieser SMB-Einstellungen mit den Windows PowerShell-Cmdlets [Set-SmbClientConfiguration](/powershell/module/smbshare/set-smbclientconfiguration) und [Set-SmbServerConfiguration](/powershell/module/smbshare/set-smbserverconfiguration) konfigurieren. Du kannst Einstellungen nur für die Registrierung konfigurieren, indem du auch Windows PowerShell verwendest, wie im folgenden Beispiel:

`Set-ItemProperty -Path "HKLM:\\SYSTEM\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters" RequireSecuritySignature -Value 0 -Force`

### <a name="additional-settings-from-the-windows-restricted-traffic-limited-functionality-baseline-guidance"></a>Zusätzliche Einstellungen aus dem Leitfaden „Windows Restricted Traffic Limited Functionality Baseline“.

Microsoft hat für Umgebungen, die entweder nicht direkt mit dem Internet verbunden sind, oder die Menge an Daten, die an Microsoft und andere Dienste gesendet werden, reduzieren möchten, eine Baseline veröffentlicht, die mit den gleichen Verfahren wie die [Windows-Sicherheitsgrundsätze](/windows/device-security/windows-security-baselines) erstellt wurde.

Die [Windows Restricted Traffic Limited Functionality Baseline](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services)-Einstellungen sind in der Gruppenrichtlinien-Tabelle mit einem Sternchen gekennzeichnet.

### <a name="disk-cleanup-including-using-the-disk-cleanup-wizard"></a>Datenträgerbereinigung (einschließlich des Datenträgerbereinigungs-Assistenten)

Die Datenträgerbereinigung kann besonders bei Master-Image-VDI-Implementierungen hilfreich sein. Nachdem das Master-Image vorbereitet, aktualisiert und konfiguriert wurde, ist eine der letzten durchgeführten Aufgaben die Datenträgerbereinigung. Der in Windows integrierte Datenträgerbereinigungs-Assistent kann dir helfen, die meisten potenziellen Bereiche der Festplattenspeichereinsparung zu bereinigen.

> [!NOTE]
> Der Datenträgerbereinigungs-Assistent wird nicht weiterentwickelt. Windows wird mit anderen Methoden Funktionen zur Datenträgerbereinigung bereitstellen.



Hier erhältst du Vorschläge für verschiedene Datenträgerbereinigungsaufgaben. Du solltest sie jeweils vor der Implementierung testen:

1. Führe nach dem Anwenden aller Updates den Datenträgerbereinigungs-Assistenten (mit erhöhten Rechten) aus. Beziehe die Kategorien **Übermittlungsoptimierung** und **Windows Update-Bereinigung** mit ein. Du kannst diesen Prozess mit **Cleanmgr.exe** mit der Option **/SAGESET:11** automatisieren. Diese Option legt Registrierungswerte fest, die später zur Automatisierung der Datenträgerbereinigung verwendet werden können, wobei alle verfügbaren Optionen im Datenträgerbereinigungs-Assistenten verwendet werden.

   1.  Die Ausführung von **Cleanmgr.exe /SAGESET:11** auf einer Test-VM von einer sauberen Installation aus zeigt, dass standardmäßig nur zwei automatische Optionen für die Datenträgerbereinigung aktiviert sind:

   - Heruntergeladene Programmdateien

   - Temporäre Internetdateien

   2. Wenn du weitere Optionen oder alle Optionen festlegst, werden diese Optionen entsprechend dem im vorherigen Befehl (**Cleanmgr.exe /SAGESET:11**) angegebenen Indexwert in der Registrierung gespeichert. In diesem Beispiel verwenden wir den Wert *11* als unseren Index für ein nachfolgend automatisiertes Datenträgerbereinigungsverfahren.

   3. Nach der Ausführung von **Cleanmgr.exe /SAGESET:11** siehst du verschiedene Kategorien von Optionen zur Datenträgerbereinigung. Du kannst jede Option auswählen, und wähle dann **OK**. Beachte, dass der Datenträgerbereinigungs-Assistent nun nicht mehr angezeigt wird. Deine ausgewählten Einstellungen werden allerdings in der Registrierung gespeichert und können durch Ausführung von **Cleanmgr.exe /SAGERUN:11** aufgerufen werden.

2. Bereinige den Volumeschattenkopie-Speicher, sofern er verwendet wird. Führe hierzu an einer Eingabeaufforderung mit erhöhten Rechten diese Befehle aus:

   - **vssadmin list shadows**

   - **vssadmin list shadowstorage**

       Wenn die Ausgabe dieser Befehle *Es wurden keine Ergebnisse für die Abfrage gefunden* lautet, wird kein VSS-Speicher verwendet.

3. Bereinige temporäre Dateien und Protokolle. Führe an einer Eingabeaufforderung mit erhöhten Rechten diese Befehle aus:

   - **Del C:\\\*.tmp /s**

   - **Del C:\\Windows\\Temp\\.**

   - **Del %temp%\\.**

4. Lösche nicht verwendete Profile auf dem System mit folgendem Befehl:

   **wmic path win32_UserProfile where LocalPath="c:\\\\users\\\\\<user\>" Delete**

### <a name="remove-onedrive"></a>Entfernen von OneDrive

Das Entfernen von OneDrive umfasst das Entfernen des Pakets und das Deinstallieren und Entfernen der \*.lnk-Dateien. Du kannst den folgenden PowerShell-Beispielcode zum Entfernen von OneDrive aus dem Image nutzen:

```azurecli

Taskkill.exe /F /IM "OneDrive.exe"
Taskkill.exe /F /IM "Explorer.exe"`
    if (Test-Path "C:\\Windows\\System32\\OneDriveSetup.exe")`
     { Start-Process "C:\\Windows\\System32\\OneDriveSetup.exe"`
         -ArgumentList "/uninstall"`
         -Wait }
    if (Test-Path "C:\\Windows\\SysWOW64\\OneDriveSetup.exe")`
     { Start-Process "C:\\Windows\\SysWOW64\\OneDriveSetup.exe"`
         -ArgumentList "/uninstall"`
         -Wait }
Remove-Item -Path
"C:\\Windows\\ServiceProfiles\\LocalService\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\OneDrive.lnk" -Force
Remove-Item -Path "C:\\Windows\\ServiceProfiles\\NetworkService\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\OneDrive.lnk" -Force \# Remove the automatic start item for OneDrive from the default user profile registry hive
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Load HKLM\\Temp C:\\Users\\Default\\NTUSER.DAT" -Wait
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Delete HKLM\\Temp\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run /v OneDriveSetup /f" -Wait
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Unload HKLM\\Temp" -Wait Start-Process -FilePath C:\\Windows\\Explorer.exe -Wait
```

Für Fragen oder Bedenken bezüglich der in diesem Dokument enthaltenen Informationen wende dich bitte an dein Microsoft-Kontoteam, recherchiere den Microsoft VDI-Blog, poste eine Nachricht in den Microsoft-Foren oder wende dich bei Fragen oder Bedenken an Microsoft.