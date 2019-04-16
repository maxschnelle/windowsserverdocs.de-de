---
title: Übersicht über die Umleitung des Ordners, Offline-Dateien und servergespeicherte Benutzerprofile
description: Eine Übersicht über Ordnerumleitung, Offline-Dateien und servergespeicherte Benutzerprofile Technologien.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4e3cf32cd718b906f16fc09901284d8520177df8
ms.sourcegitcommit: 375e94dc70c76e7aa5679c32f0f4dbc26cf7dd83
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2018
ms.locfileid: "2233496"
---
# <a name="folder-redirection-offline-files-and-roaming-user-profiles-overview"></a>Übersicht über die Umleitung des Ordners, Offline-Dateien und servergespeicherte Benutzerprofile

>Betrifft: 10 Windows, Windows 8, Windows 8.1, WindowsServer 2012, Windows Server 2012 R2, WindowsServer 2016

In diesem Thema wird die Umleitung des Ordners, Offline-Dateien (clientseitiges Zwischenspeichern oder CSC) und servergespeicherte Benutzerprofile (auch bekannt als servergespeicherte Benutzerprofile) Technologien, einschließlich der neuen Features und wo Sie zusätzliche Informationen finden.

## <a name="technology-description"></a>Beschreibung der Technologie

Die Ordnerumleitung und Offlinedateien werden gemeinsam verwendet, um den Pfad lokaler Ordner (z. B. des Ordners "Dokumente") an eine Netzwerkadresse umzuleiten. Die Inhalte werden dagegen lokal zwischengespeichert, um eine höhere Geschwindigkeit und Verfügbarkeit sicherzustellen. Mit Roamingbenutzerprofilen wird ein Benutzerprofil an eine Netzwerkadresse umgeleitet. Diese Funktionen verwendet, um als Intellimirror bezeichnet werden.

- **Ordnerumleitung** ermöglicht es Benutzern und Administratoren zur Umleitung von des Pfads zu einem bekannten Ordner an einen neuen Speicherort, manuell oder mithilfe von Gruppenrichtlinien. Am neue Speicherort kann es sich um einen Ordner auf dem lokalen Computer oder ein Verzeichnis auf einer Dateifreigabe sein. Benutzer interagieren mit Dateien im Ordner umgeleitete, als ob es sich immer noch auf dem lokalen Laufwerk vorhanden. Beispielsweise können Sie den Ordner Dokumente, die normalerweise auf einem lokalen Laufwerk gespeichert ist, an einem Speicherort im Netzwerk umleiten. Die Dateien im Ordner stehen dann an den Benutzer von einem beliebigen Computer im Netzwerk.
- **Offline-Dateien** zur Verfügung Netzwerkdateien auf einen Benutzer, auch wenn die Netzwerkverbindung mit dem Server nicht verfügbar oder langsam ist. Wenn Sie online arbeiten, ist die Datei Access Leistung mit der Geschwindigkeit des Netzwerks sowie die Server. Wenn Sie offline arbeiten, werden die Dateien aus dem Offlinedateienordner-Dateien mit lokalem Zugriff Geschwindigkeit abgerufen. Ein Computer wechselt in den Offlinemodus wenn:
  - **Immer** Offlinemodus wurde aktiviert
  - Der Server ist nicht verfügbar
  - Die Netzwerkschnittstelle ist langsamer als einen konfigurierbaren Schwellenwert
  - Der Benutzer wechselt manuell in den Offlinemodus mithilfe der Schaltfläche **offline arbeiten** in Windows Explorer
- **Servergespeicherte Benutzerprofile** leitet von Benutzerprofilen in einer Dateifreigabe, damit Benutzer das gleiche Betriebssystem und Anwendungseinstellungen auf mehreren Computern empfangen. Wenn ein Benutzer an einem Computer anmeldet mit einem Konto an, die mit einer Dateifreigabe als Profilpfad eingerichtet ist, ist das Profil des Benutzers auf dem lokalen Computer heruntergeladen und (falls vorhanden) mit dem lokalen Profil zusammengeführt. Wenn der Computer der Benutzer abmeldet, wird die lokale Kopie des ihr Profil, einschließlich der Änderungen, mit dem Serverexemplar des Profils zusammengeführt. In der Regel aktiviert Netzwerkadministrator servergespeicherte Benutzerprofile auf Domänenkonten.

