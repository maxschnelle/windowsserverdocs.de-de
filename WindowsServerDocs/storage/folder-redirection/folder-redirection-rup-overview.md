---
title: Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile – Übersicht
description: Übersicht über Technologien für Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8a2a76c0cdd4433ecdf445bcde01f8af5bae66a7
ms.sourcegitcommit: 457e88e5aa6be13a2bffdb8e434a8efc3698678f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548875"
---
# <a name="folder-redirection-offline-files-and-roaming-user-profiles-overview"></a>Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile – Übersicht

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2

In diesem Thema werden die Technologien für Ordnerumleitung, Offlinedateien (clientseitige Zwischenspeicherung) und Roamingbenutzerprofile (auch als RUP bezeichnet) erläutert, einschließlich der neuen Funktionen sowie Ressourcen zum Suchen nach zusätzlichen Informationen.

## <a name="technology-description"></a>Technologiebeschreibung

Die Ordnerumleitung und Offlinedateien werden gemeinsam verwendet, um den Pfad lokaler Ordner (z. B. des Ordners "Dokumente") an eine Netzwerkadresse umzuleiten. Die Inhalte werden dagegen lokal zwischengespeichert, um eine höhere Geschwindigkeit und Verfügbarkeit sicherzustellen. Mit Roamingbenutzerprofilen wird ein Benutzerprofil an eine Netzwerkadresse umgeleitet. Diese Features werden meist als IntelliMirror bezeichnet.

- **Ordnerumleitung** ermöglicht es Benutzern und Administratoren, den Pfad eines bekannten Ordners manuell oder mithilfe der Gruppenrichtlinie an einen neuen Ort umzuleiten. Der neue Ort kann ein Ordner auf dem lokalen Computer oder ein Verzeichnis in einer Dateifreigabe sein. Benutzer interagieren mit den Dateien im umgeleiteten Ordner, als würde er noch auf dem lokalen Laufwerk vorhanden sein. Sie können beispielsweise den Ordner %%amp;quot;Dokumente%%amp;quot;, der normalerweise auf einem lokalen Laufwerk gespeichert wird, an eine Netzwerkadresse umleiten. Die Dateien im Ordner stehen dem Benutzer dann auf jedem Computer im Netzwerk zur Verfügung.
- **Offlinedateien** stellen einem Benutzer Netzwerkdateien zur Verfügung, auch wenn die Netzwerkverbindung mit dem Server nicht verfügbar oder langsam ist. Wenn Sie online arbeiten, entspricht die Zugriffsleistung der Geschwindigkeit des Netzwerks und des Servers. Wenn Sie offline arbeiten, werden die Dateien mit der lokalen Zugriffsgeschwindigkeit aus dem Ordner %%amp;quot;Offlinedateien%%amp;quot; abgerufen. Ein Computer wechselt in folgenden Situationen in den Offlinemodus:
  - Der Modus **Immer offline** wurde aktiviert.
  - Der Server ist nicht verfügbar.
  - Die Netzwerkverbindung ist langsamer als ein konfigurierbarer Schwellenwert.
  - Der Benutzer wechselt mithilfe der Schaltfläche **Offlinebetrieb** im Windows-Explorer manuell in den Offlinemodus.
- **Roamingbenutzerprofile** leiten Benutzerprofile an eine Dateifreigabe um, damit Benutzer auf mehreren Computern dieselben Betriebssystem- und Anwendungseinstellungen verwenden. Wenn sich ein Benutzer an einem Computer mithilfe eines Kontos anmeldet, das mit einer Dateifreigabe als Profilpfad eingerichtet ist, wird das Profil des Benutzers auf den lokalen Computer heruntergeladen und mit dem lokalen Profil (falls vorhanden) zusammengeführt. Wenn sich der Benutzer vom Computer abmeldet, wird die lokale Kopie seines Profils, einschließlich aller Änderungen, mit der Serverkopie des Profils zusammengeführt. In der Regel aktiviert ein Netzwerkadministrator Roamingbenutzerprofile für Domänenkonten.

