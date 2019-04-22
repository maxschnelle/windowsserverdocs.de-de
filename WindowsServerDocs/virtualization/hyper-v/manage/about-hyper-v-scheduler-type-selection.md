---
title: Zur Auswahl des Hyper-V-Hypervisor scheduler
description: Bietet Informationen zu Hyper-V-Host-Administratoren bei der Verwendung von Hyper-V-Scheduler-Modi
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 5fe163d4-2595-43b0-ba2f-7fad6e4ae069
ms.openlocfilehash: c5360d8e2fdc23f8b05c6be0f665407eebedeba2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823881"
---
# <a name="about-hyper-v-hypervisor-scheduler-type-selection"></a>Zur Auswahl des Hyper-V-Hypervisor scheduler

Gilt für:

* Windows Server 2016
* Windows Server, Version 1709
* Windows Server, Version 1803
* Windows Server 2019

Dieses Dokument beschreibt wichtige Änderungen an Hyper-V-Standard und empfohlene Verwendung von Hypervisor Scheduler-Typen. Diese Änderungen beeinträchtigen, sowohl die Sicherheits- und Virtualisierung der Systemleistung. Virtualization Host-Administratoren sollte überprüfen und verstehen, die Änderungen und die Auswirkungen, die in diesem Dokument beschriebenen und sorgfältig die Auswirkungen, die vorgeschlagenen Deployment-Anleitungen und die Risikofaktoren, die Sie am besten verstehen, wie zum Bereitstellen und Verwalten von Beteiligten Hyper-V-Hosts bei schnell Sicherheit im Wandel.

>[!IMPORTANT]
>Bekannten seitenkanalangriffe Sicherheit, die Sicherheitsrisiken Ausblick Architekturen mit mehreren Prozessoren, die von einer böswilligen Gast-VM über das Planen Verhalten der ältere klassische Scheduler hypervisortyp bei Ausführung auf Hosts mit gleichzeitige ausgenutzt werden könnten Multithreading (SMT) aktiviert.  Bei einem erfolgreichen Angriff könnte eine böswillige arbeitsauslastung Daten außerhalb der Partition beobachten. Diese Art von Angriffen kann verringert werden, durch Konfigurieren des Hyper-V-Hypervisors, um den Hypervisor Core Scheduler-Typ und die Neukonfiguration-Gast-VMs zu nutzen. Mit dem Scheduler Core beschränkt der Hypervisor eine Gast-VM-VPs auf der gleichen physischen Prozessor, isolieren die Möglichkeit des virtuellen Computers, auf Daten zugreifen, um die Grenzen der physischen Kerne auf dem er ausgeführt wird daher dringend ausgeführt.  Dies ist eine äußerst wirksame Lösung vor diesen Angriffen seitenkanalangriffe der verhindert, dass den virtuelle Computer prüfen, ob alle Elemente aus anderen Partitionen, die Stamm- oder einer anderen Gast-Partition.  Aus diesem Grund wird Microsoft ist die Standardeinstellung ändern und Konfigurationseinstellungen für Virtualisierungshosts und Gast-VMs empfohlen.

## <a name="background"></a>Hintergrund

Ab Windows Server 2016 unterstützt Hyper-V mehrere Methoden zum Planen und Verwalten von virtuellen Prozessoren, die als Hypervisor Scheduler Typen bezeichnet.  Eine ausführliche Beschreibung aller Hypervisor-Scheduler-Typen finden Sie im [verstehen und Verwenden von Hyper-V-Hypervisor Scheduler Typen](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types).

>[!NOTE]
>Neue Hypervisor-Scheduler-Typen mit Windows Server 2016 eingeführt wurden, und sind in früheren Versionen nicht verfügbar. Alle Versionen von Hyper-V vor Windows Server 2016 unterstützt nur das klassische Zeitplanungsmodul. Unterstützung für das Zeitplanungsmodul Core wurde erst vor kurzem veröffentlicht.

## <a name="about-hypervisor-scheduler-types"></a>Informationen zu den Hypervisor-Scheduler-Typen

Dieser Artikel konzentriert sich auf die Verwendung des neuen Hypervisor Core Scheduler Typs im Vergleich zu den älteren "klassische" Scheduler, und wie diese Scheduler-Typen mit der Verwendung von Multithreading Symmetric oder SMT überschneiden.  Es ist wichtig zu verstehen, die Unterschiede zwischen den Zeitplanungsmodulen Core und die klassische und wie jede Arbeit von Gast-VMs auf den zugrunde liegenden Systemprozessoren platziert.

