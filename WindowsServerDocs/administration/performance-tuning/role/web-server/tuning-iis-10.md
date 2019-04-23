---
title: Optimieren von IIS 10.0
description: Recommmendations für IIS 10.0-Webserver unter Windows Server-16 für die leistungsoptimierung
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: DavSo; Ericam; YaShi
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 16ea5c857d99e8a69f528e81178911236341dbb8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869851"
---
# <a name="tuning-iis-100"></a>Optimieren von IIS 10.0

Internet Information Services (IIS) 10.0 ist im Lieferumfang von Windows Server 2016. Er verwendet ein Prozessmodell wie IIS 8.5 und IIS 7.0. Ein Web Kernelmodustreiber (http.sys) empfängt und leitet HTTP-Anforderungen und erfüllt die Anforderungen aus dem Antwortcache. Arbeitsprozesse für URL-Subspaces registrieren und http.sys leitet die Anforderung an den entsprechenden Prozess (oder eine Reihe von Prozessen für Anwendungspools).

HTTP.sys ist verantwortlich für die Verwaltung von Datenbankverbindungen und anforderungsverarbeitung. Die Anforderung kann aus dem Cache HTTP.sys bereitgestellt oder an ein Arbeitsprozess für die weitere Verarbeitung übergeben werden. Mehrere Arbeitsprozesse können konfiguriert werden, die Isolation zu geringeren Kosten bereitstellt. Weitere Informationen zum Anfordern der Behandlung funktioniert, finden Sie in der folgende Abbildung:

![anforderungsverarbeitung in Iis 10.0](../../media/perftune-guide-iis-request-handling.png)

HTTP.sys enthält einen Cache für die Antwort. Wenn eine Anforderung einen Eintrag im Antwortcache übereinstimmt, sendet HTTP.sys die Cacheantwort direkt vom Kernelmodus. Einige webanwendungsplattformen, z. B. ASP.NET bieten Mechanismen, um in den Kernelmodus-Cache zwischengespeichert werden dynamische Inhalte zu aktivieren. Der Handler statische Dateien in IIS 10.0 speichert automatisch häufig angeforderte Dateien in http.sys.

Da ein Webserver Kernel-Modus und im Benutzermodus-Komponenten verfügt, müssen beide Komponenten für eine optimale Leistung optimiert werden. Aus diesem Grund enthält IIS 10.0 für eine bestimmte arbeitsauslastung optimieren Folgendes konfigurieren:

-   HTTP.sys vorhandenen und der zugehörigen Kernelmodus-cache

-   Arbeitsprozesse und IIS-Benutzermodus, einschließlich die Anwendungspoolkonfiguration

-   Bestimmte Optimierungsparameter, die Leistung auswirken

In den folgenden Abschnitten beschrieben, wie die Kernel-Modus und im Benutzermodus Aspekte von IIS 10.0 konfiguriert wird.

## <a name="kernel-mode-settings"></a>Kernelmodus-Einstellungen

HTTP.sys Leistungseinstellungen fallen in zwei große Kategorien: Zwischenspeichern von Verwaltung und Verbindung und die Anforderung. Alle registrierungseinstellungen werden unter den folgenden Registrierungseintrag gespeichert:

``` syntax
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters
```

**Beachten Sie**   , wenn der HTTP-Dienst bereits ausgeführt wird, Sie müssen neu starten, damit die Änderungen wirksam werden.

Â 

## <a name="cache-management-settings"></a>Einstellungen für die Verwaltung von Cache

Ein Vorteil, den HTTP.sys bietet ist ein Cache im Kernelmodus. Wenn die Antwort im Kernel-Modus-Cache ist, können Sie eine HTTP-Anforderung vollständig aus dem Kernelmodus ausgelagert, erfüllen, die wozu die erheblich die CPU-Kosten für die Anforderung verringert. Allerdings Cache Kernel-Modus von IIS 10.0 basiert auf physischen Speicher und die Kosten eines Eintrags ist der Arbeitsspeicher, den es belegt.

Ein Eintrag im Cache ist hilfreich, nur, wenn er verwendet wird. Der Eintrag verbraucht jedoch immer physischen Speichers, und zwar unabhängig davon, ob der Eintrag verwendet wird. Sie müssen die Nützlichkeit eines Elements im Cache (die einsparungen, können sie aus dem Cache dienen) und die Kosten (der physischer Speicher belegt wird) über die Lebensdauer des Eintrags auswerten, indem Sie in Betracht ziehen, die verfügbaren Ressourcen (CPU und Arbeitsspeicher) und der arbeitsauslastung Anforderungen an. HTTP.sys versucht, die beibehalten werden, nur nützlich, die aktiv auf Elemente in den Cache, aber Sie die Leistung des Webservers erhöhen können, durch die HTTP.sys-Caches für bestimmte Workloads optimieren.

Im folgenden sind einige nützliche Einstellungen für den Cache der HTTP.sys-Kernel-Modus:

-   **UriEnableCache** Standardwert: 1

    Ein Wert ungleich Null ermöglicht die Kernelmodus-Antwort und Fragment-caching. Für die meisten Workloads sollte der Cache aktiviert bleiben. Beachten Sie, den Cache deaktivieren, wenn Sie eine sehr schnelle Antwortzeiten und Fragment-caching erwarten.

-   **UriMaxCacheMegabyteCount** Standardwert: 0

    Ein NULL-Wert, der angibt, den maximalen Arbeitsspeicher, der in den Cache im Kernelmodus verfügbar ist. Der Standardwert 0 (null) kann das System automatisch anpassen, wie viel Arbeitsspeicher für den Cache verfügbar ist.

    **Beachten Sie** , um die Größe nur die maximale festlegt und das System möglicherweise nicht zulässig, den Cache auf die maximale Größe vergrößert werden.

    Â 

