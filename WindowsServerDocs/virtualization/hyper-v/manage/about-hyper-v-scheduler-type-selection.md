---
title: Informationen zu Hyper-V-Hypervisor Scheduler Auswahl
description: Enthält Informationen für Hyper-V-Host Administratoren auf die Verwendung von Hyper-V-Scheduler Modi
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 5fe163d4-2595-43b0-ba2f-7fad6e4ae069
ms.openlocfilehash: c5360d8e2fdc23f8b05c6be0f665407eebedeba2
ms.sourcegitcommit: 546229d6b5fa7e16f725c6c35f4dcc272711b811
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2018
ms.locfileid: "4905127"
---
# Informationen zu Hyper-V-Hypervisor Scheduler Auswahl

Gilt für:

* Windows Server 2016
* Windows Server, Version 1709
* Windows Server, Version 1803
* WindowsServer 2019

Dieses Dokument beschreibt wichtige Änderungen bei der Hyper-V-Standard und empfohlene Verwendung der Hypervisor Scheduler Typen. Diese Änderungen wirken sich beide Systemleistung Sicherheits- und Virtualisierung. Virtualisierung Host Administratoren sollten überprüfen und Änderungen und in diesem Dokument beschriebenen Implikationen verstehen und sorgfältig Evaluieren der Auswirkungen spüren, vorgeschlagene Bereitstellung und Faktoren am besten kennen bereitstellen und Verwalten von Risiken Hyper-V-Hosts angesichts der sich schnell ändernden Sicherheitslandschaft.

>[!IMPORTANT]
>Derzeit bekannte Side-Channel, die mehrere Prozessorarchitekturen Ausblick Sicherheitslücken durch schädliche Gast VM über das scheduling Verhalten des älteren Hypervisor klassische Scheduler Typs bei der Ausführung unter Hosts mit simultane ausgenutzt werden kann Multithreading (SMT) aktiviert.  Bei einem erfolgreichen Angriff könnte eine böswillige Workload Daten außerhalb der Partition Grenze beobachten. Diese Klasse von Angriffen kann durch das Konfigurieren des Hyper-V-Hypervisors, um den Hypervisor Core Scheduler Typ und die Neukonfiguration Gast-VMs nutzen verringert werden. Mit der Planer Core schränkt der Hypervisor ein Gast-VM VPs Ausführung auf dem gleichen physischen Prozessor-Kern, daher stark Isolieren des virtuellen Computers Möglichkeit zum Zugriff auf Daten an die Grenzen des dem physischen Kern auf dem sie ausgeführt wird.  Hierbei handelt es sich um eine sehr effektive Schutzmaßnahme gegen diese Side-Channel-Angriffe, die verhindert, dass den virtuelle Computer beobachten alle Artefakte aus anderen Partitionen gibt an, ob das Stammverzeichnis oder eine andere Gast-Partition.  Aus diesem Grund wird Microsoft ist die Standardeinstellung ändern und Konfigurationseinstellungen für Virtualisierungshosts und Gast-VMs empfohlen.

## Hintergrund

Ab Windows Server 2016 unterstützt Hyper-V mehrere Methoden planen und Verwalten von virtuellen Prozessoren, als Hypervisor Scheduler Typen bezeichnet.  Eine ausführliche Beschreibung aller Hypervisor Scheduler Typen kann in [verstehen und Verwenden von Hyper-V-Hypervisor Scheduler Typen](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types)gefunden werden.

>[!NOTE]
>Neue Hypervisor Scheduler Typen erstmals mit Windows Server 2016 eingeführt wurden, und sind in früheren Versionen nicht verfügbar. Alle Versionen von Hyper-V vor Windows Server 2016 unterstützen nur die klassischen Scheduler. Unterstützung für den Core-Planer wurde nur kürzlich veröffentlicht.

## Zu den Hypervisor Scheduler Typen

Dieser Artikel befasst sich speziell auf die Verwendung des neuen Hypervisor Core Scheduler Typs im Vergleich zu der legacy "klassische" Planer und diese Scheduler-Typen wie bei der Verwendung der Multi-Threading symmetrisch oder SMT überschneiden.  Es ist wichtig zu verstehen, die Unterschiede zwischen der Planer Core und klassische und wie jede Arbeit von Gast-VMs auf die zugrunde liegende Systemprozessoren platziert.