## <a name="practical-applications"></a>Praktische Anwendungsfälle

Administratoren können Ordnerumleitung, Offline-Dateien und servergespeicherte Benutzerprofile zur Speicherung von Benutzerdaten und Einstellungen für Zentralisierung und um Benutzern den Zugriff auf ihre Daten während der offline oder im Fall eines Ausfalls Netzwerk- oder bereitzustellen verwenden. Einige bestimmten Anwendungen umfassen:

- Zentralisieren der Daten von Clientcomputern für administrative Aufgaben wie die Verwendung eines serverbasierten Sicherungsprogramms zum Sichern von Benutzerordnern und Einstellungen.
- Aktivieren Sie Benutzer weiterhin den Zugriff auf Netzwerk-Datendateien, auch wenn Netzwerk- oder derzeit nicht zur Verfügung.
- Optimieren der bandbreitennutzung und Verbesserung der Erfahrung von Benutzern in Zweigstellen, die Zugriff auf Dateien und Ordner, die von Firmenserver befindet sich außerhalb des Betriebsgeländes gehostet werden.
- Mobile Benutzer auf Netzwerkdateien zuzugreifen, während Sie arbeiten, offline oder über langsame Netzwerke zu aktivieren.

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

Die folgende Tabelle beschreibt einige der wichtigsten Änderungen im Ordnerumleitung, Offline-Dateien und servergespeicherte Benutzerprofile, die in dieser Version verfügbar sind.

|Feature/Funktionalität|Neu oder aktualisiert?|Beschreibung|
|---|---|---|
|Immer Offline-Modus|Neu|Bietet schnelleren Zugriff auf Dateien und niedriger Bandbreite von immer offline arbeiten, auch wenn über eine Hochgeschwindigkeits-Verbindung verbunden.|
|Kosten-fähigen Synchronisierung|Neu|Hilft Benutzern bei hohe Auslastung Kosten von der Synchronisierung während der Verwendung von gemessener Verbindungen, die Einschränkungen haben oder beim roaming auf einen anderen Anbieter Netzwerk vermeiden.|
|Primäre PC-Unterstützung|Neu|Ermöglicht die Verwendung von Ordnerumleitung und/oder servergespeicherte Benutzerprofile, nur die primäre Computer des Benutzers zu begrenzen.|

## <a name="always-offline-mode"></a>Immer Offline-Modus

Beginnend mit Windows 8 und Windows Server 2012, können Administratoren konfigurieren die Erfahrung für Benutzer Offlinedateien immer offline arbeiten, auch wenn sie über eine Hochgeschwindigkeits-Verbindung verbunden sind. Windows-updates stündlich im Hintergrund standardmäßig Synchronisieren von Dateien im Cache Offline-Dateien.

### <a name="what-value-does-always-offline-mode-add"></a>Der Wert ist immer Offline Modus hinzufügen?

Immer Offline-Modus bietet die folgenden Vorteile:

- Benutzer bemerken schnelleren Zugriff auf Dateien in umgeleiteten Ordnern, beispielsweise im Ordner Dokumente.
- Wird die Netzwerkbandbreite verringert Kosten für teuren WAN-Verbindungen oder gemessenen Verbindungen wie eine mobile 4 G Netzwerk gesenkt werden können.

### <a name="how-has-always-offline-mode-changed-things"></a>Wie hat immer Offlinemodus Dinge geändert?

Vor Windows 8, Windows Server 2012 würde Benutzer den Übergang zwischen den Modi Online und Offline je nach Verfügbarkeit des Netzwerks und Bedingungen, auch wenn der langsam-Link-Modus (auch bekannt als die langsame Verbindung-Modus) aktiviert und auf einer 1 Millisekunde festgelegt wurde Schwellenwert für die Wartezeit.

