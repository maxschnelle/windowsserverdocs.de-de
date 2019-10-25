---
title: Leistungsoptimierung Remotedesktop Sitzungs Hosts
description: Richtlinien zur Leistungsoptimierung für Remotedesktop Sitzungs Hosts
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: HammadBu; VladmiS; DenisGun
author: phstee
ms.date: 10/22/2019
ms.openlocfilehash: b439b0cbab66f98a1f74faeb7bff996b30a188d5
ms.sourcegitcommit: 3262c5c7cece9f2adf2b56f06b7ead38754a451c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/23/2019
ms.locfileid: "72812329"
---
# <a name="performance-tuning-remote-desktop-session-hosts"></a>Leistungsoptimierung Remotedesktop Sitzungs Hosts


In diesem Thema wird erläutert, wie Sie Remotedesktop-Sitzungshost (RD-Sitzungshost) Hardware auswählen, den Host optimieren und Anwendungen optimieren.

**In diesem Thema:**

-   [Auswählen der richtigen Hardware für die Leistung](#selecting-the-proper-hardware-for-performance)

-   [Optimieren von Anwendungen für Remotedesktop-Sitzungshost](#tuning-applications-for-remote-desktop-session-host)

-   [Remotedesktop-Sitzungshost Optimierungsparameter](#remote-desktop-session-host-tuning-parameters)

## <a name="selecting-the-proper-hardware-for-performance"></a>Auswählen der richtigen Hardware für die Leistung


Bei einer RD-Sitzungshost Server-Bereitstellung wird die Auswahl der Hardware durch den Anwendungs Satz gesteuert und wie Benutzer Sie verwenden. Die wichtigsten Faktoren, die sich auf die Anzahl der Benutzer und Ihre Benutzeroberflächen auswirken, sind CPU, Arbeitsspeicher, Datenträger und Grafiken. Dieser Abschnitt enthält zusätzliche Richtlinien, die für RD-Sitzungshost-Server spezifisch sind und hauptsächlich mit der Multibenutzerumgebung RD-Sitzungshost Server verknüpft sind.

### <a name="cpu-configuration"></a>CPU-Konfiguration

Die CPU-Konfiguration wird konzeptionell festgelegt, indem die erforderliche CPU multipliziert wird, um eine Sitzung durch die Anzahl der Sitzungen zu unterstützen, die vom System unterstützt werden sollen, während eine Pufferzone zur Behandlung temporärer Spitzen beibehalten wird. Mehrere logische Prozessoren können dabei helfen, ungewöhnliche CPU-Überlastung zu verringern, die in der Regel durch einige über aktive Threads verursacht werden, die in einer ähnlichen Anzahl logischer Prozessoren enthalten sind.

Je mehr logische Prozessoren auf einem System, desto niedriger der in der CPU-Auslastungs Schätzung integrierte Auslagerungs Rand, was zu einem größeren Prozentsatz der aktiven Auslastung pro CPU führt. Ein wichtiger Aspekt ist, dass die doppelte Anzahl der CPUs nicht die CPU-Kapazität verdoppelt.

### <a name="memory-configuration"></a>Speicherkonfiguration

Die Speicherkonfiguration ist abhängig von den Anwendungen, die Benutzer verwenden. die erforderliche Arbeitsspeicher Menge kann jedoch mithilfe der folgenden Formel geschätzt werden: totalmem = osmem + sessionmem \* NS

Osmem gibt an, wie viel Arbeitsspeicher das Betriebssystem für die Ausführung benötigt (z. b. System Binär Images, Datenstrukturen usw.), sessionmem gibt an, wie viel Arbeitsspeicher Prozesse in einer Sitzung ausgeführt werden müssen, und NS ist die Ziel Anzahl aktiver Sitzungen. Der erforderliche Arbeitsspeicher für eine Sitzung wird größtenteils durch den Verweis auf den privaten Speicher für Anwendungen und System Prozesse bestimmt, die innerhalb der Sitzung ausgeführt werden. Freigegebene Codes oder Datenseiten haben kaum Auswirkungen, da nur eine Kopie auf dem System vorhanden ist.

Eine interessante Beobachtung (wenn das Datenträger System, das die Auslagerungs Datei sichert, nicht geändert wird) ist, dass je größer die Anzahl der gleichzeitigen aktiven Sitzungen ist, die das System unterstützen soll, je größer die Arbeitsspeicher Belegung pro Sitzung sein muss. Wenn die Menge an Arbeitsspeicher, die pro Sitzung belegt wird, nicht erhöht wird, erhöht sich die Anzahl der Seiten Fehler, die von aktiven Sitzungen generiert werden, mit der Anzahl der Sitzungen. Diese Fehler überfordern letztendlich das e/a-Subsystem. Wenn Sie die Menge an Arbeitsspeicher erhöhen, die pro Sitzung zugewiesen wird, sinkt die Wahrscheinlichkeit, dass Seiten Fehler auftreten, wodurch die Gesamtrate der Seiten Fehler verringert wird.

### <a name="disk-configuration"></a>Datenträgerkonfiguration

Der Speicher ist einer der offensichtlichsten Aspekte beim Konfigurieren von RD-Sitzungshost Servern, und dies kann die häufigste Einschränkung in Systemen sein, die im-Feld bereitgestellt werden.

Die Datenträger Aktivität, die auf einem typischen RD-Sitzungshost Server generiert wird, wirkt sich auf die folgenden Bereiche aus:

-   System Dateien und Anwendungs Binärdateien

-   Seiten Dateien

-   Benutzerprofile und Benutzerdaten

Im Idealfall sollten diese Bereiche von unterschiedlichen Speichergeräten gesichert werden. Durch die Verwendung von RAID-RAID-Konfigurationen oder anderen hochleistungsfähigen Speichertypen wird die Leistung verbessert. Es wird dringend empfohlen, Speicher Adapter mit Akku gestütztem Schreib Cache zu verwenden. Controller mit Datenträger Schreib Cache bieten verbesserte Unterstützung für synchrone Schreibvorgänge. Da alle Benutzer über eine separate Hive verfügen, sind synchrone Schreibvorgänge auf einem RD-Sitzungshost Server deutlich häufiger. Registrierungs Strukturen werden regelmäßig mithilfe synchroner Schreibvorgänge auf dem Datenträger gespeichert. Um diese Optimierungen zu aktivieren, öffnen Sie in der Konsole Datenträgerverwaltung das Dialogfeld **Eigenschaften** für den Ziel Datenträger, und wählen Sie auf der Registerkarte **Richtlinien** das Kontrollkästchen **Schreib Cache auf dem** Datenträger aktivieren und **Windows-Schreib Cache Puffer ausschalten aus.** aktivieren Sie die Kontrollkästchen für das Gerät.

### <a name="network-configuration"></a>Netzwerkkonfiguration

Die Netzwerk Auslastung für einen RD-Sitzungshost Server umfasst zwei Hauptkategorien:

-   Die Verwendung von RD-Sitzungshost Verbindungs Datenverkehr wird fast ausschließlich durch die Zeichnungs Muster bestimmt, die von den in den Sitzungen ausgestellten Anwendungen und vom e/a-Datenverkehr für umgeleitete Geräte angezeigt werden.

    Anwendungen, die die Textverarbeitung und die Dateneingabe verarbeiten, verbrauchen beispielsweise eine Bandbreite von ungefähr 10 bis 100 kbit pro Sekunde, während umfangreiche Grafiken und Videowiedergabe eine deutliche Steigerung der Bandbreitenauslastung verursachen.

-   Back-End-Verbindungen wie Roamingprofile, Anwendungs Zugriff auf Dateifreigaben, Datenbankserver, e-Mail-Server und http-Server.

    Das Volume und das Profil des Netzwerk Datenverkehrs sind spezifisch für jede Bereitstellung.

## <a name="tuning-applications-for-remote-desktop-session-host"></a>Optimieren von Anwendungen für Remotedesktop-Sitzungshost


Der größte Teil der CPU-Auslastung auf einem RD-Sitzungshost Server wird von apps gesteuert. Desktop-Apps sind in der Regel auf Reaktionsfähigkeit optimiert, mit dem Ziel, die Zeit zu minimieren, die eine Anwendung für die Reaktion auf eine Benutzer Anforderung benötigt. Allerdings ist es in einer Serverumgebung ebenso wichtig, die Gesamtmenge der CPU-Auslastung zu minimieren, die zum Ausführen einer Aktion erforderlich ist, um negative Auswirkungen auf andere Sitzungen zu vermeiden.

Beachten Sie beim Konfigurieren von apps, die auf einem RD-Sitzungshost Server verwendet werden sollen, die folgenden Vorschläge:

-   Minimieren der Leerlauf Schleifen Verarbeitung im Hintergrund

    Typische Beispiele sind die Deaktivierung von Hintergrund Grammatik und Rechtschreibprüfung, die Daten Indizierung für die Suche und die Speicherung von Hintergrundwerten.

-   Minimieren Sie, wie oft eine APP eine Status Prüfung oder ein Update ausführt.

    Durch das Deaktivieren solcher Verhaltensweisen oder das Erhöhen des Intervalls zwischen Abruf Iterationen und Timer wird die CPU-Auslastung erheblich beeinträchtigt, da die Auswirkungen solcher Aktivitäten für viele aktive Sitzungen schnell verstärkt werden. Typische Beispiele sind Verbindungsstatus Symbole und Status leisten-Informations Aktualisierungen.

-   Minimieren von Ressourcenkonflikten zwischen Apps durch Verringern der Synchronisierungs Häufigkeit.

    Beispiele für derartige Ressourcen sind Registrierungsschlüssel und Konfigurationsdateien. Beispiele für Anwendungskomponenten und Features sind Status Indikatoren (z. b. shellbenachrichtigungen), Hintergrund Indizierung oder Änderungs Überwachung und Offline Synchronisierung.

-   Deaktivieren Sie unnötige Prozesse, die registriert werden, um mit der Benutzeranmeldung oder dem Start einer Sitzung zu beginnen.

    Diese Prozesse können bei der Erstellung einer neuen Benutzersitzung, bei der es sich in der Regel um einen CPU-intensiven Prozess handelt, maßgeblich zu den Kosten der CPU-Auslastung beitragen und können in Morgen Szenarios sehr teuer sein. Verwenden Sie "msconfig. exe" oder "MsInfo32. exe", um eine Liste der Prozesse abzurufen, die bei der Benutzeranmeldung gestartet werden. Um ausführlichere Informationen zu erhalten, können Sie [Autoruns für Windows](https://technet.microsoft.com/sysinternals/bb963902.aspx)verwenden.

Für den Arbeitsspeicher Verbrauch sollten Sie Folgendes berücksichtigen:

-   Überprüfen Sie, ob die von einer APP geladenen DLLs nicht verschoben werden.

    -   Verschobene DLLs können überprüft werden, indem Sie die Option dll-Ansicht verarbeiten auswählen, wie in der folgenden Abbildung gezeigt, mithilfe des [Prozess-Explorers](https://technet.microsoft.com/sysinternals/bb896653.aspx).

    -   Hier sehen Sie, dass "y. dll" verschoben wurde, da "x. dll" bereits seine Standardbasis Adresse besetzt hat und ASLR nicht aktiviert wurde.

        ![verschobene DLLs](../../media/perftune-guide-relocated-dlls.png)

        Wenn DLLs verschoben werden, ist es nicht möglich, Ihren Code Sitzungs übergreifend freizugeben, was den Speicherbedarf einer Sitzung erheblich erhöht. Dies ist eines der häufigsten speicherbezogenen Leistungsprobleme auf einem RD-Sitzungshost Server.

-   Verwenden Sie für Common Language Runtime (CLR)-Anwendungen Native Image Generator (Ngen. exe), um die Seiten Freigabe zu erhöhen und den CPU-Overhead zu verringern.

    Wenden Sie nach Möglichkeit ähnliche Techniken auf andere ähnliche Ausführungs-Engines an.

## <a name="remote-desktop-session-host-tuning-parameters"></a>Remotedesktop-Sitzungshost Optimierungsparameter


### <a name="page-file"></a>Auslagerungs Datei

Unzureichende Größe der Auslagerungs Datei kann zu Fehlern bei der Speicher Belegung in Apps oder Systemkomponenten führen. Sie können den Leistungsindikatoren "Speicher zu Zugesicherte Bytes" verwenden, um zu überwachen, wie viel Commit für den virtuellen Arbeitsspeicher auf dem System ausgeführt wird.

### <a name="antivirus"></a>Antivirensoftware

Die Installation von Antivirensoftware auf einem RD-Sitzungshost Server wirkt sich stark auf die allgemeine Systemleistung aus, insbesondere auf die CPU Es wird dringend empfohlen, dass Sie aus der Liste der aktiven Überwachungen alle Ordner ausschließen, die temporäre Dateien enthalten, insbesondere diejenigen, die von Diensten und anderen Systemkomponenten generiert werden.

### <a name="task-scheduler"></a>Aufgabenplanung

Mit Taskplaner können Sie die Liste der Aufgaben untersuchen, die für verschiedene Ereignisse geplant sind. Bei einem RD-Sitzungshost Server ist es sinnvoll, sich speziell auf die Aufgaben zu konzentrieren, die für die Unterbrechung im Leerlauf, bei der Benutzeranmeldung oder bei der Verbindung und bei der Verbindung von Sitzungen konfiguriert sind. Aufgrund der Besonderheiten der Bereitstellung sind viele dieser Aufgaben möglicherweise unnötig.

### <a name="desktop-notification-icons"></a>Desktop Benachrichtigungs Symbole

Benachrichtigungs Symbole auf dem Desktop können über Recht teure Aktualisierungs Mechanismen verfügen. Sie sollten alle Benachrichtigungen deaktivieren, indem Sie die Komponente entfernen, von der Sie aus der Startliste registriert werden, oder indem Sie die Konfiguration für apps und Systemkomponenten ändern, um Sie zu deaktivieren. Mithilfe der **Symbole zum Anpassen von Benachrichtigungen** können Sie die Liste der auf dem Server verfügbaren Benachrichtigungen überprüfen.

### <a name="remote-desktop-protocol-data-compression"></a>Datenkomprimierung Remotedesktopprotokoll

Remotedesktopprotokoll Komprimierung kann mithilfe Gruppenrichtlinie unter **Computer Konfiguration** &gt; **Administrative Vorlagen** &gt; Windows- **Komponenten** &gt; **Remotedesktopdienste** konfiguriert werden &gt; **Remotedesktop-Sitzungshost** &gt; **Remote Sitzungs Umgebung** &gt; die **Komprimierung für remotefx-Daten konfigurieren**. Drei Werte sind möglich:

-   **Optimiert, um weniger Arbeitsspeicher zu verwenden** Beansprucht die geringste Menge an Arbeitsspeicher pro Sitzung, verfügt aber über das niedrigste Komprimierungs Verhältnis und somit über den höchsten Bandbreitenverbrauch.

-   Arbeits **Speicher und Netzwerkbandbreite** Geringere Bandbreitenauslastung bei geringfügig steigender Speicherauslastung (ungefähr 200 KB pro Sitzung).

-   **Optimiert für die Verwendung der geringeren Netzwerkbandbreite** Außerdem wird die Nutzung der Netzwerkbandbreite auf Kosten von ungefähr 2 MB pro Sitzung reduziert. Wenn Sie diese Einstellung verwenden möchten, sollten Sie die maximale Anzahl von Sitzungen bewerten und diese Ebene mit dieser Einstellung testen, bevor Sie den Server in der Produktionsumgebung platzieren.

Sie können auch auswählen, dass kein Remotedesktopprotokoll Komprimierungs Algorithmus verwendet werden soll. Daher empfiehlt es sich, ihn nur mit einem Hardware Gerät zu verwenden, das zur Optimierung des Netzwerk Datenverkehrs konzipiert ist Auch wenn Sie keinen Komprimierungs Algorithmus verwenden möchten, werden einige Grafikdaten komprimiert.

### <a name="device-redirection"></a>Geräte Umleitung

Die Geräte Umleitung kann mithilfe der Gruppenrichtlinie unter **Computer Konfiguration** &gt; **Administrative Vorlagen** &gt; **Windows-Komponenten** &gt; **Remotedesktopdienste &gt;** Remote konfiguriert werden.  **Desktop Sitzungs Host** &gt; **Geräte-und Ressourcen Umleitung** oder das Eigenschaften Feld **Sitzungs Sammlung** in Server-Manager.

Im allgemeinen erhöht die Geräte Umleitung, wie viel Netzwerkbandbreite RD-Sitzungshost Serververbindungen verwendet werden, da Daten zwischen Geräten auf den Client Computern und Prozessen ausgetauscht werden, die in der Server Sitzung ausgeführt werden. Der Umfang der Erhöhung ist eine Funktion der Häufigkeit von Vorgängen, die von den Anwendungen ausgeführt werden, die auf dem Server gegen die umgeleiteten Geräte ausgeführt werden.

Die Drucker Umleitung und die Plug & Play Geräte Umleitung erhöhen auch die CPU-Auslastung bei der Anmeldung. Drucker können auf zwei Arten umgeleitet werden:

-   Übereinstimmende Druckertreiber basierte Umleitung, wenn ein Treiber für den Drucker auf dem Server installiert werden muss. In früheren Versionen von Windows Server wurde diese Methode verwendet.

-   Die in Windows Server 2008 eingeführte einfache Druckertreiber Umleitung verwendet einen allgemeinen Druckertreiber für alle Drucker.

Wir empfehlen die Easy Print-Methode, da Sie zur Verbindungszeit weniger CPU-Auslastung für die Drucker Installation verursacht. Die entsprechende Treiber Methode bewirkt eine Erhöhung der CPU-Auslastung, da der Spoolerdienst verschiedene Treiber laden muss. Für die Bandbreitennutzung verursacht Easy Print eine geringfügige Erhöhung der Netzwerkbandbreite, aber nicht genug, um die sonstigen Vorteile der Leistung, Verwaltbarkeit und Zuverlässigkeit auszugleichen.

Die Audioumleitung bewirkt einen stetigen Stream von Netzwerk Datenverkehr. Mit der Audioumleitung können Benutzer auch Multimediaanwendungen ausführen, die in der Regel einen hohen CPU-Verbrauch aufweisen.

### <a name="client-experience-settings"></a>Einstellungen für die Client Umgebung

Standardmäßig wählt Remotedesktopverbindung (RDC) automatisch die Einstellung für die richtige Umgebung basierend auf der Eignung der Netzwerkverbindung zwischen dem Server und den Client Computern aus. Es wird empfohlen, dass die RDC-Konfiguration bei der **automatischen Erkennung der Verbindungsqualität**beibehalten wird.

Für fortgeschrittene Benutzer bietet die RDC Kontrolle über eine Reihe von Einstellungen, die die Leistung der Netzwerkbandbreite für die Remotedesktopdienste Verbindung beeinflussen. Sie können auf die folgenden Einstellungen zugreifen, indem Sie **die Registerkarte** "Umgebung" in Remotedesktopverbindung oder als Einstellungen in der RDP-Datei verwenden.

Beim Herstellen einer Verbindung mit einem beliebigen Computer gelten die folgenden Einstellungen:

-   **Hintergrundbild deaktivieren** (Hintergrundbild deaktivieren: i: 0) zeigt keine Desktop-Hintergrundbilder bei umgeleiteten Verbindungen an. Mit dieser Einstellung kann die Bandbreitenauslastung erheblich reduziert werden, wenn das Hintergrundbild des Desktops aus einem Bild oder anderen Inhalten mit erheblichen Kosten für das Zeichnen besteht.

-   **BitmapCache** (bitmapcachepersistenable: i: 1) Wenn diese Einstellung aktiviert ist, erstellt Sie einen Client seitigen Cache von Bitmaps, die in der Sitzung gerendert werden. Dies bietet eine deutliche Verbesserung der Bandbreitennutzung und sollte immer aktiviert sein (es sei denn, es gibt weitere Sicherheitsüberlegungen).

-   **Inhalt von Fenstern während des Zieh Vorgangs anzeigen** (Deaktivieren des vollständigen Fenster Zieh Vorgangs: i: 1) Wenn diese Einstellung deaktiviert ist, reduziert Sie die Bandbreite, indem nur der Fensterrahmen anstelle des gesamten Inhalts angezeigt wird, wenn das Fenster gezogen wird.

-   **Menü-und Fenster Animation** (Menü Animation deaktivieren: i: 1 und Deaktivieren der Cursor Einstellung: i: 1): Wenn diese Einstellungen deaktiviert sind, wird die Bandbreite durch Deaktivieren der Animation in Menüs (z. b. ausblenden) und Cursorn reduziert.

-   **Schriftart Glättung** (Schriftart Glättung zulassen: i: 0) steuert die Unterstützung von ClearType-Schriftart Rendering. Beim Herstellen einer Verbindung mit Computern, auf denen Windows 8 oder Windows Server 2012 und höher ausgeführt wird, hat die Aktivierung oder Deaktivierung dieser Einstellung keine erheblichen Auswirkungen auf die Bandbreitennutzung. Bei Computern, auf denen frühere Versionen als Windows 7 und Windows 2008 R2 ausgeführt werden, wirkt sich die Aktivierung dieser Einstellung jedoch erheblich auf die Netzwerkbandbreite aus.

Die folgenden Einstellungen gelten nur beim Herstellen einer Verbindung mit Computern, auf denen Windows 7 und frühere Betriebssystemversionen ausgeführt werden:

-   **Desktop Komposition** Diese Einstellung wird nur für eine Remote Sitzung auf einen Computer unter Windows 7 oder Windows Server 2008 R2 unterstützt.

-   **Visuelle Stile** (Themen deaktivieren: i: 1) Wenn diese Einstellung deaktiviert ist, wird die Bandbreite durch vereinfachen der Design Zeichnungen, die das klassische Design verwenden, reduziert.

Mithilfe **der Register** Karte "Funktionen" in Remotedesktopverbindung können Sie die Verbindungsgeschwindigkeit auswählen, um die Leistung der Netzwerkbandbreite zu beeinflussen. Im folgenden werden die Optionen aufgelistet, die zum Konfigurieren der Verbindungsgeschwindigkeit verfügbar sind:

-   **Automatisches Erkennen der Verbindungsqualität** (Verbindungstyp: i: 7) Wenn diese Einstellung aktiviert ist, wählt Remotedesktopverbindung automatisch Einstellungen aus, die zu einer optimalen Benutzerumgebung basierend auf der Verbindungsqualität führen. (Diese Konfiguration wird empfohlen, wenn Sie eine Verbindung mit Computern mit Windows 8 oder Windows Server 2012 oder höher herstellen.)

-   **Modem (56 Kbit** /s) (Verbindungstyp: i: 1) diese Einstellung aktiviert das persistente Zwischenspeichern der Bitmap.

-   **Breitband mit niedriger Geschwindigkeit (256 KBit/s-2 Mbit/s)** (Verbindungstyp: i: 2) diese Einstellung aktiviert das persistente Zwischenspeichern und visuelle Stile der Bitmap.

-   **Mobilfunk/Satellit (2 Mbit/s-16 Mbit/s mit hoher Latenz)** (Verbindungstyp: i: 3) diese Einstellung ermöglicht die Desktop Komposition, das persistente Zwischenspeichern von Bitmaps, visuelle Stile und den Desktop Hintergrund.

-   **Hochgeschwindigkeitsbreitband (2 Mbit/s – 10 Mbit/s)** (Verbindungstyp: i: 4) diese Einstellung ermöglicht die Desktop Komposition, das Anzeigen von Fenstern beim ziehen, die Menü-und Fenster Animation, das persistente Zwischenspeichern von bitmappen, visuelle Stile und den Desktop Hintergrund.

-   **WAN (10 Mbit/s oder höher mit hoher Latenz)** (Verbindungstyp: i: 5) diese Einstellung aktiviert die Desktop Komposition, den Inhalt von Fenstern beim ziehen, die Menü-und Fenster Animation, das persistente Zwischenspeichern der Bitmap, visuelle Stile und den Desktop Hintergrund.

-   **LAN (10 Mbit/s oder höher)** (Verbindungstyp: i: 6) diese Einstellung aktiviert die Desktop Komposition, den Inhalt von Fenstern beim ziehen, die Menü-und Fenster Animation, das persistente Zwischenspeichern der Bitmap, Designs und den Desktop Hintergrund.

### <a name="desktop-size"></a>Desktop Größe

Die Desktop Größe für Remote Sitzungen kann mithilfe der Registerkarte Anzeigen in Remotedesktopverbindung oder mithilfe der RDP-Konfigurationsdatei (Desktop width: i: 1152 und desktopheight: i: 864) gesteuert werden. Je größer die Größe des Desktops ist, desto größer ist der Arbeitsspeicher und der Bandbreitenverbrauch, der der Sitzung zugeordnet ist. Die aktuelle maximale Desktop Größe beträgt 4096 x 2048.
