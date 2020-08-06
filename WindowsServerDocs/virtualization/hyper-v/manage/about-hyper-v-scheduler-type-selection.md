---
title: Informationen zu Hyper-V Hypervisor Scheduler Type Selection
description: Bietet Informationen für Hyper-v-Host Administratoren zur Verwendung von Hyper-v-Scheduler-Modi.
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 5fe163d4-2595-43b0-ba2f-7fad6e4ae069
ms.openlocfilehash: 128f9d734311f8eaf0f06204e114171fa8b0f750
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87768428"
---
# <a name="about-hyper-v-hypervisor-scheduler-type-selection"></a>Informationen zu Hyper-V Hypervisor Scheduler Type Selection

Gilt für:

* Windows Server 2016
* Windows Server, Version 1709
* Windows Server, Version 1803
* Windows Server 2019

In diesem Dokument werden wichtige Änderungen an der standardmäßigen und empfohlenen Verwendung von Hypervisor-Scheduler-Typen für Hyper-V beschrieben. Diese Änderungen wirken sich auf die Systemsicherheit und Virtualisierungsleistung aus. Administratoren von Virtualisierungshosts sollten die in diesem Dokument beschriebenen Änderungen und Implikationen überprüfen und verstehen und die Auswirkungen, den empfohlenen Bereitstellungs Leit Faden und Risikofaktoren sorgfältig auswerten, um die Bereitstellung und Verwaltung von Hyper-V-Hosts im Hinblick auf die schnell veränderliche Sicherheitslandschaft besser zu verstehen.

>[!IMPORTANT]
>Die derzeit in mehreren Prozessorarchitekturen aussehbaren Sicherheitsrisiken für das sidelochannel können von einer bösartigen Gast-VM durch das Planungs Verhalten des herkömmlichen Hypervisor-planertyps "Hypervisor" ausgenutzt werden, wenn die Ausführung auf Hosts mit aktiviertem Multithreading (SMT) aktiviert ist.  Wenn Sie erfolgreich ausgenutzt werden, könnte eine schädliche Arbeitsauslastung Daten außerhalb ihrer Partitions Grenze beobachten. Diese Angriffs Klasse kann verringert werden, indem Sie den Hyper-V-Hypervisor so konfigurieren, dass der Hypervisor Core Scheduler-Typ verwendet und Gast-VMS neu konfiguriert werden. Mit dem Kern Planer schränkt der Hypervisor die VPS eines Gast-VMS auf den gleichen physischen Prozessorkern ein. Dadurch wird die Fähigkeit des virtuellen Computers, auf die Grenzen des physischen Kerns zuzugreifen, auf dem es ausgeführt wird, stark isoliert.  Dies ist eine äußerst effektive Entschärfung gegen diese Seitenkanalangriffe, wodurch verhindert wird, dass der virtuelle Computer Artefakte von anderen Partitionen beobachtet, egal ob es sich um den Stamm oder eine andere Gast Partition handelt.  Daher ändert Microsoft die standardmäßigen und empfohlenen Konfigurationseinstellungen für Virtualisierungshosts und Gast-VMS.

## <a name="background"></a>Hintergrund

Ab Windows Server 2016 unterstützt Hyper-V verschiedene Methoden zum Planen und Verwalten virtueller Prozessoren, die als Hypervisor-planertypen bezeichnet werden.  Eine ausführliche Beschreibung aller Hypervisor-planertypen finden Sie Untergrund Legendes zu [und Verwendung von Hyper-V-Hypervisor-Scheduler-Typen](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types).

>[!NOTE]
>Neue Hypervisor-Scheduler-Typen wurden erstmals mit Windows Server 2016 eingeführt und sind in früheren Versionen nicht verfügbar. Alle Versionen von Hyper-V vor Windows Server 2016 unterstützen nur den klassischen Scheduler. Die Unterstützung für den Kern Planer wurde erst kürzlich veröffentlicht.