Immer Offline-Modus wechseln Computer nie in den Onlinemodus, wenn die gruppenrichtlinieneinstellung **langsamer Links Konfigurationsmodus** konfiguriert ist und der **Wartezeit** Schwellenwertparameter 1 Millisekunde festgelegt ist. Änderungen werden synchronisiert im Hintergrund 120 Minuten standardmäßig, aber Synchronisierung kann mithilfe der Gruppenrichtlinien-Einstellung **Konfigurieren Hintergrund Sync** konfiguriert werden.

Weitere Informationen finden Sie unter [Aktivieren der immer Offlinemodus schneller Zugriff auf Dateien bereitstellen](enable-always-offline.md).

## <a name="cost-aware-synchronization"></a>Kosten-fähigen Synchronisierung

Mit Kosten-fähigen Synchronisierung wird Windows Synchronisierung im Hintergrund deaktiviert, wenn der Benutzer eine Netzwerkverbindung gemessenen verwenden, wie eine mobile 4G-Netzwerk und des Abonnenten ist in Ihrer Nähe oder ihre Bandbreite Grenzwert überschreitet, oder auf einen anderen Anbieter Netzwerk roaming.

>[!NOTE]
>Gemessenen Netzwerkverbindungen haben in der Regel Round-Trip Wartezeiten, die langsamer als der Wert für die Wartezeit von 35 Millisekunden für den Übergang zu Offline (langsame Verbindung)-Modus in Windows 8, Windows Server 2012 und Windows Server 2016 sind. Aus diesem Grund Übergang diese Verbindungen in der Regel auf Offline (langsame Verbindung) Modus automatisch.

### <a name="what-value-does-cost-aware-synchronization-add"></a>Welchen Wert Fügt Kosten-fähigen Synchronisierung hinzu?

Kosten-fähigen Synchronisierung hilft Benutzern bei unerwartet hohe Auslastung Kosten zu vermeiden, während der Verwendung von gemessener Verbindungen, die Einschränkungen haben oder beim roaming auf einen anderen Anbieter Netzwerk.

### <a name="how-has-cost-aware-synchronization-changed-things"></a>Wie hat sich Kosten-fähigen Synchronisierung Dinge geändert?

Benutzer, die Gebühren zu minimieren, bei Verwendung von Offline-Dateien auf gemessenen Netzwerkverbindungen wollten musste vor Windows 8 und Windows Server 2012 ihre Verwendung von Daten mithilfe von Tools aus der mobilen Netzwerkanbieter verfolgen. Der Benutzer konnte in den Offlinemodus, wenn sie roaming wurden, ihre Bandbreite Grenzwert oder über die Grenze dann manuell wechseln.

Mit Kosten-fähigen Sync verfolgt Windows automatisch roaming und Bandbreite Einschränkungen beim Ressourceneinsatz während in gemessenen Verbindungen. Wenn der Benutzer ihre Bandbreite Grenzwert oder über die Grenze roaming ist in den Offlinemodus wechselt und Windows verhindert, dass alle Synchronisierung. Benutzer können immer noch manuell initiieren, Synchronisierung und Administratoren können Kosten-fähigen Synchronisierung für bestimmte Benutzer, wie die Führungskräfte außer Kraft setzen.

Weitere Informationen finden Sie unter [Dateisynchronisierung im Hintergrund auf gemessene Netzwerke aktivieren](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj127408(v%3dws.11)).

## <a name="primary-computers-for-folder-redirection-and-roaming-user-profiles"></a>Primäre Computern für Ordnerumleitung und servergespeicherte Benutzerprofile