### <a name="the-classic-scheduler"></a>Der klassische scheduler

Der klassische Scheduler bezieht sich auf die Methode "Roundrobin" Fair-Freigabe, der Planung der Arbeit an virtuellen Prozessoren (VPs) im System – einschließlich Stamm VPs sowie VPs zu Gast-VMs gehören. Der klassische Planer wurde der Scheduler-Standardtyp, die in allen Versionen von Hyper-V (bis zu Windows Server 2019, wie in diesem Dokument beschrieben) verwendet.  Die Leistungsmerkmale des klassischen Zeitplanungsmoduls gut verstanden, und der klassischen Scheduler wird veranschaulicht, um Klassenentwürfen Überzeichnung Workloads – d. h. die Überzeichnung des Hosts VP:LP Verhältnisses durch eine angemessene Rand zu unterstützen (je nachdem auf die Arten von Workloads, die die diesbezüglichen, allgemeine Ressourcenverwendung usw.).

Wenn auf einem Virtualisierungshost mit SMT aktiviert ausführen möchten, wird der klassische Scheduler Gast VPs von jedem virtuellen Computer in jedem SMT-Thread, die unabhängig voneinander auf einen Kern gehören geplant. Aus diesem Grund können verschiedene virtuelle Computer im gleichen Kern ausgeführt werden, zur gleichen Zeit (mehrere VMs in einem Thread eines Kerns, während eine andere virtuelle Computer auf dem anderen Thread ausgeführt wird).

### <a name="the-core-scheduler"></a>Der Kern-Planer

Der Planer Core nutzt die Eigenschaften des SMT zur Isolation von Gast-Workloads, die Sicherheit "und" Systemleistung wirkt sich auf. Der Planer Core stellt sicher, dass es sich bei VPs von einem virtuellen Computer in gleichgeordnetes Element SMT Threads geplant sind. Dies erfolgt symmetrisch, sodass Wenn LPs sind Gruppen von zwei VPs in Gruppen von zwei geplant sind, und ein System-CPU-Kern zwischen virtuellen Computern niemals.

Durch die Planung Gast VPs auf zugrunde liegende SMT-Paaren, die Core-Scheduler bietet eine starke sicherheitsbegrenzung für Workloads zu isolieren und kann auch verwendet werden, um leistungsschwankungen sensiblen Workloads für die Latenz zu verringern.

Beachten Sie, dass der VP ohne SMT aktiviert, für einen virtuellen Computer geplant ist, dass VP den gesamte Kern genutzt werden, wird wenn er ausgeführt wird, und der Kern des nebengeordneten SMT-Thread im Leerlauf bleiben.  Dies ist notwendig, den richtigen Workloads zu isolieren, jedoch wirkt sich auf allgemeine Systemleistung, insbesondere dann, wie Sie die System-LPs überzeichnet – d. h., wenn insgesamt VP:LP Verhältnis 1:1 überschreitet. Daher ist die Gast-VMs konfiguriert, ohne mehrere Threads pro Kern ausgeführt, ein nicht optimaler Konfiguration.

### <a name="benefits-of-the-using-the-core-scheduler"></a>Vorteile der Verwendung des Core-Planers

Der Planer Core bietet folgende Vorteile:

* Eine starke sicherheitsbegrenzung für Gast workloadisolation - Gast VPs sind eingeschränkt, auf die zugrunde liegenden physischen Kern-Paare, verringert die Anfälligkeit für die Seiten-Kanal-Spoofingangriffen ausgeführt.

* Arbeitsauslastung Variabilität - Gast-Workload Durchsatz Variabilität wird deutlich verkürzt, größere Workloads Konsistenz bietet.

* Verwenden von SMT in Gast-VMs – das Betriebssystem und Anwendungen, die auf dem virtuellen Gastcomputer kann genutzt werden SMT-Verhalten und Programmierschnittstellen (APIs), um zu steuern und Verteilung von Arbeitsaufgaben über SMT-Threads, genau wie sie beim Ausführen nicht virtualisiert.

Das Core-Zeitplanungsmodul wird derzeit auf Azure Virtualisierungshosts, speziell für die Grenze für hohe Sicherheit und eine geringe arbeitsauslastung Variabilty nutzen verwendet. Microsoft ist davon überzeugt, dass die Core-Scheduler-Typ muss und der Standard-Hypervisor weiterhin ist-Typ für die meisten Szenarios der Benutzerstatusvirtualisierung planen.  Aus diesem Grund ist um sicherzustellen, dass unsere Kunden standardmäßig sicher sind, Microsoft diese Änderung für Windows Server-2019 jetzt erfolgt.

