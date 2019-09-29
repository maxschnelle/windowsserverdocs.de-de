---
title: Überlegungen zur Hardware bei der AD-Leistungsoptimierung
description: Überlegungen zur Hardware bei der AD-Leistungsoptimierung
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 8e9b121036d33bc36cabb92ca682407bc2382fca
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355098"
---
# <a name="hardware-considerations-in-adds-performance-tuning"></a>Überlegungen zur Hardware in werden Leistungsoptimierungen hinzugefügt 

>[!Important]
> Im folgenden finden Sie eine Zusammenfassung der wichtigsten Empfehlungen und Überlegungen zur Optimierung der Server Hardware für Active Directory Arbeits Auslastungen, die in der [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566) Artikel ausführlicher behandelt werden. Leser werden dringend empfohlen, die [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566) zu überprüfen, um das technische Verständnis und die Auswirkungen dieser Empfehlungen zu überprüfen.

## <a name="avoid-going-to-disk"></a>Vermeiden des Datenträgers

Active Directory speichert so viele Datenbanken wie der Arbeitsspeicher zulässt. Beim Abrufen von Seiten aus dem Arbeitsspeicher werden die Größenordnungen schneller als bei physischen Medien angezeigt, unabhängig davon, ob es sich um eine Spindel-oder SSD-basiert handelt Fügen Sie weiteren Arbeitsspeicher hinzu, um die Datenträger-e/a

