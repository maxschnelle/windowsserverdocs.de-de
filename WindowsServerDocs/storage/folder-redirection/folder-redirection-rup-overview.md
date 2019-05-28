---
title: Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile – Übersicht
description: Eine Übersicht über Technologien für Ordnerumleitung, Offlinedateien und servergespeicherte Benutzerprofile.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ad44ba4bbe0b31f423a4ae4593e349571d838de2
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475923"
---
# <a name="folder-redirection-offline-files-and-roaming-user-profiles-overview"></a>Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile – Übersicht

>Gilt für: Windows 10, Windows 8, Windows 8.1, WindowsServer 2019, WindowsServer 2016, WindowsServer 2012, Windows Server 2012 R2

In diesem Thema wird erläutert, die Ordnerumleitung, Offlinedateien (clientseitige Zwischenspeicherung oder CSC) und Roamingbenutzerprofile (auch als RUP bezeichnet)-Technologien, einschließlich Neuigkeiten und, wo Sie weitere Informationen zu finden.

## <a name="technology-description"></a>Technologiebeschreibung

Die Ordnerumleitung und Offlinedateien werden gemeinsam verwendet, um den Pfad lokaler Ordner (z. B. des Ordners "Dokumente") an eine Netzwerkadresse umzuleiten. Die Inhalte werden dagegen lokal zwischengespeichert, um eine höhere Geschwindigkeit und Verfügbarkeit sicherzustellen. Mit Roamingbenutzerprofilen wird ein Benutzerprofil an eine Netzwerkadresse umgeleitet. Diese Features werden meist als IntelliMirror bezeichnet.

- **Ordnerumleitung** ermöglicht es Benutzern und Administratoren, den Pfad eines bekannten Ordners manuell oder mithilfe der Gruppenrichtlinie an einem neuen Speicherort, zu umzuleiten. Der neue Ort kann ein Ordner auf dem lokalen Computer oder ein Verzeichnis in einer Dateifreigabe sein. Benutzer interagieren mit den Dateien im umgeleiteten Ordner, als würde er noch auf dem lokalen Laufwerk vorhanden sein. Sie können beispielsweise den Ordner %%amp;quot;Dokumente%%amp;quot;, der normalerweise auf einem lokalen Laufwerk gespeichert wird, an eine Netzwerkadresse umleiten. Die Dateien im Ordner stehen dem Benutzer dann auf jedem Computer im Netzwerk zur Verfügung.
- **Offlinedateien** stellen Netzwerkdateien zur Verfügung, die ein Benutzer, selbst wenn die Netzwerkverbindung mit dem Server nicht verfügbar oder langsam ist. Wenn Sie online arbeiten, entspricht die Zugriffsleistung der Geschwindigkeit des Netzwerks und des Servers. Wenn Sie offline arbeiten, werden die Dateien mit der lokalen Zugriffsgeschwindigkeit aus dem Ordner %%amp;quot;Offlinedateien%%amp;quot; abgerufen. Ein Computer wechselt in folgenden Situationen in den Offlinemodus:
  - **Immer Offline** Modus aktiviert wurde
  - Der Server ist nicht verfügbar.
  - Die Netzwerkverbindung ist langsamer als ein konfigurierbarer Schwellenwert.
  - Der Benutzer wechselt mithilfe der Schaltfläche **Offlinebetrieb** im Windows-Explorer manuell in den Offlinemodus.
- **Servergespeicherte Benutzerprofile** leiten Benutzerprofile an eine Dateifreigabe, damit Benutzer der dieselben Betriebssystem- und Anwendungseinstellungen auf mehreren Computern. Wenn sich ein Benutzer an einem Computer mithilfe eines Kontos anmeldet, das mit einer Dateifreigabe als Profilpfad eingerichtet ist, wird das Profil des Benutzers auf den lokalen Computer heruntergeladen und mit dem lokalen Profil (falls vorhanden) zusammengeführt. Wenn sich der Benutzer vom Computer abmeldet, wird die lokale Kopie seines Profils, einschließlich aller Änderungen, mit der Serverkopie des Profils zusammengeführt. In der Regel kann ein Netzwerkadministrator servergespeicherte Benutzerprofile für Domänenkonten.