-   **UriMaxUriBytes** Standardwert: 262.144 Byte (256 KB)

    Die maximale Größe eines Eintrags im Kernelmodus-Cache. Antworten oder größer als dieser Fragmente werden nicht zwischengespeichert. Wenn Sie über genügend Speicher haben, erhöhen Sie den Grenzwert. Wenn Arbeitsspeicher beschränkt ist, und große Einträge Sie kleinere Versammeln sind, kann es hilfreich, verringern die Grenze sein.

-   **UriScavengerPeriod** Standardwert: 120 Sekunden

    Die HTTP.sys-Caches ist durch eine Aufräumdienst in regelmäßigen Abständen geprüft, und Einträge, die zwischen Aufräumdienst Überprüfungen nicht zugegriffen werden, werden entfernt. Festlegen des Zeitraums Aufräumdienst auf einen hohen Wert verringert die Anzahl der Aufräumdienst Scans. Allerdings kann die cachespeicherverwendung erhöhen, da ältere, weniger häufig verwendete Einträge im Cache verbleiben können. Festlegen von den Zeitraum zu niedrig bewirkt, dass häufigere Aufräumdienst Scans, und führen zu viele leert und codeänderung zwischenspeichern können.

## <a name="request-and-connection-management-settings"></a>Einstellungen für die Verwaltung von Anforderungs- und Verbindung

In Windows Server 2016 werden Verbindungen von "http.sys" automatisch verwaltet. Die folgenden registrierungseinstellungen nicht mehr verwendet:

-   **"MaxConnections"**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\MaxConnections
    ```

-   **IdleConnectionsHighMark**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\IdleConnectionsHighMark
    ```

-   **IdleConnectionsLowMark**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\IdleConnectionsLowMark
    ```

-   **IdleListTrimmerPeriod**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\IdleListTrimmerPeriod
    ```

-   **RequestBufferLookasideDepth**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\RequestBufferLookasideDepth
    ```

-   **InternalRequestLookasideDepth**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\InternalRequestLookasideDepth
    ```


## <a name="user-mode-settings"></a>Benutzermodus-Einstellungen

Die Einstellungen in diesem Abschnitt, das IISÂ 10.0 Worker Process Verhalten beeinflussen. Die meisten dieser Einstellungen finden Sie in der folgenden XML-Konfigurationsdatei:

%SystemRoot%\\system32\\inetsrv\\config\\applicationHost.config

Verwenden Sie Appcmd.exe, die IIS 10.0-Verwaltungskonsole, WebAdministration oder IISAdministration-PowerShell-Cmdlets, um diese zu ändern. Die meisten Einstellungen werden automatisch erkannt, und sie erfordern keinen Neustart der IIS 10.0-Arbeitsprozesse oder Webanwendungsserver. Weitere Informationen zu der Datei "applicationHost.config", finden Sie unter [Einführung in die Datei "applicationHost.config"](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig).


## <a name="ideal-cpu-setting-for-numa-hardware"></a>Ideale CPU-Einstellung für NUMA-hardware

Ab Windows 2016 wird unterstützt IIS 10.0 Automatische idealen CPU-Zuweisung für die Threadpool-Threads zur Verbesserung der Leistung und Skalierbarkeit auf NUMA-Hardware. Dieses Feature ist standardmäßig aktiviert und kann so konfiguriert werden, über den folgenden Registrierungsschlüssel:

``` syntax
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\InetInfo\Parameters\ThreadPoolUseIdealCpu
```

Dieses Feature aktiviert ist macht IIS Threadverwaltung ihr Möglichstes, um IIS Threadpool-Threads für alle CPUs in allen NUMA-Knoten, die basierend auf ihren aktuellen Auslastung gleichmäßig zu verteilen. Im Allgemeinen wird empfohlen, diese Standardeinstellung unverändert für NUMA-Hardware zu halten.