### <a name="core-scheduler-performance-impacts-on-guest-workloads"></a>Core Scheduler leistungsbeeinträchtigungen für Gast-workloads

Zwar erforderlich, um effektiv bestimmte Klassen von Sicherheitsrisiken zu minimieren, kann der Planer Core auch möglicherweise die Leistung beeinträchtigen. Kunden möglicherweise einen Unterschied in der Leistungsmerkmale mit mehreren ihre VMs und die Auswirkungen auf die Workload-Gesamtkapazität, der die Virtualisierungshosts angezeigt. In Fällen, in der Core-Planer ein nicht - SMT VP ausführen müssen, führt nur eine Anweisung Streams in der zugrunde liegenden logischen Kern, während die andere im Leerlauf bleiben muss. Dadurch wird die gesamte Host-Kapazität für gastarbeitsauslastungen beschränkt.

Diese Auswirkungen auf die Leistung können minimiert werden, anhand der Anleitungen zur Bereitstellung in diesem Dokument. Hostadministratoren müssen sorgfältig sollten Sie ihre bestimmten Virtualisierung Bereitstellungsszenarien und ausgleichen ihrer Toleranz für die Sicherheitsrisiken für die Notwendigkeit der Dichte der maximalen arbeitsauslastung, zu der Konsolidierung der Virtualisierungshosts usw.

## <a name="changes-to-the-default-and-recommended-configurations-for-windows-server-2016-and-windows-server-2019"></a>Änderungen an den standardmäßigen und empfohlenen Konfigurationen für Windows Server 2016 und Windows Server-2019

Bereitstellen von Hyper-V-Hosts mit der maximalen Sicherheitsstatus erfordert die Verwendung von der Hypervisor-Core-Scheduler-Typ. Microsoft, um sicherzustellen, dass unsere Kunden standardmäßig sicher sind, ändert sich die folgende Standardgruppen und empfohlene Einstellungen.

>[!NOTE]
>Updates sind erforderlich, um das Konfigurationssteuerelement zugreifen, dem Sie auswählen können, während des Hypervisors interner Support für die Zeitplanungsmodul-Typen in der ersten Version von Windows Server 2016, Windows Server 1709 und Windows Server-Version 1803 enthalten war, die Hypervisor-Scheduler-Typ.  Näheres [verstehen und Verwenden von Hyper-V-Hypervisor Scheduler Typen](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types) ausführliche Informationen über diese Updates.

### <a name="virtualization-host-changes"></a>Virtualization Host ändert

* Der Hypervisor verwendet den Planer Core standardmäßig ab, mit Windows Server-2019.

* Microsoft-Reccommends den Planer Core unter Windows Server 2016 konfigurieren. Der Hypervisor-Core-Scheduler-Typ wird in Windows Server 2016 unterstützt, jedoch die Standardeinstellung der klassischen Scheduler ist. Das Core-Zeitplanungsmodul ist optional und muss explizit durch den Hyper-V-Host-Administrator aktiviert werden.

### <a name="virtual-machine-configuration-changes"></a>VM-konfigurationsänderungen

* Windows Server-2019, erben neuer virtueller Maschinen, die mit der Standard-VM-Version 9.0 erstellt automatisch die SMT-Eigenschaften (aktiviert oder deaktiviert) des Virtualisierungshosts. Also wenn SMT für aktiviert ist der physischen Hosts, die neu erstellte virtuelle Computer außerdem SMT aktiviert haben und übernimmt die SMT-Topologie des Hosts wird standardmäßig mit dem virtuellen Computer müssen die gleiche Anzahl von Hardwarethreads pro Kern des zugrunde liegenden Systems. Dies wird in der VM Konfiguration mit HwThreadCountPerCore widergespiegelt = 0 (null), in denen 0 gibt an, der virtuellen Computer sollte der Host des SMT-Einstellungen erben.

