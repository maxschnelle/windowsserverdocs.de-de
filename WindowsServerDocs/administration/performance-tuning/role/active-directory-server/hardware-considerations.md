---
title: Überlegungen zur Hardware unter AD zur leistungsoptimierung
description: Überlegungen zur Hardware unter AD zur leistungsoptimierung
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 0f1aa1e3c07c5cb9238a332156abfec248e74176
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866091"
---
# <a name="hardware-considerations-in-adds-performance-tuning"></a>Überlegungen zur Hardware in AD DS zur leistungsoptimierung 

>[!Important]
> Im folgenden finden Sie eine Zusammenfassung der wichtigsten Empfehlungen und Überlegungen zur Optimierung der Serverhardware für Active Directory-Workloads in detaillierter behandelt die [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566) Artikel. Leser werden dringend empfohlen, überprüfen [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566) für ein besseres Verständnis für die technische und die Auswirkungen dieser Empfehlungen.

## <a name="avoid-going-to-disk"></a>Vermeiden Sie laufende auf dem Datenträger

Active Directory wird so viel von der Datenbank zwischengespeichert, da Speicher ermöglicht. Abrufen von Seiten aus dem Arbeitsspeicher sind sehr viel schneller, als Sie auf ein physisches Speichermedium aus, ob das Medium Spindel oder SSD-basierte. Fügen Sie mehr Arbeitsspeicher zur Minimierung der Datenträger-e/a.