## <a name="about-hypervisor-scheduler-types"></a>Informationen zu Hypervisor-Scheduler-Typen

Der Schwerpunkt dieses Artikels liegt auf der Verwendung des neuen Hypervisor-kernplanertyps im Vergleich zum Legacy-Scheduler "klassisch" und der Schnittmenge dieser Scheduler-Typen mit symmetrischem Multithreading oder SMT.  Es ist wichtig, die Unterschiede zwischen den Kern-und klassischen Zeit Planungs Modulen zu verstehen und zu erfahren, wie die einzelnen Orte von Gast-VMS auf den zugrunde liegenden System Prozessoren funktionieren.

### <a name="the-classic-scheduler"></a>Der klassische Scheduler

Der klassische Scheduler bezieht sich auf die Methode "Fair-Share", "Roundrobin" für die Planung von Arbeitsaufgaben an virtuellen Prozessoren (VPS) im gesamten System, einschließlich Stamm-VPS und VPS, die zu Gast-VMS gehören. Der klassische Scheduler ist der standardmäßige Scheduler-Typ, der für alle Versionen von Hyper-V verwendet wird (bis Windows Server 2019, wie in diesem Dokument beschrieben).  Die Leistungsmerkmale des klassischen Zeit Planungs Moduls sind gut verständlich, und das klassische Zeit Planungs Modul wird demonstriert, dass das Abonnement von Workloads unterstützt wird. das heißt, dass das über-Abonnement des VP: LP-Verhältnis des Hosts um einen angemessenen Rand (abhängig von den Typen der virtualisierten Workloads, Gesamtressourcen Auslastung usw.) unterstützt wird.

Bei der Ausführung auf einem Virtualisierungshost mit aktiviertem SMT plant der klassische Scheduler Gast-VPS von einem beliebigen virtuellen Computer in jedem SMT-Thread, der zu einem Kern gehört. Daher können unterschiedliche VMS gleichzeitig auf demselben Kern ausgeführt werden (eine VM, die auf einem Thread eines Kerns ausgeführt wird, während eine andere VM auf dem anderen Thread ausgeführt wird).

### <a name="the-core-scheduler"></a>Der Kern Planer

Der Kern Planer nutzt die Eigenschaften von SMT, um die Isolation von Gast Arbeits Auslastungen zu ermöglichen, was sich auf die Sicherheit und die Systemleistung auswirkt. Der zentrale Scheduler stellt sicher, dass VPS von einem virtuellen Computer auf gleich geordneten SMT-Threads geplant sind. Dies erfolgt symmetrisch, sodass VPS in Gruppen von zwei Gruppen geplant werden, und ein System-CPU-Kern wird nie von virtuellen Computern gemeinsam genutzt, wenn LPs in Gruppen von zwei Gruppen verwendet werden.

Wenn Sie Gast-VPS für zugrunde liegende SMT-Paare planen, bietet der Kern Planer eine starke Sicherheitsgrenze für die workloadisolation und kann auch verwendet werden, um die Leistungs Variabilität für Latenz abhängige Workloads zu verringern.

Beachten Sie Folgendes: Wenn für einen virtuellen Computer, auf dem kein SMT aktiviert ist, der VP geplant ist, nutzt dieser VP den gesamten Kern, wenn er ausgeführt wird, und der gleich geordnete SMT-Thread des Kerns bleibt im Leerlauf.  Dies ist erforderlich, um die richtige workloadisolation bereitzustellen, wirkt sich jedoch auf die Gesamtleistung des Systems aus, insbesondere wenn die System LPs überschrieben werden, d. h., wenn das Gesamtverhältnis von VP: LP 1:1 überschreitet Aus diesem Grund ist das Ausführen von virtuellen Gast Computern, die ohne mehrere Threads pro Kern konfiguriert wurden, eine suboptimale Konfiguration.

