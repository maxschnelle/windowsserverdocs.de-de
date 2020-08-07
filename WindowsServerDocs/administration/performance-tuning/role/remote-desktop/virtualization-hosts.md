---
title: Leistungsoptimierung Remotedesktop Virtualisierungshosts
description: Leistungsoptimierung für Remotedesktop Virtualisierungshosts
ms.topic: article
ms.author: hammadbu; vladmis; denisgun
author: phstee
ms.date: 10/22/2019
ms.openlocfilehash: 071321249db62c927ee5677a48c52a7f2cd9c20d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896032"
---
# <a name="performance-tuning-remote-desktop-virtualization-hosts"></a>Leistungsoptimierung Remotedesktop Virtualisierungshosts

Remotedesktop-Virtualisierungshost (RD-Virtualisierungshost) ist ein Rollen Dienst, der Szenarien für die virtuelle Desktop Infrastruktur (VDI) unterstützt und es mehreren Benutzern ermöglicht, Windows-basierte Anwendungen auf virtuellen Computern auszuführen, die auf einem Server mit Windows Server und Hyper-V gehostet werden.

Windows Server unterstützt zwei Arten von virtuellen Desktops: Persönliche virtuelle Desktops und in einem Pool zusammengefasste virtuelle Desktops.

## <a name="general-considerations"></a>Allgemeine Hinweise

### <a name="storage"></a>Storage

Der Speicher ist der wahrscheinlichste Leistungsengpass, und es ist wichtig, die Größe Ihres Speichers so zu skaliert, dass die e/a-Auslastung ordnungsgemäß verarbeitet wird, die durch Zustandsänderungen virtueller Maschinen generiert wird. Wenn ein Pilotprojekt oder eine Simulation nicht durchführbar ist, empfiehlt es sich, eine Datenträger Spindel für vier aktive virtuelle Computer bereitzustellen. Verwenden Sie Datenträger Konfigurationen mit guter Schreibleistung (z. b. RAID 1 + 0).

Verwenden Sie ggf. die datenträgerdeduplizierung und Zwischenspeicherung, um die Datenträger-Lese Auslastung zu reduzieren und Ihre Speicherlösung zu aktivieren, um die Leistung zu beschleunigen, indem Sie einen signifikanten Teil des Images

### <a name="data-deduplication-and-vdi"></a>Datendeduplizierung und VDI

Die in Windows Server 2012 R2 eingeführte Datendeduplizierung unterstützt die Optimierung von geöffneten Dateien. Um virtuelle Computer zu verwenden, die auf einem deduplizierten Volume ausgeführt werden, müssen die Dateien der virtuellen Maschine auf einem separaten Host vom Hyper-V-Host gespeichert werden. Wenn Hyper-V und Deduplizierung auf dem gleichen Computer ausgeführt werden, werden die beiden Features für Systemressourcen in den Mittelwert geraten, was sich negativ auf die Gesamtleistung auswirkt.

Außerdem muss das Volume so konfiguriert werden, dass der deduplizierungstyp "Virtual Desktop Infrastructure (VDI)" verwendet wird. Sie können dies mithilfe Server-Manager konfigurieren (**deduplizierungseinstellungen für Datei-und Speicherdienste**  - &gt; **Volumes**  - &gt; **Dedup Settings**), oder indem Sie den folgenden Windows PowerShell-Befehl verwenden:

``` syntax
Enable-DedupVolume <volume> -UsageType HyperV
```

> [!NOTE]
> Die datendeduplizierungsoptimierung von geöffneten Dateien wird nur für VDI-Szenarien mit Hyper-V unterstützt, die Remote Speicher über SMB 3,0 verwenden.

### <a name="memory"></a>Memory

Die Auslastung des Server Arbeitsspeichers wird durch drei Hauptfaktoren gesteuert:

- Betriebssystem Aufwand

- Hyper-V-Dienst Aufwand pro virtuellem Computer

- Jedem virtuellen Computer zugeordneter Arbeitsspeicher

Bei einer typischen workerworkerworkloads sollten virtuelle Gastcomputer, auf denen x86 Window 8 oder Windows 8.1 ausgeführt wird, ~ 512 MB Arbeitsspeicher als Baseline erhalten. Allerdings erhöht dynamischer Arbeitsspeicher wahrscheinlich den Arbeitsspeicher des virtuellen Gast Computers auf ungefähr 800 MB, abhängig von der Arbeitsauslastung. Für x64 werden ungefähr 800 MB gestartet, die auf 1024 MB erhöht werden.