## <a name="practical-applications"></a>Praktische Anwendung

Administratoren können die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile verwenden, um den Speicher für Benutzerdaten und -einstellungen zu zentralisieren und Benutzern die Möglichkeit zu bieten, im Offlinemodus oder im Falle eines Netzwerk- oder Serverausfalls auf ihre Daten zuzugreifen. Einige spezielle Anwendungsfälle umfassen Folgendes:

- Zentralisieren von Daten auf Clientcomputern für administrative Aufgaben wie das Verwenden eines serverbasierten Sicherungstools zum Sichern von Benutzerordnern und -einstellungen
- Ermöglichen des dauerhaften Zugriffs auf Netzwerkdateien für Benutzer, selbst wenn ein Netzwerk- oder Serverausfall auftritt
- Optimieren der Bandbreitenverwendung und Verbessern der Arbeitsmöglichkeiten von Benutzern in Filialen, die auf Dateien und Ordner zugreifen, die von Unternehmensservern an anderen Standorten gehostet werden
- Ermöglichen des Zugriffs auf Netzwerkdateien für mobile Benutzer, während sie offline oder über langsame Netzwerke arbeiten

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

In der folgenden Tabelle sind einige wichtige Änderungen an der Ordnerumleitung, den Offlinedateien und den Roamingbenutzerprofilen beschrieben, die in dieser Version verfügbar sind.

| Feature/Funktionalität | Neu oder aktualisiert? | Beschreibung |
| --- | --- | --- |
| Immer im Offlinemodus | „Neu“, | Bietet schnelleren Zugriff auf Dateien und geringere Bandbreitenverwendung, selbst wenn eine Hochgeschwindigkeits-Netzwerkverbindung besteht. |
| Sparsame Synchronisation | „Neu“, | Hilft Benutzern dabei, hohe Datennutzungskosten durch Synchronisierung zu vermeiden, indem getaktete Verbindungen mit Nutzungslimits verwendet werden oder in das Netzwerk eines anderen Anbieters gewechselt wird. |
| Unterstützung von Hauptcomputern | „Neu“, | Ermöglicht es, die Verwendung der Ordnerumleitung, Roamingbenutzerprofile oder beiden nur auf den primären Computer eines Benutzers zu beschränken. |

## <a name="always-offline-mode"></a>Immer im Offlinemodus

Ab Windows 8 und Windows Server 2012 können Administratoren die Erfahrung für Benutzer von Offlinedateien immer für den Offlinebetrieb konfigurieren, selbst wenn eine Hochgeschwindigkeits-Netzwerkverbindung besteht. Unter Windows werden Dateien standardmäßig durch stündliche Synchronisierung im Hintergrund im Zwischenspeicher für Offlinedateien aktualisiert.

### <a name="what-value-does-always-offline-mode-add"></a>Welche Vorteile bietet der Modus „Immer offline“?

Der Modus "Immer offline" bietet die folgenden Vorteile:

- Benutzer profitieren von einem schnelleren Zugriff auf Dateien in umgeleiteten Ordnern wie dem Ordner "Dokumente".
- Die Netzwerkbandbreite ist reduziert, wodurch Kosten für teure WAN-Verbindungen oder getaktete Verbindungen wie ein mobiles 4G-Netzwerk gesenkt werden.

### <a name="how-has-always-offline-mode-changed-things"></a>Wie hat der Modus „Immer offline“ die Dinge verändert?

Vor Windows 8 und Windows Server 2012 wechselten Benutzer je nach Netzwerkverfügbarkeit und -bedingungen zwischen dem Online- und Offlinemodus, selbst wenn der Modus für langsame Verbindungen aktiviert und auf einen Wartezeitschwellenwert von 1 Millisekunde festgelegt war.