**Beachten Sie**   die ideale CPU-Einstellung unterscheidet sich vom Worker Prozess Einstellungen NUMA-Knoten Zuweisung (NumaNodeAssignment und NumaNodeAffinityMode) eingeführt, die [CPU-Einstellungen für einen Anwendungspool](https://www.iis.net/configreference/system.applicationhost/applicationpools/add/cpu). Die ideale CPU-Einstellung wirkt sich auf, wie IIS die Threadpool-Threads, verteilt, während die Worker Process Einstellungen NUMA-Knotens Zuordnung bestimmen, auf die NUMA-Knoten ein Arbeitsprozess gestartet wird.

## <a name="user-mode-cache-behavior-settings"></a>Benutzermodus-Verhalten cacheeinstellungen

Dieser Abschnitt beschreibt die Einstellungen, die Verhalten beim Zwischenspeichern im IISÂ 10.0 betreffen. Benutzermodus-Cache wird als Modul implementiert, die auf die globale caching-Ereignisse lauscht, die von der integrierten Pipeline ausgelöst werden. Um den Cache im Benutzermodus vollständig deaktivieren zu können, entfernen Sie das Modul FileCacheModule (cachfile.dll) aus der Liste der installierten Module im system.webServer/globalModules Konfigurationsabschnitt in der Datei "applicationHost.config".

**system.webServer/caching**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|Enabled|Deaktiviert die IIS-Benutzermodus-Cache bei Festlegung auf **"false"**. Wenn der Cache erreicht ist die Rate, sehr klein, Sie deaktivieren können den Cache, vollständig, um den Mehraufwand zu vermeiden, der der Pfad für den Cache zugeordnet ist. Deaktivieren den Benutzermodus-Cache wird nicht den Cache im Kernelmodus deaktiviert.|True|
|enableKernelCache|Deaktiviert den Kernelmodus-Cache bei Festlegung auf **"false"**.|True|
|maxCacheSize|Schränkt die Größe des IIS-Benutzermodus in die angegebene Größe in Megabyte an. IIS wird der Standardwert hängt vom verfügbaren Arbeitsspeicher. Wählen Sie den Wert, der sorgfältig häufig basierend auf der Größe des Satzes von Dateien und die Menge an Arbeitsspeicher oder die IIS-Prozess-Adressbereich zugegriffen.|0|
|maxResponseSize|Speichert Dateien bis zur angegebenen Größe an. Der tatsächliche Wert hängt von der Anzahl und Größe der größten Dateien in den Daten im Vergleich zu den verfügbaren Arbeitsspeicher ab. Große Caching können häufig angeforderte Dateien CPU-Auslastung, Datenträger zuzugreifen und zugehörige Latenz reduzieren.|262144|

## <a name="compression-behavior-settings"></a>Verhalten der komprimierungseinstellungen

IIS 7.0 beginnend werden statischen Inhalte standardmäßig komprimiert. Darüber hinaus ist die Komprimierung dynamischer Inhalte wird standardmäßig aktiviert, wenn die DynamicCompressionModule installiert ist. Die Komprimierung reduziert die Auslastung der Netzwerkbandbreite allerdings steigt die CPU-Nutzung. Komprimierter Inhalte wird nach Möglichkeit im Kernelmodus-Cache zwischengespeichert. 8.5 ab, kann IIS die Komprimierung für statische und dynamische Inhalte unabhängig voneinander kontrolliert werden. Statischer Inhalt bezieht sich in der Regel auf Inhalte, die nicht, z. B. GIF oder HTM-Dateien geändert wird verwendet wird. Dynamischer Inhalt wird in der Regel von Skripts oder Code auf dem Server, d. h. die ASP.NET-Seiten generiert. Sie können die Klassifizierung der bestimmte Erweiterung als statisch oder dynamisch anpassen.

Um die Komprimierung vollständig deaktivieren zu können, entfernen Sie "staticcompressionmodule" und DynamicCompressionModule aus der Liste der Module im Abschnitt "system.webServer/globalModules" in "applicationHost.config" ein.

**system.webServer/httpCompression**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|staticCompression-EnableCpuUsage<br><br>staticCompression-DisableCpuUsage<br><br>dynamicCompression-EnableCpuUsage<br><br>dynamicCompression-DisableCpuUsage|Aktiviert oder deaktiviert die Komprimierung fällt der aktuelle Prozentsatz CPU-Auslastung oberhalb oder unterhalb der angegebenen Grenzen.<br><br>Ab IIS 7.0 ist Komprimierung automatisch deaktiviert, wenn im stabilen Zustand CPU überschreitet den Schwellenwert deaktivieren steigt. Wenn CPU unter den aktivieren-Schwellenwert fällt, ist die Komprimierung aktiviert.|50, 100, 50 und 90 bzw.|
|Verzeichnis|Gibt das Verzeichnis, in dem komprimierte Versionen der statischen Dateien vorübergehend gespeichert und zwischengespeichert werden. Sollten Sie dieses Verzeichnis aus dem Systemlaufwerk verschieben, wenn diese regelmäßig zugegriffen wird.|%SystemDrive%\inetpub\temp\IIS temporary Compressed Files|
|doDiskSpaceLimiting|Gibt an, ob ein Grenzwert vorhanden ist. wie viel Speicherplatz für alle komprimierte Dateien belegt werden können. Komprimierte Dateien befinden sich im Komprimierungsverzeichnis, die angegeben wird die **Directory** Attribut.|True|
|maxDiskSpaceUsage|Gibt die Anzahl der Bytes der Speicherplatz auf dem Datenträger, die komprimierten Dateien im Komprimierungsverzeichnis an.<br><br>Diese Einstellung möglicherweise erhöht werden, wenn die Gesamtgröße aller komprimierten Inhalte zu groß ist.|100 MB|

**system.webServer/urlCompression**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|doStaticCompression|Gibt an, ob die statischer Inhalte komprimiert wird.|True|
|doDynamicCompression|Gibt an, ob dynamischer Inhalte komprimiert werden.|True|

**Beachten Sie** für Server mit IIS 10.0, die geringe durchschnittliche CPU-Auslastung haben, erwägen Sie die Aktivierung Komprimierung dynamischer Inhalte, insbesondere dann, wenn Antworten groß sind. Dies muss zuerst in einer testumgebung, um die Auswirkungen auf die CPU-Auslastung von der Baseline bewerten ausgeführt werden.


### <a name="tuning-the-default-document-list"></a>Optimieren die Liste der Standarddokumente

Das Standardmodul für das Dokument verarbeitet HTTP-Anforderungen für den Stamm eines Verzeichnisses und übersetzt sie in Anforderungen für eine bestimmte Datei, z. B. "default.htm" oder "Index.htm". Der Standardpfad für das Dokument im Durchschnitt durchlaufen AroundÂ 25 Prozent aller Anforderungen über das Internet. Dies variiert erheblich für jede Website einzeln. Wenn eine HTTP-Anforderung keinen Dateinamen angibt, sucht das Standardmodul für das Dokument die Liste der zulässigen Standarddokumente für jeden Namen eines im Dateisystem. Dies kann sich negativ auf die Leistung beeinträchtigen, insbesondere dann, wenn erreichen den Inhalt erforderlich ist, dass ein Netzwerk round Trip oder berühren einen Datenträger.

Sie können den Aufwand vermeiden, Standarddokumente selektiv zu deaktivieren und durch das reduzieren oder die Reihenfolge der Liste von Dokumenten. Für Websites, die ein Standarddokument verwenden, sollten Sie die Liste, nur die Standard-Dokumenttypen reduzieren, die verwendet werden. Sortieren Sie darüber hinaus die Liste, damit es beginnt mit die am häufigsten verwendete Dokument Standardnamen.

Sie können das Standardverhalten für das Dokument auf bestimmte URLs selektiv festlegen, durch das Anpassen der Konfigurations in eine standortkennzeichnung, in der Datei "applicationHost.config" oder durch eine web.config-Datei direkt in das Verzeichnis mit dem Inhalt einfügen. Dies ermöglicht einen Hybridansatz, der Standarddokumente nur, wo sie sind erforderlich und legt die Liste, um die richtige Datei benennen Sie für jede URL ermöglicht.

Um Standarddokumente vollständig zu deaktivieren, entfernen Sie DefaultDocumentModule aus der Liste der Module im Abschnitt "system.webServer/globalModules" in "applicationHost.config".

**system.webServer/defaultDocument**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|enabled|Gibt an, dass Standarddokumente aktiviert sind.|True|
|&lt;Dateien&gt; Element|Gibt den Dateinamen, die als Standarddokumente konfiguriert sind.|Die Standardliste ist "default.htm", "default.asp", "Index.htm", "Index.HTML", "Iisstart.htm" und "default.aspx".|

## <a name="central-binary-logging"></a>Zentrale binäre Protokollierung

Wenn die serversitzung zahlreiche URL-Gruppen, darunter verfügt, kann der Prozess der Hunderte von formatierten Protokolldateien für einzelne URL-Gruppen erstellen und Schreiben von Protokolldaten auf einem Datenträger schnell wertvolle CPU und Speicherressourcen, wodurch die Leistung nutzen und Skalierbarkeitsprobleme. Die zentrale binäre Protokollierung minimiert die Menge an Systemressourcen, die verwendet werden, für die Protokollierung, während gleichzeitig die Bereitstellung ausführliche Protokolldaten für Organisationen, die dies erfordern. Binary-Format-Protokolle analysieren, erfordert Nachbearbeitung Tools.

Sie können die zentralen binäre Protokollierung aktivieren, durch Festlegen des Attributs CentralLogFileMode CentralBinary und Festlegen der **aktiviert** Attribut **"true"**. Erwägen Sie den Speicherort der zentrale Protokolldatei deaktiviert die Systempartition und auf einem dedizierten Protokollierung-Laufwerk, um Konflikte zwischen System und Protokollierung von Aktivitäten zu vermeiden.

**system.applicationHost/log**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|centralLogFileMode|Gibt den Protokollierungsmodus für einen Server an. Ändern Sie diesen Wert auf CentralBinary zentralen binäre Protokollierung zu aktivieren.|Site|

**system.applicationHost/log/centralBinaryLogFile**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|enabled|Gibt an, ob zentrale binäre Protokollierung aktiviert ist.|False|
|Verzeichnis|Gibt das Verzeichnis, in denen Protokolleinträge geschrieben werden.|%SystemDrive%\inetpub\logs\LogFiles|


## <a name="application-and-site-tunings"></a>Und eine siteauflistung Feinabstimmungen

Die folgenden Einstellungen beziehen sich auf Application Pool und Standort Feinabstimmungen.

**system.applicationHost/applicationPools/applicationPoolDefaults**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|queueLength|Gibt an, die "http.sys" wie viele Anforderungen für einen Anwendungspool in die Warteschlange eingereiht werden vor zukünftige Anforderungen abgelehnt werden. Wenn der Wert dieser Eigenschaft überschritten wird, lehnt IIS nachfolgende Anforderungen mit einem 503-Fehler ab.<br><br>Erhöhen Sie diese für Anwendungen, die mit hoher Latenz Back-End-Datenspeichern zu kommunizieren, wenn der Fehler "503" festgestellt werden.|1000|
|enable32BitAppOnWin64|Bei "true", können eine 32-Bit-Anwendung auf einem Computer ausgeführt, die 64-Bit-Prozessoren enthalten.<br><br>Können Sie 32-Bit-Modus aktivieren, wenn der Speicherverbrauch relevant ist. Da Zeigergrößen und die Anweisung Größen kleiner sind, verwenden Sie 32-Bit-Anwendungen weniger Arbeitsspeicher als 64-Bit-Anwendungen. Der Nachteil von 32-Bit-Anwendungen auf einem 64-Bit-Computer ausgeführt wird, dass im Benutzermodus-Adressraum auf 4 GB begrenzt ist.|False|

**system.applicationHost/sites/VirtualDirectoryDefault**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|allowSubDirConfig|Gibt an, ob IIS nach "Web.config"-Dateien in Inhaltsverzeichnisse niedriger als die aktuelle Ebene sucht (True) oder sich nicht für die web.config-Dateien in die Inhaltsverzeichnisse ist niedriger als die aktuelle Ebene (False scheint). Durch anwendet, die eine einfache Einschränkung, die Konfiguration nur in virtuellen Verzeichnissen ermöglicht, IISÂ 10.0 können kennen, die, es sei denn,  **/ &lt;Namen&gt;.htm** ist ein virtuelles Verzeichnis, es sieht nicht für eine die Konfigurationsdatei. Wird übersprungen, die zusätzliche Dateivorgänge kann die Leistung von Websites, die eine sehr große Anzahl von nach dem Zufallsprinzip statischen Inhalte verfügen, erheblich verbessern.|True|

## <a name="managing-iis-100-modules"></a>Verwalten von IIS 10.0-Module

IIS 10.0 ist in mehrere, erweiterbare Module zur Unterstützung einer modularen Struktur berücksichtigt werden. Diese faktorisierung verfügt über ein kleines Geld. Für jedes Modul muss die integrierte Pipeline das Modul für jedes Ereignis aufrufen, die an das Modul relevant sind. Dies geschieht unabhängig davon, ob das Modul alle Maßnahmen arbeiten. Sie können die CPU-Zyklen und Arbeitsspeicher einsparen, indem entfernen alle Module, die für eine bestimmte Website nicht relevant sind.

Ein Webserver, der für einfache statische Dateien optimiert ist, sind nur die folgenden fünf Module: UriCacheModule, HttpCacheModule, StaticFileModule, AnonymousAuthenticationModule und HttpLoggingModule.

Um Module aus der Datei "applicationHost.config" zu entfernen, entfernen Sie alle Verweise auf das Modul aus den Abschnitten "system.webServer/handlers und System.Webserver/Modules" neben die Moduldeklaration in system.webServer/globalModules entfernen.

## <a name="classic-asp-settings"></a>Einstellungen für das klassische ASP

Die wichtigsten Kosten für die Verarbeitung von einer klassischen ASP-Anforderung umfasst das Initialisieren einer Skript-Engine, Kompilieren die angeforderte ASP-Skript in einer ASP-Vorlage und die Vorlage auf die Skript-Engine ausführen. Hängt von der Vorlage Ausführungskosten der Komplexität von dem angeforderten ASP-Skript kann klassische ASP-Modul für IIS-Skript-Engines in den Speicher und Cache-Vorlagen in Arbeitsspeicher und Datenträger Zwischenspeichern (nur, wenn die für in-Memory-Vorlagencache führt zu einem Überlauf) für Steigerung der Leistung in CPU-orientierten Szenarien.

Die folgenden Einstellungen werden verwendet, um die klassischen ASP-Vorlagen-Cache und Skript-Engine im Cache zu konfigurieren, und sie haben keine Auswirkungen ASP.NET-Einstellungen.

**system.webServer/asp/cache**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|diskTemplateCacheDirectory|Der Name des Verzeichnisses, das ASP verwendet, um kompilierten Vorlagen zu speichern, wenn in-Memory-Cache überläuft.<br><br>Empfehlung: Satz in ein Verzeichnis an, die nicht häufig verwendet, von denen z. B. ein Laufwerk, das mit dem Betriebssystem, den IIS-Protokoll, nicht gemeinsam genutzt wird, oder andere häufig Inhalte zugegriffen.|%SystemDrive%\inetpub\temp\ASP kompilierten Vorlagen|
|maxDiskTemplateCacheFiles|Gibt die maximale Anzahl kompilierter ASP-Vorlagen, die zwischengespeichert werden, können auf dem Datenträger an.<br><br>Empfehlung: Legen Sie auf der maximale Wert des 0x7FFFFFFF.|2000|
|scriptFileCacheSize|Dieses Attribut gibt die maximale Anzahl kompilierter ASP-Vorlagen, die zwischengespeichert werden können, im Arbeitsspeicher.<br><br>Empfehlung: Legen Sie auf mindestens so viele ist als die Anzahl der am häufigsten angefragten ASP-Skripts bereitgestellt werden, indem Sie einen Anwendungspool auf. Wenn möglich, um so viele ASP-Vorlagen können Arbeitsspeicherlimits festgelegt.|500|
|scriptEngineCacheMax|Gibt die maximale Anzahl der Skript-Engines, die im Cache beibehalten werden sollen.<br><br>Empfehlung: Legen Sie auf mindestens so viele ist als die Anzahl der am häufigsten angefragten ASP-Skripts bereitgestellt werden, indem Sie einen Anwendungspool auf. Legen Sie nach Möglichkeit auf so viele Skript-Engines wie das Arbeitsspeicherlimit zulässt.|250|

**system.webServer/asp/limits**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|processorThreadMax|Gibt die maximale Anzahl von Arbeitsthreads pro Prozessor fest, die ASP erstellen kann. Erhöhen Sie, wenn die aktuelle Einstellung ist nicht ausreichend, um die Last zu handhaben, die zu Fehlern führen, wenn sie Anforderungen verarbeitet oder dazu führen, dass unzureichende Auslastung von CPU-Ressourcen durchführen können.|25|

**system.webServer/asp/comPlus**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|executeInMta|Legen Sie auf **"true"** Wenn Fehler erkannt werden, während IIS ASP Content eingesetzt wird. Dies kann beispielsweise auftreten, wenn Sie mehrere isolierte Standorte hosten, in denen jeder Standort in einen eigenen Arbeitsprozess ausgeführt wird. Fehler werden in der Regel von COM+ in der Ereignisanzeige gemeldet. Diese Einstellung ermöglicht das Multithread-Apartment-Modell in ASP.|False|


## <a name="aspnet-concurrency-setting"></a>Einstellung für die Parallelität von ASP.NET

### <a name="aspnet-35"></a>ASP.NET 3.5
Standardmäßig beschränkt ASP.NET die Anforderung Parallelität im stabilen Zustand arbeitsspeichernutzung auf dem Server zu reduzieren. Hohe Parallelität Anwendungen müssen möglicherweise anpassen, einige Einstellungen, um die gesamtleistung zu verbessern. Sie können diese Einstellung in der Datei "aspnet.config" ändern:

``` syntax
<system.web>
  <applicationPool maxConcurrentRequestsPerCPU="5000"/>
</system.web>
```

Die folgende Einstellung ist nützlich, um die Ressourcen auf einem System vollständig zu nutzen:

-   **MaxConcurrentRequestPerCpu** Standardwert: 5000

    Diese Einstellung beschränkt die maximale Anzahl gleichzeitig ausgeführter ASP.NET-Anforderungen in einem System. Der Standardwert ist konservativ, um ASP.NET-Anwendungen den Speicherverbrauch zu verringern. Erhöhen Sie diese Grenze auf Systemen, die Anwendungen ausführen, die lange, synchrone e/a-Vorgänge ausführen. Andernfalls können Benutzer hohen Latenz auftreten, aufgrund von queuing oder die Anforderung ein Fehler aufgrund von überschreiten von Grenzwerten für die Warteschlange unter einer hohen Auslastung, wenn die Standardeinstellung verwendet wird.

### <a name="aspnet-46"></a>ASP.NET 4.6
Neben der Einstellung der MaxConcurrentRequestPerCpu bietet ASP.NET 4.7 auch Einstellungen, um die Leistung in den Anwendungen zu verbessern, die sich stark auf den asynchronen Vorgang stützen. Die Einstellung kann in der Datei "aspnet.config" geändert werden.

``` syntax
<system.web>
  <applicationPool percentCpuLimit="90" percentCpuLimitMinActiveRequestPerCpu="100"/>
</system.web>
```

-   **PercentCpuLimit** Standardwert: 90 asynchrone Anforderung weist einige Skalierbarkeitsprobleme auf, wenn eine große Last (über die Hardwarefunktionen) auf solchen Szenarios dargestellt wird. Das Problem ist aufgrund der Art der Zuordnung in asynchronen Szenarien. Unter diesen Umständen Zuordnung geschieht, wenn der asynchrone Vorgang gestartet wird, und es wird genutzt werden, nachdem es abgeschlossen wurde. Bis zu diesem Zeitpunkt dafür anzugeben, weshalb s sehr gut möglich, die Objekte in Generation 1 oder 2 von GC verschoben wurden. In diesem Fall erhöht sich die Last wird zeigen Anstieg bei Anforderung pro Sekunde (rps) bis zu einem Zeitpunkt. Sobald wir diesen Punkt übergeben, die Zeit im GC gestartet wird, um zu einem Problem werden und der RPS-Wert gestartet wird, um die dip-müssen Sie eine Skalierung beeinträchtigt. Um das Problem zu beheben, wenn die cpu-Auslastung PercentCpuLimit überschreitet, werden Anforderungen an die native ASP.NET-Warteschlange gesendet werden.
-   **PercentCpuLimitMinActiveRequestPerCpu** Standardwert: 100 CPU-Einschränkung (PercentCpuLimit Einstellung) basiert nicht auf Anzahl der Anforderungen, sondern auf wie teuer werden. Es kann daher weniger CPU-Intensive Anforderungen verursacht eine Sicherung in der systemeigenen Warteschlange mit keine Möglichkeit, abgesehen von der eingehenden Anforderungen leer. Zum Lösen dieser Problme kann PercentCpuLimitMinActiveRequestPerCpu verwendet werden, um sicherzustellen, dass vor Inkrafttreten der Einschränkung definierten sicherheitsschwellwerte in eine minimale Anzahl von Anforderungen verarbeitet werden.

## <a name="worker-process-and-recycling-options"></a>Arbeitsprozess und Wiederverwendung von Optionen

Sie können konfigurieren Sie Optionen für die Wiederverwendung von IIS-Arbeitsprozesse und praktische Lösungen akute Situationen oder Ereignisse ohne Eingreifen oder das Zurücksetzen von einem Dienst oder Computer bereitstellen. Solche Situationen und Ereignisse sind Speicherverluste, zunehmenden Auslastung des Arbeitsspeichers oder reagiert nicht oder im Leerlauf Arbeitsprozesse. Unter normalen Bedingungen recycling-Optionen möglicherweise nicht erforderlich und wiederverwenden kann deaktiviert werden, oder das System kann so konfiguriert werden, dass nur sehr selten wiederverwenden.

Sie können die Wiederverwendung von Prozessen für eine bestimmte Anwendung durch Hinzufügen von Attributen zum Aktivieren der **Wiederverwendung/PeriodicRestart** Element. Das Papierkorb-Ereignis kann durch verschiedene Ereignisse wie z.B. speichernutzung durch eine feste Anzahl von Anforderungen und einem festen Zeitraum ausgelöst werden. Wenn ein Arbeitsprozess wiederverwendet wird, die in der Warteschlange und ausgeführten Anforderungen werden ausgeglichen, und ein neuer Prozess ist für neue Anforderungen gleichzeitig gestartet. Die **Wiederverwendung/PeriodicRestart** Element ist pro Anwendung, was bedeutet, dass jedes Attribut in der folgenden Tabelle, auf einer Basis pro Anwendung partitioniert ist.

**system.applicationHost/applicationPools/ApplicationPoolDefaults/recycling/periodicRestart**

|Attribut|Beschreibung|Standard|
|--- |--- |--- |
|memory|Aktivieren Sie die prozesswiederverwendung, Auslastung des virtuellen Speichers überschreitet den festgelegten Grenzwert in Kilobyte. Dies ist eine nützliche Einstellung für 32-Bit-Computer, auf denen eine kleine, Adressraum von 2 GB zur Verfügung. Es kann helfen, Anforderungsfehler aufgrund von Out-of-Memory-Fehlern zu vermeiden.|0|
|privateMemory|Aktivieren Sie die prozesswiederverwendung, wenn private speicherbelegungen in Kilobyte einen angegebenen Grenzwert überschreiten.|0|
|requests|Aktivieren Sie die prozesswiederverwendung, nach einer bestimmten Anzahl von Anforderungen.|0|
|Zeit|Aktivieren Sie die prozesswiederverwendung, nach einem angegebenen Zeitraum.|29:00:00|


## <a name="dynamic-worker-process-page-out-tuning"></a>Dynamische Optimierung der Arbeitsprozess Seite-out

Ab Windows Server 2012 R2, bietet IIS die Möglichkeit, konfigurieren Arbeitsprozess angehalten wird, nachdem sie sich im Leerlauf für eine Weile (zusätzlich zur Option von "Terminate", die seit IIS 7) wurden.

Der Hauptzweck des im Leerlauf befindlichen Arbeitsthread Process Page-Out- und im Leerlauf befindlichen Arbeitsthread Prozess beenden Features ist speicherauslastung auf dem Server zu sparen, da es sich bei ein Standort viel Arbeitsspeicher nutzen kann, auch wenn es nur dort befindet überwacht. Abhängig von der Technologie, die auf der Website verwendet (statische Inhalte und ASP.NET Vs anderen Frameworks), der verwendete Arbeitsspeicher kann einen Wert an einer beliebigen Stelle von ca. 10 MB mit Hunderten von MB, und dies bedeutet, dass bei Ihrem Server mit viele Standorte, herauszufinden, die am effektivsten Einstellungen konfiguriert ist für Ihre Websites können Sie erheblich Leistung, aktive und angehaltene Websites verbessern.

Bevor wir in den Einzelheiten gehen, müssen wir bedenken, der Wenn keine arbeitsspeichereinschränkungen vorhanden sind, ist es wahrscheinlich am besten, legen Sie einfach die Standorte nicht anhalten oder beenden. Schließlich Thereâ s nur einen geringen Wert ein Arbeitsthread beendet verarbeiten, ist dies die einzige auf dem Computer.

**Beachten Sie**   Fall, dass die Website ausgeführt, instabil Code, z. B. Code einen Arbeitsspeicherverlust wird, oder andernfalls instabil, Festlegen der Website auf beendet im Leerlauf kann eine schnelle Alternative, um die Behebung des Fehlers Code. Dies nicht etwas, das Wir ermutigen, aber in einem aufschlüsseln, ist es möglicherweise besser, verwenden Sie diese Funktion als ein Mechanismus für die Bereinigung während eine dauerhaftere Lösung gearbeitet wird.\]

