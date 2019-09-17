---
title: Empfohlene Konfiguration für VDI-Desktops
description: Empfohlene Einstellungen und Konfiguration zum Minimieren des Mehraufwands für Windows 10 1607 (10.0.1393)-Desktops, die als VDI-Images verwendet werden
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
ms.openlocfilehash: ef13369fa325d136f9e3847db9872a80b650ca37
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70870631"
---
# <a name="recommended-settings-for-vdi-desktops"></a>Empfohlene Einstellungen für VDI-Desktops

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10

Microsoft Desktop Virtualization erkennt automatisch Gerätekonfigurationen und Netzwerkbedingungen, damit Benutzer schneller durchstarten können, indem ihnen die sofortige Einrichtung von Unternehmensanwendungen und -desktops ermöglicht wird. Außerdem rüstet sie die IT aus, damit sie während der Migration zu Windows 10 Zugriff auf ältere Anwendungen hat.

Obwohl das Betriebssystem Windows 10 sehr gut vorkonfiguriert ist, gibt es für Sie Möglichkeiten, es für die Microsoft Virtual Desktop Infrastructure-Umgebung (VDI-Umgebung) speziell weiter zu verfeinern. In der VDI-Umgebung sind viele Dienste und Aufgaben im Hintergrund von Anfang deaktiviert.

Dieses Thema ist keine Blaupause, sondern eher ein Leitfaden oder ein Ausgangspunkt. Durch einige Empfehlungen wird die Funktionalität, die Sie gerne nutzen möchten, möglicherweise deaktiviert. Deshalb sollten Sie die Kosten im Vergleich zum Vorteil der Anpassung einer bestimmten Einstellung in Ihrem Szenario jeweils überlegen.

Diese Anweisungen und empfohlenen Einstellungen sind für Windows 10 1607 (Version 10.0.1393) relevant.

> [!NOTE]  
> Bei allen Einstellungen, die in diesem Thema nicht ausdrücklich erwähnt werden, können die Standardwerte beibehalten (oder Werte entsprechend Ihren Anforderungen und Richtlinien festgelegt) werden. Dies hat keine spürbare Auswirkung auf die VDI-Funktionalität.

