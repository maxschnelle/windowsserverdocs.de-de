---
title: Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile – Übersicht
description: Eine Übersicht über die Technologien für die Ordner Umleitung, Offlinedateien und Roamingbenutzerprofile.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae1b23244f141cd0806ee14d3c40117ba72aeebb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402060"
---
# <a name="folder-redirection-offline-files-and-roaming-user-profiles-overview"></a>Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile – Übersicht

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2

In diesem Thema werden die Technologien für Ordner Umleitung, Offlinedateien (Client seitiges Caching oder CSC) und Roamingbenutzerprofile (auch als RUP bezeichnet) erläutert, einschließlich der Neuerungen und der Art und Weise, wie Sie zusätzliche Informationen finden.

## <a name="technology-description"></a>Technologiebeschreibung

Die Ordnerumleitung und Offlinedateien werden gemeinsam verwendet, um den Pfad lokaler Ordner (z. B. des Ordners "Dokumente") an eine Netzwerkadresse umzuleiten. Die Inhalte werden dagegen lokal zwischengespeichert, um eine höhere Geschwindigkeit und Verfügbarkeit sicherzustellen. Mit Roamingbenutzerprofilen wird ein Benutzerprofil an eine Netzwerkadresse umgeleitet. Diese Features werden meist als IntelliMirror bezeichnet.

- **Die Ordner Umleitung** ermöglicht es Benutzern und Administratoren, den Pfad eines bekannten Ordners manuell oder mithilfe von Gruppenrichtlinie an einen neuen Speicherort umzuleiten. Der neue Ort kann ein Ordner auf dem lokalen Computer oder ein Verzeichnis in einer Dateifreigabe sein. Benutzer interagieren mit den Dateien im umgeleiteten Ordner, als würde er noch auf dem lokalen Laufwerk vorhanden sein. Sie können beispielsweise den Ordner %%amp;quot;Dokumente%%amp;quot;, der normalerweise auf einem lokalen Laufwerk gespeichert wird, an eine Netzwerkadresse umleiten. Die Dateien im Ordner stehen dem Benutzer dann auf jedem Computer im Netzwerk zur Verfügung.
- **Offlinedateien macht Netzwerk**Dateien für einen Benutzer verfügbar, selbst wenn die Netzwerkverbindung mit dem Server nicht verfügbar oder langsam ist.  Wenn Sie online arbeiten, entspricht die Zugriffsleistung der Geschwindigkeit des Netzwerks und des Servers. Wenn Sie offline arbeiten, werden die Dateien mit der lokalen Zugriffsgeschwindigkeit aus dem Ordner %%amp;quot;Offlinedateien%%amp;quot; abgerufen. Ein Computer wechselt in folgenden Situationen in den Offlinemodus:
  - Der Modus " **immer offline** " wurde aktiviert.
  - Der Server ist nicht verfügbar.
  - Die Netzwerkverbindung ist langsamer als ein konfigurierbarer Schwellenwert.
  - Der Benutzer wechselt mithilfe der Schaltfläche **Offlinebetrieb** im Windows-Explorer manuell in den Offlinemodus.
- **Roamingbenutzerprofile** leiten Benutzerprofile an eine Dateifreigabe um, damit Benutzer auf mehreren Computern dieselben Betriebssystem-und Anwendungseinstellungen erhalten. Wenn ein Benutzer sich mithilfe eines Kontos, das mit einer Dateifreigabe als Profilpfad eingerichtet ist, bei einem Computer anmeldet, wird das Profil des Benutzers auf den lokalen Computer heruntergeladen und mit dem lokalen Profil (falls vorhanden) zusammengeführt. Wenn sich der Benutzer vom Computer abmeldet, wird die lokale Kopie seines Profils, einschließlich aller Änderungen, mit der Serverkopie des Profils zusammengeführt. In der Regel aktiviert ein Netzwerkadministrator Roamingbenutzerprofile auf Domänen Konten.

## <a name="practical-applications"></a>Praktische Anwendungsfälle

