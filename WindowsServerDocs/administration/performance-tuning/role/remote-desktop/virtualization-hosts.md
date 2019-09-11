---
title: Leistungsoptimierung Remotedesktop Virtualisierungshosts
description: Leistungsoptimierung für Remotedesktop Virtualisierungshosts
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: HammadBu; VladmiS
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 24e3243d4e9791c8941729d396e0a96cd8b11a7d
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866440"
---
# <a name="performance-tuning-remote-desktop-virtualization-hosts"></a>Leistungsoptimierung Remotedesktop Virtualisierungshosts


Remotedesktop-Virtualisierungshost (RD-Virtualisierungshost) ist ein Rollen Dienst, der Szenarien für die virtuelle Desktop Infrastruktur (VDI) unterstützt und es mehreren gleichzeitigen Benutzern ermöglicht, Windows-basierte Anwendungen auf virtuellen Computern auszuführen, die auf einem Server unter ausgeführt werden. Windows Server 2016 und Hyper-V.

Windows Server 2016 unterstützt zwei Arten von virtuellen Desktops, persönlichen virtuellen Desktops und in einem Pool zusammengefasste virtuelle Desktops.

**In diesem Thema:**

-   [Allgemeine Überlegungen](#general-considerations)

-   [Leistungsoptimierungen](#performance-optimizations)

## <a name="general-considerations"></a>Allgemeine Überlegungen


### <a name="storage"></a>Speicher

Der Speicher ist der wahrscheinlichste Leistungsengpass, und es ist wichtig, die Größe Ihres Speichers so zu skaliert, dass die e/a-Auslastung ordnungsgemäß verarbeitet wird, die durch Zustandsänderungen virtueller Maschinen generiert wird. Wenn ein Pilotprojekt oder eine Simulation nicht durchführbar ist, empfiehlt es sich, eine Datenträger Spindel für vier aktive virtuelle Computer bereitzustellen. Verwenden Sie Datenträger Konfigurationen mit guter Schreibleistung (z. b. RAID 1 + 0).

Verwenden Sie ggf. die datenträgerdeduplizierung und Zwischenspeicherung, um die Datenträger-Lese Auslastung zu reduzieren und Ihre Speicherlösung zu aktivieren, um die Leistung zu beschleunigen, indem Sie einen signifikanten Teil des Images

### <a name="data-deduplication-and-vdi"></a>Datendeduplizierung und VDI

Die in Windows Server 2012 R2 eingeführte Datendeduplizierung unterstützt die Optimierung von geöffneten Dateien. Um virtuelle Computer zu verwenden, die auf einem deduplizierten Volume ausgeführt werden, müssen die Dateien der virtuellen Maschine auf einem separaten Host vom Hyper-V-Host gespeichert werden. Wenn Hyper-V und Deduplizierung auf dem gleichen Computer ausgeführt werden, werden die beiden Features für Systemressourcen in den Mittelwert geraten, was sich negativ auf die Gesamtleistung auswirkt.

Außerdem muss das Volume so konfiguriert werden, dass der deduplizierungstyp "Virtual Desktop Infrastructure (VDI)" verwendet wird. Sie können dies mithilfe Server-Manager  - konfigurieren&gt; ( **deduplizierungseinstellungen**für**Datei-und Speicherdienste**  - &gt; ), oder indem Sie den folgenden Windows PowerShell-Befehl verwenden:

``` syntax
Enable-DedupVolume <volume> -UsageType HyperV
```

> [!NOTE]
> Die datendeduplizierungsoptimierung von geöffneten Dateien wird nur für VDI-Szenarien mit Hyper-V unterstützt, die Remote Speicher über SMB 3,0 verwenden.

### <a name="memory"></a>Arbeitsspeicher

Die Auslastung des Server Arbeitsspeichers wird durch drei Hauptfaktoren gesteuert:

-   Betriebssystem Aufwand

-   Hyper-V-Dienst Aufwand pro virtuellem Computer

-   Jedem virtuellen Computer zugeordneter Arbeitsspeicher

Bei einer typischen workerworkerworkloads sollten virtuelle Gastcomputer, auf denen x86 Window 8 oder Windows 8.1 ausgeführt wird, ~ 512 MB Arbeitsspeicher als Baseline erhalten. Allerdings erhöht dynamischer Arbeitsspeicher wahrscheinlich den Arbeitsspeicher des virtuellen Gast Computers auf ungefähr 800 MB, abhängig von der Arbeitsauslastung. Für x64 werden ungefähr 800 MB gestartet, die auf 1024 MB erhöht werden.

Daher ist es wichtig, genügend Server Arbeitsspeicher bereitzustellen, um den Arbeitsspeicher zu erfüllen, der für die erwartete Anzahl von virtuellen Gast Computern benötigt wird, sowie eine ausreichende Menge an Arbeitsspeicher für den Server zuzulassen.

### <a name="cpu"></a>CPU

Wenn Sie die Serverkapazität für einen RD-Virtualisierungshostserver planen, hängt die Anzahl der virtuellen Computer pro physischem Kern von der Art der Arbeitsauslastung ab. Als Ausgangspunkt empfiehlt es sich, 12 virtuelle Computer pro physischem Kern zu planen und dann die entsprechenden Szenarios zum Überprüfen der Leistung und Dichte auszuführen. Eine höhere Dichte kann je nach den Besonderheiten der Arbeitsauslastung erreicht werden.

Es wird empfohlen, Hyperthreading zu aktivieren. Achten Sie jedoch darauf, dass Sie das Abonnement für die Überzeichnung basierend auf der Anzahl der physischen Kerne und nicht mit der Anzahl der logischen Prozessoren berechnen. Dadurch wird die erwartete Leistung auf CPU-Basis sichergestellt.

### <a name="virtual-gpu"></a>Virtuelle GPU

Microsoft RemoteFX für den RD-Virtualisierungshost bietet eine umfangreiche Grafik Darstellung für Virtual Desktop Infrastructure (VDI) über Host seitiges Remoting, eine rendererfassungs-Pipeline, eine hochgradig effiziente GPU-basierte Codierung, Drosselung basierend auf dem Client Aktivität und eine DirectX-aktivierte virtuelle GPU. RemoteFX für RD-Virtualisierungshost aktualisiert die virtuelle GPU von DirectX9 auf DirectX11. Außerdem wird die Benutzer Leistung verbessert, indem mehr Monitore mit höherer Auflösung unterstützt werden.

Die remotefx-DirectX11-Funktion ist über einen Software emulierten Treiber ohne Hardware-GPU verfügbar. Obwohl diese Software-GPU eine gute Leistung bietet, fügt die virtuelle remotefx-Grafikverarbeitungseinheit (vgpu) virtuellen Desktops eine Hardwarebeschleunigung hinzu.

Um die remotefx-vgpu auf einem Server zu nutzen, auf dem Windows Server 2016 ausgeführt wird, benötigen Sie einen GPU-Treiber (z. b. DirectX 11.1 oder WDDM 1,2) auf dem Host Server. Weitere Informationen zu GPU-angeboten, die mit RemoteFX für RD-Virtualisierungshost verwendet werden können, erhalten Sie von Ihrem GPU-Anbieter.

Wenn Sie die virtuelle remotefx-GPU in der VDI-Bereitstellung verwenden, variiert die Bereitstellungs Kapazität je nach Verwendungs Szenarien und Hardwarekonfiguration. Berücksichtigen Sie beim Planen der Bereitstellung Folgendes:

-   Anzahl von GPUs auf dem System

-   Video Speicherkapazität für die GPUs

-   Prozessor-und Hardware Ressourcen auf Ihrem System

### <a name="remotefx-server-system-memory"></a>System Arbeitsspeicher des remotefx-Servers

Für jeden virtuellen Desktop, der mit einer virtuellen GPU aktiviert ist, wird von remotefx der System Arbeitsspeicher im Gast Betriebssystem und auf dem remotefx-fähigen Server verwendet. Der Hypervisor gewährleistet die Verfügbarkeit von System Arbeitsspeicher für ein Gast Betriebssystem. Auf dem-Server muss von jedem virtuellen GPU-fähigen virtuellen Desktop die Systemspeicher Anforderung für den Hypervisor angekündigt werden. Beim Starten des virtuellen GPU-fähigen virtuellen Desktops reserviert der Hypervisor zusätzlichen System Arbeitsspeicher auf dem remotefx-fähigen Server für den vgpu-fähigen virtuellen Desktop.

Die Arbeitsspeicher Anforderung für den remotefx-fähigen Server ist dynamisch, weil der auf dem remotefx-fähigen Server belegte Arbeitsspeicher von der Anzahl der Monitore abhängig ist, die den vgpu-fähigen virtuellen Desktops zugeordnet sind, und der maximalen Auflösung für Diese Monitore.

### <a name="remotefx-server-gpu-video-memory"></a>Remotefx-Server-GPU-Videospeicher

Jeder virtuelle GPU-fähige virtuelle Desktop verwendet den Videospeicher in der GPU-Hardware auf dem Host Server, um den Desktop zu erzeugen. Zusätzlich zum Rendering wird der Videospeicher von einem Codec verwendet, um den gerenderten Bildschirm zu komprimieren. Der benötigte Speicherplatz basiert direkt auf der Anzahl der Monitore, die für den virtuellen Computer bereitgestellt werden.

Der reservierte Grafikspeicher variiert je nach Anzahl der Monitore und Bildschirmauflösung des Systems. Einige Benutzer benötigen möglicherweise eine höhere Bildschirmauflösung für bestimmte Aufgaben. Wenn alle anderen Einstellungen konstant bleiben, ist eine größere Skalierbarkeit mit niedrigeren Auflösungseinstellungen vorhanden.

### <a name="remotefx-processor"></a>Remotefx-Prozessor

Der Hypervisor plant den remotefx-fähigen Server und die virtuellen GPU-fähigen virtuellen Desktops auf der CPU. Im Gegensatz zum Systemspeicher gibt es keine Informationen, die sich auf zusätzliche Ressourcen beziehen, die remotefx für den Hypervisor freigeben muss. Der zusätzliche CPU-Overhead, der von remotefx in den virtuellen GPU-fähigen virtuellen Desktop integriert wird, bezieht sich auf die Ausführung des virtuellen GPU-Treibers und eines Remotedesktopprotokoll Stapels im Benutzermodus.

Auf dem remotefx-fähigen Server wird der Aufwand gesteigert, da das System einen zusätzlichen Prozess (rdvgm. exe) pro virtuellem GPU-aktiviertem virtuellen Desktop ausführt. Dieser Prozess verwendet den Grafikgeräte Treiber zum Ausführen von Befehlen auf der GPU. Der Codec verwendet auch die CPUs zum Komprimieren der Bildschirm Daten, die an den Client zurückgesendet werden müssen.

Mehr virtuelle Prozessoren bedeuten eine bessere Benutzer Leistung. Es wird empfohlen, mindestens zwei virtuelle CPUs pro virtuellem GPU-aktiviertem virtuellen Desktop zuzuordnen. Außerdem wird die Verwendung der x64-Architektur für virtuelle GPU-fähige virtuelle Desktops empfohlen, da die Leistung auf virtuellen x64-Computern besser als x86 Virtual Machines ist.

### <a name="remotefx-gpu-processing-power"></a>Remotefx-GPU-Verarbeitungsleistung

Für jeden virtuellen GPU-fähigen virtuellen Desktop wird ein entsprechender DirectX-Prozess auf dem remotefx-fähigen Server ausgeführt. Bei diesem Vorgang werden alle Grafikbefehle wiedergegeben, die vom virtuellen remotefx-Desktop auf die physische GPU empfangen werden. Bei der physischen GPU entspricht dies der gleichzeitigen Ausführung mehrerer DirectX-Anwendungen.

In der Regel sind Grafikgeräte und Treiber darauf abgestimmt, einige Anwendungen auf dem Desktop auszuführen. Remotefx dehnt die GPUs auf eindeutige Weise aus. Um zu messen, wie die GPU auf einem remotefx-Server funktioniert, wurden Leistungsindikatoren hinzugefügt, um die GPU-Antwort auf remotefx-Anforderungen zu messen.

Wenn eine GPU-Ressource wenig Ressourcen hat, dauert die Ausführung von Lese-und Schreibvorgängen für die GPU in der Regel lange. Mithilfe von Leistungsindikatoren können Administratoren vorbeugende Maßnahmen ergreifen, um die Möglichkeit zu Ausfallzeiten für die Endbenutzer zu vermeiden.

Die folgenden Leistungsindikatoren sind auf dem remotefx-Server verfügbar, um die Leistung der virtuellen GPU zu messen:

**Remotefx-Grafiken**

-   **Übersprungene Frames/Sekunde-unzureichende Client Ressourcen** Anzahl der pro Sekunde übersprungenen Frames aufgrund unzureichender Client Ressourcen

-   **Grafik Komprimierungs Verhältnis** Verhältnis der Anzahl von Bytes, die mit der Anzahl der Bytes codiert sind

**Remotefx-Stamm-GPU-Verwaltung**

-   **Verfügt TDRS in Server-GPUs** Gesamtanzahl der Zeitüberschreitung der TDR in der GPU auf dem Server

-   **Verfügt Virtuelle Computer, auf denen die** remotefx-Gesamtzahl der virtuellen Computer mit installierter remotefx 3D-Grafikkarte ausgeführt wird

-   **VRAM Verfügbare MB pro** GPU-Umfang des dedizierten Grafik Speichers, der nicht verwendet wird

-   **VRAM % Pro GPU** -Prozentsatz des dedizierten Grafik Speichers reserviert, der für remotefx reserviert ist

**Remotefx-Software**

-   **Erfassungs Rate für Monitor** \[1-4\] zeigt die remotefx-Erfassungs Rate für Monitore 1-4 an

-   **Komprimierungs Verhältnis** In Windows 8 als veraltet markiert und durch das **Grafik Komprimierungs Verhältnis** ersetzt

-   **Verzögerte Frames/Sek** . Anzahl von Frames pro Sekunde, bei denen Grafikdaten nicht innerhalb einer bestimmten Zeitspanne gesendet wurden

-   **GPU-Antwortzeit von Erfassung** Latenzzeit gemessen in der remotefx-Erfassung (in Mikrosekunden) für den Abschluss von GPU-Vorgängen

-   **GPU-Antwortzeit vom Rendering** Latenzzeit gemessen in remotefx-Rendering (in Mikrosekunden) für die Ausführung von GPU-Vorgängen

-   **Ausgabe Bytes** Gesamtanzahl von remotefx-Ausgabe bytes

-   **Warten auf Anzahl von Clients/SEK** . In Windows 8 als veraltet markiert und durch **Übersprungene Frames/Sekunde-unzureichende Client Ressourcen** ersetzt.

**Remotefx-vgpu-Verwaltung**

-   **Verfügt TDRS local to Virtual Machines** Gesamtzahl der TDRS, die auf diesem virtuellen Computer aufgetreten sind (TDRS, die der Server an die virtuellen Maschinen weitergegeben hat)

-   **Verfügt Von der Server** Gesamtzahl der TDRS, die auf dem Server aufgetreten sind und die an den virtuellen Computer weitergegeben wurden, weitergeleitete TDRS

**Vgpu-Leistung des virtuellen remotefx-Computers**

-   **Vorrats**  Die Gesamtanzahl der pro Sekunde auf dem Desktop der virtuellen Maschine zu rendernden Vorgänge in Sekunden.

-   **Vorrats Anzahl der ausgehenden** nachweisen/Sek. der von der virtuellen Maschine an die Server-GPU pro Sekunde gesendeten Vorgänge

-   **Vorrats Gelesene Bytes** /Sek. Gesamtanzahl der gelesenen Bytes vom remotefx-fähigen Server pro Sekunde

-   **Vorrats Sende Bytes/Sek** . Gesamtanzahl der an die remotefx-fähigen Server-GPU pro Sekunde gesendeten Bytes

-   **DMA Kommunikationspuffer durchschnittliche Wartezeit (Sek.** ) durchschnittliche Wartezeit (in Sekunden) für die Kommunikationspuffer

-   **DMA DMA-Puffer Wartezeit (** in Sekunden) ab dem Zeitpunkt, zu dem der DMA übermittelt wird, bis der Vorgang abgeschlossen ist

-   **DMA Warteschlangen** Länge DMA-Warteschlangen Länge für eine remotefx 3D-Grafikkarte

-   **Verfügt TDR-Timeouts pro** GPU-Anzahl von TDR-Timeouts, die pro GPU auf dem virtuellen Computer aufgetreten sind

-   **Verfügt TDR-Timeouts pro GPU** -Engine-Anzahl von TDR-Timeouts, die pro GPU-Engine auf dem virtuellen Computer aufgetreten sind

Zusätzlich zu den virtuellen GPU-Leistungsindikatoren von remotefx können Sie auch die GPU-Auslastung mithilfe des Prozess-Explorers Messen, der die Videospeicher Auslastung und die GPU-Auslastung anzeigt.

## <a name="performance-optimizations"></a>Leistungsoptimierungen

### <a name="dynamic-memory"></a>Dynamischer Arbeitsspeicher

Dynamischer Arbeitsspeicher ermöglicht eine effizientere Auslastung der Speicherressourcen des Servers, auf dem Hyper-V ausgeführt wird, indem der Arbeitsspeicher zwischen den laufenden virtuellen Maschinen verteilt wird. Der Arbeitsspeicher kann zwischen virtuellen Computern dynamisch neu zugeordnet werden, als Reaktion auf ihre veränderlichen Workloads.

Mit dynamischer Arbeitsspeicher können Sie die VM-Dichte mit den Ressourcen erhöhen, die Sie bereits besitzen, ohne Leistungseinbußen oder Skalierbarkeit zu beeinträchtigen. Das Ergebnis ist eine effizientere Verwendung kostspieliger Server Hardware Ressourcen, die in eine einfachere Verwaltung und geringere Kosten übersetzt werden können.

Bei Gastbetriebssystemen mit Windows 8 und höher mit virtuellen Prozessoren, die mehrere logische Prozessoren umfassen, sollten Sie den Kompromiss zwischen der Ausführung mit dynamischer Arbeitsspeicher in Erwägung gezogen werden, um die Speicherauslastung zu minimieren und dynamischer Arbeitsspeicher zur Verbesserung der Leistung zu deaktivieren. einer Anwendung, die Computer Topologie unterstützt. Eine solche Anwendung kann die Topologieinformationen nutzen, um Planungs-und Speicher Belegungs Entscheidungen zu treffen.

### <a name="tiered-storage"></a>Mehrschichtiger Speicher

Der RD-Virtualisierungshost unterstützt mehrstufigen Speicher für virtuelle Desktop Pools. Der physische Computer, der von allen in einem Pool zusammengefassten virtuellen Desktops in einer Sammlung gemeinsam genutzt wird, kann eine kleine Hochleistungsspeicher Lösung, z. b. ein gespiegeltes Solid-State-Laufwerk (SSD), verwenden. Die in einem Pool zusammengefassten virtuellen Desktops können auf kostengünstigeren, herkömmlichen Speicher wie z. b. RAID 1 + 0 platziert werden.

Der physische Computer sollte auf einem SSD abgelegt werden, weil die meisten Lese-e/a-Vorgänge von in einem Pool zusammengefassten virtuellen Desktops zum Verwaltungs Betriebssystem wechseln. Daher muss der Speicher, der vom physischen Computer verwendet wird, eine wesentlich höhere e/a-Lesevorgänge pro Sekunde unterstützen.

Diese Bereitstellungs Konfiguration gewährleistet die kostengünstige Leistung, wenn die Leistung benötigt wird. Die SSD bietet eine höhere Leistung auf einem Datenträger mit geringerer Größe (~ 20 GB pro Sammlung, abhängig von der Konfiguration). Herkömmlicher Speicher für in einem Pool zusammengefasste virtuelle Desktops (RAID 1 + 0) verwendet ca. 3 GB pro virtuellem Computer.

### <a name="csv-cache"></a>CSV-Cache

Failoverclustering in Windows Server 2012 und höher ermöglicht das Zwischenspeichern auf freigegebenen Clustervolumes (CSV). Dies ist äußerst vorteilhaft für in einem Pool zusammengefasste Sammlungen virtueller Desktops, bei denen der Großteil der Lese-e/a-Vorgänge vom Verwaltungs Betriebssystem stammt. Der CSV-Cache sorgt für eine höhere Leistung, da er Blöcke zwischenspeichert, die mehr als einmal gelesen werden, und Sie aus dem Systemspeicher übermittelt, wodurch die e/a-Vorgänge reduziert werden. Weitere Informationen zum CSV-Cache finden [Sie unter Aktivieren des CSV-Caches](http://blogs.msdn.com/b/clustering/archive/2012/03/22/10286676.aspx).

### <a name="pooled-virtual-desktops"></a>Gepoolte virtuelle Desktops

Standardmäßig werden für in einem Pool zusammengefasste virtuelle Desktops nach der Abmeldung eines Benutzers wieder in den ursprünglichen Zustand zurückgesetzt. alle Änderungen, die seit der letzten Benutzeranmeldung am Windows-Betriebssystem vorgenommen wurden, werden abgebrochen.

Obwohl es möglich ist, das Rollback zu deaktivieren, ist es immer noch eine vorübergehende Bedingung, da eine in einem Pool zusammengefasste Sammlung virtueller Desktops aufgrund verschiedener Updates der Vorlage für virtuelle Desktops neu erstellt wird.

Es ist sinnvoll, Windows-Features und-Dienste zu deaktivieren, die vom permanenten Zustand abhängen. Außerdem ist es sinnvoll, Dienste zu deaktivieren, die in erster Linie für nicht-Enterprise-Szenarios vorgesehen sind.

Jeder bestimmte Dienst sollte vor jeder breiten Bereitstellung angemessen ausgewertet werden. Im folgenden sind einige der folgenden Punkte zu beachten:

| Dienst                                      | Weshalb?                                                                                                                                                                                                      |
|----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Automatisch aktualisieren                                  | In einem Pool zusammengefasste virtuelle Desktops werden aktualisiert, indem die Vorlage für virtuelle Desktops neu erstellt wird.                                                                                                                          |
| Offline Dateien                                | Virtuelle Desktops sind immer online und über einen Netzwerk Ansichts Punkt verbunden.                                                                                                                         |
| Hintergrund-Debug                            | Dateisystem Änderungen werden verworfen, nachdem sich ein Benutzer abgemeldet hat (aufgrund eines Rollbacks zum ursprünglichen Zustand oder Neuerstellen der Vorlage für virtuelle Desktops, was zur erneuten Erstellung aller in einem Pool zusammengefassten virtuellen Desktops führt). |
| Ruhezustand oder Standbymodus                           | Kein solches Konzept für VDI                                                                                                                                                                                   |
| Fehlerüberprüfung für Speicher Abbild                        | Kein solches Konzept für in einem Pool zusammengefasste virtuelle Desktops. Ein in einem Pool zusammengestellter virtueller Desktop mit Fehlerüberprüfung wird vom ursprünglichen Zustand aus gestartet.                                                                                       |
| Automatische WLAN-Konfiguration                              | Es ist keine WLAN-Geräteschnittstelle für VDI vorhanden.                                                                                                                                                                 |
| Windows Media Player-Netzwerkfreigabe Dienst | Verbraucherorientierter Dienst                                                                                                                                                                                  |
| Startgruppen Anbieter                          | Verbraucherorientierter Dienst                                                                                                                                                                                  |
| Freigabe der Internet Verbindung                  | Verbraucherorientierter Dienst                                                                                                                                                                                  |
| Erweiterte Dienste von Media Center               | Verbraucherorientierter Dienst                                                                                                                                                                                  |
> [!NOTE]
> Diese Liste ist keine komplette Liste, da Änderungen sich auf die beabsichtigten Ziele und Szenarios auswirken. Weitere Informationen finden Sie unter [Hot Off the Backups, get it now, the Windows 8 VDI Optimization Script, courtesy of pfe!](http://blogs.technet.com/b/jeff_stokes/archive/2013/04/09/hot-off-the-presses-get-it-now-the-windows-8-vdi-optimization-script-courtesy-of-pfe.aspx).

 
> [!NOTE]
> Superfetch in Windows 8 ist standardmäßig aktiviert. Es ist VDI-fähig und sollte nicht deaktiviert werden. Superfetch kann die Arbeitsspeicher Nutzung durch die Freigabe von Arbeitsspeicher Seiten weiter reduzieren, was für VDI von Vorteil ist. Für in einem Pool zusammengefasste virtuelle Desktops, auf denen Windows 7 ausgeführt wird, sollte SuperFetch deaktiviert werden. für persönliche virtuelle Desktops, auf denen Windows 7 ausgeführt wird, sollte es jedoch weiterhin

 