Mit dem Modus „Immer offline“ wechseln Computer nie in den Onlinemodus, wenn die Gruppenrichtlinieneinstellung **Modus für langsame Verbindungen konfigurieren** konfiguriert und der Schwellenwertparameter **Wartezeit** auf 1 Millisekunde festgelegt ist. Änderungen werden standardmäßig alle 120 Minuten im Hintergrund synchronisiert, aber die Synchronisierung kann mithilfe der Gruppenrichtlinieneinstellung **Configure Background Sync** konfiguriert werden.

Weitere Informationen finden Sie unter [Enable the Always Offline Mode to Provide Faster Access to Files](enable-always-offline.md).

## <a name="cost-aware-synchronization"></a>Sparsame Synchronisation

Bei der sparsamen Synchronisierung wird die Hintergrundsynchronisierung deaktiviert, wenn der Benutzer eine getaktete Netzwerkverbindung (z. B. ein 4G-Mobilfunknetz) verwendet und wenn der Computer in das Netzwerk eines anderen Anbieters wechselt oder das Bandbreitenlimit des Abonnenten fast erreicht oder überschritten ist.

> [!NOTE]
> Getaktete Netzwerkverbindungen weisen in der Regel Roundtrip-Netzwerkwartezeiten auf, die langsamer als der Standardwartezeitwert von 35 Millisekunden für den Wechsel in den Offlinemodus (Modus für langsame Verbindungen) unter Windows 8, Windows Server 2019, Windows Server 2016 und Windows Server 2012 sind. Daher wechseln diese Verbindungen in der Regel automatisch in den Offlinemodus (Modus für langsame Verbindungen).

### <a name="what-value-does-cost-aware-synchronization-add"></a>Welcher Mehrwert entsteht durch kostenbewusste Synchronisierung?

kostenbewusste Synchronisierung hilft Benutzern dabei, unerwartet hohe Datennutzungskosten zu vermeiden, indem getaktete Verbindungen mit Nutzungslimits verwendet werden oder in das Netzwerk eines anderen Anbieters gewechselt wird.

### <a name="how-has-cost-aware-synchronization-changed-things"></a>Wie hat kostenbewusste Synchronisierung die Dinge geändert?

Vor Windows 8 und Windows Server 2012 mussten Benutzer, die die Gebühren für die Verwendung von Offlinedateien bei getakteten Verbindungen minimieren wollten, ihre Datennutzung mithilfe von Tools des Anbieters ihres mobilen Netzwerks nachverfolgen. Benutzer konnten dann manuell den Offlinemodus aktivieren, wenn sie in ein anderes Netzwerk gewechselt sind oder das Bandbreitenlimit fast erreicht oder überschritten hatten.

Durch kostenbewusste Synchronisierung verfolgt Windows den Wechsel und die Limits der Bandbreitenverwendung bei getakteten Verbindungen automatisch nach. Wenn der Benutzer in ein anderes Netzwerk wechselt oder sein Limit erreicht oder überschreitet, wird unter Windows in den Offlinemodus gewechselt und die Synchronisierung verhindert. Benutzer können die Synchronisierung weiterhin manuell initiieren, und Administratoren können die sparsame Synchronisierung für bestimmte Benutzer wie Führungskräfte außer Kraft setzen.

Weitere Informationen finden Sie unter [Enable Background File Synchronization on Metered Networks](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj127408(v%3dws.11)).

## <a name="primary-computers-for-folder-redirection-and-roaming-user-profiles"></a>Hauptcomputer für Ordnerumleitung und Roamingbenutzerprofile

Sie können nun für jeden Domänenbenutzer eine Reihe von Computern festlegen, die als primäre Computer bezeichnet werden, um zu steuern, auf welchen Computern Ordnerumleitung, Roamingbenutzerprofile oder beides verwendet wird. Das Festlegen von Hauptcomputern ist eine einfache und leistungsfähige Methode, um Benutzerdaten und -einstellungen bestimmten Computern oder Geräten zuzuordnen. Dadurch kann sich der Administrator leichter eine Übersicht verschaffen, die Datensicherheit wird verbessert, und die Benutzerprofile werden vor Beschädigung geschützt.