Â 

Zu berücksichtigen ist, sofern die Website viel Arbeitsspeicher belegen, verwendet und dann der Unterbrechung Prozess selbst eine gebührenfreie, dauert, da der Computer zum Schreiben der Daten, die von der Arbeitsprozess auf dem Datenträger verwendet. Wenn der Arbeitsprozess einen großen Speicherblock verwendet wird, kann die Anwendung dann anhalten teurer als die Kosten eines warten soll, bis er wieder hochgefahren sein.

Um das beste aus der Funktion "Worker Prozess anhalten" zu machen, müssen Sie Ihre Standorte in jeder Anwendungspool prüfen und entscheiden, die angehalten werden soll, die beendet werden soll, und die auf unbestimmte Zeit aktiv sein sollte. Für jede Aktion und jedem Standort müssen Sie herausfinden, ideale Timeout-Zeitraum.

Im Idealfall die Standorte, die Sie anhaltes oder Beendens konfigurieren, sind diejenigen, die Besucher tagtäglich, haben aber nicht genug, um dafür active ständig zu rechtfertigen. Hierbei handelt es sich normalerweise um Websites mit ca. 20 Besucher pro Tag oder weniger. Sie können die Datenverkehrsmustern mithilfe von Protokolldateien von der Website analysieren und berechnen den durchschnittlichen täglichen Datenverkehr.