-   Active Directory – bewährte Methoden empfehlen Einfügen von ausreichend Arbeitsspeicher zum Laden der gesamten DIT in den Arbeitsspeicher sowie zu ermöglichen, das Betriebssystem und andere installierten Anwendungen, z. B. eine Software Virenschutz, Sicherung, Überwachung, und so weiter.

    -   Informationen zu Einschränkungen der älteren Plattformen finden Sie unter [speicherauslastung durch den Prozess "Lsass.exe" auf Domänencontrollern, auf denen Windows Server 2003 oder Windows 2000 Server](https://support.microsoft.com/kb/308356).

    -   Verwenden Sie den Arbeitsspeicher\\Long-term durchschnittliche Standby Cachelebensdauer (s) &gt; Leistungsindikator 30 Minuten.

-   Fügen Sie das Betriebssystem, Protokolle und die Datenbank auf separaten Volumes an. Wenn alle oder die Mehrheit der DIT kann zwischengespeichert werden, sobald der Cache vorbereitet wird und unter einem stabilen Zustand Dadurch wird weniger relevant, und bietet ein wenig mehr Flexibilität bei der Speicher-Layout. In Szenarien, in dem die gesamte DIT nicht zwischengespeichert werden können, wird die Bedeutung von Teilen, dem Betriebssystem, Protokolle und -Datenbank auf separaten Volumes noch wichtiger ist.

-   E/a-Verhältnis auf die DIT-Datenbank stehen normalerweise etwa 90 % lesen und Schreiben von 10 %. Szenarien, in denen e/a-Volumes schreiben erheblich 10-20 % überschreiten, werden als mit vielen Schreibvorgängen betrachtet. Mit vielen Schreibvorgängen Szenarien profitieren stark nicht aus dem Active Directory-Cache. Um die Dauerhaftigkeit von Daten zu gewährleisten, die in das Verzeichnis geschrieben wird, führt Active Directory keine Datenträger Schreibcache aus. Stattdessen führt einen Commit dafür alle Schreibvorgänge auf den Datenträger vor der Rückgabe eines erfolgreichen Abschluss-Status für einen Vorgang, es sei denn, es gibt eine explizite Anforderung nicht so vorgehen. Schnelle Datenträger-e/a ist daher wichtig, die Leistung von Schreibvorgängen auf Active Directory. Im folgenden sind die hardwareempfehlungen, die Leistung für diese Szenarien verbessert werden können:

    -   Hardware-RAID-Controllern

    -   Erhöhen Sie die Anzahl der Low-Latenz/hohe-RPM-Datenträger hostet die DIT-Datenbank und-Protokolldateien

    -   Schreibcache auf dem controller

-   Überprüfen Sie die Datenträger-subsystemleistung einzeln für jedes Volume ein. Die meisten Active Directory-Szenarien basieren auf vorwiegend Lese-, daher sind die Statistiken auf dem Datenträger die DIT-Datenbank, die wichtigsten, zu überprüfen. Allerdings nicht vergessen, den Rest dieser Laufwerke einschließlich des Betriebssystems, Überwachung, und melden Sie sich Dateien, Laufwerke. Um festzustellen, ob der Domänencontroller ordnungsgemäß konfiguriert ist, um wird der Engpass für die Leistung des Speichers zu vermeiden, verweisen Sie im Abschnitt in Speichersubsystemen speicherempfehlungen Standards. Ist in vielen Umgebungen die Philosophie, um sicherzustellen, dass es genügend Head Platz um Fall kämen oder Spitzenlasten zu berücksichtigen ist. Diese Schwellenwerte werden Warnung, Schwellenwerte für die Kopfzeile, in dem Platz, um Fall kämen oder Spitzenlasten zu berücksichtigen ist eingeschränkt, und Client-Reaktionsfähigkeit beeinträchtigt wird. Kurz gesagt, diese Schwellenwerte überschreiten ist nicht schlecht, kurzfristig (5 bis 15 Minuten ein paar Mal pro Tag), jedoch ein System mit längeren mit diesen Arten von Statistiken ist nicht vollständig die Zwischenspeicherung der Datenbank und möglicherweise über steuern abgeführt und sollten untersucht werden.

    -   Datenbank ==&gt; Instances(lsass/NTDSA)\\e/a-Datenbank liest die durchschnittliche Latenz &lt; 15ms

    -   Datenbank ==&gt; Instances(lsass/NTDSA)\\-Datenbank-e/a-Lesevorgänge/Sekunde &lt; 10

    -   Datenbank ==&gt; Instances(lsass/NTDSA)\\durchschnittlichen Wartezeit für e/a-Protokollschreibvorgänge &lt; 10 ms.

    -   Datenbank ==&gt; Instances(lsass/NTDSA)\\Protokoll der e/a-Schreibvorgänge/s – nur zu Informationszwecken nur.

        Um die Konsistenz der Daten zu gewährleisten, müssen alle Änderungen in das Protokoll geschrieben werden. Es ist hier keine gut oder schlecht Anzahl, sondern nur ein Measure, wie viel Speicher der unterstützt wird.

-   Planen Sie nicht zum Kern Datenträger-e/a-Auslastung, wie z. B. Sicherung und Anti-Virus-Scans für außerhalb der Spitzenzeiten Perioden. Außerdem verwenden Sie, backup und Anti-Virus-Lösungen, die die e/a-Funktion mit niedriger Priorität eingeführt wurde in Windows Server 2008 um Wettbewerb mit e/a-Anforderungen von Active Directory zu verringern. zu unterstützen.

## <a name="dont-over-tax-the-processors"></a>Die Prozessoren nicht mehr als steuern

Prozessoren, die genügend freie Zyklen nicht haben, können lange Wartezeiten führen, zum Abrufen von Threads an der Prozessor für die Ausführung. In vielen Umgebungen die Philosophie wird sichergestellt, dass genügend Head Platz, um Fall kämen aufzunehmen oder Spitzen im laden, um die Auswirkungen auf die Client-Reaktionsfähigkeit in diesen Szenarien zu minimieren. Kurz gesagt, Überschreitung der Schwellenwerte ist nicht schlecht, kurzfristig (5 bis 15 Minuten ein paar Mal täglich), aber ein System mit ausgeführtem dauerhafte Statistiken in diesen nicht bereitstellt, HEAD-Platz zur Aufnahme von ungewöhnlichen lädt und können problemlos in einem versetzt werden besteuernden s Szenario. Systeme, die über dem Schwellenwert für einen längeren Ausgaben sollten zu Verfahren zum Verringern der Auslastung des Prozessors untersucht werden.

-   Weitere Informationen zum Auswählen von eines Prozessors finden Sie unter [Performance Tuning for Server Hardware](../../hardware/index.md).

-   Hinzufügen von Hardware, Auslastung zu optimieren, Clients an anderer Stelle anweisen, oder Entfernen von Laden aus der Umgebung auf die CPU-Last reduzieren.

-   Verwenden Sie die Prozessorinformationen (\_gesamt)\\% Prozessorauslastung &lt; 60 % Leistungsindikator.

## <a name="avoid-overloading-the-network-adapter"></a>Vermeiden Sie das überlasten von des Netzwerkadapters

Genau wie mit Prozessoren verursacht Auslastung übermäßige des Netzwerkadapters lange Wartezeiten für den ausgehenden Datenverkehr, um das Netzwerk zu erhalten, auf. Active Directory tendenziell kleine eingehende Anforderungen und relativ erheblich größere Mengen an Daten, die auf den Clientsystemen zurückgegeben. Gesendete Daten geht weit über empfangenen Daten. Ist in vielen Umgebungen die Philosophie, um sicherzustellen, dass es genügend Head Platz um Fall kämen oder Spitzenlasten zu berücksichtigen ist. Dieser Schwellenwert ist ein Schwellenwert für Warnung, in dem das Anfangselement Platz, um Fall kämen oder Spitzenlasten zu berücksichtigen, ist eingeschränkt, und Client-Reaktionsfähigkeit beeinträchtigt wird. Kurz gesagt, diese Schwellenwerte überschreiten ist nicht schlecht, kurzfristig (5 bis 15 Minuten ein paar Mal pro Tag), ist jedoch ein System mit längeren in diesen Statistiken über steuern abgeführt und sollten untersucht werden.

-   Weitere Informationen zum Optimieren der Netzwerk-Subsystem, finden Sie unter [Leistungsoptimierung für Netzwerk-Subsysteme](../../../../networking/technologies/network-subsystem/net-sub-performance-top.md).

-   Verwenden Sie den NetworkInterface verglichen werden soll (\*)\\gesendete Bytes/s mit NetworkInterface (\*)\\Leistungsindikator für die aktuelle Bandbreite. Das Verhältnis muss weniger als 60 Prozent belegt.

## <a name="see-also"></a>Siehe auch
- [Active Directory-Server die Optimierung der Leistung](index.md)
- [LDAP-Überlegungen](ldap-considerations.md)
- [Ordnungsgemäße Platzierung von Domänencontrollern und Website-Überlegungen](site-definition-considerations.md)
- [Problembehandlung für AD DS-Leistung](troubleshoot.md) 
- [Kapazitätsplanung für Active Directory-Domänendienste](https://go.microsoft.com/fwlink/?LinkId=324566)