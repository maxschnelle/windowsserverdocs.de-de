---
title: Kapazitätsplanung für Active Directory Domain Services
description: Ausführliche Erörterung der Faktoren, die bei der Kapazitätsplanung für AD DS zu berücksichtigen sind.
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; kenbrunf
author: Teresa-Motiv
ms.date: 7/3/2019
ms.openlocfilehash: 8b17d7f5c7774c1c332d49962b14fe31128f1a27
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370430"
---
# <a name="capacity-planning-for-active-directory-domain-services"></a>Kapazitätsplanung für Active Directory Domain Services

Dieses Thema wurde ursprünglich von Ken Brumfield, Senior Premier Field Engineer bei Microsoft verfasst und enthält Empfehlungen für die Kapazitätsplanung für Active Directory Domain Services (AD DS).

## <a name="goals-of-capacity-planning"></a>Ziele der Kapazitätsplanung

Die Kapazitätsplanung ist nicht mit der Problembehandlung bei Leistungs Vorfällen identisch. Sie sind eng verwandt, aber sehr unterschiedlich. Die Ziele der Kapazitätsplanung lauten:  

- Ordnungsgemäße Implementierung und Betrieb einer Umgebung 
- Minimieren Sie die Zeit, die Sie bei der Problembehandlung  
  
Bei der Kapazitätsplanung kann eine Organisation in Spitzenzeiten ein Baseline-Ziel von 40% der Prozessorauslastung aufweisen, um die Anforderungen an die Client Leistung zu erfüllen und die erforderliche Zeit zum Aktualisieren der Hardware im Daten Center zu erfüllen. Um jedoch über ungewöhnliche Leistungs Vorfälle benachrichtigt zu werden, kann ein Schwellenwert für die Überwachungs Warnung in einem Intervall von 5 Minuten auf 90% festgelegt werden.

Der Unterschied besteht darin, dass ein Kapazitäts Verwaltungs Schwellenwert immer dann, wenn ein Kapazitäts Verwaltungs Schwellenwert überschritten wird (ein einmaligen Ereignis ist kein Problem ist), eine Lösung ist oder der Dienst auf mehrere Server skaliert werden kann. Not. Schwellenwerte für die Leistungs Warnung deuten darauf hin, dass die Client Leistung derzeit beeinträchtigt wird und dass sofortige Schritte zum Beheben des Problems erforderlich sind.

Eine Analogie: das Capacity Management besteht darin, einen fahrzeugunfall zu verhindern (defensives Fahrverhalten, sicherzustellen, dass die Bremsen ordnungsgemäß funktionieren usw.), während die Problembehandlung bei der Leistung von der Polizei, der feuerwehrabteilung und den medizinischen notfallspezialisten durchzuführen ist. nach einem Unfall. Dabei geht es um "defensives treiben", Active Directory Stil.

In den letzten Jahren hat sich der Leitfaden zur Kapazitätsplanung für Systeme mit horizontaler Skalierung erheblich verändert. Die folgenden Änderungen an Systemarchitekturen haben grundlegende Annahmen über das Entwerfen und Skalieren eines diendienstanzdienstanz

- 64-Bit-Serverplattformen  
- Virtualisierung  
- Erhöhter Aufmerksamkeit beim Stromverbrauch  
- SSD-Speicher  
- Cloudszenarien  

Außerdem wird der Ansatz von einer serverbasierten Kapazitäts Planungsübung zu einer Dienst basierten Kapazitäts Planungsübung verlagert. Active Directory Domain Services (AD DS), ein ausgereifter verteilter Dienst, der von vielen Produkten von Microsoft und Drittanbietern als Back-End verwendet wird, wird zu einem der wichtigsten Produkte, die für die ordnungsgemäße Planung der erforderlichen Kapazität für die Durchführung anderer Anwendungen erforderlich sind.

### <a name="baseline-requirements-for-capacity-planning-guidance"></a>Grundlegende Anforderungen für die Kapazitäts Planungs Anleitung

In diesem Artikel werden die folgenden grundlegenden Anforderungen erwartet:

- Leser haben Lese-und Lesezugriff [auf die Richtlinien zur Leistungsoptimierung für Windows Server 2012 R2](https://docs.microsoft.com/previous-versions//dn529133(v=vs.85)).
- Die Windows Server-Plattform ist eine x64-basierte Architektur. Auch wenn Ihre Active Directory-Umgebung auf Windows Server 2003 x86 installiert ist (jetzt über das Ende des Support Lebenszyklus hinaus) und eine Verzeichnis Informationsstruktur (DIT) mit einer Größe von weniger als 1,5 GB aufweist und problemlos im Speicher gehalten werden kann, gelten die Richtlinien von diesem der Artikel ist weiterhin anwendbar.
- Die Kapazitätsplanung ist ein kontinuierlicher Prozess, und Sie sollten regelmäßig überprüfen, wie gut die Umgebung die Erwartungen erfüllt.
- Die Optimierung erfolgt über mehrere Hardware Lebenszyklen, wenn sich die Hardwarekosten ändern. Beispielsweise wird der Arbeitsspeicher günstiger, die Kosten pro Kern werden verringert, oder der Preis für verschiedene Speicheroptionen ändert sich.
- Planen Sie den Spitzen Zeitraum des Tages. Es wird empfohlen, dies in Intervallen von 30 Minuten oder Stunden zu überprüfen. Durch einen größeren Wert können die tatsächlichen Spitzen ausgeblendet werden, und alle anderen werden möglicherweise durch "vorübergehende Spitzen" verzerrt.
- Planen Sie das Wachstum im Verlauf des Hardware Lebenszyklus für das Unternehmen. Dies kann eine Strategie zum Aktualisieren oder Hinzufügen von Hardware auf eine gestaffelte Weise oder eine komplette Aktualisierung alle drei bis fünf Jahre umfassen. Jeder Vorgang erfordert eine "Vermutung", um zu ermitteln, wie viel die Auslastung Active Directory zunehmen wird. Verlaufs Daten werden bei dieser Bewertung unterstützt. 
- Planen Sie die Fehlertoleranz. Nachdem eine Schätzung *n* abgeleitet wurde, sollten Sie Szenarien planen, *die n* &ndash; 1, *n* &ndash; 2, *n* &ndash; *x*enthalten.
  - Fügen Sie zusätzliche Server nach Organisations Bedarf hinzu, um sicherzustellen, dass der Verlust eines einzelnen oder mehrerer Server nicht die maximalen Schätzungen der Spitzen Kapazität überschreitet.
  - Beachten Sie auch, dass der Wachstumsplan und der Fehlertoleranz Plan integriert werden müssen. Wenn z. b. ein Domänen Controller erforderlich ist, um die Last zu unterstützen, aber die Schätzung darin besteht, dass die Auslastung im nächsten Jahr verdoppelt wird und zwei DCS insgesamt erforderlich sind, reicht die Kapazität nicht aus, um die Fehlertoleranz zu unterstützen. Die Lösung besteht darin, mit drei DCS zu beginnen. Sie können auch planen, den dritten DC nach 3 oder 6 Monaten hinzuzufügen, wenn das Budget knapp ist.

    >[!NOTE]
    >Das Hinzufügen Active Directory-fähiger Anwendungen hat möglicherweise eine spürbare Auswirkung auf die DC-Auslastung, unabhängig davon, ob die Auslastung von den Anwendungsservern oder Clients stammt.

### <a name="three-step-process-for-the-capacity-planning-cycle"></a>Dreistufiger Prozess für den Kapazitäts Planungszeitraum

Entscheiden Sie bei der Kapazitätsplanung zunächst, welche Quality of Service erforderlich ist. Ein Kern Rechenzentrum unterstützt z. b. ein höheres Maß an Parallelität und erfordert eine konsistentere Benutzer Leistung für Benutzer und Anwendungen. Dies erfordert größere Aufmerksamkeit auf Redundanz und Minimierung von System-und infrastrukturengpässen. Im Gegensatz dazu benötigt ein satellitenort mit einigen Benutzern nicht die gleiche Ebene der Parallelität oder Fehlertoleranz. Daher ist es möglich, dass die satellitenniederlassung nicht so viel Aufmerksamkeit benötigt, um die zugrunde liegende Hardware und Infrastruktur zu optimieren, was zu Kosteneinsparungen führen kann. Alle hier aufgeführten Empfehlungen und Anleitungen dienen der optimalen Leistung und können für Szenarien mit weniger anspruchsvollen Anforderungen selektiv gelockert werden.

Die nächste Frage lautet: virtualisiert oder physisch? Aus Sicht der Kapazitätsplanung gibt es keine richtige oder falsche Antwort. Es gibt nur einen anderen Satz von Variablen, mit denen Sie arbeiten können. Virtualisierungsszenarien können auf eine von zwei Optionen zurückgehen:

- "Direkte Zuordnung" mit einem Gast pro Host (wobei die Virtualisierung ausschließlich zur Abstraktion der physischen Hardware vom Server vorhanden ist)
- "Gemeinsamer Host"

Test-und Produktionsszenarien zeigen an, dass das "direkte Mapping"-Szenario identisch mit einem physischen Host behandelt werden kann. "Gemeinsamer Host" führt jedoch eine Reihe von Überlegungen ein, die später ausführlicher beschrieben werden. Das Szenario "gemeinsam genutzter Host" bedeutet, dass die AD DS auch für Ressourcen konkurrieren, und dass es zu Maßnahmen und Optimierungs Überlegungen kommt.

Wenn Sie diese Überlegungen beachten, ist der Kapazitäts Planungszeitraum ein iterativer dreistufiger Prozess:

1. Messen Sie die vorhandene Umgebung, legen Sie fest, wo sich die System Engpässe derzeit befinden, und erhalten Sie grundlegende Grundlagen, um die erforderliche Kapazität zu planen.
1. Bestimmen Sie die Hardware, die gemäß den in Schritt 1 beschriebenen Kriterien benötigt wird.
1. Überwachen und überprüfen, ob die implementierte Infrastruktur innerhalb von Spezifikationen funktioniert. Einige Daten, die in diesem Schritt gesammelt werden, werden zur Baseline für den nächsten Zeitraum der Kapazitätsplanung.

### <a name="applying-the-process"></a>Anwenden des Prozesses

Um die Leistung zu optimieren, stellen Sie sicher, dass diese Hauptkomponenten ordnungsgemäß ausgewählt und auf die Anwendungs Auslastung abgestimmt sind:

1. Arbeitsspeicher
1. Network
1. Speicher
1. Prozessor
1. Anmeldedienst

Die grundlegenden Speicheranforderungen von AD DS und das allgemeine Verhalten von gut geschriebenen Client Software ermöglichen Umgebungen mit bis zu 10.000 bis 20.000 Benutzern, große Investitionen in die Kapazitätsplanung in Bezug auf physische Hardware, wie fast jeden modernen Server, zu unterbinden. die Last wird von Class System verarbeitet. In der folgenden Tabelle wird jedoch zusammengefasst, wie eine vorhandene Umgebung ausgewertet wird, um die richtige Hardware auszuwählen. Jede Komponente wird in den nachfolgenden Abschnitten ausführlich analysiert, damit AD DS Administratoren ihre Infrastruktur mithilfe von baselineempfehlungen und Umgebungs spezifischen Prinzipalen auswerten können.

Im allgemeinen:

- Jede Größe, die auf aktuellen Daten basiert, wird nur für die aktuelle Umgebung genau sein.
- Erwarten Sie bei geschätzten Schätzungen, dass die Nachfrage über den Lebenszyklus der Hardware wächst.
- Legen Sie fest, ob Sie heutzutage übermäßig groß werden und sich in der größeren Umgebung anwachsen lassen, oder Sie können über den Lebenszyklus Kapazität
- Für die Virtualisierung gelten dieselben Kapazitäts Planungs Prinzipale und Methodologien, mit der Ausnahme, dass der Aufwand der Virtualisierung allen Domänen bezogenen Aufgaben hinzugefügt werden muss.
- Die Kapazitätsplanung, wie alles, was vorhergesagt werden soll, ist keine genaue Wissenschaft. Erwarten Sie nicht, dass Dinge perfekt und mit einer Genauigkeit von 100% berechnet werden. Hier finden Sie die Empfehlung zum leanest. erhöhen Sie die Kapazität für zusätzliche Sicherheit, und überprüfen Sie kontinuierlich, ob die Umgebung auf dem Ziel bleibt.

### <a name="data-collection-summary-tables"></a>Zusammenfassungs Tabellen für die Datensammlung

#### <a name="new-environment"></a>Neue Umgebung

| Komponente | Experten |
|-|-|
|Speicher/Datenbankgröße|40 KB bis 60 KB für jeden Benutzer|
|RAM|Datenbankgröße<br />Empfehlungen des Basis Betriebssystems<br />Anwendungen von Drittanbietern|
|Network|1 GB|
|CPU|1000 gleichzeitige Benutzer für jeden Kern|

#### <a name="high-level-evaluation-criteria"></a>Allgemeine Evaluierungs Kriterien

| Komponente | Bewertungskriterien | Planungsüberlegungen |
|-|-|-|
|Speicher/Datenbankgröße|Der Abschnitt "So aktivieren Sie die Protokollierung von Speicherplatz, der durch Defragmentierung freigegeben wird" in [Speicher Limits](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))| |
|Speicherung/Datenbankleistung|<ul><li>"LogicalDisk ( *\<NTDS-Daten\>Bank Laufwerk*) \Mittlere Sek./Lesevorgänge", "LogicalDisk ( *\<NTDS\>-Daten Bank Laufwerk*) \Durchschnittl. Sek./Schreibvorgang", "LogicalDisk" ( *\<NTDS-Daten Bank Laufwerk )\>* \ Mittlere Sek./Übertragung "</li><li>"LogicalDisk ( *\<NTDS-Daten\>Bank Laufwerk*) \ Lesevorgänge/Sek." "LogicalDisk ( *\<NTDS-Daten Bank Laufwerk\>* ) \ Schreibvorgänge/Sek." "LogicalDisk ( *\<NTDS-Daten Bank Laufwerk\>* ) \ Übertragungen/Sek. "</li></ul>|<ul><li>Für den Speicher sind zwei Aspekte zu berücksichtigen.<ul><li>Verfügbarer Speicherplatz, der für die meisten AD-Umgebungen von der Größe der aktuellen Spindel basierten und SSD-basierten Speicherung abhängig ist.</li> <li>E/a-Vorgänge (e/a-Vorgänge) verfügbar – in vielen Umgebungen wird dies oft übersehen. Es ist jedoch wichtig, nur Umgebungen auszuwerten, in denen nicht genügend RAM vorhanden ist, um die gesamte NTDS-Datenbank in den Arbeitsspeicher zu laden.</li></ul><li>Der Speicher kann ein komplexes Thema sein und sollte Hardwarehersteller-Fachkenntnisse für eine ordnungsgemäße Größenanpassung umfassen. Besonders bei komplexeren Szenarien, wie z. b. San-, NAS-und iSCSI-Szenarios. Im Allgemeinen werden Kosten pro GB Speicher jedoch häufig direkt gegen die Kosten pro e/a-Vorgänge unterstellt:<ul><li>RAID 5 hat niedrigere Kosten pro Gigabyte als RAID 1, RAID 1 hat jedoch niedrigere Kosten pro e/a.</li><li>Bei Spindel basierten Festplatten fallen niedrigere Kosten pro Gigabyte an, SSDs haben jedoch niedrigere Kosten pro e/a.</li></ul><li>Nach einem Neustart des Computers oder des Active Directory Domain Services Dienstanbieter ist der ESE-Cache (Extensible Storage Engine) leer, und die Leistung wird Datenträger gebunden, während der Cache erwärmt wird.</li><li>In den meisten Umgebungen ist AD intensive e/a-Vorgänge in zufälligen Mustern auf Datenträgern, was den Vorteil von zwischen Speicherungs-und Lese Optimierungsstrategien neiert.  Außerdem bietet AD einen viel größeren Cache im Speicher als die meisten Speichersystem Caches.</li></ul>
|RAM|<ul><li>Datenbankgröße</li><li>Empfehlungen des Basis Betriebssystems</li><li>Anwendungen von Drittanbietern</li></ul>|<ul><li>Storage ist die langsamste Komponente eines Computers. Umso mehr, was sich im RAM befinden kann, desto weniger müssen Sie auf den Datenträger wechseln.</li><li>Stellen Sie sicher, dass genügend RAM zum Speichern des Betriebssystems, der Agents (Antivirus, Sicherung, Überwachung), NTDS-Datenbank und Wachstum im Laufe der Zeit zugeordnet ist.</li><li>Für Umgebungen, in denen das Maximieren der RAM-Größe nicht kostengünstig ist (z. b. bei Satellitenstandorten) oder nicht möglich ist (DIT ist zu groß), verweisen Sie auf den Abschnitt Speicher, um sicherzustellen, dass die Größe des Speichers korrekt ist</li></ul>|
|Network|<ul><li>"Netzwerkschnittstelle (\*) \Empfangene Bytes/Sek."</li><li>"Netzwerkschnittstelle (\*) \Gesendete Bytes/Sek."|<ul><li>Im Allgemeinen überschreitet der Datenverkehr, der von einem DC gesendet wird, den an einen DC gesendeten Datenverkehr</li><li>Wenn eine Umgeschaltete Ethernet-Verbindung Vollduplex ist, muss der eingehende und ausgehende Netzwerk Datenverkehr unabhängig voneinander dimensioniert werden.</li><li>Das Konsolidieren der Anzahl von DCS erhöht den Umfang der Bandbreite, der zum Senden von Antworten an Client Anforderungen für die einzelnen Domänen Controller verwendet wird. Sie ist jedoch für den gesamten Standort nahezu gleich.</li><li>Wenn Sie satellitenspeicherort-DCS entfernen, vergessen Sie nicht, die Bandbreite für den Satelliten Controller zu den Hub-DCS hinzuzufügen und zu ermitteln, wie viel WAN-Datenverkehr vorhanden sein wird.</li></ul>|
|CPU|<ul><li>"Logischer Datenträger ( *\<NTDS-\>Daten Bank Laufwerk*) \ Mittlere Sek./Lesevorgänge"</li><li>"Process (LSASS) \\% Prozessorzeit"</li></ul>|<ul><li>Nachdem Sie den Speicher als Engpass eliminiert haben, müssen Sie die benötigte computestrommenge beheben.</li><li>Die Anzahl der Prozessorkerne, die für alle Server innerhalb eines bestimmten Bereichs (z. b. einer Website) beansprucht werden, kann zwar nicht perfekt linear sein, aber die Anzahl der Prozessoren, die zur Unterstützung der gesamten Client Last erforderlich sind, kann verwendet werden. Fügen Sie die erforderliche Mindestanzahl hinzu, um die aktuelle Dienst Ebene für alle Systeme innerhalb des Bereichs beizubehalten.</li><li>Änderungen an der Prozessorgeschwindigkeit, einschließlich der Energie verwaltungsbezogenen Änderungen, wirken sich auf die von der aktuellen Umgebung abgeleiteten Zahlen aus. Im Allgemeinen ist es nicht möglich, genau zu bewerten, wie von einem 2,5 GHz-Prozessor zu einem 3-GHz-Prozessor die Anzahl der benötigten CPUs verringert wird.</li></ul>|
|Anmeldedienst|<ul><li>"Netlogon (\*) \semaphore Ruft ab"</li><li>"Netlogon (\*) \semaphore Timeouts"</li><li>"Netlogon (\*) \average Semaphore Hold Time"</li></ul>|<ul><li>Der sichere Kanal für die Netzwerk Anmeldung/MaxConcurrentApi wirkt sich nur auf Umgebungen mit NTLM-Authentifizierungen und/oder PAC-Überprüfung aus. Die PAC-Überprüfung ist in Betriebssystemversionen vor Windows Server 2008 standardmäßig aktiviert. Dies ist eine Client Einstellung, sodass die DCS beeinträchtigt werden, bis diese auf allen Client Systemen ausgeschaltet ist.</li><li>Umgebungen mit erheblicher vertrauenswürdiger Authentifizierung, die Gesamtstruktur übergreifende Vertrauens Stellungen einschließt, haben ein höheres Risiko, wenn Sie nicht ordnungsgemäß skaliert werden.</li><li>Server Konsolidierungen erhöhen die Parallelität der vertrauenswürdigen Authentifizierung.</li><li>Die Übertragungen müssen berücksichtigt werden, wie z. b. Cluster-Failover, da Benutzer die Massen Authentifizierung für den neuen Cluster Knoten durchführen.</li><li>Einzelne Client Systeme (z. b. ein Cluster) müssen möglicherweise ebenfalls optimiert werden.</li></ul>|

## <a name="planning"></a>Planen

