---
title: Optimieren von IIS 10,0
description: Neukommungen für die Leistungsoptimierung von IIS 10,0-Webservern unter Windows Server 16
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: DavSo; Ericam; YaShi
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 9563a3f3628851a0cf7b3cb79990db8c2141faa4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384947"
---
# <a name="tuning-iis-100"></a>Optimieren von IIS 10,0

Internetinformationsdienste (IIS) 10,0 ist in Windows Server 2016 enthalten. Dabei wird ein Prozessmodell verwendet, das dem von IIS 8,5 und IIS 7,0 ähnelt. Ein Kernel Modus-webtreiber (http. sys) empfängt HTTP-Anforderungen und leitet diese weiter und erfüllt Anforderungen aus dem Antwort Cache. Arbeitsprozesse registrieren sich für URL-Teilbereiche, und http. sys leitet die Anforderung an den entsprechenden Prozess (oder Satz von Prozessen für Anwendungs Pools) weiter.

HTTP. sys ist für die Verbindungs Verwaltung und die Anforderungs Verarbeitung verantwortlich. Die Anforderung kann aus dem http. sys-Cache bereitgestellt oder zur weiteren Verarbeitung an einen Arbeitsprozess weitergeleitet werden. Es können mehrere Arbeitsprozesse konfiguriert werden, wodurch die Isolation zu geringeren Kosten ermöglicht wird. Weitere Informationen zur Funktionsweise der Anforderungs Verarbeitung finden Sie in der folgenden Abbildung:

![Anforderungs Verarbeitung in IIS 10,0](../../media/perftune-guide-iis-request-handling.png)

HTTP. sys enthält einen Antwort Cache. Wenn eine Anforderung mit einem Eintrag im Antwort Cache übereinstimmt, sendet http. sys die Cache Antwort direkt aus dem Kernel Modus. Einige Webanwendungs Plattformen, z. b. ASP.net, stellen Mechanismen bereit, mit denen dynamische Inhalte im Kernelmoduscache zwischengespeichert werden können. Der statische Datei Handler in IIS 10,0 speichert häufig angeforderte Dateien in http. sys automatisch zwischen.

Da ein Webserver über Kernel Modus-und Benutzermoduskomponenten verfügt, müssen beide Komponenten auf eine optimale Leistung abgestimmt werden. Daher umfasst die Optimierung von IIS 10,0 für eine bestimmte Arbeitsauslastung Folgendes:

-   HTTP. sys und der zugehörige Kernel Modus-Cache

-   Arbeitsprozesse und Benutzermodus-IIS, einschließlich der Anwendungs Pool Konfiguration

-   Bestimmte Optimierungsparameter, die sich auf die Leistung auswirken

In den folgenden Abschnitten wird erläutert, wie Sie die Kernel Modus-und benutzermodusaspekte von IIS 10,0 konfigurieren.

## <a name="kernel-mode-settings"></a>Kernelmoduseinstellungen

Leistungsbezogene http. sys-Einstellungen fallen in zwei allgemeine Kategorien: Cache Verwaltung und Verbindungs-und Anforderungs Verwaltung. Alle Registrierungs Einstellungen werden unter dem folgenden Registrierungs Eintrag gespeichert:

``` syntax
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters
```

**Beachten** Sie  wenn der HTTP-Dienst bereits ausgeführt wird, müssen Sie ihn neu starten, damit die Änderungen wirksam werden.

1/2 

## <a name="cache-management-settings"></a>Einstellungen für die Cache Verwaltung

Ein von http. sys bereitgestellte Vorteil ist ein Kernelmoduscache. Wenn sich die Antwort im Kernel Modus-Cache befindet, können Sie eine HTTP-Anforderung vollständig aus dem Kernel Modus erfüllen, wodurch die CPU-Kosten für die Verarbeitung der Anforderung erheblich gesenkt werden. Der Kernelmoduscache von IIS 10,0 basiert jedoch auf physischem Arbeitsspeicher, und die Kosten für einen Eintrag sind der Speicherplatz, den er einnimmt.

Ein Eintrag im Cache ist nur hilfreich, wenn er verwendet wird. Der Eintrag beansprucht jedoch immer physischen Speicher, unabhängig davon, ob der Eintrag verwendet wird. Sie müssen die Nützlichkeit eines Elements im Cache (die Einsparungen, die es aus dem Cache verarbeiten kann) und seine Kosten (der physische Speicher belegt) während der Lebensdauer des Eintrags auswerten, indem Sie die verfügbaren Ressourcen (CPU-und physischer Arbeitsspeicher) und die Arbeitsauslastung berücksichtigen. Bedingungen. HTTP. sys versucht, nur nützliche, aktiv auf Elemente im Cache zuzugreifen, aber Sie können die Leistung des Webservers steigern, indem Sie den http. sys-Cache für bestimmte Arbeits Auslastungen optimieren.

Im folgenden sind einige hilfreiche Einstellungen für den http. sys-kernelmoduscocache aufgeführt:

-   **Urienablecache** Standardwert: 1

    Ein Wert ungleich 0 (null) aktiviert die Kernel Modus-Antwort und das Zwischenspeichern von Fragmenten. Für die meisten Arbeits Auslastungen sollte der Cache aktiviert bleiben. Deaktivieren Sie den Cache, wenn Sie eine sehr geringe Antwort-und Fragmentzwischenspeicherung erwarten.

-   **UriMaxCacheMegabyteCount** Standardwert: 0

    Ein Wert ungleich 0 (null), der den maximalen Speicherplatz angibt, der für den Kernel Modus-Cache verfügbar ist. Der Standardwert 0 (null) ermöglicht dem System, automatisch anzupassen, wie viel Arbeitsspeicher für den Cache verfügbar ist.

    **Hinweis** Wenn Sie die Größe angeben, wird nur der Höchstwert festgelegt, und das System lässt den Cache möglicherweise nicht auf die maximal zulässige Größe anwachsen.

    1/2 

