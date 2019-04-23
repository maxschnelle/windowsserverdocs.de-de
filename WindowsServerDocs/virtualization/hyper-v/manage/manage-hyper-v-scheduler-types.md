---
title: Verstehen und Verwenden von Hyper-V-Hypervisor-Scheduler-Typen
description: Bietet Informationen zu Hyper-V-Host-Administratoren bei der Verwendung von Hyper-V-Scheduler-Modi
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 6cb13f84-cb50-4e60-a685-54f67c9146be
ms.openlocfilehash: 7af6d68b02367d349580eacb27405c6f37e97ff8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871991"
---
# <a name="managing-hyper-v-hypervisor-scheduler-types"></a>Verwalten von Hyper-V-Hypervisor-Scheduler-Typen

>Gilt für: Windows 10, WindowsServer 2016, Windows Server, Version 1709, Windows Server, Version 1803, Windows Server-2019

Dieser Artikel beschreibt die neuen Modi der virtuellen Prozessor planen die Logik, die in Windows Server 2016 eingeführt wurden. Diese Modi oder Scheduler-Typen, bestimmen, wie der Hyper-V-Hypervisor belegt, und verwaltet Arbeit auf Gast virtuelle Prozessoren. Ein Hyper-V-Host-Administrator kann Hypervisor-Scheduler-Typen auswählen, die sich am besten für den virtuellen Gastcomputern (VMs) und konfigurieren, um die Planungslogik nutzen.