* Vorhandene virtuelle Computer mit einem VM-Version 8.2 oder früher wird beibehalten, ihre ursprüngliche VM-Prozessor-Einstellung für HwThreadCountPerCore und der Standardwert für 8.2 VM-Version-Gäste ist HwThreadCountPerCore = 1. Wenn diese Gäste auf einem Windows Server-2019-Host ausführen, werden sie wie folgt behandelt:

    1. Verfügt der virtuelle Computer VP Anzahl, die kleiner oder gleich der Anzahl von Kernen für LP ist, wird der virtuelle Computer als ein nicht - SMT VM vom Scheduler Core behandelt. Wenn der Gast VP in einem einzelnen SMT-Thread ausgeführt wird, wird der Kern des nebengeordneten SMT-Thread im Leerlauf. Dies ist nicht optimal, und allgemeine Leistungsverlust führen.

    2. Wenn der virtuelle Computer weitere VPs als LP Prozessoren verfügt, werden der virtuellen Computer als SMT-VM vom Scheduler Core behandelt. Jedoch wird der virtuelle Computer nicht andere Anzeichen Beachten Sie, dass es einer SMT-VM. Beispielsweise wird die Verwendung des CPUID-Anweisung oder der Windows-APIs zum Abfragen von CPU-Topologie mit vom Betriebssystem oder Anwendungen nicht, dass SMT aktiviert ist.

* Bei ein vorhandener virtuellen Computer auf Version 9.0, durch den Update-VM-Vorgang explizit aus früheren VM-Version aktualisiert wird, wird der virtuelle Computer den aktuellen Wert für HwThreadCountPerCore beizubehalten.  Der virtuelle Computer müssen sich nicht auf SMT-Force-fähigen aus.

* Unter Windows Server 2016 empfiehlt Microsoft das Aktivieren von SMT für Gast-VMs.  Wird standardmäßig unter Windows Server 2016 erstellte SMT würde deaktiviert haben virtuelle Computer, ist, die, dass HwThreadCountPerCore auf 1 festgelegt ist, es sei denn, Sie explizit geändert werden.

>[!NOTE]
>Windows Server 2016 unterstützt keine HwThreadCountPerCore auf 0 festlegen.

#### <a name="managing-virtual-machine-smt-configuration"></a>Verwalten von SMT-Konfiguration des virtuellen Computers

Der Gast-VM-SMT-Konfiguration wird auf einer Basis pro virtuellem Computer festgelegt. Der hostadministrator kann untersuchen und Konfigurieren eines virtuellen Computers SMT-Konfiguration die folgenden Optionen aus:

    1. Konfigurieren von virtuellen Computern als SMT-fähig ist, erben den SMT-Topologie des Hosts optional automatisch ausführen

    2. Konfigurieren von virtuellen Computern zur Ausführung als nicht-SMT

Die Configuaration SMT für einen virtuellen Computer wird in der Zusammenfassung Bereiche in der Hyper-V-Manager-Konsole angezeigt.  Konfigurieren von SMT-Einstellungen eines virtuellen Computers kann mithilfe der VM-Einstellungen oder PowerShell erfolgen.

#### <a name="configuring-vm-smt-settings-using-powershell"></a>Konfigurieren der VM SMT-Einstellungen, die mithilfe von PowerShell