-   **Urimaxuribytes** Standardwert: 262144 bytes (256 KB)

    Die maximale Größe eines Eintrags im Kernel Modus-Cache. Antworten oder Fragmente, die größer sind als diese, werden nicht zwischengespeichert. Wenn Sie über ausreichend Arbeitsspeicher verfügen, sollten Sie den Grenzwert erhöhen. Wenn der Arbeitsspeicher begrenzt ist und große Einträge kleinere auslagern, kann es hilfreich sein, den Grenzwert zu verringern.

-   **Uriscavengerperiod** Standardwert: 120 Sekunden

    Der http. sys-Cache wird in regelmäßigen Abständen von einer Scavenger gescannt, und Einträge, auf die zwischen Scavenger-Scans nicht zugegriffen wird, werden entfernt. Wenn Sie den Scavenger-Zeitraum auf einen hohen Wert festlegen, wird die Anzahl der Scavenger-Scans reduziert. Allerdings kann sich die Cache Speicherauslastung erhöhen, da ältere Einträge, auf die seltener zugegriffen wird, im Cache verbleiben können. Wenn Sie den Zeitraum zu niedrig festlegen, werden häufigere Scavenger-Scans durchführt, und es kann zu vielen Leerungen und Cache Änderungen kommen.

## <a name="request-and-connection-management-settings"></a>Anforderungs-und Verbindungs Verwaltungs Einstellungen

In Windows Server 2016 werden Verbindungen von http. sys automatisch verwaltet. Die folgenden Registrierungs Einstellungen werden nicht mehr verwendet:

-   **MaxConnections**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\MaxConnections
    ```

-   **Idleconnectionshighmark**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\IdleConnectionsHighMark
    ```

-   **Idleconnectionslowmark**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\IdleConnectionsLowMark
    ```

-   **Idlelistkarmmerperiod**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\IdleListTrimmerPeriod
    ```

-   **Requestbufferlookasidetiefe**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\RequestBufferLookasideDepth
    ```

-   **Internalrequestlookasidetiefe**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\InternalRequestLookasideDepth
    ```


## <a name="user-mode-settings"></a>Benutzermoduseinstellungen

Die Einstellungen in diesem Abschnitt wirken sich auf das Verhalten des Workerprozesses von iis10,0 aus. Die meisten dieser Einstellungen finden Sie in der folgenden XML-Konfigurationsdatei:

% Systemroot%\\System32\\inetsrv\\config\\ApplicationHost. config