Für einen längeren Zeitraum ist die Empfehlung der Community für die Größenanpassung von AD DS, "in so viel RAM wie die Datenbankgröße" zu versetzen. Zum größten Teil ist diese Empfehlung alles, was für die meisten Umgebungen sorgen muss. Das Ökosystem, das AD DS beansprucht AD DS, hat sich jedoch seit seiner Einführung in 1999 erheblich vergrößert. Obwohl der Anstieg der computeleistung und der Wechsel von x86-Architekturen zu x64-Architekturen dazu geführt haben, dass die subleraspekte der Größenanpassung für eine größere Anzahl von Kunden, die AD DS auf physischer Hardware ausführen, nicht relevant sind, hat das Wachstum der Virtualisierung die Optimierungsprobleme wurden wieder in eine größere Zielgruppe als zuvor eingeführt.

Im folgenden wird erläutert, wie Sie die Anforderungen Active Directory as-as-a-Service ermitteln und planen, unabhängig davon, ob Sie in physischer, virtueller/physischer Mischung oder in einem reinen virtualisierten Szenario bereitgestellt wird. Daher wird die Auswertung auf jede der vier Hauptkomponenten unterteilen: Speicher, Arbeitsspeicher, Netzwerk und Prozessor. Kurz gesagt, um die Leistung auf AD DS zu maximieren, besteht das Ziel darin, so nah wie möglich an den Prozessor gebunden zu werden.

## <a name="ram"></a>RAM

Ganz einfach: umso mehr, die im RAM zwischengespeichert werden können, desto weniger müssen Sie auf den Datenträger wechseln. Um die Skalierbarkeit des Servers zu maximieren, muss die Mindestgröße des Arbeitsspeichers die Summe aus der aktuellen Datenbankgröße, der SYSVOL-Gesamtgröße, dem empfohlenen Betriebssystem Betrag und den Lieferanten Empfehlungen für die Agents (Antivirus, Monitoring, Backup usw.) sein. ). Eine zusätzliche Menge sollte hinzugefügt werden, um das Wachstum der Server Lebensdauer zu berücksichtigen. Dies wird auf der Grundlage von Schätzungen des Daten Bank Wachstums auf der Grundlage von Umgebungs Änderungen umweltfreundlich sein.

Für Umgebungen, in denen das Maximieren der RAM-Größe nicht kostengünstig ist (z. b. Satellitenstandorte) oder nicht möglich ist (DIT ist zu groß), verweisen Sie auf den Abschnitt Storage, um sicherzustellen, dass der Speicher ordnungsgemäß entworfen wurde.

Eine Konsequenz, die im allgemeinen Kontext bei der Größenanpassung des Arbeitsspeichers erscheint, ist die Größe der Auslagerungs Datei. Im gleichen Kontext wie der gesamte Arbeitsspeicher, ist das Ziel, die Umstellung auf den viel langsameren Datenträger zu minimieren. Daher sollte die Frage lauten: "wie sollte die Auslagerungs Datei skaliert werden?" wie viel RAM ist erforderlich, um das Paging zu minimieren? Die Antwort auf die letztere Frage wird im restlichen Teil dieses Abschnitts beschrieben. Dadurch wird der größte Teil der Erörterung der Auslagerungs Datei in den Bereich allgemeiner Empfehlungen des Betriebssystems und die Notwendigkeit, das System für Speicher Abbilder zu konfigurieren, die nicht mit AD DS Leistung zusammenhängen.

### <a name="evaluating"></a>Überprüft

Der Arbeitsspeicher, der von einem Domänen Controller (DC) benötigt wird, ist aus folgenden Gründen eine komplexe Übung:

- Hohes Risiko eines Fehlers beim Versuch, ein vorhandenes System zu verwenden, um zu messen, wie viel RAM benötigt wird, da LSASS unter unzureichenden Arbeitsspeicher Mangel zuschneidet, wodurch die Notwendigkeit künstlich defliert wird.
- Die subjektive Tatsache, dass ein einzelner Domänen Controller nur Zwischenspeichern muss, was für seine Clients interessant ist. Dies bedeutet, dass die Daten, die auf einem Domänen Controller an einem Standort mit nur einem Exchange-Server zwischengespeichert werden müssen, sich stark von den Daten unterscheiden, die auf einem Domänen Controller zwischengespeichert werden müssen, der nur Benutzer authentifiziert.
- Die Arbeitsspeicher Arbeit zum Auswerten des RAM für jeden Domänen Controller ist von Fall zu Fall unzulässig und ändert sich, wenn sich die Umgebung ändert.
- Die Kriterien hinter der Empfehlung helfen Ihnen, fundierte Entscheidungen zu treffen: 
- Umso mehr, die im Arbeitsspeicher zwischengespeichert werden können, desto weniger müssen Sie auf den Datenträger wechseln. 
- Der Speicher ist bei weitem die langsamste Komponente eines Computers. Der Zugriff auf Daten auf Spindel-und SSD-Speichermedien erfolgt in der Reihenfolge von 1, 000, 000X langsamer als der Zugriff auf Daten im Arbeitsspeicher.

Um die Skalierbarkeit des Servers zu maximieren, ist die Mindestgröße des RAM die Summe aus der aktuellen Datenbankgröße, der SYSVOL-Gesamtgröße, dem empfohlenen Betriebssystem Betrag und den Lieferanten Empfehlungen für die Agents (Antivirus, Monitoring, Backup, usw.). Fügen Sie zusätzliche Beträge hinzu, um das Wachstum während der Lebensdauer des Servers zu unterstützen. Dies wird auf der Grundlage von Schätzungen des Daten Bank Wachstums umweltfreundlich sein. Für Satellitenstandorte mit einer kleinen Gruppe von Endbenutzern können diese Anforderungen jedoch gelockert werden, da diese Websites nicht so viel Zwischenspeichern müssen, um die meisten Anforderungen zu erfüllen.

Für Umgebungen, in denen das Maximieren der RAM-Größe nicht kostengünstig ist (z. b. bei Satellitenstandorten) oder nicht möglich ist (DIT ist zu groß), verweisen Sie auf den Abschnitt Speicher, um sicherzustellen, dass die Größe des Speichers korrekt ist

> [!NOTE]
> Eine Korrelation bei der Größenanpassung der Auslagerungs Datei. Da das Ziel darin besteht, auf den viel langsameren Datenträger zu reduzieren, geht die Frage von "wie soll die Auslagerungs Datei skaliert werden?". wie viel RAM ist erforderlich, um das Paging zu minimieren? Die Antwort auf die letztere Frage wird im restlichen Teil dieses Abschnitts beschrieben. Dadurch wird der größte Teil der Erörterung der Auslagerungs Datei in den Bereich allgemeiner Empfehlungen des Betriebssystems und die Notwendigkeit, das System für Speicher Abbilder zu konfigurieren, die nicht mit AD DS Leistung zusammenhängen.

### <a name="virtualization-considerations-for-ram"></a>Überlegungen zur Virtualisierung für RAM

Vermeiden Sie den über-Commit-Speicher auf dem Host. Das grundlegende Ziel bei der Optimierung der RAM-Größe besteht darin, den Zeitaufwand für den Datenträger zu minimieren. In Virtualisierungsszenarien ist das Konzept des Arbeitsspeichers über einen Commit vorhanden, bei dem den Gästen mehr RAM zugewiesen ist, und dann auf dem physischen Computer vorhanden ist. Dies ist kein Problem. Es wird zu einem Problem, wenn der gesamte Arbeitsspeicher, der von allen Gästen aktiv genutzt wird, den RAM des Hosts überschreitet und der zugrunde liegende Host das Paging startet. Die Leistung wird Datenträger gebunden, wenn der Domänen Controller zu NTDS. dit wechselt, um Daten zu erhalten, oder der Domänen Controller wechselt zur Auslagerungs Datei, um Daten zu erhalten, oder der Host geht auf den Datenträger, um Daten zu erhalten, die der Gast im RAM hat.

### <a name="calculation-summary-example"></a>Beispiel für Berechnungs Zusammenfassung

|Komponente|Geschätzter Speicher (Beispiel)|
|-|-|
|Empfohlenen RAM für das Basis Betriebssystem (Windows Server 2008)|2 GB|
|Interne LSASS-Aufgaben|200 MB|
|Überwachungs-Agent|100 MB|
|Antivirensoftware|100 MB|
|Datenbank (globaler Katalog)|8,5 GB sind sicher???|
|Die Sicherung wird für die Sicherung ausgeführt, Administratoren können sich ohne Auswirkung anmelden.|1 GB|
|Gesamt|12 GB|

**Empfohlen 16 GB**

Im Laufe der Zeit kann angenommen werden, dass der Datenbank weitere Daten hinzugefügt werden, und der Server wird für 3 bis 5 Jahre wahrscheinlich in der Produktion ausgeführt. Basierend auf einer Schätzung des Wachstums von 33% wäre 16 GB eine angemessene Menge an RAM, die auf einem physischen Server abgelegt werden kann. Auf einem virtuellen Computer ist die Einfachheit, mit der Einstellungen geändert werden können, und der Arbeitsspeicher kann dem virtuellen Computer hinzugefügt werden, beginnend bei 12 GB mit dem Plan zur Überwachung und zum Upgrade in Zukunft angemessen.

## <a name="network"></a>Network

### <a name="evaluating"></a>Überprüft
In diesem Abschnitt geht es um die Auswertung der Anforderungen im Hinblick auf Replikations Datenverkehr, bei dem es sich um den Datenverkehr im WAN handelt, der in [Active Directory Replikations Datenverkehr](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10))ausführlich behandelt wird, als die gesamte Bandbreite und das Netzwerk erforderliche Kapazität, einschließlich Client Abfragen, Gruppenrichtlinie Anwendungen usw. Für vorhandene Umgebungen kann diese mithilfe der Leistungsindikatoren "Netzwerkschnittstelle (\*) \Empfangene Bytes/Sek." und "Netzwerkschnittstelle (\*) \Gesendete Bytes/Sek." erfasst werden. Beispiel Intervalle für Netzwerkschnittstellen Zähler in 15, 30 oder 60 Minuten. Für gute Messungen sind normalerweise weniger als flüchtig. alles höhere wird die tägliche anwirkung übermäßig stark glätten.

> [!NOTE]
> Im Allgemeinen ist der Großteil des Netzwerk Datenverkehrs auf einem Domänen Controller ausgehend, da der DC auf Client Abfragen antwortet. Dies ist der Grund für den Schwerpunkt auf ausgehendem Datenverkehr. es wird jedoch empfohlen, jede Umgebung auch für eingehenden Datenverkehr auszuwerten. Die gleichen Ansätze können verwendet werden, um eingehende Anforderungen für den Netzwerk Datenverkehr zu erfüllen und zu überprüfen Weitere Informationen finden Sie im Knowledge Base- [Artikel 929851: Der standardmäßige dynamische Port Bereich für TCP/IP hat sich in Windows Vista und Windows Server 2008](http://support.microsoft.com/kb/929851)geändert.

### <a name="bandwidth-needs"></a>Bandbreitenanforderungen

Die Planung der Netzwerk Skalierbarkeit umfasst zwei unterschiedliche Kategorien: die Menge an Datenverkehr und die CPU-Auslastung des Netzwerk Datenverkehrs. Jedes dieser Szenarien ist im Vergleich zu einigen anderen Themen in diesem Artikel geradlinig.

Wenn Sie bewerten möchten, wie viel Datenverkehr unterstützt werden muss, gibt es zwei eindeutige Kategorien der Kapazitätsplanung für AD DS in Bezug auf den Netzwerk Datenverkehr. Der erste ist der Replikations Datenverkehr, der zwischen Domänen Controllern durchläuft, und wird im Verweis [Active Directory Replikations Datenverkehr](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10)) gründlich behandelt und ist weiterhin für aktuelle Versionen von AD DS relevant. Die zweite ist der Client-zu-Server-Datenverkehr für den Standort. Eines der einfacheren Szenarios, bei denen der Standort interne Datenverkehr in Bezug auf die großen Datenmengen, die an die Clients zurückgesendet werden, überwiegend kleine Anforderungen von Clients empfängt. 100 MB sind im Allgemeinen in Umgebungen mit bis zu 5.000 Benutzern pro Server, an einem Standort, ausreichend. Die Verwendung eines 1-GB-Netzwerkadapters und der Unterstützung 5.000 für die Empfangs seitige Skalierung (Receive Side Scaling, RSS) wird für alle Benutzer Um dieses Szenario zu überprüfen, insbesondere im Fall von Server Konsolidierungs Szenarien, prüfen Sie die Netzwerk\*Schnittstelle () \ Bytes/Sek. über alle DCS an einem Standort hinweg, fügen Sie sie zusammen hinzu, und teilen Sie Sie durch die Ziel Anzahl von Domänen Controllern, um sicherzustellen, dass ist ausreichend Kapazität. Die einfachste Möglichkeit hierzu ist die Verwendung der Ansicht "Gestapelte Flächen" in der Windows-Zuverlässigkeits-und Leistungsüberwachung (früher als Perfmon bezeichnet), um sicherzustellen, dass alle Leistungsindikatoren gleich skaliert werden.

Sehen Sie sich das folgende Beispiel an (auch bekannt als eine wirklich komplexe Methode, um zu überprüfen, ob die allgemeine Regel auf eine bestimmte Umgebung anwendbar ist). Die folgenden Annahmen werden vorgenommen:

- Ziel ist es, den Bedarf auf so wenige Server wie möglich zu reduzieren. Im Idealfall wird ein Server den Ladevorgang ausführen, und ein zusätzlicher Server wird für Redundanz bereitgestellt (*N* + 1 Szenario). 
- In diesem Szenario unterstützt der aktuelle Netzwerkadapter nur 100 MB und befindet sich in einer umschanden Umgebung.  
  Die maximale Auslastung der Zielnetzwerk Bandbreite beträgt 60% in einem N-Szenario (Ausfall eines DC).
- Jeder Server verfügt über ungefähr 10.000 Clients, die mit ihm verbunden sind.

Informationen aus den Daten im Diagramm (Netzwerkschnittstelle (\*) \Gesendete Bytes/Sek.):

1. Der Geschäftstag beginnt um 5:30 Uhr und geht um 7:00 Uhr.
1. Der Haupt Zeitraum liegt zwischen 8:00 Uhr und 8:15 Uhr, wobei mehr als 25 Bytes pro Sekunde auf dem am stärksten ausgelasteten DC gesendet werden.  
   > [!NOTE]
   > Alle Leistungsdaten sind Verlaufs Daten. Der Spitzen Datenpunkt bei 8:15 gibt also die Last von 8:00 auf 8:15 an.
1. Es gibt Spitzen vor 4:00 Uhr, wobei mehr als 20 Bytes pro Sekunde auf dem am stärksten ausgelasteten DC gesendet werden. Dies kann darauf hindeuten, dass die Auslastung aus verschiedenen Zeitzonen oder aus einer Hintergrund Infrastruktur Aktivität, wie z. b. Sicherungen, Da der Höchstwert von 8:00 Uhr diese Aktivität überschreitet, ist er nicht relevant.
1. Am-Standort sind fünf Domänen Controller vorhanden.
1. Die maximale Auslastung beträgt ca. 5,5 MB/s pro DC, was 44% der 100 MB-Verbindung repräsentiert. Mithilfe dieser Daten kann geschätzt werden, dass die erforderliche Gesamtbandbreite zwischen 8:00 Uhr und 8:15 Uhr 28 MB/s beträgt.
   >[!NOTE]
   >Seien Sie vorsichtig mit der Tatsache, dass die Sende-/empfangsindikatoren der Netzwerkschnittstelle in Bytes vorliegen und die Netzwerkbandbreite in Bits gemessen wird. 100 MB &divide; 8 = 12,5 MB, 1 GB &divide; 8 = 128 MB.
  
Ergebnisse

1. Diese aktuelle Umgebung erfüllt die N + 1-Ebene der Fehlertoleranz bei einer Ziel Auslastung von 60%. Wenn ein System offline geschaltet wird, wird die Bandbreite pro Server um etwa 5,5 MB/s (44%) verlagert. auf ungefähr 7 MB/s (56%).
1. Basierend auf dem zuvor genannten Ziel der Konsolidierung auf einem Server überschreiten beide die maximale Ziel Auslastung und theoretisch die mögliche Auslastung einer 100 MB-Verbindung.
1. Bei einer Verbindung mit einer Größe von 1 GB stellt dies 22% der Gesamtkapazität dar.
1. Unter normalen Betriebsbedingungen im Szenario " *N* + 1" wird die Client Auslastung relativ gleichmäßig auf ungefähr 14 MB/s pro Server oder 11% der Gesamtkapazität verteilt.
1. Um sicherzustellen, dass die Kapazität während der Nichtverfügbarkeit eines DC ausreichend ist, liegen die normalen Betriebs Ziele pro Server bei etwa 30% der Netzwerk Auslastung oder 38 MB/s pro Server. Failoverziele sind 60% Netzwerk Auslastung oder 72 MB/s pro Server.  
  
Kurz gesagt, muss die endgültige Bereitstellung von Systemen über einen 1-GB-Netzwerkadapter verfügen und mit einer Netzwerkinfrastruktur verbunden sein, die die genannte Last unterstützt. Ein weiterer Hinweis ist, dass die CPU-Auslastung der Netzwerkkommunikation aufgrund der Menge an Netzwerk Datenverkehr erhebliche Auswirkungen haben kann und die maximale Skalierbarkeit von AD DS einschränken kann. Derselbe Prozess kann verwendet werden, um die Menge der eingehenden Kommunikation mit dem DC einzuschätzen. Aufgrund der vorherrschenden Datenverkehrs Überstellung in Bezug auf den eingehenden Datenverkehr ist es für die meisten Umgebungen eine akademische Übung. Sicherstellen, dass die Hardwareunterstützung für RSS in Umgebungen mit mehr als 5.000 Benutzern pro Server wichtig ist. Bei Szenarios mit hohem Netzwerk Datenverkehr kann der Ausgleich der interruptlast einen Engpass darstellen. Dies kann von der Prozessor-Interruptzeit\% (\*) erkannt werden, die nicht gleichmäßig auf die CPUs verteilt ist. RSS-fähige NICs können diese Einschränkung mindern und die Skalierbarkeit erhöhen.

> [!NOTE]
> Ein ähnlicher Ansatz kann verwendet werden, um die zusätzliche erforderliche Kapazität beim Konsolidieren von Rechenzentren zu schätzen oder einen Domänen Controller an einem Satelliten Standort abzukoppeln. Erfassen Sie einfach den ausgehenden und eingehenden Datenverkehr an Clients, und dies ist die Menge an Datenverkehr, die jetzt in den WAN-Verbindungen vorhanden ist.  
>  
> In einigen Fällen können Sie mehr Datenverkehr als erwartet erleben, weil der Datenverkehr langsamer ist, z. b. wenn die Zertifikats Überprüfung keine aggressiven Timeouts für das WAN erfüllt. Aus diesem Grund sollte die WAN-Größe und-Auslastung ein iterativer, kontinuierlicher Prozess sein.

### <a name="virtualization-considerations-for-network-bandwidth"></a>Überlegungen zur Virtualisierung der Netzwerkbandbreite

Es ist einfach, Empfehlungen für einen physischen Server zu erstellen: 1 GB für Server, die mehr als 5000 Benutzer unterstützen. Nachdem mehrere Gäste mit der Freigabe einer zugrunde liegenden virtuellen switchinfrastruktur begonnen haben, ist zusätzliche Aufmerksamkeit erforderlich, um sicherzustellen, dass der Host über ausreichend Netzwerkbandbreite verfügt, um alle Gäste des Systems zu unterstützen, und daher die zusätzliche strenge erfordert. Dabei handelt es sich nicht mehr um eine Erweiterung der Netzwerkinfrastruktur auf dem Host Computer. Dies gilt unabhängig davon, ob das Netzwerk den Domänen Controller einschließt, der als Gast eines virtuellen Computers auf einem Host ausgeführt wird und der Netzwerk Datenverkehr über einen virtuellen Switch oder direkt mit einem physischen Switch verbunden ist. Der virtuelle Switch ist nur eine weitere Komponente, in der uplinkportprofil die übertragene Datenmenge unterstützen muss. Daher sollte der physische Host physische Netzwerkadapter, der mit dem Switch verknüpft ist, die DC-Last und alle anderen Gäste unterstützen können, die den virtuellen Switch gemeinsam nutzen, der mit dem physischen Netzwerkadapter verbunden ist.

### <a name="calculation-summary-example"></a>Beispiel für Berechnungs Zusammenfassung

|System|Spitzen Bandbreite|
|-|-|
DC 1|6,5 MB/s|
DC 2|6,25 MB/s|
|DC 3|6,25 MB/s|
|DC 4|5,75 MB/s|
|DC 5|4,75 MB/s|
|Gesamt|28,5 MB/s|