### <a name="benefits-of-the-using-the-core-scheduler"></a>Vorteile der mit dem Kern Planer

Der zentrale Scheduler bietet die folgenden Vorteile:

* Eine starke Sicherheitsgrenze für die Isolation von Gast Arbeitslasten (Gast-VPS) ist darauf beschränkt, auf zugrunde liegenden physischen Kern Paaren ausgeführt zu werden

* Reduzierte workloadvarianz: die Variabilität der workloadarbeitsauslastung ist erheblich reduziert und bietet eine höhere Arbeitsauslastung

* Verwendung von SMT in Gast-VMS: das Betriebssystem und die Anwendungen, die auf dem virtuellen Gastcomputer ausgeführt werden, können SMT-Verhaltens-und Programmierschnittstellen (APIs) verwenden, um die Arbeit über SMT-Threads zu steuern und zu verteilen, genauso wie bei der Ausführung nicht virtualisierter Anwendungen.

Der zentrale Scheduler wird derzeit auf Azure-Virtualisierungshosts verwendet, insbesondere, um die starke Sicherheitsgrenze und eine geringe Arbeitsauslastung zu nutzen. Microsoft ist der Meinung, dass der kernplanertyp sein sollte und weiterhin der standardmäßige Hypervisor-Zeit Plantyp für die Mehrzahl der Virtualisierungsszenarien ist.  Um sicherzustellen, dass unsere Kunden standardmäßig sicher sind, nimmt Microsoft diese Änderung jetzt für Windows Server 2019 vor.

### <a name="core-scheduler-performance-impacts-on-guest-workloads"></a>Grundlegende Auswirkungen der Leistung von Scheduler auf Gast Arbeits Auslastungen

Obwohl es erforderlich ist, bestimmte Sicherheitsrisiken effektiv zu mindern, kann der Kern Planer möglicherweise auch die Leistung beeinträchtigen. Kunden haben möglicherweise einen Unterschied in den Leistungsmerkmalen mit ihren VMS und Auswirkungen auf die Gesamtauslastung der Arbeitsauslastung ihrer Virtualisierungshosts. In Fällen, in denen der Kern Planer einen nicht-SMT-VP ausführen muss, wird nur einer der Anweisungs Datenströme im zugrunde liegenden logischen Kern ausgeführt, während der andere im Leerlauf bleiben muss. Dadurch wird die gesamte Host Kapazität für Gast Arbeits Auslastungen eingeschränkt.

Diese Auswirkungen auf die Leistung können minimiert werden, indem die Bereitstellungs Anleitung in diesem Dokument erläutert wird. Host Administratoren müssen Ihre spezifischen Szenarien für die Virtualisierungssoftware sorgfältig berücksichtigen und deren Toleranz für das Sicherheitsrisiko gegen den Bedarf an maximaler Arbeits Auslastungs Dichte, die Konsolidierung von Virtualisierungshosts usw. abwägen.

## <a name="changes-to-the-default-and-recommended-configurations-for-windows-server-2016-and-windows-server-2019"></a>Änderungen an den Standardkonfigurationen und empfohlenen Konfigurationen für Windows Server 2016 und Windows Server 2019

Zum Bereitstellen von Hyper-V-Hosts mit dem maximalen Sicherheitsstatus ist die Verwendung des Typs "Hypervisor Core Scheduler" erforderlich. Um sicherzustellen, dass unsere Kunden standardmäßig sicher sind, ändert Microsoft die folgenden Standardeinstellungen und empfohlenen Einstellungen.

>[!NOTE]
>Obwohl die interne Unterstützung der Scheduler-Typen in der ersten Version von Windows Server 2016, Windows Server 1709 und Windows Server 1803 enthalten war, sind Updates erforderlich, um auf die Konfigurations Steuerung zuzugreifen, mit der der Hypervisor-Planertyp ausgewählt werden kann.  Ausführliche Informationen zu diesen Updates finden Sie unter [verstehen und Verwenden von Hyper-V-Hypervisor-planertypen](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types) .