Wenn Sie ein Image als Basis für die VDI-Bereitstellung erstellen, verwenden Sie dafür unbedingt den **Current Branch**. Weitere Informationen zu Current Branch finden Sie unter [Windows 10-Versionsinformationen](https://technet.microsoft.com/windows/release-info.aspx).

## <a name="creating-the-windows-10-image"></a>Erstellen des Windows 10-Images
Der erste Schritt besteht darin, ein Referenzimage von Windows 10 1607 (Version 10.0.1393) auf einem physischen oder virtuellen Computer zu installieren. Die Installation auf einem virtuellen Computer ist einfach und ermöglicht es Ihnen, Versionen der VHD-Datei (Virtual Hard-Disk, virtuelle Festplatte) für den Fall zu speichern, dass Sie Ihre Version auf eine frühere zurücksetzen möchten.

Während der Installation können Sie zwischen **Expresseinstellungen** und **Anpassen** auswählen. Weil die im Rahmen der Option **Anpassen** angebotenen Einstellungen über die Gruppenrichtlinie angepasst werden können, ist die Installationsmethode für das Basisbetriebssystem nicht wichtig.


Wenn Sie **Anpassen** ausgewählt haben, können Sie während der Installation diese Einstellungen anpassen:

## <a name="in-customize-settings"></a>In „Einstellungen anpassen“

Sie können diese Einstellungen auch noch nach der Installation mit dem Gruppenrichtlinien-Editor anpassen; lesen Sie dazu den Abschnitt „Gruppenrichtlinieneinstellungen“ in diesem Thema.

|Einstellung|Standardwert|Empfohlener Wert für VDI-Verwendung|  
|-------------------|----------|--------------|
|**Personalisierung**| | |
|Spracherkennung, Eingabe und Freihand personalisieren, indem Ihre Eingabedaten an Microsoft übermittelt werden.|    Ein| Deaktiviert|
|Eingabe- und Freihanddaten an Microsoft senden, um die Plattform für Spracherkennung und Vorschläge zu verbessern.|  Ein| Deaktiviert|
|Apps die Verwendung Ihrer Werbe-ID für die App-übergreifende Nutzung erlauben.|  Ein| Deaktiviert|
|Skype (falls installiert) darf Ihnen helfen, sich mit Freunden in Ihrem Adressbuch zu vernetzen, und Ihre Mobiltelefonnummer überprüfen. Es können SMS- und Datengebühren anfallen.|    Ein| Deaktiviert|
|**Speicherort**| | |
|„Mein Gerät suchen“ aktivieren und Windows und Apps die Abfrage Ihrer Positionsdaten (einschließlich Positionsverlauf) erlauben| Ein| Deaktiviert|
|Verbindungs- und Fehlerberichterstattung| | |
|„Automatisch eine Verbindung mit vorgeschlagenen öffentlichen Hotspots herstellen“ aktiviert wurde. Nicht alle Netze sind sicher.|    Ein| Deaktiviert|
|Vorübergehend automatisch eine Verbindung mit öffentlichen Hotspots herstellen, um zu überprüfen, ob kostenpflichtige Netzwerkdienste verfügbar sind.| Ein| Deaktiviert|
|Vollständige Diagnose- und Nutzungsdaten an Microsoft senden. Wenn Sie diese Option deaktivieren, werden nur grundlegende Daten gesendet.| Ein| Deaktiviert|
|**Browser, Schutz und Update**| | |
|SmartScreen-Onlinedienste verwenden, um den PC vor schadhaften Inhalten und Downloads in Websites zu schützen, die von Windows-Browsern und Store-Apps heruntergeladen werden.|    Ein| „Ein“ (wenn es keinen Zugriff auf das Internet gibt, auf „Aus“ festlegen.)
|Nutzt die Seitenvorhersage, um das Browsen zu beschleunigen sowie das Lesen und die gesamte Nutzung von Windows-Browsern zu verbessern. Ihre Browserdaten werden an Microsoft gesendet.| Ein| Deaktiviert|
|Updates auf anderen PCs im Internet hoch- und herunterladen, um Downloads von Apps und Windows-Updates zu beschleunigen.|   Ein| Deaktiviert|

Nach Abschluss der Installation können Sie das Anpassen von Einstellungen fortsetzen und damit bei **Windows-Einstellungen** beginnen.

## <a name="in-windows-settings"></a>In „Windows-Einstellungen“
Klicken Sie für den Zugriff auf „Windows-Einstellungen“ auf **Start** (das Windows-Symbol auf der Taskleiste) und dann auf das Symbol **Einstellungen** (sieht aus wie ein Zahnrad).

### <a name="in-the-system-area-of-windows-settings"></a>Im Bereich „System“ von „Windows-Einstellungen“
Wenn Sie im Bereich „Windows-Einstellungen“ auf das Symbol **System** klicken, erhalten Sie Zugriff auf eine Reihe von systembezogenen Einstellungen. Nicht alle davon müssen für eine optimale VDI-Verwendung angepasst werden. Dies sind die wichtigsten Einstellungen:

#### <a name="apps-and-features"></a>Apps und Features

Wenn Sie eine App entfernen und dadurch aus Ihrem VDI-Image ausschließen möchten, klicken Sie auf die App und dann auf **Deinstallieren**. Wenn die Option **Deinstallieren** abgeblendet („ausgegraut“) ist, können Sie sie durch diese Methode nicht entfernen; möglicherweise können Sie sie mit Windows PowerShell entfernen oder diese Schritte ausprobieren:
1. Klicken Sie auf **Optionale Features verwalten** (auf derselben Seite direkt unter der Überschrift **Apps und Features**).
2. Klicken Sie auf das gewünschte optionale Feature und dann auf **Deinstallieren**.

Features, die (falls vorhanden) vielleicht entfernt werden sollten, sind die folgenden:
- **An Support wenden**
- **Inhalte für Einzelhandelsdemos – Englisch (USA)**
- **Inhalte für Einzelhandelsdemos – neutral**
- **Remotehilfe**

#### <a name="default-apps"></a>Standard-Apps

In diesem Bereich wird die App definiert, die für bestimmte generische Funktionen wie E-Mail, Webbrowsen und Karten standardmäßig verwendet werden soll. Wenn Sie für eine bestimmte Funktion eine andere App verwenden möchten, klicken Sie auf den aktuellen Eintrag und dann auf die für das VDI-Image gewünschte App. Soll eine Nicht-Microsoft-App eine verfügbare Option sein, müssen Sie sie installieren, bevor Sie diese Einstellung anpassen.

#### <a name="notifications-and-actions"></a>Benachrichtigungen und Aktionen

Durch diese empfohlenen Werte werden Benachrichtigungen und Netzwerkaktivitäten im Hintergrund in einer VDI-Umgebung verringert:

|Einstellung|Standardwert|Empfohlener Wert für VDI-Verwendung|  
|-------------------|----------|--------------|
|Benachrichtigungen von Apps und anderen Absendern abrufen| Ein| Deaktiviert|
|Benachrichtigungen auf dem Sperrbildschirm anzeigen|    Ein| Deaktiviert|
|Weckzeiten, Erinnerungen und eingehende VoIP-Anrufe auf Sperrbildschirm anzeigen|   Ein| Deaktiviert|
|Bei der Nutzung von Windows Tipps, Tricks und Vorschläge erhalten|    Ein| Deaktiviert|


#### <a name="offline-maps"></a>Offlinekarten

Diese Einstellung kann nur angewendet werden, wenn die Karten-App installiert wurde. Der Standardwert ist **Ein**; der empfohlene Wert für VDI-Verwendung ist **Aus**. 

#### <a name="tablet-mode"></a>Tablet-Modus

|Einstellung|Standardwert|Empfohlener Wert für VDI-Verwendung|  
|-------------------|----------|--------------|
|Bei der Anmeldung|    Passenden Modus für meine Hardware verwenden|   Desktopmodus verwenden|
|Wenn dieses Gerät den Tablet-Modus automatisch ein- oder ausschaltet|    Vor dem Wechseln immer fragen| Nicht fragen und nicht wechseln|
|App-Symbole im Tablet-Modus auf der Taskleiste ausblenden|  Ein| Deaktiviert|


### <a name="in-the-devices-area-of-windows-settings"></a>Im Bereich „Geräte“ von „Windows-Einstellungen“
Wenn Sie im Bereich „Windows-Einstellungen“ auf das Symbol **Geräte** klicken, erhalten Sie Zugriff auf eine Reihe von systembezogenen Einstellungen. Nicht alle davon müssen für eine optimale VDI-Verwendung angepasst werden. Dies sind die wichtigsten Einstellungen:

#### <a name="autoplay"></a>Automatische Wiedergabe

|Einstellung|Standardwert|Empfohlener Wert für VDI-Verwendung|  
|-------------------|----------|--------------|
|Automatische Wiedergabe für alle Medien und Geräte verwenden|    Ein| Deaktiviert|
|Wechseldatenträger:|Standard wählen|Keine Aktion ausführen|
|Speicherkarte|Standard wählen|Keine Aktion ausführen|

### <a name="in-the-personalization-area-of-windows-settings"></a>Im Bereich „Personalisierung“ von „Windows-Einstellungen“
Wenn Sie im Bereich „Windows-Einstellungen“ auf das Symbol **Personalisierung** klicken, erhalten Sie Zugriff auf eine Reihe von systembezogenen Einstellungen. Nicht alle davon müssen für eine optimale VDI-Verwendung angepasst werden. Dies sind die wichtigsten Einstellungen:

#### <a name="background"></a>Hintergrund
Manchmal kann der schwarze Standardhintergrund bei Benutzern zu der Vermutung führen, dass der Computer nicht reagiert. Mit einer Änderung der Hintergrundfarbe kommt es nicht mehr zu dieser Vermutung. Gehen Sie hierzu folgendermaßen vor:
1. Klicken Sie im Bereich **Hintergrund** auf das Pulldownmenü.
2. Wenn Sie die Hintergrundfarbe ändern möchten, klicken Sie auf **Einfarbig** und dann auf eine andere Farbe als Schwarz. Alternativ könnten Sie auf **Bild** klicken und dann ein Bild auswählen, das als Hintergrund verwendet werden soll.

#### <a name="start"></a>Beginn

|Einstellung|Standardwert|Empfohlener Wert für VDI-Verwendung|  
|-------------------|----------|--------------|
|Gelegentlich Vorschläge im Startmenü anzeigen|    Ein| Deaktiviert|
|Meistverwendete Apps anzeigen|Ein|Deaktiviert|
|Zuletzt hinzugefügte Apps anzeigen|Ein|Deaktiviert|
|Zuletzt geöffnete Elemente in Sprunglisten im Startmenü oder auf der Taskleiste anzeigen|Ein|Deaktiviert|

#### <a name="taskbar"></a>Taskleiste
Die Standardeinstellung ist die Verwendung von großen Schaltflächen der Taskleiste (d.h. der Wert „Aus“ für **Kleine Schaltflächen der Taskleiste verwenden**. Diese Einstellung bewirkt, dass das Element Cortana einen großen Teil des Taskleistenbereichs einnimmt. Um dies zu vermeiden, legen Sie **Kleine Schaltflächen der Taskleiste verwenden** auf „Ein“ fest. Wenn die Taskleistenelemente größer bleiben sollen, Cortana aber nicht so viel Platz einnehmen soll, klicken Sie mit der rechten Maustaste auf die Taskleiste, zeigen Sie auf **Cortana**, und wählen Sie im dann eingeblendeten Menü **Ausgeblendet** aus.

### <a name="in-the-privacy-area-of-windows-settings"></a>Im Bereich „Datenschutz“ von „Windows-Einstellungen“
Wenn Sie im Bereich „Windows-Einstellungen“ auf das Symbol **Datenschutz** klicken, erhalten Sie Zugriff auf eine Reihe von systembezogenen Einstellungen. Nicht alle davon müssen für eine optimale VDI-Verwendung angepasst werden. Dies sind die wichtigsten Einstellungen:

#### <a name="general"></a>Allgemein
Einige dieser Einstellungen werden auch über das Fenster „Einstellungen anpassen“ festgelegt, das am Anfang dieses Themas erläutert wird.

|Einstellung|Standardwert|Empfohlener Wert für VDI-Verwendung|  
|-------------------|----------|--------------|
|Apps die Verwendung der Werbungs-ID für App-übergreifende Erlebnisse erlauben (bei Deaktivierung wird Ihre ID zurückgesetzt)|  Ein| Deaktiviert|
|„Webseiten den Zugriff auf die eigene Sprachliste gestatten, um die Anzeige lokal relevanter Inhalte zu ermöglichen“|Ein|Deaktiviert|
|Apps auf anderen Geräten das Öffnen von Apps gestatten und auf der Oberfläche dieses Geräts weiterarbeiten|Ein|Deaktiviert|

#### <a name="camera"></a>Kamera

Der Standardwert für „Apps die Verwendung meiner Kamera erlauben“ ist **Ein**; der empfohlene Wert für VDI-Verwendung ist **Aus**.


#### <a name="microphone"></a>Mikrofon

Der Standardwert für „Apps die Verwendung meines Mikrofons erlauben“ ist **Ein**; der empfohlene Wert für VDI-Verwendung ist **Aus**.

#### <a name="notifications"></a>Benachrichtigungen

Der Standardwert für „Apps den Zugriff auf meine Benachrichtigungen erlauben“ ist **Ein**; der empfohlene Wert für VDI-Verwendung ist **Aus**.

#### <a name="contacts"></a>Kontakte

Der Standardwert für „Apps den Zugriff auf meine Kontakte erlauben“ ist **Ein**; der empfohlene Wert für VDI-Verwendung ist **Aus**.

#### <a name="calendar"></a>Calendar

Der Standardwert für „Apps den Zugriff auf meinen Kalender erlauben“ ist **Ein**; der empfohlene Wert für VDI-Verwendung ist **Aus**.

#### <a name="call-history"></a>Anrufliste

Der Standardwert für „Apps den Zugriff auf meine Anrufliste erlauben“ ist **Ein**; der empfohlene Wert für VDI-Verwendung ist **Aus**.

#### <a name="email"></a>E-Mail

Der Standardwert für „Apps den Zugriff und das Senden von E-Mails erlauben“ ist **Aus**; der empfohlene Wert für VDI-Verwendung ist **Aus**.

#### <a name="messaging"></a>Messaging

Der Standardwert für „Apps das Lesen oder Senden von Nachrichten (SMS oder MMS) erlauben“ ist **Ein**; der empfohlene Wert für VDI-Verwendung ist **Aus**.

#### <a name="radios"></a>Funkempfang

Der Standardwert für „Funksteuerung durch Apps zulassen“ ist **Ein**; der empfohlene Wert für VDI-Verwendung ist **Aus**.

#### <a name="other-devices"></a>Weitere Geräte

Der Standardwert für „Erlauben Sie Apps, automatisch Informationen mit Drahtlosgeräten auszutauschen und zu synchronisieren, die nicht explizit mit Ihrem PC, Tablet oder Handy gekoppelt sind.“ ist **Ein**; der empfohlene Wert für VDI-Verwendung ist **Aus**.

#### <a name="feedback-and-diagnostics"></a>Feedback und Diagnose

Der Standardwert für „Mein Feedback soll von Windows angefordert werden“ ist **Automatisch**; der empfohlene Wert für VDI-Verwendung ist **Nie**.

#### <a name="background-apps"></a>Hintergrund-Apps
Der Standardwert für aufgeführte Apps ist **Ein**. Dies ermöglicht es ihnen, Informationen zu empfangen, Benachrichtigungen zu senden und sich selbst zu aktualisieren – unabhängig davon, ob sie genutzt werden oder nicht. Sie sollten Apps, die nicht im Hintergrund des VDI-Images ausgeführt werden sollen, deaktivieren (auf **Aus** festlegen).

### <a name="update-and-security"></a>Update und Sicherheit
#### <a name="windows-update"></a>Windows Update
Klicken Sie im Bereich **Einstellungen aktualisieren** auf **Erweiterte Optionen**, um diese Einstellungen anzupassen:

|Einstellung|Standardwert|Empfohlener Wert für VDI-Verwendung|  
|-------------------|----------|--------------|
|Updates für andere Microsoft-Produkte bereitstellen, wenn ein Windows-Update ausgeführt wird|    Deaktiviert|    Ausgewählt|
|Zurückstellen von Featureupdates|Deaktiviert|Ausgewählt|
|Die Einrichtung meines Geräts soll nach einem Update mit meinen Anmeldeinformationen automatisch abgeschlossen werden. |Deaktiviert|Ist abhängig von bestimmter VDI-Konfiguration|

Klicken Sie auf der Seite **Erweiterte Optionen** auf **Übermittlung von Updates auswählen**, um auf die Einstellung für „Updates von mehr als einem Ort“ zuzugreifen. Der Standwert ist **Ein**; der empfohlene Wert für VDI-Verwendung ist **Aus**.

## <a name="in-control-panel-and-other-system-utilities"></a>In der Systemsteuerung und anderen Systemprogrammen

Die Einstellungen in diesem Abschnitt können entweder durch Navigieren durch die Systemsteuerung oder direktes Öffnen des Systemprogramms angepasst werden.

> [!NOTE]  
> Bei allen Einstellungen, die in diesem Thema nicht ausdrücklich erwähnt werden, können die Standardwerte beibehalten (oder Werte entsprechend Ihren Anforderungen und Richtlinien festgelegt) werden. Dies hat keine spürbare Auswirkung auf die VDI-Funktionalität.


### <a name="task-scheduler"></a>Aufgabenplanung
Sie können die Aufgabenplanung am schnellsten öffnen, indem Sie auf die Windows-Schaltfläche klicken, und *aufgabenplanung* oder *taskschd.msc* eingeben. Klicken Sie in den dann angezeigten Ergebnissen auf **Aufgabenplanung**, um das gewünschte Systemprogramm zu öffnen. Erweitern Sie in der Aufgabenplanung nacheinander **Aufgabenplanungsbibliothek**, **Microsoft** und **Windows**. Jetzt können Sie auf die Liste von Aufgabensammlungen zugreifen. Wenn Sie den Status der einzelnen geplanten Aufgaben ändern möchten, klicken Sie jeweils mit der rechten Maustaste darauf, und klicken Sie dann auf den gewünschten Status (für VDI-Verwendung in der Regel **Deaktiviert**).

|Aufgabensammlung|Aufgabenname|Standardstatus|Empfohlener Status für VDI-Verwendung|  
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
|Mobile Breitbandkonten||||
||MNO-Metadatenparser|Enabled|Deaktiviert|
|Energieeffizienzdiagnose||||
||System analysieren|Enabled|Deaktiviert|
|Wiederherstellungsumgebung||||
||VerifyWinRE|Enabled|Deaktiviert|
|Einzelhandelsdemos||||
||CleanupOfflineContent|Enabled|Deaktiviert|
|Shell||||
||FamilySafetyMonitor|Enabled|Deaktiviert|
||FamilySafetyRefreshTask|Enabled|Deaktiviert|
|Windows-Fehlerberichterstattung||||
||QueueReporting|Enabled|Deaktiviert|
|Windows-Medienfreigabe||||
||UpdateLibrary|Enabled|Deaktiviert|

Klicken Sie wieder auf **Windows**, um es zu reduzieren, und dann auf **XblGameSave**. Damit erhalten Sie Zugriff auf die Aufgaben **XBLGameSaveTask** und **XBLGameSaveTaskLogon**; beide können auf **Deaktiviert** festgelegt werden.

### <a name="performance-monitor"></a>Performance Monitor (Leistungsüberwachung)
Am schnellsten können Sie die Leistungsüberwachung öffnen, indem Sie auf die Windows-Schaltfläche klicken und dann *leistungsüberwachung* oder *perfmon.msc* eingeben. Klicken Sie in den angezeigten Ergebnissen auf **Leistungsüberwachung**. Klicken Sie in der Leistungsüberwachung auf **Datensammlersätze**, und doppelklicken Sie dann auf **Ereignisablaufverfolgungssitzungen**. Klicken Sie mit der rechten Maustaste auf **WiFiSession**; wenn der Standardzustand **Wird ausgeführt** lautet, klicken Sie auf **Beenden**.

Klicken Sie auf **StartupEventTraceSessions**. Klicken Sie dann mit der rechten Maustaste auf **ReadyBoot**; wenn dies ausgeführt wird, klicken Sie auf **Beenden**. Klicken Sie auf **Ereignisablaufverfolgungssitzungen**, klicken Sie mit der rechten Maustaste auf **ReadyBoot**, und klicken Sie dann auf **Eigenschaften**. Klicken Sie im daraufhin geöffneten Dialogfeld auf die Registerkarte **Ablaufverfolgungssitzung**. Deaktivieren Sie das Kontrollkästchen **Aktiviert**.

### <a name="services"></a>Dienste
Als schnellste Möglichkeit zum Verwalten von Diensten klicken Sie auf die Windows-Schaltfläche, und geben Sie *dienste* ein. Klicken Sie in den angezeigten Ergebnissen auf **Dienste**. Die folgenden Dienste sind gut geeignet, für eine Verwendung in VDI-Szenarien deaktiviert zu werden. Allerdings müssen Sie möglicherweise einige Tests durchführen, um zu überprüfen, ob diese Dienste für Ihre Zwecke wirklich nicht benötigt werden. Wenn Sie einen Dienst deaktivieren möchten, klicken Sie im Snap-In **Dienste** mit der rechten Maustaste auf den Dienstnamen, und klicken Sie dann auf **Eigenschaften**. Klicken Sie auf der Registerkarte **Allgemein** auf das Pulldownmenü **Starttyp** und dann auf **Deaktiviert**. Klicken Sie auf **OK**.

- BranchCache
- Übermittlungsoptimierung
- Diagnosediensthost
- Windows-Dienst für mobile Hotspots
- Xbox Live Authentifizierungs-Manager
- Xbox Live-Spiele speichern
- Xbox Live-Netzwerkservice

### <a name="file-explorer-options"></a>Explorer-Optionen
Klicken Sie auf die Windows-Schaltfläche, und geben Sie *systemsteuerung* ein. Klicken Sie in den angezeigten Ergebnissen auf **Systemsteuerung**. Klicken Sie in der Systemsteuerung auf **Explorer-Optionen**. Klicken Sie im daraufhin geöffneten Dialogfeld auf die Registerkarte **Suchen**, und deaktivieren Sie im Bereich **Beim Durchsuchen nicht indizierter Speicherorte** das Kontrollkästchen **Systemverzeichnisse einbeziehen**. Klicken Sie zum Speichern auf **OK**.

### <a name="flash-settings"></a>Flash-Einstellungen
Klicken Sie auf die Windows-Schaltfläche, und geben Sie *systemsteuerung* ein. Klicken Sie in den angezeigten Ergebnissen auf **Systemsteuerung**. Klicken Sie in der Systemsteuerung auf **Flash Player**, um den Einstellungs-Manager für Flash Player zu öffnen. Wählen Sie auf der Registerkarte **Speicher** das Optionsfeld für **Bei allen Standorten das Speichern von Informationen auf diesem Computer blockieren** aus. Klicken Sie im daraufhin geöffneten Dialogfeld auf **OK**.

Wählen Sie auf der Registerkarte **Kamera und Mikrofon** im Bereich **Einstellungen für Kamera und Mikrofon** das Optionsfeld für **Bei allen Standorten die Verwendung von Kamera und Mikrofon blockieren** aus.

Wählen Sie auf der Registerkarte **Wiedergabe** im Bereich **Peer-gestützte Netzwerke** das Optionsfeld für **Bei allen Standorten die Verwendung von Peer-gestützten Netzwerken blockieren** aus. Schließen Sie den Einstellungs-Manager für Flash Player.

### <a name="internet-options"></a>Internetoptionen
Klicken Sie auf die Windows-Schaltfläche, und geben Sie *systemsteuerung* ein. Klicken Sie in den angezeigten Ergebnissen auf **Systemsteuerung**. Klicken Sie in der Systemsteuerung auf **Internetoptionen** um „Interneteigenschaften“ zu öffnen. Geben Sie im Bereich **Startseite** die URL für die Website ein, die Benutzern als Startseite in Browsern angezeigt werden soll. Dies könnte eine Website von Ihrem Unternehmen sein, oder Sie können den Wert durch Eingabe von *about:blank* auf eine leere Startseite festlegen.

Aktivieren Sie im Bereich **Browserverlauf** das Kontrollkästchen für **Browserverlauf beim Beenden löschen**.

### <a name="power-options"></a>Energieoptionen
Klicken Sie auf die Windows-Schaltfläche, und geben Sie *systemsteuerung* ein. Klicken Sie in den angezeigten Ergebnissen auf **Systemsteuerung**. Klicken Sie in der Systemsteuerung auf **Energieoptionen**, um die Systemsteuerung für „Energieoptionen“ zu öffnen. Klicken Sie im Bereich **Einen Energiesparplan auswählen oder anpassen** auf den Abwärtspfeil für **Zusätzliche Pläne anzeigen**, und wählen Sie das Optionsfeld für **Höchstleistung** aus. Diese Einstellung hat eine sehr geringe Auswirkung auf den VDI-Host.

### <a name="system"></a>System
Klicken Sie auf die Windows-Schaltfläche, und geben Sie *systemsteuerung* ein. Klicken Sie in den angezeigten Ergebnissen auf **Systemsteuerung**. Klicken Sie in der Systemsteuerung auf **System**, um den Bereich „Systemsteuerung“ zu öffnen. Klicken Sie im linken Bereich auf **Erweiterte Systemeinstellungen**. Klicken Sie im daraufhin geöffneten Dialogfeld auf die Registerkarte **Erweitert**. Klicken Sie im Bereich **Leistung** auf die Schaltfläche **Einstellungen**. Wählen Sie im daraufhin geöffneten Dialogfeld auf der Registerkarte **Visuelle Effekte** das Optionsfeld **Für optimale Leistung anpassen** aus. Klicken Sie auf **OK**, um die Einstellung zu speichern und den Vorgang zu beenden.

## <a name="group-policy-settings"></a>Gruppenrichtlinieneinstellungen

Klicken Sie zum Bearbeiten der Einstellungen „Gruppenrichtlinie“ auf die Windows-Schaltfläche, und geben Sie *gruppenrichtlinie* oder *gpedit.msc* ein. Klicken Sie in den angezeigten Ergebnissen auf **Gruppenrichtlinie bearbeiten**, um den Editor für lokale Gruppenrichtlinien zu öffnen.

> [!NOTE]  
> Bei allen Einstellungen, die in diesem Thema nicht ausdrücklich erwähnt werden, können die Standardwerte beibehalten (oder Werte entsprechend Ihren Anforderungen und Richtlinien festgelegt) werden. Dies hat keine spürbare Auswirkung auf die VDI-Funktionalität.

Erweitern Sie unter **Computerkonfiguration** die Option **Windows-Einstellungen** und dann **Sicherheitseinstellungen**. Klicken Sie auf **Netzwerklisten-Manager-Richtlinien**, und doppelklicken Sie dann auf **Alle Netzwerke**. Wählen Sie im daraufhin geöffneten Dialogfeld im Bereich **Netzwerkadresse** das Optionsfeld für **Benutzer kann Ort nicht ändern** aus. Klicken Sie zum Speichern auf die Schaltfläche **OK**.

Reduzieren Sie **Windows-Einstellungen**, und erweitern Sie **Administrative Vorlagen**. Klicken Sie auf oder erweitern Sie **Netzwerk**. Passen Sie dann die einzelnen Einstellungen folgendermaßen an, indem Sie jeweils darauf doppelklicken, dann das Optionsfeld für den angegebenen Wert auswählen und auf die Schaltfläche **OK** klicken:

|Einstellungsbereich|Einstellung|Empfohlener Wert für VDI-Verwendung|  
|-------------------|-------|----------|
|BITS (Background Intelligent Transfer Service, Intelligenter Hintergrundübertragungsdienst)|||
||Verwendung des Windows Branch-Caches durch BITS-Client nicht zulassen|Enabled|
||Computer darf nicht als BITS-Peercachingclient fungieren|Enabled|
||Computer darf nicht als BITS-Peercachingserver fungieren|Enabled|
||BITS-Peercaching zulassen|Deaktiviert|
|BranchCache||
||BranchCache aktivieren|Deaktiviert|
|Hotspotauthentifizierung||
||Hotspotauthentifizierung aktivieren|Deaktiviert|
|Microsoft Peer-zu-Peer-Netzwerkdienste||
||Microsoft Peer-zu-Peer-Netzwerkdienste deaktivieren|Enabled|
|Offlinedateien||
||Die Funktion „Offlinedateien“ zulassen bzw. nicht zulassen|Deaktiviert|

Reduzieren Sie **Netzwerk**, und erweitern Sie dann **System**. Passen Sie die einzelnen Einstellungen folgendermaßen an, indem Sie jeweils darauf doppelklicken, dann das Optionsfeld für den angegebenen Wert auswählen und auf die Schaltfläche **OK** klicken:

|Einstellungsbereich|Einstellung|Empfohlener Wert für VDI-Verwendung|  
|-------------------|----------|--------------|
|Geräteinstallation||
||Keinen Windows-Fehlerbericht senden, wenn ein Standardtreiber für ein Gerät installiert ist|Enabled|
||Bei der Installation eines neuen Gerätetreibers keinen Systemwiederherstellungspunkt erstellen|Enabled|
||Abrufen von Gerätemetadaten aus dem Internet verhindern|Enabled|
||Verhindern, dass ein Fehlerbericht gesendet wird, wenn ein Gerätetreiber während der Installation zusätzliche Software anfordert|Enabled|
||Sprechblasen mit der Meldung „Neue Hardware gefunden“ während der Geräteinstallation deaktivieren|Enabled|

Erweitern Sie **Dateisystem**, doppelklicken Sie auf **NTFS**, doppelklicken Sie auf **Optionen für die Erstellung von Kurznamen**, wählen Sie das Optionsfeld für **Aktiviert** aus, und wählen Sie dann im Pulldownmenü **Optionen** den Eintrag **Für alle Volumes aktivieren** aus. Klicken Sie zum Speichern auf die Schaltfläche **OK**.

Reduzieren Sie **Dateisystem**, und erweitern Sie **Internetkommunikationsverwaltung**. Klicken Sie auf **Internetkommunikationseinstellungen**. Passen Sie jede Einstellung folgendermaßen an, indem Sie darauf doppelklicken, anschließend das Optionsfeld für **Aktiviert** auswählen und dann auf die Schaltfläche **OK** klicken:

- Events.asp-Links der Ereignisanzeige deaktivieren
- Freigabe von Daten für die Handschriftanpassung deaktivieren
- Handschrifterkennungs-Fehlerberichterstattung deaktivieren
- „Wussten Sie schon?“-Inhalte im Hilfe- und Supportcenter deaktivieren content
- Knowledge Base-Suche des Hilfe- und Supportcenters deaktivieren
- Verbindungs-Assistenten deaktivieren, wenn sich die URL-Verbindung auf microsoft.com bezieht
- Internet-Download für die Assistenten „Webpublishing“ und „Onlinebestellung von Abzügen“ deaktivieren
- Internet-Dateizuordnungdienst deaktivieren
- Registrierung deaktivieren, wenn sich die URL-Verbindung auf „Microsoft.com“ bezieht:
- Aufgabe „Abzüge online bestellen“ für Bilder deaktivieren
- Aufgabe „Im Web veröffentlichen“ für Dateien und Ordner deaktivieren
- Programm zur Verbesserung der Benutzerfreundlichkeit deaktivieren
- Programm zur Verbesserung der Benutzerfreundlichkeit von Windows deaktivieren
- Fehlerberichterstattung deaktivieren
- Suche nach Gerätetreibern auf Windows Update deaktivieren

Klicken Sie auf **Energieverwaltung**, und doppelklicken Sie dann auf **Aktiven Energieplan auswählen**. Wählen Sie das Optionsfeld für **Aktiviert** aus, und wählen Sie dann im Pulldownmenü **Optionen** den Eintrag **Höchstleistung** aus. Klicken Sie zum Speichern auf die Schaltfläche **OK**.

Klicken Sie auf **Wiederherstellung**, und doppelklicken Sie dann auf **Systemwiederherstellung in Standardzustand zulassen**. Wählen Sie das Optionsfeld für **Aktiviert** aus, und klicken Sie zum Speichern auf **OK**.

Erweitern Sie **Problembehandlung und Diagnose**. Klicken Sie auf **Geplante Wartung**, doppelklicken Sie auf **Verhalten für geplante Wartung konfigurieren**, und wählen Sie das Optionsfeld für **Deaktiviert** aus. Klicken Sie zum Speichern auf die Schaltfläche **OK**.

Klicken Sie bei jedem der folgenden Einstellungsbereiche auf den Bereich. Doppelklicken Sie anschließend auf **Szenarioausführungsebene konfigurieren**, wählen Sie das Optionsfeld für **Deaktiviert** aus, und klicken Sie auf die Schaltfläche **OK**, um Folgendes zu speichern:

- Windows-Startleistungsdiagnose
- Windows-Arbeitsspeicherverlust-Diagnose
- Windows-Ressourcenauslastungserkennung und -Konfliktlösung
- Windows-Herunterfahr-Leistungsdiagnose
- Diagnose für Windows-Standby-/Wiederaufnahmeleistung
- Diagnose der Leistung für Windows-Systemreaktionszeit

Reduzieren Sie **System**, und erweitern Sie dann **Windows-Komponenten**. Passen Sie jede Einstellung folgendermaßen an, indem Sie darauf doppelklicken, dann das Optionsfeld für den angegebenen Wert auswählen und auf die Schaltfläche **OK** klicken:

|Einstellungsbereich|Einstellung|Empfohlener Wert für VDI-Verwendung|  
|-------------------|-------|----------|
|Features zu Windows 10 hinzufügen|||
||Ausführung des Assistenten verhindern|Enabled|
|Richtlinien für die automatische Wiedergabe|||
||Standardverhalten von AutoAusführen festlegen|Wählen Sie „Aktiviert“ aus. Wählen Sie dann im Pulldownmenü **Optionen** den Eintrag **Keine AutoAusführen-Befehle ausführen** aus.|
|Cloudinhalt|||
||Windows-Tipps nicht anzeigen|Enabled|
||Microsoft-Anwenderfeatures deaktivieren|Enabled|
|Datensammlung und Vorabversionen|||
||Telemetrie zulassen|Wählen Sie „Aktiviert“ aus. Wählen Sie dann im Pulldownmenü **Optionen** den Eintrag **1– Einfach** aus.|
||Pre-Release-Features oder -Einstellungen deaktivieren|     Deaktiviert|
||Feedbackbenachrichtigungen nicht mehr anzeigen|       Enabled|
||Benutzersteuerung für Insider-Builds umstellen|      Deaktiviert|
|Desktopfenster-Manager|||
||Aufruf von Flip-3D nicht zulassen|       Enabled|
||Fensteranimationen nicht zulassen|       Enabled|
||Volltonfarbe für Starthintergrund verwenden|     Enabled|
|Rand-UI|||
||Wischen vom Bildschirmrand zulassen|     Deaktiviert|
||Hilfetipps deaktivieren|        Enabled|
|Datei-Explorer|||
||Benachrichtigung „Neue Anwendung installiert“ nicht anzeigen|     Enabled|
|Spiel-Explorer|||
||Herunterladen von Spielinformationen deaktivieren|     Enabled|
||Spielupdates deaktivieren|        Enabled|
||Ablaufverfolgung der letzten Spielzeiten im Ordner „Spiele“ deaktivieren|     Enabled|
|Heimnetzgruppe|||
||Beitritt des Computers zu einer Heimnetzgruppe verhindern|        Enabled|
|Internet Explorer|||
||Für Microsoft-Dienste das Bereitstellen von erweiterten Vorschlägen zulassen, wenn Benutzer Text in die Adressleiste eingeben|        Deaktiviert|
||Periodische Überprüfungen auf Internet Explorer-Softwareupdates deaktivieren|        Enabled|
||Anzeigen des Begrüßungsbildschirms deaktivieren|        Enabled|
||Automatisch neue Versionen von Internet Explorer installieren|      Deaktiviert|
||Teilnahme am Programm zur Verbesserung der Benutzerfreundlichkeit verhindern|     Enabled|
||Ausführen des Anpassungs-Assistenten verhindern – Direkt zur Startseite wechseln|   Wählen Sie „Aktiviert“ aus. Wählen Sie dann im Pulldownmenü **Optionen** den Eintrag **Direkt zur Startseite wechseln** aus.|
||Zunahme von Registerkartenprozess festlegen|Wählen Sie „Aktiviert“ aus. Geben Sie dann im Feld **Zunahme von Registerkartenprozess** Folgendes ein: *Niedrig*.|
||Standardverhalten für eine neue Registerkarte festlegen|Wählen Sie „Aktiviert“ aus. Wählen Sie dann im Pulldownmenü **Optionen** den Eintrag **Neue Registerkartenseite** aus.|
||Benachrichtigungen zur Add-On-Leistung deaktivieren|        Enabled|
||Browser-Geolocation deaktivieren|     Enabled|
||Erneutes Öffnen der letzten Browsersitzung deaktivieren|        Enabled|
||Vorschläge für alle benutzerinstallierten Anbieter deaktivieren|        Enabled|
||„Vorgeschlagene Sites“ aktivieren|       Deaktiviert|

Beachten Sie auf derselben Ebene wie die Einstellungen **Internet Explorer**, die Sie gerade in der vorstehenden Tabelle angepasst haben, eine weitere Ebene von Ordnern, die von **Schnellinfos** bis **Symbolleisten** reicht. Damit befinden Sie sich auf folgender Ebene: „Richtlinie für Lokaler Computer“ > „Computerkonfiguration“ > „Administrative Vorlagen“ > „Windows-Komponenten“ > „Internet Explorer“. 

Öffnen Sie den Ordner **Browserverlauf löschen**, doppelklicken Sie auf **Löschen des Browserverlaufs beim Beenden zulassen**, wählen Sie **Aktivieren** aus, und klicken Sie auf **OK**, um Ihre Einstellung zu speichern und den Vorgang zu beenden.

Wechseln Sie mit dem Rückwärtspfeil oben links im Editor für lokale Gruppenrichtlinien zurück zur Ebene **Internet Explorer**. Doppelklicken Sie auf **Interneteinstellungen**, dann auf **Erweiterte Einstellungen**, und passen Sie die Einstellungen in den Unterordnern folgendermaßen an:

|Ordner "Einstellung" unter **Erweiterte Einstellungen**|Einstellung|Empfohlener Wert für VDI-Verwendung|  
|-------------------|-------|----------|
|**Browsen**|||
||Finden von Telefonnummern deaktivieren|Enabled|
|**Multimedia**|||
||Internet Explorer erlauben Mediendateien wiederzugeben, die alternative Codecs verwenden|Deaktiviert|

Wechseln Sie zurück bis zur Ebene **Internet Explorer**, und doppelklicken Sie auf **Interneteinstellungen**. Legen Sie in diesem Ordner die beiden folgenden Einstellungen unter **AutoVervollständigen** auf **Aktiviert** fest:

- Vorschlagen von URLs ausschalten
- AutoVervollständigen für Windows-Suche deaktivieren

Wechseln Sie vier Ebenen zurück bis zur Ebene **Windows-Komponenten**, doppelklicken Sie auf **Position und Sensoren**, und legen Sie diese drei Einstellungen auf **Aktiviert** fest (klicken Sie bei jeder Einstellung auf **OK**, um sie zu speichern und den Vorgang zu beenden):

- Speicherort deaktivieren
- Positionskripting deaktivieren
- Sensoren deaktivieren

Doppelklicken Sie auf der Ebene **Position und Sensoren** auf **Windows-Positionssuche**, und legen Sie **Windows-Positionssuche deaktivieren** auf **Aktiviert** fest. Klicken Sie auf **OK**, um die Einstellung zu speichern und den Vorgang zu beenden.

Klicken Sie im linken Bereich auf **Karten**, und legen Sie diese Einstellungen auf **Aktiviert**fest. Klicken Sie dann bei jeder Einstellung auf **OK**, um sie zu speichern und den Vorgang zu beenden:

- Turn off Automatic Download and Update of Map Data
- Nicht angeforderten Netzwerk-Datenverkehr auf der Einstellungsseite „Offlinekarten“ deaktivieren

Geben Sie im linken Bereich jeden der folgenden Unterordner für Einstellungen ein, und passen Sie die einzelnen Einstellungen folgendermaßen an:

|Ordner „Einstellungen“ unter **Windows-Komponenten**|Einstellung|Empfohlener Wert für VDI-Verwendung|  
|-------------------|-------|----------|
|**OneDrive**|||
||Verwendung von OneDrive zum Speichern von Daten verhindern|Enabled|
||Dokumente standardmäßig auf OneDrive speichern|Deaktiviert|
|**RSS-Feeds**|||
||Automatische Ermittlung von Feeds und Web Slices verhindern|Enabled|
|**Suche**|||
||Cortana zulassen|        Deaktiviert|
||Cortana auf Sperrbildschirm zulassen|      Deaktiviert|
||Der Suche und Cortana die Nutzung von Positionsdaten erlauben|     Deaktiviert|
||Websuche nicht zulassen|      Enabled|
||Nicht im Web suchen und keine Webergebnisse in der Suche anzeigen|        Enabled|
||Hinzufügen von UNC-Speicherorten für die Indizierung in der Systemsteuerung verhindern|     Enabled|
||Indizierung von Dateien im Offlinedateicache verhindern|        Enabled|
|**Store**|||
||Deaktivieren des Angebots zum Update auf die aktuelle Version von Windows|Enabled|
|**Windows-Fehlerberichterstattung**|||
||Speicherabbild für vom Betriebssystem erstellte Fehlerberichte automatisch senden|       Deaktiviert|
||Deaktivieren der Windows-Fehlerberichterstattung|      Enabled|
|**Windows Installer**|||
||Maximalgröße für den Basisdateicache steuern|  Wählen Sie „Aktiviert“ aus. Legen Sie dann mit dem Drehfeld im Bereich **Optionen** den Wert für **Maximalgröße für den Basisdateicache** auf *5* fest.|
||Erstellung von Systemwiederherstellungsprüfpunkten deaktivieren|      Enabled|
|**Windows Mail**|||
||Communities–Features deaktivieren|Enabled|
|**Windows Media Player**|||
||Dialogfelder für die erste Verwendung nicht anzeigen|       Enabled|
||Medienfreigabe verhindern|        Enabled|
|**Windows-Mobilitätscenter**|||
||Windows-Mobilitätscenter deaktivieren|Enabled|
|**Windows-Zuverlässigkeitsanalyse**|||
||WMI-Anbieter für Zuverlässigkeit konfigurieren|Deaktiviert|
|**Windows Update**|||
||Automatische Updates sofort installieren|       Enabled|
||Zugriff auf alle Windows Update-Funktionen entfernen|     Enabled|
|Im Ordner **Windows Update** den Eintrag **Windows Update zurückstellen** öffnen|||
||Beim Empfang von Funktionsupdates auswählen|Wählen Sie „Aktiviert“ aus. Wählen Sie dann im Bereich **Optionen** das Pulldownmenü **Wählen Sie das Branch-Bereitschaftsniveau für die Funktionsupdates aus, die Sie erhalten möchten:** den Eintrag **Current Branch for Business** aus. Legen Sie den Wert im Drehfeld **Anzahl der Tage, die der Empfang eines Funktionsupdates nach der Freigabe zurückgestellt werden soll** auf *180 Tage* fest.
||Beim Empfang von Qualitätsupdates auswählen|Wählen Sie „Aktiviert“ aus. Legen Sie dann im Bereich **Optionen** mit dem Drehfeld **Anzahl der Tage, die der Empfang eines Qualitätsupdates nach der Freigabe zurückgestellt werden soll** den Wert auf *30 Tage* fest, und aktivieren Sie das Kontrollkästchen für **Qualitätsupdates aussetzen**.

Klicken Sie im linken Bereich des Editors für lokale Gruppenrichtlinien auf **Benutzerkonfiguration**. Klicken Sie im linken Bereich auf **Administrative Vorlagen**. Geben Sie dann jeden der folgenden Unterordner für Einstellungen ein, und passen Sie die einzelnen Einstellungen folgendermaßen an:

|Ordner „Einstellungen“ unter **Administrative Vorlagen**|Einstellung|Empfohlener Wert für VDI-Verwendung|  
|-------------------|-------|----------|
|**Desktop**|||
||Freigaben von zuletzt geöffneten Dateien nicht in „Netzwerkumgebung“ hinzufügen|Enabled|
|Im Ordner **Desktop** den Eintrag **Active Directory** öffnen|||
||Maximale Suchgröße von Active Directory|Wählen Sie „Aktiviert“ aus. Legen Sie dann im Bereich **Optionen** mit dem Drehfeld den Wert in **Anzahl der zurückgegebenen Objekte** auf *5000* fest.|
|**Startmenü und Taskleiste**|||
||Liste kürzlich verwendeter Programme für neue Benutzer löschen|     Enabled|
||Keine Elemente in Sprunglisten von Remotestandorten anzeigen oder nachverfolgen|        Enabled|
||Sprechblasenbenachrichtigungen für Featureankündigungen deaktivieren|     Enabled|
||Benutzerüberwachung deaktivieren|       Enabled|
|Öffnen Sie im Ordner **Startmenü und Taskleiste** den Eintrag **Benachrichtigungen**|||
||Popupbenachrichtigungen deaktivieren|Enabled|
|Öffnen Sie im Ordner **Windows-Komponenten** Folgendes:|||
|**Cloudinhalt**|||
||Features von Windows-Blickpunkt deaktivieren|Enabled|
|**Datei-Explorer**|||
||Zwischenspeicherung von Bildern in Miniaturansicht deaktivieren|       Enabled|
||Anzeige der letzten Sucheinträge im Datei-Explorer-Suchfeld deaktivieren|        Enabled|
||Zwischenspeicherung von Miniaturansichten in versteckten thumbs.db-Dateien deaktivieren|      Enabled|

## <a name="microsoft-store-apps"></a>Microsoft Store-Apps
Es gibt eine Reihe von Microsoft Store-Apps, die Sie vielleicht aus dem VDI-Image entfernen möchten; durch das Entfernen wird die CPU-Auslastung verringert und Speicherplatz gespart. Gut geeignet zum Entfernen sind:

- „Office abrufen“
- „Skype (Vorschau)“
- „Erste Schritte“ (insbesondere, wenn es keine Internetverbindung gibt)
- Feedback-Hub
- Microsoft Solitaire Collection
- Kostenpflichtiges WLAN und Mobilfunk

Verwenden Sie zum Anpassen des Standardbenutzerprofils, das zum Erstellen von VDI-Images verwendet wird, das integrierte Administratorkonto. Wenn es noch nicht aktiviert wurde, aktivieren Sie es unter „Computerverwaltung“ mithilfe von „Lokale Benutzer und Gruppen“. Melden Sie sich dann beim Administratorkonto an, um die nachstehenden Schritte auszuführen.

> [!NOTE]  
> Entfernen Sie keine System-Apps wie die Store-App. Deren Neuinstallation ist schwierig. Andere Apps können aus dem Store ganz einfach erneut installiert werden.

### <a name="delete-unwanted-apps-from-the-administrator-user-profile"></a>Löschen von unerwünschten Apps aus dem Benutzerprofil „Administrator“
1. Führen Sie in Windows PowerShell `Get-AppxPackage | ft PackageFamilyName` aus, um die Liste der installierten Apps anzuzeigen.
2. Bei jedem App-Objekt-Manager können Sie zum Deinstallieren Cmdlets mit diesem Beispielformat ausführen:

    `Get-AppxPackage *messaging* | Remove-AppxPackage`

    `Get-AppxPackage *WindowsMaps* | Remove-AppxPackage`

    `Get-AppxPackage *ZuneMusic* | Remove-AppxPackage`

### <a name="delete-the-payload-of-unwanted-store-apps"></a>Löschen der Nutzlast von unerwünschten Store-Apps
Dadurch wird verhindert, dass die Apps erneut installiert werden.
1. Listen Sie Store-Apps und andere Elemente, die Daten im Speicher bereitgestellt haben, mit diesem Cmdlet auf: `Get-AppxProvisionedPackage -Online`.
2. Entfernen Sie ein bestimmtes Paket mit `Remove-AppxProvisionedPackage -Online -PackageName MyAppPackage`, und verwenden Sie dazu das aus Schritt 1 zurückgegebene „MyAppPackage“. Um beispielsweise das Zune-bezogene Paket zu entfernen, würden Sie `Remove-AppxProvisionedPackage -Online -PackageName Microsoft.ZuneMusic_2019.17012.10311.0_neutral_~_8wekyb3d8bbwe` ausführen.

## <a name="removing-other-items"></a>Entfernen von anderen Elementen
Sie können das OneDrive-Symbol und die OneDrive-App entfernen, Systemsymbole deaktivieren und heruntergeladene Updates löschen.

### <a name="remove-onedrive-icon-and-app"></a>Entfernen des OneDrive-Symbols und der OneDrive-App
1. Klicken Sie auf **Start**, und scrollen Sie zum **OneDrive**-Symbol.
2. Klicken Sie mit der rechten Maustaste auf das **OneDrive**-Symbol, zeigen Sie auf **Mehr**, und klicken Sie auf **Dateipfad öffnen**.
3. Klicken Sie mit der rechten Maustaste auf das **OneDrive**-Symbol an seinem Dateispeicherort, und klicken Sie auf **Löschen**.

So entfernen Sie die OneDrive-App:
1. Klicken Sie auf **Start**, und scrollen Sie zum **OneDrive**-Symbol.
2. Klicken Sie mit der rechten Maustaste auf das **OneDrive**-Symbol, und klicken Sie dann auf **Deinstallieren**. „Programme und Features“ wird geöffnet.
3. Klicken Sie in „Programme und Features“ mit der rechten Maustaste auf **Microsoft OneDrive**, und klicken Sie auf **Deinstallieren**.

### <a name="programs-and-features-from-previous-versions-of-control-panel"></a>Programme und Features (aus früheren Versionen der Systemsteuerung)
1. Klicken Sie auf die Schaltfläche **Start**, geben Sie *Steuerung* ein, und drücken Sie die EINGABETASTE.
2. Tippen oder doppelklicken Sie auf  **Programme und Features**.
3. Tippen oder klicken Sie ganz links unter **Startseite der Systemsteuerung**  auf **Windows-Features aktivieren oder deaktivieren**. Eine neue Benutzeroberfläche wird geöffnet.
4. Deaktivieren Sie die Kontrollkästchen für alle Elemente, die Sie im Basisimage nicht haben möchten oder nicht benötigen, beispielsweise: **SMB 1.0-/CIFS-Dateifreigabeunterstützung**

### <a name="turn-system-icons-off"></a>Deaktivieren von Systemsymbolen
1. Drücken Sie **Start**, oder klicken Sie darauf. Klicken Sie dann auf **Einstellungen** (das Zahnradsymbol).
2. Geben Sie im Textbereich **Einstellung suchen** den Begriff *Taskleiste* ein, und klicken Sie auf **Taskleisteneinstellungen**.
3. Scrollen oder wischen Sie unter dem Abschnitt **Taskleiste** nach unten zum Abschnitt **Infobereich**.
4. Klicken oder tippen Sie auf **Systemsymbole aktivieren oder deaktivieren**, und aktivieren oder deaktivieren Sie nach Wunsch jedes Systemsymbol für das Image.

### <a name="delete-downloaded-updates"></a>Löschen von heruntergeladenen Updates
1. Navigieren Sie im Datei-Explorer zu **C:\Windows\Software Distribution\Download**.
2. Löschen Sie alle Dateien und Ordner in diesem Verzeichnis.













 













