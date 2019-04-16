---
title: Verstehen und Verwenden von Hyper-V-Hypervisor Scheduler Typen
description: Enthält Informationen für Hyper-V-Host Administratoren über die Verwendung der Hyper-V-Scheduler Modi
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 6cb13f84-cb50-4e60-a685-54f67c9146be
ms.openlocfilehash: 7af6d68b02367d349580eacb27405c6f37e97ff8
ms.sourcegitcommit: 3883eebbba70bfea0221e510863ee1a724a5f926
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2018
ms.locfileid: "5783692"
---
# Verwalten von Hyper-V-Hypervisor Scheduler Typen

>Gilt für: Windows 10, WindowsServer 2016, Windows Server, Version 1709, Windows Server, Version 1803, Windows Server 2019

Dieser Artikel beschreibt neue Modi des virtuellen Prozessors Planung Logik erstmals in Windows Server 2016 eingeführt. Diese Modi oder Scheduler-Typen, bestimmen, wie der Hyper-V-Hypervisor reserviert und virtuelle Gast-Prozessoren Arbeit verwaltet. Ein Hyper-V-Host-Administrator kann Hypervisor Scheduler Typen auswählen, die eignen sich am besten für den Gast virtuelle Maschinen (VMs) und Konfigurieren der virtuellen Computer, um die scheduling Logik nutzen.