### <a name="virtualization-host-changes"></a>Änderungen am Virtualisierungshost

* Der Hypervisor verwendet standardmäßig den Kern Planer ab Windows Server 2019.

* Microsoft startet die Konfiguration des Kern Planers auf Windows Server 2016. Der Typ "Hypervisor Core Scheduler" wird in Windows Server 2016 unterstützt, aber der Standardwert ist der klassische Scheduler. Der Kern Planer ist optional und muss vom Hyper-V-Host Administrator explizit aktiviert werden.

### <a name="virtual-machine-configuration-changes"></a>Änderungen an der Konfiguration der virtuellen Maschine

* Unter Windows Server 2019 erben neue virtuelle Computer, die mit der Standard-VM-Version 9,0 erstellt wurden, automatisch die SMT-Eigenschaften (aktiviert oder deaktiviert) des Virtualisierungshosts. Das heißt, wenn SMT auf dem physischen Host aktiviert ist, wird für neu erstellte VMS auch die SMT-Funktion aktiviert, und die SMT-Topologie des Hosts wird standardmäßig geerbt, wobei die VM die gleiche Anzahl von Hardwarethreads pro Kern wie das zugrunde liegende System aufweist. Dies wird in der VM-Konfiguration mit hwthreadzählpercore = 0 übernommen, wobei 0 angibt, dass der virtuelle Computer die SMT-Einstellungen des Hosts erben soll.

* Vorhandene virtuelle Computer mit einer VM-Version von 8,2 oder früher behalten ihre ursprüngliche VM-Prozessor Einstellung für hwthreadzähltpercore bei, und die Standardeinstellung für 8,2-VM-Versions Gäste lautet hwthreadzählpercore = 1. Wenn diese Gäste auf einem Windows Server 2019-Host ausgeführt werden, werden Sie wie folgt behandelt:

    1. Wenn die VM eine VP-Anzahl hat, die kleiner oder gleich der Anzahl der LP-Kerne ist, wird der virtuelle Computer vom Kern Planer als nicht-SMT-VM behandelt. Wenn der Gast-VP in einem einzelnen SMT-Thread ausgeführt wird, wird der gleich geordnete SMT-Thread des Kerns als idled verwendet. Dies ist nicht optimal, was zu einem Gesamtverlust der Leistung führt.

    2. Wenn die VM mehr VPS als LP-Kerne aufweist, wird der virtuelle Computer vom Kern Planer als SMT-VM behandelt. Der virtuelle Computer hat jedoch keine anderen Anzeichen dafür, dass es sich um eine SMT-VM handelt. Beispielsweise weist die Verwendung der CPUID-Anweisung oder der Windows-APIs zum Abfragen der CPU-Topologie durch das Betriebssystem oder die Anwendung nicht darauf hin, dass SMT aktiviert ist.

* Wenn eine vorhandene VM durch den Vorgang "Update-VM" explizit von der VM-Version des virtuellen Computers auf die Version 9,0 aktualisiert wird, behält der virtuelle Computer seinen aktuellen Wert für hwthreadzähltpercore bei.  Für den virtuellen Computer ist die SMT-aktivierte Funktion nicht aktiviert.

* Unter Windows Server 2016 empfiehlt Microsoft, SMT für Gast-VMS zu aktivieren.  Standardmäßig ist für virtuelle Computer, die unter Windows Server 2016 erstellt werden, die SMT-Deaktivierung aktiviert, d. h. hwthreadzählwert ist auf 1 festgelegt, sofern nicht explizit geändert.

>[!NOTE]
>Windows Server 2016 bietet keine Unterstützung für das Festlegen von hwthreadzählpercore auf 0.

#### <a name="managing-virtual-machine-smt-configuration"></a>Verwalten der SMT-Konfiguration für virtuelle Computer