### Die klassische scheduler

Der klassische Planer bezieht sich auf die gleichberechtigten, Round-Robin-Methode des Arbeit für virtuelle Prozessoren (VPs) über das System – einschließlich Stamm VPs sowie den Gast-VMs gehören VPs planen. Die klassische Scheduler wurde der Scheduler-Standardtyp, die in allen Versionen von Hyper-V (bis zu Windows Server 2019, wie in diesem Dokument beschrieben) verwendet.  Die Leistungsmerkmale der klassischen Planer gut verstanden werden, und die klassische Scheduler wird veranschaulicht, ably Überzeichnung Workloads – d. h. Überzeichnung von der Host VP:LP Verhältnis von einer angemessenen Gewinnspanne unterstützen (je nach den Arten von Workloads, die virtualisiert, allgemeine Ressourcenverwendung usw..).

Bei der Ausführung auf einem Virtualisierungshost mit SMT aktiviert plant die klassische Scheduler Gast VPs aus jeder virtuelle Computer auf jedes SMT-Threads gehören für einen Kern unabhängig voneinander. Aus diesem Grund können verschiedene VMs auf dem gleichen Kern ausgeführt werden, zur gleichen Zeit (einer VM in einem Thread aus einem ausgeführt wird, während einer anderen virtuellen Computer auf den anderen Thread ausgeführt wird).

### Der Planer core

Der Planer Core nutzt die Eigenschaften der SMT, Isolierung von Gast Workloads bereitzustellen, die wirkt sich auf die Sicherheit und Leistung des Systems. Der Planer Core wird sichergestellt, dass VPs aus einem virtuellen Computer auf gleichgeordneter Elemente SMT-Threads geplant werden. Dies geschieht symmetrisch so, dass wenn LPs werden in Gruppen von zwei Gruppen von zwei, VPs geplant sind, und eine Systemkerns CPU nie zwischen virtuellen Computer gemeinsam verwendet.

Durch das Planen von Gast VPs auf zugrunde liegenden SMT-Paaren, der Planer Core bietet eine hohes Maß an Sicherheitsgrenze für Workload Netzwerkisolation erzwungen, und kann auch verwendet werden, um die Leistung Variabilität für sensible Workloads Latenz zu reduzieren.

Beachten Sie, dass bei der Vice President für einen virtuellen Computer ohne SMT aktiviert, geplant ist, dass Vice President alle wichtigen genutzt wird, wenn sie ausgeführt wird, und die wichtigsten gleichgeordneter Elemente SMT-Threads Leerlauf.  Dies ist erforderlich, um die richtige Workload Isolation bieten jedoch wirkt sich auf allgemeine Systemleistung, insbesondere dann, wie das System LPs Ausnahmepfad abonnierten – d. h. werden, wenn insgesamt VP:LP Verhältnis 1:1 überschreitet. Mit Gast-VMs konfiguriert, ohne mehrere Threads pro Kern ist daher eine optimal Konfiguration.

### Vorteile der Verwendung des Planers core

Der Planer Core bietet folgende Vorteile:

* Eine hohes Maß an Sicherheitsgrenze für die Gast Workload Isolation - Gast VPs sind beschränkt auf zugrunde liegenden physischen Kern-Paaren, Reduzierung von Sicherheitsrisiken zu snooping Side-Channel-Angriffe ausführen.

* Reduzierte Workload Variabilität - Gast Workload Durchsatz Variabilität wird erheblich reduziert, bietet eine bessere Workload Konsistenz.

* Verwendung von SMT im Gast-VMs - des Betriebssystems und Anwendungen, die auf dem virtuellen Gastcomputer ausgeführt SMT Verhalten nutzen kann und Programmierschnittstellen (APIs) zum Steuern und Verteilen von Arbeit über SMT-Threads genauso, wie sie die Ausführung würde nicht virtualisierten.

