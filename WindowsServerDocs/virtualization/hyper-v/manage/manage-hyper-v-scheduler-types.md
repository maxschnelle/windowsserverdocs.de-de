---
title: Grundlegendes zu und Verwendung von Hyper-V-Hypervisor-Scheduler-Typen
description: Bietet Informationen für Hyper-v-Host Administratoren zur Verwendung von Hyper-v-Scheduler-Modi.
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 6cb13f84-cb50-4e60-a685-54f67c9146be
ms.openlocfilehash: 8ba413b831c7b11780113ee2ffd3cce598781a44
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465574"
---
# <a name="managing-hyper-v-hypervisor-scheduler-types"></a>Verwalten von Hyper-V-Hypervisor-Scheduler-Typen

>Gilt für: Windows 10, Windows Server 2016, Windows Server, Version 1709, Windows Server, Version 1803, Windows Server 2019

In diesem Artikel werden neue Modi der Logik für die Planung virtueller Prozessoren beschrieben, die zuerst in Windows Server 2016 eingeführt wurden. Diese Modi oder Scheduler-Typen bestimmen, wie der Hyper-V-Hypervisor die Arbeit über virtuelle Gast Prozessoren hinweg ordnet und verwaltet. Ein Hyper-V-Host Administrator kann Hypervisor-planertypen auswählen, die am besten für die virtuellen Gastcomputer (Virtual Machines, VMS) geeignet sind, und die VMs so konfigurieren, dass Sie von der Planungslogik profitieren.