### <a name="what-value-do-primary-computers-add"></a>Welchen Mehrwert bedeuten primäre Computer?

Das Festlegen von Hauptcomputern für Benutzer hat vier wesentliche Vorteile:

- Der Administrator kann angeben, mit welchen Computern Benutzer auf ihre umgeleiteten Daten und Einstellungen zugreifen können. Der Administrator kann beispielsweise auswählen, dass für Benutzerdaten und -einstellungen zwischen dem Desktop und Laptop eines Benutzers gewechselt werden sollen, aber die Informationen nicht gewechselt werden sollen, wenn sich dieser Benutzer bei einem anderen Computer wie einem Konferenzraumcomputer anmeldet.
- Durch das Festlegen von Hauptcomputern wird das Sicherheits- und Datenschutzrisiko reduziert, dass auf dem Computer, auf dem sich der Benutzer angemeldet hat, noch persönliche Daten und Unternehmensdaten hinterlassen werden. Beispielsweise hinterlässt ein Geschäftsführer, der sich für vorübergehenden Zugriff auf dem Computer eines Mitarbeiters anmeldet, keine persönlichen Daten oder Unternehmensdaten.
- Mit Hauptcomputern kann der Administrator das Risiko eines nicht ordnungsgemäß konfigurierten oder anderweitig beschädigten Profils mindern, was durch das Roaming zwischen unterschiedlich konfigurierten Systemen (z. B. zwischen x86-basierten und x64-basierten Computern) verursacht worden sein könnte.
- Die Zeit, die für die Erstanmeldung eines Benutzers auf einem nicht primären Computer (z. B. einem Server) benötigt wird, ist kürzer, da das Roamingbenutzerprofil und die umgeleiteten Ordner des Benutzers nicht heruntergeladen werden. Die Abmeldezeiten werden auch verkürzt, da Änderungen am Benutzerprofil nicht in die Dateifreigabe hochgeladen werden müssen.

### <a name="how-have-primary-computers-changed-things"></a>Wie haben primäre Computer die Dinge verändert?

Wenn Sie das Herunterladen privater Benutzerdaten auf Hauptcomputer beschränken möchten, werden von den Technologien Ordnerumleitung und Roamingbenutzerprofile die folgenden Logiküberprüfungen ausgeführt, sobald sich ein Benutzer an einem Computer anmeldet:

1. Vom Windows-Betriebssystem werden die neuen Gruppenrichtlinieneinstellungen (**Roamingprofile nur auf primäre Computer herunterladen** und **Ordner nur auf primären Computern umleiten**) überprüft, um zu bestimmen, ob das Attribut **msDS-Primary-Computer** in Active Directory Domain Services (AD DS) die Entscheidung für das Roaming des Benutzerprofils oder das Anwenden der Ordnerumleitung beeinflussen soll.
2. Wenn durch die Richtlinieneinstellung die Unterstützung für Hauptcomputer aktiviert wird, wird von Windows überprüft, ob das AD DS-Schema das Attribut **msDS-Primary-Computer** unterstützt. Ist dies der Fall, wird von Windows folgendermaßen bestimmt, ob der Computer, an dem sich der Benutzer gerade anmeldet, als Hauptcomputer für den Benutzer festgelegt ist:
    1. Wenn es sich bei dem Computer um einen der primären Computer des Benutzers handelt, werden von Windows die Einstellungen „Roamingbenutzerprofil“ und „Ordnerumleitung“ angewendet.
    2. Wenn es sich bei dem Computer nicht um einen der primären Computer des Benutzers handelt, wird von Windows das zwischengespeicherte lokale Profil des Benutzers (falls vorhanden) geladen oder ein neues lokales Profil erstellt. Von Windows werden gemäß der Entfernungsaktion, die in der zuvor angewendeten Gruppenrichtlinieneinstellung angegeben ist, auch alle vorhandenen Ordnerumleitungen entfernt. Diese Einstellung wird in der lokalen Konfiguration für die Ordnerumleitung beibehalten.