## <a name="practical-applications"></a>Praktische Anwendungsfälle

Administratoren können die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile verwenden, um den Speicher für Benutzerdaten und -einstellungen zu zentralisieren und Benutzern die Möglichkeit zu bieten, im Offlinemodus oder im Falle eines Netzwerk- oder Serverausfalls auf ihre Daten zuzugreifen. Einige spezielle Anwendungsfälle umfassen Folgendes:

- Zentralisieren von Daten auf Clientcomputern für administrative Aufgaben wie das Verwenden eines serverbasierten Sicherungstools zum Sichern von Benutzerordnern und -einstellungen
- Ermöglichen des dauerhaften Zugriffs auf Netzwerkdateien für Benutzer, selbst wenn ein Netzwerk- oder Serverausfall auftritt
- Optimieren der Bandbreitenverwendung und Verbessern der Arbeitsmöglichkeiten von Benutzern in Filialen, die auf Dateien und Ordner zugreifen, die von Unternehmensservern an anderen Standorten gehostet werden
- Ermöglichen des Zugriffs auf Netzwerkdateien für mobile Benutzer, während sie offline oder über langsame Netzwerke arbeiten

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

In der folgenden Tabelle sind einige wichtige Änderungen an der Ordnerumleitung, den Offlinedateien und den Roamingbenutzerprofilen beschrieben, die in dieser Version verfügbar sind.

|Feature/Funktionalität|Neu oder aktualisiert?|Beschreibung|
|---|---|---|
|Immer im Offlinemodus|Neu|Bietet schnelleren Zugriff auf Dateien und geringere Bandbreitenverwendung, selbst wenn eine Hochgeschwindigkeits-Netzwerkverbindung besteht.|
|Sparsame Synchronisation|Neu|Hilft Benutzern dabei, hohe Datennutzungskosten durch Synchronisierung zu vermeiden, indem getaktete Verbindungen mit Nutzungslimits verwendet werden oder in das Netzwerk eines anderen Anbieters gewechselt wird.|
|Unterstützung von Hauptcomputern|Neu|Ermöglicht es, die Verwendung der Ordnerumleitung, Roamingbenutzerprofile oder beiden nur auf den Hauptcomputer eines Benutzers zu beschränken.|

## <a name="always-offline-mode"></a>Immer im Offlinemodus

Ab Windows 8 und Windows Server 2012, können Administratoren konfigurieren die Erfahrung für Benutzer von Offlinedateien immer offline arbeiten, selbst wenn sie über eine schnelle Netzwerkverbindung besteht. Unter Windows werden Dateien standardmäßig durch stündliche Synchronisierung im Hintergrund im Zwischenspeicher für Offlinedateien aktualisiert.

### <a name="what-value-does-always-offline-mode-add"></a>Welcher Wert wird immer Offline Mode hinzufügen?

Der Modus "Immer offline" bietet die folgenden Vorteile:

- Benutzer profitieren von einem schnelleren Zugriff auf Dateien in umgeleiteten Ordnern wie dem Ordner "Dokumente".
- Die Netzwerkbandbreite ist reduziert, wodurch Kosten für teure WAN-Verbindungen oder getaktete Verbindungen wie ein mobiles 4G-Netzwerk gesenkt werden.

### <a name="how-has-always-offline-mode-changed-things"></a>Wie hat immer Offline-Modus Dinge geändert?

Vor Windows 8, Windows Server 2012, würde Übergang der Benutzer zwischen dem Online- und Offlinemodus je nach netzwerkverfügbarkeit und-Bedingungen, selbst wenn der Modus für langsame Verbindungen (auch bekannt als Modus für langsame Verbindungen) aktiviert und auf einem 1 Millisekunde festgelegt war Schwellenwert für Latenz.