Administratoren können die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile verwenden, um den Speicher für Benutzerdaten und -einstellungen zu zentralisieren und Benutzern die Möglichkeit zu bieten, im Offlinemodus oder im Falle eines Netzwerk- oder Serverausfalls auf ihre Daten zuzugreifen. Einige spezielle Anwendungsfälle umfassen Folgendes:

- Zentralisieren von Daten auf Clientcomputern für administrative Aufgaben wie das Verwenden eines serverbasierten Sicherungstools zum Sichern von Benutzerordnern und -einstellungen
- Ermöglichen des dauerhaften Zugriffs auf Netzwerkdateien für Benutzer, selbst wenn ein Netzwerk- oder Serverausfall auftritt
- Optimieren der Bandbreitenverwendung und Verbessern der Arbeitsmöglichkeiten von Benutzern in Filialen, die auf Dateien und Ordner zugreifen, die von Unternehmensservern an anderen Standorten gehostet werden
- Ermöglichen des Zugriffs auf Netzwerkdateien für mobile Benutzer, während sie offline oder über langsame Netzwerke arbeiten

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

In der folgenden Tabelle sind einige wichtige Änderungen an der Ordnerumleitung, den Offlinedateien und den Roamingbenutzerprofilen beschrieben, die in dieser Version verfügbar sind.

| Feature/Funktionalität | Neu oder aktualisiert? | Beschreibung |
| --- | --- | --- |
| Immer im Offlinemodus | Neu | Bietet schnelleren Zugriff auf Dateien und geringere Bandbreitenverwendung, selbst wenn eine Hochgeschwindigkeits-Netzwerkverbindung besteht. |
| Sparsame Synchronisation | Neu | Hilft Benutzern, hohe Daten Nutzungskosten durch Synchronisierung zu vermeiden, indem getaktete Verbindungen mit Nutzungs Limits verwendet werden oder das Roaming im Netzwerk eines anderen Anbieters durchlaufen wird. |
| Unterstützung von Hauptcomputern | Neu | Ermöglicht es Ihnen, die Verwendung der Ordner Umleitung, Roamingbenutzerprofile oder beides auf die primären Computer eines Benutzers zu beschränken. |

## <a name="always-offline-mode"></a>Immer im Offlinemodus

Ab Windows 8 und Windows Server 2012 können Administratoren die Benutzer Offlinedateien so konfigurieren, dass Sie immer offline arbeiten, auch wenn Sie über eine Hochgeschwindigkeitsnetzwerk Verbindung verbunden sind. Unter Windows werden Dateien standardmäßig durch stündliche Synchronisierung im Hintergrund im Zwischenspeicher für Offlinedateien aktualisiert.

### <a name="what-value-does-always-offline-mode-add"></a>Welcher Wert wird vom Offline Modus hinzugefügt?

Der Modus "Immer offline" bietet die folgenden Vorteile:

- Benutzer profitieren von einem schnelleren Zugriff auf Dateien in umgeleiteten Ordnern wie dem Ordner "Dokumente".
- Die Netzwerkbandbreite ist reduziert, wodurch Kosten für teure WAN-Verbindungen oder getaktete Verbindungen wie ein mobiles 4G-Netzwerk gesenkt werden.

### <a name="how-has-always-offline-mode-changed-things"></a>Wie hat sich die Dinge im Offline Modus geändert?

Vor Windows 8, Windows Server 2012, wechselten Benutzer je nach Netzwerkverfügbarkeit und-Bedingungen zwischen dem Online-und Offline Modus, selbst wenn der Modus für langsame Verbindungen aktiviert und auf einen Wert von 1 Millisekunde festgelegt wurde. Latenz Schwellenwert.

