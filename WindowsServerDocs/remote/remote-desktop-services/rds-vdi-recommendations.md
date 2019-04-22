---
title: Empfohlene Konfiguration für VDI-desktops
description: Empfohlene Einstellungen und Konfiguration der Aufwand für Windows 10 1607 (10.0.1393)-Desktopcomputer als VDI-Abbilder zu minimieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 12/18/2018
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a44dc9f-c221-4bf7-89c3-fb4c86a90f8c
author: jaimeo
manager: dougkim
ms.openlocfilehash: 24704373dedf6a44809b83f3df17bd073cee2bf8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818381"
---
# <a name="recommended-settings-for-vdi-desktops"></a>Empfohlene Einstellungen für VDI-Desktops

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

Microsoft Desktop Virtualization erkennt automatisch, Konfigurationen und netzwerkbedingungen, Benutzer einrichten und Ausführen schneller erhalten durch die Aktivierung der sofortigen Einrichtung von unternehmensanwendungen und Desktops, und es stellt IT-Abteilung den Zugriff auf ältere ermöglichen während der Migration zu Windows 10-Anwendungen.

Obwohl das Betriebssystem Windows 10 sehr gute Leistung standardmäßig optimiert ist, es gibt Möglichkeiten für Sie optimieren, speziell für die unternehmensumgebung von Microsoft Virtual Desktop Infrastructure (VDI) weiter. In der VDI-Umgebung sind viele Diensten im Hintergrund und Aufgaben von Anfang deaktiviert.

Dieses Thema ist nicht an eine Blaupause, aber stattdessen eine Führungslinie oder Ausgangspunkt. Einige Empfehlungen können Funktionen deaktivieren, die Sie verwenden möchten, damit Sie die Kosten im Vergleich zu den Vorteil, dass bestimmte Einstellung in Ihrem Szenario anpassen berücksichtigen sollten.

Diese Anweisungen und die empfohlenen Einstellungen sind für Windows 10 1607 (Version 10.0.1393) relevant.

> [!NOTE]  
> Alle Einstellungen, die nicht ausdrücklich in diesem Thema erwähnten belassen werden ihre Standardwerte (oder pro Ihren Anforderungen und Richtlinien) ohne merkliche Auswirkungen auf die VDI-Funktionalität.