Die SMT-Konfiguration des Gast-virtuellen Computers wird pro VM-Basis festgelegt. Der Host Administrator kann die SMT-Konfiguration eines virtuellen Computers überprüfen und konfigurieren, um eine der folgenden Optionen auszuwählen:

1. Konfigurieren von virtuellen Computern für die ausführen als SMT-fähig, wobei optional die Host-SMT-Topologie automatisch geerbt wird

2. Konfigurieren von virtuellen Computern, die als nicht-SMT ausgeführt werden

Die SMT-Konfiguration für einen virtuellen Computer wird in den Übersichts Bereichen der Hyper-V-Manager-Konsole angezeigt.  Die Konfiguration der SMT-Einstellungen eines virtuellen Computers kann mithilfe der VM-Einstellungen oder PowerShell erfolgen.

#### <a name="configuring-vm-smt-settings-using-powershell"></a>Konfigurieren von VM-SMT-Einstellungen mithilfe von PowerShell

Um die SMT-Einstellungen für einen virtuellen Gastcomputer zu konfigurieren, öffnen Sie ein PowerShell-Fenster mit ausreichenden Berechtigungen, und geben Sie Folgendes ein:

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <0, 1, 2>
```

Hierbei gilt:

- 0 = die SMT-Topologie wird vom Host geerbt (diese Einstellung von hwthreadzähltpercore = 0 wird unter Windows Server 2016 nicht unterstützt)

- 1 = nicht-SMT

- Werte > 1 = die gewünschte Anzahl von SMT-Threads pro Kern. Die Anzahl der physischen SMT-Threads pro Kern darf nicht überschritten werden.

Um die SMT-Einstellungen für einen virtuellen Gastcomputer zu lesen, öffnen Sie ein PowerShell-Fenster mit ausreichenden Berechtigungen, und geben Sie Folgendes ein:

``` powershell
(Get-VMProcessor -VMName <VMName>).HwThreadCountPerCore
```

Beachten Sie, dass Gast-VMS, die mit hwthreadzähltpercore = 0 konfiguriert werden, angeben, dass SMT für den Gast aktiviert ist, und dass die gleiche Anzahl von SMT-Threads für den Gast verfügbar ist wie auf dem zugrunde liegenden Virtualisierungshost, in der Regel 2.

### <a name="guest-vms-may-observe-changes-to-cpu-topology-across-vm-mobility-scenarios"></a>Gast-VMs können Änderungen an der CPU-Topologie über VM-Mobilitäts Szenarien hinweg beobachten

Das Betriebssystem und die Anwendungen auf einem virtuellen Computer können vor und nach dem Lebenszyklus von virtuellen Computern (z. b. Live Migration oder Speicher-und Wiederherstellungs Vorgänge) Änderungen an den Einstellungen für Host und VM Während eines Vorgangs, bei dem der Zustand des virtuellen Computers gespeichert und wieder hergestellt wird, werden sowohl die hwthreadzählpercore-Einstellung der VM als auch der erkannte Wert (d. h. die berechnete Kombination aus der Einstellung des virtuellen Computers und der Konfiguration des Quell Hosts) migriert. Der virtuelle Computer wird mit diesen Einstellungen auf dem Zielhost weiter ausgeführt. Zu dem Zeitpunkt, an dem der virtuelle Computer heruntergefahren und neu gestartet wird, wird möglicherweise der von der VM beobachtete erkannte Wert geändert. Dies sollte nicht ausreichen, da Betriebssystem-und anwendungsebenensoftware im Rahmen ihrer normalen Start-und Initialisierungs Code Flüsse nach CPU-Topologieinformationen suchen soll. Da diese Start Zeit-Initialisierungs Sequenzen bei Live Migrationen oder Speicher-/Wiederherstellungs Vorgängen übersprungen werden, können virtuelle Computer, die diese Zustandsübergänge durchlaufen, den ursprünglich berechneten erkannten Wert beobachten, bis Sie heruntergefahren und neu gestartet werden.

### <a name="alerts-regarding-non-optimal-vm-configurations"></a>Warnungen bezüglich nicht optimaler VM-Konfigurationen

Virtuelle Computer, die mit mehr VPS konfiguriert sind als physische Kerne auf dem Host vorhanden sind, führen zu einer nicht optimalen Konfiguration. Der Hypervisor-Planer behandelt diese VMS so, als ob Sie SMT-fähig sind. Betriebssystem-und Anwendungssoftware auf dem virtuellen Computer wird jedoch eine CPU-Topologie angezeigt, die anzeigt, dass SMT deaktiviert ist. Wenn diese Bedingung erkannt wird, protokolliert der Hyper-V-Arbeitsprozess ein Ereignis auf dem Virtualisierungshost, und der Host Administrator wird darauf gewarnt, dass die VM-Konfiguration nicht optimal ist und dass für den virtuellen Computer SMT empfohlen wird.

#### <a name="how-to-identify-non-optimally-configured-vms"></a>Identifizieren von nicht optimal konfigurierten VMS

Sie können nicht-SMT-VMS ermitteln, indem Sie das System Protokoll in Ereignisanzeige für die Hyper-V-Arbeitsprozess Ereignis-ID 3498 überprüfen, die für einen virtuellen Computer ausgelöst wird, wenn die Anzahl der VPS in der VM größer als die Anzahl der physischen Kerne ist. Arbeitsprozess Ereignisse können von Ereignisanzeige oder über PowerShell abgerufen werden.

#### <a name="querying-the-hyper-v-worker-process-vm-event-using-powershell"></a>Abfragen des Hyper-V-Arbeitsprozess-VM-Ereignisses mithilfe von PowerShell

Geben Sie die folgenden Befehle von einer PowerShell-Eingabeaufforderung ein, um die Ereignis-ID 3498 für den Hyper-V-Arbeitsprozess mit PowerShell abzufragen.

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Worker"; ID=3498}
```