Der Planer Core ist derzeit auf Azure Virtualisierungshosts verwendet, speziell auf die Grenze hohes Maß an Sicherheit und niedrigen Workload Variabilty nutzen. Microsoft geht davon aus, dass der Typ des Kerns Scheduler und weiterhin den Standard-Hypervisor Typ für die Mehrzahl der Virtualisierung Szenarien planen.  Aus diesem Grund, um sicherzustellen, dass unsere Kunden standardmäßig sicher sind, Microsoft diese Änderung für Windows Server 2019 jetzt macht.

### Core Scheduler Leistung Einfluss auf Gast workloads

Während erforderlich, um effektiv bestimmte Klassen von Sicherheitsrisiken verringern, kann der Planer Core auch potenziell Leistung reduziert werden. Kunden möglicherweise einen Einfluss auf die Leistungsmerkmale mit ihren virtuellen Computer und folgen der allgemeinen Arbeitslast Kapazität des ihre Virtualisierungshosts angezeigt. In Fällen, in denen der Core Planer einen nicht - SMT Vice President ausgeführt werden müssen, werden nur eines der Streams Anweisung in der zugrunde liegenden logischen Kern laufender anderen im Leerlauf bleiben muss. Dadurch wird die gesamte Host Kapazität für Gast Workloads begrenzt.

Diese Leistung folgen können minimiert werden, gemäß den Richtlinien in diesem Dokument. Host-Administratoren müssen sorgfältig sollten Sie ihre spezifischen Virtualisierung Szenarien für die Bereitstellung und ausgeglichen jeweilige Toleranz für Sicherheitsrisiko gegen die Notwendigkeit für maximale Workload Dichte, übermäßige Konsolidierung des Virtualisierungshosts usw. sein.

## Zum Ändern der standardmäßigen und Konfigurationen für Windows Server 2016 und Windows Server 2019 empfohlen

Bereitstellen von Hyper-V-Hosts mit den maximalen Sicherheitssituation erfordert die Verwendung der Hypervisor Core Scheduler Schrift. Um sicherzustellen, dass unsere Kunden standardmäßig sicher sind, Microsoft ändert sich das folgende standardmäßige und empfohlene Einstellungen.

>[!NOTE]
>Updates sind erforderlich, um das Konfigurationssteuerelement zugreifen, die auswählen können, während der Hypervisor interne Unterstützung für die Scheduler-Typen in der ersten Veröffentlichung von Windows Server 2016, Windows Server 1709 und Windows Server 1803 enthalten war, die Hypervisor Scheduler-Typ.  [Verstehen](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types) und Verwenden von Hyper-V-Hypervisor Scheduler Typen finden Sie Details zu diesen Updates.

### Virtualisierung Host ändert

* Der Hypervisor wird den Core-Zeitplan durch standardmäßige beginnend mit Windows Server 2019 verwenden.

* Microsoft Reccommends Konfigurieren von Core-Scheduler auf Windows Server 2016. Der Hypervisor Core Scheduler-Typ ist in Windows Server 2016 unterstützt, jedoch der Standardwert der klassischen Planer ist. Der Planer Core ist optional und muss explizit durch den Administrator Hyper-V-Host aktiviert sein.

### Ändern der VM-Konfiguration

* Auf Windows Server 2019 erben neuer virtuelle Computer mit dem Standard-VM-Version 9.0 erstellt automatisch die SMT-Eigenschaften (aktiviert oder deaktiviert) von den Virtualisierungshost. D. h. wenn SMT auf aktiviert ist wird der physische Host neu erstellten virtuellen Computer auch SMT aktiviert, und erbt die SMT-Topologie des Hosts wird standardmäßig mit der gleichen Anzahl von Hardwarethreads pro Kern wie das zugrunde liegende System den virtuellen Computer. Dies wird in der VM-Konfiguration mit HwThreadCountPerCore widergespiegelt = 0, wobei 0 angibt des virtuellen Computers sollten dem Host SMT Einstellungen erben.