Sie können jetzt festlegen, dass eine Gruppe von Computern, die als primäre Computern für jeden Domänenbenutzer, der Ihnen die Kontrolle ermöglicht Ordnerumleitung, servergespeicherte Benutzerprofile oder beide, welchen Computern verwenden bezeichnet. Zuweisen eines primäre Computern ist eine einfache und leistungsstarke Methode Zuordnen von Benutzerdaten und Einstellungen zu bestimmten Computern oder Geräten, Administrator Aufsicht vereinfachen, Verbesserung der Sicherheit und Schutz von Benutzerprofilen aus einer Beschädigung.

### <a name="what-value-do-primary-computers-add"></a>Welchen Wert füge primären Computer hinzu?

Es gibt vier wichtigsten Vorteile der primären Computer für Benutzer festlegen:

- Der Administrator kann festlegen, welche Computer Benutzer Zugriff auf ihre umgeleitete Daten und Einstellungen verwenden können. Beispielsweise kann der Administrator wählen, um Roaming von Benutzerdaten und Einstellungen zwischen Desktop- und Laptopcomputern eines Benutzers und kein Roaming von die Informationen an, wenn der Benutzer zu einem anderen Computer, wie eine Konferenz Raum Computer anmeldet.
- Festlegen der primären Computer reduziert, Sicherheit und Datenschutz Risiko verlassen persönliche oder corporate Restdaten auf Computern, auf dem der Benutzer angemeldet hat. Geschäftsführer, eines Mitarbeiters temporäre auf Computer anmeldet, wird beispielsweise nicht hinter alle persönlichen Daten und Unternehmensdaten lassen.
- Primäre Computern ermöglicht den Administrator das Risiko eines falsch konfigurierten zu verringern oder andernfalls beschädigtes Profil, wodurch konnte von roaming zwischen unterschiedlich konfiguriert Systeme, wie beispielsweise zwischen X86 und X64-basierten Computer.
- Die Zeitdauer, die für einen Benutzer erste Anmeldung auf einem Computer nicht als Primärschlüssel, wie ein Server erforderlich ist schneller, da servergespeicherte Benutzerprofil und/oder umgeleitete Ordner des Benutzers nicht heruntergeladen werden. Abmelde Zeiten sind auch verringert, da Änderungen an dem Benutzerprofil nicht auf die Dateifreigabe hochgeladen werden müssen.

### <a name="how-have-primary-computers-changed-things"></a>Geändert primäre Computern haben wie Dinge?

Zum Beschränken der persönlichen Daten zum primären Computer herunterladen, führen Sie die Technologien Ordnerumleitung und servergespeicherte Benutzerprofile die folgenden Logik überprüft, wenn ein Benutzer an einem Computer anmeldet:

1. Windows-Betriebssystems überprüft die neuen Einstellungen für Gruppenrichtlinien (**Download servergespeicherten Benutzerprofilen auf primäre Computern nur** und **Umleiten Ordnern auf primäre Computern nur**) zu ermitteln, ob das Attribut **MsDS-primärer-Computer** aktiven Directory-Domänendienste (AD DS) sollte die Entscheidung für das Profil des Benutzers Roaming oder Ordnerumleitung anwenden beeinflussen.
2. Wenn die Einstellung in der Unterstützung von primären Computer ermöglicht, überprüft Windows, dass das AD DS-Schema das Attribut **MsDS-primärer-Computer** unterstützt. Wenn dies der Fall ist, bestimmt Windows, wenn der Computer, auf dem der Benutzer angemeldet ist als primäre Computer für den Benutzer festgelegt ist:
    1. Wenn der Computer mit einem der primäre Computer des Benutzers ist, wendet Windows die Einstellungen für servergespeicherte Benutzerprofile und Ordnerumleitung.
    2. Wenn der Computer nicht der primäre Computer des Benutzers ist, Windows lädt zwischengespeicherten lokalen Profil des Benutzers, sofern vorhanden, oder es erstellt ein neues lokales Profil. Windows entfernt auch alle vorhandenen umgeleitete Ordner entsprechend die entfernen-Aktion, die von der Einstellung der zuvor angewendeten Gruppenrichtlinien angegeben wurde, das der in der lokalen Ordnerumleitung Konfiguration beibehalten wird.

