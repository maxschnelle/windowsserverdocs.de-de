---
title: Auswählen einer Netzwerkkarte
description: Dieses Thema ist Teil der Netzwerk-Subsystem-Leistungsoptimierung Anleitung für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a6615411-83d9-495f-8a6a-1ebc8b12f164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4b3b9d206273dfd0e9115ebc27cf28aa960bfb0f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="choosing-a-network-adapter"></a>Auswählen einer Netzwerkkarte

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie einige der Features von Netzwerkadaptern erfahren, die Ihre Einkäufe Auswahlmöglichkeiten beeinflussen könnten.

Netzwerk-Intensive Anwendungen benötigen High-End-Netzwerkadapter. In diesem Abschnitt wird erläutert, einige Aspekte für die Auswahl von Netzwerkadaptern als auch so konfigurieren Sie unterschiedliche netzwerkadaptereinstellungen, um die netzwerkleistung zu erzielen.

> [!TIP]
>  Sie können Einstellungen des Netzwerkadapters mithilfe von Windows PowerShell konfigurieren. Weitere Informationen finden Sie unter [Netzwerkadapter-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj134956.aspx).

##  <a name="bkmk_offload"></a>Verschieben von Funktionen

Auslagern der Aufgaben von Central Processing Unit können \(CPU\) auf den Netzwerkadapter CPU-Auslastung auf dem Server reduzieren, wodurch die gesamtleistung des Systems verbessert wird.

Der Netzwerkstapel im Microsoft-Produkte kann eine Verschiebung oder mehrere Vorgänge an einen Netzwerkadapter, wenn Sie einen Netzwerkadapter mit Auswählen der entsprechenden Funktionen auslagern. Die folgende Tabelle enthält eine kurze Übersicht über die verschiedenen Auslagerungsfunktionen, die in Windows Server 2016 verfügbar sind.
  
|Typ-Abladung|Beschreibung|
|------------------|-----------------|  
|Berechnung der Prüfsumme für TCP|Der Netzwerkstapel kann die Berechnung Auslagern und Überprüfung der Transmission Control Protocol \(TCP\) Prüfsummen für senden und Empfangen von Codepfaden. Es kann auch auslagern, die Berechnung und Überprüfung von IPv4 und IPv6-Prüfsummen für senden und Empfangen von Codepfade.|  
|Berechnung der Prüfsumme für UDP |Der Netzwerkstapel kann die Berechnung Auslagern und Überprüfung des User Datagram-Protokoll \(UDP\) Prüfsummen für senden und Empfangen von Codepfaden.|
|Berechnung der Prüfsumme für IPv4 |Die Berechnung und Überprüfung von IPv4 Prüfsummen für senden und Empfangen von Codepfade, kann der Netzwerkstapel Abladen. |
|Berechnung der Prüfsumme für IPv6 |Die Berechnung und Überprüfung von IPv6 Prüfsummen für senden und Empfangen von Codepfade, kann der Netzwerkstapel Abladen. | 
|Segmentierung von großen TCP-Pakete|Die TCP/IP-Transportschicht unterstützt großer Sendungen v2 (LSOv2). Mit LSOv2 kann die TCP/IP-Transportschicht die Segmentierung von großen TCP-Pakete auf den Netzwerkadapter Abladen.|  
|Empfangen Sie Side Scaling \(RSS\)|RSS ist eine Netzwerk-Treiber-Technologie, die effiziente Verteilung des Netzwerks ermöglicht, eine Verarbeitung über mehrere CPUs in Systemen mit mehreren Prozessoren. Weitere Informationen zu RSS finden Sie weiter unten in diesem Thema.|  
|Empfangen Sie Segment Coalescing \(RSC\)|RSC ist die Möglichkeit, Gruppe Pakete zusammen, um die Kopfzeile verarbeitet werden, die zu minimieren für den Host auszuführenden erforderlich ist. Ein Maximum von 64 KB empfangenen Nutzlast kann in einer einzelnen größeren Paket für die Verarbeitung miteinander verbunden werden. Weitere Details zu RSC wird später in diesem Thema bereitgestellt.|  
  
###  <a name="bkmk_rss"></a>Empfangsseitige Skalierung

Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Windows Server 2008 R2 und Windows Server 2008 unterstützen \(RSS\) empfangsseitige Skalierung. 