Bedenken Sie, dass nach ein bestimmten Benutzer mit dem Standort verbunden ist, sie in der Regel darauf mindestens eine Weile möglicherweise weitere Abfragen bleiben werden, und daher nur gezählt wird jeden Tag Anfragen nicht genau die realen Datenverkehrsmuster wider. Rufen Sie genauere auch können ein Tool wie Microsoft Excel Sie um die durchschnittliche Zeit zwischen den Anforderungen zu berechnen. Zum Beispiel:

||Anforderungs-URL|Anforderungszeit|Delta|
|--- |--- |--- |--- |
|1|/SourceSilverLight/Geosource.web/grosource.html|10:01||
|2|/SourceSilverLight/Geosource.web/sliverlight.js|10:10|0:09|
|3|/SourceSilverLight/Geosource.web/clientbin/geo/1.aspx|10:11|0:01|
|4|/lClientAccessPolicy.xml|10:12|0:01|
|5|/ SourceSilverLight/GeosourcewebService/Service.asmx|10:23|0:11|
|6|/ SourceSilverLight/Geosource.web/GeoSearchServer...¦.|11:50|1:27|
|7|/Rest/Services/CachedServices/Silverlight_load_la...¦|12:50|1:00|
|8|/rest/Services/CachedServices/Silverlight_basemap...¦.|12:51|0:01|
|9|/ Rest/Services/DynamicService/Silverlight_basemap... ¦.|12:59|0:08|
|10|/rest/Services/CachedServices/Ortho_2004_cache.as...|13:40|0:41|
|11|/rest/Services/CachedServices/Ortho_2005_cache.js|13:40|0:00|
|12|/rest/Services/CachedServices/OrthoBaseEngine.aspx|13:41|0:01|