* Vorhandene virtuelle Computer mit einer VM-Version 8.2 oder einer früheren Version wird behalten ihre ursprüngliche VM-Prozessor-Einstellung für HwThreadCountPerCore und der Standardwert für 8.2 VM-Version Gäste ist HwThreadCountPerCore = 1. Wenn diese Gäste auf einem Windows Server 2019 Host ausführen, werden auch wie folgt behandelt:

    1. Hat die VM Vice President Anzahl, die kleiner oder gleich der Anzahl der – ZIELSEITE Kernen ist, wird der virtuelle Computer als eine nicht SMT VM vom Core Planer behandelt. Wenn der Gast Vice President auf einem einzelnen SMT-Thread ausgeführt wird, werden die wichtigsten gleichgeordneter Elemente SMT-Threads Leerlauf überging. Dies ist nicht optimal und allgemeine Verlust der Leistung führt.

    2. Hat die VM Weitere VPs als – ZIELSEITE Kernen, werden der virtuellen Computer als einer SMT-VM vom Core Planer behandelt. Der virtuelle Computer wird jedoch nicht anderen Angaben Beachten Sie, dass es einer SMT-VM ist. Z. B. der CPUID-Anweisung oder des Windows-APIs verwenden Sie, um Abfragezeichenfolgen CPU-Topologie durch das Betriebssystem oder Anwendungen nicht angezeigt wird, dass SMT aktiviert ist.

* Bei eine vorhandene VM explizit auf Version 9.0 über den Update-VM-Vorgang von Eariler VM-Versionen aktualisiert wird, wird der virtuelle Computer den aktuellen Wert für HwThreadCountPerCore beibehalten.  Der virtuelle Computer keinen SMT-Force-fähigen.

* Unter Windows Server 2016 empfiehlt Microsoft das SMT für Gast-VMs aktivieren.  VMs erstellt unter Windows Server 2016 SMT würde deaktiviert haben wird standardmäßig, die, dass HwThreadCountPerCore auf 1 festgelegt ist, wenn explizit geändert.

>[!NOTE]
>Windows Server 2016 unterstützt keine Einstellung HwThreadCountPerCore auf 0 fest.

#### Verwalten von SMT Konfiguration des virtuellen Computers

Die Gast virtuellen Computer SMT-Konfiguration wird auf einer pro-VM-Basis festgelegt. Der hostadministrator kann überprüfen und konfigurieren Sie eine VM SMT-Konfiguration aus der folgenden Optionen auswählen:

    1. Konfigurieren von virtuellen Computern ausgeführt als SMT-fähigen, optional automatisch erben die Host-SMT-Topologie

    2. Konfigurieren von virtuellen Computern als nicht SMT ausführen

Die SMT Configuaration für einen virtuellen Computer wird in der Zusammenfassung Bereiche in der Hyper-V-Manager-Konsole angezeigt.  Konfigurieren von einer VM SMT-Einstellungen kann mithilfe der VM-Einstellungen oder PowerShell erfolgen.

#### Konfigurieren von VM SMT-Einstellungen, die mithilfe von PowerShell