Ändern Sie die Cmdlets "Appcmd. exe", die IIS 10,0-Verwaltungskonsole, die Webadministration oder die iisadministration-PowerShell-Cmdlets. Die meisten Einstellungen werden automatisch erkannt, und es ist kein Neustart der IIS 10,0-Workerprozesse oder des Webanwendungs Servers erforderlich. Weitere Informationen zur Datei "applicationHost. config" finden [Sie unter Einführung in "applicationHost. config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig)".


## <a name="ideal-cpu-setting-for-numa-hardware"></a>Ideale CPU-Einstellung für NUMA-Hardware

Ab Windows 2016 unterstützt IIS 10,0 die automatische ideale CPU-Zuweisung für Thread Pool-Threads, um die Leistung und Skalierbarkeit auf NUMA-Hardware zu verbessern. Diese Funktion ist standardmäßig aktiviert und kann über den folgenden Registrierungsschlüssel konfiguriert werden:

``` syntax
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\InetInfo\Parameters\ThreadPoolUseIdealCpu
```

Wenn diese Funktion aktiviert ist, unternimmt der IIS-Thread-Manager den besten Aufwand für die gleichmäßige Verteilung von IIS-Threadpoolthreads auf alle CPUs in allen NUMA-Knoten auf der Grundlage ihrer aktuellen Auslastung. Im Allgemeinen empfiehlt es sich, diese Standardeinstellung für NUMA-Hardware unverändert zu lassen.

**Beachten Sie**  sich die ideale CPU-Einstellung von den Einstellungen für die NUMA-Knoten Zuweisung des Arbeitsprozesses (numanodezuweisung und numanodeaffinitymode) unterscheidet, die in den [CPU-Einstellungen für einen Anwendungs Pool](https://www.iis.net/configreference/system.applicationhost/applicationpools/add/cpu)eingeführt wurden. Die ideale CPU-Einstellung wirkt sich darauf aus, wie IIS die Threads des Thread Pools verteilt, während die Einstellungen der NUMA-Knoten Zuweisung des Arbeitsprozesses bestimmen, welcher NUMA-Knoten von einem Arbeitsprozess gestartet wird

## <a name="user-mode-cache-behavior-settings"></a>Einstellungen für das Cache Verhalten im Benutzermodus

In diesem Abschnitt werden die Einstellungen beschrieben, die sich auf das zwischen Speicherungs Verhalten in iis10,0 auswirken. Der Cache im Benutzermodus wird als Modul implementiert, das die globalen zwischen Speicherungs Ereignisse überwacht, die von der integrierten Pipeline ausgelöst werden. Um den Cache im Benutzermodus vollständig zu deaktivieren, entfernen Sie das Modul "flecachemodule (cachfile. dll)" aus der Liste der installierten Module im Konfigurations Abschnitt "System. Webserver/globalModules" in der Datei "applicationHost. config".

**System. Webserver/Caching**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|Enabled|Deaktiviert den IIS-Cache im Benutzermodus, wenn der Wert auf **false**festgelegt ist. Wenn die Cache-Treffer Rate sehr klein ist, können Sie den Cache vollständig deaktivieren, um den mehr Aufwand zu vermeiden, der mit dem Cache Codepfad verknüpft ist. Durch das Deaktivieren des Cache im Benutzermodus wird der Kernelmoduscache nicht deaktiviert.|True|
|enablekernelcache|Deaktiviert den Kernelmoduscache, wenn der Wert auf **false**festgelegt ist.|True|
|MaxCacheSize|Begrenzt die IIS-benutzermoduscache-Größe auf die angegebene Größe in Megabyte. IIS passt den Standardwert abhängig vom verfügbaren Arbeitsspeicher an. Wählen Sie den Wert abhängig von der Größe des Satzes von Dateien, auf die häufig zugegriffen wird, im Vergleich zur Größe des Arbeitsspeichers oder des IIS-Prozess Adressraums sorgfältig aus.|0|
|Maxresponsetsize|Speichert Dateien bis zur angegebenen Größe zwischen. Der tatsächliche Wert hängt von der Anzahl und Größe der größten Dateien im DataSet im Vergleich zum verfügbaren Arbeitsspeicher ab. Das Zwischenspeichern großer, häufig angeforderter Dateien kann die CPU-Auslastung, den Datenträger Zugriff und zugehörige Wartezeiten reduzieren.|262144|

## <a name="compression-behavior-settings"></a>Komprimierungs Verhaltens Einstellungen

Von IIS ab 7,0 werden statische Inhalte standardmäßig komprimiert. Außerdem ist die Komprimierung dynamischer Inhalte standardmäßig aktiviert, wenn dynamiccompressionmodule installiert ist. Durch die Komprimierung wird die Bandbreitenauslastung reduziert, aber die CPU Komprimierte Inhalte werden, sofern möglich, im Kernel Modus Cache zwischengespeichert. Ab 8,5 kann die Komprimierung von IIS unabhängig von statischem und dynamischem Inhalt gesteuert werden. Statischer Inhalt bezieht sich in der Regel auf Inhalte, die sich nicht ändern, wie GIF-oder HTM-Dateien. Dynamische Inhalte werden in der Regel von Skripts oder Code auf dem Server generiert, d. h. ASP.NET Seiten. Sie können die Klassifizierung einer bestimmten Erweiterung als statisch oder dynamisch anpassen.

Um die Komprimierung vollständig zu deaktivieren, entfernen Sie StaticCompressionModule und dynamiccompressionmodule aus der Liste der Module im Abschnitt System. Webserver/globalModules in ApplicationHost. config.

**System. Webserver/httpCompression**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|staticcompression-enablecpuusage<br><br>staticcompression-disablecpuusage<br><br>dynamiccompression-enablecpuusage<br><br>dynamiccompression-disablecpuusage|Aktiviert oder deaktiviert die Komprimierung, wenn der aktuelle Prozentsatz der CPU-Auslastung die angegebenen Grenzwerte über oder unterschreitet.<br><br>Ab IIS 7,0 wird die Komprimierung automatisch deaktiviert, wenn die CPU des Konstanten Zustands über dem Schwellenwert für die Deaktivierung zunimmt. Die Komprimierung ist aktiviert, wenn die CPU unter den Aktivierungs Schwellenwert sinkt.|50, 100, 50 und 90|
|befinden|Gibt das Verzeichnis an, in dem komprimierte Versionen von statischen Dateien temporär gespeichert und zwischengespeichert werden. Erwägen Sie, dieses Verzeichnis vom Systemlaufwerk zu verschieben, wenn häufig darauf zugegriffen wird.|%SystemDrive%\inetpub\temp\IIS temporäre komprimierte Dateien|
|dodiskspaceliangrenzungs|Gibt an, ob eine Beschränkung vorhanden ist, die angibt, wie viel Speicherplatz alle komprimierten Dateien belegen dürfen. Komprimierte Dateien werden im Komprimierungs Verzeichnis gespeichert, das durch das **Directory** -Attribut angegeben wird.|True|
|maxdiskspaceusage|Gibt die Anzahl der Bytes an Speicherplatz an, die komprimierte Dateien im Komprimierungs Verzeichnis belegen können.<br><br>Diese Einstellung muss möglicherweise angehoben werden, wenn die Gesamtgröße aller komprimierten Inhalte zu groß ist.|100 MB|

**System. Webserver/urlCompression**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|DoStaticCompression|Gibt an, ob statischer Inhalt komprimiert ist.|True|
|DoDynamicCompression|Gibt an, ob dynamischer Inhalt komprimiert wird.|True|

**Hinweis** Bei Servern mit IIS 10,0, die eine niedrige durchschnittliche CPU-Auslastung aufweisen, sollten Sie die Komprimierung für dynamischen Inhalt aktivieren, insbesondere, wenn die Antworten sehr groß sind. Dies sollte zuerst in einer Testumgebung durchgeführt werden, um die Auswirkung auf die CPU-Auslastung von der Baseline zu bewerten.


### <a name="tuning-the-default-document-list"></a>Optimieren der Standarddokument Liste

Das Standarddokument Modul verarbeitet HTTP-Anforderungen für den Stamm eines Verzeichnisses und übersetzt Sie in Anforderungen für eine bestimmte Datei, z. b. "default. htm" oder "index. htm". Im Durchschnitt übersteigen 25 Prozent aller Anforderungen im Internet den Standarddokument Pfad. Dies variiert für einzelne Websites erheblich. Wenn eine HTTP-Anforderung keinen Dateinamen angibt, durchsucht das Standarddokument Modul die Liste der zulässigen Standarddokumente nach den einzelnen Namen im Dateisystem. Dies kann sich negativ auf die Leistung auswirken, insbesondere, wenn das Erreichen des Inhalts einen Netzwerkroundtrip oder einen Datenträger erfordert.

Sie können den Aufwand vermeiden, indem Sie die Standarddokumente selektiv deaktivieren und die Liste der Dokumente reduzieren oder anordnen. Bei Websites, die ein Standarddokument verwenden, sollten Sie die Liste auf die verwendeten Standarddokument Typen reduzieren. Ordnen Sie außerdem die Liste so an, dass Sie mit dem am häufigsten verwendeten Standarddokument Dateinamen beginnt.

Sie können das standardmäßige Dokument Verhalten selektiv für bestimmte URLs festlegen, indem Sie die Konfiguration innerhalb eines Location-Tags in "applicationHost. config" anpassen oder indem Sie eine Web. config-Datei direkt in das Inhaltsverzeichnis einfügen. Dies ermöglicht einen Hybrid Ansatz, bei dem Standarddokumente nur an der Stelle, an der Sie benötigt werden, aktiviert werden und die Liste für jede URL auf den richtigen Dateinamen festgelegt wird.

Um Standarddokumente vollständig zu deaktivieren, entfernen Sie defaultdocumentmodule aus der Liste der Module im Abschnitt System. Webserver/globalModules in ApplicationHost. config.

**System. Webserver/defaultDocument**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|enabled|Gibt an, dass Standarddokumente aktiviert sind.|True|
|&lt;Dateien&gt; Element|Gibt die Dateinamen an, die als Standarddokumente konfiguriert sind.|Die Standardliste lautet Default. htm, Default. ASP, Index. htm, Index. html, iisstart. htm und default. aspx.|

## <a name="central-binary-logging"></a>Zentrale binäre Protokollierung

Wenn die Server Sitzung über zahlreiche URL-Gruppen verfügt, kann der Prozess zum Erstellen von Hunderten von formatierten Protokolldateien für einzelne URL-Gruppen und zum Schreiben der Protokolldaten auf einen Datenträger schnell wertvolle CPU-und Arbeitsspeicher Ressourcen verbrauchen, wodurch die Leistung und Skalierbarkeits Probleme. Die zentralisierte binäre Protokollierung minimiert die Menge an Systemressourcen, die für die Protokollierung verwendet werden, während gleichzeitig detaillierte Protokolldaten für Organisationen bereitgestellt werden, für die dies erforderlich ist. Das Protokollieren von Protokollen im Binärformat erfordert ein Postprocessing-Tool.

Sie können die zentrale binäre Protokollierung aktivieren, indem Sie das centrzufilemode-Attribut auf centralbinary festlegen und das **aktivierte** Attribut auf " **true**" festlegen. Erwägen Sie, den Speicherort der zentralen Protokolldatei von der Systempartition auf ein dediziertes Protokollierungs Laufwerk zu verschieben, um Konflikte zwischen Systemaktivitäten und Protokollierungs Aktivitäten zu vermeiden.

**System. applicationHost/Log**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|centrzuweisung FileMode|Gibt den Protokollierungs Modus für einen Server an. Ändern Sie diesen Wert in centralbinary, um die zentrale binäre Protokollierung zu aktivieren.|Site|

**System. applicationHost/Log/centralbinarylogfile**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|enabled|Gibt an, ob die zentrale binäre Protokollierung aktiviert ist.|False|
|befinden|Gibt das Verzeichnis an, in das Protokolleinträge geschrieben werden.|%SystemDrive%\inetpub\logs\LogFiles|


## <a name="application-and-site-tunings"></a>Anwendungs-und Standort-Tunings

Die folgenden Einstellungen beziehen sich auf die Anwendungs Pool-und Standort-Tunings.

**System. applicationHost/ApplicationPools/applicationPoolDefaults**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|queueLength|Gibt http. sys an, wie viele Anforderungen für einen Anwendungs Pool in die Warteschlange eingereiht werden, bevor zukünftige Anforderungen zurückgewiesen werden. Wenn der Wert für diese Eigenschaft überschritten wird, lehnt IIS nachfolgende Anforderungen mit einem Fehler 503 ab.<br><br>Erhöhen Sie diese für Anwendungen, die mit Daten speichern mit hoher Latenz kommunizieren, wenn 503-Fehler festgestellt werden.|1000|
|Enable32BitAppOnWin64|Wenn der Wert true ist, kann eine 32-Bit-Anwendung auf einem Computer mit einem 64-Bit-Prozessor ausgeführt werden.<br><br>Aktivieren Sie den 32-Bit-Modus, wenn die Arbeitsspeicher Nutzung von Bedeutung ist. Da Zeiger Größen und Anweisungs Größen kleiner sind, verwenden 32-Bit-Anwendungen weniger Arbeitsspeicher als 64-Bit-Anwendungen. Der Nachteil der Ausführung von 32-Bit-Anwendungen auf einem 64-Bit-Computer besteht darin, dass der Adressraum im Benutzermodus auf 4 GB beschränkt ist.|False|

**System. applicationHost/Sites/virtualdirecterydefault**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|allowSubDirConfig|Gibt an, ob IIS nach Web. config-Dateien in Inhaltsverzeichnissen sucht, die niedriger als die aktuelle Ebene sind (true), oder ob Web. config-Dateien in Inhaltsverzeichnissen unterhalb der aktuellen Ebene (false) gesucht werden. Durch die Durchsetzung einer einfachen Einschränkung, die nur die Konfiguration in virtuellen Verzeichnissen zulässt, kann IIS-10,0 wissen, dass, sofern **/&lt;Namen&gt;. htm** ein virtuelles Verzeichnis ist, nicht nach einer Konfigurationsdatei suchen sollte. Das Überspringen der zusätzlichen Datei Vorgänge kann die Leistung von Websites erheblich verbessern, die über einen sehr großen Satz von statisch zugänglichen statischen Inhalten verfügen.|True|

## <a name="managing-iis-100-modules"></a>Verwalten von IIS 10,0-Modulen

IIS 10,0 wurde in mehrere Benutzer erweiterbare Module integriert, um eine modulare Struktur zu unterstützen. Diese Faktorisierung hat geringe Kosten. Für jedes Modul muss die integrierte Pipeline das Modul für jedes für das Modul relevante Ereignis aufzurufen. Dies geschieht unabhängig davon, ob das Modul irgendwelche Aufgaben ausführen muss. Sie können CPU-Zyklen und Arbeitsspeicher einsparen, indem Sie alle Module entfernen, die für eine bestimmte Website nicht relevant sind.

Ein Webserver, der auf einfache statische Dateien abgestimmt ist, kann nur die folgenden fünf Module enthalten: uricachemodule, httpcachemodule, StaticFileModule, anonymousauthenticationmodule und HttpLoggingModule.

Um Module aus "applicationHost. config" zu entfernen, entfernen Sie alle Verweise auf das Modul aus den Abschnitten "System. Webserver/Handlers" und "System. Webserver/Module", und entfernen Sie die Modul Deklaration in "System. Webserver/globalModules".

## <a name="classic-asp-settings"></a>Klassische ASP-Einstellungen

Die Hauptkosten für die Verarbeitung einer klassischen ASP-Anforderung umfassen das Initialisieren einer Skript-Engine, das Kompilieren des angeforderten ASP-Skripts in eine ASP-Vorlage und das Ausführen der Vorlage für die Skript-Engine. Die Ausführungskosten für die Vorlage hängen von der Komplexität des angeforderten ASP-Skripts ab. das klassische ASP-Modul von IIS kann Skript-Engines im Arbeitsspeicher zwischenspeichern und Vorlagen sowohl im Arbeitsspeicher als auch auf dem Datenträger zwischenspeichern, um die Leistung in zu verbessern. CPU-gebundene Szenarien.

Die folgenden Einstellungen werden verwendet, um den klassischen ASP-Vorlagen Cache und Skript-Engine-Cache zu konfigurieren. diese Einstellungen wirken sich nicht auf die ASP.NET-Einstellungen aus.

**System. Webserver/ASP/Cache**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|diskTemplateCacheDirectory|Der Name des Verzeichnisses, das ASP zum Speichern kompilierter Vorlagen verwendet, wenn der in-Memory-Cache überläuft.<br><br>Empfehlung: Legen Sie auf ein Verzeichnis fest, das nicht häufig verwendet wird, z. b. ein Laufwerk, das nicht für das Betriebssystem, das IIS-Protokoll oder andere Inhalte verwendet wird, auf die häufig zugegriffen wird.|%SystemDrive%\inetpub\temp\asp kompilierte Vorlagen|
|maxDiskTemplateCacheFiles|Gibt die maximale Anzahl kompilierter ASP-Vorlagen an, die auf dem Datenträger zwischengespeichert werden können.<br><br>Empfehlung: Legen Sie auf den maximalen Wert von 0x7FFFFFFF fest.|2000|
|scriptmelecachesize|Dieses Attribut gibt die maximale Anzahl kompilierter ASP-Vorlagen an, die im Arbeitsspeicher zwischengespeichert werden können.<br><br>Empfehlung: Legen Sie auf mindestens so viele wie die Anzahl der häufig angeforderten ASP-Skripts fest, die von einem Anwendungs Pool bedient werden. Wenn möglich, legen Sie auf so viele ASP-Vorlagen fest, wie die Speicher Limits dies zulassen.|500|
|scriptEngineCacheMax|Gibt die maximale Anzahl von Skript-Engines an, die im Arbeitsspeicher zwischengespeichert werden.<br><br>Empfehlung: Legen Sie auf mindestens so viele wie die Anzahl der häufig angeforderten ASP-Skripts fest, die von einem Anwendungs Pool bedient werden. Wenn möglich, legen Sie auf so viele Skript-Engines fest, wie das Arbeitsspeicher Limit zulässt.|250|

**System. Webserver/ASP/Limits**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|processorthread Max|Gibt die maximale Anzahl von Arbeitsthreads pro Prozessor an, die ASP erstellen kann. Erhöhen Sie diese Einstellung, wenn die aktuelle Einstellung für die Verarbeitung der Last unzureichend ist, was zu Fehlern führen kann, wenn Sie Anforderungen verarbeiten oder eine Unterauslastung der CPU-Ressourcen verursachen.|25|

**System. Webserver/ASP/ComPlus**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|executeingemta|Legen Sie diese Einstellung auf **true** fest, wenn Fehler oder Fehler erkannt werden, während IIS ASP-Inhalte bedient. Dies kann beispielsweise der Fall sein, wenn mehrere isolierte Standorte gehostet werden, an denen die einzelnen Standorte unter einem eigenen Arbeitsprozess ausgeführt werden. Fehler werden in der Regel von com+ im Ereignisanzeige gemeldet. Diese Einstellung aktiviert das Multithread-Apartment Modell in ASP.|False|


## <a name="aspnet-concurrency-setting"></a>ASP.net-Parallelitäts Einstellung

### <a name="aspnet-35"></a>ASP.NET 3,5
Standardmäßig wird durch ASP.net Limits die Parallelität angefordert, um den Speicherverbrauch des stabilen Zustands auf dem Server zu verringern. Hohe Parallelitäts Anwendungen müssen möglicherweise einige Einstellungen anpassen, um die Gesamtleistung zu verbessern. Sie können diese Einstellung in der Datei Aspnet. config ändern:

``` syntax
<system.web>
  <applicationPool maxConcurrentRequestsPerCPU="5000"/>
</system.web>
```

Die folgende Einstellung ist nützlich, um Ressourcen auf einem System vollständig zu verwenden:

-   **maxconcurrentrequestpercpu** Standardwert: 5000

    Mit dieser Einstellung wird die maximale Anzahl gleichzeitig ausgeführter ASP.NET-Anforderungen auf einem System beschränkt. Der Standardwert ist konservativ, um den Arbeitsspeicher Verbrauch von ASP.NET-Anwendungen zu verringern. Ziehen Sie in Erwägung, dieses Limit für Systeme zu erhöhen, die Anwendungen ausführen, die lange synchrone e/a-Vorgänge ausführen. Andernfalls kann es bei Benutzern aufgrund von Warteschlangen-oder Anforderungs Fehlern zu einer hohen Latenz kommen, wenn die Warteschlangen Limits bei hoher Auslastung überschritten werden, wenn die Standardeinstellung verwendet wird.

### <a name="aspnet-46"></a>ASP.NET 4.6
Neben der Einstellung maxconcurrentrequestpercpu bietet ASP.NET 4,7 auch Einstellungen zum Verbessern der Leistung in den Anwendungen, die stark von einem asynchronen Vorgang abhängig sind. Die Einstellung kann in der Datei "ASPNET. config" geändert werden.

``` syntax
<system.web>
  <applicationPool percentCpuLimit="90" percentCpuLimitMinActiveRequestPerCpu="100"/>
</system.web>
```

-   **prozentucpulimit** Standardwert: 90 asynchrone Anforderung hat einige Skalierbarkeits Probleme, wenn eine große Auslastung (über die Hardwarefunktionen hinaus) in einem solchen Szenario liegt. Das Problem liegt in der Art der Zuordnung für asynchrone Szenarien. In diesen Fällen findet die Zuordnung statt, wenn der asynchrone Vorgang gestartet wird, und wird nach Abschluss des Vorgangs verarbeitet. Zu diesem Zeitpunkt wurden die Objekte sehr möglich auf die Generation 1 oder 2 von GC verschoben. Wenn dies der Fall ist, wird beim Erhöhen der Auslastung eine Erhöhung der Anforderungen pro Sekunde (RPS) bis zu einem Punkt angezeigt. Nachdem wir diesen Punkt bestanden haben, wird die Zeit, die für die GC aufgewendet wird, zu einem Problem, und die RPS wird mit einem negativen Skalierungs Effekt begonnen. Um das Problem zu beheben, werden Anforderungen an die systemeigene ASP.NET-Warteschlange gesendet, wenn die CPU-Auslastung die Einstellung%% amp; qutriewert überschreitet.
-   **prozentucpulimitminactiverequestpercpu** Standardwert: 100 die CPU-Drosselung (Einstellung "prozentucpulimit") basiert nicht auf der Anzahl von Anforderungen, sondern auf der Anzahl der Anforderungen. Demzufolge kann es nur wenige CPU-intensive Anforderungen geben, die eine Sicherung in der systemeigenen Warteschlange verursachen, ohne eine Möglichkeit zu geben, Sie von eingehenden Anforderungen zu leeren. Zum lösen dieses problme kann "prozentucpulimitminactiverequestpercpu" verwendet werden, um sicherzustellen, dass eine Mindestanzahl von Anforderungen verarbeitet wird, bevor die Drosselung erreicht wird.

## <a name="worker-process-and-recycling-options"></a>Arbeitsprozess-und Wiederverwendungs Optionen

Sie können Optionen für die Wiederverwendung von IIS-Arbeitsprozessen konfigurieren und praktische Lösungen für akute Situationen oder Ereignisse bereitstellen, ohne dass ein Eingriff erforderlich ist oder ein Dienst oder Computer zurückgesetzt werden muss Zu solchen Situationen und Ereignissen gehören Speicher Verluste, eine höhere Arbeitsspeicher Auslastung oder nicht reagierende oder Leerlauf Arbeitsprozesse. Unter normalen Bedingungen werden möglicherweise keine Wiederverwendungs Optionen benötigt, und die Wiederverwendung kann deaktiviert werden, oder das System kann so konfiguriert werden, dass es sehr selten verwendet wird.

Sie können die Prozess Wiederverwendung für eine bestimmte Anwendung aktivieren, indem Sie dem Wiederverwendungs **-/periodikrestart-Element** Attribute hinzufügen. Das-Wiederverwendungs Ereignis kann von mehreren Ereignissen ausgelöst werden, einschließlich der Speicherauslastung, einer bestimmten Anzahl von Anforderungen und einem bestimmten Zeitraum. Wenn ein Arbeitsprozess wieder verwendet wird, werden die in die Warteschlange eingereihten und ausgeführten Anforderungen entladen, und ein neuer Prozess wird gleichzeitig gestartet, um neue Anforderungen zu verarbeiten. Das Element " **Recycling/periodikrestart** " ist pro Anwendung, was bedeutet, dass jedes Attribut in der folgenden Tabelle pro Anwendung partitioniert wird.

**System. applicationHost/ApplicationPools/applicationPoolDefaults/recyceln/periodikrestart**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|memory|Prozess Wiederverwendung aktivieren, wenn die Auslastung des virtuellen Arbeitsspeichers den angegebenen Grenzwert in Kilobyte überschreitet. Dies ist eine nützliche Einstellung für 32-Bit-Computer, die über einen kleinen, 2 GB großen Adressraum verfügen. Dadurch können fehlgeschlagene Anforderungen aufgrund von Fehlern aufgrund von nicht genügend Arbeitsspeicher vermieden werden.|0|
|PrivateMemory|Aktivieren Sie die Prozess Wiederverwendung, wenn private Speicher Belegungen die angegebene Grenze in Kilobyte überschreiten.|0|
|requests|Aktivieren Sie die Prozess Wiederverwendung nach einer bestimmten Anzahl von Anforderungen.|0|
|Zeit|Aktivieren Sie die Prozess Wiederverwendung nach einem bestimmten Zeitraum.|29:00:00|


## <a name="dynamic-worker-process-page-out-tuning"></a>Dynamische Worker-Prozess-Seite-Out-Optimierung

Ab Windows Server 2012 R2 bietet IIS die Möglichkeit, den Arbeitsprozess so zu konfigurieren, dass er angehalten wird, nachdem Sie sich eine Weile im Leerlauf befunden haben (zusätzlich zur Option "beenden", die seit IIS 7 vorhanden war).

Der Hauptzweck sowohl der Seiten-out-als auch der Arbeitsprozess Beendigungs Funktionen für den Arbeitsspeicher im Leerlauf besteht darin, die Arbeitsspeicher Auslastung auf dem Server zu sparen, da eine Website viel Arbeitsspeicher beanspruchen kann, auch wenn Sie sich an dieser Stelle befindet und lauscht. Abhängig von der auf der Site verwendeten Technologie (statischer Inhalt im Vergleich zu anderen Frameworks) kann der verwendete Arbeitsspeicher zwischen ungefähr 10 MB und Hunderten von MSB liegen. das bedeutet, dass wenn Ihr Server mit vielen Standorten konfiguriert ist, die effektivsten Einstellungen ermitteln. für Ihre Websites kann die Leistung aktiver und angehaltene Standorte erheblich verbessern.

Bevor wir uns mit den Besonderheiten befassen, müssen wir beachten, dass es wahrscheinlich am besten ist, dass die Sites nie angehalten oder beendet werden, wenn keine Speicher Einschränkungen vorliegen. Schließlich ist es nur wenig Wert, wenn ein Arbeitsprozess beendet wird, wenn es sich um das einzige auf dem Computer handelt.

**Beachten Sie**  für den Fall, dass die Site instabilen Code ausführt, z. b. Code mit einem Speichermangel oder anderweitig instabil, kann das Festlegen der Site, die im Leerlauf beendet werden soll, eine schnelle und geänderte Alternative zum Beheben des Code Fehlers sein. Dies ist nicht zu empfehlen, aber es kann besser sein, dieses Feature als Bereinigungs Mechanismus zu verwenden, während eine permanente Lösung in der Arbeit ist.\]

1/2 

Ein weiterer Faktor, der berücksichtigt werden muss, ist, dass der Unterbrechungs Prozess selbst eine Mautgebühr übernimmt, wenn der Computer die vom Arbeitsprozess verwendeten Daten auf den Datenträger schreiben muss. Wenn der Arbeitsprozess einen großen Teil des Arbeitsspeichers verwendet, ist das Anhalten möglicherweise teurer als die Kosten, die gewartet werden muss, bis der Arbeitsprozess wieder gestartet wird.

Um das Beste aus der Funktion zum Anhalten des Workerprozesses zu machen, müssen Sie Ihre Websites in den einzelnen Anwendungs Pools überprüfen und entscheiden, welche angehalten werden sollen, welche beendet werden sollen und welche unbegrenzt aktiv sein sollte. Für jede Aktion und jede Site müssen Sie den idealen Timeout Zeitraum ermitteln.

Idealerweise sind die Standorte, die Sie für die Unterbrechung oder Beendigung konfigurieren, diejenigen, die täglich Besucher haben, aber nicht genug, um zu gewährleisten, dass Sie immer aktiv bleiben. Dabei handelt es sich in der Regel um Websites mit ungefähr 20 eindeutigen Besuchern pro Tag oder weniger. Sie können die Datenverkehrs Muster mithilfe der Protokolldateien der Site analysieren und den durchschnittlichen täglichen Datenverkehr berechnen.

Beachten Sie, dass Sie, sobald ein bestimmter Benutzer eine Verbindung mit der Website herstellt, in der Regel mindestens eine Weile darauf warten, dass es zusätzliche Anforderungen gibt und dass das zählen der täglichen Anforderungen möglicherweise nicht exakt den tatsächlichen Datenverkehrs Mustern entspricht. Um ein genaueres lesen zu erzielen, können Sie auch ein Tool wie Microsoft Excel verwenden, um die durchschnittliche Zeit zwischen den Anforderungen zu berechnen. Zum Beispiel:

||Anforderungs-URL|Anforderungs Zeit|Delta|
|--- |--- |--- |--- |
|1|/SourceSilverLight/Geosource.Web/grosource.html|10:01||
|2|/SourceSilverLight/Geosource.web/sliverlight.js|10:10|0:09|
|3|/SourceSilverLight/Geosource.web/clientbin/geo/1.aspx|10:11|0:01|
|4|/lClientAccessPolicy.xml|10:12|0:01|
|5|/Sourcesilverlight/geosourcewebservice/Service. asmx|10:23|0:11|
|6|/Sourcesilverlight/geosource. Web/geosearchserver....|11:50|1:27|
|7|/Rest/Services/cachedservices/-Silverlight_load_la...|12:50|1:00|
|8|/Rest/Services/cachedservices/Silverlight_basemap....|12:51|0:01|
|9|/Rest/Services/DynamicService/Silverlight_basemap....|12:59|0:08|
|10|/Rest/Services/cachedservices/Ortho_2004_cache...|13:40|0:41|
|11|/Rest/Services/cachedservices/Ortho_2005_cache. js|13:40|0:00|
|12|/rest/Services/CachedServices/OrthoBaseEngine.aspx|13:41|0:01|

Der schwierigste Teil ist jedoch, herauszufinden, welche Einstellung auf "Sense" angewendet werden soll. In unserem Fall erhält der Standort eine Reihe von Anforderungen von Benutzern, und die obige Tabelle zeigt, dass insgesamt vier eindeutige Sitzungen in einem Zeitraum von 4 Stunden stattgefunden haben. Mit den Standardeinstellungen für die Arbeitsprozess Unterbrechung des Anwendungs Pools wird die Website nach dem Standard Timeout von 20 Minuten beendet. Dies bedeutet, dass jeder dieser Benutzer den Standort Aufgliederungs Prozess sehen würde. Dies ist ein idealer Kandidat für die Unterbrechung des Arbeitsprozesses, weil sich die Website in den meisten Fällen im Leerlauf befindet. durch das Anhalten wird die Ressource gespart, und die Benutzer können die Website fast sofort erreichen.

Ein letztes und sehr wichtiger Hinweis darauf ist, dass die Datenträger Leistung für dieses Feature entscheidend ist. Da der Unterbrechungs-und Aktivierungsprozess das Schreiben und Lesen großer Datenmengen auf der Festplatte umfasst, wird dringend empfohlen, hierfür eine schnelle Festplatte zu verwenden. Solid-State-Laufwerke (SSDs) sind ideal für diese, und Sie sollten sicherstellen, dass die Windows-Auslagerungs Datei darauf gespeichert ist (wenn das Betriebssystem selbst nicht auf dem SSD installiert ist, konfigurieren Sie das Betriebssystem, um die Auslagerungs Datei zu verschieben).

Unabhängig davon, ob Sie eine SSD verwenden oder nicht, empfiehlt es sich auch, die Größe der Auslagerungs Datei zu beheben, um die Auslagerungs Daten ohne Dateigröße in diese zu schreiben. Die Größenänderung von Seiten Dateien kann auftreten, wenn das Betriebssystem Daten in der Auslagerungs Datei speichern muss, da Windows standardmäßig so konfiguriert ist, dass seine Größe nach Bedarf automatisch angepasst wird. Durch Festlegen der Größe auf einen festgelegten Wert können Sie die Größenänderung verhindern und die Leistung deutlich verbessern.

Zum Konfigurieren einer Dateigröße mit vorab fester Größe müssen Sie die ideale Größe berechnen, die davon abhängt, wie viele Standorte Sie anhalten und wie viel Arbeitsspeicher Sie verbrauchen. Wenn der Durchschnitt für einen aktiven Arbeitsprozess 200 MB beträgt und Sie über 500 Standorte auf den Servern verfügen, die angehalten werden, sollte die Auslagerungs Datei mindestens (200 \* 500) MB über der Basis Größe der Auslagerungs Datei (also "Base + 100 GB" in unserem Beispiel) sein.

**Hinweis** Wenn Standorte angehalten werden, verbrauchen Sie jeweils ungefähr 6 MB. in diesem Fall beträgt die Speicherauslastung, wenn alle Standorte angehalten werden, etwa 3 GB. In der Realität werden Sie jedoch wahrscheinlich nicht alle gleichzeitig angehalten.

 
## <a name="transport-layer-security-tuning-parameters"></a>Transport Layer Security Optimierungsparameter

Die Verwendung von Transport Layer Security (TLS) erfordert zusätzliche CPU-Kosten. Die teuerste Komponente von TLS ist der Aufwand für die Einrichtung einer Sitzungs Einrichtung, da Sie einen vollständigen Handshake umfasst. Durch die erneute Verbindungs Herstellung, Verschlüsselung und Entschlüsselung werden auch die Kosten addiert. Führen Sie die folgenden Schritte aus, um eine bessere Leistung zu erzielen:

-   Aktivieren von HTTP-Keep-Alives für TLS-Sitzungen. Dadurch werden die Einrichtungskosten der Sitzung vermieden.

-   Verwenden Sie ggf. Sitzungen, insbesondere bei nicht Keep-Alive-Datenverkehr.

-   Wenden Sie die Verschlüsselung selektiv nur auf Seiten oder Teile der Website an, die Sie benötigen, und nicht auf die gesamte Website.

**Hinweis**
-   Größere Schlüssel bieten mehr Sicherheit, aber Sie verbrauchen auch mehr CPU-Zeit.

-   Möglicherweise müssen nicht alle Komponenten verschlüsselt werden. Das Kombinieren von Plain HTTP und HTTPS kann jedoch dazu führen, dass nicht alle Inhalte auf der Seite sicher sind.

 
## <a name="internet-server-application-programming-interface-isapi"></a>Internet Server Application Programming Interface (ISAPI)

Für ISAPI-Anwendungen sind keine speziellen Optimierungsparameter erforderlich. Wenn Sie eine private ISAPI-Erweiterung schreiben, stellen Sie sicher, dass Sie für die Leistung und Ressourcenverwendung geschrieben wurde.

## <a name="managed-code-tuning-guidelines"></a>Optimierungs Richtlinien für verwalteten Code

Das integrierte Pipeline Modell in IIS 10,0 ermöglicht ein hohes Maß an Flexibilität und Erweiterbarkeit. Benutzerdefinierte Module, die in System eigenem oder verwaltetem Code implementiert werden, können in die Pipeline eingefügt werden, oder Sie können vorhandene Module ersetzen. Obwohl dieses Erweiterbarkeits Modell Komfort und Einfachheit bietet, sollten Sie sorgfältig vorgehen, bevor Sie neue verwaltete Module einfügen, die in globale Ereignisse eingebunden werden. Das Hinzufügen eines globalen verwalteten Moduls bedeutet, dass alle Anforderungen, einschließlich statischer Datei Anforderungen, verwalteten Code berühren müssen. Benutzerdefinierte Module sind anfällig für Ereignisse wie z. b. Garbage Collection. Außerdem erhöhen benutzerdefinierte Module erhebliche CPU-Kosten aufgrund des Marshalling von Daten zwischen nativem und verwaltetem Code. Wenn möglich, sollten Sie die Vorbedingung für das verwaltete Modul auf managedHandler festlegen.

Um eine bessere Leistung beim Systemstart zu erzielen, stellen Sie sicher, dass Sie die ASP.NET-Website vorkompilieren oder das IIS-Anwendungs Initialisierungs Feature nutzen, um die Anwendung zu bereinigen.

Wenn der Sitzungs Status nicht erforderlich ist, sollten Sie ihn für jede Seite deaktivieren.

Wenn es viele e/a-gebundene Vorgänge gibt, versuchen Sie, die asynchrone Version relevanter APIs zu verwenden, die Ihnen eine viel bessere Skalierbarkeit bietet.

Außerdem wird die Leistung der Website durch die ordnungsgemäße Verwendung des Ausgabe Caches gesteigert.

Wenn Sie mehrere Hosts ausführen, die ASP.net-Skripts im isolierten Modus (einen Anwendungs Pool pro Standort) enthalten, überwachen Sie die Speicherauslastung. Stellen Sie sicher, dass der Server über genügend RAM für die erwartete Anzahl von gleichzeitig ausgeführten Anwendungs Pools verfügt. Verwenden Sie ggf. mehrere Anwendungs Domänen anstelle mehrerer isolierter Prozesse.


## <a name="other-issues-that-affect-iis-performance"></a>Andere Probleme, die die IIS-Leistung beeinträchtigen

Die folgenden Probleme können sich auf die IIS-Leistung auswirken:

-   Installation von Filtern, die nicht zwischengespeichert werden können

    Die Installation eines Filters, bei dem es sich nicht um HTTP-Cache-fähig handelt, bewirkt, dass IIS die Zwischenspeicherung vollständig deaktiviert, was zu einer schlechten Leistung führt ISAPI-Filter, die vor "IIS6,0" geschrieben wurden, können dieses Verhalten verursachen.

-   CGI-Anforderungen (Common Gateway Interface)

    Aus Leistungsgründen wird die Verwendung von CGI-Anwendungen zum Verarbeiten von Anforderungen nicht mit IIS empfohlen. Das häufige erstellen und Löschen von CGI-Prozessen umfasst erheblichen Aufwand. Bessere Alternativen sind die Verwendung von FastCGI, ISAPI-Anwendungs Skripts und ASP-oder ASP.net-Skripts. Für jede dieser Optionen ist eine Isolation verfügbar.

# <a name="see-also"></a>Weitere Informationen
- [Leistungsoptimierung für Webserver](index.md) 
- [HTTP 1.1/2-Optimierung](http-performance.md)
