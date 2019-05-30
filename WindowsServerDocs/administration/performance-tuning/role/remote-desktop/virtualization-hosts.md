---
title: Remotedesktop-Virtualisierungshost-Hosts die Optimierung der Leistung
description: Leistungsoptimierung für Remotedesktop-Virtualisierungshost-Hosts
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: HammadBu; VladmiS
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 0aa359644f5e9bf85f4e013e6571276716ed0218
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266615"
---
# <a name="performance-tuning-remote-desktop-virtualization-hosts"></a>Remotedesktop-Virtualisierungshost-Hosts die Optimierung der Leistung


Remote Desktop-Virtualisierungshost (RD-Virtualisierungshost) ist ein Rollendienst, der Virtual Desktop Infrastructure (VDI)-Szenarios unterstützt und kann von mehreren gleichzeitigen Benutzern führen Sie auf einem Server mit Windows-basierten Anwendungen auf virtuellen Computern, die gehostet werden WindowsServer 2016 und Hyper-V.

Windows Server 2016 unterstützt zwei Arten von virtuellen Desktops, persönliche virtuelle Desktops und in einem Pool zusammengefasste virtuelle Desktops.

**In diesem Thema:**

-   [Allgemeine Überlegungen](#general)

-   [Leistungsoptimierungen](#perfopt)

## <a href="" id="general"></a>Allgemeine Überlegungen


### <a name="storage"></a>Speicher

Speicher ist die am wahrscheinlichsten Leistungsengpass, und es ist wichtig, die Größe Ihres Speichers, um die e/a-Last ordnungsgemäß zu behandeln, die von VM-Zustandsänderungen generiert wird. Wenn eines Pilotprojekts oder einer Simulation nicht möglich ist, ist eine gute Richtlinie eine Datenträger-Spindel für vier aktive virtuelle Maschinen bereitstellen. Verwenden Sie die Datenträgerkonfigurationen, gute schreibleistung (z. B. RAID 1 + 0).

Bei Bedarf verwenden Sie die Festplattendeduplizierung und das Zwischenspeichern der Datenträgerlesevorgänge, die Last zu reduzieren und Ihre speicherlösung, die Sie die Leistung zu steigern, durch das Zwischenspeichern eines beträchtlicher Teils des Bilds zu aktivieren.

### <a name="data-deduplication-and-vdi"></a>Die Datendeduplizierung und VDI

In Windows Server 2012 R2 eingeführt wurde, unterstützt die Datendeduplizierung die Optimierung von geöffneten Dateien an. Um virtuelle Maschinen auf einem deduplizierten Volume verwenden zu können, müssen Dateien der virtuellen Maschine auf einem separaten Host, auf dem Hyper-V-Host gespeichert werden. Wenn Hyper-V und Deduplizierung auf demselben Computer ausgeführt werden, werden die beiden Features für Ressourcen konkurrieren und sich negativ auf die gesamtleistung auswirken.

Das Volume muss auch konfiguriert werden, um den optimierungstyp "Datendeduplizierung" Virtual Desktop Infrastructure (VDI) "" zu verwenden. Sie können dies mithilfe von Server-Manager konfigurieren (**Datei- und Speicherdienste**  - &gt; **Volumes**  - &gt; **Deduplizierungseinstellungen**) oder mithilfe des folgenden Windows PowerShell Befehl verwenden:

``` syntax
Enable-DedupVolume <volume> -UsageType HyperV
```

> [!Note]
> Daten deduplizierungsoptimierung von geöffneten Dateien wird nur für VDI-Szenarien mit Hyper-V mithilfe von Remotespeicher über SMB 3.0 unterstützt.

### <a name="memory"></a>Arbeitsspeicher

Speicherauslastung des Servers wird durch drei Hauptfaktoren gesteuert:

-   Betriebssystem-Mehraufwand

-   Hyper-V-Dienst Mehraufwand pro virtuellem Computer

-   Speichermenge für die einzelnen virtuellen Computer

Bei einer typischen Knowledge Worker-Workload Computer virtuellen Gast ausgeführten X86, die Windows 8 oder Windows 8.1 ~ 512 MB Arbeitsspeicher als Baseline zugewiesen werden soll. Dynamischer Arbeitsspeicher erhöht sich jedoch wahrscheinlich auf der Gast-VM-Arbeitsspeicher, um ungefähr 800 MB, je nach arbeitsauslastung aus. X64 finden Sie wir über eine 800 MB ab, auf 1.024 MB erhöht.

Aus diesem Grund ist es wichtig, geben Sie genügend Server-Speicher den Arbeitsspeicher zu erfüllen, der die erwartete Anzahl von virtuellen Gastcomputern erforderlich ist, sowie eine ausreichende Menge an Arbeitsspeicher für den Server erlauben.

### <a name="cpu"></a>CPU

Wenn Sie Server-Kapazität für einen Remotedesktop-Virtualisierungshost-Server planen, hängt die Anzahl von virtuellen Computern pro physischen Kern von der Art der Workload. Als Ausgangspunkt ist es sinnvoll, 12 virtuelle Computer pro physischen Kern, und führen Sie die geeigneten Szenarien aus, um Leistung und Dichte zu überprüfen. Höherer Dichte kann je nach den Besonderheiten der arbeitsauslastung erreicht werden.

Es wird empfohlen, aktivieren die hyper-threading, aber Achten Sie darauf, um das Verhältnis überzähliger Abonnements basierend auf der Anzahl der physischen Kerne und nicht die Anzahl der logischen Prozessoren zu berechnen. Dadurch wird die verlässliches Maß an Leistung auf einer Basis pro CPU.

### <a name="virtual-gpu"></a>Virtual GPU

Microsoft RemoteFX für RD-Virtualisierungshost bietet eine reichhaltige Grafiken für Virtual Desktop Infrastructure (VDI) durch hostseitiges Remoting, eine Pipeline Render-Capture-Codierung, ein hocheffizientes GPU-basierte codieren, Drosselung basierend auf der Clientleistung Aktivität und eine DirectX-fähiges virtuellen GPU. RemoteFX für RD-Virtualisierungshost aktualisiert DirectX9 die virtuelle GPU auf DirectX11. Außerdem wird die benutzerfreundlichkeit verbessert, indem mehrere Monitore mit höherer Auflösung unterstützt.

Die RemoteFX DirectX11-benutzererfahrung ist ohne eine Hardware-GPU, über einen Software emulierte Treiber zur Verfügung. Obwohl diese Software GPU eine gute Erfahrung bietet, fügt der RemoteFX virtuellen Grafikprozessor (VGPU) eine hardwarebeschleunigt Erfahrung mit virtuellen Desktops.

Um die RemoteFX VGPU-Benutzeroberfläche auf einem Server unter Windows Server 2016 nutzen zu können, benötigen Sie einen GPU-Treiber (z. B. DirectX11.1 oder WDDM 1.2) auf dem Host. Weitere Informationen über die Verwendung mit RemoteFX für RD-Virtualisierungshost GPU-Angebote wenden Sie sich an Ihren Anbieter für GPU.

Wenn Sie in der VDI-Bereitstellung die virtuelle RemoteFX-GPU verwenden, wird die Bereitstellungskapazität basierend auf Szenarien für die Verwendung und Konfiguration der Systemhardware variieren. Wenn Sie die Bereitstellung planen, beachten Sie Folgendes:

-   Anzahl von GPUs in Ihrem system

-   Die GPUs Videospeicher Kapazität

-   Prozessor und Hardware-Ressourcen auf Ihrem system

### <a name="remotefx-server-system-memory"></a>RemoteFX-Server-System-Arbeitsspeicher

Für jeden virtuellen Desktop, einen virtuellen Grafikprozessor aktiviert verwendet der RemoteFX Systemspeicher in Gast-Betriebssystems und die RemoteFX-fähigen Server. Der Hypervisor garantiert die Verfügbarkeit des Systemspeichers für Gast-Betriebssystem. Auf dem Server muss jeder virtueller GPU-fähigen virtueller Desktop die Systemanforderungen für die Arbeitsspeicher auf den Hypervisor angekündigt werden soll. Wenn es sich bei der virtuelle GPU-fähigen virtuelle Desktop gestartet wird, reserviert der Hypervisor zusätzliche Systemspeicher auf dem RemoteFX-fähigen Server für den VGPU-fähigen virtuellen Desktop.

Die speicheranforderungen der RemoteFX-fähigen Server ist dynamisch, da die Größe des Speicherplatzes, die auf dem RemoteFX-fähigen Server hängt von der Anzahl der Monitore ist, die die VGPU-fähigen virtuellen Desktops und die maximale Auflösung für zugeordnet sind Diese Monitore.

### <a name="remotefx-server-gpu-video-memory"></a>RemoteFX-Servers video GPU-Arbeitsspeicher

Jeder virtueller GPU-fähigen virtueller Desktop verwendet den Videospeicher in der GPU-Hardware, auf dem Host, um den Desktop zu rendern. Zusätzlich zu rendern, wird den Videospeicher von einem Codec verwendet, um den gerenderten Bildschirm zu komprimieren. Der Umfang des benötigten Speichers basiert direkt auf der Menge der Monitore, die mit dem virtuellen Computer bereitgestellt werden.

Das video reservierten Arbeitsspeichers variiert basierend auf der Anzahl von Monitoren und die Auflösung des Bildschirms. Einige Benutzer möglicherweise eine höhere Bildschirmauflösung für bestimmte Aufgaben. Es gibt bessere Skalierbarkeit mit niedriger auflösungseinstellungen auf, wenn alle anderen Einstellungen unverändert bleiben.

### <a name="remotefx-processor"></a>RemoteFX-Prozessor

Der Hypervisor plant der RemoteFX-fähigen Server und die virtuellen GPU-fähigen virtuellen Desktops auf der CPU. Im Gegensatz zu den Arbeitsspeicher des Systems gibt es keine Informationen, die zu zusätzlichen Ressourcen beziehen, die RemoteFX mit dem Hypervisor freigeben muss. Für die Ausführung der virtuellen GPU-Treiber und einer Benutzermodus-Remote Desktop Protocol-Stack bezieht sich der zusätzlichen CPU-overhead, der RemoteFX in den virtuellen GPU-fähigen virtuellen Desktop hergestellt wird.

Auf dem RemoteFX-fähigen Server ist der Mehraufwand erhöht, da das System einen weiteren Vorgang (rdvgm.exe) ausgeführt wird pro virtuellen GPU-fähigen virtuellen Desktop. Dieser Prozess verwendet den Gerätetreiber von Grafiken zum Ausführen von Befehlen auf der GPU. Der Codec verwendet auch die CPUs für das Komprimieren der Daten, die an den Client zurückgesendet werden müssen.

Weitere virtuellen Prozessoren bedeuten eine bessere benutzererfahrung. Es wird empfohlen, mindestens zwei virtuelle CPUs pro virtuellen GPU-fähigen virtuellen Desktop zuweisen. Wir empfehlen auch die Verwendung der X64 Architektur für die virtuellen GPU-fähige virtuelle Desktops da die Leistung auf virtuelle Computern besser im Vergleich zu X86 X64 virtuelle Computer.

### <a name="remotefx-gpu-processing-power"></a>RemoteFX GPU-verarbeitungsleistung

Ist für jeden virtuellen GPU-fähigen virtuellen Desktop gibt es einen entsprechenden DirectX-Prozess auf dem RemoteFX-fähigen Server ausgeführt. Dieser Vorgang gibt die Grafikbefehle, die von den virtuellen RemoteFX-Desktop auf die physischen GPU empfangen wieder. Für die physischen GPU verwenden ist es gleich mehrere DirectX-Anwendungen gleichzeitig ausgeführt.

In der Regel Grafikgeräte und Treiber angepasst, sodass Sie einige Anwendungen auf dem Desktop ausgeführt. RemoteFX wird gestreckt, die GPUs auf eindeutige Weise verwendet werden. Um messen, wie die GPU auf eine RemoteFX-Server ausgeführt wird, wurden die Leistungsindikatoren zum Messen der GPU-Antwort auf Anforderungen für RemoteFX hinzugefügt.

In der Regel, wenn Sie eine GPU-Ressource nicht über genügend Ressourcen ist, wird Lese- und Schreibvorgänge auf der GPU-dauert sehr lange abgeschlossen. Mithilfe von Leistungsindikatoren können Administratoren vorbeugende Aktion ausführen, verhindern dadurch, dass keine Ausfallzeiten für ihre Endbenutzer.

Die folgenden Leistungsindikatoren sind verfügbar, auf dem RemoteFX-Server für die virtuellen GPU-Leistung zu messen:

**RemoteFX-Grafiken**

-   **Frames übersprungen/Sekunde - nicht genügend Clientressourcen** Anzahl von Frames pro Sekunde aufgrund unzureichender Clientressourcen übersprungen

-   **Grafiken Komprimierungsverhältnis** Verhältnis der Anzahl von Bytes codiert, um die Anzahl der Byte-Eingabe

**RemoteFX-Stamm GPU-Verwaltung**

-   **Ressourcen: Von TDRs in Server-GPUs** Gesamtzahl der Fälle, in denen die TDR in die GPU auf dem Server ein auftritt Timeout

-   **Ressourcen: Virtuelle Computer mit RemoteFX** Gesamtzahl der virtuellen Computer, die den RemoteFX 3D Video Adapter installiert haben.

-   **VRAM: Verfügbare MB pro GPU** dedizierte Videospeicher, die nicht verwendet wird

-   **VRAM: Reservierte % pro GPU** Prozent der dedizierten Grafikspeicher, der für RemoteFX reserviert wurde

**RemoteFX-software**

-   **Erfassen der Rate für Monitor** \[1-4\] zeigt die Rate der RemoteFX-Erfassung für Monitore 1 bis 4

-   **Komprimierungsverhältnis** Deprecated in Windows 8 und durch ersetzt **Komprimierungsverhältnis von Grafiken**

-   **Frames pro Sekunde verzögert** Anzahl von Frames pro Sekunde, in denen Grafikdaten in einer bestimmten Zeitspanne nicht gesendet wurde,

-   **GPU-Antwortzeit aus Capture** Latenzzeit ermittelt in RemoteFX erfassen (in Mikrosekunden) für die GPU-Vorgängen noch nicht abgeschlossen

-   **GPU-Antwortzeit von Render** Latenzzeit ermittelt in RemoteFX Render (in Mikrosekunden) für die GPU-Vorgängen noch nicht abgeschlossen

-   **Ausgabe von Bytes** Gesamtanzahl der RemoteFX Ausgabe Bytes

-   **Warten auf Client-Anzahl/s** Deprecated in Windows 8 und durch ersetzt **Frames übersprungen/Sekunde - nicht genügend Ressourcen für Client**

**RemoteFX vGPU management**

-   **Ressourcen: Von TDRs für virtuelle Computer lokal** Gesamtanzahl von TDRs, die auf diesem virtuellen Computer (von TDRs, dass der Server, auf die virtuellen Computer weitergegeben werden nicht eingeschlossen) aufgetreten sind

-   **Ressourcen: Von TDRs vom Server weitergegeben werden** Gesamtanzahl von TDRs, der auf dem Server aufgetreten ist und, weitergegeben wurden, mit dem virtuellen Computer,

**RemoteFX vGPU der Leistung virtueller Computer**

-   **Daten: Zeigt/Sekunde aufgerufen** Gesamtanzahl vorhanden Vorgänge auf dem Desktop des virtuellen Computers pro Sekunde gerendert werden soll (in Sekunden)

-   **Daten: Ausgehende zeigt/s** Gesamtanzahl von vorhanden Vorgängen, die von der virtuellen Maschine gesendet werden, auf dem GPU-Server pro Sekunde

-   **Daten: Gelesene Bytes/s** Gesamtanzahl der gelesenen Bytes aus dem RemoteFX-fähigen Server pro Sekunde

-   **Daten: Gesendete Bytes/Sek.** Gesamtzahl der Bytes, die an den Server RemoteFX-fähigen GPU pro Sekunde gesendet

-   **DMA: Kommunikationspuffer durchschnittliche Wartezeit (s)** durchschnittlich aufgewendete Zeit (in Sekunden) in den Puffern Kommunikation

-   **DMA: DMA-Puffer-Wartezeit (s)** Zeitspanne (in Sekunden) aus, wenn die DMA, bis zum Abschluss gesendet wird

-   **DMA: Warteschlangenlänge** DMA-Warteschlangenlänge für einen RemoteFX 3D Video Adapter

-   **Ressourcen: TDR Timeouts pro GPU** Anzahl von TDR-Timeouts, die pro GPU auf dem virtuellen Computer aufgetreten sind

-   **Ressourcen: TDR Timeouts pro GPU-Engine** Anzahl von TDR-Timeouts, die pro GPU aufgetreten sind, die auf dem virtuellen Computer-engine

Zusätzlich zu den RemoteFX virtuellen GPU-Leistungsindikatoren können Sie auch die GPU-Nutzung messen, mithilfe des Prozess-Explorer, der video-Speicherverwendung und die GPU-Auslastung zeigt.

## <a href="" id="perfopt"></a>Leistungsoptimierungen


### <a name="dynamic-memory"></a>Dynamischer Arbeitsspeicher

Dynamischer Arbeitsspeicher ermöglicht eine effizientere Nutzung der Arbeitsspeicherressourcen des Servers mit Hyper-V vom Lastenausgleich wie Arbeitsspeicher zwischen virtuellen Computern verteilt werden. Speicher kann dynamisch zwischen virtuellen Computern in der Antwort auf ihre auslastungen verschoben werden.

Dynamischer Arbeitsspeicher können Sie VM-Dichte mit den Ressourcen, die Sie bereits verfügen, ohne Einbußen bei der Leistung oder die Skalierbarkeit zu erhöhen. Das Ergebnis ist eine effizientere Nutzung der teure Hardware Serverressourcen, wiederum in einfachere Verwaltung und Kosten senken können.

Für Gastbetriebssysteme Windows 8 ausgeführt wird, und berücksichtigen oben mit virtuellen Prozessoren, die mehrere logische Prozessoren, umfassen den Kompromiss zwischen ausführen mit dynamischen Speichers, um die Speicherverwendung zu minimieren, und Deaktivieren des dynamischen Arbeitsspeichers zur Verbesserung der Leistung eine Anwendung, die Computer-Topologie bewusst ist. Eine solche Anwendung kann die Topologieinformationen zur Planung und arbeitsspeicherverwaltung zuordnungsentscheidungen treffen, nutzen.

### <a name="tiered-storage"></a>Mehrschichtiger Speicher

RD-Virtualisierungshost unterstützt mehrstufigen Speicher für virtuelle Desktoppools. Der physische Computer, der alle in einem Pool zusammengefasste virtuelle Desktops in einer Sammlung gemeinsam können eine kleine, hochleistungsfähige speicherlösung, z. B. eine gespiegelte Solid State Drive (SSD). Die in einem Pool zusammengefassten virtuellen Desktops können auf kostengünstigeren, traditionelle Speicher wie z. B. RAID 1 + 0 platziert werden.

Der physische Computer platziert werden soll, auf eine SSD handelt es sich, da die meisten der Read-ich/Os-aus in einem Pool zusammengefasste virtuelle Desktops auf dem Verwaltungsbetriebssystem wechseln. Der Speicher, der von dem physischen Computer verwendet wird, muss daher viel höher tolerieren e/a pro Sekunde gelesene.

Diese Bereitstellungskonfiguration stellt sicher, kosteneffektiv Leistung, in denen Leistung erforderlich ist. Bietet eine höhere Leistung die SSD auf eine kleinere Größe Datenträger (ca. 20 GB pro Sammlung, abhängig von der Konfiguration). Herkömmlicher Speicher für in einem Pool zusammengefasste virtuelle Desktops (RAID 1 + 0) ungefähr 3 GB pro virtuellem Computer verwendet.

### <a name="csv-cache"></a>CSV-cache

Failover-Clusterunterstützung in Windows Server 2012 und höher ermöglicht das Zwischenspeichern auf freigegebenen Clustervolumes (CSV). Dies ist von großem Vorteil für die in einem Pool zusammengefasste virtuelle desktopsammlungen den Großteil der Lesevorgang e/as aus dem Verwaltungsbetriebssystem stammen. Der CSV-Cache eine höhere Leistung von Größenordnung bietet, da Blöcke, die mehr als einmal gelesen werden zwischengespeichert und übermittelt sie Systemspeicher, wodurch die e/a reduziert wird. Weitere Informationen zum CSV-Cache, finden Sie unter [How to Enable CSV Cache](http://blogs.msdn.com/b/clustering/archive/2012/03/22/10286676.aspx).

### <a name="pooled-virtual-desktops"></a>In einem Pool zusammengefasste virtuelle desktops

Standardmäßig werden in einem Pool zusammengefasste virtuelle Desktops auf den ursprünglichen Zustand zurückgesetzt zurückgesetzt, nachdem ein Benutzer abmeldet, also alle Änderungen an der Windows-Betriebssystem seit der letzten Benutzeranmeldung abgebrochen werden.

Obwohl es möglich, die das Rollback deaktiviert ist, ist es immer noch ein temporäres Problem, da in der Regel ein in einem Pool zusammengefasste Sammlung virtueller Desktops aufgrund verschiedener Updates für die Vorlage für virtuelle Desktops neu erstellt wird.

Es ist sinnvoll, deaktivieren Sie Windows-Features und Dienste, die persistenten Status abhängig sind. Darüber hinaus Sie es sinnvoll, auf die Dienste zu deaktivieren, die in erster Linie für nicht-Enterprise-Szenarios sind.

Jeden spezifischen Dienst sollte vor jeder umfassende Bereitstellung entsprechend ausgewertet werden. Es folgen einige anfängliche Dinge zu beachten:

| Service                                      | Weshalb?                                                                                                                                                                                                      |
|----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Die automatische Aktualisierung                                  | In einem Pool zusammengefasste virtuelle Desktops werden aktualisiert, von der Vorlage für virtuelle Desktops neu zu erstellen.                                                                                                                          |
| Offlinedateien                                | Virtuelle Desktops sind immer online und über eine Netzwerk-von-Sicht verbunden.                                                                                                                         |
| Hintergrund-Defragmentierung                            | Dateisystem-Änderungen werden verworfen, nachdem ein Benutzer meldet sich deaktiviert (aufgrund der ein Rollback auf den ursprünglichen Zustand zurückgesetzt oder neu erstellt die Vorlage für virtuelle Desktops, was dazu führt alle in einem Pool zusammengefasste virtuelle Desktops neu erstellt werden soll). |
| In den Ruhezustand oder Energiesparmodus.                           | Kein solcher Konzept für VDI                                                                                                                                                                                   |
| Bug Check Speicherabbild                        | Keine solche Konzept in einem Pool zusammengefasste virtuelle Desktops. Ein in einem Pool zusammengefassten virtuellen Desktop von fehlerüberprüfung startet aus den ursprünglichen Zustand zurückgesetzt.                                                                                       |
| WLAN-Konfiguration                              | Es gibt keine WiFi-Gerät-Schnittstelle für VDI                                                                                                                                                                 |
| Windows Media Player-Netzwerkfreigabedienst | Zentrierte consumerdiensts                                                                                                                                                                                  |
| Heimnetzgruppen-Anbieter                          | Zentrierte consumerdiensts                                                                                                                                                                                  |
| Gemeinsame Nutzung der Internetverbindung                  | Zentrierte consumerdiensts                                                                                                                                                                                  |
| Media Center erweiterte Dienste               | Zentrierte consumerdiensts                                                                                                                                                                                  |

 

**Beachten Sie**    diese Liste ist nicht für die eine vollständige Liste werden vorgesehen, da alle Änderungen der gewünschten Ziele und Szenarios gelten. Weitere Informationen finden Sie unter ["heiß" aus der drückt, erhalten sie nun das Skript für den Windows 8-VDI-Optimierung, der PFE alternativen!](http://blogs.technet.com/b/jeff_stokes/archive/2013/04/09/hot-off-the-presses-get-it-now-the-windows-8-vdi-optimization-script-courtesy-of-pfe.aspx).

 

**Beachten Sie**    SuperFetch, Windows 8 ist standardmäßig aktiviert. Dabei handelt es sich VDI-fähige sollte nicht deaktiviert werden. SuperFetch kann weiter arbeitsspeichernutzung über Arbeitsspeicherfreigabe Seite reduziert werden, die für VDI vorteilhaft ist. In einem Pool zusammengefasste virtuelle Desktops mit Windows 7, SuperFetch sollte deaktiviert werden, aber für persönliche virtuelle Desktops unter Windows 7 ausgeführt wird, werden links auf.

 