Um die SMT-Einstellungen für virtuelle Gastcomputer zu konfigurieren, öffnen Sie ein PowerShell-Fenster mit über ausreichende Berechtigungen, und geben Sie ein:

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <0, 1, 2>
```

Es gilt Folgendes:

    0 = Inherit SMT topology from the host (this setting of HwThreadCountPerCore=0 is not supported on Windows Server 2016)

    1 = Non-SMT

    Values > 1 = the desired number of SMT threads per core. May not exceed the number of physical SMT threads per core.

Um die SMT-Einstellungen für virtuelle Gastcomputer zu lesen, öffnen Sie ein PowerShell-Fenster mit über ausreichende Berechtigungen, und geben Sie ein:

``` powershell
(Get-VMProcessor -VMName <VMName>).HwThreadCountPerCore
```

Beachten Sie diesen Gast-VMs mit HwThreadCountPerCore konfiguriert = 0 gibt an, dass SMT für den Gast aktiviert sein wird und die gleiche Anzahl von SMT-Threads auf dem Gast macht, wie sie auf den zugrunde liegenden Virtualisierungshost, die in der Regel 2 sind.

### Gast-VMs Druckeroptionen Änderungen an CPU-Topologie über VM Mobility Szenarien

Das Betriebssystem und Anwendungen auf einem virtuellen Computer können Änderungen an Host und VM-Einstellungen vor und angezeigt, nachdem VM-Lebenszyklusereignisse wie z. B.-Migration Live oder speichern und wiederherstellen. Während eines Vorgangs auf welchen virtuellen, das Computer Zustand gespeichert und wiederhergestellt wird, werden die VM HwThreadCountPerCore Einstellung und den realisierten Wert (d. h. die berechnete Kombination die VM-Einstellung und Konfiguration des Quellhosts) migriert. Der virtuelle Computer wird weiter ausgeführt mit diesen Einstellungen auf dem Zielhost. An dem Punkt ist der virtuelle Computer herunterfahren und neu gestartet, es ist möglich, die der realisierte Wert beobachtet durch den virtuellen Computer wird geändert. Dies sollte keine Auswirkung, als Betriebssystem- und sollte Layer-Software für die CPU-Topologieinformationen als Teil ihrer normalen Startvorgang und die Initialisierung Code Flüsse aussehen. Jedoch, da diese Start-Zeit-Initialisierung, die Sequenzen während der live-Migration oder speichern/wiederherzustellen Vorgänge, VMs übersprungen werden, die diese Statusübergänge der Tasten werden beobachten konnte die ursprünglich berechnete Wert erkannt, bis sie beendet und neu gestartet.  

### Warnungen in Bezug auf eine nicht optimale VM-Konfigurationen

Virtuelle Computer mit mehr VPs als physischen Kerne auf dem Host-Ergebnis in einer nicht optimalen Konfiguration stehen konfiguriert wurde. Der Hypervisor Planer behandelt diese VMs, als ob sie SMT unterstützenden sind. Allerdings Betriebssystem und Anwendungssoftware auf dem virtuellen Computer wird angezeigt, wenn Sie eine CPU-Topologie mit SMT ist deaktiviert. Wenn diese Bedingung erkannt wird, wird der Hyper-V-Arbeitsprozess protokolliert ein Ereignis auf den Virtualisierungshost hostadministrator darauf hinzuweisen, dass die VM-Konfiguration nicht optimal ist, und empfehlen SMT werden für den virtuellen Computer aktiviert.

#### Informationen zum Identifizieren von nicht optimal konfiguriert VMs

Ermitteln Sie nicht - SMT VMs durch Untersuchen der Systemprotokoll in der Ereignisanzeige für Hyper-V-Arbeitsprozess Ereignis-ID 3498, welcher für einen virtuellen Computer ausgelöst wird, wenn die Anzahl der VPs auf dem virtuellen Computer größer als die Anzahl der physischen Kern ist. Prozessereignisse Worker erhalten Sie in der Ereignisanzeige oder über PowerShell.

#### Abfragen der Hyper-V-Worker VM Prozessereignis mithilfe von PowerShell

Zur Abfrage für Hyper-V-Worker Prozessereignis-ID 3498 mithilfe von PowerShell, geben Sie die folgenden Befehle aus einer PowerShell-Eingabeaufforderung.

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Worker"; ID=3498}
```

### Folgen dieses Gast SMT Configuaration über die Verwendung der Hypervisor Enlightenments für Gastbetriebssysteme

Der Microsoft-Hypervisor bietet mehrere Enlightenments oder Hinweise, was das Betriebssystem in einem virtuellen Gastcomputer ausgeführt Abfragen und Optimierungen, z. B. auszulösen, die andernfalls Behandlung der verschiedenen Bedingungen verbessern, während der Ausführung profitieren, Leistung virtualisiert. Ein vor kurzem eingeführten Optimierung betrifft die Behandlung des virtuellen Prozessors Planung und die Verwendung von Betriebssystem-Gegenmaßnahmen für Side-Channel-Angriffe, die auszunutzen SMT.

>[!NOTE]
>Microsoft empfiehlt, Host-Administratoren SMT für Gast-VMs zum Optimieren der Leistung Workload zu aktivieren.