Weitere Informationen finden Sie unter [Bereitstellen von primären Computern für Ordnerumleitung und servergespeicherte Benutzerprofile](deploy-primary-computers.md)

## <a name="hardware-requirements"></a>Hardwareanforderungen

Ordnerumleitung, Offline-Dateien und servergespeicherte Benutzerprofile erfordern einen X64 oder X86-basierten Computer, und sie werden nicht von Windows unterstützt, auf Computern mit ARM-WOA.

## <a name="software-requirements"></a>Softwareanforderungen

Zum Bestimmen von primären Computer muss die Umgebung die folgenden Anforderungen erfüllen:

- Das Schema der Active Directory-Domänendienste (AD DS) zum Einschließen von Windows Server 2012-Schema und Bedingungen aktualisiert werden muss (Installieren von einem Windows Server 2012 oder höher Domänencontroller automatisch aktualisiert das Schema). Weitere Informationen zum Aktualisieren des AD DS-Schemas finden Sie unter [Upgrade-Domänencontrollern auf Windows Server 2016](../../identity/ad-ds/deploy/upgrade-domain-controllers.md).
- Clientcomputer ausführen müssen, 10 für Windows, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 und Active Directory-Domäne, die Sie verwalten beigetreten sein.

## <a name="more-information"></a>Weitere Informationen

Weitere verwandte Informationen finden Sie in den folgenden Ressourcen:

|Inhaltstyp|Verweise|
|---|---|
|Produktbewertung|[Unterstützung für Information Worker mit zuverlässige Dateidienste und Speicher](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831495(v%3dws.11)>)<br>[Was ist neu in Offline-Dateien](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff183315(v=ws.10)>) (Windows 7 und Windows Server 2008 R2)<br>[Was ist neu in Offline-Dateien für Windows Vista](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc749449(v=ws.10)>)<br>[Änderungen an Offline-Dateien in Windows Vista](<https://technet.microsoft.com/library/2007.11.offline.aspx>) (TechNet Magazine)|
|Bereitstellung|[Bereitstellen von Ordnerumleitung, Offline-Dateien und servergespeicherte Benutzerprofile](deploy-folder-redirection.md)<br>[Implementieren einer Endbenutzer-Datenlösung Zentralisierung: Ordnerumleitung und Offlinedatendateien Technologie Validierung und Bereitstellung](http://download.microsoft.com/download/3/0/1/3019A3DA-2F41-4F2D-BBC9-A6D24C4C68C4/Implementing%20an%20End-User%20Data%20Centralization%20Solution.docx)<br>[Verwalten von Bereitstellungshandbuch für Roaming](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc766489(v=ws.10)>)<br>[Konfigurieren neuer Offline Dateien Features für schrittweise Anleitung für Windows 7-Computern](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff633429(v=ws.10)>)<br>[Verwenden der Ordnerumleitung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753996(v=ws.11)>)<br>[Implementieren von Ordnerumleitung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc737434(v=ws.10)>) (WindowsServer 2003)|
|Tools und Einstellungen|[Offline-Dateien auf MSDN](https://msdn.microsoft.com/library/cc296092.aspx)<br>[Offline Dateien Group Policy Reference](https://msdn.microsoft.com/library/ms878937.aspx) (Windows 2000)|
|Communityressourcen|[Forum zu Dateidiensten und Speicher](https://social.technet.microsoft.com/forums/windowsserver/home?forum=winserverfiles)<br>[Hallo, Scripting Guy! Wie kann ich mit dem Feature Offline-Dateien in Windows arbeiten?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>)<br>[Hallo, Scripting Guy! Wie kann ich aktivieren und Deaktivieren von Offline-Dateien?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>)|
Verwandte Technologien|[Identitäts- und Windows Server](../../identity/identity-and-access.md)<br>[Speicher in Windows Server](../storage.md)<br>[Remotezugriff und Serververwaltung](../../remote/index.md)|