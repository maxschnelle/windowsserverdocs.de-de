---
title: Kapazitätsplanung für Active Directory Domain Services
description: Ausführliche Informationen zu den Faktoren bei der kapazitätsplanung für AD DS berücksichtigt.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; kenbrunf
author: Teresa-Motiv
ms.date: 7/3/2019
ms.openlocfilehash: 5a9e2d39d4eedd1e8fdb4bfeaf267ad4cb4c596a
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67799832"
---
# <a name="capacity-planning-for-active-directory-domain-services"></a>Kapazitätsplanung für Active Directory Domain Services

Dieses Thema wurde ursprünglich in Ken Brumfield, Senior Premier Field Engineer bei Microsoft geschrieben und enthält Empfehlungen zur kapazitätsplanung für Active Directory Domain Services (AD DS).

## <a name="goals-of-capacity-planning"></a>Ziele der kapazitätsplanung

Planen der Kapazität ist nicht identisch mit der Problembehandlung der Leistung von Incidents. Sie sind eng miteinander verwandten, aber sehr unterschiedlich. Die Ziele der kapazitätsplanung sind:  

- Ordnungsgemäß zu implementieren und Betreiben einer Umgebung 
- Minimieren Sie die Zeit zur Problembehandlung Leistungsprobleme im Zusammenhang.  
  
Planen der Kapazität möglicherweise eine Organisation eine Baseline-Ziel der 40 Prozent prozessorauslastung durch den Spitzenzeiten, um die Client-leistungsanforderungen zu erfüllen, und berücksichtigen die Zeit, das upgrade der Hardware im Rechenzentrum erforderlich sind. Dagegen um leistungsanomalien Vorfälle benachrichtigt zu werden, ein Überwachung Warnungsschwellenwert bei 90 % über einen Zeitraum von 5 Minuten festgelegt werden kann.

Der Unterschied besteht darin, die bei ein Capacity Management-Schwellenwert ständig überschritten wird (ein einmaliges Ereignis ist nicht relevant), Hinzufügen von Kapazität (die in mehr oder schnellere Prozessoren addieren) wäre eine Lösung oder den Dienst auf mehrere Server horizontal hochskalieren wäre ein die Lösung. Warnung Leistungsschwellenwerte anzugeben, dass die Clientfunktionen derzeit leidet und sofortige Schritte sind erforderlich, um das Problem zu beheben.

Als eine Analogie: Capacity Management wird zum Verhindern einer Auto Unfall (defensive driving sicherstellen, dass die Bremsen funktionieren ordnungsgemäß, und so weiter) hingegen Leistung Fehlerbehebung vorgehen, die Polizei, Feuerwache und Notfall Mediziner nach einem Unfall. Dies bezieht sich auf "defensive driving," Active Directory-Stil.

In den letzten Jahren hat die Kapazität Planen des Implementierungsvorgangs für skalierbare Systeme erheblich geändert. Die folgenden Änderungen an der Systemarchitekturen haben grundlegende Annahmen zum Entwerfen und Skalieren eines Diensts konfrontiert:

- 64-Bit-Server-Plattformen  
- Virtualisierung  
- Erhöhte Aufmerksamkeit auf den Energieverbrauch  
- SSD-Speicher  
- Cloud-Szenarien  

Darüber hinaus ist der Ansatz von einer Server-basierte kapazitätsplanung Übung aus, um eine Dienst-basierte kapazitätsplanung Übung verschieben. Active Directory-Domänendienste (AD DS), ein ausgereiftes verteilter Dienst, mit denen viele Microsoft und Drittanbieter-Produkte als Backend verwendet werden, wird eine der wichtigsten Produkte richtig planen, um sicherzustellen, dass die erforderliche Kapazität für andere Anwendungen ausführen.

### <a name="baseline-requirements-for-capacity-planning-guidance"></a>Grundlegende Voraussetzungen für die Leitfaden zur kapazitätsplanung

In diesem Artikel werden die folgenden grundlegenden Anforderungen bestehen erwartet:

- Leser über Lese- und kennen [Performance Tuning Richtlinien für Windows Server 2012 R2](https://docs.microsoft.com/previous-versions//dn529133(v=vs.85)).
- Windows Server-Plattform ist x X64 basierende Architektur. Aber selbst wenn die Active Directory-Umgebung unter Windows Server 2003 X86 ("jetzt" hinter dem Ende des Produktlebenszyklus) installiert ist und eine Verzeichnisstruktur (DIT) hat, weniger 1,5 GB groß ist und dass kann problemlos gespeichert werden im Arbeitsspeicher, die Richtlinien aus dieser Artikel können weiterhin angewendet werden.
- Planen der Kapazität ist ein kontinuierlicher Prozess aus, und Sie sollten regelmäßig überprüfen, wie gut die Umgebung Erwartungen erfüllt werden.
- Optimierung wird über mehrere Hardware Lebenszyklen Kosten hardwareänderung auftreten. Z. B. Arbeitsspeicher wird kostengünstiger, verringert die Kosten pro Kern und der Preis für unterschiedliche Optionen ändern.
- Planen Sie auslastungszeitraums Spitzenwert des Tages. Es wird empfohlen, diese in Intervallen von 30 Minuten oder Stunden entweder ansehen. Etwas größer kann die tatsächliche Spitzen und etwas, das weniger durch "vorübergehende Spitzen" verzerrt werden möglicherweise ausgeblendet
- Planen Sie für Wachstum im Laufe des Lebenszyklus der Hardware, für das Unternehmen. Dies kann eine Strategie für das Aktualisieren oder Hinzufügen von Hardware in einer gestaffelten Weise, oder eine vollständige Aktualisierung alle drei bis fünf Jahre umfassen. Wie viel die Last auf Active Directory ausgeweitet wird, müssen jedes "erraten". Verlaufsdaten, hilft, wenn gesammelt wurden, mit dieser Bewertung. 
- Plan für die Fehlertoleranz zu gewährleisten. Sobald eine Schätzung *N* abgeleitet wird, Plan für Szenarios mit *N* &ndash; 1 *N* &ndash; 2, *N* &ndash; *x*.
  - Fügen Sie in zusätzlichen Servern entsprechend der Organisation erforderlich, um sicherzustellen, dass der Verlust einer einzelnen oder mehreren Servern nicht Schätzungen für maximale maximale Kapazität überschritten wird.
  - Berücksichtigen Sie auch, dass die Wachstum planen und Fault-Tolerance-Plan integriert werden müssen. Z. B. wenn ein Domänencontroller ist erforderlich, um die Last zu unterstützen, aber die Schätzung, die die Last wird im nächsten Jahr verdoppelt werden und erfordern zwei DCs insgesamt, es werden nicht genügend Kapazität, um die Fehlertoleranz zu unterstützen. Die Lösung wäre, mit drei Domänencontroller zu beginnen. Eine kann auch planen, den dritten DC nach 3 oder 6 Monaten hinzufügen, wenn Budgets, enge sind.

    >[!NOTE]
    >Hinzufügen von Active Directory-kompatiblen Anwendungen möglicherweise die spürbare Auswirkungen auf die DC-Last, ob die Last der Anwendungsserver oder des Clients stammen.

### <a name="three-step-process-for-the-capacity-planning-cycle"></a>Drei Schritte für die kapazitätsplanung-Zyklus

Entscheiden Sie bei der kapazitätsplanung, welche Quality of Service, erforderlich ist. Beispielsweise wird ein Datacenter Core unterstützt ein höheres Maß an Parallelität und konsistentere Erfahrung für Benutzer und Nutzen von Anwendungen, die mehr Aufmerksamkeit auf Redundanz erfordert und Minimieren der System- und Infrastrukturebene Engpässe erfordert. Im Gegensatz dazu ist einem Satellitenstandort durch eine Reihe von Benutzern nicht das gleiche Maß an Parallelität oder Fehlertoleranz erforderlich. Daher der Zweigstelle benötigen möglicherweise nicht so viel Aufmerksamkeit zur Optimierung der zugrunde liegende Hardware und Infrastruktur, die zu einsparungen führen kann. Alle Empfehlungen und Anleitungen in diesem Dokument gelten für eine optimale Leistung und können selektiv gelockerte für Szenarien mit weniger anspruchsvolle Anforderungen werden.

Die nächste Frage lautet: virtualisiert oder physisch? Hinsichtlich der Capacity planning antwortet nicht richtig oder falsch; Es gibt nur einen anderen Satz von Variablen mit arbeiten. Virtualisierungsszenarien sinken, eine der beiden Optionen:

- "Direkte Zuordnung" mit nur einem Gast pro Host (wobei Virtualisierung vorhanden ausschließlich zum abstrahieren der physischen Hardware auf dem Server)
- "Freigegebene Host"

Szenarien für Test- und produktionsumgebungen anzugeben, dass das Szenario "direkte Zuordnung" genauso wie auf einem physischen Host behandelt werden kann. "Shared-Host" führt jedoch einige Aspekte, die später noch ausführlicher ausgeschrieben. Das Szenario "freigegebenen Host" bedeutet, dass AD DS ist auch um Ressourcen konkurriert, sind zur Folge haben und Optimierung Überlegungen für die auf diese Weise.

Unter Berücksichtigung dieser Faktoren ist Zyklus für die kapazitätsplanung ein iterativer Prozess mit drei Schritten:

1. Messen Sie die vorhandene Umgebung, zu bestimmen Sie, in dem die Engpässe im System derzeit sind, und erhalten environmental Grundlagen erforderlich, um die Menge der erforderlichen Kapazität zu planen.
1. Bestimmen Sie die Hardware gemäß den in Schritt 1 beschriebenen Kriterien erforderlich.
1. Überwachen Sie und überprüfen Sie, dass die Infrastruktur, die gemäß der Implementierung in Spezifikationen ausgeführt wird. Einige Daten gesammelt, die in diesem Schritt werden die Baseline für den nächsten Zyklus der kapazitätsplanung.

### <a name="applying-the-process"></a>Den Prozess anwenden

Um die Leistung zu optimieren, stellen Sie sicher diese wichtigen Komponenten ordnungsgemäß ausgewählt und optimiert, um die Anwendung geladen:

1. Arbeitsspeicher
1. Network
1. Speicher
1. Prozessor
1. Anmeldedienst

Die grundlegende speicheranforderungen von AD DS und das allgemeine Verhalten der gut geschriebene-Clientsoftware können Umgebungen mit bis zu 10.000 bis 20.000 Benutzer, verzichten hohen Investitionen in im Hinblick auf die physische Hardware, als nahezu jede moderne Server zur kapazitätsplanung -System der Klasse, die die Last behandelt wird. Dies bedeutet, dass der folgenden Tabelle eine vorhandene Umgebung auswerten, um die passende Hardware auszuwählen sind. Jede Komponente wird detailliert in den folgenden Abschnitten können Sie AD DS-Administratoren ihrer Infrastruktur mit Sicherheitsbaseline-Empfehlungen und umgebungsspezifische Prinzipale auswerten analysiert.

Im Allgemeinen:

- Größenanpassung basierend auf aktuellen Daten werden nur für die aktuelle Umgebung genau.
- Für alle Schätzungen, erwarten Sie bei Bedarf über den Lebenszyklus der Hardware erreicht.
- Bestimmen, ob das Vergleich heute und problemlos in größere Umgebung, oder fügen Sie Kapazitäten hinzu, über den Lebenszyklus.
- Für die Virtualisierung gelten die gleichen kapazitätsplanung Prinzipale und Methoden, mit dem Unterschied, dass der Mehraufwand für die Virtualisierung muss nichts im Zusammenhang Domäne hinzugefügt werden.
- Kapazitätsplanung, wie alle Elemente, die versucht vorherzusagen, ist keine genaue Wissenschaft. Erwarten Sie nicht die Dinge, die perfekt und mit 100 % iger Genauigkeit zu berechnen. Leanest empfiehlt es sich hier die Anweisungen; Fügen Sie Kapazität für zusätzliche Sicherheit, und kontinuierlich zu überprüfen Sie, dass die Umgebung auf Ziel bleibt.

### <a name="data-collection-summary-tables"></a>Zusammenfassung Datentabellen für Sammlung

#### <a name="new-environment"></a>Neue Umgebung

| Komponente | Schätzungen |
|-|-|
|Größe von Storage-Datenbank|40 KB bis 60 KB für jeden Benutzer|
|RAM|Datenbankgröße<br />Basisbetriebssystem-Empfehlungen<br />Drittanbieter-Anwendungen|
|Network|1 GB|
|CPU|1\.000 gleichzeitigen Benutzern für jeden Kern|

#### <a name="high-level-evaluation-criteria"></a>Allgemeine Kriterien

| Komponente | Auswertungskriterien | Planungsüberlegungen |
|-|-|-|
|Größe von Storage-Datenbank|Im Abschnitt: "So aktivieren die Protokollierung von Speicherplatz, der freigegeben wird, durch die Defragmentierung" in [Grenzwerte für Storage](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))| |
|Speicher / der datenbankleistung|<ul><li>"Logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Avg Sek./Lesevorgänge," "logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Avg Sek./Schreibvorgänge," " Logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Avg Sek./Übertragung "</li><li>"LogicalDisk( *\<NTDS Database Drive\>* )\Reads/sec," "LogicalDisk( *\<NTDS Database Drive\>* )\Writes/sec," "LogicalDisk( *\<NTDS Database Drive\>* )\Transfers/sec"</li></ul>|<ul><li>Storage verfügt über zwei Sicherheitsaspekte zu bedenken<ul><li>Speicherplatz verfügbar ist, der mit der Größe der heutigen Spindel basiert und SSD-Speicher Speicher basierender, ist irrelevant für die meisten AD-Umgebungen.</li> <li>Eingabe/Ausgabe (e/a) Vorgänge verfügbar – In vielen Umgebungen, wird dies oft übersehen. Aber es ist wichtig, nur Umgebungen zu bewerten, es nicht genügend Arbeitsspeicher ist für die gesamte NTDS-Datenbank in den Arbeitsspeicher geladen.</li></ul><li>Speicher kann ein komplexes Thema und sollte Hardware-Hersteller-Kenntnisse für die richtige größenanpassung umfassen. Insbesondere bei komplexeren Szenarien wie SAN, NAS und iSCSI-Szenarien. Häufig ist jedoch im Allgemeinen die Kosten pro Gigabyte an Speicher in direkten Widerspruch Kosten pro e/a:<ul><li>RAID 5 geringeren Kosten pro Gigabyte als Raid 1, aber Raid 1 hat geringere Kosten pro e/a</li><li>Festplatten Spindel basierende niedrigeren Kosten pro Gigabyte, aber SSDs geringeren Kosten pro e/a</li></ul><li>Klicken Sie nach einem Neustart des Computers oder der Active Directory Domain Services-Dienst der Extensible Storage Engine (ESE)-Cache ist leer, und Leistung werden die Datenträger, die gebunden werden, während der Cache leseanforderungen.</li><li>In den meisten Umgebungen ist AD intensive e/a in einem zufälligen Muster auf Datenträgern, viele Vorteile des Zwischenspeicherns negieren lesen und Optimierungsstrategien zu lesen.  Darüber hinaus wurde AD einen viel größeren Cache im Arbeitsspeicher als die meisten Speichersystem zwischenspeichert.</li></ul>
|RAM|<ul><li>Datenbankgröße</li><li>Basisbetriebssystem-Empfehlungen</li><li>Drittanbieter-Anwendungen</li></ul>|<ul><li>Speicher ist die langsamste Komponente auf einem Computer. Je mehr sein kann, im Arbeitsspeicher, desto weniger ist es erforderlich, auf der Festplatte.</li><li>Stellen Sie sicher, genügend Arbeitsspeicher wird zugeordnet, um das Speichern des Betriebssystems, Agents (Antivirus, Sicherung, Überwachung), NTDS-Datenbank und das Wachstum im Laufe der Zeit.</li><li>Für Umgebungen, in dem die Größe des Arbeitsspeichers maximiert kein, Kosten effektiv (z. B. eine Satelliten-Speicherorte) oder nicht möglich (DIT-Datenbank ist zu groß), Referenz, die Größe des Speicherabschnitts, um sicherzustellen, dass der Speicher ordnungsgemäß konfiguriert ist.</li></ul>|
|Network|<ul><li>"Netzwerkschnittstelle (\*) \Bytes/Sek."</li><li>"Netzwerkschnittstelle (\*) \Bytes/Sek."|<ul><li>Im Allgemeinen überschreitet Datenverkehr von einem Domänencontroller mit viel Datenverkehr, der mit einem DC gesendet.</li><li>Wenn eine Ethernet-Verbindung gewechselt vollduplexadapter lautet, müssen ein- und ausgehenden Netzwerkdatenverkehr unabhängig voneinander angepasst werden.</li><li>Konsolidieren die Anzahl von DCs erhöht sich die Menge an Bandbreite, die zum Senden von Antworten zurück an den Client-Anforderungen für jeden Domänencontroller verwendet, können jedoch nahe genug, um linearer für den Standort als Ganzes.</li><li>Wenn Satellitenstandort Domänencontroller zu entfernen, vergessen Sie nicht, fügen die Bandbreite für die Satellite-DC in den Hub-DCs als auch verwenden, die zum Auswerten, wie viele WAN-Datenverkehr vorhanden.</li></ul>|
|CPU"Logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Avg Sek./Lesevorgänge"descripti"Process(lsass)\\" Prozessorzeit "tors to consider during capacity planning for AD DS.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; kenbrunf
author: Teresa-Motiv
ms.date: 7/3/2019
---

# Capacity planning for Active Directory Domain Services

This topic is originally written by Ken Brumfield, Senior Premier Field Engineer at Microsoft, and provides recommendations for capacity planning for Active Directory Domain Services (AD DS).

## Goals of capacity planning

Capacity planning is not the same as troubleshooting performance incidents. They are closely related, but quite different. The goals of capacity planning are:  

- Properly implement and operate an environment 
- Minimize the time spent troubleshooting performance issues.  
  
In capacity planning, an organization might have a baseline target of 40% processor utilization during peak periods in order to meet client performance requirements and accommodate the time necessary to upgrade the hardware in the datacenter. Whereas, to be notified of abnormal performance incidents, a monitoring alert threshold might be set at 90% over a 5 minute interval.

The difference is that when a capacity management threshold is continually exceeded (a one-time event is not a concern), adding capacity (that is, adding in more or faster processors) would be a solution or scaling the service across multiple servers would be a solution. Performance alert thresholds indicate that client experience is currently suffering and immediate steps are needed to address the issue.

As an analogy: capacity management is about preventing a car accident (defensive driving, making sure the brakes are working properly, and so on) whereas performance troubleshooting is what the police, fire department, and emergency medical professionals do after an accident. This is about “defensive driving,” Active Directory-style.

Over the last several years, capacity planning guidance for scale-up systems has changed dramatically. The following changes in system architectures have challenged fundamental assumptions about designing and scaling a service:

- 64-bit server platforms  
- Virtualization  
- Increased attention to power consumption  
- SSD storage  
- Cloud scenarios  

Additionally, the approach is shifting from a server-based capacity planning exercise to a service-based capacity planning exercise. Active Directory Domain Services (AD DS), a mature distributed service that many Microsoft and third-party products use as a backend, becomes one the most critical products to plan correctly to ensure the necessary capacity for other applications to run.

### Baseline requirements for capacity planning guidance

Throughout this article, the following baseline requirements are expected:

- Readers have read and are familiar with [Performance Tuning Guidelines for Windows Server 2012 R2](https://docs.microsoft.com/previous-versions//dn529133(v=vs.85)).
- The Windows Server platform is an x64 based architecture. But even if your Active Directory environment is installed on Windows Server 2003 x86 (now beyond the end of the support lifecycle) and has a directory information tree (DIT) that is less 1.5 GB in size and that can easily be held in memory, the guidelines from this article are still applicable.
- Capacity planning is a continuous process and you should regularly review how well the environment is meeting expectations.
- Optimization will occur over multiple hardware lifecycles as hardware costs change. For example, memory becomes cheaper, the cost per core decreases, or the price of different storage options change.
- Plan for the peak busy period of the day. It is recommended to look at this in either 30 minute or hour intervals. Anything greater may hide the actual peaks and anything less may be distorted by “transient spikes.”
- Plan for growth over the course of the hardware lifecycle for the enterprise. This may include a strategy of upgrading or adding hardware in a staggered fashion, or a complete refresh every three to five years. Each will require a “guess” as how much the load on Active Directory will grow. Historical data, if collected, will help with this assessment. 
- Plan for fault tolerance. Once an estimate *N* is derived, plan for scenarios that include *N* &ndash; 1, *N* &ndash; 2, *N* &ndash; *x*.
  - Add in additional servers according to organizational need to ensure that the loss of a single or multiple servers does not exceed maximum peak capacity estimates.
  - Also consider that the growth plan and fault tolerance plan need to be integrated. For example, if one DC is required to support the load, but the estimate is that the load will be doubled in the next year and require two DCs total, there will not be enough capacity to support fault tolerance. The solution would be to start with three DCs. One could also plan to add the third DC after 3 or 6 months if budgets are tight.

    >[!NOTE]
    >Adding Active Directory-aware applications might have a noticeable impact on the DC load, whether the load is coming from the application servers or clients.

### Three-step process for the capacity planning cycle

In capacity planning, first decide what quality of service is needed. For example, a core datacenter supports a higher level of concurrency and requires more consistent experience for users and consuming applications, which requires greater attention to redundancy and minimizing system and infrastructure bottlenecks. In contrast, a satellite location with a handful of users does not need the same level of concurrency or fault tolerance. Thus, the satellite office might not need as much attention to optimizing the underlying hardware and infrastructure, which may lead to cost savings. All recommendations and guidance herein are for optimal performance, and can be selectively relaxed for scenarios with less demanding requirements.

The next question is: virtualized or physical? From a capacity planning perspective, there is no right or wrong answer; there is only a different set of variables to work with. Virtualization scenarios come down to one of two options:

- “Direct mapping” with one guest per host (where virtualization exists solely to abstract the physical hardware from the server)
- “Shared host”

Testing and production scenarios indicate that the “direct mapping” scenario can be treated identically to a physical host. “Shared host,” however, introduces a number of considerations spelled out in more detail later. The “shared host” scenario means that AD DS is also competing for resources, and there are penalties and tuning considerations for doing so.

With these considerations in mind, the capacity planning cycle is an iterative three-step process:

1. Measure the existing environment, determine where the system bottlenecks currently are, and get environmental basics necessary to plan the amount of capacity needed.
1. Determine the hardware needed according to the criteria outlined in step 1.
1. Monitor and validate that the infrastructure as implemented is operating within specifications. Some data collected in this step becomes the baseline for the next cycle of capacity planning.

### Applying the process

To optimize performance, ensure these major components are correctly selected and tuned to the application loads:

1. Memory
1. Network
1. Storage
1. Processor
1. Net Logon

The basic storage requirements of AD DS and the general behavior of well written client software allow environments with as many as 10,000 to 20,000 users to forego heavy investment in capacity planning with regards to physical hardware, as almost any modern server class system will handle the load. That said, the following table summarizes how to evaluate an existing environment in order to select the right hardware. Each component is analyzed in detail in subsequent sections to help AD DS administrators evaluate their infrastructure using baseline recommendations and environment-specific principals.

In general:

- Any sizing based on current data will only be accurate for the current environment.
- For any estimates, expect demand to grow over the lifecycle of the hardware.
- Determine whether to oversize today and grow into the larger environment, or add capacity over the lifecycle.
- For virtualization, all the same capacity planning principals and methodologies apply, except that the overhead of the virtualization needs to be added to anything domain related.
- Capacity planning, like anything that attempts to predict, is NOT an accurate science. Do not expect things to calculate perfectly and with 100% accuracy. The guidance here is the leanest recommendation; add in capacity for additional safety and continuously validate that the environment remains on target.

### Data collection summary tables

#### New environment

| Component | Estimates |
|-|-|
|Storage/Database Size|40 KB to 60 KB for each user|
|RAM|Database Size<br />Base operating system recommendations<br />Third-party applications|
|Network|1 GB|
|CPU|1000 concurrent users for each core|

#### High-level evaluation criteria

| Component | Evaluation criteria | Planning considerations |
|-|-|-|
|Storage/Database size|The section entitled “To activate logging of disk space that is freed by defragmentation” in [Storage Limits](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))| |
|Storage/ Database performance|<ul><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Write," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer"</li><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Reads/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Writes/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec"</li></ul>|<ul><li>Storage has two concerns to address<ul><li>Space available, which with the size of today’s spindle based and SSD based storage is irrelevant for most AD environments.</li> <li>Input/Output (IO) Operations available – In many environments, this is often overlooked. But it is important to evaluate only environments where there is not enough RAM to load the entire NTDS Database into memory.</li></ul><li>Storage can be a complex topic and should involve hardware vendor expertise for proper sizing. Particularly with more complex scenarios such as SAN, NAS, and iSCSI scenarios. However, in general, cost per Gigabyte of storage is often in direct opposition to cost per IO:<ul><li>RAID 5 has lower cost per Gigabyte than Raid 1, but Raid 1 has lower cost per IO</li><li>Spindle-based hard drives have lower cost per Gigabyte, but SSDs have a lower cost per IO</li></ul><li>After a restart of the computer or the Active Directory Domain Services service, the Extensible Storage Engine (ESE) cache is empty and performance will be disk bound while the cache warms.</li><li>In most environments AD is read intensive I/O in a random pattern to disks, negating much of the benefit of caching and read optimization strategies.  Plus, AD has a way larger cache in memory than most storage system caches.</li></ul>
|RAM|<ul><li>Database size</li><li>Base operating system recommendations</li><li>Third-party applications</li></ul>|<ul><li>Storage is the slowest component in a computer. The more that can be resident in RAM, the less it is necessary to go to disk.</li><li>Ensure enough RAM is allocated to store the operating system, Agents (antivirus, backup, monitoring), NTDS Database and growth over time.</li><li>For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage section to ensure that storage is properly sized.</li></ul>|
|Network|<ul><li>“Network Interface(\*)\Bytes Received/sec”</li><li>“Network Interface(\*)\Bytes Sent/sec”|<ul><li>In general, traffic sent from a DC far exceeds traffic sent to a DC.</li><li>As a switched Ethernet connection is full-duplex, inbound and outbound network traffic need to be sized independently.</li><li>Consolidating the number of DCs will increase the amount of bandwidth used to send responses back to client requests for each DC, but will be close enough to linear for the site as a whole.</li><li>If removing satellite location DCs, don’t forget to add the bandwidth for the satellite DC into the hub DCs as well as use that to evaluate how much WAN traffic there will be.</li></ul>|
|CPU|<ul><li>“Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read”</li><li>“Process(lsass)\\% Processor Time”</li></ul>|<ul><li>Nach dem Entfernen von Speicher als Engpass wirkt, beheben Sie die Menge an rechenleistung, die erforderlich sind.</li><li>Zwar nicht perfekt linear ist, kann die Anzahl der Prozessorkerne auf allen Servern innerhalb eines bestimmten Bereichs (z. B. eine Website) genutzt verwendet werden, um abzuschätzen, wie viele Prozessoren zur Unterstützung der Clientlast für die gesamte erforderlich sind. Fügen Sie die erforderlichen mindestvoraussetzungen, zum Verwalten der aktuellen Ebene des Diensts auf allen Systemen innerhalb des Bereichs.</li><li>Änderungen in der prozessorgeschwindigkeit, einschließlich der energieverwaltung im Zusammenhang mit Änderungen, die Auswirkungen aus der aktuellen Umgebung ermittelt wurden. Im Allgemeinen ist es unmöglich, genau zu bewerten, wie der Übergang von einem Prozessor mit 2,5 GHz auf ein 3-GHz-Prozessor die Anzahl der CPUs erforderlich verringern wird.</li></ul>|
|Anmeldedienst|<ul><li>"Netlogon (\*) \Semaphore erhält."</li><li>"Netlogon (\*) \Semaphore Timeouts"</li><li>"Netlogon (\*) \Average Semaphor Haltezeit"</li></ul>|<ul><li>NET-Anmeldung, Secure Channel / "MaxConcurrentApi" betrifft nur Umgebungen mit NTLM-Authentifizierungen und/oder die PAC-Überprüfung. Die PAC-Überprüfung ist in Versionen vor Windows Server 2008 standardmäßig aktiviert. Dies ist eine Clienteinstellung, damit die DCs betroffen sein werden, bis diese auf alle Clientsysteme deaktiviert ist.</li><li>Umgebungen mit erheblichen Vertrauensgrenzen-Authentifizierung, die innerhalb einer Gesamtstruktur-Vertrauensstellungen enthält, haben stärker gefährdet ist dies nicht Größe aufweisen.</li><li>Server Konsolidierungen erhöht die Parallelität von Cross-Trust-Authentifizierung.</li><li>Fall kämen müssen untergebracht werden, z. B. Cluster Fail-Failover, da Benutzer datasetwerte auf den neuen Clusterknoten erneut zu authentifizieren.</li><li>Einzelne Client-Systemen (z. B. ein Cluster) möglicherweise zu optimieren.</li></ul>|

## <a name="planning"></a>Planen

Für einen langen Zeitraum wurde der Community-Empfehlung für die größenanpassung von AD DS in "in so viel RAM, als die Größe der Datenbank eingefügt." Zum größten Teil, es empfohlen, die meisten Umgebungen wird erforderlich, um kümmern. Das Verwenden von AD DS-Ökosystem in letzter Zeit aber sehr viel größer, wie der AD DS-Umgebungen, die sich seit seiner Einführung im Jahr 1999. Obwohl die Erhöhung der rechenleistung und das Wechseln von X86 Architekturen X64 Architekturen hat die Größe für die Leistung für eine größere Anzahl von Kunden, die AD DS auf physischer Hardware, das Wachstum der Virtualisierung Ausführen komplexer Aspekte wieder die Optimierung sorgen für eine größere Zielgruppe als vor dem eingeführt.

Die folgende Anleitung ist daher zum Bestimmen und Planen Sie die Anforderungen der Active Directory als Dienst unabhängig davon, ob sie in einem physischen, sowohl virtuelle/physische oder ein rein virtualisierten Szenario bereitgestellt wird. Es wird daher die Auswertung zu jedem der vier Hauptkomponenten unterteilen: Speicher, Speicher, Netzwerk und Prozessor. Kurz gesagt, ist das Ziel zum Maximieren der Leistung, AD DS, um wie in der Nähe Prozessor gebunden wie möglich zu erhalten.

## <a name="ram"></a>RAM

Einfach, desto kann, die im Arbeitsspeicher erhalten, zwischengespeichert werden, ist es weniger zu auf dem Datenträger erforderlich. Um der Skalierbarkeit des Servers die Mindestmenge an Arbeitsspeicher zu maximieren sollte die Summe der aktuellen Datenbankgröße, die Gesamtgröße von SYSVOL, das Betriebssystem Amount "und" die Anbieter-Empfehlungen für die Agents (antivirus, Überwachung, Sicherung usw. empfohlen werden ). Ein zusätzlicher Wert sollte für Wachstum im Laufe der Lebensdauer des Servers hinzugefügt werden. Dies ist ökologischen subjektive wird basierend auf Schätzungen der Wachstum der Datenbank, die basierend auf umgebungsänderungen.

Für Umgebungen, in denen die Größe des Arbeitsspeichers maximiert nicht ist, wirksam (z. B. eine Satelliten-Speicherorte) oder nicht machbar (DIT-Datenbank ist zu groß) und Verweis des Speicherabschnitts, um sicherzustellen, dass der Speicher ordnungsgemäß dient.

Eine begleitende, die in der Größe des Arbeitsspeichers im Allgemein Kontext erscheint, Ändern der Größe der Auslagerungsdatei ist. In demselben Kontext wie alle anderen verknüpft Speicher, das Ziel besteht darin zu minimieren, soll die wesentlich langsamer Datenträger. Daher die Frage sollte wechseln Sie zu "wie die Auslagerungsdatei dimensioniert sein muss?" um "ist wie viel RAM erforderlich, um Paging zu minimieren?" Die Antwort auf die zweite Frage wird in den restlichen Teil dieses Abschnitts beschrieben. Dies bewirkt, dass die meisten der Diskussion zum Anpassen der Größe der Auslagerungsdatei in den Bereich der Allgemeines Betriebssystem Empfehlungen und die Notwendigkeit, die das System für Speicherabbilder, konfigurieren, die nicht mit AD DS-Leistung verbunden sind.

### <a name="evaluating"></a>Auswerten von

Die Größe des Arbeitsspeichers, der einem Domänencontroller (DC) muss ist tatsächlich eine komplexe Aufgabe, aus diesen Gründen:

- Hohe Potenzial für Fehler beim Versuch, ein vorhandenes System verwenden, um abzuschätzen, wie viel Arbeitsspeicher benötigt wird, wie LSASS unter die speicherauslastung, maggie künstlich Entleeren erforderlich.
- Die subjektive Tatsache, dass nur ein einzelnen DC benötigt, zwischengespeichert, was "interessanten" seinen Clients ist. Dies bedeutet, dass die Daten, die auf einem Domänencontroller an einem Standort mit nur einem Exchange-Server zwischengespeichert werden müssen als die Daten sehr unterschiedliche werden, die auf einem Domänencontroller zwischengespeichert werden, die nur Benutzer authentifiziert werden soll.
- Der Arbeit RAM für jeden Domänencontroller auf von Fall zu Fall auswerten tragbar ist und ändert sich die Umgebung ändern.
- Die Kriterien hinter der Empfehlung helfen und fundierte Entscheidungen treffen: 
- Je mehr können, die im Arbeitsspeicher zwischengespeichert werden, desto weniger ist es erforderlich, auf der Festplatte. 
- Speicher ist bei weitem die langsamsten Komponenten eines Computers. Zugriff auf Daten auf Spindle- und SSD Speichermedien, die Größenordnung von 1.000.000 x langsamer als der Zugriff auf Daten im Arbeitsspeicher ist.

Daher wird um die Skalierbarkeit des Servers an, die Mindestmenge an Arbeitsspeicher zu erhöhen. die Summe der aktuellen Datenbankgröße, die Gesamtgröße von SYSVOL, das Betriebssystem Amount "und" die Anbieter-Empfehlungen für die Agents (Antivirus, Überwachung, Sicherung, empfohlen und so weiter). Fügen Sie zusätzliche Beträge um Wachstum im Laufe der Lebensdauer des Servers zu ermöglichen. Dies ist ökologischen subjektive wird basierend auf Schätzungen der Wachstum der Datenbank. Für Satelliten-Standorte mit einer kleinen Gruppe von Endbenutzern, können jedoch diese Anforderungen gelockert werden, da diese Websites nicht Cache so weit benötigen die meisten Anforderungen zu verarbeiten.

Für Umgebungen, in dem die Größe des Arbeitsspeichers maximiert kein, Kosten effektiv (z. B. eine Satelliten-Speicherorte) oder nicht möglich (DIT-Datenbank ist zu groß), Referenz, die Größe des Speicherabschnitts, um sicherzustellen, dass der Speicher ordnungsgemäß konfiguriert ist.

> [!NOTE]
> Eine begleitende beim Festlegen der Speichergröße Ändern der Größe der Auslagerungsdatei ist. Da das Ziel ist, zu minimieren, soll die wesentlich langsamer Datenträger, geht die Frage, von "sollte wie die Auslagerungsdatei groß sein?" um "ist wie viel RAM erforderlich, um Paging zu minimieren?" Die Antwort auf die zweite Frage wird in den restlichen Teil dieses Abschnitts beschrieben. Dies bewirkt, dass die meisten der Diskussion zum Anpassen der Größe der Auslagerungsdatei in den Bereich der Allgemeines Betriebssystem Empfehlungen und die Notwendigkeit, die das System für Speicherabbilder, konfigurieren, die nicht mit AD DS-Leistung verbunden sind.

### <a name="virtualization-considerations-for-ram"></a>Überlegungen zur Virtualisierung für Arbeitsspeicher

Vermeiden Sie Arbeitsspeicher zu Commit auf dem Host. Das grundlegende Ziel hinter optimieren die Größe des Arbeitsspeichers ist, die viel Zeit aufgewendet, die auf Datenträger zu minimieren. In Virtualisierungsszenarios das Konzept der Arbeitsspeicher zu Commit vorhanden ist, in dem die Gäste mehr RAM zugewiesen ist und dann auf dem physischen Computer vorhanden ist. In und von sich selbst ist kein Problem. Es wird ein Problem, wenn es sich bei der insgesamt von aller Gäste aktiv verwendete Arbeitsspeicher überschreitet die Größe des RAM auf dem Host und der zugrunde liegenden Host startet, Paging. Leistung wird Bindung in Fällen, in denen der Domänencontroller die Datei "Ntds.dit" zum Abrufen von Daten, geht der Domänencontroller wird die Auslagerungsdatei, zum Abrufen von Daten oder der Host wird auf den Datenträger zum Abrufen von Daten, die der Gast im Arbeitsspeicher wird.

### <a name="calculation-summary-example"></a>Beispiel einer Berechnung

|Komponente|Geschätzte Arbeitsspeicher (Beispiel)|
|-|-|
|Zugrunde liegende Betriebssystem Empfohlener Arbeitsspeicher (Windows Server 2008)|2 GB|
|Interne LSASS-Aufgaben|200 MB|
|Überwachungs-agent|100 MB|
|Antivirensoftware|100 MB|
|Datenbank (globaler Katalog)|8,5 GB wirklich???|
|Puffer für die Sicherung ausgeführt wird, melden Sie sich ohne Auswirkungen auf Administratoren|1 GB|
|Gesamt|12 GB|

**Empfohlen: 16 GB**

Im Laufe der Zeit kann davon ausgegangen, dass mehr Daten in der Datenbank hinzugefügt werden werden, und der Server möglicherweise in der Produktion 3 bis 5 Jahren erfolgen. Basierend auf eine Schätzung der Zunahme von 33 %, wäre 16 GB RAM auf einem physischen Server Platzieren eines angemessenen Zeitraums. In einem virtuellen Computer ist erhält die Leichtigkeit, mit denen Einstellungen geändert werden können, und RAM des virtuellen Computers hinzugefügt werden kann, ab dem mit der Plan zum Überwachen und aktualisieren Sie in der Zukunft 12 GB sinnvoll.

## <a name="network"></a>Network

### <a name="evaluating"></a>Auswerten von
In diesem Abschnitt liegt zum Auswerten der der Anforderungen in Bezug auf die Replikationsdatenverkehr, der konzentriert sich auf die WAN-Datenverkehr und wird gründlich in behandelt [Active Directory-Replikationsdatenverkehr](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10)), als es zum Auswerten der insgesamt ist Bandbreite und Netzwerkkapazität, die erforderlich sind, einschließlich Clientabfragen, Gruppenrichtlinien-Anwendungen und So weiter. Für vorhandene Umgebungen kann dies mithilfe von Leistungsindikatoren gesammelt werden "Netzwerkschnittstelle (\*) \Bytes empfangen/s," und "Netzwerkschnittstelle (\*) \Bytes gesendet/s." Beispiel-Intervalle für die Netzwerkschnittstelle-Leistungsindikatoren in 15, 30 oder 60 Minuten. Alles wird im Allgemeinen zu flüchtigen für aussagekräftige Messergebnisse liegen; etwas größer wird täglich sieht übermäßig glätten.

> [!NOTE]
> Im Allgemeinen ist der Großteil des Netzwerkdatenverkehrs für einen DC ausgehender, wie der DC-Clientabfragen reagiert. Dies ist der Grund für den Fokus auf den ausgehenden Datenverkehr, aber es wird empfohlen, jede Umgebung für eingehenden Datenverkehr auch auswerten. Die gleichen Methoden können zum Behandeln und zu den Anforderungen an den eingehenden Datenverkehr verwendet werden. Weitere Informationen finden Sie im Knowledge Base-Artikel [929851: Der dynamische Standardportbereich für TCP/IP hat sich geändert, in Windows Vista und Windows Server 2008](http://support.microsoft.com/kb/929851).

### <a name="bandwidth-needs"></a>Bedarf an Netzwerkbandbreite

Planung für netzwerkskalierbarkeit zwei unterschiedliche Nachrichtenkategorien behandelt: die Menge des Datenverkehrs und die CPU-Auslastung zu laden, aus der Netzwerkdatenverkehr. Jedes dieser Szenarien ist einfach im Vergleich zu einigen der anderen Themen in diesem Artikel.

Bei der Auswertung, wie viel Datenverkehr muss unterstützt werden, gibt es zwei eindeutige Kategorien der kapazitätsplanung für AD DS bezüglich des Netzwerkverkehrs. Die erste ist die Replikationsdatenverkehr, der zwischen Domänencontrollern durchsucht und wird gründlich behandelt, in der Referenz zur [Active Directory-Replikationsdatenverkehr](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10)) und ist immer noch relevant ist, auf die aktuellen Versionen von AD DS. Die zweite ist der standortinternen-Client-zu-Server-Datenverkehr. Eines der einfacheren Szenarien, die hauptsächlich für standortübergreifende Datenverkehr planen empfängt kleine Anforderungen von Clients Bezug auf die großen Mengen von Daten, die an die Clients gesendet. 100 MB wird im Allgemeinen in Umgebungen mit bis zu 5.000 Benutzer pro Server, an einem Standort ausreichend sein. Mit einem 1-GB-Netzwerkadapter und Empfangen von empfangsseitige Skalierung (RSS), wird Unterstützung für alles, was oben 5.000 Benutzer empfohlen. Betrachten Sie dieses Szenario, insbesondere im Fall von Serverkonsolidierungsszenarios, überprüft die Netzwerkschnittstelle (\*) \Bytes/sec für alle Domänencontroller an einem Standort zusammen hinzuzufügen, und teilen Sie durch die vorgegebene Anzahl von Domänencontrollern, um sicherzustellen, dass es ist eine angemessene Kapazität. Die einfachste Möglichkeit hierzu ist, verwenden Sie die Ansicht "Gestapelte Fläche" in Windows-Zuverlässigkeits- und Leistungsüberwachung (früher als Perfmon bezeichnet), um sicherzustellen, dass alle Indikatoren sind die gleichen skaliert.

Im folgenden Beispiel (auch bekannt als ein wirklich sehr komplexe Art zu überprüfen, ob die allgemeine Regel gilt für eine bestimmte Umgebung). Die folgenden Annahmen:

- Ziel ist es, den Fußabdruck auf möglichst wenige Server wie möglich zu verringern. Im Idealfall ein Server wird die Last tragen und ein weiteren Server für die Redundanz bereitgestellt wird (*N* + 1-Szenario). 
- In diesem Szenario wird der aktuellen Netzwerkadapter unterstützt nur 100 MB, und Sie befindet sich in einer Umgebung mit Switch.  
  Die Nutzung der Netzwerkbandbreite maximal Ziel ist 60 % in einem N-Szenario (Verlust eines Domänencontrollers).
- Jeder Server hat etwa 10.000 verbundenen Clients.

Erworbene wissen von den Daten im Diagramm (Netzwerkschnittstelle (\*) \Bytes gesendet/s):

1. Die Business-Tag beginnt Planungsansicht ca. 5:30 und Winde nach unten um 7:00 Uhr.
1. Der höchsten Auslastung spitzenauslastungszeit liegt zwischen 8:00 Uhr und 8:15 Uhr, mit mehr als 25 Protokollbytes gesendet/Sekunde auf dem zentralen DC.  
   > [!NOTE]
   > Alle Leistungsdaten ist historisch. Daher gibt der maximale Datenpunkt um 8:15 die Last zwischen 8:00 Uhr, 8:15.
1. Es gibt Spitzen vor 4:00 Uhr, mit mehr als 20 Bytes gesendet/s auf dem DC aktivsten konnte entweder Laden aus verschiedenen Zeitzonen anzugeben oder Infrastruktur-Aktivität, z. B. Sicherungen im Hintergrund. Da der Spitzenwert um 8:00 Uhr. diese Aktivität überschreitet, ist es nicht relevant.
1. Es gibt fünf Domänencontroller am Standort.
1. Die maximale Auslastung ist etwa 5.5 MB/s pro DC, der 44 % der 100-MB-Verbindung darstellt. Anhand dieser Daten kann es geschätzt werden, dass die gesamte erforderliche Bandbreite zwischen 8:00 und 08:15 Uhr 28 MB/s ist.
   >[!NOTE]
   >Achten Sie darauf, dass mit der Tatsache, die Netzwerkschnittstelle gesendet/empfangen-Leistungsindikatoren sind in Bytes und die Netzwerkbandbreite in Bits gemessen wird. 100 MB &divide; 8 = 12,5 MB, 1 GB &divide; 8 = 128 MB.
  
Schlussfolgerungen:

1. Diese aktuelle Umgebung erfüllt die N + 1 Grad der Fehlertoleranz zu 60 % Ziel. Ein System offline geschaltet wird die Bandbreite pro Server vom etwa 5,5 MBIT/s (44 %) verschieben. von ca. 7 MB/s (56 %).
1. Basierend auf den zuvor genannten Ziel auf einem Server konsolidieren, diese beiden überschreitet die maximale zielauslastung und theoretisch die mögliche Auslastung für eine 100-MB-Verbindung.
1. Mit einer 1 GB-Verbindung stellt diese 22 % der Gesamtkapazität dar.
1. Unter normalen betriebsbedingungen in die *N* + 1 Szenario Clientauslastung bei ca. 14 MBIT/s pro Server oder 11 % der Kapazität relativ gleichmäßig verteilt werden.
1. Um sicherzustellen, dass die Kapazität ausreichend ist, während der nichtverfügbarkeit eines Domänencontrollers, den normalen Betrieb Ziele pro Server wäre etwa 30 % Netzwerk-Auslastung oder 38 MB/s pro Server. Failoverziele würde es sich um 60 % Netzwerkauslastung oder 72 MB/s pro Server sein.  
  
Kurz gesagt, wird die endgültige Bereitstellung von Systemen müssen einen Netzwerkadapter 1 GB festgelegt, und es wird an der Netzwerkinfrastruktur, die genannte laden unterstützen, verbunden sein. Ein weiterer Hinweis ist, dass die Menge an Netzwerkverkehr generiert, die CPU-Auslastung von Netzwerkkommunikation kann erhebliche Auswirkungen haben und die maximale Skalierbarkeit von AD DS beschränkt. Dieser Prozess kann verwendet werden, zum Schätzen des Umfangs der eingehenden Kommunikation an den DC. Aber wenn die auseinandersetzen, da der ausgehende Datenverkehr relativ zu den eingehenden Datenverkehr, academic Übung für die meisten Umgebungen. Sicherstellen, dass hardwareunterstützung für RSS ist wichtig in Umgebungen mit mehr als 5.000 Benutzer pro Server. Für Szenarien mit hoher Netzwerkverkehr kann der Interrupt Load balancing einen Engpass darstellen. Dies kann erkannt werden, indem Prozessor (\*)\% Interruptzeit CPUs ungleichmäßig verteilt wird. RSS-fähige Netzwerkkarten können diese Einschränkung zu minimieren und Skalierbarkeit zu erhöhen.

> [!NOTE]
> Ein ähnlicher Ansatz kann verwendet werden, um die zusätzliche Kapazität erforderlich zu schätzen, bei der Konsolidierung von Rechenzentren oder Zurückziehen eines Domänencontrollers in einem Satellitenstandort. Sammeln einfach den eingehender und ausgehender Datenverkehr für Clients und auf die die Menge an Datenverkehr, der nun für die WAN-Verbindungen vorhanden sein werden.  
>  
> In einigen Fällen erleben Sie möglicherweise mehr Datenverkehr als erwartet, da der Datenverkehr ist langsamer, z. B. wenn zertifikatüberprüfung nicht kurze Timeouts auf das WAN zu erfüllen. Aus diesem Grund sollte WAN-größenanpassung und Auslastung, die ein iterativer, fortlaufender Prozess sein.

### <a name="virtualization-considerations-for-network-bandwidth"></a>Überlegungen zur Virtualisierung für Netzwerkbandbreite

Es ist einfach, Empfehlungen für einen physischen Server: 1 GB für Server, die mehr als 5000 Benutzer unterstützen. Sobald mehrere Gäste Freigeben einer zugrunde liegenden Infrastruktur für den virtuellen Switch, ist zusätzliche Aufmerksamkeit erforderlich, um sicherzustellen, dass der Host zur Unterstützung aller Gäste auf dem System ausreichend Netzwerkbandbreite ist und daher die zusätzliche strenge erfordert. Dies ist nicht mehr als eine Erweiterung die Netzwerkinfrastruktur auf den Hostcomputer sicherzustellen. Dies ist unabhängig davon, ob das Netzwerk, einschließlich der Domänencontroller als VM-Gast mit den Netzwerkverkehr über einen virtuellen Switch auf einem Host ausgeführt wird oder ob Sie direkt mit einem physischen Switch verbunden. Der virtuelle Switch ist nur eine weitere Komponente, in denen der Uplink muss, um die Menge der übertragenen Daten zu unterstützen. Daher sollte der physischen Netzwerkadapter physischen Host verknüpft, mit dem Switch unterstützen die DC-Auslastung sowie andere Gäste, die für die Freigabe von des virtuellen Switches mit dem physischen Netzwerkadapter verbunden sind.

### <a name="calculation-summary-example"></a>Beispiel einer Berechnung

|System|Maximale Bandbreite|
|-|-|
DC 1|6.5 MBIT/s|
DC 2|Preis von 6,25 MBIT/s|
|DC 3|Preis von 6,25 MBIT/s|
|DC 4|5,75 MBIT/s|
|DC 5|4,75 MBIT/s|
|Gesamt|28,5 MBIT/s|

**Empfohlen: 72 MBIT/s** (28.5 MBIT/s geteilt um 40 %)

|/ Den Stammverwaltungsserver-System(en) Zielanzahl|Gesamtbandbreite (von oben)|
|-|-|
|2|28,5 MBIT/s|
|Normale Verhalten|28,5 &divide; 2 = 14.25 MBIT/s|

Wie immer können im Laufe der Zeit ausgegangen werden Clientbelastung erhöht, und dieses Wachstum sollte so gut wie möglich geplant werden. Die empfohlene Menge zu planen, würde für eine geschätzte Zunahme des Netzwerkdatenverkehrs von 50 % ermöglichen.

## <a name="storage"></a>Speicher

Planen der Speicher bildet zwei Komponenten:

- Kapazität und Speichergröße
- Leistung

Eine sehr viel Zeit und Dokumentation wird für die Planung Kapazität, Leistung, die vollständig oft übersehen verlassen aufgewendet. Mit aktuellen Hardwarekosten, die meisten Umgebungen sind nicht groß genug, dass entweder dieser ist tatsächlich ein Problem, und die Empfehlung, "put in so viel RAM, als die Größe der Datenbank" in der Regel behandelt den Rest, obwohl sie zu viel des guten für Satelliten-Speicherorte in möglicherweise größer Umgebungen.

### <a name="sizing"></a>Größenanpassung

#### <a name="evaluating-for-storage"></a>Für die Speicherung auswerten

Verglichen mit 13 Jahren bei Active Directory eingeführt wurde, eine Zeit, die bei 4 GB und 9 GB-Laufwerken für die am häufigsten verwendeten Laufwerkgrößen wurden, ist die größenanpassung für Active Directory nicht selbst eine Überlegung für alle, sondern umfangreichsten. Mit der kleinsten verfügbaren Festplatte können in der 180-GB-Bereich, das gesamte Betriebssystem, SYSVOL und NTDS.dit-Größen ganz einfach auf einem bestimmten Laufwerk entsprechen. Daher wird empfohlen, die hohen Investitionen in diesem Bereich als veraltet markiert.

Wird nur empfohlen berücksichtigen sollten, um sicherzustellen, dass 110 % der Größe "Ntds.dit" sein, um die Defragmentierung zu aktivieren. Darüber hinaus sollten Unterkünfte für Wachstum während der Lebensdauer der Hardware vorgenommen werden.

Der erste und wichtigste Aspekt wertet wie groß die NTDS.dit und SYSVOL sind. Diese Messungen führt in größenanpassung sowohl feste Datenträger und RAM-Zuordnung. Aufgrund der (relativ) niedrigen Kosten dieser Komponenten muss die Berechnungen nicht strengen und präzise sein. Finden Sie Informationen zu dieser auswerten für vorhandene und neue Umgebungen Sie in finden der [Datenspeicherung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961771(v=technet.10)) Reihe von Artikeln. Vor allem in den folgenden Artikeln:

- **Für vorhandene Umgebungen &ndash;**  im Abschnitt mit dem Titel "So aktivieren die Protokollierung von Speicherplatz, der freigegeben wird, durch die Defragmentierung" in diesem Artikel [Speicherlimits](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10)).
- **Für neue Umgebungen &ndash;**  im Artikel [Wachstum Schätzungen für Active Directory-Benutzer und Organisationseinheiten](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961779(v=technet.10)).

  > [!NOTE]
  > Die Artikel basieren auf Daten Größe Schätzungen, die zum Zeitpunkt der Version von Active Directory unter Windows 2000 vorgenommen. Verwenden Sie die Größe der Objekte, die die tatsächliche Größe der Objekte in Ihrer Umgebung widerspiegeln.

Bei der Überprüfung der vorhandener Umgebungen mit mehreren Domänen möglicherweise abweichungen bei der Datenbankgröße. Wenn dies true ist, verwenden Sie die kleinste globalen Katalog (GC) und die Größe des nicht-GC.  

Die Größe der Datenbank kann zwischen Betriebssystemversionen variieren. Domänencontroller, dass die ältere Betriebssysteme ausführen, z. B. Windows Server 2003 eine kleinere Datenbankgröße als einen Domänencontroller enthält, die ein neueres Betriebssystem wie z. B. Windows Server 2008 R2 ausgeführt wird, insbesondere dann, wenn Funktionen solche Active Directory-Papierkorb "bin" oder die Serverspeicherung von Anmeldeinformationen aktiviert sind.

> [!NOTE]  
  >
>- Beachten Sie, dass die Schätzungen in Wachstum schätzt für Active Directory-Benutzer und Organisationseinheiten anzugeben, dass etwa 450 MB Speicherplatz beansprucht werden 100.000 Benutzer (in derselben Domäne) aus, für neue Umgebungen. Beachten Sie, dass die Attribute gefüllt enorme Auswirkungen auf die Gesamtmenge verfügen können. Attribute werden sowohl von Drittanbietern als auch Microsoft-Produkten, einschließlich Microsoft Exchange Server und Lync auf viele Objekte gefüllt. Eine Bewertung anhand des Portfolios der Produkte in der Umgebung wird bevorzugt, aber die Übung, in denen detailliert erläutert, die mathematische und Tests für genaue Schätzungen für alle, aber die größten Umgebungen möglicherweise nicht zu viel Zeit und Mühe.
>- Sicherstellen Sie, dass 110 % der Größe als freier Speicherplatz verfügbar ist, damit offline können NTDS.dit defragmentieren, und Planen Sie für Wachstum, über eine Lebensdauer der drei bis fünf-Jahres-Hardware. Der angegebene wie billigen Speicher ist, schätzen Speicher auf 300 % der Größe der DIT wie speicherbelegung für Wachstum und der potenzielle Bedarf für offline sicher ist defragmentiert.

#### <a name="virtualization-considerations-for-storage"></a>Überlegungen zur Virtualisierung für Speicher

In einem Szenario, in denen mehrere Dateien der virtuellen Festplatte (VHD) auf einem einzelnen Volume zugewiesen werden, Größe verwendet, die eine feste Datenträger mindestens 210 % (100 % der DIT + 110 % freier Speicherplatz) die Größe der DIT, stellen Sie sicher, dass ausreichend Speicherplatz reserviert ist.  

#### <a name="calculation-summary-example"></a>Beispiel einer Berechnung

|Vom Auswertungsphase gesammelten Daten| |
|-|-|
|NTDS.dit-Größe|35 GB|
|Defragmentieren Modifizierer, um offline zu ermöglichen|2.1|
|Gesamtspeicher erforderlich|UM 73,5 GB|

> [!NOTE]
> Dieser Speicher erforderlich ist, zusätzlich zu dem Speicher für SYSVOL, Betriebssystem, Auslagerungsdatei, temporäre Dateien, lokal zwischengespeicherte Daten (z. B. Installer-Dateien) und Anwendungen erforderlich sind.

### <a name="storage-performance"></a>Speicherleistung

#### <a name="evaluating-performance-of-storage"></a>Analysieren der Leistung des Speichers

Wie die langsamste Komponente in einem beliebigen Computer haben Speicher die größte negative Auswirkung auf Client-Benutzeroberfläche. Für diese Umgebungen, die Groß können genug für die die größenempfehlungen für RAM nicht durchführbar, sind die Folgen der abfrageparallelität, Planen Speicher für Leistung verheerend sein.  Der Komplexität und die Arten von Storage-Technologie noch weiter erhöhen das Risiko eines Ausfalls auch, wie die Relevanz der lange bestehendes, die Best Practices "operating System, Protokolle und -Datenbank auf separaten physischen Datenträgern put", der für die nützliche Szenarien begrenzt ist.  Dies ist, da die bewährte Methode für lange bestehendes auf der Annahme, die besteht darin, dass basierend "Disk" ist eine dedizierte Spindel, und dies zulässig, e/a, isoliert werden.  Diese Annahmen, mit denen "true" sind nicht mehr mit der Einführung von relevant:

- Neue Speichertypen und virtualisierten und gemeinsam genutzte speicherszenarien
- Freigegebene Spindeln auf einem Storage Area Network (SAN)
- VHD-Datei auf einem SAN oder NAS-
- Solid-State-Laufwerke
- Mehrstufiger Speicherarchitekturen (z. B. SSD-Speicherebene Zwischenspeichern größeren Spindel-basierten Speicher)

Kurz gesagt, wird das Endziel von allen Speicher Leistung bemühungen, unabhängig vom zugrunde liegenden Architektur und Entwurf, um sicherzustellen, dass die erforderliche Menge an e/a-Vorgänge pro Sekunde (IOPS) verfügbar sind und, dass die IOPS innerhalb einer akzeptablen Zeitrahmens ausgeführt . Dieser Abschnitt enthält Gewusst wie: bewerten, welche AD DS-Anforderungen des zugrunde liegenden Speichers, um sicherzustellen, dass speicherlösungen ordnungsgemäß entworfen wurden.  Die Variabilität der Technologien von heute wird angegeben, ist es ratsam, mit der Speicheranbieter, um sicherzustellen, dass ausreichend IOPS.  Verweisen auf den Anhang C für die Grundlagen zum Entwerfen der Szenarien mit herkömmlichen lokalen Speicher für diese Szenarien mit dem lokal verbundenen Speicher.  Diese Prinzipale in der Regel gelten, für komplexere Speicherebenen und hilft auch im Dialogfeld mit den Anbietern, die Back-End-Speicher-Lösungen unterstützen.

- Wenn die Breite Spektrum von Speicheroptionen zur Verfügung stehen, empfiehlt es sich die Erfahrung des Supportteams von Hardware oder Anbieter, um sicherzustellen, dass die jeweilige Lösung die Anforderungen von AD DS in Verbindung setzen. Die folgenden Zahlen stellen die Informationen, die den Speicher für Spezialisten eingegeben werden müssten.

Verwenden Sie für Umgebungen, in dem die Datenbank im Arbeitsspeicher gespeichert werden zu groß ist die Leistungsindikatoren, um zu bestimmen, wie viel e/a unterstützt werden muss:

- Logischer Datenträger (\*) \Avg Sek./Lesevorgänge (z. B., wenn "Ntds.dit", auf dem Laufwerk D: gespeichert ist / Laufwerk, der vollständige Pfad wäre ein logischer Datenträger (d:)) \Avg Sek./Lesevorgänge)
- Logischer Datenträger (\*) \Avg Sek./Schreibvorgänge
- Logischer Datenträger (\*) \Avg Sek./Übertragung
- LogicalDisk(\*)\Reads/sec
- LogicalDisk(\*)\Writes/sec
- LogicalDisk(\*)\Transfers/sec

Diese sollten in 15/30/60-Minuten-Intervalle von den Anforderungen für die aktuelle Umgebung Vergleichstests Stichproben erstellt werden.

#### <a name="evaluating-the-results"></a>Auswertung der Ergebnisse

> [!NOTE]
> Der Schwerpunkt liegt auf Lesevorgänge aus der Datenbank angezeigt, da es sich in der Regel die anspruchsvollsten Komponente handelt, die gleiche Logik für Schreibvorgänge in die Protokolldatei angewendet werden kann, durch Ersetzen von logischer Datenträger ( *\<Log mit NTDS-\>* ) \Avg Sek./Schreibvorgänge und logischer Datenträger ( *\<Log mit NTDS-\>* ) \Writes/sec):
>  
> - Logischer Datenträger ( *\<NTDS\>* ) \Avg Sek./Lesevorgänge gibt an, und zwar unabhängig davon, ob der aktuelle Speicher angemessen dimensioniert ist.  Wenn die Ergebnisse ungefähr gleich ist, die Datenträger-Zugriffszeit für den Datenträgertyp, logischer Datenträger ( *\<NTDS\>* ) \Reads/sec ist ein gültiges Measure.  Überprüfen Sie die Hersteller-Spezifikationen für den Speicher auf dem Back-End, aber gutes Bereiche für logischer Datenträger ( *\<NTDS\>* ) \Avg Sek./Lesevorgänge wäre etwa:
>   - 7200 – 9, 12,5 Millisekunden (ms)
>   - 10.000 – 6 bis 10 ms.
>   - 15.000 – 4 bis 6 ms  
>   - SSD: 1 bis 3 ms  
>   - >[!NOTE]
>     >Empfehlungen vorhanden sind, die besagt, dass die speicherleistung unter 15ms auf 20 ms (abhängig von der Quelle) beeinträchtigt wird.  Der Unterschied zwischen den oben angegebenen Werten und den anderen Leitfäden ist, dass die oben genannten Werte der normalen Betriebsbereich.  Die anderen Empfehlungen sind Anleitungen, um zu ermitteln, wann die Clientfunktionen erheblich beeinträchtigt wird, und offensichtlich wird, zur Problembehandlung.  Verweis Anhang C eine detailliertere Beschreibung.
> - Logischer Datenträger ( *\<NTDS\>* ) \Reads/sec ist die Menge an e/a, die ausgeführt wird.
>   - Wenn logischer Datenträger ( *\<NTDS\>* ) \Avg Sek./Lesevorgänge liegt im optimalen Bereich für den Back-End-Speicher, logischer Datenträger ( *\<NTDS\>* ) \Reads/ s kann direkt in den Speicher verwendet werden.
>   - Wenn logischer Datenträger ( *\<NTDS\>* ) \Avg Sek./Lesevorgänge liegt nicht innerhalb des optimalen Bereichs für den Back-End-Speicher, zusätzliche e/a gemäß der folgenden Formel erforderlich ist:
>     > (Logischer Datenträger ( *\<NTDS\>* ) \Avg Sek./Lesevorgänge) &divide; (physische Medien Disk Zugriffszeit) &times; (logischer Datenträger ( *\<NTDS\>* ) \Avg Sek./Lesevorgänge)

Überlegungen:

- Beachten Sie, dass wenn der Server mit einer keine optimale Menge an Arbeitsspeicher konfiguriert ist, diese Werte zu Planungszwecken ungenau.  Sie werden fälschlicherweise auf der maximale dauerhafte Durchsatz und können als nur im ungünstigsten Fall weiterhin verwendet werden.
- Hinzufügen von/optimieren RAM wird insbesondere eine Verringerung der beim Lesen e/a Laufwerk (logischer Datenträger ( *\<NTDS\>* ) \Reads/Sec.  Dies bedeutet, dass die speicherlösung möglicherweise nicht stabil als ursprünglich berechnete sein.  Leider kann nichts je spezifischer als dieser allgemeinen Aussage ökologischen Clientauslastung und Hilfestellungen abhängt bereitgestellt werden.  Die beste Option ist Storage Größe nach dem Optimieren von Arbeitsspeicher anpassen.

#### <a name="virtualization-considerations-for-performance"></a>Überlegungen zur Virtualisierung für Leistung

Ähnlich wie all die vorherigen Diskussionen der Virtualisierung, ist der Schlüssel um sicherzustellen, dass die zugrunde liegende freigegebene Infrastruktur kann die Last der Domänencontroller unterstützen, sowie die anderen Ressourcen, die mit dem zugrunde liegenden, Medien und alle Pfade freigegeben. Dies ist die "true" gibt an, ob ein physischen Domänencontroller die gleichen zugrunde liegenden Medien auf einem SAN, NAS oder iSCSI-Infrastruktur als anderen Servern oder Anwendungen, freigibt, ob ein Gast mit Pass-through-Zugriff auf ein SAN, NAS oder iSCSI-Infrastruktur, die gemeinsam die zugrunde liegende Medium, oder wenn der Gast eine VHD-Datei, die befindet sich auf freigegebene Medien lokal oder ein SAN, NAS oder iSCSI-Infrastruktur verwendet wird. Die Ausübung der Planung geht es um sicherzustellen, dass die zugrunde liegenden Medien, die Gesamtlast alle Consumer unterstützen können.

Darüber hinaus hinsichtlich der Gast besteht wie zusätzliche Codepfade, die durchlaufen werden müssen stehen, dass über einen Host, auf Speicher zu Auswirkungen auf die Leistung. Überrascht nicht, dass Speicher Leistungstests gibt an, dass die Virtualisierung von wirkt sich auf den Durchsatz, die auf die prozessorauslastung des Hostsystems subjektive ist (siehe Anhang A: CPU-Größenanpassung Kriterien), das wird natürlich durch die Ressourcen des Hosts gefordert, durch den Gast beeinflusst. Dies trägt zu den Überlegungen zur Virtualisierung in Bezug auf die von verarbeitungsanforderungen in einem Szenario mit virtualisierten (finden Sie unter [Überlegungen zur Virtualisierung für die Verarbeitung](#virtualization-considerations-for-processing)).

Deshalb wird diese komplexer ist, dass es eine Vielzahl von verschiedenen Speicheroptionen kennen, die verfügbar sind, dass alle anderen leistungsbeeinträchtigungen. Verwenden Sie als eine sichere Schätzung, bei der Migration von physischen zu virtuellen einen Multiplikator dieser 1.10 für die verschiedenen Speicheroptionen für virtualisierte Gäste in Hyper-V, z.B. Pass-Through-Speicher, SCSI-Adapter oder IDE anpassen. Die Anpassungen, die vorgenommen werden, bei der Übertragung zwischen den verschiedenen Szenarien sind irrelevant, ob der Speicher lokal ist, SAN, NAS oder iSCSI.

#### <a name="calculation-summary-example"></a>Beispiel einer Berechnung

Bestimmen die Menge an e/a-System unter normalen betriebsbedingungen einwandfrei funktioniert:

- Logischer Datenträger ( *\<NTDS-Datenbank-Laufwerk\>* ) \Transfers/sec während der spitzenauslastungszeit 15-Minuten-Zeitraum 
- So bestimmen Sie die Menge an e/a-für den Speicher, in dem die Kapazität des zugrunde liegenden Speichers überschritten wird:
  >*IOPS benötigt* = (logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Avg Sek./Lesevorgänge &divide; *\<durchschn. Sek./Lesevorgänge als Ziel\>* ) &times; Logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Read/sec

|Leistungsindikator|Wert|
|-|-|
|Tatsächliche logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Avg Sek./Übertragung|0,02 Sekunden (20 Millisekunden)|
|Ziel-logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Avg Sek./Übertragung|.01 Sekunden|
|Multiplikator für die Änderung der verfügbaren e/a|0.02 &divide; 0.01 = 2|  
  
|Wertname|Wert|
|-|-|
|Logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Transfers/sec|400|
|Multiplikator für die Änderung der verfügbaren e/a|2|
|Die Gesamtzahl der IOPS erforderlich sind, während der spitzenauslastungszeit|800|

Um die Rate zu bestimmen, an der der Cache gewünscht wird, um vorbereitet werden:

- Bestimmen Sie die maximal zulässige Zeitraum, den Cache zu befassen. Es ist entweder die verstrichene Zeitspanne, die um die gesamte Datenbank vom Datenträger zu ladenden beanspruchen darf, oder für Szenarien, in denen nicht die gesamte Datenbank im Arbeitsspeicher geladen werden kann, wäre dies die maximale Zeit, RAM zu füllen.
- Ermitteln der Größe der Datenbank, mit Ausnahme von Leerzeichen.  Weitere Informationen finden Sie unter [auswerten, die für die Speicherung von](#evaluating-for-storage).  
- Unterteilen Sie die Größe der Datenbank von 8 KB; werden das gesamte IOs erforderlich, um die Datenbank zu laden.
- Teilen Sie das gesamte IOs durch die Anzahl der Sekunden in die definierten Zeitraums.

Beachten Sie, dass die Rate berechnet, während Sie genau, da zuvor geladene Seiten entfernt werden, wenn ESE nicht konfiguriert ist, dass eine feste Größe und AD DS standardmäßig verwendet die Variablen Cachegröße nicht genau sein.

|Sammeln von Datenpunkten|Werte
|-|-|
|Maximal zulässige Zeitraum befassen|10 Minuten (600 Sekunden)
|Datenbankgröße|2 GB|  
  
|Berechnungsschritt|Formula|Ergebnis|
|-|-|-|
|Berechnen der Größe der Datenbank in Datenseiten|(2 GB &times; 1024 &times; 1024) = *Größe der Datenbank in KB*|2\.097.152 KB|
|Berechnen der Anzahl der Seiten in der Datenbank|2\.097.152 KB &divide; 8 KB = *Anzahl von Seiten*|262.144 Seiten|
|Berechnen von IOPS vollständig den Cache befassen erforderlich|262.144 Seiten &divide; = 600 Sekunden *IOPS erforderlich sind*|437 IOPS|

## <a name="processing"></a>Verarbeitung

### <a name="evaluating-active-directory-processor-usage"></a>Auswerten von Active Directory-prozessorauslastung

Für die meisten Umgebungen nachdem Speicher, Arbeitsspeicher und Netzwerk ordnungsgemäß optimiert werden, wie beschrieben im Abschnitt Planen von wird die Menge an CPU-Kapazität verwalten Komponente sein, die die meiste Aufmerksamkeit verdient. Es gibt zwei Herausforderungen bei der Auswertung der CPU-Kapazität, die erforderlich sind:

- Unabhängig davon, ob die Anwendungen in der Umgebung werden und funktionieren in einer freigegebenen Infrastruktur und wird im Abschnitt "Nachverfolgen von teuren und ineffizienten suchen" in diesem Artikel erläutert erstellen effizienter Microsoft aktiveren AD-aktivierte Anwendungen oder die Migrierung Weg abwärtskompatible SAM Aufrufe von LDAP-Aufrufe.  
  
  In größeren Umgebungen ist der Grund, die, den dies wichtig ist, dass fehlerhaft codierte Anwendungen können Laufwerk Volatilität in CPU-Auslastung, "stehlen" übermäßig viel CPU-Zeit von anderen Anwendungen, künstlich Laufwerk um kapazitätsanforderungen ungleichmäßig verteilt Load für die DCs.  
- Wie AD DS mit einer großen Vielzahl von potenziellen Clients einer verteilten Umgebung ist, ist die Schätzung der Kosten eines "einzelnen Clients" ökologischen subjektive aufgrund von Verwendungsmustern und den Typ oder die Menge der Anwendungen, die Nutzung von AD DS. Kurz gesagt, wird ähnlich wie den Netzwerkabschnitt für Breite Anwendbarkeit, dies besser aus der Perspektive der Auswertung der gesamten Kapazität, die erforderlich sind, in der Umgebung aufgeteilt.

Für vorhandene Umgebungen wie zuvor, Speichergröße erläutert wird ausgegangen, dass Storage ist jetzt ordnungsgemäß dimensioniert, und daher die Daten in Bezug auf die prozessorauslastung gültig ist. Wie bereits ausgeführt wird, ist es unerlässlich, um sicherzustellen, dass der Engpass im System nicht über die Leistung des Speichers ist. Wenn ein Engpass vorhanden ist, und der Prozessor wartet, stehen im Leerlauf Zustände, die verschwinden werden, sobald der Engpass entfernt wird.  Prozessor Wartezustand entfernt werden, per Definition auch CPU-Auslastung aufweist nicht mehr auf die Daten zu warten. Daher Erfassen von Leistungsindikatoren "logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Avg Sek./Lesevorgänge" und "Process(lsass)\\Prozessorzeit (%)". Die Daten in "Process(lsass)\\Prozessorzeit (%)" künstlich gering Wenn "logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Avg Sek./Lesevorgänge" überschreitet 10 bis 15 ms, die einen allgemeinen Schwellenwert ist, Microsoft-Support verwendet Storage-bezogene Probleme zu behandeln. Wie zuvor, empfiehlt es sich, dass Abtastintervalls 15, 30 oder 60 Minuten sein. Alles wird im Allgemeinen zu flüchtigen für aussagekräftige Messergebnisse liegen; etwas größer wird täglich sieht übermäßig glätten.

### <a name="introduction"></a>Einführung

Um planen die kapazitätsplanung für Domänencontroller, erfordert verarbeitungsleistung, die meiste Aufmerksamkeit und Verständnis. Systeme, um maximale Leistung sicher richtig zu dimensionieren, gibt es immer eine Komponente, die der Engpass ist und in der richtigen Größe Domänencontroller werden dies den Prozessor.

Ähnlich wie Abschnitt über das Netzwerk, in dem die Anforderung der Umgebung auf Basis von Standorten überprüft wird, muss dasselbe für die Rechenkapazität gefordert, ausgeführt werden. Im Gegensatz zu den Netzwerkabschnitt, in dem die verfügbaren netzwerktechnologien den normalen Bedarf weit überschreiten, bezahlen Sie mehr Aufmerksamkeit auf die Größe der CPU-Kapazität.  Wie jede Umgebung selbst für moderate Größe Alles über ein paar tausend gleichzeitigen Benutzern kann deutliche Auslastung auf der CPU platziert.

Leider liegt die große Variabilität von Clientanwendungen, die AD nutzen, die allgemeine Schätzung von Benutzern pro CPU Schlüsselgröße für alle Umgebungen nicht anwendbar. Benutzerprofil und insbesondere die Compute-Anforderungen gelten. Aus diesem Grund muss jede Umgebung individuell angepasst werden.

#### <a name="target-site-behavior-profile"></a>Zielprofil für Site-Verhalten

Wie bereits erwähnt, bei der Planung der Kapazität für eine gesamte Site, Ziel ist es, ein Design mit als Ziel einer *N* + 1-Kapazität Design, z. B., die für die Fortsetzung des Diensts auf eine angemessene Ausfall eines Systems während der spitzenauslastungszeit ermöglichen Ebene der Qualität. Dies bedeutet, dass in einer "*N*" Szenario in Last ist in alle Felder muss weniger als 100 % (noch besser, weniger als 80 %) während der Spitzenzeiten.

Darüber, wenn die Anwendungen und Clients am Standort bewährte Methoden zum Suchen von Domänencontrollern (d. h. die [DsGetDcName-Funktion](http://msdn.microsoft.com/en-us/library/windows/desktop/ms675983(v=vs.85).aspx)), die Clients sollten geringfügigen relativ gleichmäßig verteilt werden vorübergehende Spitzen aufgrund von eine beliebige Anzahl von Faktoren ab.

Im nächsten Beispiel werden die folgenden Annahmen vorgenommen:

- Jede der fünf Domänencontroller am Standort verfügt über vier CPUs.
- Gesamt-Ziel-CPU-Auslastung während der Geschäftszeiten ist 40 % unter normalen betriebsbedingungen ("*N* + 1") und 60 % andernfalls ("*N*"). Während der Geschäftszeiten, ist die Ziel-CPU-Nutzung 80 %, da Sicherungssoftware und andere Wartungsaufgaben erwartet werden, um alle verfügbaren Ressourcen zu nutzen.

![Diagramm zur CPU-Nutzung](media/capacity-planning-considerations-cpu-chart.png)

Analysieren der Daten im Diagramm (Prozessor Information(_Total)\% Prozessor-Hilfsprogramm) für die einzelnen Domänencontroller:

- Zum größten Teil, wird die Auslastung relativ gleichmäßig verteilt handelt es sich wie erwartet werden würde, wenn Clients Domänencontrollerlocator verwenden und auch Suchvorgänge geschrieben haben. 
- Es gibt eine Anzahl von fünf Minuten Spitzen von 10 %, mit einigen möglichst große als 20 %. Ist im Allgemeinen, es sei denn, sie bewirken, das Ziel des Capacity-Plan dass überschritten wird, untersuchen diese nicht lohnt.  
- Der spitzenauslastungszeit für alle Systeme liegt zwischen ca. 8:00 Uhr und 9:15 Uhr. Bei der reibungslosen Übergang von ca. 5:00 Uhr bis ca. 17:00 Uhr ist das in der Regel auf den Geschäftszyklus hin. Mehr zufälligen Spitzen, die der CPU-Auslastung auf einem Feld-nach-Feld-Szenario 4:00 Uhr bis 17:00 Uhr wäre außerhalb der Aspekte der kapazitätsplanung.

  >[!NOTE]
  >Auf einem ordnungsgemäß verwalteten System kann besagten Spitzen Sicherungssoftware ausgeführt wird, vollständige systemüberprüfung auf Viren überprüft, Hardware- oder Softwareinventur, Softwareupdates oder Patch-Bereitstellung und usw. sein. Da sie außerhalb von Spitzenzeiten Geschäftszyklus Benutzer fallen, werden die Ziele nicht überschritten wurde.

- Jedes System etwa 40 % und alle Systeme müssen die gleiche Anzahl von CPUs, sollte ein Fehler oder offline geschaltet werden, die verbleibenden Systeme werden ausgeführt, auf eine geschätzte 53 % (System D 40 % Auslastung ist gleichmäßig aufgeteilt und System A und System C des vorhandenen 40 % Last hinzugefügt). Eine Reihe von Gründen, ist diese linearen Annahme nicht vollkommen exakt, aber bietet ausreichender Genauigkeit zu messen.  

  **Alternatives Szenario –** zwei Domänencontroller, die von 40 % ausführen: Eine Domäne-Controller ein Fehler auftritt, Geschätzte CPU auf dem verbleibenden wäre eine geschätzte 80 %. Dies wesentlich für Kapazitätsplan oben beschriebenen überschritten und wird auch stark Begrenzung des Umfangs der Head-Raum für die 10 bis 20 % finden Sie in das Lastprofil, oben, was bedeutet, dass die Spitzen den DC auf 90 % und 100 %, während Laufwerk würde die "*N*"Szenario und Reaktionsfähigkeit auf jeden Fall zu beeinträchtigen.

### <a name="calculating-cpu-demands"></a>Berechnen von CPU-Anforderungen

Die "Prozess\\Prozessorzeit (%)" Leistungsindikator-Objekts addiert die Gesamtmenge der Zeit, dass alle Threads einer Anwendung auf der CPU verbringen und dividiert durch die Gesamtmenge des Systems, die Zeit übergeben wurde. Der Effekt ist, dass eine Anwendung mit mehreren Threads auf einem System mit mehreren CPUS 100 % CPU-Zeit überschreiten kann und sehr unterschiedlich würde, als interpretiert werden "Prozessorinformationen\\% Prozessor Dienstprogramm". In der Praxis die "Process(lsass)\\Prozessorzeit (%)" angezeigt werden können, als die Anzahl der CPUs, die mit 100 %, die für die Unterstützung des Prozesses Anforderungen erforderlich sind. Ein Wert von 200 % bedeutet, dass es sich bei 2 CPUs, jede mit 100 %, erforderlich sind, um die vollständige AD DS-Auslastung zu unterstützen. Obwohl eine CPU-auf 100 % Kapazität ausgeführt Auslastung am meisten kosteneffiziente aus der Perspektive des Geld für den CPUs und Strom- und Energieverbrauch Verbrauch für eine Reihe von Gründen, finden Sie im Anhang A, bessere Reaktionsfähigkeit auf einem System mit mehreren Threads tritt auf, wenn das system bei 100 % nicht ausgeführt.

Um vorübergehende Spitzen bei der Clientauslastung zu unterstützen, wird empfohlen, eine maximale Zeitraum CPU zwischen 40 und 60 % der Kapazität des Systems als Ziel. Arbeiten mit dem obigen Beispiel würde bedeuten, dass zwischen 3.33 (60 % Ziel) und 5 (40 % Ziel) CPUs für AD DS-Auslastung (Lsass-Prozess) benötigt werden. Zusätzlicher Kapazität sollte entsprechend den Anforderungen des zugrunde liegenden Betriebssystems und anderen Agents, die erforderlich sind (z. B. Antivirus, Sicherung, Überwachung usw.) hinzugefügt werden. Obwohl die Auswirkungen von Agents auf einer Basis pro Umgebung ausgewertet werden muss, kann eine Schätzung der zwischen 5 und 10 % einer CPU gemacht werden. Im aktuellen Beispiel würden dies wird empfohlen, zwischen 3.43 (60 % Ziel) und 5.1 (40 % Ziel) CPUs Zeiten erforderlich sind.

Die einfachste Möglichkeit hierzu ist, verwenden Sie die Ansicht "Gestapelte Fläche" in Windows-Zuverlässigkeits- und -Systemmonitor (Perfmon), um sicherzustellen, dass alle Indikatoren sind die gleichen skaliert.

Annahmen:

- Ziel ist es, die auf Servern mit so wenigen wie möglich zu verkleinern. Im Idealfall würde einen Server ausführen, die Last und einen zusätzlichen Server, die für von Redundanz hinzugefügt (*N* + 1-Szenario).

![Prozessorzeitdiagramm für Lsass-Prozess (über alle Prozessoren)](media/capacity-planning-considerations-proc-time-chart.png)

Erworbene wissen von den Daten im Diagramm (Process(lsass)\\Prozessorzeit (%)):

- Des Geschäftstags startet Planungsansicht ca. 7:00 und um 17:00 Uhr verringert.
- Der höchsten Auslastung spitzenauslastungszeit liegt zwischen 9:30 Uhr und 11:00 Uhr. 
  > [!NOTE]
  > Alle Leistungsdaten ist historisch. Der maximale Datenpunkt um 9:15 gibt an, die Last zwischen 9:00 Uhr, 9:15.
- Es gibt Spitzen vor 7:00 Uhr was entweder Auslastung aus verschiedenen Zeitzonen oder Infrastruktur Hintergrundaktivitäten, z. B. Sicherungen hinweisen könnte. Da der Spitzenwert um 9:30 Uhr dieser Aktivität überschreitet, ist es nicht relevant.
- Es gibt drei Domänencontroller am Standort.

Auf die maximale Auslastung verbraucht Lsass etwa 485 % einer CPU oder 4,85 CPUs, die bei 100 % ausgeführt. Gemäß der mathematischen also zuvor dies die Website etwa 12,25 CPUs für AD DS benötigt. Fügen Sie in den oben genannten Vorschlägen von 5 bis 10 % für Hintergrundprozesse hinzu, und dies bedeutet, dass ersetzen den Server noch heute ungefähr 12.30 zu 12,35 CPUs unterstützen dieselbe Last müssten. Eine Umgebung Schätzung für Wachstum jetzt muss berücksichtigt werden.

### <a name="when-to-tune-ldap-weights"></a>Wenn LDAP-Gewichtungen zu optimieren

Es gibt mehrere Szenarios, bei der Optimierung [LdapSrvWeight](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc957291(v=technet.10)) angesehen werden. Innerhalb des Kontexts der kapazitätsplanung beschäftigen würde dies erfolgen, wenn das Laden der Anwendung oder Benutzer sind nicht gleichmäßig verteilt, oder die zugrunde liegenden Systeme in Bezug auf die Funktion nicht gleichmäßig verteilt sind. Gründe dafür über die kapazitätsplanung sind außerhalb des Bereichs der in diesem Artikel.

Es gibt zwei häufige Gründe für die LDAP-Gewichtungen zu optimieren:

- Der PDC-Emulator ist ein Beispiel, das jede Umgebung wirkt sich auf, für welche Benutzer oder eine Anwendung Ladeverhalten nicht gleichmäßig verteilt sind. Als bestimmte Tools und Aktionen den PDC-Emulator, wie die Gruppenrichtlinien-Verwaltungstools, die zweite Versuche im Fall von Authentifizierungsfehlern, Vertrauensstellung ausfallen, usw., Ziel können CPU-Ressourcen auf dem PDC-Emulator stärker als an anderer Stelle im angeforderten sein. die Site.
  - Es ist nur nützlich, um dies zu optimieren, wenn Sie vorhanden ist, dass eine gleichmäßigere Verteilung der Last ein erheblichen Unterschied in der CPU-Auslastung, um die Last auf dem PDC-Emulator zu reduzieren und erhöhen Sie die arbeitsauslastung auf anderen Domänencontrollern ermöglicht.
  - Legen Sie in diesem Fall LDAPSrvWeight zwischen 50 und 75, für den PDC-Emulator.
- Server mit unterschiedlicher Anzahl von CPUs (und Geschwindigkeit) an einem Standort.  Angenommen Sie, dass zwei 8-Core-Server und einem 4-Core-Server.  Der letzte Server hat die Hälfte die Prozessoren, die von den anderen beiden Servern.  Dies bedeutet, dass ein gut verteilte Clientauslastung durchschnittliche CPU-Auslastung auf der vier Kernen mit ungefähr zweimal die Kontrollkästchen für die acht Kernen erhöht.
  - Beispielsweise würde die beiden Kartons mit acht Kernen ausgeführt werden, von 40 % und 80 % würde das Feld für die vier Kernen ausgeführt werden.
  - Berücksichtigen Sie auch die Auswirkungen des Verlusts von einem 8-Core-Feld in diesem Szenario speziell die Tatsache, dass das Kontrollkästchen für die vier Kernen nun überladen werden würde.

#### <a name="example-1---pdc"></a>Beispiel 1: PDC

| |Nutzung mit den Standardeinstellungen|New LdapSrvWeight|Geschätzte neue Auslastung|
|-|-|-|-|
|DC-1 (PDC-Emulator)|53%|57|40 %|
|DC 2|33%|100|40 %|
|DC 3|33%|100|40 %|

Der Haken ist, wenn die PDC-Emulatorrolle, insbesondere auf einen anderen Domänencontroller in der Website übernommen oder übertragen wird, eine drastische Erhöhung auf die neue PDC-Emulator werden.

Verwenden Sie das Beispiel aus dem Abschnitt [Site Verhalten Zielprofil](#target-site-behavior-profile), erfolgte eine Annahme, dass alle drei Domänencontroller am Standort vier CPUs veraltet. Was soll, unter normalen Bedingungen passieren, wenn einer der Domänencontroller haben, dass acht CPUs? Es wäre zwei Domänencontroller mit 40 % Auslastung und unter Nutzung von 20 %. Dies ist, zwar keine fehlerhaften besteht die Möglichkeit, die etwas besser zum Lastenausgleich. Nutzen Sie die LDAP-Gewichtungen, um dies zu erreichen.  Ein Beispielszenario wäre:

#### <a name="example-2---differing-cpu-counts"></a>Beispiel 2: zählt, unterschiedliche CPU

| |Prozessorinformationen\\ %&nbsp;Prozessor Utility(_Total)<br />Nutzung mit den Standardeinstellungen|New LdapSrvWeight|Geschätzte neue Auslastung|
|-|-|-|-|
|4-CPU DC 1|40|100|30 %|
|4-CPU DC 2|40|100|30 %|
|8-CPU DC 3|20|200|30 %|

Werden Sie jedoch sehr vorsichtig mit diesen Szenarien. Wie oben gezeigt werden kann, sucht die mathematischen Grundlagen von wirklich gut und schön auf Papier. Aber in diesem Artikel, die Planung für eine "*N* + 1" Szenario ist von größter Wichtigkeit. Die Auswirkungen von einem Domänencontroller offline geschaltet, muss für jedes Szenario berechnet werden. In dem unmittelbar vorhergehenden Szenario, in denen die lastverteilung gerade ist, um sicherzustellen, dass einen 60 % beim Laden einer "*N*" Szenario, bei der Auslastung gleichmäßig auf alle Server verteilt die Verteilung verwendet werden können wie das Verhältnis bleiben konsistent. Sucht den PDC-Emulator optimierungsszenario und jedes Szenario, in denen Benutzer- oder Anwendungsfehler Load unausgeglichene, unterscheidet sich die Auswirkungen:

| |Optimierte Nutzung|New LdapSrvWeight|Geschätzte neue Auslastung|
|-|-|-|-|
|DC-1 (PDC-Emulator)|40 %|85|47%|
|DC 2|40 %|100|53%|
|DC 3|40 %|100|53%|

### <a name="virtualization-considerations-for-processing"></a>Überlegungen zur Virtualisierung für die Verarbeitung

Es gibt zwei Ebenen der kapazitätsplanung beschäftigen, die in einer virtualisierten Umgebung ausgeführt werden müssen. Auf der Hostebene, ähnlich wie die Identifikation des Geschäftszyklus für den Domänencontroller, die Verarbeitung von zuvor beschriebenen müssen Schwellenwerte, die während der spitzenauslastungszeit identifiziert werden. Da die zugrunde liegenden Prinzipien für einen Hostcomputer Planen von Gast-Threads auf der CPU für das Abrufen von AD DS-Threads auf der CPU auf einem physischen Computer identisch sind, werden das gleiche Ziel von 40 bis 60 % auf dem zugrunde liegenden Host empfohlen. Auf der nächsten Ebene die Gast-Ebene, seit die Prinzipale der Threadplanung wurden nicht geändert, das Ziel in der Gast bleibt im Bereich 40, 60 %.

In einem direkten zugeordneten Szenario mit nur einem Gast pro Host, alle die kapazitätsplanung abgeschlossen bis zum angegebenen Zeitpunkt den Anforderungen (Arbeitsspeicher, Datenträger, Netzwerk) an die zugrunde liegende Hostbetriebssystem hinzugefügt werden muss. In einem Szenario mit freigegebener Hosts gibt testing an, dass 10 % Auswirkungen auf die Effizienz der zugrunde liegenden Prozessoren vorhanden ist. Das heißt, wenn ein Standort 10 CPUs an ein Ziel von 40 %, die empfohlene Menge an virtuellen CPUs in allen zuordnen benötigt die "*N*" Gäste wäre 11. An einem Standort mit einer gemischten Verteilung von physischen Servern und virtuellen Servern gilt der Modifizierer nur für die virtuellen Computer. Wenn ein Standort hat z. B. ein "*N* + 1" Szenario wäre ein physischer oder direkt zugeordneten-Server mit 10 CPUs zu entspricht ein Gast mit 11 CPUs auf einem Host mit 11 CPUs, die für den Domänencontroller reserviert.

Während der Analyse und die Berechnung der erforderlichen CPU-Mengen werden zur Unterstützung von AD DS-Auslastung, die Anzahl der CPUs, die zugeordnet, was in Bedingungen physische Hardware erworben werden, können nicht unbedingt ordnungsgemäß zugeordnet. Virtualisierung entfällt das Aufrunden. Virtualisierung verringert den Aufwand für die computekapazität einer Website hinzufügen, erhält die Leichtigkeit, mit der eine CPU mit einem virtuellen Computer hinzugefügt werden kann. Es beseitigt nicht die Notwendigkeit, bewerten genau die rechenleistung erforderlich, damit die zugrunde liegende Hardware verfügbar ist, wenn zusätzliche Prozessoren für die Gäste hinzugefügt werden müssen.  Wie immer: Denken Sie daran, zum Planen und Überwachung von bedarfsanstieg werden sollen.

### <a name="calculation-summary-example"></a>Beispiel einer Berechnung

|System|Spitzenwert CPU|
|-|-|-|
|DC 1|120%|
|DC 2|147%|
|Dc 3|218%|
|Gesamt-CPU verwendet wird|485%|  
  
|/ Den Stammverwaltungsserver-System(en) Zielanzahl|Gesamtbandbreite (von oben)|
|-|-|
|CPUs, die erforderlich sind, am Ziel von 40 %|4.85 &divide; .4 = 12.25|

Aufgrund der Wichtigkeit von diesem Punkt wiederholen *Denken Sie daran, für Wachstum planen*. 50 % Wachstum in den nächsten drei Jahren, sofern dieser Umgebung benötigen 18.375 CPUs (12,25 &times; 1.5) auf die drei-Jahres-Marke. Ein alternativer Plan wäre, überprüfen im ersten Jahr und nach Bedarf zusätzliche Kapazität hinzufügen.

### <a name="cross-trust-client-authentication-load-for-ntlm"></a>Cross-Trust-Clientauslastung-Authentifizierung für NTLM

#### <a name="evaluating-cross-trust-client-authentication-load"></a>Auswerten von Cross-Trust-Client-Authentifizierung laden

Viele Umgebungen möglicherweise eine oder mehrere Domänen, die durch eine Vertrauensstellung verbunden sind. Eine Vertrauensstellung mithilfe des Domänencontrollers, sicheren Kanal an einen anderen Domänencontroller in der Zieldomäne oder die nächste Domäne im Pfad durchlaufen eine Authentifizierungsanforderung für eine Identität in einer anderen Domäne, die keine Kerberos-Authentifizierung verwendet werden soll die Zieldomäne. Die Anzahl gleichzeitiger Aufrufe, die über den sicheren Kanal an, die ein Domänencontroller zu einem Domänencontroller in einer vertrauenswürdigen Domäne vornehmen können wird gesteuert durch eine Einstellung, die als bekannt **"MaxConcurrentApi"** . Für Domänencontroller, um sicherzustellen, dass der sichere Kanal das Maß der Auslastung verarbeiten kann erfolgt durch einen von zwei Ansätzen: Optimierung **"MaxConcurrentApi"** oder in einer Gesamtstruktur mit vertrauensstellungsabkürzungen zu erstellen. Um die Menge an Datenverkehr über eine einzelne Vertrauensstellung zu messen, finden Sie unter [Vorgehensweise zur leistungsoptimierung für die NTLM-Authentifizierung mit der Einstellung "MaxConcurrentApi"](https://support.microsoft.com/kb/2688798).

Während der Datensammlung muss, während der Spitzenzeiten ausgelastet des Tages die Daten können nützlich sein, wie bei allen anderen Szenarien erfasst werden.

> [!NOTE]
> Innerhalb einer Gesamtstruktur und zwischen Gesamtstrukturen Szenarien können dazu führen, dass die Authentifizierung bei mehreren Vertrauensstellungen durchlaufen, und jede Phase optimiert werden müssen.

#### <a name="planning"></a>Planen

Es gibt eine Anzahl von Anwendungen, die NTLM-Authentifizierung verwenden, standardmäßig, oder verwenden es in einem Konfigurationsszenario mit bestimmten. Application Server nimmt in der Kapazität und service eine zunehmende Anzahl von aktiven Clients. Es gibt auch ein Trend, dass Clients Sitzungen für einen begrenzten Zeitraum geöffnet lassen und stattdessen erneut eine Verbindung, in regelmäßigen Abständen (z. B. e-Mail-Pull-Synchronisierung herzustellen). Ein weiteres häufiges Beispiel für die NTLM-Überlastung ist Webproxyserver, für die Authentifizierung für den Internetzugriff erforderlich.

Diese Anwendungen kann eine spürbare Last für die NTLM-Authentifizierung die kann erhebliche Belastung auf den DCs, besonders wenn Benutzer und Ressourcen in verschiedenen Domänen befinden.

Es gibt mehrere Ansätze zur Verwaltung von Cross-Trust-Last, die in der Praxis in Verbindung und nicht in einen exklusiven entweder verwendet werden / oder -Szenario. Folgende Optionen sind möglich:

- Reduzieren Sie Cross-Trust-Clientauthentifizierung, suchen Sie die Dienste, die ein Benutzer in der gleichen Domäne verwendet wird, denen der Benutzer im.
- Erhöhen Sie die Anzahl der secure-Kanäle verfügbar sind. Dies ist innerhalb einer Gesamtstruktur und gesamtstrukturübergreifende Datenverkehr relevant und werden als vertrauensstellungsabkürzungen bezeichnet.
- Optimieren Sie die Standardeinstellungen für **"MaxConcurrentApi"** .

Für die Optimierung **"MaxConcurrentApi"** auf einem vorhandenen Server, die Gleichung ist:

> *New_MaxConcurrentApi_setting* &ge; (*Semaphore_acquires* + *Semaphore_time-Timeouts*) &times; *Average_semaphore_ Hold_time* &divide; *Time_collection_length*

Weitere Informationen finden Sie unter [2688798 im KB-Artikel: Wie Sie zur leistungsoptimierung für die NTLM-Authentifizierung mit der Einstellung "MaxConcurrentApi"](http://support.microsoft.com/kb/2688798).

## <a name="virtualization-considerations"></a>Virtualisierung: Überlegungen

Keine, ist dies ein Betriebssystem, die Einstellung zu optimieren.

### <a name="calculation-summary-example"></a>Beispiel einer Berechnung

|Datentyp|Wert|
|-|-|
|Semaphor erhält (mindestens)|6,161|
|Semaphor erhält (maximal)|6,762|
|Semaphore-Timeouts|0|
|Durchschnittliche Semaphor Haltezeit|0.012|
|Sammlungsdauer (Sekunden)|1:11 Minuten (71 Sekunden)|
|Die Formel (in KB 2688798)|((6762 &ndash; 6161) + 0) &times; 0.012 /|
|Minimalwert für **"MaxConcurrentApi"**|((6762 &ndash; 6161) + 0) &times; 0.012 &divide; 71 = .101|

Für dieses System für diesen Zeitraum sind die Standardwerte zulässig.

## <a name="monitoring-for-compliance-with-capacity-planning-goals"></a>Überwachung für die Kompatibilität bei der kapazitätsplanung für Ziele

In diesem Artikel wurde beschrieben wurde, dass die Auslastung Ziele Zielpunkt planen und zu skalieren. Hier ist ein zusammenfassendes Diagramm der empfohlenen Schwellenwerte, die überwacht werden müssen, um sicherzustellen, dass die Systeme innerhalb von Schwellenwerten für eine angemessene Kapazität betrieben werden. Bedenken Sie, dass diese keine Schwellenwerte von ressourcenleistungen, sondern Schwellenwerte für die kapazitätsplanung. Ein Server, der über diese Schwellenwerte funktioniert, aber es ist Zeit, zu überprüfen, dass alle Anwendungen auch Verhalten sind. Wenn es sich bei, dass Anwendungen ordnungsgemäß verhaltenden sind allerdings ist es Zeit, die mit der Evaluierung von Hardware oder andere konfigurationsänderungen.

|Kategorie|Leistungsindikator|Intervall/Sampling|Ziel|Warnung|
|-|-|-|-|-|
|Prozessor|Processor Information(_Total)\\% Processor Utility|60 min|40%|60%|
|RAM (Windows Server 2008 R2 or earlier)|Memory\Available MB|< 100 MB|N/A|< 100 MB|
|RAM (Windows Server 2012)|Memory\Long-Term Average Standby Cache Lifetime(s)|30 min|Must be tested|Must be tested|
|Network|Network Interface(\*)\Bytes Sent/sec<br /><br />Network Interface(\*)\Bytes Received/sec|30 min|40%|60%|
|Storage|LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read<br /><br />LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Write|60 min|10 ms|15 ms|
|AD Services|Netlogon(\*)\Average Semaphore Hold Time|60 min|0|1 second|

## Appendix A: CPU sizing criteria

### Definitions

**Processor (microprocessor) –** a component that reads and executes program instructions  

**CPU –** Central Processing Unit  

**Multi-Core processor –** multiple CPUs on the same integrated circuit  

**Multi-CPU –** multiple CPUs, not on the same integrated circuit  

**Logical Processor –** one logical computing engine from the perspective of the operating system  

This includes hyper-threaded, one core on multi-core processor, or a single core processor.  

As today’s server systems have multiple processors, multiple multi-core processors, and hyper-threading, this information is generalized to cover both scenarios. As such, the term logical processor will be used as it represents the operating system and application perspective of the available computing engines.

### Thread-level parallelism

Each thread is an independent task, as each thread has its own stack and instructions. Because AD DS is multi-threaded and the number of available threads can be tuned by using [How to view and set LDAP policy in Active Directory by using Ntdsutil.exe](http://support.microsoft.com/kb/315071), it scales well across multiple logical processors.

### Data-level parallelism

This involves sharing data across multiple threads within one process (in the case of the AD DS process alone) and across multiple threads in multiple processes (in general). With concern to over-simplifying the case, this means that any changes to data are reflected to all running threads in all the various levels of cache (L1, L2, L3) across all cores running said threads as well as updating shared memory. Performance can degrade during write operations while all the various memory locations are brought consistent before instruction processing can continue.

### CPU speed vs. multiple-core considerations

The general rule of thumb is faster logical processors reduce the duration it takes to process a series of instructions, while more logical processors means that more tasks can be run at the same time. These rules of thumb break down as the scenarios become inherently more complex with considerations of fetching data from shared-memory, waiting on data-level parallelism, and the overhead of managing multiple threads. This is also why scalability in multi-core systems is not linear.

Consider the following analogies in these considerations: think of a highway, with each thread being an individual car, each lane being a core, and the speed limit being the clock speed.

1. If there is only one car on the highway, it doesn’t matter if there are two lanes or 12 lanes. That car is only going to go as fast as the speed limit will allow.
1. Assume that the data the thread needs is not immediately available. The analogy would be that a segment of road is shutdown. If there is only one car on the highway, it doesn’t matter what the speed limit is until the lane is reopened (data is fetched from memory).
1. As the number of cars increase, the overhead to manage the number of cars increases. Compare the experience of driving and the amount of attention necessary when the road is practically empty (such as late evening) versus when the traffic is heavy (such as mid-afternoon, but not rush hour). Also, consider the amount of attention necessary when driving on a two-lane highway, where there is only one other lane to worry about what the drivers are doing, versus a six-lane highway where one has to worry about what a lot of other drivers are doing.
   > [!NOTE]
   > The analogy about the rush hour scenario is extended in the next section: Response Time/How the System Busyness Impacts Performance.

As a result, specifics about more or faster processors become highly subjective to application behavior, which in the case of AD DS is very environmentally specific and even varies from server to server within an environment. This is why the references earlier in the article do not invest heavily in being overly precise, and a margin of safety is included in the calculations. When making budget-driven purchasing decisions, it is recommended that optimizing usage of the processors at 40% (or the desired number for the environment) occurs first, before considering buying faster processors. The increased synchronization across more processors reduces the true benefit of more processors from the linear progression (2&times; the number of processors provides less than 2&times; available additional compute power).

> [!NOTE]
> Amdahl’s Law and Gustafson’s Law are the relevant concepts here.

### Response time/How the system busyness impacts performance

Queuing theory is the mathematical study of waiting lines (queues). In queuing theory, the Utilization Law is represented by the equation:

*U* k = *B* &divide; *T*

Where *U* k is the utilization percentage, *B* is the amount of time busy, and *T* is the total time the system was observed. Translated into the context of Windows, this means the number of 100-nanosecond (ns) interval threads that are in a Running state divided by how many 100-ns intervals were available in given time interval. This is exactly the formula for calculating % Processor Utility (reference [Processor Object](https://docs.microsoft.com/previous-versions/ms804036(v=msdn.10)) and [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/previous-versions/windows/embedded/ms901169(v=msdn.10))).

Queuing theory also provides the formula: *N* = *U* k &divide; (1 &ndash; *U* k) to estimate the number of waiting items based on utilization ( *N* is the length of the queue). Charting this over all utilization intervals provides the following estimates to how long the queue to get on the processor is at any given CPU load.

![Queue length](media/capacity-planning-considerations-queue-length.png)

It is observed that after 50% CPU load, on average there is always a wait of one other item in the queue, with a noticeably rapid increase after about 70% CPU utilization.

Returning to the driving analogy used earlier in this section:

- The busy times of “mid-afternoon” would, hypothetically, fall somewhere into the 40% to 70% range. There is enough traffic such that one’s ability to pick any lane is not majorly restricted, and the chance of another driver being in the way, while high, does not require the level of effort to “find” a safe gap between other cars on the road.
- One will notice that as traffic approaches rush hour, the road system approaches 100% capacity. Changing lanes can become very challenging because cars are so close together that increased caution must be exercised to do so.

This is why the long term averages for capacity conservatively estimated at 40% allows for head room for abnormal spikes in load, whether said spikes transitory (such as poorly coded queries that run for a few minutes) or abnormal bursts in general load (the morning of the first day after a long weekend).

The above statement regards % Processor Time calculation being the same as the Utilization Law is a bit of a simplification for the ease of the general reader. For those more mathematically rigorous:  
- Translating the [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10))
  - *B* = The number of 100-ns intervals “Idle” thread spends on the logical processor. The change in the “*X*” variable in the [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) calculation
  - *T* = the total number of 100-ns intervals in a given time range. The change in the “*Y*” variable in the [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) calculation.
  - *U* k = The utilization percentage of the logical processor by the “Idle Thread” or % Idle Time.  
- Working out the math:
  - *U* k = 1 – %Processor Time
  - %Processor Time = 1 – *U* k
  - %Processor Time = 1 – *B* / *T*
  - %Processor Time = 1 – *X1* – *X0* / *Y1* – *Y0*

### Applying the concepts to capacity planning

The preceding math may make determinations about the number of logical processors needed in a system seem overwhelmingly complex. This is why the approach to sizing the systems is focused on determining maximum target utilization based on current load and calculating the number of logical processors required to get there. Additionally, while logical processor speeds will have a significant impact on performance, cache efficiencies, memory coherence requirements, thread scheduling and synchronization, and imperfectly balanced client load will all have significant impacts on performance that will vary on a server-by-server basis. With the relatively cheap cost of compute power, attempting to analyze and determine the perfect number of CPUs needed becomes more an academic exercise than it does provide business value.

Forty percent is not a hard and fast requirement, it is a reasonable start. Various consumers of Active Directory require various levels of responsiveness. There may be scenarios where environments can run at 80% or 90% utilization as a sustained average, as the increased wait times for access to the processor will not noticeably impact client performance. It is important to re-iterate that there are many areas in the system that are much slower than the logical processor in the system, including access to RAM, access to disk, and transmitting the response over the network. All of these items need to be tuned in conjunction. Examples:

- Adding more processors to a system running 90% that is disk-bound is probably not going to significantly improve performance. Deeper analysis of the system will probably identify that there are a lot of threads that are not even getting on the processor because they are waiting on I/O to complete.
- Resolving the disk-bound issues potentially means that threads that were previously spending a lot of time in a waiting state will no longer be in a waiting state for I/O and there will be more competition for CPU time, meaning that the 90% utilization in the previous example will go to 100% (because it can not go higher). Both components need to be tuned in conjunction.
  > [!NOTE]
  > Processor Information(*)\\% Processor Utility can exceed 100% with systems that have a "Turbo" mode.  This is where the CPU exceeds the rated processor speed for short periods.  Reference CPU manufacturers documentation and description of the counter for greater insight.  

Discussing whole system utilization considerations also brings into the conversation domain controllers as virtualized guests. [Response time/How the system busyness impacts performance](#response-timehow-the-system-busyness-impacts-performance) applies to both the host and the guest in a virtualized scenario. This is why in a host with only one guest, a domain controller (and generally any system) has near the same performance it does on physical hardware. Adding additional guests to the hosts increases the utilization of the underlying host, thereby increasing the wait times to get access to the processors as explained previously. In short, logical processor utilization needs to be managed at both the host and at the guest levels.

Extending the previous analogies, leaving the highway as the physical hardware, the guest VM will be analogized with a bus (an express bus that goes straight to the destination the rider wants). Imagine the following four scenarios:

- It is off hours, a rider gets on a bus that is nearly empty, and the bus gets on a road that is also nearly empty. As there is no traffic to contend with, the rider has a nice easy ride and gets there just as fast as if the rider had driven instead. The rider’s travel times are still constrained by the speed limit.
- It is off hours so the bus is nearly empty but most of the lanes on the road are closed, so the highway is still congested. The rider is on an almost-empty bus on a congested road. While the rider does not have a lot of competition in the bus for where to sit, the total trip time is still dictated by the rest of the traffic outside.
- It is rush hour so the highway and the bus are congested. Not only does the trip take longer, but getting on and off the bus is a nightmare because people are shoulder to shoulder and the highway is not much better. Adding more busses (logical processors to the guest) does not mean they can fit on the road any more easily, or that the trip will be shortened.
- The final scenario, though it may be stretching the analogy a little, is where the bus is full, but the road is not congested. While the rider will still have trouble getting on and off the bus, the trip will be efficient after the bus is on the road. This is the only scenario where adding more busses (logical processors to the guest) will improve guest performance.

From there it is relatively easy to extrapolate that there are a number of scenarios in between the 0%-utilized and the 100%-utilized state of the road and the 0%- and 100%-utilized state of the bus that have varying degrees of impact.

Applying the principals above of 40% CPU as reasonable target for the host as well as the guest is a reasonable start for the same reasoning as above, the amount of queuing.

## Appendix B: Considerations regarding different processor speeds, and the effect of processor power management on processor speeds

Throughout the sections on processor selection the assumption is made that the processor is running at 100% of clock speed the entire time the data is being collected and that the replacement systems will have the same speed processors. Despite both assumptions in practice being false, particularly with Windows Server 2008 R2 and later, where the default power plan is **Balanced**, the methodology still stands as it is the conservative approach. While the potential error rate may increase, it only increases the margin of safety as processor speeds increase.

- For example, in a scenario where 11.25 CPUs are demanded, if the processors were running at half speed when the data was collected, the more accurate estimate might be 5.125 &divide; 2.
- It is impossible to guarantee that doubling the clock speeds would double the amount of processing that happens for a given time period. This is due to the fact the amount of time that the processors spend waiting on RAM or other system components could stay the same. The net effect is that the faster processors might spend a greater percentage of the time idle while waiting on data to be fetched. Again, it is recommended to stick with the lowest common denominator, being conservative, and avoid trying to calculate a potentially false level of accuracy by assuming a linear comparison between processor speeds.

Alternatively, if processor speeds in replacement hardware are lower than current hardware, it would be safe to increase the estimate of processors needed by a proportionate amount. For example, it is calculated that 10 processors are needed to sustain the load in a site, and the current processors are running at 3.3 Ghz and replacement processors will run at 2.6 Ghz, this is a 21% decrease in speed. In this case, 12 processors would be the recommended amount.

That said, this variability would not change the Capacity Management processor utilization targets. As processor clock speeds will be adjusted dynamically based on the load demanded, running the system under higher loads will generate a scenario where the CPU spends more time in a higher clock speed state, making the ultimate goal to be at 40% utilization in a 100% clock speed state at peak. Anything less than that will generate power savings as CPU speeds will be throttled back during off peak scenarios.

> [!NOTE]
> An option would be to turn off power management on the processors (setting the power plan to **High Performance**) while data is collected. That would give a more accurate representation of the CPU consumption on the target server.

To adjust estimates for different processors, it used to be safe, excluding other system bottlenecks outlined above, to assume that doubling processor speeds doubled the amount of processing that could be performed.  Today, the internal architecture of processors is different enough between processors, that a safer way to gauge the effects of using different processors than data was taken from is to leverage the SPECint_rate2006 benchmark from Standard Performance Evaluation Corporation.

1. Find the SPECint_rate2006 scores for the processor that are in use and that plan to be used.
    1. On the website of the Standard Performance Evaluation Corporation, select **Results**, highlight **CPU2006**, and select **Search all SPECint_rate2006 results**.
    1. Under **Simple Request**, enter the search criteria for the target processor, for example **Processor Matches E5-2630 (baselinetarget)** and **Processor Matches E5-2650 (baseline)**.
    1. Find the server and processor configuration to be used (or something close, if an exact match is not available) and note the value in the **Result** and **# Cores** columns.
1. To determine the modifier use the following equation:
   >((*Target platform per-core score value*) &times; (*MHz per-core of baseline platform*)) &divide; ((*Baseline per-core score value*) &times; (*MHz per-core of target platform*))  

    Using the above example:
   >(35.83 &times; 2000) &divide; (33.75 &times; 2300) = 0.92
1. Multiply the estimated number of processors by the modifier.  In the above case to go from the E5-2650 processor to the E5-2630 processor multiply the calculated 11.25 CPUs &times; 0.92 = 10.35 processors needed.

## Appendix C: Fundamentals regarding the operating system interacting with storage

The queuing theory concepts outlined in [Response time/How the system busyness impacts performance](#response-timehow-the-system-busyness-impacts-performance) are also applicable to storage. Having a familiarity of how the operating system handles I/O is necessary to apply these concepts. In the Microsoft Windows operating system, a queue to hold the I/O requests is created for each physical disk. However, a clarification on physical disk needs to be made. Array controllers and SANs present aggregations of spindles to the operating system as single physical disks. Additionally, array controllers and SANs can aggregate multiple disks into one array set and then split this array set into multiple “partitions”, which is in turn presented to the operating system as multiple physical disks (ref. figure).

![Block spindles](media/capacity-planning-considerations-block-spindles.png)  

In this figure the two spindles are mirrored and split into logical areas for data storage (Data 1 and Data 2). These logical areas are viewed by the operating system as separate physical disks.

Although this can be highly confusing, the following terminology is used throughout this appendix to identify the different entities:

- **Spindle –** the device that is physically installed in the server.
- **Array –** a collection of spindles aggregated by controller.
- **Array partition –** a partitioning of the aggregated array
- **LUN –** an array, used when referring to SANs
- **Disk –** What the operating system observes to be a single physical disk.
- **Partition –** a logical partitioning of what the operating system perceives as a physical disk.

### Operating system architecture considerations

The operating system creates a First In/First Out (FIFO) I/O queue for each disk that is observed; this disk may be representing a spindle, an array, or an array partition. From the operating system perspective, with regard to handling I/O, the more active queues the better. As a FIFO queue is serialized, meaning that all I/Os issued to the storage subsystem must be processed in the order the request arrived. By correlating each disk observed by the operating system with a spindle/array, the operating system now maintains an I/O queue for each unique set of disks, thereby eliminating contention for scarce I/O resources across disks and isolating I/O demand to a single disk. As an exception, Windows Server 2008 introduces the concept of I/O prioritization, and applications designed to use the “Low” priority fall out of this normal order and take a back seat. Applications not specifically coded to leverage the “Low” priority default to “Normal.”

### Introducing simple storage subsystems

Starting with a simple example (a single hard drive inside a computer) a component-by-component analysis will be given. Breaking this down into the major storage subsystem components, the system consists of:

- **1 –** 10,000 RPM Ultra Fast SCSI HD (Ultra Fast SCSI has a 20 MB/s transfer rate)
- **1 –** SCSI Bus (the cable)
- **1 –** Ultra Fast SCSI Adapter
- **1 –** 32-bit 33 MHz PCI bus

Once the components are identified, an idea of how much data can transit the system, or how much I/O can be handled, can be calculated. Note that the amount of I/O and quantity of data that can transit the system is correlated, but not the same. This correlation depends on whether the disk I/O is random or sequential and the block size. (All data is written to the disk as a block, but different applications using different block sizes.) On a component-by-component basis:

- **The hard drive –** The average 10,000-RPM hard drive has a 7-millisecond (ms) seek time and a 3 ms access time. Seek time is the average amount of time it takes the read/write head to move to a location on the platter. Access time is the average amount of time it takes to read or write the data to disk, once the head is in the correct location. Thus, the average time for reading a unique block of data in a 10,000-RPM HD constitutes a seek and an access, for a total of approximately 10 ms (or .010 seconds) per block of data.

  When every disk access requires movement of the head to a new location on the disk, the read/write behavior is referred to as “random.” Thus, when all I/O is random, a 10,000-RPM HD can handle approximately 100 I/O per second (IOPS) (the formula is 1000 ms per second divided by 10 ms per I/O or 1000/10=100 IOPS).

  Alternatively, when all I/O occurs from adjacent sectors on the HD, this is referred to as sequential I/O. Sequential I/O has no seek time because when the first I/O is complete, the read/write head is at the start of where the next block of data is stored on the HD. Thus a 10,000-RPM HD is capable of handling approximately 333 I/O per second (1000 ms per second divided by 3 ms per I/O).

  >[!NOTE]
  >This example does not reflect the disk cache, where the data of one cylinder is typically kept. In this case, the 10 ms are needed on the first I/O and the disk reads the whole cylinder. All other sequential I/O is satisfied from the cache. As a result, in-disk caches might improve sequential I/O performance.
  
  So far, the transfer rate of the hard drive has been irrelevant. Whether the hard drive is 20 MB/s Ultra Wide or an Ultra3 160 MB/s, the actual amount of IOPS the can be handled by the 10,000-RPM HD is ~100 random or ~300 sequential I/O. As block sizes change based on the application writing to the drive, the amount of data that is pulled per I/O is different. For example, if the block size is 8 KB, 100 I/O operations will read from or write to the hard drive a total of 800 KB. However, if the block size is 32 KB, 100 I/O will read/write 3,200 KB (3.2 MB) to the hard drive. As long as the SCSI transfer rate is in excess of the total amount of data transferred, getting a “faster” transfer rate drive will gain nothing. See the following tables for comparison.

  | |7200 RPM 9ms seek, 4ms access|10,000 RPM 7ms seek, 3ms access|15,000 RPM 4ms seek, 2ms access
  |-|-|-|-|
  |Random I/O|80|100|150|
  |Sequential I/O|250|300|500|  
  
  |10,000 RPM drive|8 KB block size (Active Directory Jet)|
  |-|-|
  |Random I/O|800 KB/s|
  |Sequential I/O|2400 KB/s|

- **SCSI backplane (bus) –** Understanding how the “SCSI backplane (bus)”, or in this scenario the ribbon cable, impacts throughput of the storage subsystem depends on knowledge of the block size. Essentially the question would be, how much I/O can the bus handle if the I/O is in 8 KB blocks? In this scenario, the SCSI bus is 20 MB/s, or 20480 KB/s. 20480 KB/s divided by 8 KB blocks yields a maximum of approximately 2500 IOPS supported by the SCSI bus.

  >[!NOTE]
  >The figures in the following table represent an example. Most attached storage devices currently use PCI Express, which provides much higher throughput.  
  
  |I/O supported by SCSI bus per block size|2 KB block size|8 KB block size (AD Jet) (SQL Server 7.0/SQL Server 2000)
  |-|-|-|
  |20 MB/s|10,000|2,500|
  |40 MB/s|20,000|5,000|
  |128 MB/s|65,536|16,384|
  |320 MB/s|160,000|40,000|

  As can be determined from this chart, in the scenario presented, no matter what the use, the bus will never be a bottleneck, as the spindle maximum is 100 I/O, well below any of the above thresholds.

  >[!NOTE]
  >This assumes that the SCSI bus is 100% efficient.
  
- **SCSI adapter –** For determining the amount of I/O that this can handle, the manufacturer’s specifications need to be checked. Directing I/O requests to the appropriate device requires processing of some sort, thus the amount of I/O that can be handled is dependent on the SCSI adapter (or array controller) processor.

  In this example, the assumption that 1,000 I/O can be handled will be made.

- **PCI bus –** This is an often overlooked component. In this example, this will not be the bottleneck; however as systems scale up, it can become a bottleneck. For reference, a 32 bit PCI bus operating at 33Mhz can in theory transfer 133 MB/s of data. Following is the equation:  
  > 32 bits &divide; 8 bits per byte &times; 33 MHz = 133 MB/s.  

  Note that is the theoretical limit; in reality only about 50% of the maximum is actually reached, although in certain burst scenarios, 75% efficiency can be obtained for short periods.

  A 66Mhz 64-bit PCI bus can support a theoretical maximum of (64 bits &divide; 8 bits per byte &times; 66 Mhz) = 528 MB/sec. Additionally, any other device (such as the network adapter, second SCSI controller, and so on) will reduce the bandwidth available as the bandwidth is shared and the devices will contend for the limited resources.

After analysis of the components of this storage subsystem, the spindle is the limiting factor in the amount of I/O that can be requested, and consequently the amount of data that can transit the system. Specifically, in an AD DS scenario, this is 100 random I/O per second in 8 KB increments, for a total of 800 KB per second when accessing the Jet database. Alternatively, the maximum throughput for a spindle that is exclusively allocated to log files would suffer the following limitations: 300 sequential I/O per second in 8 KB increments, for a total of 2400 KB (2.4 MB) per second.

Now, having analyzed a simple configuration, the following table demonstrates where the bottleneck will occur as components in the storage subsystem are changed or added.

|Notes|Bottleneck analysis|Disk|Bus|Adapter|PCI bus|
|-|-|-|-|-|-|
|This is the domain controller configuration after adding a second disk. The disk configuration represents the bottleneck at 800 KB/s.|Add 1 disk (Total=2)<br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD|200 I/Os total<br />800 KB/s total.| | | |
|After adding 7 disks, the disk configuration still represents the bottleneck at 3200 KB/s.|**Add 7 disks (Total=8)**  <br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD|800 I/Os total.<br />3200 KB/s total| | | |
|After changing I/O to sequential, the network adapter becomes the bottleneck because it is limited to 1000 IOPS.|Add 7 disks (Total=8)<br /><br />**I/O is sequential**<br /><br />4 KB block size<br /><br />10,000 RPM HD| | |2400 I/O sec can be read/written to disk, controller limited to 1000 IOPS| |
|After replacing the network adapter with a SCSI adapter that supports 10,000 IOPS, the bottleneck returns to the disk configuration.|Add 7 disks (Total=8)<br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD<br /><br />**Upgrade SCSI adapter (now supports 10,000 I/O)**|800 I/Os total.<br />3,200 KB/s total| | | |
|After increasing the block size to 32 KB, the bus becomes the bottleneck because it only supports 20 MB/s.|Add 7 disks (Total=8)<br /><br />I/O is random<br /><br />**32 KB block size**<br /><br />10,000 RPM HD| |800 I/Os total. 25,600 KB/s (25 MB/s) can be read/written to disk.<br /><br />The bus only supports 20 MB/s| | |
|After upgrading the bus and adding more disks, the disk remains the bottleneck.|**Add 13 disks (Total=14)**<br /><br />Add second SCSI adapter with 14 disks<br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD<br /><br />**Upgrade to 320 MB/s SCSI bus**|2800 I/Os<br /><br />11,200 KB/s (10.9 MB/s)| | | |
|After changing I/O to sequential, the disk remains the bottleneck.|Add 13 disks (Total=14)<br /><br />Add second SCSI Adapter with 14 disks<br /><br />**I/O is sequential**<br /><br />4 KB block size<br /><br />10,000 RPM HD<br /><br />Upgrade to 320 MB/s SCSI bus|8,400 I/Os<br /><br />33,600 KB\s<br /><br />(32.8 MB\s)| | | |
|After adding faster hard drives, the disk remains the bottleneck.|Add 13 disks (Total=14)<br /><br />Add second SCSI adapter with 14 disks<br /><br />I/O is sequential<br /><br />4 KB block size<br /><br />**15,000 RPM HD**<br /><br />Upgrade to 320 MB/s SCSI bus|14,000 I/Os<br /><br />56,000 KB/s<br /><br />(54.7 MB/s)| | | |
|After increasing the block size to 32 KB, the PCI bus becomes the bottleneck.|Add 13 disks (Total=14)<br /><br />Add second SCSI adapter with 14 disks<br /><br />I/O is sequential<br /><br />**32 KB block size**<br /><br />15,000 RPM HD<br /><br />Upgrade to 320 MB/s SCSI bus| | | |14,000 I/Os<br /><br />448,000 KB/s<br /><br />(437 MB/s) is the read/write limit to the spindle.<br /><br />The PCI bus supports a theoretical maximum of 133 MB/s (75% efficient at best).|

### Introducing RAID

The nature of a storage subsystem does not change dramatically when an array controller is introduced; it just replaces the SCSI adapter in the calculations. What does change is the cost of reading and writing data to the disk when using the various array levels (such as RAID 0, RAID 1, or RAID 5).

In RAID 0, the data is striped across all the disks in the RAID set. This means that during a read or a write operation, a portion of the data is pulled from or pushed to each disk, increasing the amount of data that can transit the system during the same time period. Thus, in one second, on each spindle (again assuming 10,000-RPM drives), 100 I/O operations can be performed. The total amount of I/O that can be supported is N spindles times 100 I/O per second per spindle (yields 100*N I/O per second).

![Logical d: drive](media/capacity-planning-considerations-logical-d-drive.png)

In RAID 1, the data is mirrored (duplicated) across a pair of spindles for redundancy. Thus, when a read I/O operation is performed, data can be read from both of the spindles in the set. This effectively makes the I/O capacity from both disks available during a read operation. The caveat is that write operations gain no performance advantage in a RAID 1. This is because the same data needs to be written to both drives for the sake of redundancy. Though it does not take any longer, as the write of data occurs concurrently on both spindles, because both spindles are occupied duplicating the data, a write I/O operation in essence prevents two read operations from occurring. Thus, every write I/O costs two read I/O. A formula can be created from that information to determine the total number of I/O operations that are occurring:  

> *Read I/O* + 2 &times; *Write I/O* = *Total available disk I/O consumed*  

When the ratio of reads to writes and the number of spindles are known, the following equation can be derived from the above equation to identify the maximum I/O that can be supported by the array:  

> *Maximum IOPS per spindle* &times; 2 spindles &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 2 &times; *%Writes*)] = *Total IOPS*

RAID 1+ 0, behaves exactly the same as RAID 1 regarding the expense of reading and writing. However, the I/O is now striped across each mirrored set. If  

> *Maximum IOPS per spindle* &times; 2 spindles &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 2 &times; *%Writes*)] = *Total I/O*  

in a RAID 1 set, when a multiplicity (*N*) of RAID 1 sets are striped, the Total I/O that can be processed becomes N &times; I/O per RAID 1 set:  

> *N* &times; {*Maximum IOPS per spindle* &times; 2 spindles &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 2 &times; *%Writes*)] } = *Total IOPS*

In RAID 5, sometimes referred to as *N* + 1 RAID, the data is striped across *N* spindles and parity information is written to the “+ 1” spindle. However, RAID 5 is much more expensive when performing a write I/O than RAID 1 or 1 + 0. RAID 5 performs the following process every time a write I/O is submitted to the array:

1. Read the old data
1. Read the old parity
1. Write the new data
1. Write the new parity

As every write I/O request that is submitted to the array controller by the operating system requires four I/O operations to complete, write requests submitted take four times as long to complete as a single read I/O. To derive a formula to translate I/O requests from the operating system perspective to that experienced by the spindles:  

> *Read I/O* + 4 &times; *Write I/O* = *Total I/O*  

Similarly in a RAID 1 set, when the ratio of reads to writes and the number of spindles are known, the following equation can be derived from the above equation to identify the maximum I/O that can be supported by the array (Note that total number of spindles does not include the “drive” lost to parity):  

> *IOPS per spindle* &times; (*Spindles* – 1) &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 4 &times; *%Writes*)] = *Total IOPS*

### Introducing SANs

Expanding the complexity of the storage subsystem, when a SAN is introduced into the environment, the basic principles outlined do not change, however I/O behavior for all of the systems connected to the SAN needs to be taken into account. As one of the major advantages in using a SAN is an additional amount of redundancy over internally or externally attached storage, capacity planning now needs to take into account fault tolerance needs. Also, more components are introduced that need to be evaluated. Breaking a SAN down into the component parts:

- SCSI or Fibre Channel hard drive
- Storage unit channel backplane
- Storage units
- Storage controller module
- SAN switch(es)
- HBA(s)
- The PCI bus

When designing any system for redundancy, additional components are included to accommodate the potential of failure. It is very important, when capacity planning, to exclude the redundant component from available resources. For example, if the SAN has two controller modules, the I/O capacity of one controller module is all that should be used for total I/O throughput available to the system. This is due to the fact that if one controller fails, the entire I/O load demanded by all connected systems will need to be processed by the remaining controller. As all capacity planning is done for peak usage periods, redundant components should not be factored into the available resources and planned peak utilization should not exceed 80% saturation of the system (in order to accommodate bursts or anomalous system behavior). Similarly, the redundant SAN switch, storage unit, and spindles should not be factored into the I/O calculations.

When analyzing the behavior of the SCSI or Fibre Channel hard drive, the method of analyzing the behavior as outlined previously does not change. Although there are certain advantages and disadvantages to each protocol, the limiting factor on a per disk basis is the mechanical limitation of the hard drive.

Analyzing the channel on the storage unit is exactly the same as calculating the resources available on the SCSI bus, or bandwidth (such as 20 MB/s) divided by block size (such as 8 KB). Where this deviates from the simple previous example is in the aggregation of multiple channels. For example, if there are 6 channels, each supporting 20 MB/s maximum transfer rate, the total amount of I/O and data transfer that is available is 100 MB/s (this is correct, it is not 120 MB/s). Again, fault tolerance is a major player in this calculation, in the event of the loss of an entire channel, the system is only left with 5 functioning channels. Thus, to ensure continuing to meet performance expectations in the event of failure, total throughput for all of the storage channels should not exceed 100 MB/s (this assumes load and fault tolerance is evenly distributed across all channels). Turning this into an I/O profile is dependent on the behavior of the application. In the case of Active Directory Jet I/O, this would correlate to approximately 12,500 I/O per second (100 MB/s &divide; 8 KB per I/O).

Next, obtaining the manufacturer’s specifications for the controller modules is required in order to gain an understanding of the throughput each module can support. In this example, the SAN has two controller modules that support 7,500 I/O each. The total throughput of the system may be 15,000 IOPS if redundancy is not desired. In calculating maximum throughput in the case of failure, the limitation is the throughput of one controller, or 7,500 IOPS. This threshold is well below the 12,500 IOPS (assuming 4 KB block size) maximum that can be supported by all of the storage channels, and thus, is currently the bottleneck in the analysis. Still for planning purposes, the desired maximum I/O to be planned for would be 10,400 I/O.

When the data exits the controller module, it transits a Fibre Channel connection rated at 1 GB/s (or 1 Gigabit per second). To correlate this with the other metrics, 1 GB/s turns into 128 MB/s (1 GB/s &divide; 8 bits/byte). As this is in excess of the total bandwidth across all channels in the storage unit (100 MB/s), this will not bottleneck the system. Additionally, as this is only one of the two channels (the additional 1 GB/s Fibre Channel connection being for redundancy), if one connection fails, the remaining connection still has enough capacity to handle all the data transfer demanded.

En route to the server, the data will most likely transit a SAN switch. As the SAN switch has to process the incoming I/O request and forward it out the appropriate port, the switch will have a limit to the amount of I/O that can be handled, however, manufacturers specifications will be required to determine what that limit is. For example, if there are two switches and each switch can handle 10,000 IOPS, the total throughput will be 20,000 IOPS. Again, fault tolerance being a concern, if one switch fails, the total throughput of the system will be 10,000 IOPS. As it is desired not to exceed 80% utilization in normal operation, using no more than 8000 I/O should be the target.

Finally, the HBA installed in the server would also have a limit to the amount of I/O that it can handle. Usually, a second HBA is installed for redundancy, but just like with the SAN switch, when calculating maximum I/O that can be handled, the total throughput of *N* &ndash; 1 HBAs is what the maximum scalability of the system is.

### Caching considerations

Caches are one of the components that can significantly impact the overall performance at any point in the storage system. Detailed analysis about caching algorithms is beyond the scope of this article; however, some basic statements about caching on disk subsystems are worth illuminating:

- Caching does improved sustained sequential write I/O as it can buffer many smaller write operations into larger I/O blocks and de-stage to storage in fewer, but larger block sizes. This will reduce total random I/O and total sequential I/O, thus providing more resource availability for other I/O.
- Caching does not improve sustained write I/O throughput of the storage subsystem. It only allows for the writes to be buffered until the spindles are available to commit the data. When all the available I/O of the spindles in the storage subsystem is saturated for long periods, the cache will eventually fill up. In order to empty the cache, enough time between bursts, or extra spindles, need to be allotted in order to provide enough I/O to allow the cache to flush.

  Larger caches only allow for more data to be buffered. This means longer periods of saturation can be accommodated.

  In a normally operating storage subsystem, the operating system will experience improved write performance as the data only needs to be written to cache. Once the underlying media is saturated with I/O, the cache will fill and write performance will return to disk speed.

- When caching read I/O, the scenario where the cache is most advantageous is when the data is stored sequentially on the disk, and the cache can read-ahead (it makes the assumption that the next sector contains the data that will be requested next).
- When read I/O is random, caching at the drive controller is unlikely to provide any enhancement to the amount of data that can be read from the disk. Any enhancement is non-existent if the operating system or application-based cache size is greater than the hardware-based cache size.

  In the case of Active Directory, the cache is only limited by the amount of RAM.

### SSD considerations

SSDs are a completely different animal than spindle-based hard disks. Yet the two key criteria remain: “How many IOPS can it handle?” and “What is the latency for those IOPS?” In comparison to spindle-based hard disks, SSDs can handle higher volumes of I/O and can have lower latencies. In general and as of this writing, while SSDs are still expensive in a cost-per-Gigabyte comparison, they are very cheap in terms of cost-per-I/O and deserve significant consideration in terms of storage performance.

Considerations:

- Both IOPS and latencies are very subjective to the manufacturer designs and in some cases have been observed to be poorer performing than spindle based technologies. In short, it is more important to review and validate the manufacturer specs drive by drive and not assume any generalities.
- IOPS types can have very different numbers depending on whether it is read or write. AD DS services, in general, being predominantly read-based, will be less affected than some other application scenarios.
- “Write endurance” – this is the concept that SSD cells will eventually wear out. Various manufacturers deal with this challenge different fashions. At least for the database drive, the predominantly read I/O profile allows for downplaying the significance of this concern as the data is not highly volatile.

### Summary

One way to think about storage is picturing household plumbing. Imagine the IOPS of the media that the data is stored on is the household main drain. When this is clogged (such as roots in the pipe) or limited (it is collapsed or too small), all the sinks in the household back up when too much water is being used (too many guests). This is perfectly analogous to a shared environment where one or more systems are leveraging shared storage on an SAN/NAS/iSCSI with the same underlying media. Different approaches can be taken to resolve the different scenarios:

- A collapsed or undersized drain requires a full scale replacement and fix. This would be similar to adding in new hardware or redistributing the systems using the shared storage throughout the infrastructure.
- A “clogged” pipe usually means identification of one or more offending problems and removal of those problems. In a storage scenario this could be storage or system level backups, synchronized antivirus scans across all servers, and synchronized defragmentation software running during peak periods.

In any plumbing design, multiple drains feed into the main drain. If anything stops up one of those drains or a junction point, only the things behind that junction point back up. In a storage scenario, this could be an overloaded switch (SAN/NAS/iSCSI scenario), driver compatibility issues (wrong driver/HBA Firmware/storport.sys combination), or backup/antivirus/defragmentation. To determine if the storage “pipe” is big enough, IOPS and I/O size needs to be measured. At each joint add them together to ensure adequate “pipe diameter.”

## Appendix D - Discussion on storage troubleshooting - Environments where providing at least as much RAM as the database size is not a viable option

It is helpful to understand why these recommendations exist so that the changes in storage technology can be accommodated. These recommendations exist for two reasons. The first is isolation of IO, such that performance issues (that is, paging) on the operating system spindle do not impact performance of the database and I/O profiles. The second is that log files for AD DS (and most databases) are sequential in nature, and spindle-based hard drives and caches have a huge performance benefit when used with sequential I/O as compared to the more random I/O patterns of the operating system and almost purely random I/O patterns of the AD DS database drive. By isolating the sequential I/O to a separate physical drive, throughput can be increased. The challenge presented by today’s storage options is that the fundamental assumptions behind these recommendations are no longer true. In many virtualized storage scenarios, such as iSCSI, SAN, NAS, and Virtual Disk image files, the underlying storage media is shared across multiple hosts, thus completely negating both the “isolation of IO” and the “sequential I/O optimization” aspects. In fact these scenarios add an additional layer of complexity in that other hosts accessing the shared media can degrade responsiveness to the domain controller.

In planning storage performance, there are three categories to consider: cold cache state, warmed cache state, and backup/restore. The cold cache state occurs in scenarios such as when the domain controller is initially rebooted or the Active Directory service is restarted and there is no Active Directory data in RAM. Warm cache state is where the domain controller is in a steady state and the database is cached. These are important to note as they will drive very different performance profiles, and having enough RAM to cache the entire database does not help performance when the cache is cold. One can consider performance design for these two scenarios with the following analogy, warming the cold cache is a “sprint” and running a server with a warm cache is a “marathon.”

For both the cold cache and warm cache scenario, the question becomes how fast the storage can move the data from disk into memory. Warming the cache is a scenario where, over time, performance improves as more queries reuse data, the cache hit rate increases, and the frequency of needing to go to disk decreases. As a result the adverse performance impact of going to disk decreases. Any degradation in performance is only transient while waiting for the cache to warm and grow to the maximum, system-dependent allowed size. The conversation can be simplified to how quickly the data can be gotten off of disk, and is a simple measure of the IOPS available to Active Directory, which is subjective to IOPS available from the underlying storage. From a planning perspective, because warming the cache and backup/restore scenarios happen on an exceptional basis, normally occur off hours, and are subjective to the load of the DC, general recommendations do not exist except in that these activities be scheduled for non-peak hours.

AD DS, in most scenarios, is predominantly read IO, usually a ratio of 90% read/10% write. Read I/O often tends to be the bottleneck for user experience, and with write IO, causes write performance to degrade. As I/O to the NTDS.dit is predominantly random, caches tend to provide minimal benefit to read IO, making it that much more important to configure the storage for read I/O profile correctly.

For normal operating conditions, the storage planning goal is minimize the wait times for a request from AD DS to be returned from disk. This essentially means that the number of outstanding and pending I/O is less than or equivalent to the number of pathways to the disk. There are a variety of ways to measure this. In a performance monitoring scenario, the general recommendation is that LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read be less than 20 ms. The desired operating threshold must be much lower, preferably as close to the speed of the storage as possible, in the 2 to 6 millisecond (.002 to .006 second) range depending on the type of storage.

Example:

![Storage latency chart](media/capacity-planning-considerations-storage-latency.png)

Analyzing the chart:

- **Green oval on the left –** The latency remains consistent at 10 ms. The load increases from 800 IOPS to 2400 IOPS. This is the absolute floor to how quickly an I/O request can be processed by the underlying storage. This is subject to the specifics of the storage solution.
- **Burgundy oval on the right –** The throughput remains flat from the exit of the green circle through to the end of the data collection while the latency continues to increase. This is demonstrating that when the request volumes exceed the physical limitations of the underlying storage, the longer the requests spend sitting in the queue waiting to be sent out to the storage subsystem.

Applying this knowledge:

- **Impact to a user querying membership of a large group –** Assume this requires reading 1 MB of data from the disk, the amount of I/O and how long it takes can be evaluated as follows:
  - Active Directory database pages are 8 KB in size. 
  - A minimum of 128 pages need to be read in from disk. 
  - Assuming nothing is cached, at the floor (10 ms) this is going to take a minimum 1.28 seconds to load the data from disk in order to return it to the client. At 20 ms, where the throughput on storage has long since maxed out and is also the recommended maximum, it will take 2.5 seconds to get the data from disk in order to return it to the end user.  
- **At what rate will the cache be warmed –** Making the assumption that the client load is going to maximize the throughput on this storage example, the cache will warm at a rate of 2400 IOPS &times; 8 KB per IO. Or, approximately 20 MB/s per second, loading about 1 GB of database into RAM every 53 seconds.

> [!NOTE]
> It is normal for short periods to observe the latencies climb when components aggressively read or write to disk, such as when the system is being backed up or when AD DS is running garbage collection. Additional head room on top of the calculations should be provided to accommodate these periodic events. The goal being to provide enough throughput to accommodate these scenarios without impacting normal function.

As can be seen, there is a physical limit based on the storage design to how quickly the cache can possibly warm. What will warm the cache are incoming client requests up to the rate that the underlying storage can provide. Running scripts to “pre-warm” the cache during peak hours will provide competition to load driven by real client requests. That can adversely affect delivering data that clients need first because, by design, it will generate competition for scarce disk resources as artificial attempts to warm the cache will load data that is not relevant to the clients contacting the DC.Prozessor-Information(_Total)\\"Prozessor-Hilfsprogramm Domain Services
description: Detailed discussion of the factors to consider during capacity planning for AD DS.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; kenbrunf
author: Teresa-Motiv
ms.date: 7/3/2019
---

# Capacity planning for Active Directory Domain Services

This topic is originally written by Ken Brumfield, Senior Premier Field Engineer at Microsoft, and provides recommendations for capacity planning for Active Directory Domain Services (AD DS).

## Goals of capacity planning

Capacity planning is not the same as troubleshooting performance incidents. They are closely related, but quite different. The goals of capacity planning are:  

- Properly implement and operate an environment 
- Minimize the time spent troubleshooting performance issues.  
  
In capacity planning, an organization might have a baseline target of 40% processor utilization during peak periods in order to meet client performance requirements and accommodate the time necessary to upgrade the hardware in the datacenter. Whereas, to be notified of abnormal performance incidents, a monitoring alert threshold might be set at 90% over a 5 minute interval.

The difference is that when a capacity management threshold is continually exceeded (a one-time event is not a concern), adding capacity (that is, adding in more or faster processors) would be a solution or scaling the service across multiple servers would be a solution. Performance alert thresholds indicate that client experience is currently suffering and immediate steps are needed to address the issue.

As an analogy: capacity management is about preventing a car accident (defensive driving, making sure the brakes are working properly, and so on) whereas performance troubleshooting is what the police, fire department, and emergency medical professionals do after an accident. This is about “defensive driving,” Active Directory-style.

Over the last several years, capacity planning guidance for scale-up systems has changed dramatically. The following changes in system architectures have challenged fundamental assumptions about designing and scaling a service:

- 64-bit server platforms  
- Virtualization  
- Increased attention to power consumption  
- SSD storage  
- Cloud scenarios  

Additionally, the approach is shifting from a server-based capacity planning exercise to a service-based capacity planning exercise. Active Directory Domain Services (AD DS), a mature distributed service that many Microsoft and third-party products use as a backend, becomes one the most critical products to plan correctly to ensure the necessary capacity for other applications to run.

### Baseline requirements for capacity planning guidance

Throughout this article, the following baseline requirements are expected:

- Readers have read and are familiar with [Performance Tuning Guidelines for Windows Server 2012 R2](https://docs.microsoft.com/previous-versions//dn529133(v=vs.85)).
- The Windows Server platform is an x64 based architecture. But even if your Active Directory environment is installed on Windows Server 2003 x86 (now beyond the end of the support lifecycle) and has a directory information tree (DIT) that is less 1.5 GB in size and that can easily be held in memory, the guidelines from this article are still applicable.
- Capacity planning is a continuous process and you should regularly review how well the environment is meeting expectations.
- Optimization will occur over multiple hardware lifecycles as hardware costs change. For example, memory becomes cheaper, the cost per core decreases, or the price of different storage options change.
- Plan for the peak busy period of the day. It is recommended to look at this in either 30 minute or hour intervals. Anything greater may hide the actual peaks and anything less may be distorted by “transient spikes.”
- Plan for growth over the course of the hardware lifecycle for the enterprise. This may include a strategy of upgrading or adding hardware in a staggered fashion, or a complete refresh every three to five years. Each will require a “guess” as how much the load on Active Directory will grow. Historical data, if collected, will help with this assessment. 
- Plan for fault tolerance. Once an estimate *N* is derived, plan for scenarios that include *N* &ndash; 1, *N* &ndash; 2, *N* &ndash; *x*.
  - Add in additional servers according to organizational need to ensure that the loss of a single or multiple servers does not exceed maximum peak capacity estimates.
  - Also consider that the growth plan and fault tolerance plan need to be integrated. For example, if one DC is required to support the load, but the estimate is that the load will be doubled in the next year and require two DCs total, there will not be enough capacity to support fault tolerance. The solution would be to start with three DCs. One could also plan to add the third DC after 3 or 6 months if budgets are tight.

    >[!NOTE]
    >Adding Active Directory-aware applications might have a noticeable impact on the DC load, whether the load is coming from the application servers or clients.

### Three-step process for the capacity planning cycle

In capacity planning, first decide what quality of service is needed. For example, a core datacenter supports a higher level of concurrency and requires more consistent experience for users and consuming applications, which requires greater attention to redundancy and minimizing system and infrastructure bottlenecks. In contrast, a satellite location with a handful of users does not need the same level of concurrency or fault tolerance. Thus, the satellite office might not need as much attention to optimizing the underlying hardware and infrastructure, which may lead to cost savings. All recommendations and guidance herein are for optimal performance, and can be selectively relaxed for scenarios with less demanding requirements.

The next question is: virtualized or physical? From a capacity planning perspective, there is no right or wrong answer; there is only a different set of variables to work with. Virtualization scenarios come down to one of two options:

- “Direct mapping” with one guest per host (where virtualization exists solely to abstract the physical hardware from the server)
- “Shared host”

Testing and production scenarios indicate that the “direct mapping” scenario can be treated identically to a physical host. “Shared host,” however, introduces a number of considerations spelled out in more detail later. The “shared host” scenario means that AD DS is also competing for resources, and there are penalties and tuning considerations for doing so.

With these considerations in mind, the capacity planning cycle is an iterative three-step process:

1. Measure the existing environment, determine where the system bottlenecks currently are, and get environmental basics necessary to plan the amount of capacity needed.
1. Determine the hardware needed according to the criteria outlined in step 1.
1. Monitor and validate that the infrastructure as implemented is operating within specifications. Some data collected in this step becomes the baseline for the next cycle of capacity planning.

### Applying the process

To optimize performance, ensure these major components are correctly selected and tuned to the application loads:

1. Memory
1. Network
1. Storage
1. Processor
1. Net Logon

The basic storage requirements of AD DS and the general behavior of well written client software allow environments with as many as 10,000 to 20,000 users to forego heavy investment in capacity planning with regards to physical hardware, as almost any modern server class system will handle the load. That said, the following table summarizes how to evaluate an existing environment in order to select the right hardware. Each component is analyzed in detail in subsequent sections to help AD DS administrators evaluate their infrastructure using baseline recommendations and environment-specific principals.

In general:

- Any sizing based on current data will only be accurate for the current environment.
- For any estimates, expect demand to grow over the lifecycle of the hardware.
- Determine whether to oversize today and grow into the larger environment, or add capacity over the lifecycle.
- For virtualization, all the same capacity planning principals and methodologies apply, except that the overhead of the virtualization needs to be added to anything domain related.
- Capacity planning, like anything that attempts to predict, is NOT an accurate science. Do not expect things to calculate perfectly and with 100% accuracy. The guidance here is the leanest recommendation; add in capacity for additional safety and continuously validate that the environment remains on target.

### Data collection summary tables

#### New environment

| Component | Estimates |
|-|-|
|Storage/Database Size|40 KB to 60 KB for each user|
|RAM|Database Size<br />Base operating system recommendations<br />Third-party applications|
|Network|1 GB|
|CPU|1000 concurrent users for each core|

#### High-level evaluation criteria

| Component | Evaluation criteria | Planning considerations |
|-|-|-|
|Storage/Database size|The section entitled “To activate logging of disk space that is freed by defragmentation” in [Storage Limits](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))| |
|Storage/ Database performance|<ul><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Write," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer"</li><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Reads/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Writes/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec"</li></ul>|<ul><li>Storage has two concerns to address<ul><li>Space available, which with the size of today’s spindle based and SSD based storage is irrelevant for most AD environments.</li> <li>Input/Output (IO) Operations available – In many environments, this is often overlooked. But it is important to evaluate only environments where there is not enough RAM to load the entire NTDS Database into memory.</li></ul><li>Storage can be a complex topic and should involve hardware vendor expertise for proper sizing. Particularly with more complex scenarios such as SAN, NAS, and iSCSI scenarios. However, in general, cost per Gigabyte of storage is often in direct opposition to cost per IO:<ul><li>RAID 5 has lower cost per Gigabyte than Raid 1, but Raid 1 has lower cost per IO</li><li>Spindle-based hard drives have lower cost per Gigabyte, but SSDs have a lower cost per IO</li></ul><li>After a restart of the computer or the Active Directory Domain Services service, the Extensible Storage Engine (ESE) cache is empty and performance will be disk bound while the cache warms.</li><li>In most environments AD is read intensive I/O in a random pattern to disks, negating much of the benefit of caching and read optimization strategies.  Plus, AD has a way larger cache in memory than most storage system caches.</li></ul>
|RAM|<ul><li>Database size</li><li>Base operating system recommendations</li><li>Third-party applications</li></ul>|<ul><li>Storage is the slowest component in a computer. The more that can be resident in RAM, the less it is necessary to go to disk.</li><li>Ensure enough RAM is allocated to store the operating system, Agents (antivirus, backup, monitoring), NTDS Database and growth over time.</li><li>For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage section to ensure that storage is properly sized.</li></ul>|
|Network|<ul><li>“Network Interface(\*)\Bytes Received/sec”</li><li>“Network Interface(\*)\Bytes Sent/sec”|<ul><li>In general, traffic sent from a DC far exceeds traffic sent to a DC.</li><li>As a switched Ethernet connection is full-duplex, inbound and outbound network traffic need to be sized independently.</li><li>Consolidating the number of DCs will increase the amount of bandwidth used to send responses back to client requests for each DC, but will be close enough to linear for the site as a whole.</li><li>If removing satellite location DCs, don’t forget to add the bandwidth for the satellite DC into the hub DCs as well as use that to evaluate how much WAN traffic there will be.</li></ul>|
|CPU|<ul><li>“Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read”</li><li>“Process(lsass)\\% Processor Time”</li></ul>|<ul><li>After eliminating storage as a bottleneck, address the amount of compute power needed.</li><li>While not perfectly linear, the number of processor cores consumed across all servers within a specific scope (such as a site) can be used to gauge how many processors are necessary to support the total client load. Add the minimum necessary to maintain the current level of service across all the systems within the scope.</li><li>Changes in processor speed, including power management related changes, impact numbers derived from the current environment. Generally, it is impossible to precisely evaluate how going from a 2.5 GHz processor to a 3 GHz processor will reduce the number of CPUs needed.</li></ul>|
|NetLogon|<ul><li>“Netlogon(\*)\Semaphore Acquires”</li><li>“Netlogon(\*)\Semaphore Timeouts”</li><li>“Netlogon(\*)\Average Semaphore Hold Time”</li></ul>|<ul><li>Net Logon Secure Channel/MaxConcurrentAPI only affects environments with NTLM authentications and/or PAC Validation. PAC Validation is on by default in operating system versions before Windows Server 2008. This is a client setting, so the DCs will be impacted until this is turned off on all client systems.</li><li>Environments with significant cross trust authentication, which includes intra-forest trusts, have greater risk if not sized properly.</li><li>Server consolidations will increase concurrency of cross-trust authentication.</li><li>Surges need to be accommodated, such as cluster fail-overs, as users re-authenticate en masse to the new cluster node.</li><li>Individual client systems (such as a cluster) might need tuning too.</li></ul>|

## Planning

For a long time, the community’s recommendation for sizing AD DS has been to “put in as much RAM as the database size.” For the most part, that recommendation is all that most environments needed to be concerned about. But the ecosystem consuming AD DS has gotten much bigger, as have the AD DS environments themselves, since its introduction in 1999. Although the increase in compute power and the switch from x86 architectures to x64 architectures has made the subtler aspects of sizing for performance irrelevant to a larger set of customers running AD DS on physical hardware, the growth of virtualization has reintroduced the tuning concerns to a larger audience than before.

The following guidance is thus about how to determine and plan for the demands of Active Directory as a service regardless of whether it is deployed in a physical, a virtual/physical mix, or a purely virtualized scenario. As such, we will break down the evaluation to each of the four main components: storage, memory, network, and processor. In short, in order to maximize performance on AD DS, the goal is to get as close to processor bound as possible.

## RAM

Simply, the more that can be cached in RAM, the less it is necessary to go to disk. To maximize the scalability of the server the minimum amount of RAM should be the sum of the current database size, the total SYSVOL size, the operating system recommended amount, and the vendor recommendations for the agents (antivirus, monitoring, backup, and so on). An additional amount should be added to accommodate growth over the lifetime of the server. This will be environmentally subjective based on estimates of database growth based on environmental changes.

For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage  section to ensure that storage is properly designed.

A corollary that comes up in the general context in sizing memory is sizing of the page file. In the same context as everything else memory related, the goal is to minimize going to the much slower disk. Thus the question should go from, “how should the page file be sized?” to “how much RAM is needed to minimize paging?” The answer to the latter question is outlined in the rest of this section. This leaves most of the discussion for sizing the page file to the realm of general operating system recommendations and the need to configure the system for memory dumps, which are unrelated to AD DS performance.

### Evaluating

The amount of RAM that a domain controller (DC) needs is actually a complex exercise for these reasons:

- High potential for error when trying to use an existing system to gauge how much RAM is needed as LSASS will trim under memory pressure conditions, artificially deflating the need.
- The subjective fact that an individual DC only needs to cache what is “interesting” to its clients. This means that the data that needs to be cached on a DC in a site with only an Exchange server will be very different than the data that needs to be cached on a DC that only authenticates users.
- The labor to evaluate RAM for each DC on a case-by-case basis is prohibitive and changes as the environment changes.
- The criteria behind the recommendation will help to make informed decisions: 
- The more that can be cached in RAM, the less it is necessary to go to disk. 
- Storage is by far the slowest component of a computer. Access to data on spindle-based and SSD storage media is on the order of 1,000,000x slower than access to data in RAM.

Thus, in order to maximize the scalability of the server, the minimum amount of RAM is the sum of the current database size, the total SYSVOL size, the operating system recommended amount, and the vendor recommendations for the agents (antivirus, monitoring, backup, and so on). Add additional amounts to accommodate growth over the lifetime of the server. This will be environmentally subjective based on estimates of database growth. However, for satellite locations with a small set of end users, these requirements can be relaxed as these sites will not need to cache as much to service most of the requests.

For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage section to ensure that storage is properly sized.

> [!NOTE]
> A corollary while sizing memory is sizing of the page file. Because the goal is to minimize going to the much slower disk, the question goes from “how should the page file be sized?” to “how much RAM is needed to minimize paging?” The answer to the latter question is outlined in the rest of this section. This leaves most of the discussion for sizing the page file to the realm of general operating system recommendations and the need to configure the system for memory dumps, which are unrelated to AD DS performance.

### Virtualization considerations for RAM

Avoid memory over-commit at the host. The fundamental goal behind optimizing the amount of RAM is to minimize the amount of time spent going to disk. In virtualization scenarios, the concept of memory over-commit exists where more RAM is allocated to the guests then exists on the physical machine. This in and of itself is not a problem. It becomes a problem when the total memory actively used by all the guests exceeds the amount of RAM on the host and the underlying host starts paging. Performance becomes disk-bound in cases where the domain controller is going to the NTDS.dit to get data, or the domain controller is going to the page file to get data, or the host is going to disk to get data that the guest thinks is in RAM.

### Calculation summary example

|Component|Estimated memory (example)|
|-|-|
|Base operating system recommended RAM (Windows Server 2008)|2 GB|
|LSASS internal tasks|200 MB|
|Monitoring agent|100 MB|
|Antivirus|100 MB|
|Database (Global Catalog)|8.5 GB are you sure ???|
|Cushion for backup to run, administrators to log on without impact|1 GB|
|Total|12 GB|

**Recommended: 16 GB**

Over time, the assumption can be made that more data will be added to the database and the server will probably be in production for 3 to 5 years. Based on an estimate of growth of 33%, 16 GB would be a reasonable amount of RAM to put in a physical server. In a virtual machine, given the ease with which settings can be modified and RAM can be added to the VM, starting at 12 GB with the plan to monitor and upgrade in the future is reasonable.

## Network

### Evaluating
This section is less about evaluating the demands regarding replication traffic, which is focused on traffic traversing the WAN and is thoroughly covered in [Active Directory Replication Traffic](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10)), than it is about evaluating total bandwidth and network capacity needed, inclusive of client queries, Group Policy applications, and so on. For existing environments, this can be collected by using performance counters “Network Interface(\*)\Bytes Received/sec,” and “Network Interface(\*)\Bytes Sent/sec.” Sample intervals for Network Interface counters in either 15, 30, or 60-Minutenutes. Anything less will generally be too volatile for good measurements; anything greater will smooth out daily peeks excessively.

> [!NOTE]
> Generally, the majority of network traffic on a DC is outbound as the DC responds to client queries. This is the reason for the focus on outbound traffic, though it is recommended to evaluate each environment for inbound traffic also. The same approaches can be used to address and review inbound network traffic requirements. For more information, see Knowledge Base article [929851: The default dynamic port range for TCP/IP has changed in Windows Vista and in Windows Server 2008](http://support.microsoft.com/kb/929851).

### Bandwidth needs

Planning for network scalability covers two distinct categories: the amount of traffic and the CPU load from the network traffic. Each of these scenarios is straight-forward compared to some of the other topics in this article.

In evaluating how much traffic must be supported, there are two unique categories of capacity planning for AD DS in terms of network traffic. The first is replication traffic that traverses between domain controllers and is covered thoroughly in the reference [Active Directory Replication Traffic](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10)) and is still relevant to current versions of AD DS. The second is the intrasite client-to-server traffic. One of the simpler scenarios to plan for, intrasite traffic predominantly receives small requests from clients relative to the large amounts of data sent back to the clients. 100 MB will generally be adequate in environments up to 5,000 users per server, in a site. Using a 1 GB network adapter and Receive Side Scaling (RSS) support is recommended for anything above 5,000 users. To validate this scenario, particularly in the case of server consolidation scenarios, look at Network Interface(\*)\Bytes/sec across all the DCs in a site, add them together, and divide by the target number of domain controllers to ensure that there is adequate capacity. The easiest way to do this is to use the “Stacked Area” view in Windows Reliability and Performance Monitor (formerly known as Perfmon), making sure all of the counters are scaled the same.

Consider the following example (also known as, a really, really complex way to validate that the general rule is applicable to a specific environment). The following assumptions are made:

- The goal is to reduce the footprint to as few servers as possible. Ideally, one server will carry the load and an additional server is deployed for redundancy (*N* + 1 scenario). 
- In this scenario, the current network adapter supports only 100 MB and is in a switched environment.  
  The maximum target network bandwidth utilization is 60% in an N scenario (loss of a DC).
- Each server has about 10,000 clients connected to it.

Knowledge gained from the data in the chart (Network Interface(\*)\Bytes Sent/sec):

1. The business day starts ramping up around 5:30 and winds down at 7:00 PM.
1. The peak busiest period is from 8:00 AM to 8:15 AM, with greater than 25 Bytes sent/sec on the busiest DC.  
   > [!NOTE]
   > All performance data is historical. So the peak data point at 8:15 indicates the load from 8:00 to 8:15.
1. There are spikes before 4:00 AM, with more than 20 Bytes sent/sec on the busiest DC, which could indicate either load from different time zones or background infrastructure activity, such as backups. Since the peak at 8:00 AM exceeds this activity, it is not relevant.
1. There are five Domain Controllers in the site.
1. The max load is about 5.5 MB/s per DC, which represents 44% of the 100 MB connection. Using this data, it can be estimated that the total bandwidth needed between 8:00 AM and 8:15 AM is 28 MB/s.
   >[!NOTE]
   >Be careful with the fact that Network Interface sent/receive counters are in bytes and network bandwidth is measured in bits. 100 MB &divide; 8 = 12.5 MB, 1 GB &divide; 8 = 128 MB.
  
Conclusions:

1. This current environment does meet the N+1 level of fault tolerance at 60% target utilization. Taking one system offline will shift the bandwidth per server from about 5.5 MB/s (44%) to about 7 MB/s (56%).
1. Based on the previously stated goal of consolidating to one server, this both exceeds the maximum target utilization and theoretically the possible utilization of a 100 MB connection.
1. With a 1 GB connection this will represent 22% of the total capacity.
1. Under normal operating conditions in the *N* + 1 scenario, client load will be relatively evenly distributed at about 14 MB/s per server or 11% of total capacity.
1. To ensure that capacity is adequate during unavailability of a DC, the normal operating targets per server would be about 30% network utilization or 38 MB/s per server. Failover targets would be 60% network utilization or 72 MB/s per server.  
  
In short, the final deployment of systems must have a 1 GB network adapter and be connected to a network infrastructure that will support said load. A further note is that given the amount of network traffic generated, the CPU load from network communications can have a significant impact and limit the maximum scalability of AD DS. This same process can be used to estimate the amount of inbound communication to the DC. But given the predominance of outbound traffic relative to inbound traffic, it is an academic exercise for most environments. Ensuring hardware support for RSS is important in environments with greater than 5,000 users per server. For scenarios with high network traffic, balancing of interrupt load can be a bottleneck. This can be detected by Processor(\*)\% Interrupt Time being unevenly distributed across CPUs. RSS enabled NICs can mitigate this limitation and increase scalability.

> [!NOTE]
> A similar approach can be used to estimate the additional capacity necessary when consolidating data centers, or retiring a domain controller in a satellite location. Simply collect the outbound and inbound traffic to clients and that will be the amount of traffic that will now be present on the WAN links.  
>  
> In some cases, you might experience more traffic than expected because traffic is slower, such as when certificate checking fails to meet aggressive time-outs on the WAN. For this reason, WAN sizing and utilization should be an iterative, ongoing process.

### Virtualization considerations for network bandwidth

It is easy to make recommendations for a physical server: 1 GB for servers supporting greater than 5000 users. Once multiple guests start sharing an underlying virtual switch infrastructure, additional attention is necessary to ensure that the host has adequate network bandwidth to support all the guests on the system, and thus requires the additional rigor. This is nothing more than an extension of ensuring the network infrastructure into the host machine. This is regardless whether the network is inclusive of the domain controller running as a virtual machine guest on a host with the network traffic going over a virtual switch, or whether connected directly to a physical switch. The virtual switch is just one more component where the uplink needs to support the amount of data being transmitted. Thus the physical host physical network adapter linked to the switch should be able to support the DC load plus all other guests sharing the virtual switch connected to the physical network adapter.

### Calculation summary example

|System|Peak bandwidth|
|-|-|
DC 1|6.5 MB/s|
DC 2|6.25 MB/s|
|DC 3|6.25 MB/s|
|DC 4|5.75 MB/s|
|DC 5|4.75 MB/s|
|Total|28.5 MB/s|

**Recommended: 72 MB/s** (28.5 MB/s divided by 40 %)

|Target system(s) count|Total bandwidth (from above)|
|-|-|
|2|28.5 MB/s|
|Resulting normal behavior|28.5 &divide; 2 = 14.25 MB/s|

As always, over time the assumption can be made that client load will increase and this growth should be planned for as best as possible. The recommended amount to plan for would allow for an estimated growth in network traffic of 50%.

## Storage

Planning storage constitutes two components:

- Capacity, or storage size
- Performance

A great amount of time and documentation is spent on planning capacity, leaving performance often completely overlooked. With current hardware costs, most environments are not large enough that either of these is actually a concern, and the recommendation to “put in as much RAM as the database size” usually covers the rest, though it may be overkill for satellite locations in larger environments.

### Sizing

#### Evaluating for storage

Compared to 13 years ago when Active Directory was introduced, a time when 4 GB and 9 GB drives were the most common drive sizes, sizing for Active Directory is not even a consideration for all but the largest environments. With the smallest available hard drive sizes in the 180 GB range, the entire operating system, SYSVOL, and NTDS.dit can easily fit on one drive. As such, it is recommended to deprecate heavy investment in this area.

The only recommendation for consideration is to ensure that 110% of the NTDS.dit size is available in order to enable defrag. Additionally, accommodations for growth over the life of the hardware should be made.

The first and most important consideration is evaluating how large the NTDS.dit and SYSVOL will be. These measurements will lead into sizing both fixed disk and RAM allocation. Due to the (relatively) low cost of these components, the math does not need to be rigorous and precise. Content about how to evaluate this for both existing and new environments can be found in the [Data Storage](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961771(v=technet.10)) series of articles. Specifically, refer to the following articles:

- **For existing environments &ndash;** The section titled “To activate logging of disk space that is freed by defragmentation” in the article [Storage Limits](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10)).
- **For new environments &ndash;** The article titled [Growth Estimates for Active Directory Users and Organizational Units](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961779(v=technet.10)).

  > [!NOTE]
  > The articles are based on data size estimates made at the time of the release of Active Directory in Windows 2000. Use object sizes that reflect the actual size of objects in your environment.

When reviewing existing environments with multiple domains, there may be variations in database sizes. Where this is true, use the smallest global catalog (GC) and non-GC sizes.  

The database size can vary between operating system versions. DCs that run earlier operating systems such as Windows Server 2003 has a smaller database size than a DC that runs a later operating system such as Windows Server 2008 R2, especially when features such Active Directory Recycle Bin or Credential Roaming are enabled.

> [!NOTE]  
  >
>- For new environments, notice that the estimates in Growth Estimates for Active Directory Users and Organizational Units indicate that 100,000 users (in the same domain) consume about 450 MB of space. Please note that the attributes populated can have a huge impact on the total amount. Attributes will be populated on many objects by both third-party and Microsoft products, including Microsoft Exchange Server and Lync. An evaluation based on the portfolio of the products in the environment is preferred, but the exercise of detailing out the math and testing for precise estimates for all but the largest environments may not actually be worth significant time and effort.
>- Ensure that 110% of the NTDS.dit size is available as free space in order to enable offline defrag, and plan for growth over a three to five year hardware lifespan. Given how cheap storage is, estimating storage at 300% the size of the DIT as storage allocation is safe to accommodate growth and the potential need for offline defrag.

#### Virtualization considerations for storage

In a scenario where multiple Virtual Hard Disk (VHD) files are being allocated on a single volume use a fixed sized disk of at least 210% (100% of the DIT + 110% free space) the size of the DIT to ensure that there is adequate space reserved.  

#### Calculation summary example

|Data collected from evaluation phase| |
|-|-|
|NTDS.dit size|35 GB|
|Modifier to allow for offline defrag|2.1|
|Total storage needed|73.5 GB|

> [!NOTE]
> This storage needed is in addition to the storage needed for SYSVOL, operating system, page file, temporary files, local cached data (such as installer files), and applications.

### Storage performance

#### Evaluating performance of storage

As the slowest component within any computer, storage can have the biggest adverse impact on client experience. For those environments large enough for which the RAM sizing recommendations are not feasible, the consequences of overlooking planning storage for performance can be devastating.  Also, the complexities and varieties of storage technology further increase the risk of failure as the relevance of long standing best practices of “put operating system, logs, and database” on separate physical disks is limited in it’s useful scenarios.  This is because the long standing best practice is based on the assumption that is that a “disk” is a dedicated spindle and this allowed I/O to be isolated.  This assumptions that make this true are no longer relevant with the introduction of:

- New storage types and virtualized and shared storage scenarios
- Shared spindles on a Storage Area Network (SAN)
- VHD file on a SAN or network-attached storage
- Solid State Drives
- Tiered storage architectures (i.e. SSD storage tier caching larger spindle based storage)

In short, the end goal of all storage performance efforts, regardless of underlying storage architecture and design, is to ensure the needed amount of Input/Output Operations per Second (IOPS) are available and that those IOPS happen within an acceptable time frame. This section covers how to evaluate what AD DS demands of the underlying storage in order to ensure storage solutions are properly designed.  Given the variability of today’s storage technologies, it is best to work with the storage vendors to ensure adequate IOPS.  For those scenarios with locally attached storage, reference the Appendix C for the basics in how to design traditional local storage scenarios.  This principals are generally applicable to more complex storage tiers and will also help in dialog with the vendors supporting backend storage solutions.

- Given the wide breadth of storage options available, it is recommended to engage the expertise of hardware support teams or vendors to ensure that the specific solution meets the needs of AD DS. The following numbers are the information that would be provided to the storage specialists.

For environments where the database is too large to be held in RAM, use the performance counters to determine how much I/O needs to be supported:

- LogicalDisk(\*)\Avg Disk sec/Read (for example, if NTDS.dit is stored on the D:/ drive, the full path would be LogicalDisk(D:)\Avg Disk sec/Read)
- LogicalDisk(\*)\Avg Disk sec/Write
- LogicalDisk(\*)\Avg Disk sec/Transfer
- LogicalDisk(\*)\Reads/sec
- LogicalDisk(\*)\Writes/sec
- LogicalDisk(\*)\Transfers/sec

These should be sampled in 15/30/60 minute intervals to benchmark the demands of the current environment.

#### Evaluating the results

> [!NOTE]
> The focus is on reads from the database as this is usually the most demanding component, the same logic can be applied to writes to the log file by substituting LogicalDisk(*\<NTDS Log\>*)\Avg Disk sec/Write and LogicalDisk(*\<NTDS Log\>*)\Writes/sec):
>  
> - LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read indicates whether or not the current storage is adequately sized.  If the results are roughly equal to the Disk Access Time for the disk type, LogicalDisk(*\<NTDS\>*)\Reads/sec is a valid measure.  Check the manufacturer specifications for the storage on the back end, but good ranges for LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read would roughly be:
>   - 7200 – 9 to 12.5 milliseconds (ms)
>   - 10,000 – 6 to 10 ms
>   - 15,000 – 4 to 6 ms  
>   - SSD – 1 to 3 ms  
>   - >[!NOTE]
>     >Recommendations exist stating that storage performance is degraded at 15ms to 20ms (depending on source).  The difference between the above values and the other guidance is that the above values are the normal operating range.  The other recommendations are troubleshooting guidance to identify when client experience significantly degrades and becomes noticeable.  Reference Appendix C for a deeper explanation.
> - LogicalDisk(*\<NTDS\>*)\Reads/sec is the amount of I/O that is being performed.
>   - If LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read is within the optimal range for the backend storage, LogicalDisk(*\<NTDS\>*)\Reads/sec can be used directly to size the storage.
>   - If LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read is not within the optimal range for the backend storage, additional I/O is needed according to the following formula:
>     > (LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read) &divide; (Physical Media Disk Access Time) &times; (LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read)

Considerations:

- Note that if the server is configured with a sub-optimal amount of RAM, these values will be inaccurate for planning purposes.  They will be erroneously on the high side and can still be used as a worst case scenario.
- Adding/Optimizing RAM specifically will drive a decrease in the amount of read I/O (LogicalDisk(*\<NTDS\>*)\Reads/Sec.  This means the storage solution may not have to be as robust as initially calculated.  Unfortunately, anything more specific than this general statement is environmentally dependent on client load and general guidance cannot be provided.  The best option is to adjust storage sizing after optimizing RAM.

#### Virtualization considerations for performance

Similar to all of the preceding virtualization discussions, the key here is to ensure that the underlying shared infrastructure can support the DC load plus the other resources using the underlying shared media and all pathways to it. This is true whether a physical domain controller is sharing the same underlying media on a SAN, NAS, or iSCSI infrastructure as other servers or applications, whether it is a guest using pass through access to a SAN, NAS, or iSCSI infrastructure that shares the underlying media, or if the guest is using a VHD file that resides on shared media locally or a SAN, NAS, or iSCSI infrastructure. The planning exercise is all about making sure that the underlying media can support the total load of all consumers.

Also, from a guest perspective, as there are additional code paths that must be traversed, there is a performance impact to having to go through a host to access any storage. Not surprisingly, storage performance testing indicates that the virtualizing has an impact on throughput that is subjective to the processor utilization of the host system (see Appendix A: CPU Sizing Criteria), which is obviously influenced by the resources of the host demanded by the guest. This contributes to the virtualization considerations regarding processing needs in a virtualized scenario (see [Virtualization considerations for processing](#virtualization-considerations-for-processing)).

Making this more complex is that there are a variety of different storage options that are available that all have different performance impacts. As a safe estimate when migrating from physical to virtual, use a multiplier of 1.10 to adjust for different storage options for virtualized guests on Hyper-V, such as pass-through storage, SCSI Adapter, or IDE. The adjustments that need to be made when transferring between the different storage scenarios are irrelevant as to whether the storage is local, SAN, NAS, or iSCSI.

#### Calculation summary example

Determining the amount of I/O needed for a healthy system under normal operating conditions:

- LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec during the peak period 15 minute period 
- To determine the amount of I/O needed for storage where the capacity of the underlying storage is exceeded:
  >*Needed IOPS* = (LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read &divide; *\<Target Avg Disk sec/Read\>*) &times; LogicalDisk(*\<NTDS Database Drive\>*)\Read/sec

|Counter|Value|
|-|-|
|Actual LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer|.02 seconds (20 milliseconds)|
|Target LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer|.01 seconds|
|Multiplier for change in available IO|0.02 &divide; 0.01 = 2|  
  
|Value name|Value|
|-|-|
|LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec|400|
|Multiplier for change in available IO|2|
|Total IOPS needed during peak period|800|

To determine the rate at which the cache is desired to be warmed:

- Determine the maximum acceptable time to warm the cache. It is either the amount of time that it should take to load the entire database from disk, or for scenarios where the entire database cannot be loaded in RAM, this would be the maximum time to fill RAM.
- Determine the size of the database, excluding white space.  For more information, see [Evaluating for storage](#evaluating-for-storage).  
- Divide the database size by 8 KB; that will be the total IOs necessary to load the database.
- Divide the total IOs by the number of seconds in the defined time frame.

Note that the rate calculated, while accurate, will not be exact because previously loaded pages are evicted if ESE is not configured to have a fixed cache size, and AD DS by default uses variable cache size.

|Data points to collect|Values
|-|-|
|Maximum acceptable time to warm|10 minutes (600 seconds)
|Database size|2 GB|  
  
|Calculation step|Formula|Result|
|-|-|-|
|Calculate size of database in pages|(2 GB &times; 1024 &times; 1024) = *Size of database in KB*|2,097,152 KB|
|Calculate number of pages in database|2,097,152 KB &divide; 8 KB = *Number of pages*|262,144 pages|
|Calculate IOPS necessary to fully warm the cache|262,144 pages &divide; 600 seconds = *IOPS needed*|437 IOPS|

## Processing

### Evaluating Active Directory processor usage

For most environments, after storage, RAM, and networking are properly tuned as described in the Planning section, managing the amount of processing capacity will be the component that deserves the most attention. There are two challenges in evaluating CPU capacity needed:

- Whether or not the applications in the environment are being well-behaved in a shared services infrastructure, and is discussed in the section titled “Tracking Expensive and Inefficient Searches” in the article Creating More Efficient Microsoft Active Directory-Enabled Applications or migrating away from down-level SAM calls to LDAP calls.  
  
  In larger environments, the reason this is important is that poorly coded applications can drive volatility in CPU load, “steal” an inordinate amount of CPU time from other applications, artificially drive up capacity needs, and unevenly distribute load against the DCs.  
- As AD DS is a distributed environment with a large variety of potential clients, estimating the expense of a “single client” is environmentally subjective due to usage patterns and the type or quantity of applications leveraging AD DS. In short, much like the networking section, for broad applicability, this is better approached from the perspective of evaluating the total capacity needed in the environment.

For existing environments, as storage sizing was discussed previously, the assumption is made that storage is now properly sized and thus the data regarding processor load is valid. To reiterate, it is critical to ensure that the bottleneck in the system is not the performance of the storage. When a bottleneck exists and the processor is waiting, there are idle states that will go away once the bottleneck is removed.  As processor wait states are removed, by definition, CPU utilization increases as it no longer has to wait on the data. Thus, collect performance counters “Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read” and “Process(lsass)\\% Processor Time”. The data in “Process(lsass)\\% Processor Time” will be artificially low if “Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read” exceeds 10 to 15 ms, which is a general threshold that Microsoft support uses for troubleshooting storage-related performance issues. As before, it is recommended that sample intervals be either 15, 30, or 60 minutes. Anything less will generally be too volatile for good measurements; anything greater will smooth out daily peeks excessively.

### Introduction

In order to plan capacity planning for domain controllers, processing power requires the most attention and understanding. When sizing systems to ensure maximum performance, there is always a component that is the bottleneck and in a properly sized Domain Controller this will be the processor.

Similar to the networking section where the demand of the environment is reviewed on a site-by-site basis, the same must be done for the compute capacity demanded. Unlike the networking section, where the available networking technologies far exceed the normal demand, pay more attention to sizing CPU capacity.  As any environment of even moderate size; anything over a few thousand concurrent users can put significant load on the CPU.

Unfortunately, due to the huge variability of client applications that leverage AD, a general estimate of users per CPU is woefully inapplicable to all environments. Specifically, the compute demands are subject to user behavior and application profile. Therefore, each environment needs to be individually sized.

#### Target site behavior profile

As mentioned previously, when planning capacity for an entire site, the goal is to target a design with an *N* + 1 capacity design, such that failure of one system during the peak period will allow for continuation of service at a reasonable level of quality. That means that in an “*N*” scenario, load across all the boxes should be less than 100% (better yet, less than 80%) during the peak periods.

Additionally, if the applications and clients in the site are using best practices for locating domain controllers (that is, using the [DsGetDcName function](http://msdn.microsoft.com/en-us/library/windows/desktop/ms675983(v=vs.85).aspx)), the clients should be relatively evenly distributed with minor transient spikes due to any number of factors.

In the next example, the following assumptions are made:

- Each of the five DCs in the site has four of CPUs.
- Total target CPU usage during business hours is 40% under normal operating conditions (“*N* + 1”) and 60 % otherwise (“*N*”). During non-business hours, the target CPU usage is 80% because backup software and other maintenance are expected to consume all available resources.

![CPU usage chart](media/capacity-planning-considerations-cpu-chart.png)

Analyzing the data in the chart (Processor Information(_Total)\% Processor Utility) for each of the DCs:

- For the most part, the load is relatively evenly distributed which is what would be expected when clients use DC locator and have well written searches. 
- There are a number of five-minute spikes of 10%, with some as large as 20%. Generally, unless they cause the capacity plan target to be exceeded, investigating these is not worthwhile.  
- The peak period for all systems is between about 8:00 AM and 9:15 AM. With the smooth transition from about 5:00 AM through about 5:00 PM, this is generally indicative of the business cycle. The more randomized spikes of CPU usage on a box-by-box scenario between 5:00 PM and 4:00 AM would be outside of the capacity planning concerns.

  >[!NOTE]
  >On a well-managed system, said spikes are might be backup software running, full system antivirus scans, hardware or software inventory, software or patch deployment, and so on. Because they fall outside the peak user business cycle, the targets are not exceeded.

- As each system is about 40% and all systems have the same numbers of CPUs, should one fail or be taken offline, the remaining systems would run at an estimated 53% (System D's 40% load is evenly split and added to System A's and System C’s existing 40% load). For a number of reasons, this linear assumption is NOT perfectly accurate, but provides enough accuracy to gauge.  

  **Alternate scenario –** Two domain controllers running at 40%: One domain controller fails, estimated CPU on the remaining one would be an estimated 80%. This far exceeds the thresholds outlined above for capacity plan and also starts to severely limit the amount of head room for the 10% to 20% seen in the load profile above, which means that the spikes would drive the DC to 90% to 100% during the “*N*” scenario and definitely degrade responsiveness.

### Calculating CPU demands

The “Process\\% Processor Time” performance object counter sums the total amount of time that all of the threads of an application spend on the CPU and divides by the total amount of system time that has passed. The effect of this is that a multi-threaded application on a multi-CPU system can exceed 100% CPU time, and would be interpreted VERY differently than “Processor Information\\% Processor Utility”. In practice the “Process(lsass)\\% Processor Time” can be viewed as the count of CPUs running at 100% that are necessary to support the process’s demands. A value of 200% means that 2 CPUs, each at 100%, are needed to support the full AD DS load. Although a CPU running at 100% capacity is the most cost efficient from the perspective of money spent on CPUs and power and energy consumption, for a number of reasons detailed in Appendix A, better responsiveness on a multi-threaded system occurs when the system is not running at 100%.

To accommodate transient spikes in client load, it is recommended to target a peak period CPU of between 40% and 60% of system capacity. Working with the example above, that would mean that between 3.33 (60% target) and 5 (40% target) CPUs would be needed for the AD DS (lsass process) load. Additional capacity should be added in according to the demands of the base operating system and other agents required (such as antivirus, backup, monitoring, and so on). Although the impact of agents needs to be evaluated on a per environment basis, an estimate of between 5% and 10% of a single CPU can be made. In the current example, this would suggest that between 3.43 (60% target) and 5.1 (40% target) CPUs are necessary during peak periods.

The easiest way to do this is to use the “Stacked Area” view in Windows Reliability and Performance Monitor (perfmon), making sure all of the counters are scaled the same.

Assumptions:

- Goal is to reduce footprint to as few servers as possible. Ideally, one server would carry the load and an additional server added for redundancy (*N* + 1 scenario).

![Processor time chart for lsass process (over all processors)](media/capacity-planning-considerations-proc-time-chart.png)

Knowledge gained from the data in the chart (Process(lsass)\\% Processor Time):

- The business day starts ramping up around 7:00 and decreases at 5:00 PM.
- The peak busiest period is from 9:30 AM to 11:00 AM. 
  > [!NOTE]
  > All performance data is historical. The peak data point at 9:15 indicates the load from 9:00 to 9:15.
- There are spikes before 7:00 AM which could indicate either load from different time zones or background infrastructure activity, such as backups. Because the peak at 9:30 AM exceeds this activity, it is not relevant.
- There are three domain controllers in the site.

At maximum load, lsass consumes about 485% of one CPU, or 4.85 CPUs running at 100%. As per the math earlier, this means the site needs about 12.25 CPUs for AD DS. Add in the above suggestions of 5% to 10% for background processes and that means replacing the server today would need approximately 12.30 to 12.35 CPUs to support the same load. An environmental estimate for growth now needs to be factored in.

### When to tune LDAP weights

There are several scenarios where tuning [LdapSrvWeight](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc957291(v=technet.10)) should be considered. Within the context of capacity planning, this would be done when the application or user loads are not evenly balanced, or the underlying systems are not evenly balanced in terms of capability. Reasons to do so beyond capacity planning are outside of the scope of this article.

There are two common reasons to tune LDAP Weights:

- The PDC emulator is an example that affects every environment for which user or application load behavior is not evenly distributed. As certain tools and actions target the PDC emulator, such as the Group Policy management tools, second attempts in the case of authentication failures, trust establishment, and so on, CPU resources on the PDC emulator may be more heavily demanded than elsewhere in the site.
  - It is only useful to tune this if there is a noticeable difference in CPU utilization in order  to reduce the load on the PDC emulator and increase the load on other domain controllers will allow a more even distribution of load.
  - In this case, set LDAPSrvWeight between 50 and 75 for the PDC emulator.
- Servers with differing counts of CPUs (and speeds) in a site.  For example, say there are two eight-core servers and one four-core server.  The last server has half the processors of the other two servers.  This means that a well distributed client load will increase the average CPU load on the four-core box to roughly twice that of the eight-core boxes.
  - For example, the two eight-core boxes would be running at 40% and the four-core box would be running at 80%.
  - Also, consider the impact of loss of one eight-core box in this scenario, specifically the fact that the four-core box would now be overloaded.

#### Example 1 - PDC

| |Utilization with defaults|New LdapSrvWeight|Estimated new utilization|
|-|-|-|-|
|DC 1 (PDC emulator)|53%|57|40%|
|DC 2|33%|100|40%|
|DC 3|33%|100|40%|

The catch here is that if the PDC emulator role is transferred or seized, particularly to another domain controller in the site, there will be a dramatic increase on the new PDC emulator.

Using the example from the section [Target site behavior profile](#target-site-behavior-profile), an assumption was made that all three domain controllers in the site had four CPUs. What should happen, under normal conditions, if one of the domain controllers had eight CPUs? There would be two domain controllers at 40% utilization and one at 20% utilization. While this is not bad, there is an opportunity to balance the load a little bit better. Leverage LDAP weights to accomplish this.  An example scenario would be:

#### Example 2 - Differing CPU counts

| |Processor Information\\ %&nbsp;Processor Utility(_Total)<br />Utilization with defaults|New LdapSrvWeight|Estimated new utilization|
|-|-|-|-|
|4-CPU DC 1|40|100|30%|
|4-CPU DC 2|40|100|30%|
|8-CPU DC 3|20|200|30%|

Be very careful with these scenarios though. As can be seen above, the math looks really nice and pretty on paper. But throughout this article, planning for an “*N* + 1” scenario is of paramount importance. The impact of one DC going offline must be calculated for every scenario. In the immediately preceding scenario where the load distribution is even, in order to ensure a 60% load during an “*N*” scenario, with the load balanced evenly across all servers, the distribution will be fine as the ratios stay consistent. Looking at the PDC emulator tuning scenario, and in general any scenario where user or application load is unbalanced, the effect is very different:

| |Tuned Utilization|New LdapSrvWeight|Estimated New Utilization|
|-|-|-|-|
|DC 1 (PDC emulator)|40%|85|47%|
|DC 2|40%|100|53%|
|DC 3|40%|100|53%|

### Virtualization considerations for processing

There are two layers of capacity planning that need to be done in a virtualized environment. At the host level, similar to the identification of the business cycle outlined for the domain controller processing previously, thresholds during the peak period need to be identified. Because the underlying principals are the same for a host machine scheduling guest threads on the CPU as for getting AD DS threads on the CPU on a physical machine, the same goal of 40% to 60% on the underlying host are recommended. At the next layer, the guest layer, since the principals of thread scheduling have not changed, the goal within the guest remains in the 40% to 60% range.

In a direct mapped scenario, one guest per host, all the capacity planning done to this point needs to be added to the requirements (RAM, disk, network) of the underlying host operating system. In a shared host scenario, testing indicates that there is 10% impact on the efficiency of the underlying processors. That means if a site needs 10 CPUs at a target of 40%, the recommended amount of virtual CPUs to allocate across all the “*N*” guests would be 11. In a site with a mixed distribution of physical servers and virtual servers, the modifier only applies to the VMs. For example, if a site has an “*N* + 1” scenario, one physical or direct-mapped server with 10 CPUs would be about equivalent to one guest with 11 CPUs on a host, with 11 CPUs reserved for the domain controller.

Throughout the analysis and calculation of the CPU quantities necessary to support AD DS load, the numbers of CPUs that map to what can be purchased in terms physical hardware do not necessarily map cleanly. Virtualization eliminates the need to round up. Virtualization decreases the effort necessary to add compute capacity to a site, given the ease with which a CPU can be added to a VM. It does not eliminate the need to accurately evaluate the compute power needed so that the underlying hardware is available when additional CPUs need to be added to the guests.  As always, remember to plan and monitor for growth in demand.

### Calculation summary example

|System|Peak CPU|
|-|-|-|
|DC 1|120%|
|DC 2|147%|
|Dc 3|218%|
|Total CPU being used|485%|  
  
|Target system(s) count|Total bandwidth (from above)|
|-|-|
|CPUs needed at 40% target|4.85 &divide; .4 = 12.25|

Repeating due to the importance of this point, *remember to plan for growth*. Assuming 50% growth over the next three years, this environment will need 18.375 CPUs (12.25 &times; 1.5) at the three-year mark. An alternate plan would be to review after the first year and add in additional capacity as needed.

### Cross-trust client authentication load for NTLM

#### Evaluating cross-trust client authentication load

Many environments may have one or more domains connected by a trust. An authentication request for an identity in another domain that does not use Kerberos authentication needs to traverse a trust using the domain controller’s secure channel to another domain controller either in the destination domain or the next domain in the path to the destination domain. The number of concurrent calls using the secure channel that a domain controller can make to a domain controller in a trusted domain is controlled by a setting known as **MaxConcurrentAPI**. For domain controllers, ensuring that the secure channel can handle the amount of load is accomplished by one of two approaches: tuning **MaxConcurrentAPI** or, within a forest, creating shortcut trusts. To gauge the volume of traffic across an individual trust, refer to [How to do performance tuning for NTLM authentication by using the MaxConcurrentApi setting](https://support.microsoft.com/kb/2688798).

During data collection, this, as with all the other scenarios, must be collected during the peak busy periods of the day for the data to be useful.

> [!NOTE]
> Intraforest and interforest scenarios may cause the authentication to traverse multiple trusts and each stage would need to be tuned.

#### Planning

There are a number of applications that use NTLM authentication by default, or use it in a certain configuration scenario. Application servers grow in capacity and service an increasing number of active clients. There is also a trend that clients keep sessions open for a limited time and rather reconnect on a regular basis (such as email pull sync). Another common example for high NTLM load is web proxy servers that require authentication for Internet access.

These applications can cause a significant load for NTLM authentication, which can put significant stress on the DCs, especially when users and resources are in different domains.

There are multiple approaches to managing cross-trust load, which in practice are used in conjunction rather than in an exclusive either/or scenario. The possible options are:

- Reduce cross-trust client authentication by locating the services that a user consumes in the same domain that the user is resident in.
- Increase the number of secure-channels available. This is relevant to intraforest and cross-forest traffic and are known as shortcut trusts.
- Tune the default settings for **MaxConcurrentAPI**.

For tuning **MaxConcurrentAPI** on an existing server, the equation is:

> *New_MaxConcurrentApi_setting* &ge; (*semaphore_acquires* + *semaphore_time-outs*) &times; *average_semaphore_hold_time* &divide; *time_collection_length*

For more information, see [KB article 2688798: How to do performance tuning for NTLM authentication by using the MaxConcurrentApi setting](http://support.microsoft.com/kb/2688798).

## Virtualization considerations

None, this is an operating system tuning setting.

### Calculation summary example

|Data type|Value|
|-|-|
|Semaphore Acquires (Minimum)|6,161|
|Semaphore Acquires (Maximum)|6,762|
|Semaphore Timeouts|0|
|Average Semaphore Hold Time|0.012|
|Collection Duration (seconds)|1:11 minutes (71 seconds)|
|Formula (from KB 2688798)|((6762 &ndash; 6161) + 0) &times; 0.012 /|
|Minimum value for **MaxConcurrentAPI**|((6762 &ndash; 6161) + 0) &times; 0.012 &divide; 71 = .101|

For this system for this time period, the default values are acceptable.

## Monitoring for compliance with capacity planning goals

Throughout this article, it has been discussed that planning and scaling go towards utilization targets. Here is a summary chart of the recommended thresholds that must be monitored to ensure the systems are operating within adequate capacity thresholds. Keep in mind that these are not performance thresholds, but capacity planning thresholds. A server operating in excess of these thresholds will work, but is time to start validating that all the applications are well behaved. If said applications are well behaved, it is time to start evaluating hardware upgrades or other configuration changes.

|Category|Performance counter|Interval/Sampling|Target|Warning|
|-|-|-|-|-|
|Processor|Processor Information(_Total)\\% Processor Utility|60 min|40%|60%|
|RAM (Windows Server 2008 R2 oder früher)|Speicher\Verfügbare MB|< 100 MB|N/V|< 100 MB|
|RAM (Windows Server 2012)|Langfristige Memory\Long durchschnittliche Standby Cache Lifetime(s)|30 Minuten|Muss getestet werden|Muss getestet werden|
|Network|Netzwerkschnittstelle (\*) \Bytes/Sek.<br /><br />Netzwerkschnittstelle (\*) \Bytes/Sek.|30 Minuten|40 %|60 %|
|Speicher|Logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Avg Sek./Lesevorgänge<br /><br />Logischer Datenträger ( *\<NTDS-Datenbanklaufwerk\>* ) \Avg Sek./Schreibvorgänge|60-Minuten|10 ms|maximal 15 ms|
|AD-Dienste|Anmeldedienst (\*) \Average Semaphor Haltezeit|60-Minuten|0|1 Sekunde|

## <a name="appendix-a-cpu-sizing-criteria"></a>Anhang A: CPU-Größenkriterium

### <a name="definitions"></a>Definitionen

**Prozessor (Mikroprozessor) –** eine Komponente, liest und programmanweisungen ausführt,  

**CPU –** Zentralprozessor  

**Multicore-Prozessor –** mehrere CPUs in der gleichen integriert Verbindung  

**Multi-CPU –** mehreren CPUs werden nicht auf die gleiche integrierte-Verbindung  

**Logischer Prozessor –** eine logische Computer-Engine aus der Perspektive des Betriebssystems  

Dies schließt mit Hyperthreading, einen Kern auf Multicore-Prozessor sowie über einen Einzelkernprozessor.  

Heutige Serversysteme mehrere Prozessoren, mehrere Multicore-Prozessoren und hyper-threading haben, wird diese Informationen so generalisiert, beide Szenarien behandelt. Daher wird der Begriff logische Prozessor verwendet werden, weil er das Betriebssystem und die Perspektive der Anwendung verfügbare computing-Engine darstellt.

### <a name="thread-level-parallelism"></a>Parallelität auf Threadebene

Jeder Thread ist als unabhängige Aufgabe, da jeder Thread einen eigenen Stapel und Anweisungen enthält. Da AD DS mit mehreren Threads ist und die Anzahl der verfügbaren Threads optimiert werden, mithilfe von kann [anzeigen und Festlegen von LDAP-Richtlinie in Active Directory mit Ntdsutil.exe](http://support.microsoft.com/kb/315071), auch auf mehrere logische Prozessoren skaliert.

### <a name="data-level-parallelism"></a>Datenlevel-Parallelität

Dies umfasst das Freigeben von Daten über mehrere Threads in einem Prozess (im Fall von der AD DS-Prozess, das allein ist) und über mehrere Threads in mehreren Prozessen (Allgemein). Mit der Bedeutung zu stark vereinfachen die Groß-/Kleinschreibung, dies bedeutet, dass alle Änderungen an Daten widergespiegelt werden für alle ausgeführten Threads in den verschiedenen Ebenen des Caches (L1, E2, L3) aller Kerne besagten Threads ausgeführt sowie zum Aktualisieren von gemeinsam genutzten Speicher. Die Leistung kann während Schreibvorgängen beeinträchtigt werden, während die verschiedenen Speicheradressen konsistente hochgefahren werden, bevor die Verarbeitung der Anweisung fortgesetzt werden kann.

### <a name="cpu-speed-vs-multiple-core-considerations"></a>CPU-Geschwindigkeit im Vergleich zu mehreren Kernen Überlegungen

Die allgemeine Faustregel ist schneller logische Prozessoren zu reduzieren, die Dauer einer Reihe von Anweisungen, während mehr logische Prozessoren bedeutet, dass zu verarbeiten, die mehrere Aufgaben gleichzeitig ausgeführt werden können. Diese Faustregeln unterteilen Sie, wie die Szenarien grundsätzlich komplexer mit Überlegungen zum Abrufen von Daten aus freigegebenen Arbeitsspeicher auf die Datenebene Parallelität und den Aufwand für das Verwalten von mehreren Threads gewartet werden. Dies ist auch, warum die Skalierbarkeit in Multicore-Systemen nicht linear ist.

Betrachten Sie die folgenden Analogien in diese Überlegungen: Stellen Sie sich der Autobahn, wobei jeder Thread wird eine einzelne Car, jeden Bereich, wird von einem Kern ausgeführt, und das Tempolimit wird die Geschwindigkeit der Uhr.

1. Wenn nur ein Fahrzeug auf der Autobahn vorhanden ist, ist es unerheblich, ob zwei Bereiche oder Bereiche mit 12 vorhanden sind. Fahrzeugs nur geht so schnell wie das Tempolimit zugelassen wird.
1. Wird davon ausgegangen Sie, dass die Daten, die der Thread benötigt, nicht sofort verfügbar ist. Die Analogie wäre, ein Segment der Straße heruntergefahren wurde. Wenn nur ein Fahrzeug auf der Autobahn vorhanden ist, ist es unerheblich, was das Tempolimit ist erst die Lauffläche erneut geöffnet wird (-Daten aus dem Speicher abgerufen werden).
1. Wenn die Anzahl der Autos erhöhen, erhöht der Aufwand zum Verwalten der Anzahl der Autos. Vergleichen Sie die Benutzeroberfläche zu steuern, und die Menge Aufmerksamkeit erforderlich wenn unterwegs praktisch ist leer (z. B. späten Abend) im Vergleich zu, wenn für der Datenverkehr (z. B. Nachmittag, aber nicht Rush Stunde) hoch ist. Berücksichtigen Sie auch die Menge Aufmerksamkeit erforderlich, wenn auf beiden-aufnahmeschnittstellen Autobahn, es ist nur ein anderer Bereich kümmern, die Treiber wozu, im Vergleich zu den sechs-aufnahmeschnittstellen Autobahn hat, in dem Gedanken, was viele andere Treiber erforderlich machen.
   > [!NOTE]
   > Die Analogie zu den Spitzenzeiten-Szenario wird im nächsten Abschnitt erweitert: Antwortzeit/wie das System Busyness wirkt sich auf Leistung.

Daher werden die Einzelheiten dazu, mehr oder schnellere Prozessoren sehr subjektive zum Verhalten der Anwendung, die im Fall von AD DS ist sehr ökologischen spezifisch und variiert auch zwischen Servern in einer Umgebung. Daher ist die Verweise weiter oben in der Artikel ist nicht investieren in hohem Maße wird sehr präzise und ein Rand von Sicherheit in den Berechnungen enthalten. Wenn Budget gesteuerte Erwerb Entscheidungen treffen zu können, empfiehlt es sich, dass das Optimieren der Nutzung der Prozessoren auf 40 % (oder die gewünschte Anzahl für die Umgebung) zuerst, tritt ein, bevor Sie planen die Anschaffung schnellerer Prozessoren. Die erhöhte Synchronisierung über mehrere Prozessoren verringert den wahren Wert von mehr Prozessoren in der linearen Fortschritt (2&times; die Anzahl der Prozessoren enthält weniger als 2&times; verfügbare zusätzliche rechenleistung).

> [!NOTE]
> Sind hier die relevanten Konzepte Amdahlschem und Gustafsonschem Gesetz.

### <a name="response-timehow-the-system-busyness-impacts-performance"></a>Antwortzeit/Auswirkungen auf das System Busyness Leistung

Queuing Theorie handelt es sich um die mathematische Studie von wartenden Zeilen (Warteschlangen). In der Warteschlange Theorie wird das Gesetz Auslastung durch die Gleichung dargestellt:

*U* k = *B* &divide; *T*

In denen *U* k ist der Auslastungsprozentsatz, *B* die Zeitspanne ausgelastet ist, und *T* ist die Gesamtzeit, die das System festgestellt wurde. In den Kontext des Windows übersetzt, bedeutet dies die Anzahl von 100 Nanosekunden (ns) Intervall-Threads im ausgeführten Zustand geteilt durch wie viele Intervalle von 100 ns im angegebenen Zeitintervall zur Verfügung standen. Dies ist genau die Formel zum Berechnen von % Prozessor Utility (Verweis [Prozessorobjekt](https://docs.microsoft.com/previous-versions/ms804036(v=msdn.10)) und [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/previous-versions/windows/embedded/ms901169(v=msdn.10))).

Queuing Theorie bietet außerdem die Formel: *N* = *U* k &divide; (1 &ndash; *U* k) zum Schätzen der Anzahl der wartenden-Elemente, die basierend auf der Auslastung ( *N* ist die Länge der Warteschlange). Diagrammerstellung für diese über alle Intervalle der Auslastung bietet die folgenden Schätzungen, wie lange die Warteschlange, für den Prozessor abgerufen jede gegebene CPU-Auslastung ist.

![Warteschlangenlänge](media/capacity-planning-considerations-queue-length.png)

Wird festgestellt, dass nach CPU-Auslastung 50 %, durchschnittlich besteht immer eine Wartezeit von einem anderen Element in der Warteschlange, die mit einer deutlich schneller nach etwa 70 % CPU-Auslastung.

An die treibende Analogie, die weiter oben in diesem Abschnitt verwendeten zurückgegeben:

- Die Spitzenzeiten "Nachmittag" würden, hypothetisch auf den Bereich 40 % auf 70 % liegt. Es ist genügend Datenverkehr, sodass die Möglichkeit, alle Lauffläche auszuwählen nicht majorly eingeschränkt ist, und die Wahrscheinlichkeit von einem anderen Treiber, die in die Möglichkeit, während hohe erfordert keine der Ebene der zu eine sichere Lücke zwischen anderen Autos unterwegs "ermitteln".
- Eine bemerken, dass Datenverkehr Spitzenzeiten erreicht, das System Road Auslastung von 100 % erreicht. Ändern von Bereichen kann eine große Herausforderung werden, da Autos so nahe beieinander liegen, dass erhöhte sorgfältig vorgegangen werden zu diesem Zweck.

Aus diesem ist Grund langfristig Mittelwerte für Kapazität konservativ geschätzte 40 % für Head Raum für ungewöhnliche Spitzen in ermöglicht, zu laden, ob als (z. B. mangelhaft programmierte Abfragen, die ein paar Minuten lang ausgeführt) vorübergehende Spitzen oder ungewöhnliche bursts im Allgemeinen Load (am Morgen von der erste Tag nach der ein langes Wochenende).

Die oben genannte Anweisung sieht % Prozessorzeit-Berechnung, die nicht identisch, wie das Gesetz Auslastung etwas eine Vereinfachung für die Beschleunigung des allgemeinen Readers an. Für diese mehr mathematisch strengen:  
- Übersetzen der [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10))
  - *B* = die Anzahl der 100-ns-Intervalle "Idle" Thread an den logischen Prozessor. Die Änderung in der "*X*"-Variable in der [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) Berechnung
  - *T* = Gesamtzahl der 100-ns-Intervalle in einem bestimmten Zeitraum. Die Änderung in der "*Y*"-Variable in der [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) Berechnung.
  - *U* k = den Auslastungsprozentsatz des logischen Prozessors von der "Thread im Leerlauf" oder % Zeit im Leerlauf.  
- Die mathematischen Kenntnisse:
  - *U* k = 1 – % Prozessorzeit
  - Prozessorzeit (%) = 1 – *U* k
  - Prozessorzeit (%) = 1 – *B* / *T*
  - Prozessorzeit (%) = 1 – *X1* – *X0* / *Y1* – *Y0*

### <a name="applying-the-concepts-to-capacity-planning"></a>Anwenden der Konzepte auf die kapazitätsplanung

Die mathematischen Grundlagen von vorherige anfertigen Ermittlung über die Anzahl der logischen Prozessoren in einem System erforderlich sind, erscheinen überwältigend komplexen. Daher ist der Ansatz mit der Größe von der Systems Schwerpunkt auf die Bestimmung der maximalen zielauslastung basierend auf aktuellen laden und die Berechnung der Anzahl der logischen Prozessoren erforderlich, um es abzurufen. Darüber hinaus während mindestgeschwindigkeiten für die logischen Prozessoren einen erheblichen Einfluss auf die Leistung, Cache-Effizienz, Kohärenz arbeitsspeicheranforderungen, Threadplanung und Synchronisierung haben, und Laden aber mit Lastenausgleich Client haben erhebliche Auswirkungen alle auf Leistung, die auf Basis von Servern variieren. Mit den Kosten relativ günstig rechenleistung wird versucht, die zum Analysieren und ermitteln Sie die perfekte Anzahl der CPUs, die erforderlich sind, weitere einer akademischen Übung als es Geschäftswert bereitstellt.

Vierzig Prozent nicht verbindlichen erforderlich ist, sondern eine angemessene starten. Verschiedene Verbraucher von Active Directory erfordern verschiedene Ebenen der Reaktionsfähigkeit. Es gibt möglicherweise Szenarien, in denen Umgebungen zu 80 % oder 90 % ausgelastet als beständige Durchschnitt, ausgeführt werden kann, wie die erhöhte Wartezeiten für den Zugriff auf der Prozessor die Leistung des Clients nicht merklich beeinträchtigt werden. Es ist wichtig, erneut durchlaufen, es gibt viele Bereiche in das System, die sehr viel langsamer als die logischen Prozessoren im System, einschließlich des Zugriffs auf Arbeitsspeicher, den Zugriff auf Datenträger und die Antwort über das Netzwerk übertragen. Alle diese Elemente zusammen optimiert werden müssen. Beispiele:

- Durch Hinzufügen weiterer Prozessoren auf einem System unter 90 %, die Bindung wird wahrscheinlich nicht auf die Leistung erheblich verbessern. Tiefer gehende Analyse des Systems wird wahrscheinlich identifiziert, die viele der Threads, die noch nicht für den Prozessor erhalten werden, da sie auf e/a warten ausführen können.
- Problembehebung für die Bindung möglicherweise die Möglichkeit, die von Threads, die bereits viel Zeit in einem Wartezustand benötigen nicht mehr in einem Wartezustand für e/a und stehen weitere Konkurrenz um CPU-Zeit, dies bedeutet, dass die in den vergangenen 90 % ausgelastet Beispiel geht auf 100 % (weil er nicht höher eingefügt werden kann). Beide Komponenten zusammen optimiert werden müssen.
  > [!NOTE]
  > Prozessor-Information(*)\\% Prozessor Hilfsprogramm kann 100 % mit Systemen, die einen Modus "Turbo" überschreiten.  Dies ist, bei denen die CPU die bewerteten prozessorgeschwindigkeit für einen kurzen Zeitraum überschreitet.  Referenzdokumentation CPU-Hersteller und Beschreibung des Zählers für einen besseren Einblick.  

Überlegungen zum gesamten Nutzung erläutern bringt auch bei den Domänencontrollern für die Konversation als virtualisierte Gäste. [Antwortzeit/Auswirkungen auf das System Busyness Leistung](#response-timehow-the-system-busyness-impacts-performance) bezieht sich auf dem Host und der Gast in einem virtualisierten Szenario. Daher wird dies auf einem Host mit nur einem Gast, einem Domänencontroller (und in der Regel ein System) enthält, in der Nähe der gleichen Leistung, die es auf physischer Hardware funktioniert. Hinzufügen von weiteren Gästen auf die Hosts erhöht die Auslastung des zugrunde liegenden Hosts, erhöht sich natürlich die Wartezeiten für den Zugriff auf die Prozessoren wie zuvor erläutert. Kurz gesagt, muss logische prozessorauslastung auf sowohl dem Host und Gast auf verwaltet werden.

Erweitern die vorherigen Analogien, verlässt der Autobahn als die physische Hardware, das Gastbetriebssystem wird VM mit einem Bus analogized (ein express-Bus, der direkt an das Ziel der Rider geht möchte). Stellen Sie die folgenden vier Szenarien vor:

- Es ist außerhalb der Geschäftszeiten, einem Rider wird auf einem Bus, der fast leer ist und der Bus Ruft auf einer Straße, die auch fast leer ist. Es ist kein Datenverkehr zu bewältigen, die Rider wurde eine schön einfach Fahrt und sind nur so schnell wie bei der Rider stattdessen gesteuert haben. Die Rider des Reisen Zeiten werden immer noch durch das Tempolimit beschränkt.
- Dies ist außerhalb der Geschäftszeiten der Bus ist beinahe leer, aber die meisten Bereiche unterwegs geschlossen werden, damit der Autobahn weiterhin überlastet ist. Die Rider ist auf einem nahezu leeren-Bus auf einer Straße überlastet. Während der Rider in dem Bus, wo befinden sich nicht viele Wettbewerb verfügt, wird der gesamte Fahrtzeit weiterhin vom Rest des Datenverkehrs außerhalb vorgegeben.
- Es ist Spitzenzeiten, damit der Autobahn und Bus ausgelastet sind. Nicht nur die Fahrt dauert länger, sondern ein- und Ausschalten der Bus ist ein Albtraum da Menschen sind die Schulter, Schulter und der Autobahn nicht viel besser. Hinzufügen Weitere Bussen (logische Prozessoren auf dem Gast) bedeutet nicht, sie unterwegs eine leichter anpassen können, oder, dass die Fahrt wird gekürzt werden.
- Das letzte Szenario, ist Obwohl es die Analogie ein wenig dehnen von werden möglicherweise, in dem der Bus ist voll, unterwegs ist jedoch nicht überlastet. Während der Rider weiterhin Probleme beim Abrufen von ein- und Ausschalten der Bus besitzt, wird die Reise effizient sein, nach der Bus unterwegs ist. Dies ist das einzige Szenario, in dem die Gast-Leistung Weitere Bussen (logische Prozessoren auf dem Gast) hinzufügen verbessern kann.

Dort ist es relativ einfach zu extrapolieren, dass es eine Reihe von Szenarien, die zwischen 0 % ausgelastet und die 100 % ausgelastet Zustand der Straße und die 0 % und 100 % genutzt Zustand der Bus, die in unterschiedlichem Umfang Auswirkungen haben.

Die Prinzipale über 40 % anwenden ist CPU-Leistung wie das sinnvolle Ziel für den Host als auch der Gast angemessenen Ausgangspunkt für die ebenfalls als über die Menge der queuing.

## <a name="appendix-b-considerations-regarding-different-processor-speeds-and-the-effect-of-processor-power-management-on-processor-speeds"></a>Anhang B: Überlegungen zur anderen Prozessor beschleunigt und die Auswirkungen der energieverwaltung auf prozessorgeschwindigkeiten

In allen Abschnitten auf Prozessor-Auswahl erfolgt die Annahme, dass der Prozessor mit 100 % der Taktfrequenz die ganze Zeit ausgeführt wird, die die Daten gesammelt werden und die Austausch-Systeme über die gleichen Geschwindigkeit Prozessoren verfügt. Obwohl beide Annahmen in der Praxis wird "false", insbesondere bei Windows Server 2008 R2 und höher, in denen des standardenergiesparplans **ausgeglichen**, die Methodik steht weiterhin, da es sich um die konservativer Ansatz ist. Während die potenzielle Fehlerrate verbessert werden kann, wird nur am Rand des Sicherheit, wenn der Prozessor beschleunigt steigt vergrößert.

- Z. B. in einem Szenario, in dem als 11,25 CPUs gefordert werden, wenn die Prozessoren mit halber Geschwindigkeit ausgeführt haben, wenn die Daten gesammelt wurden, die genaueren Schätzwert möglicherweise 5.125 &divide; 2.
- Es ist unmöglich, um sicherzustellen, dass eine Verdoppelung der Taktfrequenzen doppelt so viel Verarbeitung würde, die für einen bestimmten Zeitraum vorgenommen wird. Dies ist die Zeitspanne, die verbringen die Prozessoren, RAM Warten aufgrund der Tatsache aus, oder andere Systemkomponenten können gleich bleiben. Das Endergebnis ist, dass die schnelleren Prozessoren einen höheren Prozentsatz der Zeit im Leerlauf, beim Warten auf die Daten abgerufen werden aufwenden können. In diesem Fall wird empfohlen, bleiben Sie bei den kleinsten gemeinsamen Nenner wird konservativ, und versuchen, ein potenziell "false" Maß an Genauigkeit zu berechnen, indem ein linearer Vergleich zwischen prozessorgeschwindigkeiten vorausgesetzt.

Auch wenn prozessorgeschwindigkeiten in Ersatzhardware niedriger als die aktuelle Hardware befinden, wäre es sicher ist, erhöhen Sie die Schätzung von Prozessoren, die von einem angemessenen Zeitraum benötigt. Es wird z. B. berechnet, dass 10 Prozessoren sind erforderlich, um die Last auf einer Website aufzufangen und die aktuelle Prozessoren mit 3.3 Ghz ausgeführt werden und Ersatz-Prozessoren mit 2,6 Ghz und laufen, dies ist eine 21 % Verringerung der Geschwindigkeit. In diesem Fall wäre 12 Prozessoren die empfohlene Menge.

Dies bedeutet, dass diese Variabilität der Capacity Management-Prozessor Auslastung Ziele nicht geändert werden. Wie Prozessortaktfrequenzen dynamisch basierend auf der Auslastung des laufenden Systems höherem Aufkommen gefordert, angepasst werden, wird ein Szenario generiert, für die die CPU mehr Zeit in einem Format Geschwindigkeit Zustand, benötigt das ultimative Ziel bei 40 % Auslastung in einer 100 % sein vornehmen Clock Geschwindigkeit Zustand Spitzenzeiten an. Alles, was kleiner als die einsparungen beim Energieverbrauch generiert wird, wie die CPU-Geschwindigkeiten während deaktiviert Spitzenzeiten Szenarien gedrosselt werden.

> [!NOTE]
> Eine Option wäre die energieverwaltung auf den Prozessoren zu deaktivieren (Festlegen des Energiesparplans auf **hohe Leistung**) während Daten gesammelt werden. Die erhalten würde einer genaueren Darstellung der CPU-Nutzung auf dem Zielserver.

Um Schätzungen für andere Zielprozessoren anzupassen, verwendet es sicher sein, mit Ausnahme von anderen Engpässe im System oben beschriebenen, davon ausgehen, dass eine Verdoppelung prozessorgeschwindigkeiten der Verarbeitungsaufwand verdoppelt, die ausgeführt werden konnte.  Derzeit ist die interne Architektur von Prozessoren unterschiedlich genug Prozessoren, die eine sichere Methode zum Messen der Auswirkungen der verschiedene Prozessoren als die Daten entnommen wurde den SPECint_rate2006-Vergleichstest aus Standard Leistungsbewertung nutzen Corporation.

1. Finden Sie die Ergebnisse SPECint_rate2006 für den Prozessor, der verwendet werden, und planen, die verwendet werden.
    1. Wählen Sie auf der Website der standardmäßigen Leistung Evaluation Corporation **Ergebnisse**, markieren Sie **CPU2006**, und wählen Sie **alle SPECint_rate2006 Ergebnisse der Suche nach**.
    1. Klicken Sie unter **einfache Anforderung**, geben Sie die Suchkriterien für die Zielprozessor, z. B. **Prozessor Übereinstimmungen E5-2630 (Baselinetarget)** und **Prozessor Übereinstimmungen E5-2650 (Baseline)** .
    1. Suchen Sie die Server- und prozessoranforderungen Konfiguration verwendet werden (oder etwas zu schließen, wenn eine genaue Übereinstimmung nicht verfügbar ist), und notieren Sie den Wert in der **Ergebnis** und **# Kerne** Spalten.
1. Um zu bestimmen, der Modifizierer, verwenden Sie die folgende Gleichung:
   >((*Plattform pro Kern Bewertung Zielwert*) &times; (*MHz pro Kern der Baseline-Plattform*)) &divide; ((*Baseline pro Kern Ergebniswert*) &times; (*MHz pro Kern der Zielplattform*))  

    Verwenden das obige Beispiel an:
   >(35.83 &times; 2000) &divide; (33.75 &times; 2300) = 0.92
1. Multiplizieren Sie die geschätzte Anzahl von Prozessoren, mit dem Modifizierer.  Im obigen Fall so wechseln aus der E5-2650 Prozessor an den Prozessor E5-2630 Multiplizieren Sie die berechneten als 11,25 CPUs &times; 0.92 = 10,35 Prozessoren, die erforderlich sind.

## <a name="appendix-c-fundamentals-regarding-the-operating-system-interacting-with-storage"></a>Anhang C: Grundlagen in Bezug auf das Betriebssystem, die Interaktion mit storage

Die Theorie warteschlangenbegriffe beschrieben, die in [Antwortzeit/Auswirkungen auf das System Busyness Leistung](#response-timehow-the-system-busyness-impacts-performance) gelten auch für Storage. Wenn eine vertraute wie die Betriebssystemhandles e/a-erforderlich, diese Konzepte angewendet wird. In der Microsoft Windows ausgeführt wird wird eine Warteschlange, um die e/a-Anforderungen für jeden physischen Datenträger erstellt. Allerdings muss eine Erläuterung, auf dem physischen Datenträger vorgenommen werden. Array-Controllern und SANs stellen Aggregationen von Spindeln für das Betriebssystem als einzelne physische Datenträger. Darüber hinaus können Array-Controllern und SANs aggregieren mehrere Datenträger in einem Array Satz und teilen Sie dann dieses Array festgelegt in mehrere "Partitionen", die wiederum auf das Betriebssystem als mehrere physische Datenträger (Ref. Abbildung) erhält.

![Spindles blockieren](media/capacity-planning-considerations-block-spindles.png)  

In dieser Abbildung sind die zwei Spindles gespiegelt und Teilen in logische Bereiche für die datenspeicherung ("Data-1" und "Data 2"). Diese logische Bereiche werden vom Betriebssystem als separaten physischen Datenträgern angezeigt.

Obwohl dies sehr verwirrend sein kann, wird die folgende Terminologie in diesem Anhang verwendet, um den verschiedenen Entitäten zu identifizieren:

- **Spindel –** des Geräts, die physisch auf dem Server installiert ist.
- **Array-** eine Auflistung von Spindeln aggregierte, vom Netzwerkcontroller.
- **Array-Partitionen –** eine Partitionierung des aggregierten Arrays
- **LUN-** ein Array, das zum Verweisen auf SANs
- **Datenträger –** wie das Betriebssystem auf einem einzelnen physischen Datenträger berücksichtigt.
- **Partitionen –** eine logische Partitionierung des was das Betriebssystem als ein physischer Datenträger wahrnimmt.

### <a name="operating-system-architecture-considerations"></a>Überlegungen zum Betriebssystem-Architektur

Eine erste In/First Out (FIFO) e/a-Warteschlange für jeden Datenträger, der beobachtet wird, erstellt das Betriebssystem; Dieser Datenträger kann eine Spindel, ein Array oder eine Partition Array repräsentiert. Aus Sicht des Betriebssystems in Bezug auf das Behandeln von e/a-Warteschlangen die weitere aktive umso besser. Wie eine FIFO-Warteschlange serialisiert wird, wird angezeigt, was bedeutet, dass alle e/a ausgestellt für das Speichersubsystem in der Reihenfolge verarbeitet werden müssen die Anforderung. Durch das Korrelieren von jedem Datenträger, die vom Betriebssystem mit einem Spindel/Array beobachtet, führt das Betriebssystem nun eine e/a-Warteschlange für jede eindeutige Gruppe von Datenträgern, und eliminieren Konflikte knappe e/a-Ressourcen auf Datenträgern und zum Isolieren von e/a-Anforderung mit einem einzelnen der Datenträger. Eine Ausnahme Windows Server 2008 führt das Konzept der e/a-Priorisierung und Anwendungen, die dafür ausgelegt, die Priorität "Niedrig" zu verwenden, aus diesen normalen Auftrag gehören, und setzen Sie sich zurück. Anwendungen nicht speziell codiert, nutzen Sie die Priorität "Niedrig" standardmäßig "Normal".

### <a name="introducing-simple-storage-subsystems"></a>Einführung in einfachen Speichersubsysteme

Beginnend mit einem einfachen Beispiel (eine einzelne Festplatte innerhalb eines Computers) wird eine Komponente von Analyse zugewiesen. In der detaillierten in den Hauptspeicher-subsystemkomponenten, besteht aus das System:

- **1 –** 10.000 u/Min extrem schnelle SCSI-HD (verfügt über eine 20 MB/s-Übertragungsrate der extrem schnelle SCSI)
- **1 –** SCSI-Bus (die Kabel)
- **1 –** extrem schnelle SCSI-Adapter
- **1 –** 32-Bit-33 MHz PCI-Bus

Nachdem die Komponenten identifiziert wurden, kann eine Vorstellung davon, wie viele Daten im System übertragen werden können oder wie viele e/a verarbeitet werden können, berechnet werden. Beachten Sie, dass die Menge an e/a und der Menge der Daten, die das System transitrouting korreliert werden, aber nicht identisch. Diese Korrelation, hängt davon ab, ob der Datenträger-e/a zufällig oder sequenziell ist und die Blockgröße. (Alle Daten auf den Datenträger als Block geschrieben, aber unterschiedliche Anwendungen, die mit verschiedenen Blockgrößen.) Auf Basis von Komponente:

- **Die Festplatte –** die durchschnittliche 10.000-RPM-Festplatte verfügt über ein 7-Millisekunden (ms) zu suchen, Time und einen Zugriff auf 3 ms. Seek-Zeit ist die durchschnittliche Zeit, die die Lese-/schreibkopfes auf die Festplatte an einem Speicherort zu verschieben. Zeitpunkt des Zugriffs ist die durchschnittliche Länge der Zeitaufwand zum Lesen oder schreiben die Daten auf den Datenträger, nachdem der Hauptknoten am richtigen Speicherort ist. Die durchschnittliche Zeit zum Lesen von eines eindeutigen Blocks von Daten in einem 10.000 u/Min HD bildet daher eine Suche und ein Zugriff, insgesamt etwa 10 ms (oder.010 Sekunden) pro Block von Daten.

  Wenn alle Datenträgerzugriff Bewegung des Anfangswerts an einem neuen Speicherort auf dem Datenträger erforderlich sind, das Verhalten der Lese-/Schreibzugriff bezeichnet man als "zufällige". Daher Wenn alle e/as zufällig ist, eine 10.000 u/Min HD kann behandeln ungefähr 100 e/a pro Sekunde (IOPS) (die Formel lautet 1000 ms pro Sekunde, dividiert durch 10 ms pro e/A- oder 1000/10 = 100 IOPS).

  Auch wenn alle e/as aus benachbarten Sektoren auf den HD auftritt, wird dies als sequenzieller e/a bezeichnet. Sequenzielle e/as ist ohne Suchzeit, denn wenn die erste e/a abgeschlossen ist, die Lese-/schreibkopfes am Anfang, in der nächste Block von Daten auf den HD gespeichert ist. Daher ist eine 10.000 u/Min HD ungefähr 333 verarbeiten kann e/a pro Sekunde (1000 ms pro Sekunde, dividiert durch 3 ms pro e/a).

  >[!NOTE]
  >In diesem Beispiel wird nicht den Datenträgercache angezeigt, in dem die Daten ein Zylinder in der Regel enthalten ist. In diesem Fall 10 ms werden auf der ersten e/a benötigt, und das Laufwerk liest den gesamten Zylinder. Alle anderen sequenzieller e/a wird aus dem Cache erfüllt werden. Daher können in Datenträgercaches sequenziellen e/a-Leistung verbessern.
  
  Bisher wurde die Übertragungsrate der Festplatte nicht relevant. Gibt an, ob die Festplatte 20 ist MBIT/s Ultra-Wide oder ein Ultra3 160 MB/s, die tatsächliche Speichergröße des IOPS-Wert kann der behandelt werden, indem die 10.000 u/Min HD ist ~ 100 zufälligen oder ~ 300 sequenzieller e/a. Als Block, die Ändern der Größe der Anwendung, die auf das Laufwerk schreiben basierend, unterscheidet sich die Menge der Daten, die pro e/a abgerufen werden. Wenn Blockgröße von 8 KB ist, werden 100 e/a-Vorgänge beispielsweise aus lesen oder Schreiben auf die Festplatte insgesamt 800 KB. Allerdings ist die Blockgröße 32 KB, 100 e/a wird Lese-/Schreibzugriff 3.200 KB (3,2 MB) auf die Festplatte geschrieben. Solange die SCSI-Übertragungsrate über die Gesamtmenge der übertragenen Daten ist, werden erste eine "schnellere" Übertragung Rate Laufwerk "nothing" erhalten. Finden Sie unter den folgenden Tabellen für den Vergleich.

  | |7200 u/Min 9ms Suchvorgang auf 4ms zugreifen.|10.000 u/Min 7ms Suchvorgang auf 3ms zugreifen.|Mit 15.000 u/Min 4ms Seek, Zugriff auf 2 ms
  |-|-|-|-|
  |Wahlfreier e/as|80|100|150|
  |Sequenzieller e/a|250|300|500|  
  
  |Laufwerk mit 10.000 u/Min|Blockgröße von 8 KB (Active Directory Jet)|
  |-|-|
  |Wahlfreier e/as|800 KB/s|
  |Sequenzieller e/a|2400 KB/s|

- **SCSI-Rückwandplatine (Bus) –** Verständnis wie "SCSI-Rückgrat (Bus)", oder in diesem Szenario das Flachbandkabel hängt die Auswirkungen auf Durchsatz des Speichersubsystems Kenntnisse der Blockgröße. Im Wesentlichen die Frage wäre, wie viel e/a das Handle der Bus ist die e/a in 8-KB-Blöcken können? In diesem Szenario ist der SCSI-Bus an 20 MBIT/s oder 20480 KB/Sekunde. 20480 KB/Sekunde, dividiert durch 8 KB-Blöcken gibt maximal etwa 2500 IOPS, die von den SCSI-Bus unterstützt werden.

  >[!NOTE]
  >Die Abbildungen in der folgenden Tabelle stellen ein Beispiel dar. Die meisten angefügten Speichergeräte verwenden derzeit PCI Express, die viel höheren Durchsatz bereitstellt.  
  
  |E/a von SCSI-Bus pro Blockgröße unterstützt|Blockgröße von 2 KB|Blockgröße von 8 KB (AD Jet) (SQL Server 7.0/SQL Server 2000)
  |-|-|-|
  |20 MB/s|10,000|2,500|
  |40 MB/s|20,000|5,000|
  |128 MB/s|65,536|16,384|
  |320 MB/s|160,000|40,000|

  Wie aus dem Diagramm, in dem Szenario, das angezeigt wird, bestimmt werden kann, unabhängig davon, welche die Verwendung der Bus nie mit einem Engpass führen, werden als die Spindel Höchstwert ist 100 e/a, unter einer der oben genannten Schwellenwerte.

  >[!NOTE]
  >Dies setzt voraus, dass der SCSI-Bus auf 100 % effizient ist.
  
- **SCSI-Adapter –** zum Bestimmen der Menge an e/a, die diese behandeln können, müssen den Angaben des Herstellers überprüft werden. Weiterleiten von e/a-Anforderungen an das entsprechende Gerät Verarbeitung erfordert, daher ist die Menge an e/a, die verarbeitet werden können abhängig von der SCSI-Adapter (oder Array-Controller) Prozessor.

  In diesem Beispiel davon ausgegangen, 1.000 e/a-kann verarbeitet werden erfolgen.

- **PCI-Bus –** Dies ist eine häufig übersehene-Komponente. In diesem Beispiel wird dies nicht der Engpass sein. wie Sie Systeme zentral hochskalieren, kann es jedoch als Engpass erweisen. Zu Referenzzwecken ein 32-Bit-PCI-Bus auf 33Mhz können theoretisch Übertragung 133 MB/s der Daten. Es folgt die Gleichung:  
  > 32-Bit &divide; 8 Bits pro Byte &times; 33 MHz = 133 MB/s.  

  Beachten Sie, dass die theoretische Beschränkung; in der Praxis ist nur etwa 50 % des maximal tatsächlich erreicht, obwohl in bestimmten Szenarien Burst 75 % Effizienz für einen kurzen Zeitraum abgerufen werden kann.

  Ein 66 Mhz 64-Bit-PCI-Bus kann ein theoretisches Maximum von unterstützen (64 Bit &divide; 8 Bits pro Byte &times; 66 Mhz) 528 MB/Sek. zusätzlich = jedem anderen Gerät (z. B. die Netzwerkadapter, zweite SCSI-Controller und So weiter), reduziert die verfügbare Bandbreite die Bandbreite wird freigegeben und die Geräte werden für die begrenzten Ressourcen konkurrieren.

Nach der Analyse der Komponenten von diesem Speichersubsystem ist die Spindel der einschränkende Faktor hinsichtlich der Menge des e/a, die angefordert werden kann, und daher die Menge der Daten, die das System übertragen werden können. Dabei in einem AD DS-Szenario handelt es sich 100 zufälligen e/a pro Sekunde in Schritten von 8 KB, für einen Zeitraum von 800 KB pro Sekunde bei den Zugriff auf die Jet-Datenbank. Alternativ würde der maximale Durchsatz für eine Spindel, die ausschließlich zugeordnet wird, um Protokolldateien beeinträchtigt, werden die folgenden Einschränkungen: 300 sequenzieller e/a pro Sekunde in Schritten von 8 KB für insgesamt 2400 KB (2,4 MB) pro Sekunde.

Nun wird veranschaulicht, dass analysiert eine einfache Konfiguration, in der folgende Tabelle, in dem der Engpass auftritt, wie die Komponenten im Speichersubsystem, geändert oder hinzugefügt werden.

|Hinweise|Engpass-Analyse|Datenträger|Bus|Adapter|PCI-Bus|
|-|-|-|-|-|-|
|Dies ist die Konfiguration des Domänencontrollers nach dem Hinzufügen eines zweiten Datenträgers. Die Datenträgerkonfiguration stellt den Engpass bei 800 KB/s dar.|1 Datenträger hinzufügen (insgesamt = 2)<br /><br />E/a ist zufällig<br /><br />Blockgröße von 4 KB<br /><br />HD MIT 10.000 U/MIN|200 e/a gesamt<br />800 KB/s insgesamt.| | | |
|Nach dem Hinzufügen von 7-Datenträger, stellt die Datenträgerkonfiguration immer noch den Engpass bei 3200 KB/s dar.|**Hinzufügen von 7-Datenträgern (insgesamt = 8)**  <br /><br />E/a ist zufällig<br /><br />Blockgröße von 4 KB<br /><br />HD MIT 10.000 U/MIN|800 e/as gesamt.<br />3200 KB/s insgesamt| | | |
|Nach dem Ändern der i/o, sequenziell, wird der Netzwerkadapter zu einem Engpass, da es auf 1000 IOPS beschränkt ist.|Hinzufügen von 7-Datenträgern (insgesamt = 8)<br /><br />**E/a ist sequenziell**<br /><br />Blockgröße von 4 KB<br /><br />HD MIT 10.000 U/MIN| | |2400 e/a-s kann gelesen/auf dem Datenträger, Controller, die auf 1000 IOPS beschränkt geschrieben werden| |
|Ersetzen Sie den Netzwerkadapter mit einem SCSI-Adapter, der 10.000 IOPS-Wert unterstützt, und gibt Sie der Engpass an der Datenträgerkonfiguration zurück.|Hinzufügen von 7-Datenträgern (insgesamt = 8)<br /><br />E/a ist zufällig<br /><br />Blockgröße von 4 KB<br /><br />HD MIT 10.000 U/MIN<br /><br />**Aktualisieren von SCSI-Adapter (jetzt unterstützt 10.000 e/a)**|800 e/as gesamt.<br />3\.200 KB/s insgesamt| | | |
|Nach dem Erhöhen der Blockgröße auf 32 KB, wird der Bus zu einem Engpass, da sie nur 20 MBIT/s unterstützt.|Hinzufügen von 7-Datenträgern (insgesamt = 8)<br /><br />E/a ist zufällig<br /><br />**Blockgröße von 32 KB**<br /><br />HD MIT 10.000 U/MIN| |800 e/as gesamt. 25,600 KB/s (25 MB/s) kann auf dem Datenträger gelesen/geschrieben.<br /><br />Der Bus unterstützt nur 20 MBIT/s| | |
|Nach dem Aktualisieren des Bus und weitere Datenträger hinzugefügt haben, bleibt der Datenträger der Engpass.|**Hinzufügen von 13 Datenträgern (insgesamt = 14)**<br /><br />Hinzufügen des zweiten SCSI-Adapter mit 14 Datenträgern<br /><br />E/a ist zufällig<br /><br />Blockgröße von 4 KB<br /><br />HD MIT 10.000 U/MIN<br /><br />**Ein Upgrade auf 320 MB/s-SCSI-bus**|2800 I/Os<br /><br />11,200 KB/s (10.9 MB/s)| | | |
|Nach dem Ändern der i/o, sequenziell, bleibt der Datenträger der Engpass.|Hinzufügen von 13 Datenträgern (insgesamt = 14)<br /><br />Hinzufügen des zweiten SCSI-Adapter mit 14 Datenträgern<br /><br />**E/a ist sequenziell**<br /><br />Blockgröße von 4 KB<br /><br />HD MIT 10.000 U/MIN<br /><br />Ein Upgrade auf 320 MB/s-SCSI-bus|8,400 e/a<br /><br />33,600 KB\s<br /><br />(32,8 MB\s)| | | |
|Nach dem Hinzufügen von schneller Festplatten, bleibt der Datenträger der Engpass.|Hinzufügen von 13 Datenträgern (insgesamt = 14)<br /><br />Hinzufügen des zweiten SCSI-Adapter mit 14 Datenträgern<br /><br />E/a ist sequenziell<br /><br />Blockgröße von 4 KB<br /><br />**HD MIT 15.000 U/MIN**<br /><br />Ein Upgrade auf 320 MB/s-SCSI-bus|14.000 e/a<br /><br />56.000 KB/s<br /><br />(54.7 MB/s)| | | |
|Nach dem Erhöhen der Blockgröße auf 32 KB, wird der PCI-Bus zu einem Engpass.|Hinzufügen von 13 Datenträgern (insgesamt = 14)<br /><br />Hinzufügen des zweiten SCSI-Adapter mit 14 Datenträgern<br /><br />E/a ist sequenziell<br /><br />**Blockgröße von 32 KB**<br /><br />HD MIT 15.000 U/MIN<br /><br />Ein Upgrade auf 320 MB/s-SCSI-bus| | | |14.000 e/a<br /><br />448,000 KB/s<br /><br />(437 MB/s) ist das Limit für die Lese-/Schreibzugriff auf die Spindel.<br /><br />PCI-Bus unterstützt ein theoretisches Maximum von 133 MB/s (75 % bestenfalls effizient).|

### <a name="introducing-raid"></a>Einführung in die RAID

Die Art des Speichersubsystems ändert sich nicht erheblich, wenn ein Arraycontroller eingeführt wird; Es wird nur den SCSI-Adapter, der Berechnung der Prüfsumme ersetzt. Was ändert, sind die Kosten für das Lesen und Schreiben von Daten auf den Datenträger bei Verwendung von den verschiedenen Ebenen von Arrays (z. B. RAID 0, RAID 1 oder RAID-5).

RAID 0 werden die Daten in allen verteilt, die die Datenträger in das RAID festgelegt. Dies bedeutet, dass während einer Lese- oder einen Schreibvorgang, ein Teil der Daten mithilfe von Pull aus oder per Push an jeden Datenträger und erhöhen die Menge der Daten, die das System im gleichen Zeitraum übertragen können. Daher können in einer Sekunde, für die einzelnen Spindel (erneut unter der Annahme Laufwerken mit 10.000 u/min) 100 e/a-Vorgänge ausgeführt werden. Die Gesamtmenge der e/a, die unterstützt werden können, ist N Spindeln multipliziert mit 100 e/a pro Sekunde pro Spindel (ergibt 100 * N e/a pro Sekunde).

![Laufwerk "d: logische"](media/capacity-planning-considerations-logical-d-drive.png)

In einem RAID 1 werden die Daten (doppelt) in ein Paar von Spindeln für Redundanz gespiegelt. Wenn ein e/a-Lesevorgang ausgeführt wird, können daher Daten aus der Spindles in der Menge gelesen werden. Dadurch werden effektiv die e/a-Kapazität über beide Festplatten verfügbar während eines Lesevorgangs. Der Nachteil ist, dass Vorgänge erhalten keine Leistungsvorteile in einem RAID 1 schreiben. Dies ist, da dieselben Daten auf beide Festplatten aus Gründen der Redundanz geschrieben werden müssen. Obwohl es nicht mehr, akzeptiert, wie das Schreiben von Daten gleichzeitig auf beide Spindeln, tritt auf, weil beide Spindeln duplizieren die Daten belegt sind, wird verhindert, dass ein e/a-Schreibvorgang im Wesentlichen zwei Lesevorgängen auftritt. Also lesen Sie alle schreiben e/a-Kosten zwei e/a. Anhand dieser Informationen, um die Gesamtanzahl der e/a-Vorgänge zu bestimmen, die auftreten, kann eine Formel erstellt werden:  

> *Lese-e/a* + 2 &times; *schreiben e/a-*  = *verbraucht verfügbaren Datenträger-e/a gesamt*  

Wenn das Verhältnis von Lesevorgängen zu schreibt, und die Anzahl der Spindeln bekannt sind, wird die folgende Formel abgeleitet werden kann, aus der oben aufgeführten Gleichung die maximalen e/a zu identifizieren, die vom Array unterstützt werden können:  

> *Maximale Anzahl IOPS pro Spindel* &times; 2 Spindeln &times; [( *% Lesevorgänge* +  *% Schreibvorgänge*) &divide; ( *% Lesevorgänge* + 2 &times; *% Schreibvorgänge*)] = *gesamt-IOPS*

RAID 1 + 0, verhält sich genau wie RAID 1 in Bezug auf die Kosten für Lese- und Schreibvorgänge. Die e/a wird jedoch nun über jede gespiegelter Satz verteilt werden. Wenn  

> *Maximale Anzahl IOPS pro Spindel* &times; 2 Spindeln &times; [( *% Lesevorgänge* +  *% Schreibvorgänge*) &divide; ( *% Lesevorgänge* + 2 &times; *% Schreibvorgänge*)] = *e/a gesamt*  

in einer RAID 1-Gruppe, wenn eine Multiplizität (*N*) von RAID-1, die Gruppen verteilt werden, die e/a gesamt, die verarbeitet werden können, wird N &times; e/a pro RAID 1-Satz:  

> *N* &times; {*maximalen IOPS pro Spindel* &times; 2 Spindeln &times; [( *% Lesevorgänge* +  *% Schreibvorgänge*) &divide; ( *% Lesevorgänge* + 2 &times; *% Schreibvorgänge*)]} = *gesamt-IOPS*

Im RAID-5, auch bezeichnet als *N* + 1 RAID, die Daten werden über *N* Spindeln und Parität Informationen werden in der Spindel "+ 1" geschrieben. RAID 5 ist jedoch mehr Aufwand beim Durchführen einer Schreibvorgänge als RAID 1 oder 1 + 0. RAID 5 führt den folgenden Prozess jedes Mal, wenn eine Schreibvorgänge in das Array gesendet wird:

1. Lesen Sie die alten Daten
1. Lesen Sie die alte Parität
1. Schreiben Sie die neuen Daten
1. Schreiben Sie die neue Parität

Wie alle e/a-Anforderung, die vom Betriebssystem auf den Arraycontroller übermittelt wird auf den Abschluss vier e/a-Vorgänge erforderlich ist, dauern Schreibanforderungen übermittelt vier Mal so viel Zeit in Anspruch als ein einzelnen e/a zu lesen. Eine Formel, um die e/a-Anforderungen aus der Sicht des Betriebssystems an, die von der Spindeln übersetzen abgeleitet werden:  

> *Lesen die e/a* + 4 &times; *schreiben e/a* = *e/a gesamt*  

Auf ähnliche Weise in einem RAID 1-Satz, kann Wenn das Verhältnis von Lese-, Schreib- und die Anzahl der Spindeln bekannt sind, die folgende Gleichung abgeleitet werden aus der oben aufgeführten Gleichung die maximalen e/a zu identifizieren, die vom Array (Beachten Sie, das gesamte Anzahl an Spindeln nicht unterstützt werden können e der "Drive" gehen verloren, Parität):  

> *IOPS pro Spindel* &times; (*Spindeln* – 1) &times; [( *% Lesevorgänge* +  *% Schreibvorgänge*) &divide; ( *% Lesevorgänge* + 4 &times; *% Schreibvorgänge*)] = *gesamt-IOPS*

### <a name="introducing-sans"></a>Einführung in die SANs

Erweitern die Komplexität des Speichersubsystems, wenn eine SAN in der Umgebung eingeführt wird, die grundlegenden Prinzipien nicht ändern, muss berücksichtigt werden jedoch die e/a-Verhalten für alle Systeme mit dem SAN verbunden. Da einer der wichtigsten Vorteile in die Verwendung eines SANs ein zusätzliche Maß an Redundanz über intern oder extern zugeordnetem Speicher ist, muss die kapazitätsplanung nun Konto Fault Tolerance Anforderungen berücksichtigen. Darüber hinaus werden weitere Komponenten eingeführt, die ausgewertet werden müssen. Unterteilen eines SAN in die Komponenten aus:

- SCSI oder Fibre Channel-Festplatte
- Storage-Einheit-Kanal-Rückwandplatine
- Speichereinheiten
- Speicher-Controllermodul
- SAN-Switches
- HBA(s)
- PCI-bus

Wenn Sie ein System für Redundanz zu entwerfen, sind zusätzliche Komponenten eingeschlossen, um das Potenzial des Fehlers zu ermöglichen. Es ist sehr wichtig, wenn zur kapazitätsplanung, die redundante Komponente den verfügbaren Ressourcen ausgeschlossen werden sollen. Beispielsweise ist ein Controllermodul, das die e/a-Kapazität verfügt das SAN auf beiden controllermodulen, alles, die was für e/a-Gesamtdurchsatz im System verfügbar verwendet werden soll. Dies ist darauf zurückzuführen, dass wenn ein Controller ausfällt, die gesamte e/a-Last gefordert, die für alle verbundenen Systeme wird von der verbleibende Controller verarbeitet werden muss. Alle Aspekte der kapazitätsplanung für die Spitzenauslastungszeiten Vorgang abgeschlossen ist, redundante Komponenten nicht einkalkuliert werden die verfügbaren Ressourcen und geplanten spitzenauslastung sollte maximal 80 % Sättigung des Systems (um Spitzen oder ungewöhnliche System zu berücksichtigen Verhalten). Auf ähnliche Weise sollte die redundante SAN-Switches, speichereinheit und Spindeln nicht in der e/a-Berechnungen berücksichtigt werden.

Wenn das Verhalten von der Festplatte SCSI oder Fibre Channel zu analysieren, wird die Methode der Analyse des Verhaltens, wie zuvor nicht geändert werden. Es gibt, zwar bestimmte vor- und Nachteile jedes Protokoll ist der einschränkende Faktor pro Datenträger den mechanischen Einschränkung der Festplatte.

Analysieren den Kanal für die speichereinheit ist genau identisch mit die verfügbaren Ressourcen auf dem SCSI-Bus oder Bandbreite (z. B. 20 MBIT/s) geteilt durch die Blockgröße (z. B. 8 KB) berechnet. In denen dies aus dem vorherigen einfaches Beispiel stellt eine Abweichung wird die Aggregation von mehreren Kanälen. Z. B. wenn 6 Kanäle, ist jeweils die Unterstützung von 20 MBIT/s maximale Übertragungsrate an, die Gesamtmenge der e/a und Daten übertragen, die verfügbar ist 100 MBIT/s (Dies ist richtig ist, ist keine 120 MB/s). In diesem Fall Fehlertoleranz ist eine wichtige bei der Berechnung der Ausfall eines gesamten Kanals, das System nur Links mit 5 funktionsfähigen Kanäle. Daher sollte damit leistungserwartungen Ausfall fortgesetzt werden, der Gesamtdurchsatz aller Kanäle Speicher nicht überschreiten 100 MBIT/s (Dies setzt voraus, dass die Auslastung und Fehlertoleranz auf allen Kanälen gleichmäßig verteilt sind). Durch das Aktivieren dieser in ein e/a-Profil ist abhängig von dem Verhalten der Anwendung. Im Fall von Active Directory Jet-e/a, würde dies eine korrelieren mit ca. 12.500 e/a pro Sekunde (100 MBIT/s &divide; 8 KB pro e/a).

Als Nächstes ist die Abrufen von den Angaben des Herstellers für die controllermodule erforderlich, um einen Überblick über den Durchsatz zu erhalten, die jedes Modul unterstützen kann. In diesem Beispiel hat das SAN beiden controllermodule, 7.500-Support-e/a jeder. Der Gesamtdurchsatz des Systems möglicherweise 15.000 IOPS-Wert, wenn Redundanz nicht gewünscht ist. Bei der Berechnung maximalen Durchsatzes bei einem Fehler, ist die Einschränkung der Durchsatz von einem Controller oder 7.500 IOPS. Dieser Schwellenwert liegt deutlich unterhalb der 12.500 maximale IOPS (vorausgesetzt, Blockgröße von 4 KB), die von allen die Speicher-Kanäle unterstützt werden kann, und daher befindet sich der Engpass bei der Analyse. Die gewünschte maximale e/a geplant werden wäre immer noch für Planungszwecke 10.400 e/a.

Wenn die Daten das Controllermodul beendet wird, es eine Fibre Channel-Verbindung mit 1 GBIT/s (oder 1 Gigabit pro Sekunde) bewertet denselben Übergang übergeht. Um dies mit den anderen Metriken zu korrelieren, 1 GBIT/s, wandelt Sie in 128 MB/s (1 GBIT/s &divide; 8 Bits/Byte). Da dies über die gesamte Bandbreite auf allen Kanälen in Storage-Einheit (100 MB/s) ist, wird dadurch das System nicht Engpässen bei. Da dies nur eine der beiden Kanäle (die zusätzliche 1 GB/s Fibre Channel Verbindung wird für die Redundanz), ist außerdem bei einem Verbindungsfehler, die verbleibende Verbindung immer noch über ausreichend Kapazität verfügt, alle angeforderten Datenübertragungen zu behandeln.

En Route auf dem Server, die Daten werden in den meisten Fällen einen SAN-Switch übertragen. Da es sich bei der SAN-Switch hat beim Verarbeiten der eingehenden e/a-Anforderung und weiterleiten, den entsprechenden Port, der Switch verfügt über eine Begrenzung der Menge der e/a, die verarbeitet werden können, Hersteller-Spezifikationen werden jedoch erforderlich, welche dieser Grenzwert ist. Z. B. wenn es zwei Switches gibt, und jeder Schalter kann 10.000 IOPS verarbeiten, werden der Gesamtdurchsatz 20.000 IOPS. In diesem Fall Fehlertoleranz wird relevant, wenn ein Switch aus, den Gesamtdurchsatz des Systems 10.000 IOPS werden. Wie es benötigt wird, nicht zu überschreiten die Auslastungsgrenze von 80 % im normalen Betrieb, sollte nicht mehr als 8000 mit e/a des Ziels.

Der HBA, die auf dem Server installierten müssten schließlich auch eine Begrenzung der Menge der e/a, die er verarbeiten kann. In der Regel ein zweiter HBA für Redundanz installiert ist, aber bei der Berechnung der maximalen e/a, die den Gesamtdurchsatz erfolgen, können mit dem SAN-Schalter, wie *N* &ndash; 1 HBAs ist die maximale Skalierbarkeit des Systems.

### <a name="caching-considerations"></a>Überlegungen zum Caching

Caches sind eine der Komponenten, die deutlich die gesamtleistung zu einem beliebigen Zeitpunkt innerhalb des Speichersystems beeinflussen können. Detaillierte Analyse zu caching-Algorithmen ist über den Rahmen dieses Artikels hinaus. Allerdings sind einige grundlegende Anweisungen zur Zwischenspeicherung auf Datenträger-Subsysteme zu beleuchten:

- Zwischenspeichern wird verbesserte nachhaltige sequenzielle Schreibvorgänge wie können Sie viele kleinere Schreibvorgänge in größeren Blöcken der e/a-Puffern und Auslagerung auf den Speicher in weniger aber größere Blockgröße. Dadurch wird die zufällige e/a gesamt und sequenzielle e/a gesamt, dadurch wird mehr Verfügbarkeit von Ressourcen für andere e/a reduziert.
- Zwischenspeichern von verbessert längeren schreiben e/a-Durchsatz des Speichersubsystems nicht. Es kann nur für die Schreibvorgänge gepuffert werden, bis der Spindeln für die Daten verfügbar sind. Wenn alle der verfügbaren e/a der Spindles im Speichersubsystem für längere Zeiträume gesättigt ist, wird schließlich der Cache gefüllt. Um den Cache genügend Zeit zwischen den Spitzen oder zusätzliche Spindeln leer ist, müssen Sie zugewiesen werden, um genügend e/a, um den Cache zu leeren ermöglichen bereitzustellen.

  Größere Caches können nur weitere Daten gepuffert werden. Dies bedeutet, dass die längere Zeiträume Sättigung untergebracht werden können.

  In einem normalerweise Betriebssystem Speichersubsystem wird das Betriebssystem bessere schreibleistungen auftreten, wie die Daten nur in den Cache geschrieben werden müssen. Nachdem die zugrunde liegenden Medien mit e/a ausgeschöpft ist, den Cache zu füllen, und schreibleistung auf datenträgergeschwindigkeit zurück.

- Wenn e/a Zwischenspeicherung gelesen wird, ist das Szenario, in dem der Cache günstigsten ist, wenn die Daten sequenziell auf dem Datenträger gespeichert und kann der Cache Read-ahead (es wird davon ausgegangen, dass es sich bei der nächsten Sektor der Daten enthält, die als Nächstes angefordert werden).
- Beim Lesen von ist e/a zufälligen, Zwischenspeicherung auf dem Laufwerk-Controller es unwahrscheinlich, dass jede Erweiterung, die Menge der Daten bereit, die vom Datenträger gelesen werden kann. Erweiterung ist nicht vorhanden, wenn das Betriebssystem oder die Größe des Caches anwendungsbasierte größer als die Hardware-basierte Cachegröße ist.

  Im Fall von Active Directory wird der Cache nur durch die Größe des Arbeitsspeichers begrenzt.

### <a name="ssd-considerations"></a>SSD-Überlegungen

SSDs sind eine komplett andere Sache als Spindel-basierte Festplatten. Die beiden wichtigsten Kriterien bleiben: "Wie viele IOPS-Wert kann es verarbeiten?" und "Was ist die Latenz für diese IOPS?" Im Vergleich zu Spindel-basierte Festplatten können SSDs können größere Mengen an e/a behandeln und niedrigere Latenzen. Im Allgemeinen und während ich dies schreibe, SSDs in einem Vergleich der Kosten pro Gigabyte weiterhin teuer sind, sie sind sehr günstig im Hinblick auf Kosten pro-e/A und verdienen maßgeblicher Aspekt im Hinblick auf Leistung.

Überlegungen:

- Sowohl IOPS und Latenzen sind sehr subjektiv, die Hersteller-Entwürfe, und in einigen Fällen schlechteren Leistung als Grundlage Technologien Spulen beobachtet wurde. Kurz gesagt, ist es wichtiger, lesen und überprüfen die Hersteller-Spezifikationen durch das Laufwerk aus, und alle Generalities Sie nicht davon aus.
- IOPS-Wert-Typen können sehr unterschiedlich viele abhängig davon, ob diese gelesen oder geschrieben haben. AD DS-Dienste, im Allgemeinen werden wird vorwiegend Lese--basiert, weniger als einige andere Anwendungsszenarien betroffen.
- "Write Endurance" – ist dies das Konzept, das SSD Zellen sich schließlich wear werden. Verschiedene Hersteller befassen sich mit dieser Herausforderung unterschiedlichen Größen dargestellt. Mindestens kann das Laufwerk, die hauptsächlich schreibgeschützte e/a-Profil für downplaying die Bedeutung dieses Problem, da die Daten nicht sehr unbeständigen ist.

### <a name="summary"></a>Zusammenfassung

Eine Möglichkeit zum Speicher überlegen ist einem Haushalt Plumbing picturing. Angenommen Sie, der den IOPS-Wert der Medien, denen die Daten gespeichert werden, auf die household main entladen wird. Wenn dies ist (z. B. Wurzeln in die Pipe) verstopft oder Limited (es ist reduziert oder zu klein), allen senken Haushalts sichern Wenn zu viel Wasser wird verwendet (zu viele Gäste). Dies ist perfekt analog zu einer freigegebenen Umgebung, in dem ein oder mehrere Systeme freigegebenen Speicher auf einem SAN/NAS/iSCSI-mit den gleichen zugrunde liegenden Medien nutzen werden. Verschiedene Ansätze können ausgeführt werden, um die verschiedenen Szenarien zu beheben:

- Eine Leerung reduzierte oder zu kleinen ist erforderlich, einen umfassenden Ersatz und beheben. Dies wäre ähnlich wie bei Hinzufügen neuer Hardware oder Neuverteilen von den Systemen, die mit den freigegebenen Speicher in der gesamten Infrastruktur.
- Eine Pipe "verstopften" bedeutet in der Regel Identifizierung von ein oder mehrere problematische Probleme und Entfernen dieser Probleme. Dies könnte in einem Szenario mit Storage-Speicher oder System Sicherungen, die Ebene, synchronisierte Virenprüfungen für alle Server und synchronisierte Defragmentierung Software ausgeführt wird, während der Spitzenzeiten sein.

In jedem Entwurf Plumbing-feed in der main-Abfluss mehrere geleert wird. Wenn nichts Einrichten dieser geleert wird, oder ein Verknüpfungspunkt beendet wird, zeigen nur die Dinge hinter diese Verbindungen sichern. In einem Szenario mit Storage kann dies einen überladenen Switch (SAN/NAS/iSCSI-Szenario), Treiberkompatibilitätsprobleme (falsche Treiber/HBA Firmware/storport.sys Kombination) oder Sicherung/Antivirus/Defragmentierung sein. Um festzustellen, ob der Speicher "Pipe" groß genug ist, muss IOPS- und e/a-Größe gemessen wird. Einzelnen Gelenken hinzufügen zusammen, um ausreichend sicher "Pipe Durchmesser."

## <a name="appendix-d---discussion-on-storage-troubleshooting---environments-where-providing-at-least-as-much-ram-as-the-database-size-is-not-a-viable-option"></a>Anhang D - Diskussion zur Problembehandlung für Storage - Umgebungen, in denen bereitstellen mindestens genauso viel RAM, wie die Größe der Datenbank nicht realisierbar ist.

Es ist hilfreich zu verstehen, warum Sie diese Empfehlungen vorhanden sind, damit die Änderungen im Storage-Technologie untergebracht werden können. Diese Empfehlungen sind für gibt es zwei Gründe. Die erste ist die Isolation von e/a, sodass Leistungsprobleme (das paging wird) auf dem Betriebssystem Spindel Leistung der Datenbank und der e/a-Profile nicht beeinträchtigt. Die zweite ist, dass Protokolldateien für AD DS (und die meisten Datenbanken) naturgemäß hintereinander erfolgen sind, und Festplatten Spindel-basierte und Caches einer großen Leistungssteigerung bei der Verwendung mit sequenzieller e/a im Vergleich zu zufälliger e/a-Muster des Betriebssystems und fast rein zufälligen e/a-Muster von der AD DS-Datenbank Laufwerk. Durch die sequenzielle e/a auf einem separaten physischen Laufwerk zu isolieren, kann der Durchsatz erhöht werden. Die Herausforderung, präsentiert von Speicheroptionen von heute ist, dass die grundlegenden Annahmen hinter diese Empfehlungen nicht mehr erfüllt sind. In vielen virtualisiert Storage-Szenarien, z. B. iSCSI-SAN, NAS und virtuellen Datenträger Bilddateien, die zugrunde liegende Speicher, auf die Medien über mehrere Hosts hinweg gemeinsam genutzt werden, daher vollständig negieren, sowohl "Isolation e/a-" als auch die Aspekte "sequenziellen e/a-Optimierung". In der Tat Hinzufügen dieser Szenarien eine zusätzliche Ebene der Komplexität, da andere Hosts, die Zugriff auf die freigegebene Medien Reaktionsfähigkeit gegenüber dem Domänencontroller beeinträchtigen können.

Bei der Planung von speicherleistung, es gibt drei Kategorien berücksichtigen: kalter Cachestatus, Cachestatus vorbereitet und Sicherung/Wiederherstellung. Die kalte Cachestatus tritt auf, in Szenarien wie z. B. wenn der Domänencontroller zunächst neu gestartet wird oder Active Directory-Dienst neu gestartet wird und es sind keine Active Directory-Daten im Arbeitsspeicher. Warme Cachestatus ist, in denen der Domänencontroller in einem stabilen Zustand und die Datenbank zwischengespeichert wird. Dies sind zu beachten, werden sie sehr unterschiedliche Leistungsprofile Laufwerk, und dass ausreichend Arbeitsspeicher zum Zwischenspeichern der gesamten Datenbank nicht zur Leistung, wenn der Cache ist im kalten. Einen kann berücksichtigen, Leistung-Entwurf für diese beiden Szenarien mit folgenden folgende Analogie, Auffüllen des kalten Caches "Sprints" und mit einem Server mit einem betriebsbereiten Cache ist eine "Marathon".

Für den inaktiven Cache und betriebsbereiten Cache-Szenario wird die Frage, wie schnell der Speicher die Daten vom Datenträger in den Arbeitsspeicher verschieben kann. Auffüllen des Caches ist ein Szenario, wobei im Laufe der Zeit die Leistung verbessert mehr Abfragen Wiederverwenden von Daten, die Cachetreffer Rate erhöht und verringert die Häufigkeit der müssen den Datenträger zu. Infolgedessen verringert sich Auswirkungen auf die negative Leistung wechseln, auf dem Datenträger. Beeinträchtigung der Leistung ist beim Warten auf des Caches zu befassen und zu wachsen, um die zulässige Größe der maximalen, systemabhängiger nur vorübergehend. Die Konversation vereinfacht werden, wie schnell die Daten auf Datenträger abgerufen werden können, und ein einfaches Measure der IOPS-Werte zur Active Directory, der ist subjektiv verfügbaren IOPS aus dem zugrunde liegenden Speicher. Hinsichtlich der Planung da Auffüllen der Cache und Sicherung/Wiederherstellung Szenarien gibt es in Ausnahmefällen, normalerweise außerhalb der Geschäftszeiten ausgeführt und sind subjektiv, mit dem Laden des DC, sind allgemeine Empfehlungen nicht mit Ausnahme vorhanden, da diese Aktivitäten geplant werden für nicht-Spitzenzeiten.

AD DS in den meisten Szenarien, wird in der Regel ein Verhältnis von 90 % read/10% schreiben e/a vorwiegend gelesen werden. Lese-e/a ist häufig der Engpass bei der Benutzeroberfläche und mit e/a schreiben, bewirkt, dass Leistung schreiben. Wie e/a NTDS.dit überwiegend zufällig ist, Caches tendenziell minimalen Vorteilen zum Lesen von e/a, die somit viel Wichtigeres so konfigurieren Sie der Speicher für e/a-Profil korrekt gelesen.

Für den normalen betriebsbedingungen ist das Storage-Planung-Ziel, minimiert die Wartezeit für eine Anforderung von AD DS von einem Datenträger zurückgegeben werden. Dies bedeutet im Wesentlichen, dass die Anzahl der ausstehenden und ausstehenden e/a-kleiner als oder gleich der Anzahl der Pfade, auf dem Datenträger. Es gibt eine Vielzahl von Möglichkeiten, dies zu messen. Im Szenario eine Leistungsüberwachung, es wird allgemein empfohlen, logischer Datenträger ( *\<NTDS-Datenbank-Laufwerk\>* ) \Avg Sek./Lesevorgänge werden weniger als 20 ms. Der gewünschte Betriebsmodus Schwellenwert muss viel niedriger, vorzugsweise als nahezu die Geschwindigkeit des Speichers wie möglich, im Bereich von 2 bis 6 im Millisekundenbereich (.002 zu.006 Sekunde) je nach Art des Speichers sein.

Beispiel:

![Organigramm der Speicherlatenz](media/capacity-planning-considerations-storage-latency.png)

Das Diagramm wird analysiert:

- **Grüne "-Oval" auf der linken Seite –** die Latenz bei 10 ms konsistent bleibt. Die Auslastung erhöht, von 800 IOPS 2400 IOPS. Dies ist der absolute Boden zu Reaktionsschnelligkeit eine e/a-Anforderung von der zugrunde liegende Speicher verarbeitet werden kann. Dies ist abhängig von den Besonderheiten der speicherlösung.
- **' Burgunderrot ' "-Oval" auf der rechten Seite –** der Durchsatz aus Beenden einer durch den grünen Kreis am Ende der Erfassung von Flatfiles bleibt, während die Latenz nimmt kontinuierlich zu. Dadurch wird veranschaulicht, wenn die Anforderung Volumes die physikalischen Beschränkungen von der zugrunde liegende Speicher überschritten wird, je länger die Anforderungen Ausgaben in der Warteschlange darauf warten, für das Speichersubsystem versendet werden.

Anwenden von diesem Wissen:

- **Auswirkungen auf Benutzer Abfragen Mitglied einer großen Gruppe –** wird vorausgesetzt, dies erfordert, Lesen von 1 MB Daten vom Datenträger, die Menge an e/a und wie lange es dauert ausgewertet werden kann wie folgt:
  - Active Directory-Datenbank-Seiten sind 8 KB groß. 
  - Mindestens 128 Seiten müssen in vom Datenträger gelesen werden. 
  - "Nothing" vorausgesetzt wird, an den Boden (10 ms) zwischengespeichert, dies mindestens 1,28 Sekunden dauern, bis die Daten vom Datenträger geladen wird, um es an den Client zurückgegeben wird. Bei 20 ms, wobei der Durchsatz auf den Speicher hat inzwischen längst Ihr Maximum erreicht hat und ist auch das empfohlene Maximum, dauert es, 2,5 Sekunden zum Abrufen der Daten vom Datenträger, um es für den Endbenutzer zurückgegeben werden.  
- **Mit welcher Häufigkeit wird der Cache werden vorbereitet –** vornehmen der Annahme, der Clientbelastung Maximierung des Durchsatzes auf diesem Storage-Beispiel relevant ist, wird der Cache mit einer Rate von 2400 IOPS warme &times; 8 KB pro e/a. Oder ungefähr 20 MB/s pro Sekunde, Laden von etwa 1 GB-Datenbank in den Arbeitsspeicher 53 Sekunden.

> [!NOTE]
> Es ist normal, die für einen kurzen Zeitraum beobachten die Wartezeiten ansteigt, wenn Komponenten aggressiv lesen oder Schreiben auf den Datenträger wie z. B. wenn das System gesichert wird oder wenn AD DS für die automatische speicherbereinigung ausgeführt wird. Zusätzliche Head Platz auf die Berechnungen muss angegeben werden, um diese periodische Ereignisse zu berücksichtigen. Das Ziel mit genügend Durchsatz bieten für diese Szenarien ohne Auswirkungen auf normale Funktion.

Wie Sie sehen, besteht ein physisches Limit, basierend auf den Entwurf des Speichersystems, wie schnell der Cache möglicherweise befassen kann. Wie den Cache warme wird werden eingehende Clientanforderungen, bis die Rate, mit der zugrunde liegenden Speichers bereitstellen kann. Ausführen von Skripts "den Cache während der Spitzenzeiten vorab befassen" bieten Wettbewerb von echten Clientanforderungen geladen. Die kann Bereitstellung von Daten beeinträchtigen, die Clients müssen zuerst, da programmbedingt er Konkurrenz um Ressourcen knapp Datenträger generiert wie künstliche versucht, den Cache warme Daten, die für die Clients lädt, wenden Sie sich an den DC nicht relevant ist.