Die Details dieser Gast-Optimierung werden bereitgestellt unten, jedoch der Punkt für die Virtualisierung Host Administratoren besteht darin, dass virtuelle Computer HwThreadCountPerCore so konfiguriert, dass der Konfiguration des Hosts physischen SMT übereinstimmen sollte. Dadurch wird den Hypervisor meldet, dass es keine nicht-Architektur Core ist freigeben. Aus diesem Grund können alle unterstützenden Gast OS-Optimierungen, die die Optimierung aktiviert werden. Windows Server 2019 neue virtuelle Computer erstellen und den Standardwert der HwThreadCountPerCore (0). Ältere VMs von Windows Server 2016 migriert Hosts können auf die Windows Server 2019 Konfigurationsversion aktualisiert werden. Im Anschluss daran, Microsoft empfiehlt, die Einstellung HwThreadCountPerCore = 0.  Unter Windows Server 2016 empfiehlt Microsoft Einstellung HwThreadCountPerCore entsprechend die Host-Konfiguration (in der Regel 2).

### NoNonArchitecturalCoreSharing Optimierung details

Ab Windows Server 2016, definiert der Hypervisor eine neue Optimierung, um die Behandlung der Vice President Planung und Platzierung Gastbetriebssystem zu beschreiben. Diese Optimierung wird in den [Hypervisor Top Level Functional Specification v5.0c](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/tlfs)definiert.

Hypervisor synthetische CPUID Blatt CPUID.0x40000004.EAX:18[NoNonArchitecturalCoreSharing = 1] Gibt an, dass ein virtueller Prozessoren niemals einen physischen Kern mit einem anderen virtuellen Prozessors, mit Ausnahme von virtuellen Prozessoren freigeben, die als gleichgeordneter Elemente SMT gemeldet werden Threads. Z. B. wird eine Gast Vice President nie in einem SMT Thread zusammen mit einem Vice President Root ausgeführt, die gleichzeitig auf ein gleichgeordneter Elemente SMT-Threads auf die gleiche Prozessorkern ausgeführt werden. Diese Bedingung ist nur möglich, während der Ausführung virtualisierten und daher ein nicht-Architektur SMT-Verhalten, die schwerwiegende Sicherheitsaspekte verfügt auch über dar. Das Gastbetriebssystem können NoNonArchitecturalCoreSharing = 1 als Hinweis, dass es sicher zum Aktivieren von Optimierungen, mit denen es vermeiden Sie den Leistungsaufwand STIBP festlegen kann.

In bestimmten Konfigurationen der Hypervisor wird nicht angegeben, NoNonArchitecturalCoreSharing = 1. Als Beispiel wenn ein Host SMT aktiviert hat und so konfiguriert ist, dass die klassische Hypervisor-Scheduler verwenden NoNonArchitecturalCoreSharing 0 genutzt wird. Dies kann verhindern, dass optimierte Gäste bestimmte Optimierungen aktivieren. Aus diesem Grund empfiehlt Microsoft, dass Host-Administratoren mit SMT verlassen Sie sich auf den Hypervisor Core Planer und stellen Sie sicher, dass virtuelle Computer so konfiguriert werden, dass deren Konfiguration SMT vom Host auf Workload eine optimale Leistung zu erzielen, erben.

## Zusammenfassung

Die Bedrohungslandschaft ständig weiterentwickelt. Um sicherzustellen, dass unsere Kunden standardmäßig sicher sind, ändert Microsoft die Standardkonfiguration für den Hypervisor und virtuelle Computer starten in Windows Server 2019 Hyper-V und Bereitstellen von Richtlinien und Empfehlungen für Kunden unter Windows aktualisiert Server 2016 Hyper-V. Virtualisierung Host Administratoren sollten:

* Lesen Sie und verstehen Sie die Anleitung in diesem Dokument

* Sorgfältig bewerten Sie und passen Sie ihre Bereitstellungen Virtualisierung, um sicherzustellen, dass sie die Sicherheit, Leistung, Virtualisierung Dichte und Workload Reaktionsfähigkeit Ziele für deren spezielle Anforderungen erfüllen

* Berücksichtigen Sie erneut konfigurieren von vorhandenen Windows Server 2016 Hyper-V-Hosts, die vom Hypervisor Core Planer angeboten hohes Maß an Sicherheitsvorteile nutzen

* Aktualisieren vorhandener nicht - SMT VMs zum Reduzieren Sie Einfluss auf die Leistung von Einschränkungen, die aufgrund der Vice President Isolation, die Hardware-Sicherheitslücken bedient planen