Der schwierigste Teil, ist jedoch, welche Einstellung angewendet wird, um sinnvoll sein, herauszufinden. In unserem Fall die Website wird eine Reihe von Anforderungen von Benutzern und die Tabelle oben zeigt, dass insgesamt 4 eindeutige Sitzungen in einem Zeitraum von 4 Stunden aufgetreten sind. Mit den Standardeinstellungen für Worker Process Unterbrechung des Anwendungspools würde die Website beendet werden, nachdem das standardmäßige Timeout von 20 Minuten, das einzelnen Benutzer bedeutet, dass den Standort Spin-Up-Zyklus auftreten würde. Dadurch einen idealen Kandidat für die Unterbrechung der Worker-Prozess, da für den Großteil der Zeit, die Website im Leerlauf ist, und sparen Sie Ressourcen und ermöglichen Benutzern das Erreichen des Standorts fast sofort würde Anwendung anhalten.

Letzten und sehr wichtig, sich zu diesem ist, dass die datenträgerleistung von entscheidender Bedeutung, damit diese Funktion ist. Da die Unterbrechung und der Aktivierungsproxy-Prozess beinhalten schreiben und Lesen umfangreicher Daten auf die Festplatte wird dringend empfohlen mithilfe einer schnellen Festplatte für diese. Solid-State-Laufwerken (SSDs) sind ideal und dringend empfohlen, hierfür, und stellen Sie sicher, dass die Windows-Auslagerungsdatei auf gespeichert wird (wenn das Betriebssystem selbst nicht auf die SSD-Datenträger installiert ist, konfigurieren Sie das Betriebssystem für die Auslagerungsdatei dorthin verschieben).