Um die SMT-Einstellungen für einen Gast-VM zu konfigurieren, öffnen Sie ein PowerShell-Fenster mit ausreichenden Berechtigungen, und geben ein:

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <0, 1, 2>
```

Dabei gilt:

    0 = Inherit SMT topology from the host (this setting of HwThreadCountPerCore=0 is not supported on Windows Server 2016)

    1 = Non-SMT

    Values > 1 = the desired number of SMT threads per core. May not exceed the number of physical SMT threads per core.

Um die SMT-Einstellungen für einen virtuellen Gastcomputer zu lesen, öffnen Sie ein PowerShell-Fenster mit ausreichenden Berechtigungen, und geben ein:

``` powershell
(Get-VMProcessor -VMName <VMName>).HwThreadCountPerCore
```

Beachten Sie diese Gast-VMs mit HwThreadCountPerCore = 0 gibt an, dass SMT für den Gast aktiviert, und die gleiche Anzahl von Threads von SMT für den Gast verfügbar macht, wie sie auf dem zugrunde liegenden Virtualisierungshost, die in der Regel 2 sind.

### <a name="guest-vms-may-observe-changes-to-cpu-topology-across-vm-mobility-scenarios"></a>Gast-VMs können Änderungen an der CPU-Topologie in Szenarien mit Mobilität virtueller Computer informieren.

Das Betriebssystem und Anwendungen auf einem virtuellen Computer möglicherweise Änderungen an den Host- und VM-Einstellungen vor und nach VM Lebenszyklusereignisse wie z. B.-Migration Live oder speichern und Wiederherstellungsvorgänge. Während eines Vorgangs auf die virtuellen, das Computer "sessionState" / wiederhergestellt wird, werden sowohl die realisierter Wert (d. h. die berechnete Kombination der VM Einstellung und Konfiguration des Hosts Quelle) als auch des virtuellen Computers HwThreadCountPerCore Einstellung migriert. Der virtuelle Computer weiterhin ausgeführt, die mit diesen Einstellungen auf dem Zielhost. An dem Punkt wird des virtuelle Computers heruntergefahren und neu gestartet, es ist möglich, die beobachtet die realisierte Wert durch den virtuellen Computer ändert. Dies dürfte keine Auswirkungen, die als Betriebssystem und die Anwendung sollte die Schichten einer Software für die CPU-Topologie-Informationen als Teil ihrer normalen Datenflüsse für Start- und Initialisierung Code aussehen. Allerdings, da diese Boot Initialisierung, die Sequenzen während der live Migration "oder" Speichern/Wiederherstellen-Vorgänge, virtuelle Computer übersprungen werden, die diese Zustandsänderungen werden beobachten könnte den ursprünglich berechneten Wert realisiert, bis sie heruntergefahren und neu gestartet.  

### <a name="alerts-regarding-non-optimal-vm-configurations"></a>Warnungen zu nicht optimalen VM-Konfigurationen

Virtuelle Computer mit mehr VPs als physischen Kerne auf dem Host-Ergebnis in einer nicht optimalen Konfiguration sind konfiguriert. Der Hypervisor-Planer behandelt diese virtuellen Computer aus, als ob sie den SMT-fähig sind. Allerdings Betriebssystem und die Anwendungssoftware, die auf dem virtuellen Computer eine CPU-Topologie mit SMT ist deaktiviert, angezeigt. Wenn diese Bedingung erkannt wird, der Hyper-V-Arbeitsprozess wird ein Ereignis protokollieren, auf dem Virtualisierungshost Warnung von des Host-Administrators, dass die VM Konfiguration nicht optimal ist, und empfehlen SMT für den virtuellen Computer aktiviert.

#### <a name="how-to-identify-non-optimally-configured-vms"></a>Identifizieren von nicht optimal konfiguriert virtuelle Computer

Sie können nicht - SMT-VMs durch untersuchen das Systemprotokoll in der Ereignisanzeige für Hyper-V-Arbeitsprozess-Ereignis-ID-3498 identifizieren, die für einen virtuellen Computer ausgelöst wird, wenn die Anzahl der VPs auf dem virtuellen Computer größer als die Anzahl von physischen Kernen ist. Verarbeiten von Ereignissen Worker können aus der Ereignisanzeige oder über PowerShell abgerufen werden.

#### <a name="querying-the-hyper-v-worker-process-vm-event-using-powershell"></a>Das Hyper-V-Worker-VM Prozessereignis mithilfe von PowerShell Abfragen

Abfrage für Hyper-V-Worker-Prozessereignis-ID 3498 mithilfe von PowerShell, geben Sie die folgenden Befehle aus einer PowerShell-Eingabeaufforderung.

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Worker"; ID=3498}
```

### <a name="impacts-of-guest-smt-configuaration-on-the-use-of-hypervisor-enlightenments-for-guest-operating-systems"></a>Auswirkungen der Gast SMT Configuaration für die Verwendung von Hypervisor Enlightenments für Gastbetriebssysteme

Der Hypervisor Microsoft bietet mehrere Enlightenments oder -Hinweise, die das Betriebssystem auf einem virtuellen Gastcomputer Abfragen und verwenden Sie zum Auslösen von Optimierungen, wie die, die Leistung zu profitieren kann, oder andernfalls Behandlung von verschiedenen Bedingungen zu verbessern, bei der Ausführung virtualisiert. Eine kürzlich eingeführten Erleuchtung bezieht sich auf den Umgang mit virtuellen Prozessor planen und die Verwendung von OS-entschärfungen für seitenkanalangriffe, die SMT ausnutzen.

>[!NOTE]
>Microsoft empfiehlt, aktivieren Sie hostadministratoren SMT für Gast-VMs, um die arbeitsauslastung zu optimieren.