>[!NOTE]
>Updates sind erforderlich, die Hypervisor-Scheduler-Features in diesem Dokument beschrieben verwenden. Weitere Informationen finden Sie unter [erforderliche Updates](#required-updates).

## <a name="background"></a>Hintergrund

Ehe wir näher auf die Logik und die Steuerelemente hinter Hyper-V virtuellen Prozessor planen, ist es hilfreich sein, überprüfen die grundlegenden Konzepte, die in diesem Artikel behandelt.

### <a name="understanding-smt"></a>Grundlegendes zur SMT

Gleichzeitige multithreading oder SMT, ist eine Technik in moderner Prozessor Entwürfe verwendet, die Ressourcen des Prozessors von separaten, unabhängigen Ausführungsthreads gemeinsam genutzt werden kann. SMT in der Regel eine geringe Leistungssteigerung für die meisten Workloads durch die Parallelisierung von Berechnungen nach Möglichkeit bietet, die durch das Anweisung Durchsatz zu erhöhen, jedoch keine Leistung erhalten, oder sogar eine kleine Leistungsverluste auftreten, wenn Konflikte zwischen für threads Freigegebene Prozessorressourcen auftritt.
Prozessoren mit Unterstützung von SMT sind von Intel und AMD verfügbar. Intel bezieht sich auf ihre SMT-Angebote wie Intel Hyper-Threading-Technologie oder Intel HT.

Für die Zwecke dieses Artikels gelten die Beschreibungen der SMT und wie es von Hyper-V verwendet wird gleichermaßen für Intel- und AMD-Systeme.

* Weitere Informationen zu Intel Hyper-Threading-Technologie, finden Sie unter [Intel Hyper-Threading-Technologie](https://www.intel.com/content/www/us/en/architecture-and-technology/hyper-threading/hyper-threading-technology.html)

* Weitere Informationen zu AMD SMT, finden Sie unter [die Kernarchitektur "Zen"](https://www.amd.com/en/technologies/zen-core)

## <a name="understanding-how-hyper-v-virtualizes-processors"></a>Verstehen, wie Hyper-V Prozessoren virtualisiert

Anzusehen Hypervisor Scheduler-Typen, ist es auch hilfreich zu verstehen, die Hyper-V-Architektur. Finden Sie eine allgemeine Übersicht in [Übersicht über die Hyper-V-Technologie](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-technology-overview). Dies sind wichtige Konzepte in diesem Artikel:

* Hyper-V erstellt und verwaltet virtuelle Computer-Partitionen, über welche, die Compute Ressourcen zugeordnet und freigegeben werden, von der Hypervisor kontrolliert werden. Partitionen bieten hohe Isolationsgrenzen zwischen aller virtuellen Gastcomputer sowie zwischen virtuellen Gastcomputern sowie die Root-Partition.

* Das Stammpartition ist selbst ein VM-Partition, obwohl es sich um eindeutige Eigenschaften und viel mehr Berechtigungen als virtuelle Gastcomputer hat. Das Stammpartition bietet die Management-Dienste, die alle virtuellen Gastcomputern zu steuern, bietet Unterstützung für virtuelle Geräte für Gäste und alle Geräte-e/a für virtuelle Gastcomputer verwaltet. Microsoft empfiehlt dringend, keine arbeitsauslastungen von Anwendungen in der rootpartition ausgeführt.

* Jeder virtuelle Prozessor (VP) von der Stammpartition wird zugeordneten 1:1 für einen zugrunde liegenden logischen Prozessor (LP). Ein Host VP wird immer ausgeführt werden, auf dem gleichen zugrunde liegenden LP – es ist keine Migration von der Stammpartition VPs.

* Standardmäßig können die auf dem Host VPs ausgeführt LPs auch Gast VPs ausführen.

* Ein Gast VP möglicherweise vom Hypervisor zur Ausführung auf einem beliebigen verfügbaren logischen Prozessor geplant. Während der Hypervisor-Planer kümmert Ort des temporären Caches, NUMA-Topologie und viele andere Faktoren zu berücksichtigen, bei der Planung einer Gast-VP, konnte auf einem Host LP letztlich die VP geplant werden.

## <a name="hypervisor-scheduler-types"></a>Hypervisor-Scheduler-Typen

Ab Windows Server 2016 unterstützt die Hyper-V-Hypervisor mehrere Modi der Scheduler-Logik, die bestimmen, wie der Hypervisor virtuelle Prozessoren auf den zugrunde liegenden logischen Prozessoren geplant. Diese Scheduler-Typen sind:

- [Der klassische, Fair-Share-Planer](#the-classic-scheduler)
- [Der Kern-Planer](#the-core-scheduler)
- [Der Stamm-Planer](#the-root-scheduler)

### <a name="the-classic-scheduler"></a>Der klassische scheduler

Der klassische Planer wurde der Standardwert für alle Versionen von Windows Hyper-V-Hypervisor seit seiner Einführung, einschließlich Windows Server 2016 Hyper-V. Die klassische Scheduler bietet es sich um eine gleichmäßige preemptive Round-Robin-vorausplanungsmodells für virtuelle Gäste-Prozessoren.

Der klassische Scheduler-Typ ist der am besten geeignet für die überwiegende Mehrheit der herkömmliche Verwendung von Hyper-V – für private Clouds, Hostinganbieter und So weiter. Die Leistungsmerkmale gut verstanden und sind am besten unterstützen eine Vielzahl von Szenarios der Benutzerstatusvirtualisierung, z. B. die Überzeichnung von VPs zu LPs, viele heterogene VMs und Workloads gleichzeitig ausgeführt, das Ausführen von größeren hohe optimiert Leistung-VMs unterstützen die vollständige Funktion Satz von Hyper-V ohne Einschränkungen und vieles mehr.

### <a name="the-core-scheduler"></a>Der Kern-Planer

Der Hypervisor-Core-Planer ist eine neue Alternative zu der klassischen Scheduler-Logik, eingeführt in Windows Server 2016 und Windows 10 Version 1607. Der Planer Core bietet eine starke sicherheitsbegrenzung für Gast-Workloads zu isolieren und die Variabilität der Leistung für Arbeitslasten in virtuellen Computern, die auf einem SMT-fähigen Virtualisierungshost ausgeführt werden. Die Core-Scheduler können virtuelle Maschinen sowohl SMT als auch nicht-SMT gleichzeitig auf dem gleichen SMT-fähigen Virtualisierungshost ausgeführt.

Der Planer Core nutzt den Virtualisierungshost SMT-Topologie, und optional macht SMT-Paare auf virtuellen Gastcomputern und Zeitpläne Gruppen virtueller Prozessoren Gast aus demselben virtuellen Computer in Gruppen von logischen Prozessoren SMT. Dies erfolgt symmetrisch, sodass Wenn LPs sind Gruppen von zwei VPs in Gruppen von zwei geplant sind, und ein Kern zwischen virtuellen Computern niemals.
Wenn der VP für einen virtuellen Computer ohne SMT geplant ist aktiviert, Vice President bei der Ausführung der gesamte Core nutzen.

Das Gesamtergebnis des Zeitplanungsmoduls Core darstellt:

* Gast-VPs sind eingeschränkt, auf die zugrunde liegenden physischen Kern-Paare, ein virtuellen Computers auf Prozessor Core Grenzen zu isolieren, wodurch die Anfälligkeit für die Seiten-Kanal-Spoofingangriffen von schädlichen virtuellen Computern ausgeführt.

* Variabilität bei Durchsatz ist erheblich reduziert.

* Möglicherweise ist die Leistung beeinträchtigt, da nur zu einer Gruppe von VPs ausgeführt werden kann, führt nur eine Anweisung Streams im Kern, während die andere im Leerlauf befindet.

* SMT-Verhalten "und" programming Interfaces (APIs), um zu steuern und Verteilung von Arbeitsaufgaben über SMT-Threads, genau wie sie bei nicht virtualisierten ausführen, können das Betriebssystem und Anwendungen, die auf dem virtuellen Gastcomputer nutzen.

* Eine starke sicherheitsbegrenzung für Gast workloadisolation - Gast VPs sind eingeschränkt, auf die zugrunde liegenden physischen Kern-Paare, verringert die Anfälligkeit für die Seiten-Kanal-Spoofingangriffen ausgeführt.

Der Kern-Scheduler wird standardmäßig ab Windows Server-2019 verwendet werden. Unter Windows Server 2016 Core Planer ist optional und muss explizit aktiviert werden, durch den Administrator der Hyper-V-Host, und der klassischen Scheduler ist die Standardeinstellung.

#### <a name="core-scheduler-behavior-with-host-smt-disabled"></a>Scheduler Kernverhalten mit Host SMT deaktiviert

Wenn der Hypervisor so konfiguriert ist, dass der Kern-Scheduler-Typ verwenden, aber die SMT-Funktion deaktiviert oder nicht vorhanden ist, auf dem Virtualisierungshost ist, verwendet der Hypervisor die klassischen Planerverhaltens, unabhängig vom Hypervisor-Scheduler-Typ festlegen.

### <a name="the-root-scheduler"></a>Der Stamm-Planer

Der Stamm-Planer wurde mit Windows 10, Version 1803 eingeführt. Wenn der Scheduler-Stammtyp aktiviert ist, übergibt der Hypervisor die Kontrolle des Arbeit auf der Stammpartition zu planen. Der NT-Planer in der Stammpartition-BS-Instanz verwaltet alle Aspekte der Planung von arbeiten an LPs-System.

Der Stamm-Planer werden die individuellen Anforderungen mit Unterstützung von einer Partitions Hilfsprogramm inhärenten starken Workloads zu isolieren, angeben, wie mit Windows Defender Application Guard (WDAG) verwendet. Beim Verlassen der Planung von Aufgaben an das Rootbetriebssystem in diesem Szenario bietet mehrere Vorteile. Beispielsweise können für Container-Szenarios Steuerung der CPU-Ressourcen mit der Hilfsprogramm-Partition, die Vereinfachung der Verwaltung und Bereitstellung verwendet werden. Der Stamm-betriebssystemscheduler kann darüber hinaus sofort erfasst Metriken zur CPU-Auslastung im Container-Workload und verwenden diese Daten als Eingabe für die gleiche Richtlinie zur Taskplanung gilt für alle anderen arbeitsauslastungen im System. Diese dieselben Metriken helfen auch klar Attribut in einem Anwendungscontainer auf dem Hostsystem Arbeitsabläufe. Diese Metriken nachverfolgen ist schwieriger, mit herkömmlichen Workloads auf virtuellen Computern, findet die Arbeit in allen ausgeführten VM Namen statt in der rootpartition.

#### <a name="root-scheduler-use-on-client-systems"></a>Verwenden von Root Scheduler auf Clientsystemen

Der Stamm-Planer wird ab Windows 10, Version 1803, standardmäßig auf Clientsystemen nur verwendet, kann der Hypervisor zur Unterstützung der Virtualisierung basierende Sicherheitsverfahren und WDAG Workloads zu isolieren, und klicken Sie für den ordnungsgemäßen Betrieb der Systeme in der Zukunft mit aktiviert werden heterogene Core-Architekturen. Dies ist die Konfiguration des Schedulers nur unterstützten Hypervisor für Client-Systeme. Administratoren sollten nicht versuchen, den Standardtyp für die Planer von Hypervisor auf Windows 10-Clientsysteme zu überschreiben.

#### <a name="virtual-machine-cpu-resource-controls-and-the-root-scheduler"></a>Die Steuerung der VM-CPU-Ressourcen und der Stamm-scheduler

Die von Hyper-V bereitgestellte virtuelle Maschine Prozessor Ressourcenobjekte werden nicht unterstützt, wenn der Hypervisor-Stamm-Planer aktiviert ist, wie im stammbetriebssystem Scheduler Logik Hostressourcen auf globaler Basis verwaltet und keine Kenntnisse in Bezug eines virtuellen Computers besitzt bestimmte Konfigurationseinstellungen festgelegt werden. Die Hyper-V pro virtuellem Computer Prozessor Ressourcenobjekte, z. B. sowie der Gewichtungen und reserviert, gelten nur, bei der Hypervisor direkt VP Planung, z. B. wie bei das klassische Bereitstellungsmodell und das Core Scheduler Typen steuert.

#### <a name="root-scheduler-use-on-server-systems"></a>Verwenden von Root Scheduler auf Server-Systemen

Der Stamm-Scheduler ist für die Verwendung mit Hyper-V auf Servern zu diesem Zeitpunkt nicht empfohlen, da es sich bei seiner Leistungsmerkmale noch nicht voll gekennzeichnet und wurden optimiert, um eine Vielzahl von Workloads, die typisch für viele Server-Virtualisierung-Bereitstellungen zu ermöglichen.

## <a name="enabling-smt-in-guest-virtual-machines"></a>SMT in virtuellen Gastcomputern zu aktivieren.

Sobald dem Virtualisierungshost Hypervisor konfiguriert ist, um die Core-Scheduler-Typ verwenden, können virtuelle Gastcomputer SMT nutzen, bei Bedarf konfiguriert werden. Verfügbarmachen von der Tatsache, dass VPs Hyperthread auf einem virtuellen Gastcomputer, können den Scheduler in das Gastbetriebssystem und arbeitsauslastungen, die auf dem virtuellen Computer zu erkennen und die SMT-Topologie in ihre eigenen Planen von Arbeit zu nutzen. Unter Windows Server 2016 Gast SMT ist nicht standardmäßig konfiguriert und muss explizit durch den Hyper-V-Host-Administrator aktiviert werden. Windows Server-2019 ab, erben auf dem Host erstellten neuen virtuellen Computer der Topologie des Hosts SMT standardmäßig.  Eine Version 9.0 VM auf einem Host mit 2 SMT-Threads pro Kern erstellten sehen, also auch 2 SMT-Threads pro Kern.

PowerShell muss verwendet werden, um SMT in einem virtuellen Gastcomputer zu ermöglichen. Es gibt keine Benutzeroberfläche, die in Hyper-V-Manager bereitgestellt.
Um SMT in einem virtuellen Gastcomputer zu aktivieren, öffnen Sie ein PowerShell-Fenster mit ausreichenden Berechtigungen, und geben ein:

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <n>
```

Wo <n> ist die Anzahl der SMT-Threads pro Kern der Gast, der virtuelle Computer wird angezeigt.  
Beachten Sie, dass <n> = 0 wird den HwThreadCountPerCore Wert entsprechend der Anzahl von des Hosts SMT-Threads pro Core Wert festgelegt.

>[!NOTE] 
>Festlegen von HwThreadCountPerCore = 0 wird ab Windows Server-2019 unterstützt.

Unten ist ein Beispiel von Systeminformationen Gast-Betriebssystems auf einem virtuellen Computer mit 2 virtuelle Prozessoren unter entnommen und SMT aktiviert. Das Gastbetriebssystem erkennt 2 logische Prozessoren, die zum gleichen Kern gehören.

![Screenshot mit dem msinfo32 in einer Gast-VM mit SMT aktiviert](media/Hyper-V-CoreScheduler-VM-Msinfo32.png)

## <a name="configuring-the-hypervisor-scheduler-type-on-windows-server-2016-hyper-v"></a>Konfigurieren den Typ der Hypervisor-Planer unter Windows Server 2016 Hyper-V

Windows Server 2016 Hyper-V wird das Modell der klassischen Hypervisor-Scheduler wird standardmäßig verwendet. Der Hypervisor kann optional konfiguriert werden, um den Scheduler Core zu verwenden, um die Sicherheit zu erhöhen, indem Sie einschränken, Gast VPs zur Ausführung auf den entsprechenden physischen SMT-Paaren, und klicken Sie für die Unterstützung von virtuellen Computern mit SMT für ihre Gast VPs planen.

>[!NOTE]
>Microsoft empfiehlt, dass alle Kunden, die mit Windows Server 2016 Hyper-V-auswählen den Core-Scheduler, um sicherzustellen, dass ihre Virtualisierungshosts vor potenziell schädlichen Gast-VMs optimal geschützt sind.

## <a name="windows-server-2019-hyper-v-defaults-to-using-the-core-scheduler"></a>Windows Server 2019 Hyper-V verwendet standardmäßig den Core-Planer

Um sicherzustellen, dass Hyper-V-Hosts in die optimale Sicherheit Configuaration bereitgestellt werden, wird Windows Server 2019 Hyper-V jetzt die Core-hypervisormodell Scheduler wird standardmäßig verwendet. Der hostadministrator kann optional den Host, um die ältere klassische Scheduler verwenden konfigurieren. Administratoren sollten sorgfältig lesen, verstehen und berücksichtigen Sie die Auswirkungen, die jedes Zeitplanungsmodul-Typ für die Sicherheit und Leistung von Virtualisierungshosts vor dem Überschreiben der Einstellungen für den Scheduler Standard verfügt.  Finden Sie unter [Grundlegendes zu Hyper-V-Scheduler-Typauswahl](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/understanding-hyper-v-scheduler-type-selection) für Weitere Informationen.

### <a name="required-updates"></a>Erforderliche Updates

>[!NOTE]
>Die folgenden Updates sind erforderlich, die Hypervisor-Scheduler-Features in diesem Dokument beschrieben verwenden. Diese Updates enthalten Änderungen, um die neue Option "Hypervisorschedulertype" BCD unterstützen, die für die Konfiguration des Hosts erforderlich ist.

| Version | Version  | Update erforderlich | KB-Artikel |
|--------------------|------|---------|-------------:|
|Windows Server 2016 | 1607 | 2018.07 C | [KB4338822](https://support.microsoft.com/help/4338822/windows-10-update-kb4338822) |
|Windows Server 2016 | 1703 | 2018.07 C | [KB4338827](https://support.microsoft.com/help/4338827/windows-10-update-kb4338827) |
|Windows Server 2016 | 1709 | 2018.07 C | [KB4338817](https://support.microsoft.com/help/4338817/windows-10-update-kb4338817) |
|Windows Server 2019 | 1804 | Keine | Keine |

## <a name="selecting-the-hypervisor-scheduler-type-on-windows-server"></a>Auswählen des Hypervisors Planer unter Windows Server

Die Konfiguration des Schedulers Hypervisor wird über den BCD-Eintrag Hypervisorschedulertype gesteuert.

Wählen Sie einen Planer-Typ, öffnen Sie eine Eingabeaufforderung mit Administratorrechten aus:

``` command
     bcdedit /set hypervisorschedulertype type
```

Wo `type` ist einer der:

* Klassisch
* Core

Das System muss neu gestartet werden, für alle Änderungen an den Scheduler hypervisortyp wirksam wird.

>[!NOTE]
>Der Hypervisor-Stamm-Planer wird unter Windows Server Hyper-V zu diesem Zeitpunkt nicht unterstützt werden. Hyper-V-Administratoren sollten nicht versuchen, so konfigurieren Sie die Stamm-Planer für die Verwendung mit Server-Virtualisierung-Szenarien.

## <a name="determining-the-current-scheduler-type"></a>Bestimmen den aktuellen Scheduler-Typ

Sie können den aktuellen Hypervisor-Scheduler-Typ verwendet, anhand der im Protokoll Sysem in der Ereignisanzeige das neueste Hypervisor-Start-Ereignis-ID 2, bestimmen, die den Hypervisor-Scheduler-Typ beim Start der Hypervisor konfiguriert meldet. Hypervisor-Launch-Events können aus der Windows-Ereignisanzeige oder über PowerShell abgerufen werden.

Hypervisor-Start-Ereignis-ID 2 Gibt an, der Hypervisor-Scheduler-Typ, in denen:

    1 = Classic scheduler, SMT disabled

    2 = Classic scheduler

    3 = Core scheduler

    4 = Root scheduler

![Screenshot mit Hypervisor Start-Ereignis-ID 2-details](media/Hyper-V-CoreScheduler-EventID2-Details.png)

![Screenshot der Ereignisanzeige anzeigen Hypervisor-Start-Ereignis-ID 2](media/Hyper-V-CoreScheduler-EventViewer.png)

### <a name="querying-the-hyper-v-hypervisor-scheduler-type-launch-event-using-powershell"></a>Abfragen von Hyper-V-Hypervisor Scheduler Typ einführungsveranstaltung mithilfe von PowerShell

Abfrage für Hypervisor-Ereignis-ID 2 mithilfe von PowerShell, geben Sie die folgenden Befehle aus einer PowerShell-Eingabeaufforderung.

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Hypervisor"; ID=2} -MaxEvents 1
```

![Screenshot mit PowerShell-Abfrage und die Ergebnisse für Hypervisor-Start-Ereignis-ID 2](media/Hyper-V-CoreScheduler-PowerShell.png)