Ob Sie eine SSD oder nicht verwenden, empfehlen wir, auch beheben Sie die Größe der Auslagerungsdatei von aufzunehmen, die Seite "-Out-Daten in den sie schreiben, ohne die Datei-Größe zu. Größe der Auslagerungsdatei kann auftreten, wenn das Betriebssystem muss zum Speichern von Daten in die Auslagerungsdatei, da standardmäßig Windows so konfiguriert ist für die automatische Anpassung von dessen Größe basierend auf muss. Durch Festlegen der Größe auf einen festen, können Sie verhindern, Ändern der Größe und Leistung deutlich verbessern.

Um eine Dateigröße vor fixierten Seite konfigurieren zu können, müssen Sie zum Berechnen der idealen Größe, wie viele Sie Standorte abhängig vom angehalten, und wie viel Arbeitsspeicher belegen. Wenn der Durchschnitt 200 MB für eine aktive Arbeitsprozess beträgt 500 Websites auf Servern, die angehalten werden, werden Ihnen ein, und die Auslagerungsdatei mindestens muss (200 \* 500) MB während der Basisgröße entsprechen der Auslagerungsdatei (also Basis + 100 GB in unserem Beispiel).

**Beachten Sie** bei Websites angehalten werden, werden belegen ca. 6 MB, speicherauslastung, wenn alle Standorte angehalten wurden in unserem Fall ca. 3 GB wäre. In der Praxis jedoch sind wahrscheinlich nie diesem Beispiel werden sie alle zur gleichen Zeit angehalten wurden.

 
## <a name="transport-layer-security-tuning-parameters"></a>Transport Layer Security Optimierungsparameter