Im Modus "immer offline" wechseln Computer nie in den Online Modus, wenn der **Modus für langsame Verbindungen konfigurieren** Gruppenrichtlinie konfiguriert ist und der Schwellenwert für die **Latenz** Zeit auf 1 Millisekunde festgelegt ist. Änderungen werden standardmäßig alle 120 Minuten im Hintergrund synchronisiert, aber die Synchronisierung kann mithilfe der Gruppenrichtlinieneinstellung **Hintergrundsynchronisierung konfigurieren** konfiguriert werden.

Weitere Informationen finden Sie unter [Aktivieren der Always Offline Mode to Provide Faster Access to Dateien](enable-always-offline.md).

## <a name="cost-aware-synchronization"></a>Sparsame Synchronisation

Bei der Kosten abhängigen Synchronisierung wird die Hintergrund Synchronisierung von Windows deaktiviert, wenn der Benutzer eine getaktete Netzwerkverbindung verwendet, z. b. ein 4G-Mobilfunknetz, und der Abonnent sich in der Nähe oder über seinem Bandbreiten Limit befindet oder das Roaming im Netzwerk eines anderen Anbieters erfolgt.

> [!NOTE]
> Getaktete Netzwerkverbindungen weisen in der Regel Roundtrip-Netzwerk Wartezeiten auf, die langsamer als der standardmäßige Latenz Wert von 35 Millisekunden für den Wechsel in den Offline Modus (langsamer Verbindungs Modus) in Windows 8, Windows Server 2019, Windows Server 2016 und Windows Server sind. 2012. Daher wechseln diese Verbindungen in der Regel automatisch in den Offlinemodus (Modus für langsame Verbindungen).

### <a name="what-value-does-cost-aware-synchronization-add"></a>Welcher Wert wird durch die kostenbewusste Synchronisierung hinzugefügt?

Die kostenbewusste Synchronisierung hilft Benutzern dabei, unerwartet hohe Daten Nutzungskosten zu vermeiden, indem getaktete Verbindungen mit Nutzungs Limits verwendet werden oder das Roaming im Netzwerk eines anderen Anbieters durchlaufen wird.

### <a name="how-has-cost-aware-synchronization-changed-things"></a>Wie hat sich die kostenbewusste Synchronisierung geändert?

Vor Windows 8 und Windows Server 2012 mussten Benutzer, die die Gebühren bei der Verwendung von Offlinedateien auf getaktete Netzwerkverbindungen minimieren wollten, ihre Datennutzung mithilfe von Tools des Anbieters des mobilen Netzwerks nachverfolgen. Benutzer konnten dann manuell den Offlinemodus aktivieren, wenn sie in ein anderes Netzwerk gewechselt sind oder das Bandbreitenlimit fast erreicht oder überschritten hatten.

Mit der Kosten abhängigen Synchronisierung werden von Windows automatisch Roaming-und Bandbreiten Einschränkungen nachverfolgt, während getaktete Verbindungen verwendet werden. Wenn der Benutzer in ein anderes Netzwerk wechselt oder sein Limit erreicht oder überschreitet, wird unter Windows in den Offlinemodus gewechselt und die Synchronisierung verhindert. Benutzer können die Synchronisierung weiterhin manuell initiieren, und Administratoren können die sparsame Synchronisierung für bestimmte Benutzer wie Führungskräfte außer Kraft setzen.

Weitere Informationen finden Sie unter [Enable Background File Synchronization on Metered Networks](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj127408(v%3dws.11)).

## <a name="primary-computers-for-folder-redirection-and-roaming-user-profiles"></a>Hauptcomputer für Ordnerumleitung und Roamingbenutzerprofile

Sie können jetzt für jeden Domänen Benutzer eine Reihe von Computern festlegen, die als primäre Computer bezeichnet werden. damit können Sie steuern, auf welchen Computern die Ordner Umleitung, Roamingbenutzerprofile oder beides verwendet wird. Das Festlegen von Hauptcomputern ist eine einfache und leistungsfähige Methode, um Benutzerdaten und -einstellungen bestimmten Computern oder Geräten zuzuordnen. Dadurch kann sich der Administrator leichter eine Übersicht verschaffen, die Datensicherheit wird verbessert, und die Benutzerprofile werden vor Beschädigung geschützt.