Einige Server sind so konfiguriert, mit mehreren logischen Prozessoren, die Hardware-Ressourcen freigeben \ (z. B. eine physische Core\) und Kollegen die als gleichzeitige Multithreading \(SMT\) behandelt werden. Intel-Technologie ist ein Beispiel. RSS weist die Netzwerk-Verarbeitung auf bis zu einem logischen Prozessor pro Kern. Auf einem Server mit Intel Hyper-Threading, 4 Kerne und 8 logische Prozessoren verwendet RSS z. B. nicht mehr als 4 logische Prozessoren für die Netzwerk-Verarbeitung.  

RSS verteilt eingehende e/a-Netzwerkpakete zwischen logischen Prozessoren so, dass Pakete, die auf den gleichen TCP-Verbindung gehören auf die gleichen logischen Prozessor verarbeitet werden, die wodurch die Bestellung wird beibehalten. 

RSS Kontostand UDP-Unicast und multicast-Datenverkehr auch zu laden, und es leitet die zugehörigen Flüsse \ (was durch hashing der Quell- und Zielserver Addresses\ festgelegt werden) auf den gleichen logischen Prozessor erhalten Sie die Reihenfolge der zugehörigen Eingänge. Dadurch wird die Skalierbarkeit und Leistung für empfangsintensive Szenarien für Server, auf denen weniger Netzwerkadapter als bei berechtigte logische Prozessoren zu verbessern. 

#### <a name="configuring-rss"></a>Konfigurieren von RSS

In Windows Server 2016 können Sie RSS mithilfe von Windows PowerShell-Cmdlets und RSS-Profile konfigurieren. 

Sie können RSS-Profile definieren, mit der **– Profil** -Parameter von der **Set-NetAdapterRss** Windows PowerShell-Cmdlet.

**Windows PowerShell-Befehle für RSS-Konfiguration**

Die folgenden Cmdlets können Sie RSS-Parameter pro Netzwerkadapter zu finden Sie unter.
  
>[!NOTE]
>Für eine detaillierte Befehlsreferenz für jedes Cmdlet, einschließlich Syntax und Parameter können Sie die folgenden Links klicken. Darüber hinaus können Sie den Cmdlet-Namen zu übergeben **Get-Help** an der Windows PowerShell-Eingabeaufforderung ausführliche Informationen zu jedem Befehl.  