Weitere Informationen finden Sie unter [Deploy Primary Computers for Folder Redirection and Roaming User Profiles](deploy-primary-computers.md)

## <a name="hardware-requirements"></a>Hardwareanforderungen

Die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile erfordern einen x64-basierten oder x86-basierten Computer, und sie werden von Windows auf ARM-(WOA)-basierten Computern nicht unterstützt.

## <a name="software-requirements"></a>Softwareanforderungen

Zum Festlegen von Hauptcomputern muss Ihre Umgebung die folgenden Anforderungen erfüllen:

- Das AD DS-Schema (Active Directory Domain Services) muss so aktualisiert werden, dass es das Windows Server 2012-Schema und die -Bedingungen enthält (beim Installieren eines Windows Server 2012-Domänencontrollers oder höher wird das Schema automatisch aktualisiert). Weitere Informationen zum Aktualisieren des AD DS-Schemas finden Sie unter [Aktualisieren von Domänencontrollern auf Windows Server 2016](../../identity/ad-ds/deploy/upgrade-domain-controllers.md).
- Clientcomputer müssen Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausführen und der Active Directory-Domäne angehören, die Sie verwalten.

## <a name="more-information"></a>Weitere Informationen

Weitere verwandte Informationen finden Sie in den folgenden Ressourcen:

| Inhaltstyp | Referenzen |
| --- | --- |
| Produktbewertung | [Unterstützen von Information Workern durch zuverlässige Dateidienste und Speichertechnologien](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831495(v%3dws.11)>)<br>[Neuerungen in Offlinedateien](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff183315(v=ws.10)>) (Windows 7 und Windows Server 2008 R2)<br>[Neuerungen bei Offlinedateien für Windows Vista](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc749449(v=ws.10)>)<br>[Änderungen an Offlinedateien in Windows Vista](<https://technet.microsoft.com/library/2007.11.offline.aspx>) (TechNet Magazine) |
| Bereitstellung | [Bereitstellen von Ordnerumleitung, Offlinedateien und Roamingbenutzerprofilen](deploy-folder-redirection.md)<br>[Implementieren einer Endbenutzerlösung für die Datenzentralisierung: Validierung und Bereitstellung von Technologien für Ordnerumleitung und Offlinedateien](https://download.microsoft.com/download/3/0/1/3019A3DA-2F41-4F2D-BBC9-A6D24C4C68C4/Implementing%20an%20End-User%20Data%20Centralization%20Solution.docx)<br>[Leitfaden zur Verwaltung von Roamingbenutzerdaten](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc766489(v=ws.10)>)<br>[Schrittweise Anleitung: Konfigurieren von neuen Offlinedateifunktionen für Windows 7-Computer](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff633429(v=ws.10)>)<br>[Verwenden von Ordnerumleitung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753996(v=ws.11)>)<br>[Implementieren von Ordnerumleitung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc737434(v=ws.10)>) (Windows Server 2003) |
| Tools und Einstellungen | [Offlinedateien auf MSDN](https://msdn.microsoft.com/library/cc296092.aspx)<br>[Gruppenrichtlinienreferenz für Offlinedateien](https://msdn.microsoft.com/library/ms878937.aspx) (Windows 2000) |
| Communityressourcen | [Forum zu Dateidiensten und Speicher](https://social.technet.microsoft.com/forums/windowsserver/home?forum=winserverfiles)<br>[Hey, Scripting Guy! Wie kann ich mit dem Feature „Offlinedateien“ in Windows arbeiten?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>)<br>[Hey, Scripting Guy! Wie kann ich Offlinedateien aktivieren und deaktivieren?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>) |
| Verwandte Technologien|[Identität und Zugriff in Windows Server](../../identity/identity-and-access.yml)<br>[Speicher](../storage.yml)<br>[Remotezugriff und Serververwaltung](../../remote/index.yml) |