-   Active Directory bewährten Methoden empfehlen, genügend RAM zu platzieren, um die gesamte dit in den Arbeitsspeicher zu laden, sowie das Betriebssystem und andere installierte Anwendungen wie Antivirensoftware, Sicherungssoftware, Überwachung usw.

    -   Informationen zu den Einschränkungen der Legacy Plattformen finden Sie unter [Speicherauslastung durch den LSASS. exe-Prozess auf Domänen Controllern, auf denen Windows Server 2003 oder Windows 2000 Server ausgeführt](https://support.microsoft.com/kb/308356)wird.

    -   Verwenden Sie den\\Leistungs Begriffswert für die langfristige durchschnittliche Dauer &gt; des standbycache-standbycaches von 30 Minuten.

-   Legen Sie das Betriebssystem, die Protokolle und die Datenbank auf separaten Volumes ab. Wenn der gesamte oder der Großteil der DIT zwischengespeichert werden kann, wird der Cache nach dem Aufwärmen und im stabilen Zustand weniger relevant und bietet ein wenig mehr Flexibilität beim Speicher Layout. In Szenarien, in denen die gesamte dit nicht zwischengespeichert werden kann, wird die Wichtigkeit der Aufteilung des Betriebssystems, der Protokolle und der Datenbank auf separaten Volumes wichtiger.

-   Normalerweise sind e/a-Verhältnisse für die DIT etwa 90% Lesevorgänge und 10% Schreibvorgänge. Szenarios, in denen Schreib-e/a-Volumes deutlich mehr als 10%-20% überschreiten, werden als Schreib intensiv angesehen Szenarien mit hohem Schreib Aufwand profitieren nicht von der Active Directory Cache. Um die transaktionale Dauerhaftigkeit von Daten zu gewährleisten, die in das Verzeichnis geschrieben werden, führt Active Directory keine Zwischenspeicherung von Schreibvorgängen durch. Stattdessen committet Sie alle Schreibvorgänge auf den Datenträger, bevor Sie einen erfolgreichen Abschluss Status für einen Vorgang zurückgibt, es sei denn, es gibt eine explizite Anforderung, dies zu tun. Daher ist die schnelle Datenträger-e/a wichtig für die Leistung von Schreibvorgängen für die Active Directory. Im folgenden finden Sie Hardware Empfehlungen, die die Leistung für diese Szenarien verbessern können:

    -   Hardware-RAID-Controller

    -   Erhöhen Sie die Anzahl der Datenträger mit niedriger Latenz/hoher RPM, auf denen die dit-und Protokolldateien gehostet werden.

    -   Schreiben Zwischenspeicherung auf dem Controller

-   Überprüfen Sie die Leistung des Datenträger Subsystems einzeln für jedes Volume. Die meisten Active Directory Szenarios sind hauptsächlich Schreib basiert, daher sind die Statistiken auf dem Volume, das die DIT-Anwendung gehostet, die wichtigste zu überprüfen. Übersehen Sie jedoch nicht die Überwachung der restlichen Laufwerke, einschließlich des Betriebssystems und der Protokolldatei Laufwerke. Um zu ermitteln, ob der Domänen Controller ordnungsgemäß konfiguriert ist, um zu vermeiden, dass Speicher als Engpass für die Leistung dient, finden Sie im Abschnitt Speicher Subsysteme Informationen zu Standard Speicher Empfehlungen. In vielen Umgebungen besteht die Philosophie darin, sicherzustellen, dass genügend Platz zur Verfügung steht, um Spitzen oder Spitzen bei Last zu bewältigen. Bei diesen Schwellenwerten handelt es sich um Schwellenwerte für Warnungen, bei denen der haupthfad für die Aufnahme von Spitzen oder Spitzenlast eingeschränkt wird und die Client Reaktionsfähigkeit Kurz gesagt: das Überschreiten dieser Schwellenwerte ist kurzfristig nicht schlecht (5 bis 15 Minuten mehrmals täglich), aber ein System, das mit dieser Art von Statistiken nicht vollständig ausgeführt wird, wird die Datenbank nicht vollständig Zwischenspeichern und ist möglicherweise übersteuert und sollte untersucht werden.

    -   Database = =&gt; Instanzen (LSASS/NTDSA)\\e/a-Datenbank liest durchschnittliche &lt; Latenz 15ms

    -   Database = =&gt; Instanzen (LSASS/NTDSA)\\e/a-Daten Bank Lese &lt; Vorgänge/Sek. 10

    -   Database = =&gt; Instanzen (LSASS/NTDSA)\\e/a-Protokoll Schreibvorgänge &lt; mit durchschnittlicher Latenz 10 ms

    -   Database = =&gt; Instanzen (LSASS/NTDSA)\\e/a-Protokoll Schreibvorgänge/Sek. – nur Information.

        Um die Konsistenz der Daten aufrechtzuerhalten, müssen alle Änderungen in das Protokoll geschrieben werden. Hier gibt es keine gute oder ungültige Zahl. es handelt sich lediglich um ein Maß dafür, wie viel Speicherplatz unterstützt wird.

-   Planen von e/a-Datenträger-e/a-Ladevorgängen, wie z. b. Sicherungs-und Antivirenscans, für nicht-Spitzenzeiten. Außerdem können Sie Sicherungs-und Antivirussoftware verwenden, die die in Windows Server 2008 eingeführte e/a-Funktion mit niedriger Priorität unterstützen, um den Wettbewerb mit den e/a-Anforderungen von Active Directory zu verringern.

## <a name="dont-over-tax-the-processors"></a>Steuern Sie die Prozessoren nicht.

Prozessoren, die nicht über genügend freie Zyklen verfügen, können lange Wartezeiten beim Ausführen von Threads an den Prozessor für die Ausführung verursachen. In vielen Umgebungen besteht die Philosophie darin, sicherzustellen, dass genügend Platz zur Verfügung steht, um die Auswirkungen auf die Reaktionsfähigkeit von Clients in diesen Szenarien zu minimieren. Kurz gesagt: das Überschreiten der folgenden Schwellenwerte ist kurzfristig nicht schlecht (5 bis 15 Minuten mehrmals täglich). ein System, das mit dieser Art von Statistiken ausgeführt wird, bietet jedoch keinen Platz für ungewöhnliche Lasten und kann problemlos in eine Übersteuerte CENARIO. Systeme, die die Schwellenwerte überschreiten, sollten untersucht werden, um die Prozessorauslastung zu reduzieren.

-   Weitere Informationen zum Auswählen eines Prozessors finden Sie unter [Leistungsoptimierung für Server Hardware](../../hardware/index.md).

-   Fügen Sie Hardware hinzu, optimieren Sie die Last, leiten Sie Clients an einem anderen Ort weiter, oder entfernen Sie die Auslastung aus der Umgebung, um

-   Verwenden Sie die Prozessor Informationen (\_total) \\% Prozessorauslastung &lt; 60% Leistungs Zählers.

## <a name="avoid-overloading-the-network-adapter"></a>Vermeiden Sie das Überladen des Netzwerkadapters.

Ebenso wie bei Prozessoren führt eine übermäßige Auslastung des Netzwerkadapters zu langen Wartezeiten, bis der ausgehende Datenverkehr an das Netzwerk gelangt. Active Directory haben tendenziell kleine eingehende Anforderungen und relativ zu erheblich größeren Datenmengen, die an die Client Systeme zurückgegeben werden. Die gesendeten Daten überschreiten die empfangenen Daten. In vielen Umgebungen besteht die Philosophie darin, sicherzustellen, dass genügend Platz zur Verfügung steht, um Spitzen oder Spitzen bei Last zu bewältigen. Dieser Schwellenwert ist ein Warnungs Schwellenwert, bei dem der haupthfad zum Aufnehmen von Spitzen oder Spitzen bei der Auslastung eingeschränkt wird und die Client Reaktionsfähigkeit beeinträchtigt wird. Kurz gesagt: das Überschreiten dieser Schwellenwerte ist kurzfristig nicht schlecht (5 bis 15 Minuten mehrmals täglich), aber ein System, das mit dieser Art von Statistiken ausgeführt wird, wird übersteuert und sollte untersucht werden.

-   Weitere Informationen zum Optimieren des Netzwerk Subsystems finden Sie unter [Leistungsoptimierung für Netzwerk Subsysteme](../../../../networking/technologies/network-subsystem/net-sub-performance-top.md).

-   Verwenden Sie den Leistungs Leistungs Dienst "\*netzwerkschnittstellenbytes ()\\mit gesendete\*Bytes\\/Sek." mit NetworkInterface (). Das Verhältnis sollte weniger als 60% betragen.

## <a name="see-also"></a>Siehe auch
- [Leistungsoptimierung Active Directory Server](index.md)
- [Überlegungen zu LDAP](ldap-considerations.md)
- [Ordnungsgemäße Platzierung von Domänencontrollern und Überlegungen zum Standort](site-definition-considerations.md)
- [Problembehandlung bezüglich der ADDS-Leistung](troubleshoot.md) 
- [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566)