Daher ist es wichtig, genügend Server Arbeitsspeicher bereitzustellen, um den Arbeitsspeicher zu erfüllen, der für die erwartete Anzahl von virtuellen Gast Computern benötigt wird, sowie eine ausreichende Menge an Arbeitsspeicher für den Server zuzulassen.

### <a name="cpu"></a>CPU

Wenn Sie die Serverkapazität für einen RD-Virtualisierungshostserver planen, hängt die Anzahl der virtuellen Computer pro physischem Kern von der Art der Arbeitsauslastung ab. Als Ausgangspunkt empfiehlt es sich, 12 virtuelle Computer pro physischem Kern zu planen und dann die entsprechenden Szenarios zum Überprüfen der Leistung und Dichte auszuführen. Eine höhere Dichte kann je nach den Besonderheiten der Arbeitsauslastung erreicht werden.

Es wird empfohlen, Hyperthreading zu aktivieren. Achten Sie jedoch darauf, dass Sie das Abonnement für die Überzeichnung basierend auf der Anzahl der physischen Kerne und nicht mit der Anzahl der logischen Prozessoren berechnen. Dadurch wird die erwartete Leistung auf CPU-Basis sichergestellt.

## <a name="performance-optimizations"></a>Leistungsoptimierungen

### <a name="dynamic-memory"></a>Dynamischer Arbeitsspeicher

Dynamischer Arbeitsspeicher ermöglicht eine effizientere Auslastung der Speicherressourcen des Servers, auf dem Hyper-V ausgeführt wird, indem der Arbeitsspeicher zwischen den laufenden virtuellen Maschinen verteilt wird. Der Arbeitsspeicher kann zwischen virtuellen Computern dynamisch neu zugeordnet werden, als Reaktion auf ihre veränderlichen Workloads.

Mit dynamischer Arbeitsspeicher können Sie die VM-Dichte mit den Ressourcen erhöhen, die Sie bereits besitzen, ohne Leistungseinbußen oder Skalierbarkeit zu beeinträchtigen. Das Ergebnis ist eine effizientere Verwendung kostspieliger Server Hardware Ressourcen, die in eine einfachere Verwaltung und geringere Kosten übersetzt werden können.

Berücksichtigen Sie bei Gastbetriebssystemen mit Windows 8 und höher mit virtuellen Prozessoren, die mehrere logische Prozessoren umfassen, den Kompromiss zwischen der Ausführung mit dynamischer Arbeitsspeicher, um die Speicherauslastung zu minimieren und dynamischer Arbeitsspeicher zu deaktivieren, um die Leistung einer Anwendung zu verbessern, die Computer Topologie unterstützt. Eine solche Anwendung kann die Topologieinformationen nutzen, um Planungs-und Speicher Belegungs Entscheidungen zu treffen.

### <a name="tiered-storage"></a>Mehrschichtiger Speicher

Der RD-Virtualisierungshost unterstützt mehrstufigen Speicher für virtuelle Desktop Pools. Der physische Computer, der von allen in einem Pool zusammengefassten virtuellen Desktops in einer Sammlung gemeinsam genutzt wird, kann eine kleine Hochleistungsspeicher Lösung, z. b. ein gespiegeltes Solid-State-Laufwerk (SSD), verwenden. Die in einem Pool zusammengefassten virtuellen Desktops können auf kostengünstigeren, herkömmlichen Speicher wie z. b. RAID 1 + 0 platziert werden.

Der physische Computer sollte auf einem SSD abgelegt werden, weil die meisten Lese-e/a-Vorgänge von in einem Pool zusammengefassten virtuellen Desktops zum Verwaltungs Betriebssystem wechseln. Daher muss der Speicher, der vom physischen Computer verwendet wird, eine wesentlich höhere e/a-Lesevorgänge pro Sekunde unterstützen.

Diese Bereitstellungs Konfiguration gewährleistet die kostengünstige Leistung, wenn die Leistung benötigt wird. Die SSD bietet eine höhere Leistung auf einem Datenträger mit geringerer Größe (~ 20 GB pro Sammlung, abhängig von der Konfiguration). Herkömmlicher Speicher für in einem Pool zusammengefasste virtuelle Desktops (RAID 1 + 0) verwendet ca. 3 GB pro virtuellem Computer.

### <a name="csv-cache"></a>CSV-Cache