Immer Offline-Modus können Computer nie Übergang in den Online-Modus bei der **Modus für langsame Verbindungen konfigurieren** gruppenrichtlinieneinstellung konfiguriert ist und die **Latenz** Schwellenwertparameter auf 1 Millisekunde festgelegt ist. Änderungen werden standardmäßig alle 120 Minuten im Hintergrund synchronisiert, aber die Synchronisierung kann mithilfe der Gruppenrichtlinieneinstellung **Hintergrundsynchronisierung konfigurieren** konfiguriert werden.

Weitere Informationen finden Sie unter [Enable the Always Offline Mode to Provide Faster Access to Files](enable-always-offline.md).

## <a name="cost-aware-synchronization"></a>Sparsame Synchronisation

Bei der sparsamen Synchronisierung wird die Hintergrundsynchronisierung deaktiviert, wenn der Benutzer eine getaktete Netzwerkverbindung (z. B. ein 4G-Mobilfunknetz) verwendet und wenn der Computer in das Netzwerk eines anderen Anbieters wechselt oder das Bandbreitenlimit des Abonnenten fast erreicht oder überschritten ist.

>[!NOTE]
>Getaktete Netzwerkverbindungen weisen in der Regel Roundtrip-Netzwerkwartezeiten, die langsamer als der standardwartezeitwert von 35 Millisekunden für den Übergang in den Offline (langsame Verbindung)-Modus unter Windows 8, Windows Server-2019, Windows Server 2016 und Windows Server 2012. Daher wechseln diese Verbindungen in der Regel automatisch in den Offlinemodus (Modus für langsame Verbindungen).

### <a name="what-value-does-cost-aware-synchronization-add"></a>Welcher Wert hinzufügen die sparsame Synchronisierung?

Die sparsame Synchronisierung hilft Benutzern dabei, unerwartet hohe Datennutzungskosten zu vermeiden, indem getaktete Verbindungen mit Nutzungslimits verwendet werden oder in das Netzwerk eines anderen Anbieters gewechselt wird.

### <a name="how-has-cost-aware-synchronization-changed-things"></a>Wie hat die sparsame Synchronisierung Dinge geändert?

Vor Windows 8 und Windows Server 2012 mussten Benutzer, die Gebühren, die bei der Verwendung von Offlinedateien bei getakteten Verbindungen minimieren wollten, ihre Datennutzung mithilfe von Tools des Anbieters mobilen Netzwerks nachverfolgen. Benutzer konnten dann manuell den Offlinemodus aktivieren, wenn sie in ein anderes Netzwerk gewechselt sind oder das Bandbreitenlimit fast erreicht oder überschritten hatten.

Mit sparsame Synchronisierung werden Windows roaming und Bandbreite Limits bei getakteten Verbindungen automatisch nachverfolgt. Wenn der Benutzer in ein anderes Netzwerk wechselt oder sein Limit erreicht oder überschreitet, wird unter Windows in den Offlinemodus gewechselt und die Synchronisierung verhindert. Benutzer können die Synchronisierung weiterhin manuell initiieren, und Administratoren können die sparsame Synchronisierung für bestimmte Benutzer wie Führungskräfte außer Kraft setzen.

Weitere Informationen finden Sie unter [Enable Background File Synchronization on Metered Networks](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj127408(v%3dws.11)).

## <a name="primary-computers-for-folder-redirection-and-roaming-user-profiles"></a>Hauptcomputer für Ordnerumleitung und Roamingbenutzerprofile

Sie können jetzt festlegen, dass eine Gruppe von Computern, bekannt als Hauptcomputer für jeden Domänenbenutzer, mit dessen Hilfe Sie steuern können, welchen Computern die Ordnerumleitung, Roamingbenutzerprofile oder beides verwenden. Das Festlegen von Hauptcomputern ist eine einfache und leistungsfähige Methode, um Benutzerdaten und -einstellungen bestimmten Computern oder Geräten zuzuordnen. Dadurch kann sich der Administrator leichter eine Übersicht verschaffen, die Datensicherheit wird verbessert, und die Benutzerprofile werden vor Beschädigung geschützt.