Die Verwendung von Transport Layer Security (TLS) erzwingt die zusätzliche CPU-Kosten. Die teuerste Komponente von TLS ist die Kosten für eine sitzungseinrichtung herstellen, da sie einen vollständigen Handshake umfasst. Erneute Verbindung, Verschlüsselung und Entschlüsselung können Sie auch hinzufügen, auf die Kosten. Führen Sie für eine bessere Leistung für TLS folgende Schritte aus:

-   Aktivieren von HTTP-Keep-Alive für TLS-Sitzungen. Dadurch werden die Kosten für die Einrichtung einer Sitzung.

-   Wiederverwenden von Sitzungen bei Bedarf, vor allem bei nicht-Keep-alive-Datenverkehr.

-   Anwenden der Verschlüsselung selektiv nur für Seiten oder Teile der Site, die sie stattdessen auf die gesamte Website benötigen.

**Hinweis**
-   Größere Schlüssel bieten mehr Sicherheit, aber es auch mehr CPU-Zeit.

-   Alle Komponenten müssen u. u. nicht verschlüsselt werden. Allerdings kann die Mischen von einfachen HTTP und HTTPS führen, in einem Popupfenster angezeigt, die Warnung, dass nicht alle Inhalte auf der Seite sicher ist.

 
## <a name="internet-server-application-programming-interface-isapi"></a>Internet Server Application Programming Interface (ISAPI)

Für die ISAPI-Anwendungen sind keine besonderen Parameter für die Optimierung erforderlich. Wenn Sie eine private ISAPI-Erweiterung schreiben, stellen Sie sicher, dass es für Leistung und Ressourcenverwendung geschrieben wird.

## <a name="managed-code-tuning-guidelines"></a>Verwalteter Code Leitfaden für die Optimierung

Das Modell der integrierten Pipeline in IIS 10.0 ermöglicht ein hohes Maß an Flexibilität und Erweiterbarkeit. Benutzerdefinierte Module, die in systemeigenem oder verwaltetem Code implementiert werden, die in der Pipeline eingefügt werden können, oder sie können vorhandene Module ersetzen. Obwohl dieses Erweiterbarkeitsmodell benutzerfreundlichkeit und Einfachheit bietet, sollten Sie vorsichtig, bevor Sie die neue verwaltete Module, die einklinken in globale Ereignisse einfügen. Hinzufügen ein globales verwaltetes Moduls bedeutet, dass alle Anforderungen, einschließlich der Anforderungen für statische Dateien, zugreifen müssen, verwalteten Code. Benutzerdefinierte Module sind anfällig für Ereignisse, z. B. Garbagecollection. Darüber hinaus fügen Sie benutzerdefinierte Module erhebliche CPU-Kosten aufgrund von Marshallen von Daten zwischen systemeigenen und verwalteten Code hinzu. Wenn möglich, sollten Sie Vorbedingung auf ManagedHandler für das verwaltete Modul festlegen.

Stellen Sie sicher, dass Sie das ASP.NET Website nutzen IIS Anwendungsinitialisierung Feature oder um die Anwendung befassen vorkompilieren, rufen Sie eine bessere Leistung des Kaltstarts verbessert.

Stellen Sie der Sitzungszustand nicht erforderlich ist, sicher, dass Sie sie für jede Seite deaktivieren.

Treten viele e/a-bezogener Vorgänge, die versuchen, asynchrone Version der relevanten APIs zu verwenden, wodurch Sie viel bessere Skalierbarkeit erhalten wird.

Auch ordnungsgemäß mit Ausgabecache wird auch die Leistung Ihrer Website zu steigern.

Wenn Sie mehrere Hosts, die ASP.NET-Skripts im isolierten Modus (einen Anwendungspool pro Website) enthalten ausführen, Überwachen der arbeitsspeicherauslastung. Stellen Sie sicher, dass der Server über ausreichend Arbeitsspeicher für die erwartete Anzahl gleichzeitig ausgeführter Anwendungspools verfügt. Erwägen Sie die Verwendung von mehreren Anwendungsdomänen statt mehrere isolierte Prozesse.


## <a name="other-issues-that-affect-iis-performance"></a>Andere Probleme, IIS die Leistung auswirken

Die folgenden Probleme können IIS-Leistung beeinflussen:

-   Installation von Filtern, die keine Cache-fähig sind.

    Die Installation eines Filters, der nicht HTTP-Cache-fähigen bewirkt, dass IIS vollständig zu deaktivieren, Zwischenspeicherung, was zu Leistungseinbußen führt. ISAPI-Filter, die vor IISÂ 6.0 geschrieben wurden, können dieses Verhalten verursachen.

-   Common Gateway Interface (CGI)-Anforderungen

    Aus Leistungsgründen wird die Verwendung von CGI-Anwendungen für Anforderungen mit IIS nicht empfohlen. Häufig erstellen und Löschen von CGI-Prozesse umfasst das wesentlich höheren Leistungsaufwand. Bessere Alternativen umfassen die Verwendung von FastCGI, Skripts der ISAPI-Anwendung und ASP- oder ASP.NET-DEBUGGEN, Skripts. Isolation ist für jede dieser Optionen verfügbar.

# <a name="see-also"></a>Siehe auch
- [Web-Server zur leistungsoptimierung](index.md) 
- [HTTP 1.1/2-Optimierung](http-performance.md)
