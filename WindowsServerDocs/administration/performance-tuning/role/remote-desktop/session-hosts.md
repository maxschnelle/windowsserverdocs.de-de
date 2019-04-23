---
title: Remotedesktop-Sitzungshosts die Optimierung der Leistung
description: Richtlinien zur leistungsoptimierung für Remote Desktop Session Hosts
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: HammadBu; VladmiS
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: e45d1abb545ad46e654c811a0347c589bd12adf0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863241"
---
# <a name="performance-tuning-remote-desktop-session-hosts"></a>Remotedesktop-Sitzungshosts die Optimierung der Leistung


In diesem Thema wird erläutert, wie Remote Desktop Session Host (RD-Sitzungshost) Hardware auswählen, optimieren den Host und die Optimierung von Anwendungen.

**In diesem Thema:**

-   [Wählen die richtige Hardware für Leistung](#hw)

-   [Optimieren von Anwendungen für Remote Desktop Session Host](#apps)

-   [Remotedesktop-Sitzungshost Optimierungsparameter](#host)

## <a href="" id="hw"></a>Wählen die richtige Hardware für Leistung


Für einen Remotedesktop-Sitzungshost-serverbereitstellung die Auswahl der Hardware unterliegt den Satz der Anwendung und wie Benutzer sie verwenden. Die Schlüsselfaktoren, die die Anzahl von Benutzern und benutzerfreundlichkeit beeinflussen werden CPU, Arbeitsspeicher, Datenträger und Grafiken. Dieser Abschnitt enthält zusätzliche Richtlinien, die auf RD-Sitzungshostservern beziehen und bezieht sich hauptsächlich auf die Umgebungen im Mehrbenutzermodus des Remotedesktop-Sitzungshostserver.

### <a name="cpu-configuration"></a>CPU-Konfiguration

CPU-Konfiguration wird durch Multiplizieren der erforderlichen CPU vom Konzept her bestimmt, um eine Sitzung, indem Sie die Anzahl der Sitzungen unterstützen, die das System zu unterstützen und gleichzeitig eine Zone Puffer zur temporären Spitzen zu bewältigen erwartet wird. Mehrere logische Prozessoren können CPU-Überlastung Störfälle; reduziert werden, die in der Regel durch ein paar übermäßig aktiven Threads verursacht werden, die eine vergleichbare Anzahl von logischen Prozessoren enthalten sind.

Aus diesem Grund die logischen Prozessoren auf einem System, je niedriger der Puffer-Rand, der die CPU-Auslastung Schätzung, erstellt werden, um muss die Ergebnisse in einen größeren Prozentsatz der aktiven Auslastung pro CPU. Ein wichtiger Faktor, denken Sie daran, die die Anzahl der CPUs verdoppelt wird, ist nicht doppelt CPU-Kapazität.

### <a name="memory-configuration"></a>Speicherkonfiguration

Speicherkonfiguration ist abhängig von den Anwendungen, die Benutzer verwenden; Allerdings kann die erforderliche Menge an Arbeitsspeicher geschätzt werden, mithilfe der folgenden Formel: TotalMem = OSMem + SessionMem \* NS

OSMem ist wie viel Arbeitsspeicher an, die das Betriebssystem erforderlich ist (z. B. binäre Systemimages, Datenstrukturen und So weiter), SessionMem ausgeführt wird, wie viel Arbeitsspeicher-Prozesse in eine Sitzung erforderlich ist, und NS ist die vorgegebene Anzahl von aktiven Sitzungen. Die Menge des erforderlichen Arbeitsspeichers für eine Sitzung wird vor allem bestimmt, den privaten Speicher verweist, legen Sie für Anwendungen und Systemprozesse, die innerhalb der Sitzung ausgeführt werden. Seiten für freigegebenen Code oder Daten haben nur geringe Auswirkungen, da nur eine Kopie auf dem System vorhanden ist.

Eine interessante Beobachtung (sofern das Datenträgersystem, die der Auslagerungsdatei sichern wird nicht geändert) ist, desto größer die Anzahl der gleichzeitigen aktive Sitzungen möchte, dass das System unterstützen, je größer die speicherbelegung pro Sitzung muss,. Wenn die Größe des Arbeitsspeichers, der pro Sitzung zugeordnet ist, nicht erhöht wird, generiert die Anzahl der Seitenfehler, aktive Sitzungen nimmt mit der Anzahl der Sitzungen. Diese Fehler überlasten schließlich das e/a-Subsystem an. Durch das Erhöhen der Größe des Arbeitsspeichers, der pro Sitzung zugeordnet ist, sinkt die Wahrscheinlichkeit der Seitenfehler verursachen, wodurch die Gesamtrate der Seitenfehler zu reduzieren.

### <a name="disk-configuration"></a>Datenträgerkonfiguration

Storage ist einer der am häufigsten übersehene Aspekte beim Konfigurieren von Remotedesktop-Sitzungshostserver, und sie können die am häufigsten verwendeten Einschränkung sein, in Systemen, die in das Feld bereitgestellt werden.

Die Datenträgeraktivität, die auf einem typischen RD Session Host-Server generiert wird, wirkt sich auf den folgenden Bereichen:

-   Systemdateien und die Binärdateien der Anwendung

-   Auslagerungsdateien

-   Benutzerprofile und Benutzerdaten

Im Idealfall sollten diese Bereiche von unterschiedlichen Speichergeräten gesichert werden. Mithilfe von Stripesetvolumes RAID-Konfigurationen oder andere Arten von Speicher mit hoher Leistung weiter verbessert die Leistung. Es wird dringend empfohlen, die Verwendung von Storage-Adapter mit dem Schreibcache Batterie-Backup. Controller mit dem Schreibcache für Datenträger bieten verbesserte Unterstützung für synchrone Schreibvorgänge. Da alle Benutzer eine separate Struktur haben, sind synchrone Schreibvorgänge deutlich häufiger auf einem Remotedesktop-Sitzungshost-Server. Registrierungsstrukturen werden in regelmäßigen Abständen gespeichert, auf den Datenträger mithilfe von synchronen Schreibvorgänge auszuführen. So aktivieren Sie diese Optimierungen, in der Datenträgerverwaltungskonsole, öffnen Sie die **Eigenschaften** Dialogfeld für den Zieldatenträger und auf die **Richtlinien** Registerkarte die **Schreibcache auf Aktivieren der Datenträger** und **deaktivieren Sie Windows Schreib-Cache leeren der Puffer** auf die Geräte-Kontrollkästchen.

### <a name="network-configuration"></a>Netzwerkkonfiguration

Netzwerkauslastung eines Remotedesktop-Sitzungshostservers umfasst zwei Hauptkategorien unterteilen:

-   RD-Sitzungshost Datenverkehr verbindungsnutzung wird fast ausschließlich durch die Zeichnen-Muster bestimmt, die von den Anwendungen, die in den Sitzungen und den umgeleiteten Geräte-e/a-Datenverkehr ausgeführt ausgestellt werden.

    Beispielsweise nutzen Anwendungen, die Textverarbeitung und der Dateneingabe Bandbreite von ungefähr 10 bis 100 Kilobit pro Sekunde, während komplexe Grafiken und Videowiedergabe behauptungen Auslastung der Netzwerkbandbreite führen.

-   Back-End-Verbindungen wie servergespeicherte Profile, die Anwendungszugriff auf Dateifreigaben, Datenbankserver, e-Mail-Server und HTTP-Servern.

    Die Datenträger und das Profil des Netzwerkdatenverkehrs bezieht sich auf jede Bereitstellung.

## <a href="" id="apps"></a>Optimieren von Anwendungen für Remote Desktop Session Host


Die meisten der CPU-Auslastung auf einem Remotedesktop-Sitzungshostserver wird gesteuert, von apps. Desktop-apps sind in der Regel in Richtung der Reaktionsfähigkeit, mit dem Ziel der Minimierung von einer Anwendung, reagieren auf eine benutzeranforderung Dauer optimiert. In einer serverumgebung ist es jedoch genauso wichtig ist, die die Gesamtmenge der CPU-Auslastung zu minimieren, die zum Abschließen einer Aktion, um zu vermeiden, beeinträchtigt die anderen Sitzungen erforderlich ist.

Beachten Sie die folgenden Vorschläge, wenn Sie apps konfigurieren, die auf einem Remotedesktop-Sitzungshost-Server verwendet werden sollen:

-   Minimieren der Hintergrund Leerlaufschleifen-Verarbeitung

    Typische Beispiele für deaktivieren Grammatik und Rechtschreibung hintergrundüberprüfung, Daten, die für die Suche, Indizierung und Speicherung im Hintergrund.

-   Zu minimieren, wie oft eine app eine zustandsüberprüfung oder Update führt.

    Solcher Verhaltensweisen zu deaktivieren, oder erhöhen das Intervall zwischen den Abruf Iterationen und Zeitgeber ausgelöst deutlich profitieren CPU-Auslastung, da die Auswirkungen solcher Aktivitäten schnell für viele aktive Sitzungen verstärkt wird. Typische Beispiele sind Verbindungsstatussymbole und Aktualisierungen der Statusleiste Informationen.

-   Minimieren Sie Ressourcenkonflikte zwischen apps durch Reduzieren der synchronisierungshäufigkeit.

    Beispiele für solche Ressourcen sind Registrierungsschlüssel und Konfigurationsdateien. Beispiele für Anwendungskomponenten und Funktionen sind (z. B. Benachrichtigungen der Shell)-Statusanzeige, Hintergrund Indizierung oder änderungsüberwachung und offlinesynchronisierung.

-   Deaktivieren Sie nicht erforderliche Prozesse, die registriert werden, um mit der Benutzeranmeldung oder den Start einer Sitzung zu starten.

    Diese Prozesse können erheblich auf die Kosten für CPU-Auslastung beitragen, wenn eine neue benutzersitzung zu erstellen, die in der Regel eine CPU-intensiv ist, und es kann in Szenarien für morgen sehr teuer sein. Verwenden Sie MsConfig.exe oder MsInfo32.exe, um eine Liste der Prozesse abzurufen, die bei der Benutzeranmeldung gestartet werden. Ausführlichere Informationen können Sie [Autoruns für Windows](https://technet.microsoft.com/sysinternals/bb963902.aspx).

Für die arbeitsspeichernutzung sollten Sie Folgendes berücksichtigen:

-   Stellen Sie sicher, dass von einer app geladenen DLLs nicht verschoben werden.

    -   Verschobene DLLs können durch Auswählen der Prozess-DLL-Ansicht, überprüft werden, wie in der folgenden Abbildung gezeigt, mithilfe von [Process Explorer](https://technet.microsoft.com/sysinternals/bb896653.aspx).

    -   Hier sehen Sie, dass diese y.dll verschoben wurde, da x.dll bereits die Standard-Basisadresse belegt und ASLR nicht aktiviert wurde.

        ![verschobene dlls](../../media/perftune-guide-relocated-dlls.png)

        Wenn die DLLs verschoben werden, ist es unmöglich, teilen ihren Code über Sitzungen hinweg dies den Speicherbedarf einer Sitzung erheblich erhöht. Dies ist eines der am häufigsten verwendeten speicherbezogenen Leistungsproblemen auf einem Remotedesktop-Sitzungshost-Server.

-   Verwenden Sie für die common Language Runtime (CLR)-Anwendungen Native Image Generator (Ngen.exe), um gemeinsame Verwendung von Seiten zu erhöhen und Verringern der CPU-Auslastung.

    Wenn möglich, gelten Sie ähnliche Verfahren für andere ähnliche ausführungsmodule aus.

## <a href="" id="host"></a>Remotedesktop-Sitzungshost Optimierungsparameter


### <a name="page-file"></a>Auslagerungsdatei

Größe der Auslagerungsdatei von nicht genügend verursachen Arbeitsspeicher in apps oder Komponenten des Informationssystems Zuordnungsfehler. Sie können den Leistungsindikator "Arbeitsspeicher-zu-Zugesicherte verwendete Bytes" verwenden, um zu überwachen, wie viel zugesicherten virtuellen Speichers auf dem System ist.

### <a name="antivirus"></a>Antivirensoftware

Installieren von antivirus-Software auf einem Remotedesktop-Sitzungshostserver erheblich wirkt sich auf gesamtleistung des Systems, insbesondere CPU-Auslastung aus. Es wird dringend empfohlen, dass Sie alle Ordner, die temporären Dateien aus der Liste der aktiven Überwachung ausschließen, insbesondere solche, die Dienste und andere Systemkomponenten generieren.

### <a name="task-scheduler"></a>Aufgabenplanung

Der Aufgabenplanung können Sie die Liste der Aufgaben zu untersuchen, die für verschiedene Ereignisse geplant sind. Bei einem Remotedesktop-Sitzungshost-Server ist es hilfreich, konzentrieren sich speziell auf die Aufgaben, die konfiguriert werden, um auf im Leerlauf ausgeführt, bei der Benutzeranmeldung oder auf die Sitzung eine Verbindung herstellen und trennen. Da die Einzelheiten der Bereitstellung möglicherweise viele dieser Aufgaben nicht erforderlich.

### <a name="desktop-notification-icons"></a>Desktop-Benachrichtigungssymbole

Symbole für Benachrichtigungen auf dem Desktop können recht teuer aktualisiert Mechanismen verfügen. Deaktivieren Sie alle Benachrichtigungen durch entfernen die Komponente, die sie aus der Startliste registriert oder durch Ändern der Konfiguration für apps und Komponenten, um sie zu deaktivieren. Sie können **Benachrichtigungen Symbole anpassen** untersuchen Sie die Liste der Benachrichtigungen, die auf dem Server verfügbar sind.

### <a name="remotefx-data-compression"></a>RemoteFX-datenkomprimierung

Microsoft RemoteFX-Komprimierung kann konfiguriert werden, mithilfe der Gruppenrichtlinie unter **Computerkonfiguration &gt; Administrative Vorlagen &gt; Windows-Komponenten &gt; Remote Desktop Services &gt; Remote Remotedesktop-Sitzungshost &gt; Remoteumgebung Sitzung &gt; konfigurieren Sie die Komprimierung für RemoteFX Daten**. Drei Werte sind möglich:

-   **Optimierte weniger Arbeitsspeicher beansprucht** nutzt die geringsten Arbeitsspeichermenge pro Sitzung verfügt aber über die niedrigste Komprimierungsverhältnis und aus diesem Grund der höchsten Auslastung der Netzwerkbandbreite.

-   **Lastenausgleich von Arbeitsspeicher und Netzwerkbandbreite** reduzierter bandbreitenauslastung bei unwesentlich erhöht Speicherverbrauch (etwa 200 KB pro Sitzung).

-   **Optimierte mit weniger Netzwerkbandbreite** Netzwerkbandbreiten-Nutzung zu Kosten von ungefähr 2 MB pro Sitzung weiter reduziert. Wenn Sie diese Einstellung verwenden möchten, sollten Sie die maximale Anzahl von Sitzungen zu bewerten und auf dieser Ebene mit dieser Einstellung zu testen, bevor Sie den Server in der Produktion platzieren.

Sie können auch auswählen, um einen RemoteFX-Komprimierungsalgorithmus nicht zu verwenden. Entscheiden, verwenden einen RemoteFX-Komprimierungsalgorithmus nicht mehr Netzwerkbandbreite verwendet, und es wird nur empfohlen, wenn Sie ein Gerät verwenden, die entwickelt wurde, um den Netzwerkdatenverkehr zu optimieren. Auch wenn Sie nicht mit einer RemoteFX-Komprimierungsalgorithmus, werden einige Grafikdaten komprimiert.

### <a name="device-redirection"></a>Geräteumleitung

Geräteumleitung kann konfiguriert werden, indem Sie mithilfe von Gruppenrichtlinien unter **Computerkonfiguration &gt; Administrative Vorlagen &gt; Windows-Komponenten &gt; Remote Desktop Services &gt; Remotedesktop Host für Remotedesktopsitzungen &gt; Geräte- und Ressourcenumleitung** oder mithilfe der **Sitzungssammlung** Eigenschaftenfeld im Server-Manager.

Im Allgemeinen steigt die geräteumleitung, wie viel Bandbreite RD Session Host-Server Netzwerkverbindungen verwenden, da Daten ausgetauscht werden, zwischen Geräten, auf den Clientcomputern und Prozesse, die in der serversitzung ausgeführt werden. Das Ausmaß der Erhöhung ist eine Funktion, die Häufigkeit von Vorgängen, die von den Anwendungen ausgeführt werden, die auf dem Server für den umgeleiteten Geräten ausgeführt werden.

Druckerumleitung und Plug & Play-geräteumleitung steigt auch die CPU-Auslastung während der Anmeldung bei. Sie können Drucker auf zwei Arten umleiten:

-   Übereinstimmende treiberbasiertes druckerumleitung Wenn ein Treiber für den Drucker muss auf dem Server installiert werden. Diese Methode wird von frühere Versionen von Windows Server verwendet.

-   In Windows Server 2008 eingeführt wurde, verwendet Easy Print Treiber druckerumleitung einen allgemeinen Druckertreiber für alle Drucker an.

Die Easy Print-Methode wird empfohlen, da er bewirkt, weniger CPU-Nutzung für die Druckerinstallation zur Verbindungszeit erfolgt ist dass. Die entsprechende Methode für den Treiber bewirkt, dass die CPU-Nutzung, da sie erfordert, dass den Spooler-Dienst an andere Treiber zu laden. Bei der bandbreitenverwendung, verursacht Easy Print etwas höhere Netzwerkbandbreiten-Nutzung, aber nicht groß genug ist, um die anderen Vorteile Leistung, Verwaltbarkeit und Zuverlässigkeit versetzt.

Audio-Umleitung wird im Zuge des Netzwerkdatenverkehrs. Audio-Umleitung kann auch Benutzer multimedia-apps ausgeführt werden, die in der Regel die hohe CPU-Auslastung aufweisen.

### <a name="client-experience-settings"></a>Clientumgebungseinstellungen

Standardmäßig wählt (Remote Desktop Connection, RDC) automatisch aus der rechten Seite die Einstellung, die abhängig von der Eignung der Netzwerkverbindung zwischen dem Server und Client-Computern benutzerfreundlichkeit. Es wird empfohlen, verbleiben die RDC-Konfiguration zu **Verbindungsqualität automatisch erkennen**.

Für fortgeschrittene Benutzer bietet RDC Kontrolle über eine Vielzahl von Einstellungen, die die Leistungsfähigkeit der Netzwerkbandbreite für die Remote Desktop Services-Verbindung zu beeinflussen. Sie können die folgenden Einstellungen zugreifen, indem Sie mit der **Erfahrung** Registerkarte in der Remotedesktopverbindung oder als Einstellungen in der RDP-Datei.

Die folgenden Einstellungen gelten beim Verbinden mit einem beliebigen Computer:

-   **Deaktivieren von Hintergrundbildern** (Disable Wallpaper: I:0) Desktophintergrund auf dem umgeleiteten Verbindung wird nicht angezeigt werden. Diese Einstellung kann die Auslastung der Netzwerkbandbreite deutlich reduzieren, wenn Desktophintergrund besteht aus einem Image oder andere Inhalte mit erheblichen Kosten für das Zeichnen.

-   **Bitmap-Cache** (Bitmapcachepersistenable:i:1), wenn diese Einstellung aktiviert ist, erstellt es einen clientseitigen Cache von Bitmaps, die in der Sitzung gerendert werden. Es bietet eine erhebliche Verbesserung für die Nutzung der Netzwerkbandbreite und immer aktiviert sein (es sei denn, es weitere Überlegungen zur Sicherheit gibt).

-   **Inhalte von Windows beim Ziehen anzeigen** (Deaktivieren der gesamten Fenster ziehen: I:1) Wenn diese Einstellung deaktiviert ist, die Bandbreite reduziert, indem Sie nur den Fensterrahmen, statt den gesamten Inhalt anzeigen, wenn das Fenster gezogen wird.

-   **Menü- und Fensteranimation** (deaktivieren Menü Anims:i:1 und Disable Cursor Einstellung: I:1): Wenn diese Einstellungen deaktiviert sind, wird durch das Deaktivieren von Animationen in Menüs (z. B. das Ausblenden von Fenstern) und Cursorn die Bandbreite reduziert.

-   **Schriftartglättung** (Allow Font smoothing: I:0) Steuerelemente ClearType-Schriftart-Rendering-Unterstützung. Wenn auf Computern mit Windows 8 oder Windows Server 2012 und höher eine Verbindung herstellen, aktivieren oder deaktivieren diese Einstellung einen erheblichen Einfluss auf die Nutzung der Netzwerkbandbreite keinen. Wirkt sich jedoch für Computer, die mit Versionen vor Windows 7 und Windows 2008 R2, die Aktivierung dieser Einstellung Auslastung der Netzwerkbandbreite deutlich.

Die folgenden Einstellungen gelten nur beim Verbinden mit Computern unter Windows 7 und früheren Versionen:

-   **Desktopgestaltung** mit dieser Einstellung wird nur für eine Remotesitzung zu einem Computer unter Windows 7 oder Windows Server 2008 R2 unterstützt.

-   **Visuelle Stile** (Designs: I:1 deaktivieren) Wenn diese Einstellung deaktiviert ist, wird die Bandbreite reduziert durch die Vereinfachung der Design-Zeichnungen, die das Design Classic verwenden.

Mithilfe der **Erfahrung** Registerkarte Remote Desktop Connection, können Sie die Geschwindigkeit Ihrer Verbindung, die von Bandbreite netzwerkleistung zu beeinflussen. Die folgende Liste enthält die verfügbaren Optionen zum Konfigurieren der Geschwindigkeit Ihrer Verbindung aus:

-   **Verbindungsqualität automatisch erkennen** (Verbindungs-Typ: I:7) Wenn diese Einstellung aktiviert ist, wählt Remote Desktop Connection automatisch Einstellungen, die eine optimale benutzererfahrung basierend auf Verbindungsqualität verursachen. (Diese Konfiguration wird empfohlen, beim Verbinden von Computern mit Windows 8 oder Windows Server 2012 oder höher).

-   **Modem (56 Kbit/s)** (Verbindungs-Typ: I:1) diese Einstellung ermöglicht das dauerhafte Bitmap Zwischenspeichern.

-   **Mit geringer Geschwindigkeit Breitband (256 Kbit/s – 2 Mbit/s)** (Verbindungs-Typ: I:2) mit dieser Einstellung können Sie persistente Bitmap Zwischenspeichern und visuelle Stile.

-   **Mobilfunk/Satelliten (2 Mbit /, s - 16 MBit/s mit hoher Latenz)** (Verbindungs-Typ: I:3) dieser Einstellung können desktopgestaltung, beständige Bitmap zwischenspeichern, visuelle Stile und desktop-Hintergrund.

-   **Schnelle Breitband (2 Mbit/s – 10 Mbit/s)** (Verbindungs-Typ: I:4) mit dieser Einstellung können desktop-Komposition, Inhalte von Windows beim Ziehen, Menü- und Fensteranimation, beständige Bitmap zwischenspeichern, visuelle Stile und desktop-Hintergrund anzeigen.

-   **WAN (10 Mbit/s oder höher mit hoher Latenz)** (Verbindungs-Typ: I:5) mit dieser Einstellung können desktop-Komposition, Inhalte von Windows beim Ziehen, Menü- und Fensteranimation, beständige Bitmap zwischenspeichern, visuelle Stile und desktop-Hintergrund anzeigen.

-   **LAN (10 Mbit/s oder höher)** (Verbindungs-Typ: I:6) mit dieser Einstellung können desktop-Komposition, Inhalte von Windows beim Ziehen, Menü- und Fensteranimation, beständige Bitmap zwischenspeichern, Designs und desktop-Hintergrund anzeigen.

### <a name="desktop-size"></a>Desktop-Größe

Desktop-Größe für Remotesitzungen kann mithilfe der Registerkarte "Anzeige" in der Remotedesktopverbindung oder mithilfe der RDP-Konfigurationsdatei (Desktopwidth:i:1152 und Desktopheight:i:864) gesteuert werden. Je größer die desktop-Größe, desto größer der Arbeitsspeicher und Bandbreite Verbrauch, der dieser Sitzung zugeordnet ist. Die aktuelle maximale desktop beträgt 4096 x 2048.