### <a name="what-value-do-primary-computers-add"></a>Welcher Wert füge Hauptcomputer?

Das Festlegen von Hauptcomputern für Benutzer hat vier wesentliche Vorteile:

- Der Administrator kann angeben, mit welchen Computern Benutzer auf ihre umgeleiteten Daten und Einstellungen zugreifen können. Der Administrator kann beispielsweise auswählen, dass für Benutzerdaten und -einstellungen zwischen dem Desktop und Laptop eines Benutzers gewechselt werden soll, aber für die Informationen nicht gewechselt werden soll, wenn sich dieser Benutzer bei einem anderen Computer wie einem Konferenzraumcomputer anmeldet.
- Durch das Festlegen von Hauptcomputern wird das Sicherheits- und Datenschutzrisiko reduziert, dass auf dem Computer, auf dem sich der Benutzer angemeldet hat, noch persönliche Daten und Unternehmensdaten hinterlassen werden. Beispielsweise hinterlässt ein Geschäftsführer, der sich für vorübergehenden Zugriff auf dem Computer eines Mitarbeiters anmeldet, keine persönlichen Daten oder Unternehmensdaten.
- Mit Hauptcomputern kann der Administrator das Risiko eines nicht ordnungsgemäß konfigurierten oder anderweitig beschädigten Profils mindern, was durch das Roaming zwischen unterschiedlich konfigurierten Systemen (z. B. zwischen x86-basierten und x64-basierten Computern) verursacht worden sein könnte.
- Die Zeit, die für die Erstanmeldung eines Benutzers auf einem Nichthauptcomputer (z. B. einem Server) benötigt wird, ist kürzer, da das Roamingbenutzerprofil und die umgeleiteten Ordner des Benutzers nicht heruntergeladen werden. Die Abmeldezeiten werden auch verkürzt, da Änderungen am Benutzerprofil nicht in die Dateifreigabe hochgeladen werden müssen.

### <a name="how-have-primary-computers-changed-things"></a>Inwiefern haben sich Hauptcomputer Dinge verändert?

Wenn Sie das Herunterladen privater Benutzerdaten auf Hauptcomputer beschränken möchten, werden von den Technologien Ordnerumleitung und Roamingbenutzerprofile die folgenden Logiküberprüfungen ausgeführt, sobald sich ein Benutzer an einem Computer anmeldet:

1. Vom Windows-Betriebssystem werden die neuen Gruppenrichtlinieneinstellungen (**Roamingprofile nur auf Hauptcomputer herunterladen** und **Ordner nur auf Hauptcomputern umleiten**) überprüft, um zu bestimmen, ob das Attribut **msDS-Primary-Computer** in den Active Directory-Domänendiensten (AD DS) die Entscheidung für das Roaming des Benutzerprofils oder das Anwenden der Ordnerumleitung beeinflussen soll.
2. Wenn durch die Richtlinieneinstellung die Unterstützung für Hauptcomputer aktiviert wird, wird von Windows überprüft, ob das AD DS-Schema das Attribut **msDS-Primary-Computer** unterstützt. Ist dies der Fall, wird von Windows folgendermaßen bestimmt, ob der Computer, an dem sich der Benutzer gerade anmeldet, als Hauptcomputer für den Benutzer festgelegt ist:
    1. Wenn es sich bei dem Computer um einen der Hauptcomputer des Benutzers handelt, werden von Windows die Einstellungen "Roamingbenutzerprofil" und "Ordnerumleitung" angewendet.
    2. Wenn es sich bei dem Computer nicht um einen der Hauptcomputer des Benutzers handelt, wird von Windows das zwischengespeicherte lokale Profil des Benutzers (falls vorhanden) geladen oder ein neues lokales Profil erstellt. Von Windows werden gemäß der Entfernungsaktion, die in der zuvor angewendeten Gruppenrichtlinieneinstellung angegeben ist, auch alle vorhandenen Ordnerumleitungen entfernt. Diese Einstellung wird in der lokalen Konfiguration für die Ordnerumleitung beibehalten.