Failoverclustering in Windows Server 2012 und höher ermöglicht das Zwischenspeichern auf freigegebenen Clustervolumes (CSV). Dies ist äußerst vorteilhaft für in einem Pool zusammengefasste Sammlungen virtueller Desktops, bei denen der Großteil der Lese-e/a-Vorgänge vom Verwaltungs Betriebssystem stammt. Der CSV-Cache sorgt für eine höhere Leistung, da er Blöcke zwischenspeichert, die mehr als einmal gelesen werden, und Sie aus dem Systemspeicher übermittelt, wodurch die e/a-Vorgänge reduziert werden. Weitere Informationen zum CSV-Cache finden [Sie unter Aktivieren des CSV-Caches](https://blogs.msdn.com/b/clustering/archive/2012/03/22/10286676.aspx).

### <a name="pooled-virtual-desktops"></a>Gepoolte virtuelle Desktops

Standardmäßig werden für in einem Pool zusammengefasste virtuelle Desktops nach der Abmeldung eines Benutzers wieder in den ursprünglichen Zustand zurückgesetzt. alle Änderungen, die seit der letzten Benutzeranmeldung am Windows-Betriebssystem vorgenommen wurden, werden abgebrochen.

Obwohl es möglich ist, das Rollback zu deaktivieren, ist es immer noch eine vorübergehende Bedingung, da eine in einem Pool zusammengefasste Sammlung virtueller Desktops aufgrund verschiedener Updates der Vorlage für virtuelle Desktops neu erstellt wird.

Es ist sinnvoll, Windows-Features und-Dienste zu deaktivieren, die vom permanenten Zustand abhängen. Außerdem ist es sinnvoll, Dienste zu deaktivieren, die in erster Linie für nicht-Enterprise-Szenarios vorgesehen sind.

Jeder bestimmte Dienst sollte vor jeder breiten Bereitstellung angemessen ausgewertet werden. Im folgenden sind einige der folgenden Punkte zu beachten:

| Dienst                                      | Warum?                                                                                                                                                                                                      |
|----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Automatische Aktualisierung                                  | In einem Pool zusammengefasste virtuelle Desktops werden aktualisiert, indem die Vorlage für virtuelle Desktops neu erstellt wird.                                                                                                                          |
| Offlinedateien                                | Virtuelle Desktops sind immer online und über einen Netzwerk Ansichts Punkt verbunden.                                                                                                                         |
| Hintergrund-Debug                            | Dateisystem Änderungen werden verworfen, nachdem sich ein Benutzer abgemeldet hat (aufgrund eines Rollbacks zum ursprünglichen Zustand oder Neuerstellen der Vorlage für virtuelle Desktops, was zur erneuten Erstellung aller in einem Pool zusammengefassten virtuellen Desktops führt). |
| Ruhezustand oder Standbymodus                           | Kein solches Konzept für VDI                                                                                                                                                                                   |
| Fehlerüberprüfung für Speicher Abbild                        | Kein solches Konzept für in einem Pool zusammengefasste virtuelle Desktops. Ein in einem Pool zusammengestellter virtueller Desktop mit Fehlerüberprüfung wird vom ursprünglichen Zustand aus gestartet.                                                                                       |
| Automatische WLAN-Konfiguration                              | Es ist keine WLAN-Geräteschnittstelle für VDI vorhanden.                                                                                                                                                                 |
| Windows Media Player-Netzwerkfreigabe Dienst | Verbraucherorientierter Dienst                                                                                                                                                                                  |
| Startgruppen Anbieter                          | Verbraucherorientierter Dienst                                                                                                                                                                                  |
| Freigabe der Internet Verbindung                  | Verbraucherorientierter Dienst                                                                                                                                                                                  |
| Erweiterte Dienste von Media Center               | Verbraucherorientierter Dienst                                                                                                                                                                                  |
> [!NOTE]
> Diese Liste ist keine komplette Liste, da Änderungen sich auf die beabsichtigten Ziele und Szenarios auswirken. Weitere Informationen finden Sie unter [Hot Off the Backups, get it now, the Windows 8 VDI Optimization Script, courtesy of pfe!](https://blogs.technet.com/b/jeff_stokes/archive/2013/04/09/hot-off-the-presses-get-it-now-the-windows-8-vdi-optimization-script-courtesy-of-pfe.aspx).


> [!NOTE]
> Superfetch in Windows 8 ist standardmäßig aktiviert. Es ist VDI-fähig und sollte nicht deaktiviert werden. Superfetch kann die Arbeitsspeicher Nutzung durch die Freigabe von Arbeitsspeicher Seiten weiter reduzieren, was für VDI von Vorteil ist. Für in einem Pool zusammengefasste virtuelle Desktops, auf denen Windows 7 ausgeführt wird, sollte SuperFetch deaktiviert werden. für persönliche virtuelle Desktops, auf denen Windows 7 ausgeführt wird, sollte es jedoch weiterhin