### <a name="what-value-do-primary-computers-add"></a>Welche Werte werden von primären Computern hinzugefügt?

Das Festlegen von Hauptcomputern für Benutzer hat vier wesentliche Vorteile:

- Der Administrator kann angeben, mit welchen Computern Benutzer auf ihre umgeleiteten Daten und Einstellungen zugreifen können. Beispielsweise kann der Administrator festlegen, dass Benutzerdaten und-Einstellungen zwischen dem Desktop und Laptop eines Benutzers gewechselt werden sollen, und die Informationen nicht übertragen, wenn sich der Benutzer bei einem anderen Computer, z. b. einem Konferenzraum Computer, anmeldet.
- Durch das Festlegen von Hauptcomputern wird das Sicherheits- und Datenschutzrisiko reduziert, dass auf dem Computer, auf dem sich der Benutzer angemeldet hat, noch persönliche Daten und Unternehmensdaten hinterlassen werden. Beispiel: ein allgemeiner Manager, der sich für den vorübergehenden Zugriff am Computer eines Mitarbeiters anmeldet, verlässt keine persönlichen oder Unternehmensdaten.
- Mit Hauptcomputern kann der Administrator das Risiko eines nicht ordnungsgemäß konfigurierten oder anderweitig beschädigten Profils mindern, was durch das Roaming zwischen unterschiedlich konfigurierten Systemen (z. B. zwischen x86-basierten und x64-basierten Computern) verursacht worden sein könnte.
- Die Zeitspanne, die für die erste Anmeldung eines Benutzers auf einem nicht primären Computer (z. b. einem Server) benötigt wird, ist schneller, da das Roamingbenutzerprofil und die umgeleiteten Ordner des Benutzers nicht heruntergeladen werden. Die Abmeldezeiten werden auch verkürzt, da Änderungen am Benutzerprofil nicht in die Dateifreigabe hochgeladen werden müssen.

### <a name="how-have-primary-computers-changed-things"></a>Wie haben sich primäre Computer geändert?

Wenn Sie das Herunterladen privater Benutzerdaten auf Hauptcomputer beschränken möchten, werden von den Technologien Ordnerumleitung und Roamingbenutzerprofile die folgenden Logiküberprüfungen ausgeführt, sobald sich ein Benutzer an einem Computer anmeldet:

1. Das Windows-Betriebssystem überprüft die neuen Gruppenrichtlinie Einstellungen (**Roamingprofile nur auf primären Computern herunterladen** und **Ordner nur auf primären Computern umleiten**), um zu bestimmen, ob das Attribut " **msDS-Primary-Computer** " aktiv ist. Die Verzeichnis Domänen Dienste (AD DS) sollten die Entscheidung beeinflussen, das Profil des Benutzers zu überlaufen oder die Ordner Umleitung zu übernehmen.
2. Wenn durch die Richtlinieneinstellung die Unterstützung für Hauptcomputer aktiviert wird, wird von Windows überprüft, ob das AD DS-Schema das Attribut **msDS-Primary-Computer** unterstützt. Ist dies der Fall, wird von Windows folgendermaßen bestimmt, ob der Computer, an dem sich der Benutzer gerade anmeldet, als Hauptcomputer für den Benutzer festgelegt ist:
    1. Wenn es sich bei dem Computer um einen der primären Computer des Benutzers handelt, wendet Windows die Roamingbenutzerprofile und Ordner Umleitungseinstellungen an.
    2. Wenn es sich bei dem Computer nicht um einen der primären Computer des Benutzers handelt, lädt Windows das zwischengespeicherte lokale Profil des Benutzers, sofern vorhanden, oder erstellt ein neues lokales Profil. Von Windows werden gemäß der Entfernungsaktion, die in der zuvor angewendeten Gruppenrichtlinieneinstellung angegeben ist, auch alle vorhandenen Ordnerumleitungen entfernt. Diese Einstellung wird in der lokalen Konfiguration für die Ordnerumleitung beibehalten.