### <a name="impacts-of-guest-smt-configuaration-on-the-use-of-hypervisor-enlightenments-for-guest-operating-systems"></a>Auswirkungen der Gast-SMT-Konfiguration auf die Verwendung von Hypervisor-Erleuchtungen für Gast Betriebssysteme

Der Microsoft-Hypervisor bietet mehrere-oder-Hinweise, die vom Betriebssystem, das auf einer Gast-VM ausgeführt wird, möglicherweise abgefragt und verwendet werden, um Optimierungen zu initiieren, z. b. solche, die die Leistung verbessern oder die Behandlung verschiedener Bedingungen bei der Ausführung von virtualisierten Eine vor kurzem eingeführte Erleuchtung bezieht sich auf die Behandlung von virtuellen Prozessorzeit Plänen und die Verwendung von Betriebs systementschärfungen für Seitenkanalangriffe, die SMT ausnutzen.

>[!NOTE]
>Microsoft empfiehlt, dass Host Administratoren SMT für Gast-VMS aktivieren, um die workloadleistung zu optimieren.

Die Details dieser Gast Aufklärung werden unten bereitgestellt, aber der Hauptgrund für die Virtualisierungshost-Administratoren besteht darin, dass für virtuelle Computer hwthreadzähltpercore entsprechend der physischen SMT-Konfiguration des Hosts konfiguriert werden muss. Dadurch kann der Hypervisor melden, dass keine nicht architektonische Kern Freigabe vorhanden ist. Daher können alle Gast Betriebssysteme, die Optimierungen unterstützen, die die Aufklärung erfordern, aktiviert werden. Erstellen Sie unter Windows Server 2019 neue VMs, und belassen Sie den Standardwert hwthreadzähltpercore (0). Ältere VMS, die von Windows Server 2016-Hosts migriert wurden, können auf die Windows Server 2019-Konfigurations Version aktualisiert werden. Danach empfiehlt Microsoft, hwthreadzähltpercore = 0 festzulegen.  Unter Windows Server 2016 empfiehlt Microsoft, hwthreadzähltpercore entsprechend der Host Konfiguration (in der Regel 2) festzulegen.