Wenn Sie ein Image auf Basis die VDI-Bereitstellung erstellen, müssen Sie verwenden die **Current Branch**. Weitere Informationen zu Current Branch, finden Sie unter [Windows 10-Versionsinformationen](https://technet.microsoft.com/windows/release-info.aspx).

## <a name="creating-the-windows-10-image"></a>Erstellen des Windows 10-Images
Der erste Schritt besteht darin ein Abbild von Windows 10 1607 (Version 10.0.1393) auf einem physischen oder virtuellen Computer zu installieren. Installation auf einem virtuellen Computer ist einfach und können Sie Versionen der virtuellen Festplatte (VHD) Datei, speichern, für den Fall, dass Sie auf eine frühere Version zurücksetzen möchten.

Während der Installation können Sie wählen, ob **Expresseinstellungen** oder **anpassen**. Die Einstellungen, die während angeboten die **anpassen** Option anpassbar sind, indem Sie mithilfe von Gruppenrichtlinien, sodass die Methode zum Installieren von zugrunde liegendes Betriebssystem nicht wichtig ist.


Wenn Sie ausgewählt haben **anpassen**, Sie können diese Einstellungen anpassen, während der Installation:

## <a name="in-customize-settings"></a>In "Einstellungen anpassen"

Sie können auch diese nach der Installation mit Gruppenrichtlinien-Editor anpassen. finden Sie im Abschnitt "Einstellungen" in diesem Thema.

|Einstellung|Standardwert|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|----------|--------------|
|**Personalisierung**| | |
|Personalisieren Sie Ihre Sprache, die Sie eingeben und Eingabe Freihand, indem Ihre Daten an Microsoft senden.|    Ein| Deaktiviert|
|Eingabe und Freihand-Daten an Microsoft zur Verbesserung der Erkennung und Vorschläge Plattform senden.|  Ein| Deaktiviert|
|Können Sie apps, die Ihre werbungs-ID für die Benutzeroberfläche für apps verwenden.|  Ein| Deaktiviert|
|Lassen Sie Skype (falls installiert), helfen, die Ihnen Verbinden mit Freunden, im Adressbuch, und überprüfen Sie Ihre Mobiltelefonnummer ein. SMS und Daten können anfallen.|    Ein| Deaktiviert|
|**Speicherort**| | |
|Aktivieren Sie suchen, die meine Geräte- und können Windows und apps Ihren Standort, einschließlich standortverlauf anfordern| Ein| Deaktiviert|
|Konnektivität und Fehlerberichterstattung| | |
|„Automatisch eine Verbindung mit vorgeschlagenen öffentlichen Hotspots herstellen“ aktiviert wurde. Nicht alle Netzwerke sind sicher.|    Ein| Deaktiviert|
|Verbinden Sie automatisch, zum Öffnen von Hotspots vorübergehend, um festzustellen, ob es sich bei bezahlt, dass Netzwerkdienste verfügbar sind.| Ein| Deaktiviert|
|Senden Sie vollständige Diagnose- und Nutzungsdaten an Microsoft. Wenn diese Option ausgeschaltet werden nur grundlegende Daten sendet.| Ein| Deaktiviert|
|**Browser, Schutz- und update**| | |
|Verwenden des SmartScreen online services zum Schutz vor schädlichem Inhalt aus und downloads an Standorten, die von Windows-Browser und Store-apps geladen werden|    Ein| Auf (ist kein Zugriff auf das Internet, legen Sie dann auf "aus".)
|Verwenden Sie seitenvorhersage verbessern lesen, zu beschleunigen, durchsuchen, und stellen Sie Ihr Gesamteindruck besser, im Windows-Browser. Ihre Durchsuchen von Daten werden an Microsoft gesendet werden.| Ein| Deaktiviert|
|Abrufen Sie aus und Senden von Updates auf anderen PCs im Internet zur Beschleunigung der app und Windows Update-downloads|   Ein| Deaktiviert|

Sobald die Installation abgeschlossen ist, können Sie weiterhin, beginnend mit Einstellungen anpassen **Windows-Einstellungen**.

## <a name="in-windows-settings"></a>In den Windows-Einstellungen
Um Windows-Einstellungen zuzugreifen, klicken Sie auf **starten** (das Windows-Symbol auf der Taskleiste), und klicken Sie dann auf die **Einstellungen** Symbol (das Zahnradsymbol für eine Form).

### <a name="in-the-system-area-of-windows-settings"></a>Im Bereich "System" der Windows-Einstellungen
Im Bereich "Windows-Einstellungen", auf die **System** Symbol erhalten Sie Zugriff auf eine Reihe von Einstellungen Informationssystem zusammenhängen. Nicht alle von ihnen die Anpassung benötigen für die optimale Verwendung von VDI – diese Einstellungen sind die wichtigsten:

#### <a name="apps-and-features"></a>Apps und features

So entfernen Sie eine app, wodurch sie die Geschäftsregel ausschließen aus Ihrem Image des VDI, klicken Sie auf der app, und klicken Sie dann auf **Deinstallieren**. Wenn **Deinstallieren** ausgegraut, Sie nicht entfernen können von dieser Methode; Sie möglicherweise mit Windows PowerShell entfernen, oder führen diese Schritte aus:
1. Klicken Sie auf **optionale Features verwalten** (direkt unter der **Apps und Features** Überschrift auf der gleichen Seite).
2. Klicken Sie auf die optionale Funktion, und klicken Sie dann auf **Deinstallieren**.

Die folgenden: Features zu entfernen (falls vorhanden) zu berücksichtigen
- **Support kontaktieren**
- **Englisch (Vereinigte Staaten) Retail-Demo-Inhalt**
- **Neutrale Retail-Demo-Inhalt**
- **Schnelle Hilfe**

#### <a name="default-apps"></a>Standard-Apps

In diesem Bereich definiert die app, die standardmäßig für bestimmte generische Funktionen wie E-mail, Browsen im Web und Zuordnungen verwendet werden. Wenn Sie eine andere app für eine bestimmte Funktion verwendet werden soll, klicken Sie auf den aktuellen Eintrag, und klicken Sie dann auf die app, die Sie lieber in der VDI-Abbild verwendet werden. Für eine nicht-Microsoft-app eine verfügbare knotenoption sein installieren Sie die app vor dem Anpassen dieser Einstellung.

#### <a name="notifications-and-actions"></a>Benachrichtigungen und Aktionen

Diese empfohlenen Werte werden Benachrichtigungen und Hintergrund der Netzwerkaktivität in einer VDI-Umgebung reduzieren:

|Einstellung|Standardwert|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|----------|--------------|
|Erhalten von Benachrichtigungen von apps und anderen Absendern| Ein| Deaktiviert|
|Anzeigen von Benachrichtigungen auf dem Sperrbildschirm angezeigt.|    Ein| Deaktiviert|
|Zeigen Sie auf dem Sperrbildschirm Alarme und Erinnerungen eingehende VoIP-Anrufe.|   Ein| Deaktiviert|
|Zeigen Sie Tipps, Tricks und Vorschläge, wie Sie Windows verwenden.|    Ein| Deaktiviert|


#### <a name="offline-maps"></a>Offlinekarten

Diese Einstellung ist nur anwendbar, wenn die Karten-app installiert ist. Der Standardwert ist **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**. 

#### <a name="tablet-mode"></a>Tabletmodus

|Einstellung|Standardwert|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|----------|--------------|
|Wenn die Anmeldung|    Verwenden Sie den entsprechenden Modus für die hardware|   Verwenden des Remotedesktop-Modus|
|Bei diesem Gerät automatisch aktiviert oder deaktiviert gewechselt|    Fragen Sie mich immer vor dem Wechseln| Diese Meldung nicht mehr und nicht zu wechseln.|
|„App-Symbole im Tablet-Modus auf der Taskleiste ausblenden“|  Ein| Deaktiviert|


### <a name="in-the-devices-area-of-windows-settings"></a>Im Bereich "Geräte" der Windows-Einstellungen
Im Bereich "Windows-Einstellungen", auf die **Geräte** Symbol erhalten Sie Zugriff auf eine Reihe von Einstellungen Informationssystem zusammenhängen. Nicht alle von ihnen die Anpassung benötigen für die optimale Verwendung von VDI – diese Einstellungen sind die wichtigsten:

#### <a name="autoplay"></a>Automatische Wiedergabe

|Einstellung|Standardwert|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|----------|--------------|
|Verwenden Sie die automatische Wiedergabe für alle Medien und Geräte|    Ein| Deaktiviert|
|Wechseldatenträger:|Wählen Sie den Standardwert|Keine Aktion durchführen|
|Speicherkarte|Wählen Sie den Standardwert|Keine Aktion durchführen|

### <a name="in-the-personalization-area-of-windows-settings"></a>Im Bereich "Anpassung" der Windows-Einstellungen
Im Bereich "Windows-Einstellungen", auf die **Personalisierung** Symbol erhalten Sie Zugriff auf eine Reihe von Einstellungen Informationssystem zusammenhängen. Nicht alle von ihnen die Anpassung benötigen für die optimale Verwendung von VDI – diese Einstellungen sind die wichtigsten:

#### <a name="background"></a>Hintergrund
Manchmal kann der schwarzen Hintergrund dazu führen, dass Benutzer denken, dass der Computer nicht reagiert. Ändern der Hintergrundfarbe können klarer zu machen. Gehen Sie hierzu folgendermaßen vor:
1. In der **Hintergrund** Bereich, klicken Sie auf das Pulldown-Menü.
2. Um die Farbe des Hintergrunds zu ändern, klicken Sie auf **Volltonfarbe**, und klicken Sie dann auf eine der Farben als Schwarz. Klicken Sie alternativ **Bild** , und wählen Sie ein Bild als Hintergrund verwenden.

#### <a name="start"></a>Beginn

|Einstellung|Standardwert|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|----------|--------------|
|Gelegentlich Vorschläge im Startmenü anzeigen|    Ein| Deaktiviert|
|Anzeigen, die am häufigsten verwendeten apps|Ein|Deaktiviert|
|Anzeigen von zuletzt hinzugefügte apps|Ein|Deaktiviert|
|Zuletzt geöffnete Elemente in Sprunglisten auf Start oder in der Taskleiste anzeigen|Ein|Deaktiviert|

#### <a name="taskbar"></a>Taskleiste
Die Standardeinstellung ist die Verwendung von großen Taskleistenschaltflächen (d. h., ein Wert von "Off" für **verwenden kleine Taskleistenschaltflächen**). Diese Einstellung bewirkt, dass das Cortana-Element, einen Großteil der Bereich der Taskleiste verwenden. Um dies zu vermeiden, legen Sie **verwenden kleine Taskleistenschaltflächen** "Auf". Falls gewünscht, dass Taskleistenelementen größer bleiben, aber nicht von Cortana und verbraucht dabei so viel Speicherplatz der rechten Maustaste auf die Taskleiste haben möchten, zeigen Sie auf **Cortana**, und wählen Sie auf das Menü, das Sie verwendet, **Hidden**.

### <a name="in-the-privacy-area-of-windows-settings"></a>Im Bereich "Datenschutz" der Windows-Einstellungen
Im Bereich "Windows-Einstellungen", auf die **Datenschutz** Symbol erhalten Sie Zugriff auf eine Reihe von Einstellungen Informationssystem zusammenhängen. Nicht alle von ihnen die Anpassung benötigen für die optimale Verwendung von VDI – diese Einstellungen sind die wichtigsten:

#### <a name="general"></a>Allgemein
Einige dieser Einstellungen sind auch im Fenster "Einstellungen anpassen", am Anfang dieses Themas beschrieben festlegen.

|Einstellung|Standardwert|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|----------|--------------|
|Apps, die werbungs-ID für die Umgebungen für apps verwenden können (Wenn diese Option ausgeschaltet wird, Zurücksetzen Ihrer ID)|  Ein| Deaktiviert|
|„Webseiten den Zugriff auf die eigene Sprachliste gestatten, um die Anzeige lokal relevanter Inhalte zu ermöglichen“|Ein|Deaktiviert|
|Let-apps auf meinen Geräten zu anderen apps geöffnet, und Funktionen auf diesem Gerät fortsetzen|Ein|Deaktiviert|

#### <a name="camera"></a>Kamera

Der Standardwert ist "Können apps, die meine Kamera verwenden" **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**.


#### <a name="microphone"></a>Mikrofon

Der Standardwert ist "Können apps das Mikrofon verwenden" **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**.

#### <a name="notifications"></a>Benachrichtigungen

Der Standardwert ist "Können apps, die meine Benachrichtigungen zugreifen" **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**.

#### <a name="contacts"></a>Kontakte

Der Standardwert ist "Können apps, die Kontakte zugreifen" **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**.

#### <a name="calendar"></a>Kalender

Der Standardwert ist "Können apps, die Meine Kalender zugreifen" **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**.

#### <a name="call-history"></a>Anrufliste

Der Standardwert ist "Können apps, die Ihre Anrufliste zugreifen" **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**.

#### <a name="email"></a>E-Mail

Ist der Standardwert für "Können apps den Zugriff auf und Senden von e-Mail-Adresse" **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**.

#### <a name="messaging"></a>Messaging

Der Standardwert für "-apps lesen oder Senden von Nachrichten (" Text "oder" MMS ")" ist **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**.

#### <a name="radios"></a>Funkempfang

Der Standardwert für "apps Steuerelement Radios" ist **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**.

#### <a name="other-devices"></a>Weitere Geräte

Ist der Standardwert für "Können Sie Ihre apps automatisch freigeben und Synchronisieren von Informationen für drahtlose Geräte, die nicht explizit mit Ihrem PC, Tablet oder Telefon gekoppelt sind" **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**.

#### <a name="feedback-and-diagnostics"></a>Feedback und Diagnose

Der Standardwert ist "Windows sollte mein Feedback anfordern" **automatisch**; für die Verwendung von VDI, ist der empfohlene Wert **nie**.

#### <a name="background-apps"></a>Hintergrund-Apps
Aufgeführte apps ist der Standardwert von **auf**, sodass Informationen empfangen, Senden von Benachrichtigungen und Aktualisieren von selbst, ob sie davon verwendet werden. Deaktivieren Sie (Legen Sie auf **aus**) alle apps, die Sie möchten nicht im Hintergrund in der VDI-Image ausgeführt.

### <a name="update-and-security"></a>Update und Sicherheit
#### <a name="windows-update"></a>Windows Update
In der **Aktualisieren der Einstellungen** Bereich, klicken Sie auf **erweiterte Optionen** diese Einstellungen anpassen:

|Einstellung|Standardwert|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|----------|--------------|
|Mir Updates für andere Microsoft-Produkte beim Ausführen von Windows update|    Deaktiviert|    ausgewählt|
|Funktionsupdates zurückstellen|Deaktiviert|ausgewählt|
|Anmeldeinfo verwenden, um die Einrichtung meines Geräts nach einem Update automatisch abzuschließen |Deaktiviert|Hängt von bestimmten VDI-Konfiguration|

Auf der **erweiterte Optionen** auf **wählen, wie Updates übermittelt werden** auf die Einstellung für "Updates von mehr als einem Ort". Der Standardwert ist **auf**; für die VDI-Verwendung, die der empfohlene Wert ist **aus**.

## <a name="in-control-panel-and-other-system-utilities"></a>In der Systemsteuerung und andere Systemdienstprogramme

Die Einstellungen in diesem Abschnitt sind anpassbar, navigieren über die Systemsteuerung oder das Hilfsprogramm nicht direkt öffnen.

> [!NOTE]  
> Alle Einstellungen, die nicht ausdrücklich in diesem Thema erwähnten belassen werden ihre Standardwerte (oder pro Ihren Anforderungen und Richtlinien) ohne merkliche Auswirkungen auf die VDI-Funktionalität.


### <a name="task-scheduler"></a>Aufgabenplanung
Die schnellste Möglichkeit zum Öffnen der Aufgabenplanung ist die Windows-Schaltfläche und geben mithilfe von Push übertragen *Taskplaner* oder *taskschd.msc*. In den Ergebnissen, die zurückgegeben wird, klicken Sie auf **Taskplaner** , öffnen Sie das Hilfsprogramm. Erweitern Sie im Taskplaner **Aufgabenplanungsbibliothek**, erweitern Sie **Microsoft**, und erweitern Sie dann **Windows**. Sie haben jetzt Zugriff auf die Liste von taskauflistungen. Um den Status der einzelnen geplanten Aufgaben zu ändern, Maustaste, und klicken Sie dann auf den gewünschten Zustand (in der Regel **deaktiviert** für die Verwendung von VDI).

|Task-Auflistung|Aufgabenname|Standardstatus|Empfohlene Status für die Verwendung von VDI|  
|-------------------|-------------|----------|--------------|
|Programm zur Verbesserung der Benutzerfreundlichkeit||||
||Consolidator|Enabled|Deaktiviert|
||KernelCeipTask|Enabled|Deaktiviert|
||UsbCeip|Enabled|Deaktiviert|
|Defragmentieren||||
||ScheduledDefrag|Enabled|Deaktiviert|
|Pfad||||
||Benachrichtigungen|Enabled|Deaktiviert|
||WindowsActionDialog|Enabled|Deaktiviert|
|Wartung||||
||WinSAT|Enabled|Deaktiviert|
|Karten||||
||MapsToastTask|Enabled|Deaktiviert|
||MapsUpdateTask|Enabled|Deaktiviert|
|Mobiles Breitband-Konten||||
||MNO Metadatenparser|Enabled|Deaktiviert|
|Energieeffizienzdiagnose||||
||System analysieren|Enabled|Deaktiviert|
|-Wiederherstellungsumgebung||||
||VerifyWinRE|Enabled|Deaktiviert|
|Einzelhandel-Demo||||
||CleanupOfflineContent|Enabled|Deaktiviert|
|Shell||||
||FamilySafetyMonitor|Enabled|Deaktiviert|
||FamilySafetyRefreshTask|Enabled|Deaktiviert|
|Windows-Fehlerberichterstattung||||
||QueueReporting|Enabled|Deaktiviert|
|Gemeinsame Nutzung von Windows-Medien||||
||UpdateLibrary|Enabled|Deaktiviert|

Klicken Sie auf **Windows** erneut um zu reduzieren, klicken Sie dann auf **XblGameSave**. So erhalten Sie Zugriff auf die Aufgaben **XBLGameSaveTask** und **XBLGameSaveTaskLogon**; beide können festgelegt werden, um **deaktiviert**.

### <a name="performance-monitor"></a>Performance Monitor (Leistungsüberwachung)
Die schnellste Möglichkeit, Systemmonitor geöffnet ist, die Windows-Schaltfläche und geben mithilfe von Push übertragen *Systemmonitor* oder *%% amp;quot;Perfmon.msc%%amp;quot;*. In den Ergebnissen, die zurückgegeben wird, klicken Sie auf **Systemmonitor**. Klicken Sie im Windows-Systemmonitor auf **Data Collector Sets** und doppelklicken Sie dann auf **Ereignisablaufverfolgungssitzungen**. Mit der rechten Maustaste **WiFiSession**; ist dies in den Standardzustand des **ausführen**, klicken Sie dann auf **beenden**.

Klicken Sie auf **StartupEventTraceSessions**, klicken Sie dann mit der rechten Maustaste **ReadyBoot**; wenn er ausgeführt wird, klicken Sie auf **beenden**. Klicken Sie auf **Ereignisablaufverfolgungssitzungen**, mit der rechten Maustaste **ReadyBoot**, und klicken Sie dann auf **Eigenschaften**. Klicken Sie in dem nun geöffneten Dialogfeld auf die **Ereignisablaufverfolgungs-Sitzung** Registerkarte. Deaktivieren der **aktiviert** Kontrollkästchen.

### <a name="services"></a>Dienste
Die schnellste Möglichkeit zum Verwalten von Diensten wird die Windows-Schaltfläche und geben *Services*. In den Ergebnissen, die zurückgegeben wird, klicken Sie auf **Services**. Die folgenden Dienste sind gute Kandidaten für die Verwendung in VDI-Szenarien zu deaktivieren. Allerdings müssen Sie Sie einige Tests durchführen, um sicherzustellen, dass sie für Ihre Zwecke benötigt werden. So deaktivieren Sie einen Dienst in der **Services** -Snap-in, mit der rechten Maustaste in des Dienstnamens, und klicken Sie dann auf **Eigenschaften**. Auf der **allgemeine** Registerkarte, klicken Sie auf die **Starttyp** Pulldown-Menü, und klicken Sie dann auf **deaktiviert**. Klicken Sie auf **OK**.

- BranchCache
- Übermittlungsoptimierung
- Diagnose-Diensthost
- Windows Mobile-Hotspot-Dienst
- Xbox Live Auth Manager
- Xbox Live-Spiel speichern
- Xbox Live-Netzwerk-Dienst

### <a name="file-explorer-options"></a>Datei-Explorer-Optionen
Drücken Sie die Windows-Schaltfläche und geben *Systemsteuerung*. In den Ergebnissen, die zurückgegeben wird, klicken Sie auf **Systemsteuerung**. Klicken Sie in der Systemsteuerung auf **File Explorer Options**. Klicken Sie in dem nun geöffneten Dialogfeld auf die **Suche** Registerkarte, und klicken Sie dann in der **bei der Suche nicht indizierten Orten** Bereich deaktivieren das Kontrollkästchen für **"Include"-Verzeichnissen von System**. Klicken Sie auf **OK** zu speichern.

### <a name="flash-settings"></a>Flash-Einstellungen
Drücken Sie die Windows-Schaltfläche und geben *Systemsteuerung*. In den Ergebnissen, die zurückgegeben wird, klicken Sie auf **Systemsteuerung**. Klicken Sie in der Systemsteuerung auf **Flash Player** Flash Player Settings Manager zu öffnen. Auf der **Storage** Registerkarte, wählen Sie das Optionsfeld für **Blockieren von allen Standorten über das Speichern von Informationen auf diesem Computer**. Klicken Sie in dem nun geöffneten Dialogfeld auf **OK**.

Auf der **Kamera und Mikrofon** Registerkarte die **Kamera und Mikrofon Einstellungen** wählen Sie im Bereich das Optionsfeld für **blockieren alle Standorte, von der Verwendung der Kamera und Mikrofon**.

Auf der **Wiedergabe** Registerkarte die **Peer-gestützten Netzwerke** wählen Sie im Bereich das Optionsfeld für **blockieren alle Standorte, von der Verwendung von Peer-gestützten Netzwerke**. Flash Player Settings Manager zu schließen.

### <a name="internet-options"></a>Internetoptionen
Drücken Sie die Windows-Schaltfläche und geben *Systemsteuerung*. In den Ergebnissen, die zurückgegeben wird, klicken Sie auf **Systemsteuerung**. Klicken Sie in der Systemsteuerung auf **Internetoptionen** um Internet-Eigenschaften zu öffnen. In der **Startseite** Bereich, geben Sie die URL für die Website, die Benutzern als Startseite im Browser angezeigt werden sollen. Dies ist möglicherweise eine Website für Ihr Unternehmen oder Sie können es auf eine leere Startseite festlegen, durch Eingabe *zu: leere*.

In der **Browserverlauf** wählen Sie im Bereich das Kontrollkästchen für **Löschen des Browserverlaufs beim Beenden**.

### <a name="power-options"></a>Energieoptionen
Drücken Sie die Windows-Schaltfläche und geben *Systemsteuerung*. In den Ergebnissen, die zurückgegeben wird, klicken Sie auf **Systemsteuerung**. Klicken Sie in der Systemsteuerung auf **Energieoptionen** die Systemsteuerung Energieoptionen zu öffnen. In der **auswählen oder Anpassen ein Energiesparplans** Bereich, klicken Sie auf den Pfeil nach unten **zusätzliche Pläne anzeigen**, und wählen Sie dann auf das Optionsfeld für **hohe Leistung**. Diese Einstellung hat kaum Auswirkungen auf dem VDI-Host.

### <a name="system"></a>System
Drücken Sie die Windows-Schaltfläche und geben *Systemsteuerung*. In den Ergebnissen, die zurückgegeben wird, klicken Sie auf **Systemsteuerung**. Klicken Sie in der Systemsteuerung auf **System** um die Systemsteuerung zu öffnen. Klicken Sie im linken Bereich auf **Erweiterte Systemeinstellungen**. Klicken Sie in dem nun geöffneten Dialogfeld auf die **erweitert** Registerkarte. In der **Leistung** Bereich, klicken Sie auf der **Einstellungen** Schaltfläche, klicken Sie dann auf **visuelle Effekte** Registerkarte im Dialogfeld, das geöffnet wird, wählen die **passen Sie für eine optimale Leistung**  Optionsfeld. Klicken Sie auf **OK** zum Speichern und beenden.

## <a name="group-policy-settings"></a>Gruppenrichtlinieneinstellungen

Drücken Sie zum Bearbeiten der gruppenrichtlinieneinstellungen, die Windows-Schaltfläche und geben *Gruppenrichtlinie* oder *"Gpedit.msc"*. In den Ergebnissen, die zurückgegeben wird, klicken Sie auf **Gruppenrichtlinien bearbeiten** zum Editor für lokale Gruppenrichtlinien zu öffnen.

> [!NOTE]  
> Alle Einstellungen, die nicht ausdrücklich in diesem Thema erwähnten belassen werden ihre Standardwerte (oder pro Ihren Anforderungen und Richtlinien) ohne merkliche Auswirkungen auf die VDI-Funktionalität.

Klicken Sie unter **Computerkonfiguration**, erweitern Sie **Windows-Einstellungen**, und erweitern Sie dann **Sicherheitseinstellungen**. Klicken Sie auf **Netzwerklisten-Manager-Richtlinien**, und doppelklicken Sie dann auf **alle Netzwerke**. Das Dialogfeld, das geöffnet, im wird dem **Netzwerkadresse** wählen Sie im Bereich das Optionsfeld für **Benutzer Speicherort kann nicht geändert werden**. Klicken Sie auf die **OK** zu speichern.

Reduzieren **Windows-Einstellungen**, und erweitern Sie dann **Administrative Vorlagen**. Klicken Sie auf, oder Erweitern Sie **Netzwerk**, und passen Sie dann auf jede Einstellung wie folgt durch Doppelklick, und klicken Sie dann das Optionsfeld für den angegebenen Wert und durch Klicken auf die **OK** Schaltfläche:

|Bereich festlegen|Einstellung|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|-------|----------|
|BITS (Background Intelligent Transfer Service, Intelligenter Hintergrundübertragungsdienst)|||
||Lassen Sie den BITS-Client mit Windows BranchCache nicht zu|Enabled|
||Lassen Sie sich nicht auf den Computer fungieren als Client BITS-Peercaching|Enabled|
||Lassen Sie sich nicht auf den Computer als einen BITS-Peercaching server|Enabled|
||Zulassen von BITS-Peercaching|Deaktiviert|
|BranchCache||
||BranchCache aktivieren|Deaktiviert|
|Hotspot-Authentifizierung||
||Hotspot-Authentifizierung aktivieren|Deaktiviert|
|Microsoft-Peer-zu-Peer-Netzwerkdienste||
||Deaktivieren Sie Netzwerkdienste von Microsoft-Peer-zu-Peer|Enabled|
|Offlinedateien||
||Zulassen bzw. nicht zulassen von Offlinedateien-Funktion|Deaktiviert|

Reduzieren **Netzwerk**, und erweitern Sie dann **System**. Passen Sie jede Einstellung wie folgt darauf doppelklicken, und klicken Sie dann das Optionsfeld für den angegebenen Wert und durch Klicken auf die **OK** Schaltfläche:

|Bereich festlegen|Einstellung|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|----------|--------------|
|Geräteinstallation||
||Ein Windows-Fehlerbericht nicht gesendet, wenn ein generischer Treiber auf einem Gerät installiert ist|Enabled|
||Verhindern der Erstellung eines Systemwiederherstellungspunkts während der Geräteaktivität, die normalerweise die Erstellung eines Wiederherstellungspunkts aufgefordert wird|Enabled|
||Gerät Abrufen von Metadaten aus dem Internet zu verhindern, dass|Enabled|
||Verhindern Sie, dass Windows Senden eines Fehlerberichts, wenn ein Gerätetreiber Anforderungen zusätzliche Software während der installation|Enabled|
||Deaktivieren Sie "Neue Hardware gefunden" Sprechblasen während der Geräteinstallation|Enabled|

Erweitern Sie **Filesystem**, doppelklicken Sie auf **NTFS**, doppelklicken Sie auf **kurze Namen Erstellungsoptionen**, wählen Sie das Optionsfeld für **aktiviert**, und dann die **Optionen** Pulldown-Menü auswählen **aktivieren Sie auf alle Volumes**. Klicken Sie auf die **OK** zu speichern.

Reduzieren **Filesystem**, und erweitern Sie dann **Internetkommunikationsverwaltung**. Klicken Sie auf **internetkommunikationseinstellungen**. Passen Sie jede Einstellung wie folgt durch Doppelklick aus, und wählen das Optionsfeld für **aktiviert**, und klicken Sie dann auf die **OK** Schaltfläche:

- Deaktivieren Sie die Ereignisanzeige "Events.asp" links
- Daten mit handschriftanpassung deaktivieren
- Handschrifterkennungs-Fehlerberichterstattung deaktivieren
- Deaktivieren Sie Hilfe- und Supportcenter "Wussten Sie schon?" content
- Hilfe und Support Center Microsoft Knowledge Base-Suche deaktivieren
- Verbindungs-Assistenten deaktivieren Sie, wenn sich die URL-Verbindung auf Microsoft.com bezieht
- Internet-Download für die Veröffentlichung und onlinebestellung von Abzügen deaktivieren
- Internet-Dateizuordnungdienst deaktivieren
- Registrierung deaktivieren Sie, wenn sich die URL-Verbindung auf Microsoft.com bezieht
- Die Bild-Aufgabe "Abzüge online bestellen" deaktivieren
- Aufgabe "Web veröffentlichen" für Dateien und Ordner deaktivieren
- Deaktivieren der Windows Messenger Customer Experience Improvement Program
- Deaktivieren Sie Windows Customer Experience Improvement Program
- Windows-Fehlerberichterstattung deaktivieren
- Suche nach Gerätetreibern auf Windows Update deaktivieren

Klicken Sie auf **Energieverwaltung** und doppelklicken Sie dann auf **wählen Sie einen aktiven Energiesparplan**. Wählen Sie das Optionsfeld für **aktiviert**, und verwenden Sie dann die **Optionen** Pulldown-Menü auswählen **hohe Leistung**. Klicken Sie auf die **OK** zu speichern.

Klicken Sie auf **Recovery**, und doppelklicken Sie dann auf **ermöglichen die Wiederherstellung des Systems auf Standardstatus**. Wählen Sie das Optionsfeld für **aktiviert**, und klicken Sie dann auf die **OK** zu speichern.

Erweitern Sie **Problembehandlung und Diagnose**. Klicken Sie auf **geplante Wartung**, doppelklicken Sie auf **geplante Wartung Verhalten konfigurieren**, und wählen Sie dann auf das Optionsfeld für **deaktiviert**. Klicken Sie auf die **OK** zu speichern.

Für jeden der folgenden Bereiche für die Einstellungen, klicken Sie darauf, und doppelklicken Sie dann **Szenario Ausführungsebene konfigurieren**, wählen Sie das Optionsfeld für **deaktiviert**, und klicken Sie dann auf die **OK**aus, um speichern:

- Windows Boot Performance Diagnostics
- Windows-Speicherdiagnose Speicherverlusten
- Windows-Ressourcenauslastungserkennung und Auflösung
- Windows-Herunterfahr-Leistungsdiagnose
- Windows/Resume-Standby-Leistungsdiagnose
- Windows System Reaktionsfähigkeit Leistungsdiagnose

Reduzieren **System**, und erweitern Sie dann **Windows-Komponenten**. Passen Sie jede Einstellung wie folgt durch Doppelklick, und klicken Sie dann das Optionsfeld für den angegebenen Wert und durch Klicken auf die **OK** Schaltfläche:

|Bereich festlegen|Einstellung|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|-------|----------|
|Hinzufügen von Funktionen zu Windows 10|||
||Verhindern, dass der Assistent ausgeführt wird|Enabled|
|Richtlinien für die automatische Wiedergabe|||
||Legen Sie das Standardverhalten für AutoRun|Verwenden Sie dann aktiviert, die **Optionen** Pulldown-Menü auswählen **Autorun Befehle nicht ausgeführt**|
|Cloud-Inhalten|||
||Windows-Tipps nicht mehr anzeigen|Enabled|
||Microsoft-Anwenderfeatures deaktivieren|Enabled|
|Die Datensammlung und Vorschau-Builds|||
||Telemetrie zulassen|Verwenden Sie dann aktiviert, die **Optionen** Pulldown-Menü auswählen **1: Basis**|
||Pre-Release-Features oder -Einstellungen deaktivieren|     Deaktiviert|
||Feedbackbenachrichtigungen nicht mehr anzeigen|       Enabled|
||Benutzersteuerung für Insider-Builds umstellen|      Deaktiviert|
|Desktopfenster-Manager|||
||Flip3D Aufruf nicht zulassen|       Enabled|
||Fensteranimationen nicht zulassen|       Enabled|
||Verwenden Sie die Volltonfarbe für Start-Hintergrund|     Enabled|
|Edge-Benutzeroberfläche|||
||Edge-Wischen zulassen|     Deaktiviert|
||Deaktivieren Sie die Hilfe-Tipps|        Enabled|
|Datei-Explorer|||
||Die Benachrichtigung "neue Anwendung installiert" nicht mehr anzeigen|     Enabled|
|Spiel-Explorer|||
||Download von Spiel deaktivieren|     Enabled|
||Spiele-Updates deaktivieren|        Enabled|
||Nachverfolgung der Zeitpunkt der letzten Play Spiele im Ordner "Spiele" deaktivieren|     Enabled|
|„Heimnetzgruppe“|||
||Beitritt des Computers zu einer Heimnetzgruppe verhindern|        Enabled|
|Internet Explorer|||
||Für Microsoft-Dienste das Bereitstellen von erweiterten Vorschlägen zulassen, wenn Benutzer Text in die Adressleiste eingeben|        Deaktiviert|
||Periodische Überprüfungen auf Internet Explorer-Softwareupdates deaktivieren|        Enabled|
||Deaktivieren der Anzeige des Begrüßungsbildschirms|        Enabled|
||Automatisch neue Versionen von Internet Explorer installieren|      Deaktiviert|
||Verhindern Sie die Teilnahme am Programm zur Verbesserung der Benutzerfreundlichkeit|     Enabled|
||Verhindern, dass ausgeführte Anpassungs-Assistent wechseln Sie direkt zur Homepage|   Verwenden Sie dann aktiviert, die **Optionen** Pulldown-Menü auswählen **direkt zur Homepage wechseln**|
||Legen Sie die Registerkarte Prozess Wachstum|Aktiviert ist, geben Sie Folgendes in die **Registerkarte Prozess Wachstum** Feld: *Niedrig*.|
||Geben Sie Standardverhalten für eine neue Registerkarte|Verwenden Sie dann aktiviert, die **Optionen** Pulldown-Menü auswählen **neue Registerkarte**|
||Benachrichtigungen zur Add-On-Leistung deaktivieren|        Enabled|
||Browser-Geolocation deaktivieren|     Enabled|
||Deaktivieren Sie letzte Browsersitzung erneut öffnen|        Enabled|
||Vorschläge für alle Benutzer installierten Anbieter deaktivieren|        Enabled|
||Aktivieren Sie die vorgeschlagenen Standort|       Deaktiviert|

Auf der gleichen Ebene wie die **Internet Explorer** Einstellungen, die Sie gerade in der obigen Tabelle angepasst Beachten Sie im Bereich von einer anderen Ordnerebene **Accelerators** zu **Symbolleisten**. Das heißt, Sie befinden sich jetzt Richtlinien für Lokaler Computer > Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Internet Explorer. 

Öffnen der **Browserverlauf löschen** Ordner doppelklicken Sie auf **das Löschen des Browserverlaufs beim Beenden**Option **aktivieren**, und klicken Sie dann auf **OK**zum Speichern und beenden.

Verwenden Sie der Rückwärtspfeil oben des Editors für lokale Gruppenrichtlinien Links zu zurückkehren der **Internet Explorer** Ebene. Doppelklicken Sie auf **Interneteinstellungen**, doppelklicken Sie auf **Erweiterte Einstellungen**, und passen Sie die Einstellungen in den Unterordnern wie folgt:

|Ordner "Einstellung" unter **Erweiterte Einstellungen**|Einstellung|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|-------|----------|
|**Durchsuchen**|||
||Finden von Telefonnummern deaktivieren|Enabled|
|**Multimedia**|||
||Erlauben Sie Internet Explorer zum Wiedergeben von Mediendateien, die andere Codecs verwenden|Deaktiviert|

Wechseln Sie zurück bis zur Ebene **Internet Explorer**, doppelklicken Sie dann auf **Interneteinstellungen**. In diesem Ordner legen Sie diese beiden Einstellungen unter **AutoVervollständigen** zu **aktiviert**:

- Vorschlagen von URLs ausschalten
- Windows Search-AutoVervollständigen deaktivieren

Sichern Sie die vier Ebenen, wechseln Sie **Windows-Komponenten**, doppelklicken Sie auf **Speicherort und Sensoren**, und legen Sie diese drei Einstellungen auf **aktiviert** (für jeden, klicken Sie auf  **OK** zum Speichern und beenden):

- Deaktivieren Sie Speicherort
- Deaktivieren Sie die Speicherort-Skripterstellung
- Deaktivieren von Sensoren

Während auf der Ebene der **Speicherort und Sensoren**, doppelklicken Sie auf **Windows Ortungsanbieter** und legen Sie **Deaktivieren der Windows-Location-Anbieters** zu **aktiviert**. Klicken Sie auf **OK** zum Speichern und beenden.

Klicken Sie im linken Bereich auf **Maps**, legen Sie diese Einstellungen auf **aktiviert**; und klicken Sie dann **OK** zum Speichern und beenden:

- Turn off Automatic Download and Update of Map Data
- Nicht angeforderten Netzwerk-Datenverkehr auf der Einstellungsseite „Offlinekarten“ deaktivieren

Verwenden im linken Bereich ein, geben Sie die folgenden Einstellungen für Unterordner, und passen Sie die einzelnen Einstellungen wie folgt:

|Ordner "Einstellungen" unter **Windows-Komponenten**|Einstellung|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|-------|----------|
|**OneDrive**|||
||Verwendung von OneDrive zum Speichern von Daten verhindern|Enabled|
||Speichern von Dokumenten auf OneDrive standardmäßig|Deaktiviert|
|**RSS-Feeds**|||
||Verhindert die automatische Ermittlung von Feeds und Web Slices|Enabled|
|**Suche**|||
||Cortana zulassen|        Deaktiviert|
||Cortana über Sperrbildschirm zulassen|      Deaktiviert|
||Der Suche und Cortana die Nutzung von Positionsdaten erlauben|     Deaktiviert|
||Websuche nicht zulassen|      Enabled|
||Nicht im Web suchen oder Webergebnisse in der Suche anzeigen|        Enabled|
||Hinzufügen von UNC zu verhindern, dass Standorte in der Systemsteuerung zu indizieren|     Enabled|
||Zu verhindern, dass die Indizierung von Dateien im Cache für Offlinedateien|        Enabled|
|**Store**|||
||Deaktivieren Sie das Angebot auf die neueste Version von Windows aktualisieren|Enabled|
|**Windows-Fehlerberichterstattung**|||
||Senden Sie Speicherabbilder für OS generierter Fehlerberichte automatisch|       Deaktiviert|
||Deaktivieren der Windows-Fehlerberichterstattung|      Enabled|
|**Windows Installer**|||
||Steuerelement maximale Größe des Baseline-Datei-cache|  Aktiviert ist, klicken Sie dann die Drehfeldeinheit im Verwenden der **Optionen** Bereich festlegen **maximale Größe der Baseline Cache** zu *5*.|
||Erstellung von Prüfpunkten Systemwiederherstellung deaktivieren|      Enabled|
|**Windows Mail**|||
||Deaktivieren Sie die Communitys-Funktion|Enabled|
|**Windows Media Player**|||
||Erste Verwenden von Dialogfeldern nicht mehr anzeigen|       Enabled|
||Verhindern Sie die Freigabe von Medien|        Enabled|
|**Windows Mobility Center**|||
||Deaktivieren Sie Windows-Mobilitätscenter|Enabled|
|**Analyse der Windows-Zuverlässigkeit**|||
||Konfigurieren Sie die Zuverlässigkeit von WMI-Anbieter|Deaktiviert|
|**Windows Update**|||
||Sofortige Installation von Automatische Updates zulassen|       Enabled|
||Entfernen Sie den Zugriff auf alle Windows Update-Funktionen|     Enabled|
|In der **Windows Update** Ordner **zurückstellen von Windows Update**|||
||Wählen Sie beim Empfang von Featureupdates|Aktiviert ist, klicken Sie dann in der **Optionen** Bereich der **wählen Sie die Branch-Bereitschaftsniveau für die Feature-Updates, die Sie empfangen möchten** Pulldown-Menü auswählen **Current Branch for Business**. Legen Sie die **nach der Veröffentlichung eines Featureupdates zurückgestellt es für die folgende Anzahl von Tagen** Drehfeldeinheit zu *180 Tage*.
||Wählen Sie beim Empfang von Qualitätsupdates|Aktiviert ist, klicken Sie dann in der **Optionen** legen Sie im Bereich der **nach der Veröffentlichung wird ein qualitätsupdate zurückstellen für folgende Anzahl von Tagen erhalten** Drehfeldeinheit zu *30 Tage* , und wählen Sie das Kontrollkästchen für **Qualitätsupdates**.

Klicken Sie im linken Bereich des Editors für lokale Gruppenrichtlinien auf **Benutzerkonfiguration**. Klicken Sie im linken Bereich mit **Administrative Vorlagen** und geben Sie die folgenden Einstellungen für Unterordner, und passen Sie die einzelnen Einstellungen wie folgt:

|Ordner "Einstellungen" unter **Administrative Vorlagen**|Einstellung|Empfohlene Wert für die Verwendung von VDI|  
|-------------------|-------|----------|
|**Desktop**|||
||Fügen Sie keine Freigaben der zuletzt geöffneten Dokumente zu Netzwerkspeicherorten|Enabled|
|In der **Desktop** Ordner **Active Directory**|||
||Maximale Größe der Active Directory-Suche|Aktiviert ist, klicken Sie dann in der **Optionen** Bereich mit der Drehfeldeinheit fest **Anzahl der zurückgegebenen Objekte** zu *5000*.|
|**Starten Sie Manu und auf der Taskleiste**|||
||Deaktivieren Sie die aktuelle Liste der Programme für neue Benutzer|     Enabled|
||Keine Elemente in Sprunglisten von Remotestandorten anzeigen oder nachverfolgen|        Enabled|
||Feature-Ankündigung via Sprechblasenbenachrichtigungen deaktivieren|     Enabled|
||Benutzer deaktivieren|       Enabled|
|In der **Taskleiste und Startmenü** Ordner **Benachrichtigungen**|||
||Popupbenachrichtigungen deaktivieren|Enabled|
|In der **Windows-Komponenten** Ordner geöffnet:|||
|**Cloud-Inhalten**|||
||Features von Windows-Blickpunkt deaktivieren|Enabled|
|**Datei-Explorer**|||
||Deaktivieren Sie die Zwischenspeicherung von Miniaturansichten von Bildern|       Enabled|
||Anzeige des zuletzt verwendete Suchbegriffe in der Datei-Explorer-Suchfeld deaktivieren|        Enabled|
||Deaktivieren Sie das Zwischenspeichern von Miniaturansichten in ausgeblendeten thumbs.db-Datei|      Enabled|

## <a name="microsoft-store-apps"></a>Microsoft Store-Apps
Es gibt eine Anzahl von Microsoft Store-apps, die Sie aus dem Image des VDI entfernen möchten. entfernt werden wird die CPU-Auslastung verringern und Speicherplatz sparen. Gute Kandidaten für die Entfernung gehören:

- Office abrufen
- Skype (Vorschau)
- Erste Schritte (insbesondere, wenn es keine Internetverbindung ist)
- Feedback-Hub
- Microsoft Solitaire-Auflistung
- Kostenpflichtige WLAN- und VPN-Mobiltelefon

Verwenden Sie zum Anpassen des Standard-Benutzerprofils, das zum Erstellen von VDI-Abbilder verwendet das integrierte Administratorkonto ein. Wenn sie nicht bereits aktiviert ist, dazu verwenden lokale Benutzer und Gruppen in der Computerverwaltung werden. Klicken Sie dann melden Sie sich bei dem Administratorkonto an, die folgenden Schritte ausführen.

> [!NOTE]  
> Entfernen Sie keine System-apps wie die Store-app. Sie sind schwer zu installieren. Andere apps sind einfach reinstallable, aus dem Store.

### <a name="delete-unwanted-apps-from-the-administrator-user-profile"></a>Löschen Sie unerwünschte apps aus dem Profil der Benutzer Administrator
1. Führen Sie in Windows PowerShell `Get-AppxPackage | ft PackageFamilyName` um die Liste der installierten apps anzuzeigen.
2. Führen Sie für jede app-Objekt-Manager, die Sie deinstallieren möchten Cmdlets dieses Beispiel-Format ein:

    `Get-AppxPackage *messaging* | Remove-AppxPackage`

    `Get-AppxPackage *WindowsMaps* | Remove-AppxPackage`

    `Get-AppxPackage *ZuneMusic* | Remove-AppxPackage`

### <a name="delete-the-payload-of-unwanted-store-apps"></a>Löschen Sie die Nutzlast von unerwünschten Store-apps
Dadurch wird verhindert, dass die apps neu installiert wird.
1. Liste von Store-apps und andere Elemente, die Daten im Speicher mit diesem Cmdlet bereitgestellt haben: `Get-AppxProvisionedPackage -Online`.
2. Entfernen Sie ein Paket mit `Remove-AppxProvisionedPackage -Online -PackageName MyAppPackage`, mit der entsprechenden MyAppPackage aus Schritt 1 zurückgegeben. Z. B., um das Paket Zune-bezogene zu entfernen, Sie würden ausführen `Remove-AppxProvisionedPackage -Online -PackageName Microsoft.ZuneMusic_2019.17012.10311.0_neutral_~_8wekyb3d8bbwe`.

## <a name="removing-other-items"></a>Entfernen von anderen Elementen
Sie können die OneDrive-Symbol und die app zu entfernen, Systemsymbole deaktivieren und löschen die heruntergeladenen Updates.

### <a name="remove-onedrive-icon-and-app"></a>OneDrive-Symbol und die app entfernen
1. Klicken Sie auf **starten** und einen Bildlauf zu der **OneDrive** Symbol.
2. Mit der rechten Maustaste die **OneDrive** Symbol, zeigen Sie auf **weitere**, und klicken Sie dann auf **Dateispeicherort öffnen**.
3. Mit der rechten Maustaste die **OneDrive** in der Dateispeicherort, und klicken Sie auf **löschen**.

So entfernen Sie die OneDrive-app:
1. Klicken Sie auf **starten** und einen Bildlauf zu der **OneDrive** Symbol.
2. Mit der rechten Maustaste die **OneDrive** Symbol, und klicken Sie dann auf **Deinstallieren**. Programme und Features wird geöffnet.
3. Programme und Funktionen, mit der Maustaste **Microsoft OneDrive** , und klicken Sie auf **Deinstallieren**.

### <a name="programs-and-features-from-previous-versions-of-control-panel"></a>Programme und Funktionen (aus früheren Versionen der Systemsteuerung)
1. Mithilfe von Push übertragen die **starten** , geben *Steuerelement*, und drücken Sie dann die EINGABETASTE.
2. Tippen Sie auf, oder doppelklicken Sie auf **Programme und Funktionen**.
3. Ganz links unter **Startseite der Systemsteuerung**tippen oder klicken Sie auf **Aktivieren von Windows-Funktionen ein- oder ausschalten**. Eine neue Benutzeroberfläche wird geöffnet.
4. Deaktivieren Sie die Kontrollkästchen für alle Elemente, die Sie nicht möchten oder müssen im Basisimage, z.B.: **SMB 1.0/CIFS-Datei, Unterstützung von Freigaben**.

### <a name="turn-system-icons-off"></a>Deaktivieren Sie Systemsymbole
1. Mithilfe von Push übertragen, oder klicken Sie auf **starten**, und klicken Sie dann auf **Einstellungen** (das Zahnradsymbol).
2. In der **Einstellung suchen** Textbereich, der Typ *Taskleiste*, und klicken Sie dann auf **Einstellungen der Taskleiste**.
3. Unter den **Taskleiste** Abschnitt, scrollen oder navigieren Sie nach unten zu den **Infobereich** Abschnitt.
4. Klicken oder tippen Sie auf **aktivieren oder Deaktivieren von Systemsymbole**, und aktivieren Sie jedes Systemsymbol aktiviert oder deaktiviert ein, wie Sie für das Image verwenden möchten.

### <a name="delete-downloaded-updates"></a>Löschen Sie die heruntergeladenen updates
1. Navigieren Sie mit der Datei-Explorer zu **C:\Windows\Software Distribution\Download**.
2. Löschen Sie alle Dateien und Ordner in diesem Verzeichnis.













 