**Empfohlen 72 MB/s @ no__t-0 (28,5 MB/s dividiert durch 40%)

|Anzahl der Zielsysteme|Gesamtbandbreite (von oben)|
|-|-|
|2|28,5 MB/s|
|Resultierender normales Verhalten|28,5 &divide; 2 = 14,25 MB/s|

Im Laufe der Zeit kann die Annahme, dass sich die Client Auslastung erhöht, und dieses Wachstum sollte so am besten wie möglich geplant werden. Der empfohlene Betrag für die Planung von ermöglicht ein geschätztes Wachstum des Netzwerkverkehrs von 50%.

## <a name="storage"></a>Speicher

Der Planungs Speicher besteht aus zwei Komponenten:

- Kapazität oder Speichergröße
- Leistung

Es wird viel Zeit und Dokumentation für die Kapazitätsplanung aufgewendet, sodass die Leistung häufig nicht übersehen wird. Mit den aktuellen Hardwarekosten sind die meisten Umgebungen nicht so groß, dass eine dieser Umgebungen wirklich von Bedeutung ist, und die Empfehlung, "in so viel RAM wie die Datenbankgröße" zu versetzen, deckt in der Regel den Rest ab, obwohl Sie für Satellitenstandorte in größerem Umfang außer Kraft gesetzt werden kann. Umgebungen.

### <a name="sizing"></a>Größenanpassung

#### <a name="evaluating-for-storage"></a>Auswerten von Speicher

Im Vergleich zu 13 Jahren, als Active Directory eingeführt wurde, ist eine Zeit, in der 4 GB-und 9-GB-Laufwerke die gängigste Laufwerk Größe waren, die Größenanpassung für Active Directory nicht sogar für alle größten Umgebungen in Erwägung gezogen. Mit den kleinsten verfügbaren Festplattengrößen im Bereich von 180 GB können das gesamte Betriebssystem, SYSVOL und NTDS. dit problemlos auf ein Laufwerk passen. Daher empfiehlt es sich, in diesem Bereich eine hohe Investition zu verwerfen.

Die einzige zu berücksichtigende Empfehlung besteht darin sicherzustellen, dass 110% der Größe von NTDS. dit verfügbar sind, um die Debug-Option zu aktivieren. Darüber hinaus sollten Sie für das Wachstum im Laufe der Lebensdauer der Hardware über die Hardware verfügen.

Der erste und wichtigste Aspekt ist die Auswertung der Größe von NTDS. dit und SYSVOL. Diese Messungen führen zu einer Größenanpassung der Festplatte und der RAM-Zuweisung. Aufgrund der (relativ) niedrigen Kosten dieser Komponenten muss die mathematische nicht streng und präzise sein. Informationen dazu, wie Sie diese für vorhandene und neue Umgebungen evaluieren, finden Sie in der [Datenspeicher](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961771(v=technet.10)) Reihe von Artikeln. Beachten Sie insbesondere die folgenden Artikel:

- **Für vorhandene Umgebungen &ndash;**  der Abschnitt "So aktivieren Sie die Protokollierung von Speicherplatz, der durch Defragmentierung freigegeben wird" im Artikel [Speicher Limits](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10)).
- In **neuen Umgebungen &ndash;**  wird im Artikel Vergrößerung [geschätzt für Active Directory Benutzer und Organisationseinheiten](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961779(v=technet.10))erläutert.

  > [!NOTE]
  > Die Artikel basieren auf Datengrößen Schätzungen, die zum Zeitpunkt der Veröffentlichung von Active Directory in Windows 2000 erstellt wurden. Verwenden Sie Objektgrößen, die die tatsächliche Größe von Objekten in Ihrer Umgebung widerspiegeln.

Beim Überprüfen vorhandener Umgebungen mit mehreren Domänen kann es Abweichungen in den Daten Bank Größen geben. Wenn dies zutrifft, verwenden Sie den kleinsten globalen Katalog (GC) und die nicht-GC-Größen.  

Die Datenbankgröße kann je nach Betriebssystemversion variieren. DCS, die frühere Betriebssysteme ausführen, wie z. b. Windows Server 2003, haben eine geringere Datenbankgröße als ein Domänen Controller, auf dem ein späteres Betriebssystem ausgeführt wird, wie z. b. Windows Server 2008 R2, insbesondere dann, wenn Features wie Active Directory Papierkorb oder

> [!NOTE]  
  >
>- Beachten Sie bei neuen Umgebungen, dass die Schätzungen in den Wachstumsschätzungen für Active Directory Benutzer und Organisationseinheiten darauf hindeuten, dass 100.000 Benutzer (in derselben Domäne) etwa 450 MB Speicherplatz beanspruchen. Beachten Sie, dass die aufgefüllten Attribute eine enorme Auswirkung auf den Gesamtbetrag haben können. Attribute werden für viele Objekte von Drittanbietern und Microsoft-Produkten, einschließlich Microsoft Exchange Server und lync, aufgefüllt. Eine Auswertung, die auf dem Portfolio der Produkte in der Umgebung basiert, wird bevorzugt, aber die Übung, bei der die Mathematik und das Testen auf genaue Schätzungen für alle außer den größten Umgebungen ausführlich erläutert werden, ist viel Zeit und Aufwand nicht besonders wichtig.
>- Stellen Sie sicher, dass 110% der Größe von NTDS. dit als freier Speicherplatz zur Verfügung stehen, um offline defragmentieren zu können, und planen Sie das Wachstum über eine drei bis fünf Jahre lange Hardware Lebensdauer. In Anbetracht der kostengünstigen Speicherung ist die Schätzung des Speichers um 300% die Größe der DIT als Speicher Belegung sicher, um das Wachstum zu unterstützen, und die potenzielle Notwendigkeit von Offline-Debug-Anforderungen.

#### <a name="virtualization-considerations-for-storage"></a>Überlegungen zur Virtualisierung für Storage

Verwenden Sie in einem Szenario, in dem mehrere VHD-Dateien (Virtual Hard Disk, virtuelle Festplatte) auf einem einzelnen Volume zugeordnet werden, einen Datenträger mit fester Größe von mindestens 210% (100% von DIT + 110% freier Speicherplatz), um sicherzustellen, dass ausreichend Speicherplatz reserviert ist.  

#### <a name="calculation-summary-example"></a>Beispiel für Berechnungs Zusammenfassung

|Aus Evaluierungsphase gesammelte Daten| |
|-|-|
|Größe von NTDS. dit|35 GB|
|Modifizierer, der die Offline-decofragmentierung zulässt|2.1|
|Gesamter Speicherplatz|73,5 GB|

> [!NOTE]
> Dieser Speicherplatz ist zusätzlich zu dem Speicherplatz erforderlich, der für SYSVOL, Betriebssystem, Auslagerungs Datei, temporäre Dateien, lokale zwischengespeicherte Daten (z. b. Installer-Dateien) und Anwendungen benötigt wird.

### <a name="storage-performance"></a>Speicherleistung

#### <a name="evaluating-performance-of-storage"></a>Auswerten der Leistung von Storage

Da sich die langsamste Komponente auf jedem Computer befindet, kann der Speicher die größten negativen Auswirkungen auf die Client Leistung haben. Für Umgebungen, die groß genug sind, für die die Empfehlungen für die RAM-Größenanpassung nicht möglich sind, können die Konsequenzen, die sich auf die Planung des Speicher Abbildes  Außerdem erhöhen die Komplexität und die Vielfalt der Speichertechnologie das Risiko eines Ausfalls, da die Relevanz von bewährten bewährten Methoden "Betriebssystem, Protokolle und Datenbank" auf separaten physischen Datenträgern in den nützlichen Szenarien eingeschränkt ist.  Dies liegt daran, dass die langfristige bewährte Vorgehensweise auf der Annahme basiert, dass es sich bei einem "Datenträger" um eine dedizierte Spindel handelt und dass die e/a-Vorgänge isoliert werden können.  Diese Annahmen, die diese true machen, sind mit der Einführung von nicht mehr relevant:

- Neue Speichertypen und virtualisierte und freigegebene Speicher Szenarien
- Freigegebene Spindeln in einem SAN (Storage Area Network)
- VHD-Datei in einem SAN oder im Netzwerk verbundenen Speicher
- Solid-State-Laufwerke
- Mehrstufige Speicher Architekturen (d. h. die SSD-Speicher Ebene, die größeren spinspinspeicher speichert)

Kurz gesagt: das Endziel aller Speicher Leistungs Bemühungen, unabhängig von der zugrunde liegenden Speicherarchitektur und dem Entwurf, besteht darin, sicherzustellen, dass die benötigte Menge an Eingabe-/Ausgabevorgängen pro Sekunde (IOPS) verfügbar ist und diese IOPS innerhalb eines akzeptablen Zeitraums stattfinden. . In diesem Abschnitt wird erläutert, wie Sie die AD DS Anforderungen des zugrunde liegenden Speichers auswerten, um sicherzustellen, dass Speicherlösungen ordnungsgemäß entworfen werden.  Angesichts der Variabilität der heutigen Speichertechnologien ist es am besten, mit den Speicheranbietern zusammenzuarbeiten, um angemessene IOPS zu gewährleisten.  Informationen zu Szenarien mit lokal angefügtem Speicher finden Sie in Anhang C. hier finden Sie grundlegende Informationen zum Entwerfen herkömmlicher lokaler Speicher Szenarien.  Diese Prinzipale sind in der Regel auf komplexere Speicherebenen anwendbar und unterstützen außerdem im Dialogfeld mit den Anbietern, die Back-End-Speicherlösungen unterstützen.

- Aufgrund der breiten Palette von verfügbaren Speicheroptionen empfiehlt es sich, das Fachwissen von Hardware Support Teams oder Lieferanten zu nutzen, um sicherzustellen, dass die jeweilige Lösung den Anforderungen AD DS entspricht. Die folgenden Zahlen sind die Informationen, die den Speicherspezialisten zur Verfügung gestellt werden.

Für Umgebungen, in denen die Datenbank zu groß ist, um im Arbeitsspeicher aufbewahrt zu werden, verwenden Sie die Leistungsindikatoren, um zu bestimmen, wie viel e/a unterstützt werden muss:

- LogicalDisk (\*) \Mittlere Sek./Lesevorgänge (z. b. wenn NTDS. dit auf dem Laufwerk D:/ Laufwerk lautet der vollständige Pfad LogicalDisk (D:) \ Mittlere Sek./Lesevorgänge).
- LogicalDisk (\*) \ Mittlere Sek./Schreibvorgänge
- LogicalDisk (\*) \ Mittlere Sek./Übertragung
- LogicalDisk (\*) \ Lesevorgänge/Sek.
- LogicalDisk (\*) \ Schreibvorgänge/Sek.
- LogicalDisk (\*) \ Übertragungen/Sek.

Diese sollten in Intervallen von 15/30/60 Minuten getestet werden, um die Anforderungen der aktuellen Umgebung zu messen.

#### <a name="evaluating-the-results"></a>Auswerten der Ergebnisse

> [!NOTE]
> Der Schwerpunkt liegt auf Lesevorgängen aus der Datenbank, da dies in der Regel die anspruchsvollste Komponente ist. die gleiche Logik kann auf Schreibvorgänge in die Protokolldatei angewendet werden, indem LogicalDisk ( *\<NTDS-Protokoll\>* ) \Durchschnittl. Sek./Schreibvorgang und LogicalDisk (*NTDS-\>Protokoll) \ Schreibvorgänge/Sek.):\<*
>  
> - LogicalDisk ( *\<NTDS\>* ) \Mittlere Sek./Lesevorgänge gibt an, ob der aktuelle Speicher ausreichend groß ist.  Wenn die Ergebnisse ungefähr gleich der Datenträger Zugriffszeit für den Daten Satztyp sind, ist LogicalDisk ( *\<NTDS\>* ) \ Reads/sec ein gültiges Measure.  Überprüfen Sie die Hersteller Spezifikationen für den Speicher auf dem Back-End, aber gute Bereiche für LogicalDisk ( *\<NTDS\>* ) \Durchschnittl Sek./Lesevorgänge lauten ungefähr wie folgt:
>   - 7200 – 9 bis 12,5 Millisekunden (MS)
>   - 10.000 – 6 bis 10 ms
>   - 15.000 – 4 bis 6 ms  
>   - SSD-– 1 bis 3 ms  
>   - >[!NOTE]
>     >Es gibt Empfehlungen, die angeben, dass die Speicherleistung bei 15ms bis 20 ms (abhängig von der Quelle) beeinträchtigt wird.  Der Unterschied zwischen den obigen Werten und den anderen Leitfäden besteht darin, dass die oben genannten Werte der normale Betriebsbereich sind.  Die anderen Empfehlungen sind Anleitungen zur Problembehandlung, um zu ermitteln, wann die Client Darstellung erheblich beeinträchtigt wird und bemerkbar wird.  Im Referenz Anhang C erhalten Sie eine genauere Erläuterung.
> - LogicalDisk ( *\<NTDS\>* ) \ Lesevorgänge/Sek. ist die Menge an e/a-Vorgängen, die ausgeführt wird.
>   - Wenn LogicalDisk ( *\<NTDS\>* ) \ Mittlere Sek./Lesevorgänge innerhalb des optimalen Bereichs für den Back-End-Speicher liegen, können LogicalDisk ( *\<NTDS\>* ) \ Lesevorgänge/Sek. verwendet werden, um die Größe des Speichers direkt zu speichern.
>   - Wenn LogicalDisk ( *\<NTDS\>* ) \ Mittlere Sek./Lesevorgänge nicht innerhalb des optimalen Bereichs für den Back-End-Speicher liegen, ist nach der folgenden Formel zusätzliche e/a-Vorgänge erforderlich:
>     > (Logischer Datenträger ( *\<NTDS\>* ) \Mittlere Sek./Lesevorgänge) &divide; (Datenträger Zugriff auf physische Daten &times; Träger) (LogicalDisk ( *\<NTDS\>* ) \Durchschnittl Sek./Lesevorgang)

Überlegungen:

- Beachten Sie Folgendes: Wenn der Server mit einem suboptimalen RAM konfiguriert ist, sind diese Werte zu Planungszwecken ungenau.  Sie werden fälschlicherweise auf der obersten Seite angezeigt und können weiterhin als Ungünstigster Fall verwendet werden.
- Das Hinzufügen/Optimieren von RAM führt zu einer Verringerung der Anzahl von Lese-e/a-Vorgängen (LogicalDisk ( *\<NTDS\>* ) \ Lesevorgänge/Sek.  Dies bedeutet, dass die Speicherlösung möglicherweise nicht so robust wie ursprünglich berechnet ist.  Leider ist alles, was spezifischer als diese allgemeine Erklärung ist, von der Client lastabhängig und kann nicht bereitgestellt werden.  Die beste Option besteht darin, die Speichergröße nach der Optimierung des RAM anzupassen.

#### <a name="virtualization-considerations-for-performance"></a>Überlegungen zur Virtualisierung hinsichtlich der Leistung

Ähnlich wie bei allen vorherigen virtualisierungsdiskussionen besteht der Schlüssel darin darin, sicherzustellen, dass die zugrunde liegende freigegebene Infrastruktur die DC-Last und die anderen Ressourcen unterstützt, die die zugrunde liegenden freigegebenen Medien und alle Pfade verwenden. Dies gilt unabhängig davon, ob ein physischer Domänen Controller die gleichen zugrunde liegenden Medien in einer San-, NAS-oder iSCSI-Infrastruktur wie andere Server oder Anwendungen gemeinsam verwendet, ob es sich um einen Gast mit Pass-Through-Zugriff auf eine San-, NAS-oder iSCSI-Infrastruktur handelt, die das zugrunde liegende Medien oder, wenn der Gast eine VHD-Datei verwendet, die sich lokal auf freigegebenen Medien oder eine San-, NAS-oder iSCSI-Infrastruktur befindet. Bei der Planungsübung geht es darum, sicherzustellen, dass die zugrunde liegenden Medien die Gesamtlast aller Consumer unterstützen können.

Aus Sicht des Gasts, da weitere Codepfade vorhanden sind, die durchlaufen werden müssen, wirkt sich dies auf die Leistung aus, wenn Sie einen Host für den Zugriff auf Speicher benötigen. Es ist nicht überraschend, dass Speicher Leistungstests darauf hindeuten, dass die Virtualisierung Auswirkungen auf den Durchsatz hat, der für die Prozessorauslastung des Host Systems subjektiv ist (siehe Anhang A: Kriterien für die CPU-Größe), die offensichtlich von den Ressourcen des Hosts beeinflusst werden, der vom Gast gefordert wird. Dies trägt zu den Überlegungen zur Virtualisierung in Bezug auf die Verarbeitungsanforderungen in einem virtualisierten Szenario bei. (Weitere Informationen finden Sie unter [Überlegungen zur Virtualisierung](#virtualization-considerations-for-processing)

Diese Komplexität zu vereinfachen, besteht darin, dass eine Vielzahl verschiedener Speicheroptionen verfügbar ist, die alle unterschiedliche Auswirkungen auf die Leistung haben. Verwenden Sie als sichere Schätzung bei der Migration von physisch zu virtuell einen Multiplikator von 1,10, um verschiedene Speicheroptionen für virtualisierte Gäste in Hyper-V anzupassen, z. b. Pass-Through-Speicher, SCSI-Adapter oder IDE. Die Anpassungen, die bei der Übertragung zwischen den verschiedenen Speicher Szenarien vorgenommen werden müssen, sind unerheblich, ob der Speicher lokal, San, NAS oder iSCSI ist.

#### <a name="calculation-summary-example"></a>Beispiel für Berechnungs Zusammenfassung

Ermitteln der Menge an e/a-Vorgängen, die für ein fehlerfreies System unter normalen Betriebsbedingungen erforderlich sind:

- LogicalDisk ( *\<NTDS-Daten\>Bank Laufwerk*) \ Übertragungen/Sek. während des Zeitraums von 15 Minuten 
- So bestimmen Sie die Menge an e/a-Vorgängen, die für den Speicher erforderlich sind
  >*Benötigtes IOPS* = (LogicalDisk *\<(NTDS-\>Daten Bank Laufwerk*) \Mittlere Sek. &divide; /Lesevorgänge/Lese &times; *\<Vorgänge für\>Mittlere Sek./Lese* Vorgänge) LogicalDisk ( *\< NTDS-Daten\>Bank Laufwerk*) \ Lesevorgänge/Sek.

|Indikator|Wert|
|-|-|
|Tatsächlicher LogicalDisk ( *\<NTDS-\>Daten Bank Laufwerk*) \ Mittlere Sek./Übertragung|.02 Sekunden (20 Millisekunden)|
|Ziel LogicalDisk ( *\<NTDS-Daten\>Bank Laufwerk*) \ Mittlere Sek./Übertragung|.01 Sekunden|
|Multiplikator für Änderung in verfügbarem e/a|0,02 &divide; 0,01 = 2|  
  
|Wertname|Wert|
|-|-|
|LogicalDisk ( *\<NTDS-Daten\>Bank Laufwerk*) \ Übertragungen/Sek.|400|
|Multiplikator für Änderung in verfügbarem e/a|2|
|Erforderliche IOPS-Gesamtzeit|800|

So bestimmen Sie die Rate, mit der der Cache erwärmt werden soll:

- Bestimmen Sie die maximal zulässige Zeit zum Aufwärmen des Caches. Es ist entweder die Zeitspanne, die es dauert, bis die gesamte Datenbank vom Datenträger geladen wird, oder in Szenarios, in denen die gesamte Datenbank nicht in den RAM geladen werden kann, ist dies die maximale Zeit zum Auffüllen des RAM.
- Bestimmen Sie die Größe der Datenbank, ausgenommen Leerraum.  Weitere Informationen finden Sie unter [Auswerten von Speicher](#evaluating-for-storage).  
- Dividieren Sie die Datenbankgröße um 8 KB. Dies ist die Gesamtsumme, die zum Laden der Datenbank erforderlich ist.
- Dividieren Sie die Gesamtzahl von IOS durch die Anzahl der Sekunden im definierten Zeitraum.

Beachten Sie, dass die berechnete Rate nicht exakt ist, weil zuvor geladene Seiten entfernt werden, wenn ESE nicht für eine festgelegte Cache Größe konfiguriert ist, und AD DS standardmäßig die Variable Cache Größe verwendet.

|Zu sammelnde Datenpunkte|Werte
|-|-|
|Maximal zulässige Zeit zum Aufwärmen|10 Minuten (600 Sekunden)
|Datenbankgröße|2 GB|  
  
|Berechnungsschritt|Formula|Ergebnis|
|-|-|-|
|Berechnen der Größe der Datenbank auf Seiten|(2 GB &times; 1024 &times; 1024) = *Größe der Datenbank in KB*|2\.097.152 KB|
|Berechnen der Anzahl von Seiten in der Datenbank|2\.097.152 KB &divide; 8 KB = *Anzahl von Seiten*|262.144 Seiten|
|Berechnen von IOPS, die zum vollständigen Aufwärmen des Caches erforderlich sind|262.144 Seiten &divide; 600 Sekunden = *IOPS erforderlich*|437 IOPS|

## <a name="processing"></a>Verarbeitung

### <a name="evaluating-active-directory-processor-usage"></a>Auswerten der Active Directory Prozessorauslastung

In den meisten Umgebungen werden Speicher, RAM und Netzwerke gemäß der Beschreibung im Abschnitt "Planung" ordnungsgemäß optimiert, und die Verwaltung der Verarbeitungskapazität ist die Komponente, die die größte Aufmerksamkeit verdient. Bei der Auswertung der benötigten CPU-Kapazität gibt es zwei Herausforderungen:

- Unabhängig davon, ob sich die Anwendungen in der Umgebung in einer gemeinsamen Dienst Infrastruktur gut Verhalten, und wird im Abschnitt "nachverfolgen kostspieliger und ineffizienter Suchvorgänge" im Artikel Erstellen von effizienterem Microsoft Active behandelt. Verzeichnis aktivierte Anwendungen oder Migrieren von untergeordneten Sam-Aufrufen von LDAP-aufrufen.  
  
  In größeren Umgebungen ist es wichtig, dass schlecht codierte Anwendungen Schwankungen bei der CPU-Auslastung erreichen, eine übermäßig große CPU-Zeit von anderen Anwendungen stehlen, Kapazitätsanforderungen künstlich erhöhen und die Last gleichmäßig verteilen. die DCS.  
- Da AD DS eine verteilte Umgebung mit einer Vielzahl potenzieller Clients ist, ist das Einschätzen der Kosten eines "einzelnen Clients" aufgrund von Verwendungs Mustern und dem Typ oder der Anzahl von Anwendungen, die AD DS nutzen, umweltfreundlich. Kurz gesagt, ähnlich wie im Abschnitt "Netzwerk", ist dies für eine umfassende Anwendbarkeit besser von der Perspektive der Auswertung der Gesamtkapazität, die in der Umgebung benötigt wird.

Für vorhandene Umgebungen, wie die Speichergrößen Änderung bereits erläutert wurde, wird davon ausgegangen, dass der Speicher nun ordnungsgemäß dimensioniert ist und daher die Daten bezüglich der Prozessorauslastung gültig sind. Zur Wiederholung ist es wichtig, sicherzustellen, dass der Engpass im System nicht die Leistung des Speichers darstellt. Wenn ein Engpass vorhanden ist und der Prozessor wartet, gibt es Status im Leerlauf, die nach dem Entfernen des Engpasses entfernt werden.  Da die Warte Zustände des Prozessors entfernt werden, erhöht sich die CPU-Auslastung definitionsgemäß, da Sie nicht mehr auf die Daten warten muss. Erfassen Sie daher Leistungsindikatoren "logischer Datenträger ( *\<ntds-Daten Bank Laufwerk @ no__t-2*) \Durchschnittl Sek./Lesevorgang" und "Prozess (LSASS) \\% Prozessorzeit". Die Daten in "Process (LSASS) \\% Prozessorzeit" sind künstlich niedrig, wenn "logischer Datenträger ( *\<ntds-Daten Bank Laufwerk @ no__t-3*) \Mittlere Sek./Lesevorgänge" 10 bis 15 ms überschreitet. Dies ist ein allgemeiner Schwellenwert, den der Microsoft-Support für die Problembehandlung verwendet. Leistungsprobleme im Zusammenhang mit dem Speicher. Wie zuvor wird empfohlen, dass es sich bei den Beispiel Intervallen um 15, 30 oder 60 Minuten handelt. Für gute Messungen sind normalerweise weniger als flüchtig. alles höhere wird die tägliche anwirkung übermäßig stark glätten.

### <a name="introduction"></a>Einführung

Um die Kapazitätsplanung für Domänen Controller zu planen, erfordert die Verarbeitungsleistung die meiste Aufmerksamkeit und das Verständnis. Bei der Größenanpassung von Systemen zur Sicherstellung der maximalen Leistung gibt es immer eine Komponente, die den Engpass darstellt. bei einem Domänen Controller mit ordnungsgemäßer Größe handelt es sich hierbei um den Prozessor.

Ähnlich wie im Abschnitt "Netzwerk", in dem die Nachfrage der Umgebung auf Site-an-Site-Basis überprüft wird, muss dies für die geforderte computekapazität erfolgen. Im Gegensatz zum Abschnitt Netzwerk, in dem die verfügbaren Netzwerktechnologien den normalen Bedarf nicht überschreiten, achten Sie auf die Größenanpassung der CPU-Kapazität.  Als jede Umgebung, die sogar mittelgroß ist; alle über ein paar tausend gleichzeitigen Benutzer können eine beträchtliche Auslastung der CPU mit sich bringen.

Leider ist aufgrund der großen Variabilität von Client Anwendungen, die AD nutzen, eine allgemeine Schätzung von Benutzern pro CPU für alle Umgebungen nicht zutreffend. Insbesondere unterliegen die computeanforderungen dem Benutzer Verhalten und dem Anwendungsprofil. Daher muss jede Umgebung einzeln skaliert werden.

#### <a name="target-site-behavior-profile"></a>Verhaltensprofil für Ziel Standort

Wie bereits erwähnt, ist das Ziel, beim Planen der Kapazität für einen gesamten Standort einen Entwurf mit einem Kapazitäts Entwurf von *N* + 1 als Ziel festzustellen, sodass der Ausfall eines Systems während des Spitzen Zeitraums für die Fortsetzung des dienplatzes auf einer angemessenen Qualität ermöglicht wird. Dies bedeutet, dass in einem "*N*"-Szenario das Laden in alle Felder weniger als 100% betragen muss (besser als 80%). während der Spitzenzeiten.

Wenn außerdem die Anwendungen und Clients am Standort bewährte Methoden für die Suche nach Domänen Controllern verwenden (d. h. mit der [DsGetDcName-Funktion](http://msdn.microsoft.com/en-us/library/windows/desktop/ms675983(v=vs.85).aspx)), sollten die Clients aufgrund beliebiger Anzahl der Faktoren.

Im nächsten Beispiel werden folgende Annahmen getroffen:

- Jeder der fünf DCS an der Site hat vier CPUs.
- Die Gesamtauslastung der Ziel-CPU während der Geschäftszeiten beträgt 40% unter normalen Betriebsbedingungen ("*n* + 1") und 60% andernfalls ("*n*"). Außerhalb der Geschäftszeiten beträgt die CPU-Ziel Auslastung 80%, da von der Sicherungssoftware und anderen Wartungsarbeiten erwartet wird, dass alle verfügbaren Ressourcen genutzt werden.

![Diagramm der CPU-Auslastung](media/capacity-planning-considerations-cpu-chart.png)

Analysieren der Daten im Diagramm (Prozessor Informationen (_Total) \%-Prozessor Dienstprogramm) für die einzelnen DCS:

- Die Auslastung ist größtenteils gleichmäßig verteilt, was zu erwarten ist, wenn der Domänen Controller-Serverlocatorpunkt von den Clients verwendet wird und gut geschriebene Suchvorgänge vorliegen. 
- Es gibt eine Reihe von fünfminütigen Spitzen von 10%, wobei einige bis zu 20% groß sind. Im Allgemeinen ist es nicht lohnenswert, das Kapazitätsplan Ziel zu überschreiten.  
- Der Spitzen Zeitraum für alle Systeme liegt zwischen etwa 8:00 Uhr und 9:15 Uhr. Durch den reibungslosen Übergang von ungefähr 5:00 Uhr bis etwa 5:00 Uhr ist dies im Allgemeinen ein Hinweis auf den Geschäftsbereich. Die eher zufälligen Spitzen der CPU-Auslastung in einem Box-by-Box-Szenario zwischen 5:00 Uhr und 4:00 Uhr liegen außerhalb der Kapazitäts Planungsprobleme.

  >[!NOTE]
  >Bei einem gut verwalteten System sind die Spitzen möglicherweise Sicherungssoftware, die ausgeführt wird, vollständige systemantivirussoscans, Hardware-oder Software Inventur, Software-oder Patchbereitstellung usw. Da Sie außerhalb des Geschäftszyklen für den Hauptbenutzer liegen, werden die Ziele nicht überschritten.

- Da jedes System ungefähr 40% beträgt und alle Systeme über die gleiche Anzahl von CPUs verfügen, wenn ein System ausfällt oder offline geschaltet werden soll, werden die restlichen Systeme mit einem geschätzten 53% ausgeführt (die Auslastung von System D 40% wird gleichmäßig aufgeteilt und zu System a und System 40 C hinzugefügt. Aus verschiedenen Gründen ist diese lineare Annahme nicht ganz genau, sondern bietet ausreichend Genauigkeit für die Messung.  

  **Alternatives Szenario –** Zwei Domänen Controller, die auf 40% ausgeführt werden: Bei einem Domänen Controller ist ein Fehler aufgetreten. die geschätzte CPU auf der restlichen CPU ist ein geschätzter 80%. Dies überschreitet die oben beschriebenen Schwellenwerte für den Kapazitätsplan und beginnt, die Menge des Hauptraums für die 10% auf 20% im obigen Lade Profil erheblich einzuschränken. Dies bedeutet, dass die Spitzen den Domänen Controller während des "*N*"-Szenarios auf 90% bis 100% und de die Reaktionsfähigkeit wird endgültig deaktiviert.

### <a name="calculating-cpu-demands"></a>Berechnen von CPU-Anforderungen

Der Leistungs Objekt-Leistungs Objektwert "Process @ no__t-0% Processor Time" summiert die Gesamtzeit, die alle Threads einer Anwendung für die CPU aufwenden, und dividiert durch die Gesamtmenge der bestandenen Systemzeit. Dies hat zur Folge, dass eine Multithread-Anwendung auf einem Multi-CPU-System eine CPU-Zeit von 100% überschreiten kann und sehr anders interpretiert wird als "Prozessor Informationen @ no__t-0% Processor Utility". In der Praxis kann der Prozess (LSASS) \\% Prozessorzeit als Anzahl der CPUs mit 100% angezeigt werden, die zur Unterstützung der Anforderungs Anforderungen erforderlich sind. Der Wert 200% bedeutet, dass 2 CPUs, jeweils um 100%, erforderlich sind, um die vollständige AD DS Last zu unterstützen. Obwohl eine CPU mit einer Kapazität von 100% die kostengünstigste ist, aus der Perspektive von Geld für CPUs und Stromversorgung und Energieverbrauch, erfolgt aus verschiedenen Gründen, die in Anhang a ausführlich beschrieben werden, eine bessere Reaktionsfähigkeit auf einem Multithread-System, wenn das System wird nicht um 100% ausgeführt.

Zur Unterstützung vorübergehender Spitzen bei der Client Auslastung empfiehlt es sich, eine Spitzenzeit-CPU von zwischen 40% und 60% der Systemkapazität als Ziel zu erreichen. Wenn Sie mit dem obigen Beispiel arbeiten, bedeutet dies, dass zwischen 3,33 (60% Target) und 5 (40% Ziel) CPUs für die AD DS-Auslastung (LSASS-Prozess) benötigt werden. Zusätzliche Kapazität sollte gemäß den Anforderungen des Basis Betriebssystems und anderen erforderlichen Agents (z. b. Antivirus, Sicherung, Überwachung usw.) hinzugefügt werden. Obwohl die Auswirkung von Agents pro Umgebung ausgewertet werden muss, kann eine Schätzung zwischen 5% und 10% einer einzelnen CPU vorgenommen werden. Im aktuellen Beispiel würde dies darauf hindeuten, dass bei Spitzenzeiten zwischen 3,43-CPUs (60% Target) und 5,1-CPUs (40% Ziel) erforderlich sind.

Die einfachste Möglichkeit hierzu ist die Verwendung der Ansicht "Gestapelte Flächen" in der Windows-Zuverlässigkeits-und Leistungsüberwachung (Perfmon), um sicherzustellen, dass alle Indikatoren gleich skaliert werden.

Annahmen:

- Ziel ist es, den Bedarf auf so wenige Server wie möglich zu reduzieren. Im Idealfall würde ein Server den Ladevorgang und einen zusätzlichen Server für Redundanz hinzufügen (*N* + 1 Szenario).

![Prozessorzeit Diagramm für LSASS-Prozess (über alle Prozessoren)](media/capacity-planning-considerations-proc-time-chart.png)

Informationen aus den Daten im Diagramm (Prozess (LSASS) \\% Prozessorzeit):

- Der Geschäftstag beginnt um 7:00 Uhr und sinkt um 5:00 Uhr.
- Der Haupt Zeitraum liegt zwischen 9:30 Uhr und 11:00 Uhr. 
  > [!NOTE]
  > Alle Leistungsdaten sind Verlaufs Daten. Der Spitzen Datenpunkt bei 9:15 gibt die Last von 9:00 auf 9:15 an.
- Es gibt Spitzen vor 7:00 Uhr, die entweder aus unterschiedlichen Zeitzonen oder Hintergrund Infrastrukturaktivitäten, z. b. Sicherungen, anzeigen können. Da der Höchstwert bei 9:30 Uhr diese Aktivität überschreitet, ist er nicht relevant.
- Es gibt drei Domänen Controller am-Standort.

Bei maximaler Auslastung verbraucht LSASS ungefähr 485% einer CPU oder 4,85 CPUs, die bei 100% ausgeführt werden. Wie bei der vorherigen Mathematik bedeutet dies, dass für die Website etwa 12,25 CPUs für AD DS erforderlich sind. Fügen Sie in den obigen Vorschlägen 5% bis 10% für Hintergrundprozesse hinzu. das heißt, dass das Ersetzen des Servers heute ungefähr 12,30 bis 12,35 CPUs benötigen würde, um dieselbe Last zu unterstützen. Eine Umwelt Schätzung für das Wachstum muss nun in berücksichtigt werden.

### <a name="when-to-tune-ldap-weights"></a>Zeitpunkt der Optimierung von LDAP-Gewichtungen

Es gibt verschiedene Szenarien, in denen die Optimierung von [LdapSrvWeight](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc957291(v=technet.10)) berücksichtigt werden sollte. Im Zusammenhang mit der Kapazitätsplanung erfolgt dies, wenn die Anwendungs-oder Benutzer Auslastung nicht gleichmäßig ausgeglichen ist oder die zugrunde liegenden Systeme nicht gleichmäßig in Bezug auf die Funktion ausgeglichen werden. Mögliche Gründe für die Kapazitätsplanung sind der Rahmen dieses Artikels.

Es gibt zwei Häufige Gründe, um LDAP-Gewichtungen zu optimieren:

- Der PDC-Emulator ist ein Beispiel, das sich auf jede Umgebung auswirkt, für die das Ladeverhalten von Benutzern oder Anwendungen nicht gleichmäßig verteilt ist. Wenn bestimmte Tools und Aktionen auf den PDC-Emulator abzielen, z. b. die Gruppenrichtlinie Verwaltungs Tools, bei Authentifizierungs Fehlern, bei der Vertrauensstellung usw., werden CPU-Ressourcen auf dem PDC-Emulator möglicherweise stärker gefordert als an anderer Stelle in die Site.
  - Es ist nur hilfreich, dies zu optimieren, wenn es einen spürbaren Unterschied in der CPU-Auslastung gibt, um die Last auf dem PDC-Emulator zu verringern und die Last auf anderen Domänen Controllern zu erhöhen, was eine gleichmäßige Verteilung der Last ermöglicht.
  - Legen Sie in diesem Fall LdapSrvWeight zwischen 50 und 75 für den PDC-Emulator fest.
- Server mit unterschiedlicher Anzahl von CPUs (und Geschwindigkeiten) an einem Standort.  Angenommen, es gibt 2 8-Kernserver und 1 4-Core-Server.  Der letzte Server verfügt über die Hälfte der Prozessoren der anderen beiden Server.  Dies bedeutet, dass die durchschnittliche CPU-Auslastung im vier Kern-Feld durch eine gut verteilte Client Auslastung ungefähr doppelt so groß wie die acht Kern Felder erhöht wird.
  - Beispielsweise würden die 2 8-Kern-Felder bei 40% ausgeführt werden, und die vier Kerne werden bei 80% ausgeführt.
  - Beachten Sie auch, dass in diesem Szenario die Auswirkungen des Verlusts von 1 8-Core in diesem Szenario berücksichtigt werden, insbesondere die Tatsache, dass das Feld mit vier Kernen nun überladen ist.

#### <a name="example-1---pdc"></a>Beispiel 1: PDC

| |Verwendung mit Standardwerten|Neues LdapSrvWeight|Geschätzte neue Auslastung|
|-|-|-|-|
|DC 1 (PDC-Emulator)|53%|57|40 %|
|DC 2|33%|100|40 %|
|DC 3|33%|100|40 %|

Wenn die PDC-Emulatorrolle übertragen oder übernommen wird (insbesondere an einen anderen Domänen Controller am Standort), wird der neue PDC-Emulator dadurch drastisch vergrößert.

Mit dem Beispiel aus dem [Profil "Ziel Standort Verhalten](#target-site-behavior-profile)" wurde angenommen, dass alle drei Domänen Controller am Standort über vier CPUs verfügten. Was sollte unter normalen Bedingungen geschehen, wenn einer der Domänen Controller über acht CPUs verfügte? Es gibt zwei Domänen Controller mit einer Auslastung von 40% und eine Auslastung von 20%. Obwohl dies nicht schlecht ist, besteht die Möglichkeit, die Last etwas besser auszugleichen. Nutzen Sie LDAP-Gewichtungen, um dies zu erreichen.  Ein Beispielszenario wäre:

#### <a name="example-2---differing-cpu-counts"></a>Beispiel 2: abweichende CPU-Anzahl

| |Prozessor Informationen @ no__t-0 @ no__t-1 @ no__t-2processor Utility (_Total)<br />Verwendung mit Standardwerten|Neues LdapSrvWeight|Geschätzte neue Auslastung|
|-|-|-|-|
|4-CPU-DC 1|40|100|30 %|
|4-CPU-DC 2|40|100|30 %|
|8-CPU-DC 3|20|200|30 %|

Seien Sie jedoch mit diesen Szenarien sehr vorsichtig. Wie oben zu sehen ist, sieht die Mathematik wirklich schön und sehr gut aus. Aber in diesem Artikel ist die Planung eines "*N* + 1"-Szenarios von größter Wichtigkeit. Die Auswirkung eines Domänen Controllers, der offline geschaltet wird, muss für jedes Szenario berechnet werden. In dem unmittelbar vorhergehenden Szenario, in dem die Lastverteilung gerade erfolgt, um eine Auslastung von 60% während eines "*N*"-Szenarios zu gewährleisten, während der Lastenausgleich gleichmäßig auf alle Server verteilt ist, ist die Verteilung in Ordnung, da die Verhältnisse konsistent bleiben. Wenn Sie sich das Optimierungs Szenario für den PDC-Emulator ansehen und im allgemeinen jedes Szenario, in dem die Benutzer-oder Anwendungs Last nicht ausgeglichen ist, ist der Effekt sehr unterschiedlich:

| |Optimierte Auslastung|Neues LdapSrvWeight|Geschätzte neue Auslastung|
|-|-|-|-|
|DC 1 (PDC-Emulator)|40 %|85|47%|
|DC 2|40 %|100|53%|
|DC 3|40 %|100|53%|

### <a name="virtualization-considerations-for-processing"></a>Überlegungen zur Virtualisierung für die Verarbeitung

Es gibt zwei Ebenen der Kapazitätsplanung, die in einer virtualisierten Umgebung ausgeführt werden müssen. Auf Hostebene müssen, ähnlich wie bei der Identifizierung des Geschäftsprozesses, der zuvor für die Verarbeitung des Domänen Controllers festgelegt wurde, Schwellenwerte während des Spitzen Zeitraums identifiziert werden. Da die zugrunde liegenden Prinzipale für einen Host Computer identisch sind, der Gast-Threads auf der CPU plant, wie zum AD DS von Threads auf der CPU auf einem physischen Computer, wird das gleiche Ziel von 40% bis 60% auf dem zugrunde liegenden Host empfohlen. Auf der nächsten Ebene verbleibt die Gast Schicht, da sich die Prinzipale der Thread Planung nicht geändert haben, das Ziel innerhalb des Gasts im Bereich von 40% bis 60%.

In einem direkt zugeordneten Szenario, einem Gast pro Host, muss die gesamte Kapazitätsplanung bis zu diesem Punkt den Anforderungen (RAM, Datenträger, Netzwerk) des zugrunde liegenden Host Betriebssystems hinzugefügt werden. In einem Szenario mit einem freigegebenen Host gibt das Testen an, dass die Effizienz der zugrunde liegenden Prozessoren 10% beeinträchtigt. Dies bedeutet, dass bei einem Standort, der 10 CPUs mit einem Ziel von 40% benötigt, die empfohlene Menge an virtuellen CPUs, die allen "*N*" Gästen zuzuordnen sind, 11 betragen würde. An einem Standort mit gemischter Verteilung physischer Server und virtueller Server gilt der-Modifizierer nur für die VMs. Wenn eine Website beispielsweise ein Szenario "*N* + 1" aufweist, ist ein physischer oder direkt zugeordneter Server mit 10 CPUs ungefähr gleichwertig mit einem Gast mit 11 CPUs auf einem Host, wobei 11 CPUs für den Domänen Controller reserviert sind.

Während der Analyse und Berechnung der CPU-Mengen, die für die Unterstützung der AD DS Last erforderlich sind, wird die Anzahl der CPUs, die dem entspricht, was bei physischer Hardware erworben werden kann, nicht notwendigerweise ordnungsgemäß zugeordnet. Durch die Virtualisierung ist das Aufrunden nicht mehr erforderlich. Durch die Virtualisierung wird der Aufwand verringert, der zum Hinzufügen von computekapazität zu einem Standort erforderlich ist, wenn eine CPU zu einer VM hinzugefügt werden kann. Dadurch entfällt die Notwendigkeit, die erforderliche computeleistung genau auszuwerten, sodass die zugrunde liegende Hardware verfügbar ist, wenn den Gästen zusätzliche CPUs hinzugefügt werden müssen.  Denken Sie daran, die Bedarfs gesteuerte Vergrößerung zu planen und zu überwachen.

### <a name="calculation-summary-example"></a>Beispiel für Berechnungs Zusammenfassung

|System|CPU-Spitzen Auslastung|
|-|-|-|
|DC 1|120%|
|DC 2|147%|
|DC 3|218%|
|Gesamte verwendete CPU|485%|  
  
|Anzahl der Zielsysteme|Gesamtbandbreite (von oben)|
|-|-|
|Erforderliche CPUs bei 40%-Ziel|4,85 &divide; . 4 = 12,25|

Wenn Sie sich aufgrund der Wichtigkeit dieses Punkts wiederholen, *denken Sie daran, das Wachstum zu planen*. Wenn in den nächsten drei Jahren 50% zugenommen, benötigt diese Umgebung 18,375 CPUs (12,25 &times; 1,5) an der dreijährigen Markierung. Ein alternativer Plan wäre, nach dem ersten Jahr zu prüfen und bei Bedarf zusätzliche Kapazität hinzuzufügen.

### <a name="cross-trust-client-authentication-load-for-ntlm"></a>Vertrauenswürdige Client Authentifizierungs Last für NTLM

#### <a name="evaluating-cross-trust-client-authentication-load"></a>Auswerten der vertrauenswürdigen Client Authentifizierungs Last

Viele Umgebungen haben möglicherweise eine oder mehrere Domänen, die über eine Vertrauensstellung verbunden sind. Eine Authentifizierungsanforderung für eine Identität in einer anderen Domäne, die nicht die Kerberos-Authentifizierung verwendet, muss eine Vertrauensstellung durchlaufen, indem der sichere Kanal des Domänen Controllers zu einem anderen Domänen Controller entweder in der Zieldomäne oder in der nächsten Domäne im Pfad verwendet wird. in die Zieldomäne. Die Anzahl gleichzeitiger Aufrufe mithilfe des sicheren Kanals, den ein Domänen Controller für einen Domänen Controller in einer vertrauenswürdigen Domäne ausführen kann, wird durch eine Einstellung, die als **MaxConcurrentApi**bezeichnet wird, gesteuert. Bei Domänen Controllern kann sichergestellt werden, dass der sichere Kanal den Lade Aufwand für einen von zwei Ansätzen erreicht: Optimieren von **MaxConcurrentApi** oder innerhalb einer Gesamtstruktur, Erstellen von Verknüpfungs Vertrauensstellungen. Informationen zum Messen des Datenverkehrs Volumens über eine individuelle Vertrauensstellung finden Sie unter [Verwenden der Leistungsoptimierung für die NTLM-Authentifizierung mithilfe der Einstellung "MaxConcurrentApi](https://support.microsoft.com/kb/2688798)".

Während der Datensammlung muss dieser, wie in allen anderen Szenarien, während der Spitzenzeiten des Tages gesammelt werden, damit die Daten nützlich sind.

> [!NOTE]
> In der Gesamtstruktur und in den Gesamtstruktur übergreifenden Szenarien kann die Authentifizierung mehrere Vertrauens Stellungen durchlaufen, und jede Phase muss optimiert werden.

#### <a name="planning"></a>Planen

Es gibt eine Reihe von Anwendungen, die standardmäßig die NTLM-Authentifizierung verwenden, oder Sie verwenden Sie in einem bestimmten Konfigurations Szenario. Anwendungsserver wachsen in der Kapazität und bedienen eine wachsende Anzahl aktiver Clients. Es gibt auch einen Trend, dass Clients die Sitzungen für einen begrenzten Zeitraum offen halten und stattdessen regelmäßig eine Verbindung herstellen (z. b. e-Mail-Pull Sync). Ein weiteres häufiges Beispiel für eine hohe NTLM-Auslastung sind WebProxy Server, für die eine Authentifizierung für den Internet Zugriff erforderlich ist.

Diese Anwendungen können eine beträchtliche Auslastung für die NTLM-Authentifizierung verursachen. Dies kann zu erheblichen Belastungen bei den DCS führen, insbesondere wenn sich Benutzer und Ressourcen in verschiedenen Domänen befinden.

Es gibt mehrere Ansätze für die Verwaltung von vertrauenswürdiger Auslastung, die in der Praxis anstelle eines exklusiven entweder/oder-Szenarios verwendet wird. Folgende Optionen sind möglich:

- Reduzieren Sie die vertrauenswürdige Client Authentifizierung, indem Sie die Dienste suchen, die ein Benutzer in derselben Domäne verwendet, in der sich der Benutzer befindet.
- Erhöhen Sie die Anzahl der verfügbaren sicheren Channels. Dies ist für den Gesamtstruktur-und Gesamtstruktur übergreifenden Datenverkehr relevant und wird als Verknüpfungs Vertrauensstellungen bezeichnet.
- Optimieren Sie die Standardeinstellungen für **MaxConcurrentApi**.

Zum Optimieren von **MaxConcurrentApi** auf einem vorhandenen Server lautet die Gleichung:

> *New_MaxConcurrentApi_setting* &ge; (*semaphore_acquires*  +  *semaphore_time-outs*) &times; *average_semaphore_hold_time* &divide; *time_collection_length*

Weitere Informationen finden [Sie im KB-Artikel 2688798: So führen Sie die Leistungsoptimierung für die NTLM-Authentifizierung mithilfe der Einstellung](http://support.microsoft.com/kb/2688798)"MaxConcurrentApi" aus

## <a name="virtualization-considerations"></a>Virtualisierung: Überlegungen

Keine, dies ist eine Optimierungs Einstellung für das Betriebssystem.

### <a name="calculation-summary-example"></a>Beispiel für Berechnungs Zusammenfassung

|Datentyp|Wert|
|-|-|
|Semaphore (minimal)|6\.161|
|Semaphore erhält (Maximum)|6\.762|
|Semaphore-Timeouts|0|
|Durchschnittliche Semaphore-Haltezeit|0,012|
|Sammlungs Dauer (Sekunden)|1:11 Minuten (71 Sekunden)|
|Formel (aus KB 2688798)|((6762 &ndash; 6161) + 0) &times; 0,012/|
|Minimalwert für " **MaxConcurrentApi** "|((6762 &ndash; 6161) + 0) &times; 0,012 &divide; 71 =. 101|

Für dieses System sind die Standardwerte zulässig.

## <a name="monitoring-for-compliance-with-capacity-planning-goals"></a>Überwachen der Konformität mit Kapazitäts Planungszielen

In diesem Artikel wurde erläutert, dass die Planung und Skalierung zu Verwendungs Zielen geführt hat. Im folgenden finden Sie ein Übersichts Diagramm der empfohlenen Schwellenwerte, die überwacht werden müssen, um sicherzustellen, dass die Systeme innerhalb von ausreichenden Kapazitäts Schwellenwerten betrieben werden. Beachten Sie, dass es sich hierbei nicht um Leistungs Schwellenwerte, sondern um Schwellenwerte zur Kapazitätsplanung handelt. Ein Server, der über diese Schwellenwerte hinausgeht, funktioniert, ist jedoch Zeit, zu überprüfen, ob alle Anwendungen gut funktionieren. Wenn die genannten Anwendungen gut funktionieren, ist es an der Zeit, mit der Bewertung von Hardware Upgrades oder anderen Konfigurationsänderungen zu beginnen.

|Kategorie|Leistungs Zählers|Intervall/Stichprobenentnahme|Ziel|Warnung|
|-|-|-|-|-|
|Prozessor|Prozessor Informationen (_Total) \\% Prozessor Dienstprogramm|60 min.|40 %|60 %|
|RAM (Windows Server 2008 R2 oder früher)|Speicher \ verfügbare MB|< 100 MB|Nicht zutreffend|< 100 MB|
|RAM (Windows Server 2012)|Memory\langterm durchschnittliche standbycache-Lebensdauer (n)|30 Minuten|Muss getestet werden|Muss getestet werden|
|Network|Netzwerkschnittstelle (\*) \Gesendete Bytes/Sek.<br /><br />Netzwerkschnittstelle (\*) \Empfangene Bytes/Sek.|30 Minuten|40 %|60 %|
|Speicher|LogicalDisk ( *\<NTDS-Daten\>Bank Laufwerk*) \ Mittlere Sek./Lesevorgänge<br /><br />LogicalDisk ( *\<NTDS-Daten\>Bank Laufwerk*) \ Mittlere Sek./Schreibvorgänge|60 min.|10 ms|15 ms|
|AD-Dienste|Netlogon (\*) \Durchschnittliche Semaphore-Haltezeit|60 min.|0|1 Sekunde|

## <a name="appendix-a-cpu-sizing-criteria"></a>Anhang A: CPU-Größen Kriterien

### <a name="definitions"></a>Definitionen

**Prozessor (Microprocessor) –** eine Komponente, die Programm Anweisungen liest und ausführt  

**CPU-–** Zentrale Verarbeitungseinheit  

**Multi-Core-Prozessor –** mehrere CPUs auf derselben integrierten Verbindung  

**Multi-CPU –** mehrere CPUs, nicht die gleiche integrierte Verbindung  

**Logischer Prozessor –** eine logische Computer-Engine aus der Perspektive des Betriebssystems  

Dies umfasst Hyperthreaded, einen Kern für Multicore-Prozessor oder einen einzelnen Kern Prozessor.  

Da die heutigen Serversysteme über mehrere Prozessoren, mehrere Multikern-Prozessoren und Hyperthreading verfügen, werden diese Informationen verallgemeinert, um beide Szenarios abzudecken. Daher wird der Begriff logischer Prozessor verwendet, da er das Betriebssystem und die Anwendungsperspektive der verfügbaren Computer-Engines darstellt.

### <a name="thread-level-parallelism"></a>Parallelität auf Thread Ebene

Jeder Thread ist eine unabhängige Aufgabe, da jeder Thread über einen eigenen Stapel und eine eigene Anleitung verfügt. Da AD DS Multithread ist und die Anzahl der verfügbaren Threads mithilfe der Vorgehensweise [zum Anzeigen und Festlegen der LDAP-Richtlinie in Active Directory mithilfe von "Ntdsutil. exe](http://support.microsoft.com/kb/315071)" optimiert werden kann, wird die Skalierung über mehrere logische Prozessoren hinweg gut skaliert.

### <a name="data-level-parallelism"></a>Parallelität auf Datenebene

Dies umfasst die gemeinsame Nutzung von Daten über mehrere Threads innerhalb eines Prozesses (im Fall des AD DS Prozesses allein) und über mehrere Threads in mehreren Prozessen (im allgemeinen). Wenn Sie die Groß-/Kleinschreibung überschreiten, bedeutet dies, dass alle Änderungen an den Daten an alle laufenden Threads in allen verschiedenen Cache Ebenen (L1, L2, L3) über alle Kerne, auf denen die genannten Threads ausgeführt werden, sowie auf das Aktualisieren von frei gegebenem Speicher widergespiegelt werden. Die Leistung kann während Schreibvorgängen beeinträchtigt werden, während alle verschiedenen Speicherorte konsistent sind, bevor die Anweisungs Verarbeitung fortgesetzt werden kann.

### <a name="cpu-speed-vs-multiple-core-considerations"></a>Überlegungen zur CPU-Geschwindigkeit im Vergleich zu mehreren Kernen

Die allgemeine Faustregel ist, dass höhere logische Prozessoren die Dauer verringern, die für die Verarbeitung einer Reihe von Anweisungen benötigt wird, und mehr logische Prozessoren bedeutet, dass gleichzeitig weitere Tasks ausgeführt werden können. Die Regeln des Thumb-Aufbruchs werden im Hinblick auf das Abrufen von Daten aus frei gegebenem Speicher, das warten auf Daten ebenenparallelität und der Aufwand für die Verwaltung mehrerer Threads von Natur aus komplexer. Dies ist auch der Grund, warum die Skalierbarkeit in mehr Kernsystemen nicht linear ist.

Berücksichtigen Sie die folgenden Analog Aspekte: Stellen Sie sich eine Autobahn vor, wobei jeder Thread ein einzelnes Auto ist, jede Strecke ein Kern ist und die Geschwindigkeit der Taktfrequenz ist.

1. Wenn nur ein Auto auf der Autobahn vorhanden ist, spielt es keine Rolle, ob zwei Bereiche oder 12 Bereiche vorhanden sind. Das Auto wird nur so schnell wie möglich sein, da das Geschwindigkeitslimit dies zulässt.
1. Angenommen, die Daten, die der Thread benötigt, sind nicht sofort verfügbar. Die Analogie wäre, dass ein Segment der Straße heruntergefahren wird. Wenn nur ein Auto auf der Autobahn vorhanden ist, ist es unerheblich, wie lange die Geschwindigkeit erreicht wird, bis der Bereich wieder geöffnet wird (Daten werden aus dem Arbeitsspeicher abgerufen).
1. Wenn die Anzahl der Fahrzeuge zunimmt, steigt der Aufwand für die Verwaltung der Anzahl der Autos. Vergleichen Sie die Möglichkeiten der Arbeit und die erforderliche Menge an Aufmerksamkeit, wenn die Straße praktisch leer ist (z. b. spät abends), und wenn der Datenverkehr hoch ist (z. b. Mid-Afternoon, aber keine Stoß Stunde). Berücksichtigen Sie auch die Menge an Aufmerksamkeit, die beim Durchlaufen einer zweispurigen Straße erforderlich ist, bei der es nur eine andere Spur gibt, um zu erfahren, was die Treiber tun, und eine sechsspurige Straße, bei der sich die Menge der anderen Treiber Gedanken machen muss.
   > [!NOTE]
   > Die Analogie zum Rush Hour-Szenario wird im nächsten Abschnitt erweitert: Antwortzeit/wie sich die System Auslastung auf die Leistung auswirkt.

Dies hat zur Folge, dass Besonderheiten bei mehr oder schnelleren Prozessoren für das Anwendungsverhalten äußerst subjektiv werden, was im Fall von AD DS sehr Umwelt spezifisch ist und sogar von Server zu Server innerhalb einer Umgebung abweicht. Dies ist der Grund, warum die Verweise weiter oben in diesem Artikel nicht stark in eine übermäßig genaue Investition investieren und eine Sicherheitsstufe in den Berechnungen enthalten ist. Wenn Sie Budget gesteuerte Kaufentscheidungen treffen, empfiehlt es sich, die Prozessorauslastung bei 40% (oder die gewünschte Anzahl für die Umgebung) zuerst zu optimieren, bevor Sie den Erwerb von schnelleren Prozessoren erwägen. Die verstärkte Synchronisierung über mehrere Prozessoren reduziert den wahren Vorteil mehrerer Prozessoren vom linearen Fortschritt (2&times; die Anzahl der Prozessoren bietet weniger als 2&times; verfügbare zusätzliche Compute-Leistung).

> [!NOTE]
> Das Gesetz von Amdahl und das Recht "Gustafson" sind hier die relevanten Konzepte.

### <a name="response-timehow-the-system-busyness-impacts-performance"></a>Antwortzeit/wie sich die System Auslastung auf die Leistung auswirkt

Die queuingtheorie ist die mathematische Studie von wartenden Zeilen (Warteschlangen). In der queuingtheorie wird das Nutzungsrecht durch die Gleichung dargestellt:

*U* k = *B* &divide; *T*

Dabei ist *U* k der Auslastungs Prozentsatz, *B* ist die Zeitspanne, die ausgelastet ist, und *T* ist die Gesamtzeit, die das System beobachtet hat. In den Kontext von Fenstern übersetzt, bedeutet dies, dass die Anzahl der NS-intervallthreads (100-Nanosecond), die sich in einem laufenden Zustand befinden, dividiert durch die Anzahl der in einem bestimmten Zeitintervall verfügbaren 100-ns-Intervalle aufgeteilt ist Dies ist genau die Formel für die Berechnung des Prozessors "% Processor Utility" (Referenz [Prozessor Objekt](https://docs.microsoft.com/previous-versions/ms804036(v=msdn.10)) und [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/previous-versions/windows/embedded/ms901169(v=msdn.10))).

Die queuingtheorie bietet auch die folgende Formel: *N*  =  *u* k &divide;(1 &ndash; *u* k), um die Anzahl der wartenden Elemente basierend auf der Auslastung zu schätzen (*n* ist die Länge der Warteschlange). Wenn Sie dies über alle Auslastungs Intervalle hinaus übernehmen, erhalten Sie die folgenden Schätzungen, wie lange die Warteschlange für den Prozessor eine beliebige CPU-Auslastung hat.

![Warteschlangen Länge](media/capacity-planning-considerations-queue-length.png)

Es ist zu beachten, dass die CPU-Auslastung nach 50% im Durchschnitt immer auf ein anderes Element in der Warteschlange wartet, mit einer deutlich schnelleren Zunahme nach einer CPU-Auslastung von etwa 70%.

Zurückkehren zur Fahr Weise, die weiter oben in diesem Abschnitt verwendet wird:

- Die ausgelasteten Zeiten von "Mid-Afternoon" würden hypothetisch in den Bereich zwischen 40 und 70% fallen. Der Datenverkehr ist so hoch, dass die Fähigkeit, eine beliebige Strecke auszuwählen, nicht grob eingeschränkt ist, und die Gefahr, dass ein anderer Treiber auf dem Weg ist, während er hoch ist, erfordert nicht, dass eine sichere Lücke zwischen anderen Autos auf dem Weg gefunden wird.
- Beachten Sie, dass das Straßensystem bei geöffnetes Aufkommen von Datenverkehr eine Kapazität von 100% erreicht. Das Ändern von Bereichen kann sehr schwierig werden, da Autos so nah beieinander liegen, dass eine größere Vorsicht geboten werden muss.

Aus diesem Grund können die langfristigen Durchschnittswerte für die Kapazität, die auf 40% geschätzt wird, für ungewöhnliche Spitzen beim Laden einen Vorsprung schaffen, ganz gleich, ob die Spitzen vorübergehendes (z. b. schlecht codierte Abfragen, die für einige Minuten ausgeführt werden) oder ungewöhnliche Spitzen bei allgemeiner Auslastung (der Morgen von der erste Tag nach einem langen Wochenende).

Die oben genannte Anweisung bezieht sich auf die Berechnung von% Prozessorzeit, die dem Nutzungs Gesetz entspricht, das eine gewisse Vereinfachung der Erleichterung des allgemeinen Readers ist. Für diese mathematisch strenger:  
- Übersetzen der [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10))
  - *B* = die Anzahl der Intervalle für den "Leerlauf" von 100-ns-Intervallen, die für den logischen Prozessor benötigt werden. Die Änderung in der Variablen "*X*" in der [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) -Berechnung
  - *T* = die Gesamtzahl der 100-ns-Intervalle in einem bestimmten Zeitbereich. Die Änderung in der "*Y*"-Variablen in der [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) -Berechnung.
  - *U* k = der Verwendungs Prozentsatz des logischen Prozessors durch den "Leerlauf Thread" oder die Leerlaufzeit (%).  
- Das Mathematik:
  - *U* k = 1 –% Prozessorzeit
  - Prozessorzeit (%) = 1 – *U* k
  - Prozessorzeit (%) = 1 – *B* / *t*
  - Prozessorzeit (%) = 1 – *x1* – *X0* / *Y1* – *y0*

### <a name="applying-the-concepts-to-capacity-planning"></a>Anwenden der Konzepte auf die Kapazitätsplanung

Die vorangehende Mathematik kann Determinationen hinsichtlich der Anzahl der logischen Prozessoren, die für ein System erforderlich sind, als überwältigend komplex erscheinen. Aus diesem Grund liegt der Ansatz der Größenanpassung der Systeme auf der Ermittlung der maximalen Ziel Auslastung basierend auf der aktuellen Auslastung und der Berechnung der Anzahl der logischen Prozessoren, die benötigt werden. Außerdem hat die Geschwindigkeit von logischen Prozessoren erhebliche Auswirkungen auf die Leistung, die Cache Effizienz, die Anforderungen an die Speicher Kohärenz, die Thread Planung und-Synchronisierung und eine nicht perfekt ausgeglichene Client Auslastung. Leistung, die sich auf Server Basis unterscheiden kann. Mit den relativ günstigen Kosten der computeleistung wird der Versuch, die perfekte Anzahl der benötigten CPUs zu analysieren und zu bestimmen, zu einer akademischen Übung, als der Geschäftswert bereitgestellt wird.

40 Prozent sind keine harte und schnelle Anforderung, es ist ein angemessener Start. Verschiedene Consumer von Active Directory erfordern verschiedene Ebenen der Reaktionsfähigkeit. Möglicherweise gibt es Szenarien, in denen Umgebungen mit einer Auslastung von 80% oder 90% als dauerhafter Durchschnitt ausgeführt werden können, da sich die zunehmenden Wartezeiten für den Zugriff auf den Prozessor nicht merklich auf die Client Leistung auswirken. Es ist wichtig, erneut zu durchlaufen, dass im System viele Bereiche vorhanden sind, die wesentlich langsamer sind als der logische Prozessor im System, einschließlich des Zugriffs auf RAM, des Zugriffs auf die Festplatte und der Übertragung der Antwort über das Netzwerk. Alle diese Elemente müssen zusammen abgestimmt werden. Beispiele:

- Das Hinzufügen von weiteren Prozessoren zu einem System mit 90%, das Datenträger gebunden ist, führt wahrscheinlich nicht zu einer deutlichen Verbesserung der Leistung. Eine tiefer gehende Analyse des Systems erkennt wahrscheinlich, dass viele Threads vorhanden sind, die noch nicht auf dem Prozessor ausgeführt werden, da Sie auf den Abschluss der e/a-Vorgänge warten.
- Die Behebung der Datenträger gebundenen Probleme bedeutet potenziell, dass Threads, die zuvor viel Zeit in den Wartezustand waren, nicht länger in den Wartezustand für e/a-Vorgänge versetzt werden, und es wird mehr Wettbewerb für die CPU-Zeit aufgewendet, was bedeutet, dass die Auslastung von 90% im vorherigen Das Beispiel wechselt zu 100% (weil es nicht weiter gehen kann). Beide Komponenten müssen zusammen abgestimmt werden.
  > [!NOTE]
  > Prozessor Informationen (*) \\% Prozessor Dienstprogramm kann 100% mit Systemen mit dem Modus "Turbo" überschreiten.  An dieser Stelle überschreitet die CPU die bewertete Prozessorgeschwindigkeit für kurze Zeiträume.  Referenz zur CPU-Herstellerdokumentation und-Beschreibung des Zählers für größere Einblicke.  

Die Erörterung ganzer Überlegungen zur System Auslastung bringt auch die Konversations Domänen Controller als virtualisierte Gäste ein. Die [Antwortzeit/die Auswirkung der Systemgeschwindigkeit](#response-timehow-the-system-busyness-impacts-performance) auf die Leistung gilt für den Host und den Gast in einem virtualisierten Szenario. Aus diesem Grund hat bei einem Host mit nur einem Gast ein Domänen Controller (und in der Regel jedes System) fast dieselbe Leistung wie bei physischer Hardware. Das Hinzufügen zusätzlicher Gäste zu den Hosts erhöht die Auslastung des zugrunde liegenden Hosts und erhöht so die Wartezeit, um den Zugriff auf die Prozessoren wie zuvor erläutert zu erhalten. Kurz gesagt, die Auslastung des logischen Prozessors muss sowohl auf dem Host als auch auf dem Gast Niveau verwaltet werden.

Wenn Sie die vorherigen analogen erweitern und die Straße als physische Hardware belassen, wird die Gast-VM mit einem Bus Analog (einem Express-Bus, der direkt zum Ziel wechselt, den der Fahrer möchte). Stellen Sie sich die folgenden vier Szenarien vor:

- Es liegt außerhalb der Stunden, ein Fahrer geht auf einen Bus, der fast leer ist, und der Bus erhält einen Weg, der ebenfalls fast leer ist. Da es keinen Datenverkehr gibt, ist der Fahrer eine schöne, einfache Fahrt, die so schnell wie möglich wäre, wenn der Fahrer stattdessen darauf basiert. Die Reisezeiten des Fahr Fahrers werden weiterhin durch das Geschwindigkeitslimit eingeschränkt.
- Es ist nicht mehr als Stunden, da der Bus fast leer ist, aber die meisten Bereiche auf der Straße geschlossen werden, sodass die Autobahn immer noch überlastet ist. Der Fahrer befindet sich auf einem fast leeren Bus auf einem überlasteten Weg. Obwohl der Fahrer nicht viel Wettbewerb im Bus hat, um zu sitzen, wird die Gesamtfahrt Zeit immer noch vom restlichen Datenverkehr außerhalb vorgegeben.
- Es handelt sich um eine gestürzte Stunde, sodass die Autobahn und der Bus überlastet sind. Der Weg dauert nicht nur länger, aber der Einstieg in den Bus ist ein Alptraum, da die Menschen Schulter zu Schulter haben und die Autobahn nicht viel besser ist. Das Hinzufügen von weiteren Bussen (logische Prozessoren zum Gast) bedeutet nicht, dass Sie leichter in den Weg passen oder dass die Fahrt verkürzt wird.
- Das letzte Szenario, obwohl es möglicherweise die Analogie etwas ausdehnt, ist der, wo der Bus voll ist, aber der Weg ist nicht überlastet. Während der Fahrer weiterhin Probleme beim Einstieg in den Bus hat, ist die Fahrt nach dem Weg des Busverkehrs effizient. Dies ist das einzige Szenario, in dem durch das Hinzufügen von weiteren Bussen (logische Prozessoren zum Gast) die gastleistung verbessert wird.

Von dort aus ist es relativ einfach, zu extrapolieren, dass zwischen dem "0%-ausgelastet"-und dem Status "100%-ausgelastet" und dem Status "0%-" und "100%" des Busses, der unterschiedliche Auswirkungen hat, eine Reihe von Szenarien vorliegt.

Das Anwenden der Prinzipale oberhalb von 40% CPU als vernünftiges Ziel für den Host und den Gast ist ein angemessener Ausgangspunkt für dieselbe Argumentation wie oben, die Menge der Warteschlangen.

## <a name="appendix-b-considerations-regarding-different-processor-speeds-and-the-effect-of-processor-power-management-on-processor-speeds"></a>Anhang B: Überlegungen zu unterschiedlichen Prozessor Geschwindigkeiten und der Auswirkung der Prozessor Energie Verwaltung auf Prozessor Geschwindigkeiten

In den Abschnitten zur Prozessor Auswahl wird die Annahme angenommen, dass der Prozessor um 100% der Taktgeschwindigkeit ausgeführt wird, und zwar mit der gesamten Zeit, zu der die Daten gesammelt werden, und dass die Ersetzungs Systeme über die gleichen Geschwindigkeits Prozessoren verfügen. Obwohl beide Annahmen in der Praxis falsch sind, insbesondere bei Windows Server 2008 R2 und höher, wo der Standard Energie Sparplan **ausgeglichen**ist, bleibt die Methodik weiterhin so, wie Sie der konservative Ansatz ist. Obwohl die potenzielle Fehlerrate zunehmen kann, erhöht sich die Sicherheit nur, wenn sich die Prozessorgeschwindigkeit erhöht.

- Wenn z. b. in einem Szenario, in dem 11,25 CPUs angefordert werden, die Prozessoren beim Sammeln der Daten mit der Hälfte der Geschwindigkeit ausgeführt wurden, kann die genauere &divide; Schätzung 5,125 2 betragen.
- Es ist nicht möglich, sicherzustellen, dass die doppelte Taktgeschwindigkeit die Verarbeitungs Menge verdoppeln würde, die für einen bestimmten Zeitraum stattfindet. Dies liegt daran, dass die Zeitspanne, in der die Prozessoren auf RAM oder andere Systemkomponenten warten, unverändert bleiben könnte. Der Nettoeffekt ist, dass die schnelleren Prozessoren möglicherweise einen größeren Prozentsatz der Leerlaufzeit aufwenden, während Sie auf die abzurufenden Daten warten. Auch hier wird empfohlen, den kleinsten gemeinsamen Nenner zu halten, der konservativ ist, und zu versuchen, eine potenziell falsche Genauigkeits Stufe zu berechnen, indem ein linearer Vergleich zwischen Prozessor Geschwindigkeiten angenommen wird.

Wenn die Prozessorgeschwindigkeit bei der Ersatz Hardware niedriger ist als die aktuelle Hardware, wäre es auch sicher, die Schätzung der Prozessoren zu erhöhen, die von einem angemessenen Betrag benötigt werden. Beispielsweise wird berechnet, dass 10 Prozessoren benötigt werden, um die Last an einem Standort aufrechtzuerhalten, und die aktuellen Prozessoren werden mit 3,3 GHz ausgeführt, und Ersatz Prozessoren werden mit 2,6 GHz ausgeführt. Dies ist eine Verringerung der Geschwindigkeit von 21%. In diesem Fall wäre der empfohlene Betrag bei 12 Prozessoren.

Dies bedeutet, dass die Kapazitäts Verwaltungs Ziele bei der Prozessorauslastung durch diese Variabilität nicht geändert werden. Wenn die Prozessor Taktzeiten basierend auf der geforderten Auslastung dynamisch angepasst werden, wird durch das Ausführen des Systems unter höheren Lasten ein Szenario erzeugt, bei dem die CPU mehr Zeit in einem höheren Takt Zustand verbringt, was das ultimative Ziel ist, eine Auslastung von 40% in einem 100% zu erzielen. Taktfrequenz Status bei Spitzenwert. Alles, was kleiner ist als, generiert Stromeinsparungen, da die CPU-Geschwindigkeiten außerhalb der Spitzenzeiten gedrosselt werden.

> [!NOTE]
> Eine Option wäre das Deaktivieren der Energie Verwaltung auf den Prozessoren (Festlegen des Energie Sparplans auf **hohe Leistung**), während die Daten gesammelt werden. Dadurch würde eine genauere Darstellung der CPU-Auslastung auf dem Zielserver zur Verfügung stehen.

Zum Anpassen der Schätzwerte für verschiedene Prozessoren war es sicher und mit Ausnahme anderer System Engpässe, die oben beschrieben wurden, zu übernehmen, dass die doppelte Prozessorgeschwindigkeit den Umfang der verarbeiteten Verarbeitung verdoppelt.  Heutzutage unterscheidet sich die interne Architektur der Prozessoren zwischen den Prozessoren, sodass eine sicherere Möglichkeit zum Messen der Auswirkungen der Verwendung verschiedener Prozessoren als bei der Verwendung des SPECint_rate2006-Vergleichs aus der Standard Leistungsbewertung besteht. Unternehmen.

1. Suchen Sie die SPECint_rate2006-Ergebnisse für den verwendeten Prozessor, und verwenden Sie diesen Plan.
    1. Wählen Sie auf der Website der Standard Performance Evaluation Corporation **Ergebnisse**, markieren Sie **CPU2006**, und wählen Sie **alle SPECint_rate2006 Ergebnisse suchen**aus.
    1. Geben Sie unter **einfache Anforderung**die Suchkriterien für den Zielprozessor ein, z. b. der **Prozessor entspricht E5-2630 (baselinetarget)** und der **Prozessor entspricht E5-2650 (Baseline)** .
    1. Suchen Sie die zu verwendende Server-und Prozessor Konfiguration (oder etwas, wenn eine genaue Entsprechung nicht verfügbar ist), und notieren Sie sich den Wert in den Spalten **Result** und **# Cores** .
1. Verwenden Sie zum Bestimmen des Modifizierers die folgende Gleichung:
   >((*Zielplattform-pro-Kern-* Bewertungs &times; Wert) (*MHz pro Kern der baselineplattform* &divide; )) ((*Baseline-pro-Kern-Bewertungs Wert*) &times; (*MHz pro Kern der Zielplattform*)  

    Verwenden Sie das obige Beispiel:
   >(35,83 &times; 2000) &divide; (33,75 &times; 2300) = 0,92
1. Multiplizieren Sie die geschätzte Anzahl von Prozessoren durch den-Modifizierer.  Im obigen Fall, um vom E5-2650-Prozessor zum E5-2630-Prozessor zu wechseln, Multiplizieren Sie &times; die berechneten 11,25 CPUs 0,92 = 10,35 Prozessoren.

## <a name="appendix-c-fundamentals-regarding-the-operating-system-interacting-with-storage"></a>Anhang C: Grundlagen bezüglich des Betriebssystems, das mit Storage interagiert

Die in der Antwortzeit beschriebenen Konzepte der queuingtheorie, die [Auswirkungen auf die Leistung des Systems](#response-timehow-the-system-busyness-impacts-performance) sind, können auch auf den Speicher angewendet werden. Wenn Sie sich damit vertraut machen, wie das Betriebssystem e/a-Vorgänge verarbeitet, ist es erforderlich, diese Konzepte anzuwenden. Im Microsoft Windows-Betriebssystem wird eine Warteschlange für die e/a-Anforderungen für jeden physischen Datenträger erstellt. Es muss jedoch eine Erläuterung auf dem physischen Datenträger erstellt werden. Array Controller und Sans stellen Aggregationen von Spindeln als einzelne physische Datenträger für das Betriebssystem dar. Außerdem können Array Controller und Sans mehrere Datenträger zu einem Array Satz zusammenfassen und diese Array Gruppe dann in mehrere "Partitionen" aufteilen, die wiederum dem Betriebssystem als mehrere physische Datenträger (Ref. Figure) präsentiert werden.

![Spindeln blockieren](media/capacity-planning-considerations-block-spindles.png)  

In dieser Abbildung werden die beiden Spindeln gespiegelt und in logische Bereiche für den Datenspeicher aufgeteilt (Data 1 und Data 2). Diese logischen Bereiche werden vom Betriebssystem als separate physische Datenträger angezeigt.

Obwohl dies sehr verwirrend sein kann, wird in diesem Anhang die folgende Terminologie verwendet, um die verschiedenen Entitäten zu identifizieren:

- **Spindel –** das Gerät, das physisch auf dem Server installiert ist.
- **Array –** eine Auflistung von Spindeln, die durch den Controller aggregiert werden.
- **Array Partition –** eine Partitionierung des aggregierten Arrays
- **LUN –** ein Array, das beim Verweisen auf SANs verwendet wird
- Datenträger **–** Das Betriebssystem stellt einen einzelnen physischen Datenträger fest.
- **Partition –** eine logische Partitionierung des Betriebssystems als physischer Datenträger.

### <a name="operating-system-architecture-considerations"></a>Überlegungen zur Betriebssystemarchitektur

Das Betriebssystem erstellt eine First in/First Out (FIFO)-e/a-Warteschlange für jeden beobachteten Datenträger. dieser Datenträger kann eine Spindel, ein Array oder eine Array Partition darstellen. Aus Sicht des Betriebssystems ist es im Hinblick auf die Handhabung von e/a-Vorgängen besser, die aktiven Warteschlangen zu verbessern. Wenn eine FIFO-Warteschlange serialisiert wird, bedeutet dies, dass alle für das Speichersubsystem ausgestellten e/As in der Reihenfolge verarbeitet werden müssen, in der die Anforderung eingetroffen ist. Durch die Korrelation der einzelnen Datenträger, die vom Betriebssystem mit einer Spindel bzw. einem Array erkannt werden, verwaltet das Betriebssystem nun eine e/a-Warteschlange für jeden eindeutigen Satz von Datenträgern, wodurch Konflikte bei knappen e/a-Ressourcen auf den Datenträgern vermieden und die e/a-Anforderung auf eine einzelne Diskette. Als Ausnahme führt Windows Server 2008 das Konzept der e/a-Priorisierung ein, und Anwendungen, die für die Verwendung der "niedrigen" Priorität entworfen wurden, fallen in dieser normalen Reihenfolge aus und nehmen einen Rückstand in Anspruch. Anwendungen, die nicht speziell für die Verwendung der "niedrigen" Priorität codiert sind, sind standardmäßig "Normal".

### <a name="introducing-simple-storage-subsystems"></a>Einführung in einfache Speicher Subsysteme

Beginnend mit einem einfachen Beispiel (eine einzelne Festplatte innerhalb eines Computers) wird eine Komponenten Weise Analyse erstellt. Wenn Sie dies in die Hauptkomponenten des Speicher Subsystems aufteilen, besteht das System aus folgendem:

- **1 –** 10.000 rpm, ultraschnelle SCSI-HD (Ultra Fast SCSI hat eine Übertragungsrate von 20 MB/s)
- **1 –** SCSI-Bus (das Kabel)
- **1 –** Ultra Fast SCSI-Adapter
- **1 –** 32-Bit 33 MHz PCI-Bus

Nachdem Sie die Komponenten identifiziert haben, können Sie berechnen, wie viele Daten das System übertragen können oder wie viele e/a-Vorgänge verarbeitet werden können. Beachten Sie, dass die Menge an e/a und Menge der Daten, die das System übertragen können, korreliert ist, aber nicht identisch ist. Diese Korrelation hängt davon ab, ob die Datenträger-e/a zufällig oder sequenziell und die Blockgröße ist. (Alle Daten werden als Block auf den Datenträger geschrieben, aber unterschiedliche Anwendungen, die unterschiedliche Blockgrößen verwenden.) Auf Komponentenbasis:

- **Die Festplatte –** Die durchschnittliche Festplatte 10.000-rpm hat eine Suchzeit von 7 Millisekunden (MS) und eine 3 MS-Zugriffszeit. Die Suchzeit ist die durchschnittliche Zeitspanne, die der Lese-/Schreibzugriff an einen Speicherort auf der Platte nimmt. Die Zugriffszeit ist die durchschnittliche Zeitspanne, die benötigt wird, um die Daten auf den Datenträger zu lesen oder zu schreiben, sobald sich der Kopf am richtigen Speicherort befindet. Daher stellt die durchschnittliche Zeit für das Lesen eines eindeutigen Datenblocks in einer 10.000-rpm-HD eine Suche und einen Zugriff dar, die insgesamt ungefähr 10 ms (oder .010 Sekunden) pro Datenblock beträgt.

  Wenn jeder Datenträger Zugriff eine Bewegung des Kopfes an einen neuen Speicherort auf dem Datenträger erfordert, wird das Lese-/Schreibverhalten als "Random" bezeichnet. Wenn also alle e/a-Vorgänge zufällig erfolgen, kann eine 10.000-rpm-HD ungefähr 100 e/a pro Sekunde (IOPS) verarbeiten (die Formel ist 1000 ms pro Sekunde dividiert durch 10 MS pro e/a oder 1000/10 = 100 IOPS).

  Wenn alle e/a-Vorgänge von angrenzenden Sektoren auf der Festplatte ausgeführt werden, wird dies als sequenzielle e/a bezeichnet. Ein sequenzieller e/a-Vorgang hat keine Suchzeit, da der Lese-/schreibanfang am Anfang des Vorgangs ist, an dem der nächste Datenblock auf der Festplatte gespeichert ist, wenn der erste e/a-Vorgang beendet ist. Eine 10.000-rpm-HD kann also ungefähr 333 e/a pro Sekunde verarbeiten (1000 ms pro Sekunde dividiert durch 3 MS pro e/a).

  >[!NOTE]
  >Dieses Beispiel spiegelt nicht den Datenträger Cache wider, in dem die Daten eines Zylinder in der Regel beibehalten werden. In diesem Fall werden die 10 ms auf der ersten e/a benötigt, und der Datenträger liest den gesamten Zylinder. Alle anderen sequenziellen e/a-Vorgänge werden aus dem Cache erfüllt. Folglich kann die sequenzielle e/a-Leistung durch in-Disk-Caches verbessert werden.
  
  Bisher war die Übertragungsrate der Festplatte irrelevant. Unabhängig davon, ob es sich bei der Festplatte um eine ultrabreite von 20 MB/s oder um einen Ultra3-Wert von 160 MB/s handelt, ist der tatsächliche IOPS-Wert, der von der 10.000-rpm-HD verarbeitet werden kann, ~ 100 Random oder ~ 300 sequenzielle Wenn sich Blockgrößen auf der Grundlage der Anwendung ändern, die auf das Laufwerk schreibt, ist die Menge der Daten, die pro e/a-Vorgänge abgerufen werden, unterschiedlich. Wenn die Blockgröße z. b. 8 KB beträgt, werden 100-e/a-Vorgänge auf der Festplatte eingelesen oder auf die Festplatte geschrieben, d. h. 800 KB. Wenn die Blockgröße jedoch 32 KB beträgt, werden 100 e/a-Vorgänge mit 3.200 KB (3,2 MB) auf der Festplatte gelesen/geschrieben. Solange die SCSI-Übertragungsrate die gesamte übertragene Datenmenge überschreitet, wird ein "schnelleres" Übertragungsraten-Laufwerk nicht mehr angezeigt. Einen Vergleich finden Sie in den folgenden Tabellen.

  | |7200 rpm 9ms Suche, 4ms-Zugriff|10.000 rpm 7 ms Suche, 3 MS-Zugriff|15.000 rpm 4ms suchen, 2 MS Zugriff
  |-|-|-|-|
  |Zufällige e/a|80|100|150|
  |Sequenzielle e/a|250|300|500|  
  
  |10.000-rpm-Laufwerk|Blockgröße 8 KB (Active Directory Jet)|
  |-|-|
  |Zufällige e/a|800 KB/s|
  |Sequenzielle e/a|2400 KB/s|

- **SCSI-Rückwand (Bus) –** Wenn Sie verstehen, wie die "SCSI-Rückwand (Bus)" oder in diesem Szenario das Menüband-Kabel den Durchsatz des Speicher Subsystems beeinträchtigt, hängt von den Kenntnissen der Blockgröße ab. Im Grunde ist die Frage, wie viele e/a-Vorgänge der Bus verarbeiten kann, wenn sich die e/a-Vorgänge in 8-KB-Blöcken befinden? In diesem Szenario beträgt der SCSI-Bus 20 MB/s oder 20480 KB/s. 20480 KB/s dividiert durch 8-KB-Blöcke ergeben maximal etwa 2500 IOPS, die vom SCSI-Bus unterstützt werden.

  >[!NOTE]
  >Die Abbildungen in der folgenden Tabelle stellen ein Beispiel dar. Die meisten angeschlossenen Speichergeräte verwenden derzeit PCI Express, das einen deutlich höheren Durchsatz bereitstellt.  
  
  |E/a-Unterstützung durch SCSI-Bus pro Blockgröße|Blockgröße 2 KB|Blockgröße 8 KB (AD Jet) (SQL Server 7.0/SQL Server 2000)
  |-|-|-|
  |20 MB/s|10.000|2\.500|
  |40 MB/s|20.000|5\.000|
  |128 MB/s|65.536|16.384|
  |320 MB/s|160.000|40.000|

  Wie von diesem Diagramm bestimmt werden kann, ist im Szenario, unabhängig von der Art der Verwendung, der Bus nie ein Engpass, da der maximale spinspinwert 100-e/a-Vorgänge unter einem der oben genannten Schwellenwerte liegt.

  >[!NOTE]
  >Dabei wird davon ausgegangen, dass der SCSI-Bus 100% effizient ist.
  
- **SCSI-Adapter –** Zum Ermitteln der Menge an e/a-Vorgängen, die von diesem verarbeitet werden können, müssen die Spezifikationen des Herstellers geprüft werden. Wenn Sie e/a-Anforderungen an das entsprechende Gerät weiterleiten müssen, ist die Verarbeitung einiger Sortierungen erforderlich. Daher ist die Menge der e/a-Vorgänge, die verarbeitet werden können, vom SCSI-Adapter Prozessor (oder Array Controller) abhängig.

  In diesem Beispiel wird davon ausgegangen, dass 1.000 e/a behandelt werden kann.

- **PCI-Bus –** Dies ist eine häufig übersehene Komponente. In diesem Beispiel ist dies nicht der Engpass. da Systeme jedoch zentral hochskaliert werden, kann dies zu einem Engpass werden. Zur Referenz kann ein 32-Bit-PCI-Bus mit einer Größe von 33mhz theoretisch 133 MB/s Daten übertragen. Im folgenden finden Sie die Gleichung:  
  > 32 Bits &divide; 8 Bits pro Byte &times; 33 MHz = 133 MB/s.  

  Beachten Sie, dass das theoretische Limit ist. Tatsächlich ist nur etwa 50% des Höchstwerts tatsächlich erreicht. in bestimmten Burst Szenarien kann jedoch für kurze Zeiträume eine Effizienz von 75% erreicht werden.

  Ein-PCI-64-Bit-PCI-Bus von 66MHz kann eine theoretische &divide; maximale Anzahl von ( &times; 64 Bits 8 Bits pro Byte 66 MHz) = 528 MB/s unterstützen. Darüber hinaus wird bei jedem anderen Gerät (z. b. Netzwerkadapter, zweiter SCSI-Controller usw.) die verfügbare Bandbreite reduziert. die Bandbreite wird gemeinsam genutzt, und die Geräte werden mit den begrenzten Ressourcen in den Mittelwert setzen.

Nach der Analyse der Komponenten dieses Speicher Subsystems ist die Spindel der einschränkende Faktor für die Menge an e/a-Vorgängen, die angefordert werden kann, und folglich die Datenmenge, die das System übertragen kann. Insbesondere in einem AD DS Szenario ist dies 100 zufällige e/a-Vorgänge pro Sekunde in Schritten von 8 KB, d. h., für den Zugriff auf die Jet-Datenbank sind insgesamt 800 KB pro Sekunde. Alternativ hätte der maximale Durchsatz für eine Spindel, die ausschließlich Protokolldateien zugeordnet ist, die folgenden Einschränkungen: 300 sequenzielle e/a pro Sekunde in Schritten von 8 KB, für insgesamt 2400 KB (2,4 MB) pro Sekunde.

Nachdem Sie nun eine einfache Konfiguration analysiert haben, zeigt die folgende Tabelle, wo der Engpass auftritt, wenn Komponenten im Speichersubsystem geändert oder hinzugefügt werden.

|Hinweise|Engpass-Analyse|Datenträger|Bus|Adapter|PCI-Bus|
|-|-|-|-|-|-|
|Dies ist die Konfiguration des Domänen Controllers nach dem Hinzufügen eines zweiten Datenträgers. Die Datenträger Konfiguration stellt den Engpass bei 800 KB/s dar.|1 Datenträger hinzufügen (Gesamt = 2)<br /><br />E/a ist zufällig<br /><br />Blockgröße 4 KB<br /><br />10.000 RPM HD|200 I/OS Gesamt<br />800 KB/s insgesamt.| | | |
|Nach dem Hinzufügen von 7 Datenträgern stellt die Datenträger Konfiguration weiterhin den Engpass bei 3200 KB/s dar.|**7 Datenträger hinzufügen (Gesamt = 8)**  <br /><br />E/a ist zufällig<br /><br />Blockgröße 4 KB<br /><br />10.000 RPM HD|800 I/OS gesamt.<br />3200 KB/s insgesamt| | | |
|Nachdem die e/a-Vorgänge in eine sequenzielle Änderung geändert wurden, wird der Netzwerkadapter zum Engpass, weil er auf 1000 IOPS beschränkt ist.|7 Datenträger hinzufügen (Gesamt = 8)<br /><br />**E/a ist sequenziell**<br /><br />Blockgröße 4 KB<br /><br />10.000 RPM HD| | |2400 e/a-Sek. können auf den Datenträger gelesen/geschrieben werden, Controller beschränkt auf 1000 IOPS| |
|Nachdem Sie den Netzwerkadapter durch einen SCSI-Adapter ersetzt haben, der 10.000 IOPS unterstützt, kehrt der Engpass zur Datenträger Konfiguration zurück.|7 Datenträger hinzufügen (Gesamt = 8)<br /><br />E/a ist zufällig<br /><br />Blockgröße 4 KB<br /><br />10.000 RPM HD<br /><br />**SCSI-Adapter aktualisieren (unterstützt jetzt 10.000-e/a)**|800 I/OS gesamt.<br />3\.200 KB/s insgesamt| | | |
|Nachdem die Blockgröße auf 32 KB erhöht wurde, wird der Bus zum Engpass, da er nur 20 MB/s unterstützt.|7 Datenträger hinzufügen (Gesamt = 8)<br /><br />E/a ist zufällig<br /><br />**Blockgröße 32 KB**<br /><br />10.000 RPM HD| |800 I/OS gesamt. 25.600 KB/s (25 MB/s) können auf den Datenträger gelesen/geschrieben werden.<br /><br />Der Bus unterstützt nur 20 MB/s.| | |
|Nachdem Sie den Bus aktualisiert und weitere Datenträger hinzugefügt haben, bleibt der Datenträger als Engpass.|**13 Datenträger hinzufügen (Gesamt = 14)**<br /><br />Hinzufügen eines zweiten SCSI-Adapters mit 14 Datenträgern<br /><br />E/a ist zufällig<br /><br />Blockgröße 4 KB<br /><br />10.000 RPM HD<br /><br />**Upgrade auf 320 MB/s SCSI-Bus**|2800 I/OS<br /><br />11.200 KB/s (10,9 MB/s)| | | |
|Nach dem Ändern des e/a-Vorgängen in den sequenziellen Datenträger bleibt der Datenträger|13 Datenträger hinzufügen (Gesamt = 14)<br /><br />Hinzufügen eines zweiten SCSI-Adapters mit 14 Datenträgern<br /><br />**E/a ist sequenziell**<br /><br />Blockgröße 4 KB<br /><br />10.000 RPM HD<br /><br />Upgrade auf 320 MB/s SCSI-Bus|8\.400 I/OS<br /><br />33.600 kb\s<br /><br />(32,8 mb\s)| | | |
|Nachdem Sie schnellere Festplatten hinzugefügt haben, bleibt der Datenträger als Engpass fest.|13 Datenträger hinzufügen (Gesamt = 14)<br /><br />Hinzufügen eines zweiten SCSI-Adapters mit 14 Datenträgern<br /><br />E/a ist sequenziell<br /><br />Blockgröße 4 KB<br /><br />**15.000 RPM HD**<br /><br />Upgrade auf 320 MB/s SCSI-Bus|14.000 I/OS<br /><br />56.000 KB/s<br /><br />(54,7 MB/s)| | | |
|Nachdem die Blockgröße auf 32 KB erhöht wurde, wird der PCI-Bus zu einem Engpass.|13 Datenträger hinzufügen (Gesamt = 14)<br /><br />Hinzufügen eines zweiten SCSI-Adapters mit 14 Datenträgern<br /><br />E/a ist sequenziell<br /><br />**Blockgröße 32 KB**<br /><br />15.000 RPM HD<br /><br />Upgrade auf 320 MB/s SCSI-Bus| | | |14.000 I/OS<br /><br />448.000 KB/s<br /><br />(437 MB/s) ist das Lese-/schreiblimit für die Spindel.<br /><br />Der PCI-Bus unterstützt ein theoretisches Maximum von 133 MB/s (75% effizient).|

### <a name="introducing-raid"></a>Einführung in RAID

Die Art eines Speicher Subsystems ändert sich nicht erheblich, wenn ein Array Controller eingeführt wird. der SCSI-Adapter wird lediglich in den Berechnungen ersetzt. Änderungen sind die Kosten für das Lesen und Schreiben von Daten auf dem Datenträger, wenn die verschiedenen Array Ebenen (z. b. RAID 0, RAID 1 oder RAID 5) verwendet werden.

In RAID 0 werden die Daten über alle Datenträger im RAID-Satz verteilt. Dies bedeutet, dass während eines Lese-oder eines Schreibvorgangs ein Teil der Daten von jedem Datenträger abgerufen oder per Pushvorgang übertragen wird. dadurch erhöht sich die Datenmenge, die das System während des gleichen Zeitraums übertragen kann. In einer Sekunde kann auf jeder Spindel (wieder 10.000-rpm-Laufwerke) 100 e/a-Vorgänge ausgeführt werden. Die Gesamtmenge an e/a-Vorgängen, die unterstützt werden kann, beträgt N spin100 deln pro Sekunde pro Spindel (ergibt 100 * N e/a pro Sekunde).

![Logisches Laufwerk "d:"](media/capacity-planning-considerations-logical-d-drive.png)

In RAID 1 werden die Daten für Redundanz über ein Spindeln-paar hinweg gespiegelt (dupliziert). Wenn also ein Lese-e/a-Vorgang ausgeführt wird, können Daten aus beiden Spindeln in der Menge gelesen werden. Dadurch wird die e/a-Kapazität von beiden Datenträgern während eines Lesevorgangs verfügbar. Der Nachteil ist, dass Schreibvorgänge in einem RAID 1-System keinen Leistungsvorteil haben. Dies liegt daran, dass die gleichen Daten auf beide Laufwerke geschrieben werden müssen, um Redundanz zu gewährleisten. Obwohl das Schreiben von Daten gleichzeitig auf beiden Spindeln erfolgt, weil beide Spindeln das Duplizieren der Daten belegen, verhindert ein Schreib-e/a-Vorgang im Wesentlichen, dass zwei Lesevorgänge ausgeführt werden. Folglich sind für jede Schreib-e/a zwei Lese-e/a-Vorgänge Kosten. Aus diesen Informationen kann eine Formel erstellt werden, um die Gesamtzahl der auftretenden e/a-Vorgänge zu bestimmen:  

> E/a *-Lese* Vorgänge &times; + 2 *geschriebene* = e/a-Vorgänge*insgesamt verfügbar*  

Wenn das Verhältnis zwischen Lese-und Schreibvorgängen und der Anzahl der Spindeln bekannt ist, kann die folgende Gleichung von der obigen Gleichung abgeleitet werden, um die maximale e/a zu identifizieren, die vom Array unterstützt werden kann:  

> *Maximaler IOPS pro Spindel* &times; 2 Spindeln &times; [( *%Liest* +  *%Schreibt*) &divide; ( *%Liest* + 2 &times; *%Schreibt*)] = *Gesamt-IOPS*

RAID 1 + 0 verhält sich in Bezug auf das Lesen und Schreiben genauso wie RAID 1. Die e/a-Vorgänge werden jedoch jetzt über jeden gespiegelten Satz verteilt. Wenn  

> *Maximaler IOPS pro Spindel* &times; 2 Spindeln &times; [( *%Liest* +  *%Schreibt*) &divide; ( *%Liest* + 2 &times; *%Schreibt*)] = *Gesamt-IOPS*  

Wenn in einem RAID 1-Satz eine Multiplizität (*N*) von RAID 1-Sätzen Stripeset ist, wird die Gesamtzahl der e/ &times; a-Vorgänge, die verarbeitet werden können, N e/a pro RAID 1-Satz:  

> *N* &times; {*Maximaler IOPS pro Spindel* &times; 2 spindels &times; [( *%Liest* +  *%Schreibt*) &divide; ( *%Liest* + 2 &times; *%Schreibt*)] } = *Gesamt-IOPS*

In RAID 5 (manchmal auch als " *n* + 1 RAID" bezeichnet) werden die Daten auf *n* Spindeln verteilt, und Paritätsinformationen werden in die "+ 1"-Spindel geschrieben. RAID 5 ist jedoch viel kostengünstiger, wenn e/a-Vorgänge als RAID 1 oder 1 + 0 durchgeführt werden. RAID 5 führt den folgenden Prozess jedes Mal aus, wenn ein e/a-Schreibvorgang an das Array übermittelt wird:

1. Alte Daten lesen
1. Alte Parität lesen
1. Schreiben der neuen Daten
1. Schreiben der neuen Parität

Da für jede Schreib-e/a-Anforderung, die vom Betriebssystem an den Array Controller gesendet wird, vier e/a-Vorgänge ausgeführt werden müssen, dauert die Ausführung von Schreib Anforderungen viermal so lange, bis Sie als einzelne Lese-e/a-Vorgänge ausgeführt werden. So leiten Sie eine Formel zum Übersetzen von e/a-Anforderungen aus der Perspektive des Betriebssystems in die von den Spindeln durch:  

> E/a *-Lese* Vorgänge &times; *+ 4* = e/a-Vorgänge*Gesamt*  

Ebenso kann in einer RAID 1-Gruppe die folgende Gleichung abgeleitet werden, wenn das Verhältnis zwischen Lese-und Schreibvorgängen und der Anzahl der Spindeln bekannt ist, um die maximale e/a zu ermitteln, die vom Array unterstützt werden kann. (Beachten Sie, dass die Gesamtanzahl der Spindeln nicht Folgendes umfasst: e: das "Laufwerk" geht bei der Parität verloren):  

> *IOPS per spindel* &times; (*Spindel* – 1) &times; [( *%Liest* +  *%Schreibt*) &divide; ( *%Liest* + 4 &times; *%Schreibt*)] = *Gesamt IOPS*

### <a name="introducing-sans"></a>Einführung in Sans

Wenn Sie die Komplexität des Speicher Subsystems erweitern, wenn ein San in die Umgebung eingeführt wird, werden die grundlegenden Prinzipien nicht geändert, aber das e/a-Verhalten für alle Systeme, die mit dem SAN verbunden sind, muss berücksichtigt werden. Einer der Hauptvorteile bei der Verwendung eines San ist eine zusätzliche Redundanz im internen oder extern angeschlossenen Speicher. die Kapazitätsplanung muss nun die Fehlertoleranz Anforderungen berücksichtigen. Außerdem werden weitere Komponenten eingeführt, die ausgewertet werden müssen. Unterbrechen eines San in die Komponenten Teile:

- SCSI-oder Fibre Channel Festplatte
- Rück Ebene des Speichereinheiten Kanals
- Speichereinheiten
- Speichercontroller Modul
- SAN-Switch (es)
- HBA (s)
- Der PCI-Bus

Wenn Sie ein System für Redundanz entwerfen, sind zusätzliche Komponenten enthalten, um das mögliche Auftreten von Fehlern zu ermöglichen. Bei der Kapazitätsplanung ist es sehr wichtig, die redundante Komponente von verfügbaren Ressourcen auszuschließen. Wenn das San z. b. über zwei Controller Module verfügt, muss die e/a-Kapazität eines Controller Moduls für den gesamten e/a-Durchsatz verwendet werden, der für das System verfügbar ist. Dies liegt daran, dass bei einem Ausfall eines Controllers die gesamte von allen verbundenen Systemen geforderte e/a-Last vom verbleibenden Controller verarbeitet werden muss. Da die gesamte Kapazitätsplanung für Spitzenzeiten durchgeführt wird, sollten redundante Komponenten nicht in den verfügbaren Ressourcen berücksichtigt werden, und die geplante Spitzen Auslastung sollte die Sättigung des Systems von 80% nicht überschreiten (um Spitzen oder anomale Systeme zu berücksichtigen). Verhalten). Ebenso sollten der redundante SAN-Switch, die Speichereinheit und die Spindeln nicht in die e/a-Berechnungen einbezogen werden.

Wenn Sie das Verhalten der SCSI-oder Fibre Channel Festplatte analysieren, wird die Methode zum Analysieren des Verhaltens wie zuvor beschrieben nicht geändert. Obwohl jedes Protokoll bestimmte vor-und Nachteile hat, ist der einschränkende Faktor pro Datenträger die mechanische Einschränkung der Festplatte.

Das Analysieren des Kanals auf der Speichereinheit ist identisch mit dem Berechnen der auf dem SCSI-Bus verfügbaren Ressourcen oder der Bandbreite (z. b. 20 MB/s) dividiert durch Blockgröße (z. b. 8 KB). Wenn dies vom einfachen vorherigen Beispiel abweicht, ist die Aggregation mehrerer Kanäle. Wenn z. b. sechs Kanäle vorhanden sind, die jeweils eine maximale Übertragungsrate von 20 MB/s unterstützen, beträgt die Gesamtzahl der verfügbaren e/a-und Datenübertragungen 100 MB/s (Dies ist richtig, nicht 120 MB/s). Auch hier ist die Fehlertoleranz ein wichtiger Akteur in dieser Berechnung. im Falle des Verlusts eines gesamten Kanals ist das System nur mit fünf funktionierenden Kanälen übrig. Damit sichergestellt ist, dass die Leistungserwartungen im Fall eines Fehlers weiterhin erfüllt werden, sollte der Gesamtdurchsatz für alle Speicherkanäle 100 MB/s nicht überschreiten (Dies geht davon aus, dass die Auslastung und die Fehlertoleranz gleichmäßig auf alle Kanäle verteilt sind). Die Umwandlung in ein e/a-Profil hängt vom Verhalten der Anwendung ab. Im Fall von Active Directory Jet-e/a korreliert dies ungefähr 12.500 e/a pro Sekunde (100 MB/s 8 KB pro &divide; e/a).

Im nächsten Schritt wird das Abrufen der Hersteller Spezifikationen für die Controller Module benötigt, um einen Einblick in den Durchsatz zu erhalten, der von den einzelnen Modulen unterstützt werden kann. In diesem Beispiel verfügt das San über zwei Controller Module, die jeweils 7.500 I/O unterstützen. Der Gesamtdurchsatz des Systems kann 15.000 IOPS betragen, wenn keine Redundanz erwünscht ist. Beim Berechnen des maximalen Durchsatzes im Falle eines Fehlers ist die Einschränkung der Durchsatz von einem Controller oder 7.500 IOPS. Dieser Schwellenwert liegt unter dem maximalen Wert von 12.500 IOPS (bei einer Blockgröße von 4 KB), der von allen Speicher Kanälen unterstützt werden kann. Folglich ist dies derzeit der Engpass bei der Analyse. Zu Planungszwecken wäre der gewünschte maximale e/a-Wert 10.400 i/o.

Wenn die Daten das Controller Modul beenden, wird eine Fibre Channel mit 1 GB/s (oder 1 Gigabit pro Sekunde) bewertete Verbindung übertragen. Um dies mit den anderen Metriken zu korrelieren, werden 1 GB/s in 128 MB/s (1 GB &divide; /s 8 Bits/Byte) umgewandelt. Da dies die Gesamtbandbreite für alle Kanäle in der Speichereinheit (100 MB/s) überschreitet, wird das System dadurch nicht Engpass. Da es sich dabei nur um einen der beiden Kanäle handelt (die zusätzlichen 1 GB/s Fibre Channel Verbindung zur Redundanz), verfügt die verbleibende Verbindung, wenn eine Verbindung nicht hergestellt werden kann, weiterhin über genügend Kapazität, um alle angeforderten Datenübertragungen zu verarbeiten.

Wenn die Daten an den Server weitergeleitet werden, überqueren Sie höchstwahrscheinlich einen SAN-Switch. Da der SAN-Switch die eingehende e/a-Anforderung verarbeiten und den entsprechenden Port weiterleiten muss, hat der Switch eine Beschränkung für die Anzahl der e/a-Vorgänge, die verarbeitet werden können. Allerdings sind Hersteller Spezifikationen erforderlich, um zu bestimmen, was das Limit ist. Wenn beispielsweise zwei Switches vorhanden sind und jeder Switch 10.000 IOPS verarbeiten kann, beträgt der Gesamtdurchsatz 20.000 IOPS. Auch hier gilt: Wenn ein Switch fehlschlägt, ist der Gesamtdurchsatz des Systems 10.000 IOPS. Da es gewünscht wird, dass die Auslastung von 80% im normalen Betrieb nicht überschritten wird, sollte die Verwendung von nicht mehr als 8000 e/a das Ziel sein.

Schließlich hätte der auf dem Server installierte HBA auch eine Beschränkung für die Anzahl der e/a-Vorgänge, die er verarbeiten kann. Normalerweise wird ein zweiter HBA für die Redundanz installiert, aber ebenso wie beim SAN-Switch, wenn die maximale e/a-Verarbeitung, die verarbeitet werden kann, der Gesamtdurchsatz von *N* &ndash; 1 HBAs die maximale Skalierbarkeit des Systems ist.

### <a name="caching-considerations"></a>Überlegungen zum Caching

Caches sind eine der-Komponenten, die sich zu jedem Zeitpunkt im Speichersystem erheblich auf die Gesamtleistung auswirken können. Eine ausführliche Analyse der zwischen Speicherungs Algorithmen geht über den Rahmen dieses Artikels hinaus. einige grundlegende Anweisungen zum Zwischenspeichern auf Datenträger Subsystemen sind jedoch sinnvoll:

- Durch die Zwischenspeicherung werden die dauerhaften e/a-Vorgänge für sequenzielle Schreibvorgänge verbessert, da dadurch viele kleinere Schreibvorgänge in größere e/a-Blöcke gepuffert und in weniger, aber größere Blockgrößen eingefügt werden. Dadurch werden die Gesamtzahl zufälliger e/a-Vorgänge und die gesamte sequenzielle e/a-Vorgänge reduziert, wodurch die Verfügbarkeit von Ressourcen für andere e/As
- Durch das Zwischenspeichern wird der e/a-Durchsatz des Speicher Subsystems nicht verbessert. Die Schreibvorgänge können nur gepuffert werden, bis die Spindeln zum Commit für die Daten verfügbar sind. Wenn alle verfügbaren e/a-Vorgänge der Spindeln im Speichersubsystem über lange Zeiträume hinweg erschöpft sind, wird der Cache schließlich aufgefüllt. Um den Cache zu leeren, muss ausreichend Zeit zwischen Spitzen oder zusätzlichen Spindeln zugewiesen werden, damit genügend e/a-Vorgänge bereitgestellt werden, damit der Cache geleert werden kann.

  Größere Caches erlauben nur, dass mehr Daten gepuffert werden. Dies bedeutet, dass längere Zeiträume der Sättigung untergebracht werden können.

  In einem normalerweise betriebenen Betriebssystem wird das Betriebssystem die Schreibleistung verbessern, da die Daten nur in den Cache geschrieben werden müssen. Sobald die zugrunde liegenden Medien mit e/a-Vorgängen ausgelastet sind, wird die Datenträger Geschwindigkeit im Cache aufgefüllt, und die Schreibleistung wird zurückgegeben.

- Beim Zwischenspeichern von Lese-e/a-Vorgängen ist das Szenario, in dem der Cache am nützlichsten ist, die sequenzielle Speicherung der Daten auf dem Datenträger, und der Cache kann mit einem Lesevorgang versehen werden (es wird davon ausgegangen, dass der nächste Sektor die Daten enthält, die als nächstes angefordert werden).
- Wenn die e/a-Lesevorgänge zufällig durchlaufen werden, ist es unwahrscheinlich, dass die Zwischenspeicherung auf dem Laufwerk Controller eine Erweiterung der Datenmenge bietet, die vom Datenträger gelesen werden kann. Jede Erweiterung ist nicht vorhanden, wenn das Betriebssystem oder die Anwendungs basierte Cache Größe größer als die hardwarebasierte Cache Größe ist.

  Im Fall von Active Directory wird der Cache nur durch die RAM-Größe beschränkt.

### <a name="ssd-considerations"></a>SSD-Überlegungen

Bei SSDs handelt es sich um ein völlig anderes Tier als bei Spindel basierten Festplatten. Die zwei wichtigsten Kriterien bleiben jedoch bestehen: "Wie viele IOPS kann es verarbeiten?" und "wie hoch ist die Latenz für diese IOPS?" Im Vergleich zu Spindel basierten Festplatten können SSDS höhere e/a-Mengen verarbeiten und geringere Latenzzeiten aufweisen. Im allgemeinen und zum Zeitpunkt der Erstellung dieses Artikels sind SSDs bei einem Vergleich mit Kosten pro GB sehr kostengünstig und sind im Hinblick auf die Speicherleistung sehr kostengünstig zu berücksichtigen.

Überlegungen:

- Sowohl IOPS als auch Latenzen sind für die Hersteller Entwürfe sehr subjektiv und werden in einigen Fällen als eine schlechtere Leistung betrachtet, als auf Spindel basierten Technologien. Kurz gesagt, ist es wichtiger, das Laufwerk der Hersteller Spezifikationen nach Laufwerk zu überprüfen und zu validieren.
- IOPS-Typen können in Abhängigkeit davon, ob Sie Lese-oder Schreibvorgänge sind, sehr unterschiedliche Zahlen aufweisen. AD DS Dienste, die in der Regel überwiegend auf Lese basiert basieren, werden weniger beeinträchtigt als einige andere Anwendungsszenarien.
- "Ausdauer schreiben" – Dies ist das Konzept, das SSD-Zellen schließlich abgleichen. Verschiedene Hersteller behandeln diese Herausforderungen unterschiedlichen Fashions. Zumindest für das Daten Bank Laufwerk ermöglicht das überwiegend gelesene e/a-Profil das Herunterspielen der Bedeutung dieses Problems, da die Daten nicht stark flüchtig sind.

### <a name="summary"></a>Zusammenfassung

Eine Möglichkeit, den Speicher zu berücksichtigen, ist das einarbeiten mit dem Haushalt. Stellen Sie sich vor, dass die IOPS des Mediums, auf dem die Daten gespeichert sind, der Hauptgrund für den Haushalt ist. Wenn dies (z. b. Stämme in der Pipe) oder eingeschränkt (es ist reduziert oder zu klein) ist, werden alle senken im Haushalt wieder hergestellt, wenn zu viel Wasser verwendet wird (zu viele Gäste). Dies entspricht in etwa einer freigegebenen Umgebung, in der ein oder mehrere Systeme freigegebenen Speicher in einem SAN/NAS/iSCSI mit demselben zugrunde liegenden Medium nutzen. Es gibt verschiedene Ansätze zum Auflösen der verschiedenen Szenarien:

- Für einen reduzierten oder unter großen Ausgleich ist ein vollständiger Ersetzungs-und Korrekturbedarf erforderlich. Dies ähnelt dem Hinzufügen neuer Hardware oder der Verteilung der Systeme mithilfe des freigegebenen Speichers in der gesamten Infrastruktur.
- Eine gekoppelte Pipe bezeichnet in der Regel die Identifizierung von einem oder mehreren problematischen Problemen und das Entfernen dieser Probleme. In einem Speicher Szenario könnte dies Speicher-oder System Sicherungen, synchronisierte Antivirenscans auf allen Servern und synchronisierte Defragmentierungssoftware sein, die während der Spitzenzeiten ausgeführt wird.

Bei jedem Grundlagen-Entwurf werden mehrere ihm ausgleicht in den Hauptweg übertragen. Wenn eine dieser ihm ausgleicht oder ein Verknüpfungs Punkt beendet wird, werden nur die Dinge hinter diesem Verknüpfungs Punkt wieder hochskalieren. In einem Speicher Szenario könnte dies ein überladener Switch (SAN/NAS/iSCSI-Szenario), Treiber Kompatibilitätsprobleme (falscher Treiber/HBA-Firmware/Storport. sys-Kombination) oder Sicherung/Antivirus/Defragmentierung sein. Um zu ermitteln, ob der Speicher "Pipe" groß genug ist, müssen die IOPS und die e/a-Größe gemessen werden. Fügen Sie Sie bei jedem Joint zusammen, um einen ausreichenden "pipedurchmesser" zu gewährleisten.

## <a name="appendix-d---discussion-on-storage-troubleshooting---environments-where-providing-at-least-as-much-ram-as-the-database-size-is-not-a-viable-option"></a>Anhang D-Diskussion zur Speicherproblem Behandlung: Umgebungen, in denen mindestens so viel Arbeitsspeicher bereitgestellt wird, wie die Datenbankgröße nicht praktikabel ist

Es ist hilfreich zu verstehen, warum diese Empfehlungen vorhanden sind, damit die Änderungen in der Speichertechnologie untergebracht werden können. Diese Empfehlungen sind aus zwei Gründen vorhanden. Die erste ist die Isolation von e/a, sodass sich Leistungsprobleme (d. h. Paging) auf der Betriebssystem Spindel nicht auf die Leistung der Datenbank und der e/a-profile auswirken. Die zweite besteht darin, dass die Protokolldateien für AD DS (und die meisten Datenbanken) sequenziell sind und die Spindel basierten Festplatten und Caches bei der Verwendung mit sequenziellen e/a-Vorgängen im Vergleich zu den eher zufälligen e/a-Mustern des Betriebssystems und fast reine Zufalls-e/a-Muster des AD DS Daten Bank Laufwerks. Durch die Isolierung der sequenziellen e/a-Vorgänge auf einem separaten physischen Laufwerk kann der Durchsatz erhöht werden. Die Herausforderung, die die heutigen Speicheroptionen darstellen, besteht darin, dass die grundlegenden Annahmen hinter diesen Empfehlungen nicht mehr zutreffen. In vielen virtualisierten Speicher Szenarien, wie z. b. iSCSI-, San-, NAS-und Virtual Disk-Image Dateien, werden die zugrunde liegenden Speichermedien auf mehreren Hosts freigegeben, sodass sowohl die "Isolation der e/a" als auch die "sequenziellen e/a-Optimierung"-Aspekte völlig nealisiert werden. Tatsächlich wird in diesen Szenarien eine zusätzliche Komplexitäts Ebene hinzugefügt, in der andere Hosts, die auf die freigegebenen Medien zugreifen, die Reaktionsfähigkeit des Domänen Controllers beeinträchtigen können.

Bei der Planung der Speicherleistung gibt es drei Kategorien, die berücksichtigt werden müssen: der Status des kalten Caches, der Status des erwärmten Caches und die Sicherung/Wiederherstellung Der Status des kalten Caches tritt in Szenarien auf, z. b. wenn der Domänen Controller anfänglich neu gestartet oder der Active Directory-Dienst neu gestartet wird und keine Active Directory Daten im RAM vorhanden sind. Der Status "warm Cache" ist, in dem sich der Domänen Controller in einem stabilen Zustand befindet und die Datenbank zwischengespeichert wird. Diese müssen beachtet werden, da Sie sehr unterschiedliche Leistungsprofile Steuern und ausreichend RAM zum Zwischenspeichern der gesamten Datenbank zur Verfügung steht, wenn der Cache kalt ist. Sie können den Leistungs Entwurf für diese beiden Szenarios mit der folgenden Analogie in Erwägung gezogen. die Erwärmung des kalten Caches ist ein "Sprint" und das Ausführen eines Servers mit einem warmen Cache ist ein "Marathon".

Sowohl für das Szenario für kalte Caches als auch für den warmen Cache wird die Frage, wie schnell der Speicher die Daten vom Datenträger in den Arbeitsspeicher verschieben kann. Das Aufwärmen des Caches ist ein Szenario, in dem sich die Leistung im Laufe der Zeit verbessert, wenn mehr Abfragen Daten wieder verwenden, die Cache-Treffer Rate zunimmt und die Häufigkeit, mit der auf den Datenträger gehen muss, abnimmt. Demzufolge sinkt die Beeinträchtigung der Leistung von Datenträgern. Jegliche Beeinträchtigung der Leistung ist nur vorübergehend, während darauf gewartet wird, dass der Cache warm ist, und die maximale, vom systemabhängige zulässige Größe vergrößert. Die Konversation kann so vereinfacht werden, wie schnell die Daten vom Datenträger abgerufen werden können. Dies ist ein einfaches Maß für die IOPS, die für Active Directory verfügbar sind. Dies ist für IOPS, die aus dem zugrunde liegenden Speicher verfügbar sind, subjektiv. Aus Sicht der Planung, da das Aufwärmen der Cache-und Sicherungs-/Wiederherstellungsszenarien in der Regel außerhalb der Stunden stattfindet und für die Last des DC subjektiv ist, gibt es keine allgemeinen Empfehlungen, es sei denn, diese Aktivitäten sind geplant. für Zeiten außerhalb der Spitzenzeiten.

In den meisten Szenarien ist AD DS in den meisten Fällen eine Lese-e/a, normalerweise ein Verhältnis von 90% Lese-/10% Schreibvorgänge. Lese-e/a-Vorgänge sind häufig der Engpass für die Benutzer Darstellung und mit Schreib-e/a-Vorgängen, die die Schreibleistung beeinträchtigen. Da e/a-Vorgänge für die NTDS. dit vorwiegend zufällig erfolgen, bietet der Cache tendenziell einen minimalen Vorteil für Lese-e/a-Vorgänge, sodass es wesentlich wichtiger ist, den Speicher für das Lese-e/a-Profil richtig zu konfigurieren.

Bei normalen Betriebsbedingungen wird durch das Ziel der Speicher Planung die Wartezeit für eine Anforderung von AD DS von der Festplatte minimiert. Dies bedeutet im Wesentlichen, dass die Anzahl der ausstehenden und ausstehenden e/a-Vorgänge kleiner als oder gleich der Anzahl der Pfade zum Datenträger ist. Es gibt eine Vielzahl von Möglichkeiten, dies zu messen. In einem Szenario mit der Leistungsüberwachung lautet die allgemeine Empfehlung, dass LogicalDisk ( *\<NTDS\>-Daten Bank Laufwerk*) \Mittlere Sek./Lesevorgänge kleiner als 20 MS sind. Der gewünschte Betriebs Schwellenwert muss wesentlich niedriger sein, vorzugsweise möglichst nahe an der Geschwindigkeit des Speichers im Bereich von 2 bis 6 Millisekunden (. 002 bis .006 Sekunde), je nach Art des Speichers.

Beispiel:

![Speicherlatenz Diagramm](media/capacity-planning-considerations-storage-latency.png)

Analysieren des Diagramms:

- **Grünes Oval auf der linken Seite –** Die Latenz bleibt bei 10 MS konsistent. Die Auslastung steigt von 800 IOPS auf 2400 IOPS. Dies ist der absolute Grund für die schnelle Verarbeitung einer e/a-Anforderung durch den zugrunde liegenden Speicher. Dies unterliegt den Besonderheiten der Speicherlösung.
- **Burgund Oval auf der rechten Seite –** Der Durchsatz bleibt vom Ende des grünen Kreises bis zum Ende der Datensammlung flach, während die Latenz weiterhin zunimmt. Dies zeigt, dass die Anforderungs Volumes, die die physischen Beschränkungen des zugrunde liegenden Speichers überschreiten, länger in der Warteschlange verbracht haben, die darauf warten, an das Speichersubsystem gesendet zu werden.

Anwenden dieses Wissens:

- **Auswirkung auf einen Benutzer, der die Mitgliedschaft einer großen Gruppe abfragt –** Angenommen, Sie müssen 1 MB Daten vom Datenträger lesen, die Menge an e/a-Vorgängen und die benötigte Dauer können wie folgt ausgewertet werden:
  - Active Directory Datenbankseiten sind 8 KB groß. 
  - Mindestens 128 Seiten müssen vom Datenträger gelesen werden. 
  - Wenn nichts zwischengespeichert wird, dauert es im Fußboden (10 ms) mindestens 1,28 Sekunden, bis die Daten vom Datenträger geladen werden, damit Sie an den Client zurückgegeben werden. Bei 20 ms, bei denen der Durchsatz des Speichers seit dem Abgleich lange abgelaufen ist und auch das empfohlene Maximum ist, nimmt es 2,5 Sekunden in Anspruch, die Daten vom Datenträger zu erhalten, damit Sie an den Endbenutzer zurückgegeben werden können.  
- **Mit welcher Geschwindigkeit wird der Cache erwärmt –** Wenn Sie davon ausgehen, dass die Client Last den Durchsatz für dieses Speicher Beispiel maximiert, wird der Cache mit einer Rate von 2400 IOPS &times; 8 KB pro e/a erwärmt. Oder ungefähr 20 MB/s pro Sekunde, laden Sie ca. 1 GB der Datenbank alle 53 Sekunden in den Arbeitsspeicher.

> [!NOTE]
> Es ist normalerweise in kurzen Zeitabständen, den Anstieg der Wartezeiten zu beobachten, wenn Komponenten aggressiv auf den Datenträger lesen oder schreiben, z. b. wenn das System gesichert wird oder wenn AD DS Garbage Collection ausgeführt wird. Zusätzlich zu den Berechnungen sollte zusätzlicher oberraum bereitgestellt werden, um diese periodischen Ereignisse zu berücksichtigen. Das Ziel, einen ausreichenden Durchsatz bereitzustellen, um diese Szenarios ohne Beeinträchtigung der normalen Funktion zu unterstützen.

Wie Sie sehen können, gibt es auf der Grundlage des Speicher Entwurfs eine physische Beschränkung, wie schnell der Cache möglicherweise warm ist. Wie hoch ist der Cache für eingehende Client Anforderungen, bis zu dem Satz, den der zugrunde liegende Speicher bereitstellen kann. Durch das Ausführen von Skripts, um den Cache während der Spitzenzeiten "vorab zu" machen, wird der Lastenausgleich durch echte Client Anforderungen ermöglicht. Dies kann sich negativ auf die Bereitstellung von Daten auswirken, die von Clients zuerst benötigt werden, da dadurch der Wettbewerb für knappe Datenträger Ressourcen generiert wird, da künstliche Versuche, den Cache zu erwärmen, Daten laden, die für die Clients, die den DC kontaktieren, nicht relevant sind.