>[!NOTE]
>Updates sind erforderlich, um die in diesem Dokument beschriebenen Features für den Hypervisor-Scheduler zu verwenden. Weitere Informationen finden Sie unter [erforderliche Updates](#required-updates).

## <a name="background"></a>Hintergrund

Vor der Erörterung der Logik und der Kontrollen hinter der virtuellen Hyper-V-Prozessor Planung ist es hilfreich, die grundlegenden Konzepte in diesem Artikel zu überprüfen.

### <a name="understanding-smt"></a>Informationen zu SMT

Gleichzeitiges Multithreading (oder SMT) ist ein Verfahren, das in modernen Prozessor Entwürfen genutzt wird, mit dem die Ressourcen des Prozessors von separaten, unabhängigen Ausführungsthreads gemeinsam genutzt werden können. SMT bietet im Allgemeinen eine geringfügige Leistungssteigerung für die meisten Arbeits Auslastungen, indem Berechnungen nach Möglichkeit parallelisiert werden, um den Anweisungs Durchsatz zu erhöhen, obwohl keine Leistungssteigerung oder sogar ein geringfügiger Leistungsverlust auftreten kann, wenn Konflikte zwischen Threads für freigegebene Prozessorressourcen werden verwendet.
Prozessoren, die SMT unterstützen, sind sowohl bei Intel als auch bei AMD verfügbar Intel bezieht sich auf die SMT-Angebote als Intel Hyperthreading-Technologie oder Intel HT.

Für den Zweck dieses Artikels gelten die Beschreibungen von SMT und deren Verwendung durch Hyper-V gleichermaßen für Intel-und AMD-Systeme.

* Weitere Informationen zur Intel HT-Technologie finden Sie in der [Intel Hyper-Threading-Technologie](https://www.intel.com/content/www/us/en/architecture-and-technology/hyper-threading/hyper-threading-technology.html) .

* Weitere Informationen zu AMD SMT finden Sie in [der Kernarchitektur "Zen"](https://www.amd.com/en/technologies/zen-core) .

## <a name="understanding-how-hyper-v-virtualizes-processors"></a>Grundlegendes zur Virtualisierung von Prozessoren durch Hyper-V

Vor der Betrachtung der Hypervisor-planertypen ist es auch hilfreich, die Hyper-V-Architektur zu verstehen. Eine allgemeine Zusammenfassung finden Sie in der [Übersicht über die Hyper-V-Technologie](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-technology-overview). Dies sind wichtige Konzepte für diesen Artikel:

* Hyper-V erstellt und verwaltet virtuelle Computer Partitionen, für die Compute-Ressourcen zugeordnet und freigegeben werden, unter Kontrolle über den Hypervisor. Partitionen bieten starke Isolations Grenzen zwischen allen virtuellen Gast Computern und zwischen Gast-VMS und der Stamm Partition.

* Die Stamm Partition ist selbst eine virtuelle Computer Partition, obwohl Sie über eindeutige Eigenschaften und weitaus größere Berechtigungen als virtuelle Gastcomputer verfügt. Die Stamm Partition stellt die Verwaltungsdienste zur Verfügung, die alle virtuellen Gastcomputer steuern, Unterstützung für virtuelle Geräte für Gäste bereitstellen und alle Geräte-e/a für virtuelle Gast Maschinen verwalten. Microsoft empfiehlt dringend, keine anwendungsworkloads in der Stamm Partition auszuführen.

* Jeder virtuelle Prozessor (VP) der Stamm Partition ist 1:1 einem zugrunde liegenden logischen Prozessor (LP) zugeordnet. Ein Host-VP wird immer auf der gleichen zugrunde liegenden LP ausgeführt – es gibt keine Migration der VPS der Stamm Partition.

* Standardmäßig können die LPs, auf denen Host-VPS ausgeführt wird, auch Gast-VPS ausführen.

* Ein Gast-VP kann vom Hypervisor geplant werden, damit er auf allen verfügbaren logischen Prozessoren ausgeführt werden kann. Der Hypervisor-Planer kümmert sich um die zeitliche Cache Lokalität, die NUMA-Topologie und viele andere Faktoren beim Planen eines Gast-VP-Diensts. letztlich könnte der VP auf jeder Host-LP geplant werden.

## <a name="hypervisor-scheduler-types"></a>Typen von Hypervisor-Scheduler

Ab Windows Server 2016 unterstützt der Hyper-V-Hypervisor verschiedene Modi der planerlogik, die bestimmen, wie der Hypervisor virtuelle Prozessoren auf den zugrunde liegenden logischen Prozessoren plant. Diese Scheduler-Typen lauten wie folgt:

- [Der klassische, faire Freigabe Planer](#the-classic-scheduler)
- [Der Kern Planer](#the-core-scheduler)
- [Der Stamm Planer](#the-root-scheduler)

### <a name="the-classic-scheduler"></a>Der klassische Scheduler

Der klassische Scheduler war seit seiner Inbetriebnahme der Standardwert für alle Versionen des Windows Hyper-v-Hypervisors, einschließlich Windows Server 2016 Hyper-v. Der klassische Scheduler bietet eine faire Freigabe, präemptives Roundrobin-Planungsmodell für virtuelle Gast Prozessoren.

Der klassische schedulertyp ist die am besten geeignete Option für die große Mehrheit herkömmlicher Hyper-V-Verwendungen – für Private Clouds, Hostinganbieter usw. Die Leistungsmerkmale sind gut verständlich und am besten optimiert, um eine Vielzahl von Virtualisierungsszenarien zu unterstützen, z. b. das über-Abonnement von VPS zu LPs, das gleichzeitige Ausführen von vielen heterogenen virtuellen Computern und Workloads, die größere Skalierung Leistungs-VMS, die den vollständigen Featuresatz von Hyper-V ohne Einschränkungen unterstützen, und vieles mehr.

### <a name="the-core-scheduler"></a>Der Kern Planer

Der Hypervisor Core Scheduler ist eine neue Alternative zur klassischen Scheduler-Logik, die in Windows Server 2016 und Windows 10, Version 1607, eingeführt wurde. Der Kern Planer bietet eine starke Sicherheitsgrenze für die workloadworkloadisolation und reduzierte Leistungsschwankungen für Workloads innerhalb von VMS, die auf einem SMT-fähigen Virtualisierungshost ausgeführt werden. Der Kern Planer ermöglicht das gleichzeitige Ausführen von virtuellen SMT-und nicht-SMT-Computern auf dem gleichen SMT-aktivierten Virtualisierungshost.

Der Kern Planer nutzt die SMT-Topologie des Virtualisierungshosts und macht optional SMT-Paare für Gast-VMS verfügbar, und es werden Gruppen von virtuellen Gast Prozessoren von demselben virtuellen Computer auf Gruppen von SMT-logischen Prozessoren geplant. Dies erfolgt symmetrisch, sodass VPS in Gruppen von zwei Gruppen geplant werden, und ein Kern wird nie von virtuellen Computern gemeinsam genutzt, wenn LPs in Gruppen von zwei Gruppen verwendet werden.
Wenn der VP für einen virtuellen Computer ohne aktivierte SMT geplant ist, wird der gesamte Kern bei der Ausführung des VP-Computers genutzt.

Das Gesamtergebnis des Kern Planers ist Folgendes:

* Gast-VPS sind so eingeschränkt, dass Sie auf zugrunde liegenden physischen Kern Paaren ausgeführt werden, indem Sie einen virtuellen Computer auf die Kern Grenzen des Prozessors isolieren und dadurch die Sicherheits Anfälligkeit für Angriffe durch böswillige virtuelle Computer verringern.

* Die Varianz im Durchsatz ist erheblich reduziert.

* Die Leistung wird möglicherweise reduziert, denn wenn nur eine Gruppe von VPS ausgeführt werden kann, wird nur einer der Anweisungs Datenströme im Kern ausgeführt, während der andere in den Leerlauf versetzt wird.

* Das Betriebssystem und die Anwendungen, die auf dem virtuellen Gastcomputer ausgeführt werden, können SMT-Verhaltens-und Programmierschnittstellen (APIs) verwenden, um die Arbeit über SMT-Threads zu steuern und zu verteilen, genauso wie bei der Ausführung nicht virtualisierter Anwendungen.

* Eine starke Sicherheitsgrenze für die Isolation von Gast Arbeitslasten (Gast-VPS) ist darauf beschränkt, auf zugrunde liegenden physischen Kern Paaren ausgeführt zu werden

Der Kern Planer wird standardmäßig ab Windows Server 2019 verwendet. Unter Windows Server 2016 ist der Kern Planer optional und muss vom Hyper-V-Host Administrator explizit aktiviert werden, und der klassische Scheduler ist die Standardeinstellung.

#### <a name="core-scheduler-behavior-with-host-smt-disabled"></a>Kern Planer-Verhalten mit deaktiviertem Host SMT

Wenn der Hypervisor für die Verwendung des kernplanertyps konfiguriert ist, aber die SMT-Funktion auf dem Virtualisierungshost deaktiviert oder nicht vorhanden ist, verwendet der Hypervisor das klassische schedulerverhalten, unabhängig von der Einstellung für den hypervisorschedulertyp.

### <a name="the-root-scheduler"></a>Der Stamm Planer

Der Stamm Planer wurde mit Windows 10, Version 1803, eingeführt. Wenn der stammschedulertyp aktiviert ist, steuert der Hypervisor die Arbeitsplanung der Stamm Partition. Der NT-Scheduler in der Betriebssystem Instanz der Stamm Partition verwaltet alle Aspekte der Planungsarbeit an System LPs.

Der Stamm Planer erfüllt die besonderen Anforderungen, die bei der Unterstützung einer hilfsprogrammpartition bestehen, um eine starke workloadisolation bereitzustellen, wie Sie mit Windows Defender Application Guard (WDAG) verwendet wird. In diesem Szenario bietet das belassen von Planungsaufgaben für das Stamm Betriebssystem mehrere Vorteile. Beispielsweise können CPU-Ressourcen Steuerungen, die auf Container Szenarien anwendbar sind, mit der hilfsprogrammpartition verwendet werden, um die Verwaltung und Bereitstellung zu vereinfachen. Außerdem kann der Stamm Betriebssystem-Scheduler im Container problemlos Metriken zur CPU-Auslastung der Arbeitsauslastung erfassen und diese Daten als Eingabe für dieselbe Planungsrichtlinie verwenden, die für alle anderen Arbeits Auslastungen im System gilt. Diese Metriken helfen Ihnen auch, eine eindeutige Attribut Arbeit in einem Anwendungs Container für das Host System durchzuführen. Die Nachverfolgung dieser Metriken ist mit herkömmlichen VM-Workloads schwieriger, bei denen einige Arbeiten an allen laufenden virtuellen Computern in der Stamm Partition stattfinden.

#### <a name="root-scheduler-use-on-client-systems"></a>Verwendung von root Scheduler auf Client Systemen

Ab Windows 10, Version 1803, wird der Stamm Planer standardmäßig nur auf Client Systemen verwendet, wobei der Hypervisor Unterstützung für virtualisierungsbasierte Sicherheit und WDAG-Arbeits Auslastungs Isolation aktiviert werden kann, und für den ordnungsgemäßen Betrieb zukünftiger Systeme mit heterogene Kern Architekturen. Dies ist die einzige unterstützte Konfiguration für den Hypervisor-Scheduler für Client Systeme. Administratoren sollten nicht versuchen, den standardmäßigen Hypervisor-Planertyp auf Windows 10-Client Systemen zu überschreiben.

#### <a name="virtual-machine-cpu-resource-controls-and-the-root-scheduler"></a>CPU-Ressourcen Steuerelemente für virtuelle Computer und der Stamm Planer

Die von Hyper-V bereitgestellten Prozessorressourcen-Steuerelemente für virtuelle Computer werden nicht unterstützt, wenn der Hypervisor-Stamm Planer aktiviert ist, da die Scheduler-Logik des Stamm Betriebssystems Host Ressourcen auf globaler Basis verwaltet und keine Kenntnisse über die bestimmte Konfigurationseinstellungen. Die Hyper-V-Prozessorressourcen Kontrolle, wie z. b. Caps, Gewichtungen und Reserven, sind nur anwendbar, wenn der Hypervisor die VP-Planung direkt steuert, z. b. mit den klassischen und den wichtigsten Scheduler-Typen.

#### <a name="root-scheduler-use-on-server-systems"></a>Verwendung von root Scheduler auf Serversystemen

Der Stamm Planer wird zurzeit nicht für die Verwendung mit Hyper-V auf Servern empfohlen, da seine Leistungsmerkmale noch nicht vollständig charakterisiert und optimiert wurden, um die breite Palette von Workloads zu erfüllen, die für viele servervirtualisierungsbereitstellungen typisch sind.

## <a name="enabling-smt-in-guest-virtual-machines"></a>Aktivieren von SMT auf virtuellen Gast Computern

Sobald der Hypervisor des Virtualisierungshosts für die Verwendung des kernplanertyps konfiguriert ist, können virtuelle Gastcomputer für die Verwendung von SMT konfiguriert werden, wenn gewünscht. Das verfügbar machen der Tatsache, dass VPS mit einem virtuellen Gastcomputer Hyperthread werden, ermöglicht dem Planer im Gast Betriebssystem und den Arbeits Auslastungen, die auf der VM ausgeführt werden, die SMT-Topologie in ihrer eigenen Arbeitsplanung zu erkennen und zu nutzen. Auf Windows Server 2016 ist Gast SMT nicht standardmäßig konfiguriert und muss vom Hyper-V-Host Administrator explizit aktiviert werden. Ab Windows Server 2019 erben neue virtuelle Computer, die auf dem Host erstellt werden, standardmäßig die SMT-Topologie des Hosts.  Das heißt, eine VM der Version 9,0, die auf einem Host mit 2 SMT-Threads pro Kern erstellt wurde, würde ebenfalls 2 SMT-Threads pro Kern sehen.

PowerShell muss zum Aktivieren von SMT auf einem virtuellen Gastcomputer verwendet werden. im Hyper-V-Manager wird keine Benutzeroberfläche bereitgestellt.
Um SMT auf einem virtuellen Gastcomputer zu aktivieren, öffnen Sie ein PowerShell-Fenster mit ausreichenden Berechtigungen, und geben Sie Folgendes ein:

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <n>
```

Dabei ist <n> die Anzahl der SMT-Threads pro Kern, die der Gast-VM angezeigt wird.  
Beachten Sie, dass <n> = 0 den Wert hwthreadzähltpercore auf den Wert des SMT-Threads des Hosts pro Kernwert festgelegt.

>[!NOTE] 
>Das Festlegen von hwthreadzähltpercore = 0 wird ab Windows Server 2019 unterstützt.

Im folgenden finden Sie ein Beispiel für System Informationen, die vom Gast Betriebssystem auf einem virtuellen Computer mit zwei virtuellen Prozessoren und SMT aktiviert wurden. Das Gast Betriebssystem erkennt zwei logische Prozessoren, die zu demselben Kern gehören.

![Screenshot, der msinfo32 in einer Gast-VM mit aktivierter SMT anzeigt](media/Hyper-V-CoreScheduler-VM-Msinfo32.png)

## <a name="configuring-the-hypervisor-scheduler-type-on-windows-server-2016-hyper-v"></a>Konfigurieren des Hypervisor-Scheduler-Typs auf Windows Server 2016 Hyper-V

Windows Server 2016 Hyper-V verwendet standardmäßig das klassische Hypervisor-Scheduler-Modell. Der Hypervisor kann optional für die Verwendung des Kern Planers konfiguriert werden, um die Sicherheit zu erhöhen, indem Gast-VPS für die Ausführung auf entsprechenden physischen SMT-Paaren eingeschränkt werden und die Verwendung von virtuellen Computern mit SMT-Zeitplanung für Ihre Gast-VPS unterstützt wird.

>[!NOTE]
>Microsoft empfiehlt, dass alle Kunden, die Windows Server 2016 Hyper-V ausführen, den Kern Planer auswählen, um sicherzustellen, dass Ihre Virtualisierungshosts optimal vor potenziell schädlichen Gast-VMS geschützt werden.

## <a name="windows-server-2019-hyper-v-defaults-to-using-the-core-scheduler"></a>Windows Server 2019 Hyper-V verwendet standardmäßig den Kern Planer

Um sicherzustellen, dass Hyper-v-Hosts in der optimalen Sicherheitskonfiguration bereitgestellt werden, verwendet Windows Server 2019 Hyper-v jetzt standardmäßig das Core-Hypervisor-Scheduler-Modell. Der Host Administrator kann optional den Host so konfigurieren, dass er den klassischen Legacy Planer verwendet. Administratoren sollten vor dem Überschreiben der Standardeinstellungen für den Scheduler die Auswirkungen der einzelnen schedulertypen auf die Sicherheit und Leistung von Virtualisierungshosts sorgfältig lesen, verstehen und berücksichtigen.  Weitere Informationen finden Sie Untergrund Legendes zur [Hyper-V-Scheduler-Typauswahl](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/understanding-hyper-v-scheduler-type-selection) .

### <a name="required-updates"></a>Erforderliche Updates

>[!NOTE]
>Die folgenden Updates sind erforderlich, um die in diesem Dokument beschriebenen Features für den Hypervisor-Scheduler zu verwenden. Diese Updates enthalten Änderungen zur Unterstützung der neuen Option "hypervisorschedulertype" (BCD), die für die Host Konfiguration erforderlich ist.

| Version | Version  | Update erforderlich | KB-Artikel |
|--------------------|------|---------|-------------:|
|Windows Server 2016 | 1607 | 2018,07 C | [KB4338822](https://support.microsoft.com/help/4338822/windows-10-update-kb4338822) |
|Windows Server 2016 | 1703 | 2018,07 C | [KB4338827](https://support.microsoft.com/help/4338827/windows-10-update-kb4338827) |
|Windows Server 2016 | 1709 | 2018,07 C | [KB4338817](https://support.microsoft.com/help/4338817/windows-10-update-kb4338817) |
|Windows Server 2019 | 1804 | Keine | Keine |

## <a name="selecting-the-hypervisor-scheduler-type-on-windows-server"></a>Auswählen des Hypervisor-planertyps unter Windows Server

Die Konfiguration des Hypervisor-Planers wird über den BCD-Eintrag hypervisorschedulertype gesteuert.

Um einen Planertyp auszuwählen, öffnen Sie eine Eingabeaufforderung mit Administratorrechten:

``` command
     bcdedit /set hypervisorschedulertype type
```

Dabei ist `type` einer der folgenden:

* Classic
* Kern
* Root

Das System muss neu gestartet werden, damit Änderungen am Typ des Hypervisor-Planers wirksam werden.

>[!NOTE]
>Der Hypervisor-Stamm Planer wird zurzeit nicht unter Windows Server Hyper-V unterstützt. Hyper-V-Administratoren sollten nicht versuchen, den Stamm Planer für die Verwendung mit servervirtualisierungsszenarien zu konfigurieren.

## <a name="determining-the-current-scheduler-type"></a>Bestimmen des aktuellen planertyps

Sie können den aktuell verwendeten Hypervisor-Planertyp ermitteln, indem Sie das System Protokoll in Ereignisanzeige auf die aktuelle Hypervisor-Start Ereignis-ID 2 untersuchen, die den beim Hypervisor Launch konfigurierten Hypervisor-Planertyp meldet. Hypervisor-Start Ereignisse können vom Windows-Ereignisanzeige oder über PowerShell abgerufen werden.

Die Hypervisor-Start Ereignis-ID 2 gibt den Hypervisor-Planertyp an, wobei Folgendes gilt:

    1 = Classic scheduler, SMT disabled

    2 = Classic scheduler

    3 = Core scheduler

    4 = Root scheduler

![Screenshot der Hypervisor-Start Ereignis-ID 2 Details](media/Hyper-V-CoreScheduler-EventID2-Details.png)

![Screenshot mit Ereignisanzeige anzeigen der Hypervisor-Start Ereignis-ID 2](media/Hyper-V-CoreScheduler-EventViewer.png)

### <a name="querying-the-hyper-v-hypervisor-scheduler-type-launch-event-using-powershell"></a>Abfragen des Start Ereignisses für den Hyper-V-Hypervisor-Scheduler mithilfe von PowerShell

Geben Sie die folgenden Befehle von einer PowerShell-Eingabeaufforderung ein, um die Hypervisor-Ereignis-ID 2 mithilfe von PowerShell abzufragen.

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Hypervisor"; ID=2} -MaxEvents 1
```

![Screenshot der PowerShell-Abfrage und Ergebnisse für die Hypervisor-Start Ereignis-ID 2](media/Hyper-V-CoreScheduler-PowerShell.png)