### <a name="nononarchitecturalcoresharing-enlightenment-details"></a>Details zu "nononarchitekturalcoresharung"

Ab Windows Server 2016 definiert der Hypervisor eine neue Erleuchtung, um die Verarbeitung der VP-Planung und-Platzierung für das Gast Betriebssystem zu beschreiben. Diese Aufklärung wird in der [Funktionsspezifikation der obersten Ebene von Hypervisor v 5.0 c](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/tlfs)definiert.

Synthetisches CPUID-Blatt "Hypervisor" CPUID. 0x40000004. EAX: 18 [nononarchitekturalcoreshareing = 1] gibt an, dass ein virtueller Prozessor nie einen physischen Kern mit einem anderen virtuellen Prozessor gemeinsam nutzt, mit Ausnahme von virtuellen Prozessoren, die als gleich geordnete SMT-Threads gemeldet werden. Beispielsweise wird ein Gast-VP nie in einem SMT-Thread parallel zu einem Stamm-VP ausgeführt, der gleichzeitig auf einem gleich geordneten SMT-Thread desselben Prozessorkerns ausgeführt wird. Diese Bedingung ist nur bei der virtualisierten Ausführung möglich und stellt ein nicht architektonisches SMT-Verhalten dar, das auch schwerwiegende Auswirkungen auf die Sicherheit hat. Das Gast Betriebssystem kann nononarchitekturalcoreshareing = 1 verwenden, um zu verhindern, dass Optimierungen sicher aktiviert werden können. Dies kann dazu beitragen, den Leistungs Aufwand bei der Festlegung von stibp zu vermeiden.

In bestimmten Konfigurationen weist der Hypervisor nicht darauf hin, dass nononarchitekturalcoreshareing = 1 ist. Wenn ein Host beispielsweise SMT aktiviert hat und für die Verwendung des klassischen Hypervisor-Schedulers konfiguriert ist, wird nononarchitekturalcoreshareing auf 0 festgelegt. Dadurch wird möglicherweise verhindert, dass aktivierte Gäste bestimmte Optimierungen aktivieren. Daher empfiehlt Microsoft, dass Host Administratoren, die SMT verwenden, den Hypervisor-Kern Planer verwenden und sicherstellen, dass virtuelle Computer so konfiguriert sind, dass die SMT-Konfiguration vom Host geerbt wird, um eine optimale workloadleistung sicherzustellen.

## <a name="summary"></a>Zusammenfassung

Die Sicherheits Bedrohungslandschaft wird weiterentwickelt. Um sicherzustellen, dass unsere Kunden standardmäßig sicher sind, ändert Microsoft die Standardkonfiguration für den Hypervisor und die virtuellen Computer ab Windows Server 2019 Hyper-v und bietet aktualisierte Anleitungen und Empfehlungen für Kunden, die Windows Server 2016 Hyper-v ausführen. Administratoren von Virtualisierungshosts sollten:

* Lesen und verstehen Sie die Anweisungen in diesem Dokument.

* Evaluieren und Anpassen der Virtualisierungsbereitstellungen, um sicherzustellen, dass Sie die Anforderungen an Sicherheit, Leistung, Virtualisierungsdichte und Arbeits Auslastungen für die Reaktionsfähigkeit ihrer individuellen Anforderungen erfüllen

* Sie sollten vorhandene Windows Server 2016 Hyper-V-Hosts neu konfigurieren, um die starken Sicherheitsvorteile des Hypervisor-Kern Planers zu nutzen.

* Aktualisieren vorhandener nicht-SMT-VMS, um die Leistung zu verringern, die durch die Planung von Einschränkungen durch die VP-Isolation auferlegt werden