Die Details der dieses Gastbetriebssystem Erleuchtung stehen unten die wichtigste Voraussetzung besteht für die Virtualisierung hostadministratoren ist jedoch, dass virtuelle Computer HwThreadCountPerCore so konfiguriert, dass die physische SMT-Konfiguration des Hosts übereinstimmen müssen. Dadurch wird den Hypervisor zu melden, dass keine nicht-Architektur Core freigeben. Aus diesem Grund können alle Guest OS unterstützenden Optimierungen, die die Erleuchtung erfordern aktiviert werden. Windows Server-2019 neue VMs erstellt, und übernehmen Sie den Standardwert des HwThreadCountPerCore (0). Ältere virtuelle Computer migriert werden, von Windows Server 2016 Hosts können auf die Version der Windows Server-2019 Konfiguration aktualisiert werden. Nach dem dies der Fall, Microsoft empfiehlt, die Einstellung HwThreadCountPerCore = 0 sein.  Unter Windows Server 2016 empfiehlt Microsoft die Einstellung HwThreadCountPerCore entsprechend die Hostkonfiguration (in der Regel 2).

### <a name="nononarchitecturalcoresharing-enlightenment-details"></a>NoNonArchitecturalCoreSharing Erleuchtung details

Ab Windows Server 2016, definiert der Hypervisor eine neue Erleuchtung, um die Behandlung VP planen und die Platzierung auf das Gastbetriebssystem zu beschreiben. Diese Erleuchtung wird definiert, der [Hypervisor Top Level Functional Specification v5.0c](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/tlfs).

Hypervisor synthetische CPUID Blattebene CPUID.0x40000004.EAX:18[NoNonArchitecturalCoreSharing = 1] Gibt an, dass ein virtueller Prozessor nie einen physischen Kern mit einem anderen virtuellen Prozessor, mit Ausnahme der virtuellen Prozessoren teilen, die als gleichgeordnetes Element SMT gemeldet werden Threads. Ein Gast VP gleichzeitig ausgeführt werden, auf ein gleichgeordnetes Element SMT-Thread auf die gleiche Prozessorkern beispielsweise nie in einem SMT-Thread zusammen mit einem Stamm VP ausgeführt. Diese Bedingung ist nur möglich, wenn virtualisierte ausgeführt, und stellt daher ein nicht-Architektur SMT-Verhalten, das auch schwerwiegende sicherheitsauswirkungen hat. Der Gast-BS können NoNonArchitecturalCoreSharing = 1 als Hinweis auf, es ist sicher zum Aktivieren von Optimierungen, die es den Leistungsaufwand von festlegen STIBP vermeiden helfen können.

In bestimmten Konfigurationen, der Hypervisor nicht angegeben wird, NoNonArchitecturalCoreSharing = 1. Als Beispiel wenn ein Host SMT aktiviert wurde und für die Verwendung den klassischen Hypervisor-Scheduler, konfiguriert wird NoNonArchitecturalCoreSharing 0 sein. Dies kann verhindern, dass RMS-aktivierte Gäste bestimmte Optimierungen zu aktivieren. Microsoft empfiehlt daher, dass SMT Verwendung hostadministratoren abhängig von der Hypervisor-Core-Planer und stellen Sie sicher, dass virtuelle Computer konfiguriert sind, um ihre SMT-Konfiguration vom Host zur Gewährleistung einer optimalen workloadleistung erben.

## <a name="summary"></a>Zusammenfassung

Die Bedrohungslage für die Sicherheit ständig weiterentwickelt. Um sicherzustellen, dass unsere Kunden sind standardmäßig sicher Microsoft ändert die Standardkonfiguration für den Hypervisor und virtuelle Computer in Windows Server 2019 Hyper-V ab und aktualisiert bereitstellen, Anleitungen und Empfehlungen für Kunden, die Windows ausführen Server 2016 Hyper-V. Virtualization Host-Administratoren sollten Folgendes beachten:

* Lesen Sie und verstehen Sie die Anleitung in diesem Dokument

* Sorgfältig bewerten Sie und passen Sie ihre Bereitstellungen Virtualisierung, um sicherzustellen, dass sie die Sicherheit, Leistung, virtualisierungsdichte und Workload-Reaktionsfähigkeit-Ziele für ihre individuellen Anforderungen erfüllen.

* Sollten Sie erneutes Konfigurieren von vorhandenen Windows Server 2016 Hyper-V-Hosts, hohe Sicherheitsvorteile von der Hypervisor-Core-Scheduler zu nutzen

* Aktualisieren von vorhandenen nicht - SMT-VMs zur Reduzierung der Auswirkungen auf die Leistung und Planung von Einschränkungen durch VP-Isolation, die Sicherheitsrisiken für die Hardware-Adressen