- [Disable-NetAdapterRss](https://technet.microsoft.com/library/jj130892). Dieser Befehl deaktiviert RSS auf dem Netzwerkadapter, den Sie angeben.

- [Enable-NetAdapterRss](https://technet.microsoft.com/library/jj130859). Dieser Befehl aktiviert RSS auf dem Netzwerkadapter, den Sie angeben.
  
- [Get-NetAdapterRss](https://technet.microsoft.com/library/jj130912). Dieser Befehl ruft die RSS-Eigenschaften des Netzwerkadapters, die Sie angeben.
  
- [Set-NetAdapterRss](https://technet.microsoft.com/library/jj130863). Dieser Befehl legt die RSS-Eigenschaften auf dem Netzwerkadapter, den Sie angeben.  

#### <a name="rss-profiles"></a>RSS-Profile

Sie können die **– Profil** -Parameter des Cmdlets Set-NetAdapterRss angeben, welche logischen Prozessoren der Netzwerkadapter zugewiesen sind. Verfügbare Werte für diesen Parameter sind:

- **Am nächsten gelegenen**. Logischer Prozessor Zahlen, die in der Nähe des Netzwerkadapters Basis RSS-Prozessor sind vorzuziehen. Mit diesem Profil kann das Betriebssystem neu zu verteilen logische Prozessoren, die dynamisch laden.
  
- **ClosestStatic**. Logischer Prozessor Ziffernfolge auf Basis des Netzwerkadapters RSS-Prozessor sind vorzuziehen. Mit diesem Profil wird das Betriebssystem nicht neu zu verteilen logische Prozessoren, die dynamisch laden.
  
- **NUMA**. Logischer Prozessor Zahlen sind im Allgemeinen auf verschiedenen NUMA-Knoten Verteilung die Last ausgewählt. Mit diesem Profil kann das Betriebssystem neu zu verteilen logische Prozessoren, die dynamisch laden.
  
- **NUMAStatic**. Dies ist die **Standardprofil**. Logischer Prozessor Zahlen sind im Allgemeinen auf verschiedenen NUMA-Knoten Verteilung die Last ausgewählt. Mit diesem Profil wird das Betriebssystem nicht neu zu verteilen logische Prozessoren, die dynamisch laden.

- **Konservative**. RSS verwendet so wenige Prozessoren wie möglich, um die Last aufzufangen. Mit dieser Option wird die Anzahl von Unterbrechungen reduziert.

Je nach Szenario und die Arbeitslast Merkmale, können Sie auch andere Parameter, der die **Set-NetAdapterRss** Windows PowerShell-Cmdlet, um Folgendes anzugeben:

- Pro-Adapter pro können für RSS-wie viele logische Prozessoren verwendet werden.
- Das Start-Offset für den Bereich der logischen Prozessoren.
- Der Knoten, von dem der Netzwerkadapter Speicher belegt.

Es folgen die zusätzlichen **Set-NetAdapterRss** Parameter, die Sie zum Konfigurieren von RSS verwenden können:

>[!NOTE]
>In der Beispielsyntax für jeden Parameter unter den Namen des Netzwerkadapters **Ethernet** dient als ein Beispiel für einen Wert für die **– Name** -Parameter von der **Set-NetAdapterRss** Befehl. Wenn Sie das Cmdlet ausführen, stellen Sie sicher, dass der Namen des Netzwerkadapters aus, mit denen Sie für Ihre Umgebung geeignet ist.

- **\ * MaxProcessors**: Legt die maximale Anzahl der RSS-Prozessoren verwendet werden. Dadurch wird sichergestellt, dass die Anwendungsdatenverkehr an eine maximale Anzahl von Prozessoren auf eine bestimmte Schnittstelle gebunden ist. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessors <value>`

- **\ * BaseProcessorGroup**: Legt die Basis prozessorgruppe von einem NUMA-Knoten. Dies wirkt sich auf das Prozessor-Array, das von RSS verwendet wird. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorGroup <value>`
  
- **\ * MaxProcessorGroup**: Legt die maximale prozessorgruppe von einem NUMA-Knoten. Dies wirkt sich auf das Prozessor-Array, das von RSS verwendet wird. Diese Einstellung wird eine maximale prozessorgruppe Einschränken des Lastenausgleichs innerhalb einer k-Gruppe ausgerichtet ist. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessorGroup <value>`

- **\ * BaseProcessorNumber**: Legt die Basis-Prozessor Anzahl von einem NUMA-Knoten. Dies wirkt sich auf das Prozessor-Array, das von RSS verwendet wird. Dies ermöglicht die Partitionierung von Prozessoren auf Netzwerkadapter. Dies ist der erste logische Prozessor in den Bereich der RSS-Prozessoren, der die jedem Adapter zugeordnet ist. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorNumber <Byte Value>`

- **\ * NumaNode**: die NUMA-Knoten, die jeden Netzwerkadapter Speicher zuweisen kann. Dies kann in einer k-Gruppe oder aus verschiedenen k-Gruppen sein. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –NumaNodeID <value>`

- **\ * NumberofReceiveQueues**: Wenn Ihre logischen Prozessoren für den eingehenden Datenverkehr nicht ausreichend ausgelastet sind scheinbar \ (z. B., wie Sie im Task-Manager\ angezeigt), können Sie versuchen, erhöhen die Anzahl der RSS-Warteschlangen vom Standardwert 2 auf das Maximum, das durch Ihren Netzwerkadapter unterstützt wird. Der Netzwerkadapter möglicherweise Optionen, um die Anzahl der RSS-Warteschlangen als Bestandteil des Treibers ändern. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –NumberOfReceiveQueues <value>`

Weitere Informationen finden Sie im folgenden Link zum Herunterladen [skalierbare Networking: Eliminieren der erhalten Verarbeitung Engpass – Einführung in die RSS-](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/NDIS_RSS.doc) im Word-Format.
  
#### <a name="understanding-rss-performance"></a>Grundlegendes zur RSS-Leistung

Optimieren RSS erfordert die Konfiguration und die Logik des Lastenausgleichs zu verstehen. Um sicherzustellen, dass die RSS-Einstellungen übernommen wurden, wenn Sie ausführen, überprüfen Sie die Ausgabe kann die **Get-NetAdapterRss** Windows PowerShell-Cmdlet. Folgendes ist die Ausgabe dieses Cmdlets.
  
```

PS C:\Users\Administrator> get-netadapterrss  
Name                           : testnic 2  
InterfaceDescription           : Broadcom BCM5708C NetXtreme II GigE (NDIS VBD Client) #66
Enabled                        : True
NumberOfReceiveQueues          : 2
Profile                        : NUMAStatic
BaseProcessor: [Group:Number]  : 0:0
MaxProcessor: [Group:Number]   : 0:15
MaxProcessors                  : 8
  
IndirectionTable: [Group:Number]:
     0:0    0:4    0:0    0:4    0:0    0:4    0:0    0:4  
…   
(# indirection table entries are a power of 2 and based on # of processors)  
…   
                          0:0    0:4    0:0    0:4    0:0    0:4    0:0    0:4  
```  

Zusätzlich zur Wiedergabe von Parametern, die festgelegt wurden, ist der wichtigste Aspekt der Ausgabe die Dereferenzierung Tabellenausgabe. Der Dereferenzierung Tabelle Buckets der Hash-Tabelle, die verwendet werden, um eingehenden Datenverkehr zu verteilen. In diesem Beispiel legt die N:c Notation der Numa K-Gruppe: CPU-Index-Paar, das verwendet wird, um eingehenden Datenverkehr weiterzuleiten. Wir genau 2 eindeutigen Einträge finden Sie unter (0:0 und 0:4), die k-Gruppe 0/CPU 0 und k-Group-0/4 cpu bzw. darstellen.

Es gibt nur eine k-Gruppe für dieses System (0 KB-Gruppe) und eine n (, wobei n < = 128) Dereferenzierung Eintrag. Da die Anzahl der Warteschlangen empfangen auf 2, nur 2 Prozessoren festgelegt ist (0:0, 0:4) - werden ausgewählt werden, auch wenn die maximale Anzahl an Prozessoren auf 8 festgelegt ist. Im Grunde ist der indirektionstabelle hashing von eingehenden Datenverkehr, um nur 2 CPUs aus dem 8 verwenden, die verfügbar sind.

Um die CPUs vollständig nutzen zu können, muss die Anzahl der RSS-Warteschlangen empfangen Max Prozessoren größer oder gleich sein. Im vorherigen Beispiel sollte der Empfangswarteschlange 8 oder höher festgelegt werden.

#### <a name="nic-teaming-and-rss"></a>NIC-Teaming und RSS

RSS kann auf einem Netzwerkadapter aktiviert werden, die mit einem anderen Netzwerkschnittstellenkarte mit NIC-Teaming zusammengeschlossen ist. In diesem Szenario kann nur die zugrunde liegenden physischen Netzwerkadapter für die Verwendung von RSS konfiguriert werden. Ein Benutzer kann nicht auf den kombinierten Netzwerkadapter RSS-Cmdlets festlegen.
  
###  <a name="bkmk_rsc"></a>Receive Segment Coalescing (RSC)

Erhalten Sie Segment Coalescing \(RSC\) hilft Leistung durch Reduzieren der Anzahl der IP-Header, die für eine bestimmte Menge an empfangenen Daten verarbeitet werden. Es sollte verwendet werden, können Sie der Leistung der empfangenen Daten durch Gruppieren von \(or coalescing\) kleinere Pakete größeren Einheiten skalieren.

Dieser Ansatz kann mit Vorteile, hauptsächlich in Durchsatzes Wartezeit beeinflussen. RSC wird empfohlen, den Durchsatz für empfangene rechenintensive arbeitsauslastungen erhöhen. Berücksichtigen Sie Netzwerkadapter, die RSC unterstützen bereitstellen. 

Auf diese Netzwerkadapter, sicherzustellen, dass RSC auf \ (Dies ist der Standard-Setting\), es sei denn, Sie spezifische Workloads \ (z. B. mit geringer Latenz, geringer Durchsatz Networking\), profitieren Sie Anzeigen von RSC deaktiviert wird.

#### <a name="understanding-rsc-diagnostics"></a>Grundlegendes zu RSC-Diagnose

Sie können RSC mithilfe von Windows PowerShell-Cmdlets diagnostizieren **Get-NetAdapterRsc** und **Get-NetAdapterStatistics**.

Es folgt der Ausgabe, wenn Sie das Cmdlet Get-NetAdapterRsc ausführen.

```  

PS C:\Users\Administrator> Get-NetAdapterRsc  
  
Name                       IPv4Enabled  IPv6Enabled  IPv4Operational IPv6Operational               IPv4FailureReason              IPv6Failure  
                                            Reason  
----                           -----------  -----------  --------------- --------------- ----------------- ------------  
Ethernet                       True         False        True            False                  NoFailure       NicProperties  
  
```  

Die **abrufen** Cmdlet zeigt, ob RSC auf der Benutzeroberfläche aktiviert ist und ob TCP RSC in einen betriebsbereiten Zustand sein kann. Die Fehlerursache enthält Details zu dem Fehler um RSC auf dieser Schnittstelle zu aktivieren.

Im vorherigen Szenario ist IPv4 RSC unterstützten und betriebliche auf der Benutzeroberfläche. Fehler bei der Diagnose kann einer der zusammengeführter Bytes oder verursachten Ausnahmen finden Sie unter. Dies bietet einen Überblick über die zusammenfügen Probleme.

Es folgt der Ausgabe, wenn Sie das Cmdlet Get-NetAdapterStatistics ausführen.

```  
PS C:\Users\Administrator> $x = Get-NetAdapterStatistics “myAdapter”   
PS C:\Users\Administrator> $x.rscstatistics  
  
CoalescedBytes       : 0  
CoalescedPackets     : 0  
CoalescingEvents     : 0  
CoalescingExceptions : 0  
  
```  

#### <a name="rsc-and-virtualization"></a>RSC und Virtualisierung

RSC wird nur auf dem physischen Host unterstützt, wenn der Netzwerkadapter des Hosts nicht mit dem virtuellen Hyper-V-Switch gebunden ist. RSC ist vom Betriebssystem deaktiviert, wenn der Host mit dem virtuellen Hyper-V-Switch gebunden ist. Darüber hinaus erhalten virtuelle Maschinen nicht RSC hat den Vorteil, da virtuelle Netzwerkadapter RSC nicht unterstützt werden.

RSC kann für einen virtuellen Computer aktiviert werden, wenn die Single-Root Input/Output Virtualization \(SR-IOV\) aktiviert ist. In diesem Fall unterstützen virtuelle Funktionen RSC-Funktion. Daher erhalten virtuelle Computer auch den Vorteil, RSC.

##  <a name="bkmk_resources"></a>Adapter-Netzwerkressourcen

Einige Netzwerkadapter verwalten aktiv Ressourcen, um eine optimale Leistung zu erzielen. Mehrere Netzwerkadapter können Sie manuell konfigurieren von Ressourcen mithilfe der **Erweiterte Netzwerkfunktionen** Registerkarte für den Adapter. Für diese Adapter können Sie die Werte der eine Anzahl von Parametern, einschließlich der Anzahl der Empfangspuffer festlegen und Puffern zu senden.

Konfigurieren von Netzwerkressourcen Adapter wird durch die Verwendung der folgenden Windows PowerShell-Cmdlets vereinfacht.

- [Get-NetAdapterAdvancedProperty](https://technet.microsoft.com/library/jj130901.aspx)

- [Set-NetAdapterAdvancedProperty](https://technet.microsoft.com/library/jj130894.aspx)

- [Enable-NetAdapter](https://technet.microsoft.com/library/jj130876.aspx)

- [Enable-NetAdapterBinding](https://technet.microsoft.com/library/jj130913.aspx)

- [Enable-NetAdapterChecksumOffload](https://technet.microsoft.com/library/jj130918.aspx)

- [Enable-NetAdapterIPSecOffload](https://technet.microsoft.com/library/jj130890.aspx)

- [Enable-NetAdapterLso](https://technet.microsoft.com/library/jj130922.aspx)

- [Enable-NetAdapterPowerManagement](https://technet.microsoft.com/library/jj130907.aspx)

- [Enable-NetAdapterQos](https://technet.microsoft.com/library/jj130866.aspx)

- [Enable-NetAdapterRDMA](https://technet.microsoft.com/library/jj130909.aspx)

- [Enable-NetAdapterSriov](https://technet.microsoft.com/library/jj130899.aspx)

Weitere Informationen finden Sie unter [Netzwerkadapter-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj134956.aspx).

Links zu allen Themen in diesem Handbuch finden Sie [Optimieren der Leistung mit Subsystem](net-sub-performance-top.md).