Weitere Informationen finden Sie unter [Deploy Primary Computers for Folder Redirection and Roaming User Profiles](deploy-primary-computers.md)

## <a name="hardware-requirements"></a>Hardwareanforderungen

Die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile erfordern einen x64-basierten oder x86-basierten Computer, und sie werden von Windows auf ARM-(WOA)-basierten Computern nicht unterstützt.

## <a name="software-requirements"></a>Softwareanforderungen

Zum Festlegen von Hauptcomputern muss Ihre Umgebung die folgenden Anforderungen erfüllen:

- Das Schema der Active Directory Domain Services (AD DS) muss aktualisiert werden, um Windows Server 2012-Schema und Bedingungen (Automatisches Installieren von einem Windows Server 2012 oder höher Domänencontroller aktualisiert das Schema). Weitere Informationen zum Aktualisieren des AD DS-Schemas finden Sie unter [Aktualisieren von Domänencontrollern auf Windows Server 2016](../../identity/ad-ds/deploy/upgrade-domain-controllers.md).
- Clientcomputer müssen Windows 10, Windows 8.1, Windows 8, Windows Server-2019, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausführen und verknüpft werden, mit der Active Directory-Domäne, die Sie verwalten.

## <a name="more-information"></a>Weitere Informationen

Weitere verwandte Informationen finden Sie in den folgenden Ressourcen:

|Inhaltstyp|Verweise|
|---|---|
|Produktbewertung|[Unterstützen von Büroanwendern mit zuverlässigen Dateidiensten und Speicher](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831495(v%3dws.11)>)<br>[Bei Offlinedateien Neuigkeiten](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff183315(v=ws.10)>) (Windows 7 und Windows Server 2008 R2)<br>[What's New in Offlinedateien für Windows Vista](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc749449(v=ws.10)>)<br>[Änderungen an Offlinedateien in Windows Vista](<https://technet.microsoft.com/library/2007.11.offline.aspx>) (TechNet Magazine)|
|Bereitstellung|[Bereitstellen von Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](deploy-folder-redirection.md)<br>[Implementieren eine Lösung für die Endbenutzerdatenzentralisierung: Ordnerumleitung und Offlinedateien-Technologie-Validierung und Bereitstellung](http://download.microsoft.com/download/3/0/1/3019A3DA-2F41-4F2D-BBC9-A6D24C4C68C4/Implementing%20an%20End-User%20Data%20Centralization%20Solution.docx)<br>[Verwalten von Roamingbenutzerdaten Bereitstellungshandbuch](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc766489(v=ws.10)>)<br>[Schrittweise Anleitung: Konfigurieren von neuen Offlinedateifunktionen für Windows 7-Computer](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff633429(v=ws.10)>)<br>[Ordnerumleitung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753996(v=ws.11)>)<br>[Implementieren der Ordnerumleitung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc737434(v=ws.10)>) (WindowsServer 2003)|
|Tools und Einstellungen|[Offlinedateien auf MSDN](https://msdn.microsoft.com/library/cc296092.aspx)<br>[Offline-Gruppenrichtlinienreferenz](https://msdn.microsoft.com/library/ms878937.aspx) (Windows 2000)|
|Communityressourcen|["Dateidienste" und "Storage-Forum](https://social.technet.microsoft.com/forums/windowsserver/home?forum=winserverfiles)<br>[Hey, Scripting Guy! Wie kann ich mit dem Feature "Offlinedateien" in Windows arbeiten?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>)<br>[Hey, Scripting Guy! Wie kann ich deaktivieren Offlinedateien und aktivieren?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>)|
Verwandte Technologien|[Identität und Zugriff in WindowsServer](../../identity/identity-and-access.md)<br>[Speicher in WindowsServer](../storage.md)<br>[Remote Access und Server-Verwaltung](../../remote/index.md)|