>[!NOTE]
>Updates sind erforderlich, um die in diesem Dokument beschriebenen Hypervisor Scheduler-Funktionen verwenden. Weitere Informationen finden Sie in der [Updates erforderlich](#required-updates).

## Hintergrund

Erläutert die Logik und Steuerelemente hinter virtuellen Hyper-V-Prozessor planen, ist es hilfreich, überprüfen Sie die grundlegenden Konzepte, die in diesem Artikel behandelt.

### Grundlegendes zu SMT

Simultane multithreading oder SMT, ist eine Technik in modernen Prozessor Entwürfen genutzt, die Prozessor Ressourcen von separaten, unabhängige Ausführungsthreads gemeinsam genutzt werden kann. SMT in der Regel bietet eine bequeme Leistungssteigerung für die meisten Arbeitslasten durch parallelisieren Berechnungen, wenn möglich, Anweisung Durchsatz erhöhen, obwohl keine Leistung erhalten oder sogar eine leichte Verlust Leistung kann auftreten, wenn Konflikte zwischen für threads Tritt auf, gemeinsam genutzte Prozessor-Ressourcen.
Prozessoren mit Unterstützung SMT sind von Intel und AMD verfügbar. Intel bezieht sich auf ihre SMT Angebote als Intel Hyper-Threading-Technologie oder Intel HT.

Für die Zwecke dieses Artikels gelten die Beschreibung der SMT und wie es von Hyper-V ausgelastet ist ebenso für Intel und AMD-Systeme.

* Weitere Informationen zu Intel HT-Technologie finden Sie unter [Intel Hyper-Threading-Technologie](https://www.intel.com/content/www/us/en/architecture-and-technology/hyper-threading/hyper-threading-technology.html)

* Weitere Informationen zu AMD SMT finden Sie unter ["Macht" Kernarchitektur](https://www.amd.com/en/technologies/zen-core)

## Grundlegendes zu wie Hyper-V-Prozessoren virtualisiert

Stellen Sie davor Hypervisor Scheduler Typen, ist es auch hilfreich zu wissen, die Hyper-V-Architektur. Eine allgemeine Zusammenfassung finden Sie in der [Übersicht über die Hyper-V-Technologie](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-technology-overview). Hierbei handelt es sich um wichtige Konzepte für die in diesem Artikel:

* Hyper-V erstellt und verwaltet virtuellen Computer Partitionen, über welche, die Compute Ressourcen zugewiesen und gemeinsam verwendet, von dem Hypervisor gesteuert. Partitionen bieten eine sichere Isolation Grenzen zwischen alle virtuellen Gastcomputer und Gast-VMs und die Root-Partition.

* Die Stamm-Partition ist selbst eine VM-Partition, obwohl es eindeutige Eigenschaften und viel größeren Berechtigungen als virtuelle Gastcomputer hat. Die Stamm-Partition bietet die Verwaltungsdienste, die alle virtuellen Gastcomputer steuern, bietet Unterstützung für virtuelle Geräte für Gastbetriebssysteme und alle Gerät e/a für virtuelle Gastcomputer verwaltet. Microsoft empfiehlt dringend, keine Arbeitslasten im Stamm-Partition ausgeführt.

* Jedes virtuellen Prozessors (Vice President) der Stammpartition ist zugeordnete 1:1 auf ein zugrunde liegenden logischen Prozessoren (– ZIELSEITE). Ein Host Vice President immer die gleiche zugrunde liegende – ZIELSEITE ausgeführt werden – es gibt keine Migration von der Stamm-Partition VPs.

* Standardmäßig können die auf dem Host VPs ausgeführt LPs auch Gast VPs ausführen.

* Ein Gast Vice President möglicherweise auf allen verfügbaren logischen Prozessoren Ausführung vom Hypervisor geplant werden. Während der Hypervisor Planer kümmert sich um zeitliche Cache Ort, NUMA-Topologie und viele andere Faktoren berücksichtigen beim Planen einer Gast Vice President, kann auf jedem Host – ZIELSEITE letztendlich die Vice President berechnet werden.

## Hypervisor Scheduler Typen

Ab Windows Server 2016 unterstützt Hyper-V-Hypervisor verschiedene Modi der Planer Logik, die bestimmen, wie der Hypervisor virtuelle Prozessoren auf den zugrunde liegenden logischen Prozessoren plant. Diese Scheduler-Typen sind:

- [Der Planer Klassisches, gleichberechtigten](#the-classic-scheduler)
- [Der Planer core](#the-core-scheduler)
- [Der Planer Stamm](#the-root-scheduler)

### Die klassische scheduler

Der klassische Scheduler wurde der Standardwert für alle Versionen von Windows Hyper-V-Hypervisor seit der Einführung, einschließlich Windows Server 2016 Hyper-V. Der klassische Planer stellt eine faire Freigabe präventiv scheduling Round-Robin-Modell für virtuelle Gast-Prozessoren bereit.

Der klassischen Scheduler-Typ ist am besten geeignet für den Großteil des herkömmlichen Hyper-V verwendet – für private Clouds, Hostinganbieter und So weiter. Die Leistungsmerkmale gut verstanden werden und sind am besten eine Breite Palette von Virtualisierung Szenarien, z. B. Überzeichnung des VPs bis hin zu IPS, viele heterogene VMs und Workloads gleichzeitig ausgeführt, größerem hohe ausgeführt Unterstützung optimiert Leistung VMs, unterstützen alle Features Satz von Hyper-V ohne Einschränkungen und vieles mehr.

### Der Planer core

Der Hypervisor Core Planer ist eine neue Alternative zum der klassischen Scheduler-Logik, die in Windows Server 2016 und Windows 10 Version 1607, eingeführt. Der Planer Core bietet ein hohes Maß an Sicherheitsgrenze für Gast Workload Isolation und Leistungseinbußen Variabilität für Arbeitslasten auf virtuellen Computern, die auf ein SMT-fähigen Virtualisierungshost ausgeführt werden. Der Planer Core ermöglicht SMT und nicht SMT virtuelle Computer gleichzeitig auf demselben Virtualisierungshost SMT-fähigen ausgeführt.

Der Planer Core nutzt den Virtualisierungshost SMT Topologie und optional macht SMT-Paare für virtuelle Gastcomputer und Zeitpläne Benutzergruppen virtuelle Gast-Prozessoren den gleichen virtuellen Computer auf der logischen Prozessoren SMT Gruppen. Dies geschieht symmetrisch, sodass Wenn LPs in sind Gruppen von zwei, VPs in Gruppen von zwei geplant sind, und ein Kern zwischen virtuellen Computern niemals.
Wenn der Vice President für einen virtuellen Computer ohne SMT geplant ist aktiviert, dass Vice President alle wichtigen genutzt wird, wenn sie ausgeführt wird.

Das Ergebnis des Core Scheduler ist, die:

* Gast VPs sind beschränkt auf zugrunde liegenden physischen Kern-Paaren, einen virtuellen Computer Prozessor Core Grenzen zu isolieren, wodurch Sicherheitslücke auf snooping Side-Channel-Angriffe von schädlichen VMs ausführen.

* Variabilität Durchsatz wird erheblich reduziert.

* Leistung ist potenziell verringert, da nur zu einer Gruppe von VPs ausgeführt werden kann, führt nur eines der Streams Anweisung im Core während der anderen im Leerlauf befindet.

* Das Betriebssystem und die Anwendung, die auf dem virtuellen Gastcomputer ausgeführt können verwendet werden, SMT Verhalten und Programmierschnittstellen (APIs) zum kontrollieren und verteilen Sie Arbeit über SMT-Threads, genau wie sie bei nicht virtualisierten ausgeführt würde.

* Eine hohes Maß an Sicherheitsgrenze für Gast Workload Isolation - Gast VPs sind beschränkt auf zugrunde liegenden physischen Kern-Paaren, Reduzierung von Sicherheitsrisiken zu snooping Side-Channel-Angriffe ausführen.

Der Planer Core wird standardmäßig ab Windows Server 2019 verwendet werden. Unter Windows Server 2016 Core Planer ist optional und muss explizit durch den Administrator Hyper-V-Host aktiviert sein, und der klassische Planer ist die Standardeinstellung.

#### Core Scheduler Verhalten mit dem Host SMT deaktiviert

Wenn der Hypervisor so konfiguriert ist, dass den Typ des Kerns Scheduler verwenden, aber die SMT-Funktion, deaktiviert oder nicht auf den Virtualisierungshost vorhanden ist ist, wird der Hypervisor das Verhalten der klassischen Scheduler Einstellung unabhängig vom Hypervisor Scheduler verwenden.

### Der Planer Stamm

Der Planer Stamm wurde mit Windows 10, Version 1803 eingeführt. Wenn der Stamm Scheduler Typ aktiviert ist, cedes der Hypervisor Kontrolle über die Arbeit planen, um die Root-Partition. Der Planer NT in der Stamm-Partition OS Instanz verwaltet alle Aspekte der Arbeit mit System LPs planen.

Der Planer Root bezieht sich auf die konkreten Anforderungen mit eine Dienstprogramm-Partition unterstützenden vererbten starken Workload Isolation, die angeben, wie mit Windows Defender Application Guard (WDAG) verwendet. Beim Planen von Aufgaben in das Stammverzeichnis OS verlassen in diesem Szenario bietet verschiedene Vorteile. Steuerung von CPU-Ressourcen gilt für Container-Szenarios können z. B. mit Dienstprogramm-Partition, die Vereinfachung der Verwaltung und Bereitstellung verwendet werden. Der Stamm OS Planer kann darüber hinaus leicht Metriken zur Ausführung Workload CPU-Auslastung innerhalb des Containers zu sammeln und verwenden Sie diese Daten als Eingabe für die gleiche scheduling Richtlinie gilt für alle anderen Arbeitslasten im System. Diese dieselben Metriken tragen ebenfalls deutlich Attribut erfolgt in einem Anwendungscontainer auf das Hostsystem funktionieren. Nachverfolgen von dieser Metriken ist schwieriger mit herkömmlichen virtuellen Computer Workloads, findet die einige Aufgaben aller ausgeführten virtuellen Computers im Auftrag statt in der Stammpartition.

#### Stamm Scheduler verwenden auf Client-Systemen

Der Planer Stamm wird ab Windows 10, Version 1803, standardmäßig auf Client-Systemen nur verwendet, in denen möglicherweise der Hypervisor zur Unterstützung der Virtualisierung basierende Sicherheit und WDAG Workload Isolation, und für den ordnungsgemäßen Betrieb von zukünftigen Systemen mit aktiviert sein heterogene Kern-Architekturen. Dies ist die einzige unterstützte Hypervisor Scheduler-Konfiguration für Client-Systeme. Administratoren sollten nicht versuchen, den Hypervisor Scheduler-Standardtyp auf Windows 10-Client-Systemen zu überschreiben.

#### CPU-Virtual Machine Resource Controls und der Stamm Planer

Die virtuellen Computer Prozessor Resource Controls von Hyper-V bereitgestellt werden nicht unterstützt, wenn der Hypervisor Stamm Planer aktiviert ist, wie der Stamm des Betriebssystems Scheduler Logik Hostressourcen auf globaler Basis verwaltet und hat keinen Kenntnisse in eines virtuellen Computers bestimmte Konfigurationseinstellungen. Die Hyper-V-VM-Prozessor Resource Controls z. B. FESTSTELLTASTE, Gewichte und reserviert, sind nur gültig, in denen der Hypervisor direkt Vice President planen, z. B. wie bei der klassische und Core Scheduler Typen steuert.

#### Stamm Scheduler Verwendung auf Server-Systeme

Der Planer Stamm ist für die Verwendung mit Hyper-V auf Servern zu diesem Zeitpunkt nicht empfohlen, da seine Leistungsmerkmale noch nicht vollständig gekennzeichnet und wurden optimiert, um die Breite Palette von Workloads, die typisch für viele Server Virtualization Bereitstellungen Rechnung zu tragen.

## Aktivieren der SMT in den virtuellen Gastcomputern

Sobald den Virtualisierungshost Hypervisor konfiguriert ist, um den Typ des Kerns Scheduler verwenden, möglicherweise virtuellen Gastcomputern SMT nutzen Sie bei Bedarf konfiguriert werden. Verfügbarmachen von der Tatsache, dass VPs Hyperthreading auf einem virtuellen Gastcomputer sind ermöglicht den Planer im Gastbetriebssystem und Arbeitslasten auf dem virtuellen Computer zu erkennen und nutzen Sie die SMT Topologie in ihren eigenen Arbeit planen. Unter Windows Server 2016 Gast SMT ist standardmäßig nicht konfiguriert und muss explizit durch den Administrator Hyper-V-Host aktiviert sein. Ab Windows Server 2019, erbt neue virtuelle Computer auf dem Host erstellt der Host SMT Topologie standardmäßig.  Das heißt, würde eine Version erstellten 9.0 VM auf einem Host mit 2 SMT-Threads pro Kern 2 SMT-Threads pro Kern auch angezeigt.

PowerShell muss so aktivieren Sie SMT in einem virtuellen Gastcomputer verwendet werden; Es gibt keine Benutzeroberfläche, die in Hyper-V-Manager bereitgestellt.
Um SMT in einem virtuellen Gastcomputer zu aktivieren, öffnen Sie ein PowerShell-Fenster mit über ausreichende Berechtigungen, und geben Sie ein:

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <n>
```

Wo <n> ist die Anzahl der SMT-Threads pro Kern dem Gast VM wird angezeigt.  
Beachten Sie, dass <n> = 0 wird legen Sie den Wert HwThreadCountPerCore Anzahl von der Host SMT-Threads pro Core Wert entsprechen.

>[!NOTE] 
>Festlegen von HwThreadCountPerCore = 0 wird unterstützt Windows Server 2019 ab.

Unten ist ein Beispiel für das Gastbetriebssystem auf einem virtuellen Computer mit 2 virtuelle Prozessoren entnommen Systeminformationen und SMT aktiviert. Das Gastbetriebssystem ist 2 logische Prozessoren, die auf dem gleichen Kern gehören erkennen.

![Screenshot, die in einem virtuellen Computer mit SMT aktiviert Gastcomputer msinfo32 anzeigt](media/Hyper-V-CoreScheduler-VM-Msinfo32.png)

## Konfigurieren des Hypervisor Scheduler Typs auf Windows Server 2016 Hyper-V

Windows Server 2016 Hyper-V verwendet das klassische Hypervisor Scheduler Modell in der Standardeinstellung. Der Hypervisor kann optional konfiguriert werden, um der Planer Core verwenden, um die Sicherheit zu erhöhen, indem Gast VPs auf entsprechenden physischen SMT-Paare ausgeführt und zur Unterstützung von virtuellen Computern mit SMT Planung für ihre Gast VPs beschränken.

>[!NOTE]
>Microsoft empfiehlt, dass alle Kunden mit Windows Server 2016 Hyper-V auswählen den Planer Core, um sicherzustellen, dass ihre Virtualisierungshosts optimal vor potenziell schädlichen Gast-VMs geschützt sind.

## Windows Server 2019 Hyper-V-Standardeinstellungen für die Verwendung des Planers core

Um sicherzustellen, dass Hyper-V-Hosts in die optimale Sicherheit Configuaration bereitgestellt werden, wird Windows Server 2019 Hyper-V jetzt das Core Hypervisor Scheduler-Modell in der Standardeinstellung verwenden. Der hostadministrator kann optional den Host um ältere klassische Planer verwenden konfigurieren. Administratoren sollten sorgfältig lesen, verstehen und sollten Sie die Auswirkungen spüren, die jede Art Scheduler auf die Sicherheit und Leistung des Virtualisierungshosts vor dem Überschreiben der Standardeinstellungen der Planer Typ hat.  Weitere Informationen finden Sie unter [Grundlegendes zu Hyper-V Scheduler Typ-Auswahl](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/understanding-hyper-v-scheduler-type-selection) .

### Erforderliche updates

>[!NOTE]
>Die folgenden Updates sind erforderlich, um die in diesem Dokument beschriebenen Hypervisor Scheduler-Funktionen verwenden. Diese Updates einschließen ändert sich, um die neue 'Hypervisorschedulertype' BCD-Option unterstützen, mit die Host-Konfiguration erforderlich ist.

| Version | Version  | Update erforderlich | Knowledge Base-Artikel |
|--------------------|------|---------|-------------:|
|Windows Server 2016 | 1607 | 2018.07 C | [KB4338822](https://support.microsoft.com/help/4338822/windows-10-update-kb4338822) |
|Windows Server 2016 | 1703 | 2018.07 C | [KB4338827](https://support.microsoft.com/help/4338827/windows-10-update-kb4338827) |
|Windows Server 2016 | 1709 | 2018.07 C | [KB4338817](https://support.microsoft.com/help/4338817/windows-10-update-kb4338817) |
|WindowsServer 2019 | 1804 | Keine | Keine |

## Auswahl der Hypervisor Scheduler geben unter Windows Server

Die Hypervisor Scheduler-Konfiguration wird über die Hypervisorschedulertype BCD-Eintrag gesteuert.

Um einen Zeitplan auszuwählen, öffnen Sie eine Befehlszeile mit Administratorrechten aus:

``` command
     bcdedit /set hypervisorschedulertype type
```

Wo `type` ist der:

* Klassische
* Core

Das System muss neu gestartet werden, damit die Änderungen in den Hypervisor Scheduler Typ wirksam wird.

>[!NOTE]
>Der Hypervisor Stamm Planer wird auf Windows Server Hyper-V zu diesem Zeitpunkt nicht unterstützt. Hyper-V-Administratoren sollten nicht versuchen, den Stamm Planer für die Verwendung mit Server Virtualization Szenarien konfigurieren.

## Bestimmen den aktuellen Scheduler-Typ

Sie können den aktuellen Hypervisor Scheduler Typ verwendeter Speicher durch Untersuchen des Sysem-Protokolls in der Ereignisanzeige für das neueste Hypervisor Launch-Ereignis-ID 2, bestimmen die meldet den Hypervisor Scheduler Typ beim Starten der Hypervisor konfiguriert. Hypervisor starten Ereignisse können von der Windows-Ereignisanzeige oder über PowerShell abgerufen werden.

Hypervisor-Start-Ereignis-ID 2 Gibt den Hypervisor Planer, wobei:

    1 = Classic scheduler, SMT disabled

    2 = Classic scheduler

    3 = Core scheduler

    4 = Root scheduler

![Screenshot mit Hypervisor Start-Ereignis-ID-2-details](media/Hyper-V-CoreScheduler-EventID2-Details.png)

![Screenshot der Ereignisanzeige anzeigen Hypervisor-Start-Ereignis-ID 2](media/Hyper-V-CoreScheduler-EventViewer.png)

### Abfragen der Hyper-V-Hypervisor Scheduler Typ einführungsveranstaltung mithilfe von PowerShell

Zur Abfrage für Hypervisor-Ereignis-ID 2 mithilfe von PowerShell, geben Sie die folgenden Befehle aus einer PowerShell-Eingabeaufforderung.

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Hypervisor"; ID=2} -MaxEvents 1
```

![Screenshot mit PowerShell-Abfrage und die Ergebnisse für Hypervisor-Start-Ereignis-ID 2](media/Hyper-V-CoreScheduler-PowerShell.png)