Weitere Informationen finden Sie unter [Bereitstellen von Hauptcomputern für Ordnerumleitung und Roamingbenutzerprofile](deploy-primary-computers.md)

## <a name="hardware-requirements"></a>Hardwareanforderungen

Die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile erfordern einen x64-basierten oder x86-basierten Computer, und sie werden von Windows auf ARM-(WOA)-basierten Computern nicht unterstützt.

## <a name="software-requirements"></a>Softwareanforderungen

Zum Festlegen von Hauptcomputern muss Ihre Umgebung die folgenden Anforderungen erfüllen:

- Das Schema für die Active Directory Domain Services (AD DS) muss aktualisiert werden, um das Schema und die Bedingungen für Windows Server 2012 einzuschließen. (durch die Installation eines Windows Server 2012 oder höher-Domänen Controllers wird das Schema automatisch aktualisiert Weitere Informationen zum Aktualisieren des AD DS Schemas finden [Sie unter Aktualisieren von Domänen Controllern auf Windows Server 2016](../../identity/ad-ds/deploy/upgrade-domain-controllers.md).
- Auf Client Computern muss Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden, und Sie müssen mit der Active Directory Domäne verknüpft werden, die Sie verwalten.

## <a name="more-information"></a>Weitere Informationen

Weitere verwandte Informationen finden Sie in den folgenden Ressourcen:

| Inhaltstyp | Verweise |
| --- | --- |
| Produktbewertung | [Unterstützung von Information-Workern mit zuverlässigen Datei Diensten und Speicher](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831495(v%3dws.11)>)<br>[Neues in Offlinedateien](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff183315(v=ws.10)>) (Windows 7 und Windows Server 2008 R2)<br>[Neues in Offlinedateien für Windows Vista](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc749449(v=ws.10)>)<br>[Änderungen an Offlinedateien in Windows Vista](<https://technet.microsoft.com/library/2007.11.offline.aspx>) (TechNet Magazine) |
| Bereitstellung | [Bereitstellen von Ordner Umleitung, Offlinedateien und Roamingbenutzerprofilen](deploy-folder-redirection.md)<br>[Implementieren einer Lösung für die Daten Zentralisierung durch Endbenutzer: Überprüfung und Bereitstellung von Ordner Umleitung und Offlinedateien Technologie](http://download.microsoft.com/download/3/0/1/3019A3DA-2F41-4F2D-BBC9-A6D24C4C68C4/Implementing%20an%20End-User%20Data%20Centralization%20Solution.docx)<br>[Handbuch zur Verwaltung von roamingbenutzerdaten](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc766489(v=ws.10)>)<br>[Schrittweise Anleitung: Konfigurieren von neuen Offlinedateifunktionen für Windows 7-Computer](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff633429(v=ws.10)>)<br>[Verwenden der Ordner Umleitung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753996(v=ws.11)>)<br>[Implementieren der Ordner Umleitung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc737434(v=ws.10)>) (Windows Server 2003) |
| Tools und Einstellungen | [Offline Dateien auf MSDN](https://msdn.microsoft.com/library/cc296092.aspx)<br>[Offlinedateien Gruppenrichtlinie Referenz](https://msdn.microsoft.com/library/ms878937.aspx) (Windows 2000) |
| Communityressourcen | [Forum zu Datei Diensten und Speicher](https://social.technet.microsoft.com/forums/windowsserver/home?forum=winserverfiles)<br>[Hallo, Scripting Guy! Wie kann ich mit dem Offlinedateien Feature in Windows arbeiten?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>)<br>[Hallo, Scripting Guy! Wie kann ich Offlinedateien aktivieren und deaktivieren?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>) |
| Verwandte Technologien|[Identität und Zugriff in Windows Server](../../identity/identity-and-access.md)<br>[Speicher](../storage.md)<br>[Remote Zugriff und Serververwaltung](../../remote/index.md) |