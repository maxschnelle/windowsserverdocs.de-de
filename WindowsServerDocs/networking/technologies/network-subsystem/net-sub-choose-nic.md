---
title: Auswählen einer Netzwerkkarte
description: Dieses Thema ist Teil des Leitfadens Netzwerk-Subsystem zur Leistungsoptimierung für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a6615411-83d9-495f-8a6a-1ebc8b12f164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2b50f4b286e90a450278243c0294ea0aa7f221bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875851"
---
# <a name="choosing-a-network-adapter"></a>Auswählen einer Netzwerkkarte

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um einige der Features von Netzwerkadaptern zu erfahren, die Ihre Erwerb Auswahl auswirken.

Netzwerkintensiven Anwendungen erfordern Hochleistungs-Netzwerkadapter. In diesem Abschnitt werden einige Überlegungen beim Auswählen der Netzwerkadapter, und wie so konfigurieren Sie verschiedene Einstellungen für Netzwerkadapter um die beste netzwerkleistung zu erzielen.

> [!TIP]
>  Sie können die Einstellungen des Netzwerkadapters konfigurieren, mithilfe von Windows PowerShell. Weitere Informationen finden Sie unter [Netzwerkadapter-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj134956.aspx).

##  <a name="bkmk_offload"></a> Auslagern von Funktionen

Auslagern der Aufgaben von Central Processing Unit \(CPU\) Adapter kann mit dem Netzwerk CPU-Auslastung auf dem Server, wodurch das verbessert die gesamtleistung des Systems reduzieren.

Die Netzwerkstapel in Microsoft-Produkten kann auslagern, eine oder mehr Aufgaben an einen Netzwerkadapter, wenn Sie einen Netzwerkadapter auswählen, der die entsprechende Auslagern Funktionen. Die folgende Tabelle enthält eine kurze Übersicht über verschiedene abladungsfunktionen, die in Windows Server 2016 verfügbar sind.
  
|Auslagern von Typ|Beschreibung|
|------------------|-----------------|  
|Prüfsummenberechnung für TCP|Die Berechnung und die Überprüfung des Transmission Control Protocol, kann der Netzwerkstapel Abladen \(TCP\) Prüfsummen für senden und Empfangen von Codepfade. Sie können auch auslagern, der Berechnung und die Überprüfung von IPv4 und IPv6-Prüfsummen für senden und Empfangen von Codepfade.|  
|Prüfsummenberechnung für UDP |Die Berechnung und die Überprüfung des User Datagram-Protokoll, kann der Netzwerkstapel Abladen \(UDP\) Prüfsummen für senden und Empfangen von Codepfade.|
|Prüfsummenberechnung für IPv4 |Die Berechnung und Überprüfung von IPv4 Prüfsummen für senden und Empfangen von Codepfade, kann die Netzwerkstapel Abladen. |
|Prüfsummenberechnung für IPv6 |Die Berechnung und Überprüfung von IPv6 Prüfsummen für senden und Empfangen von Codepfade, kann die Netzwerkstapel Abladen. | 
|Segmentierung von TCP-Pakete, die große|Die TCP/IP-Transportschicht unterstützt v2 Large Send Offload (LSOv2). Mit LSOv2 kann die TCP/IP-Transportschicht die Segmentierung von großen TCP-Pakete auf den Netzwerkadapter Abladen.|  
|Empfangsseitige Skalierung \(RSS\)|RSS ist eine Netzwerk-Treiber-Technologie, die effiziente Verteilung des Netzwerks ermöglicht, empfangsverarbeitung über mehrere CPUs in Systemen mit mehreren Prozessoren. Weitere Informationen zu RSS wird weiter unten in diesem Thema bereitgestellt.|  
|Empfang zusammengeführter Segmente \(RSC\)|RSC ist die Möglichkeit, Pakete der Gruppe zusammen, um den Header, die verarbeitet wird, zu minimieren. erforderlich für den Host ausführen. Ein Maximum von 64 KB, der empfangenen Nutzlast kann in einem einzelnen größeren Paket für die Verarbeitung vereinigt werden. Weitere Informationen zu RSC wird weiter unten in diesem Thema bereitgestellt.|  
  
###  <a name="bkmk_rss"></a> Empfangsseitige Skalierung

Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Windows Server 2008 R2 und Windows Server 2008 unterstützen Receive Side Scaling \(RSS\). 

Einige Server sind so konfiguriert, mit mehreren logischen Prozessoren, die Hardwareressourcen freigeben \(wie eine physische Core\) und die als gleichzeitige Multithreading behandelt \(SMT\) Peers. Intel Hyper-Threading-Technologie ist ein Beispiel. RSS weist netzwerkverarbeitung auf bis zu einem logischen Prozessor pro Kern. Beispielsweise verwendet RSS auf einem Server mit Intel Hyper-Threading, 4 Prozessorkerne und 8 logische Prozessoren, mehr als 4 logische Prozessoren für die netzwerkverarbeitung.  

RSS verteilt die eingehenden e/a-Netzwerkpakete zwischen logischen Prozessoren, damit Pakete die gehören, die gleiche TCP-Verbindung auf dem gleichen logischen Prozessor verarbeitet werden, die Reihenfolge beibehält. 

RSS auch laden, eines UDP-Unicast und -multicast-Datenverkehr und leitet dazugehörige Flows \(die durch eine Hashberechnung für die Quell- und Ziel-Adressen bestimmt sind\) auf dem gleichen logischen Prozessor, beibehalten der Reihenfolge von verwandten erhaltene Anforderungen. Dies verbessert die Skalierbarkeit und Leistung für Empfangsvorgänge Szenarien für den Server, die weniger Netzwerkadapter als mit deren verfügbare logische Prozessoren verfügen. 

#### <a name="configuring-rss"></a>Konfiguration von RSS

In Windows Server 2016 können Sie RSS mithilfe von Windows PowerShell-Cmdlets und RSS-Profile konfigurieren. 

Sie können RSS-Profile definieren, mit der **– Profil** Parameter, der die **Set-NetAdapterRss** Windows PowerShell-Cmdlet.

**Windows PowerShell-Befehle für die RSS-Konfiguration**

Die folgenden Cmdlets können Sie anzeigen und ändern Sie die RSS-Parameter pro Netzwerkadapter.
  
>[!NOTE]
>Eine ausführliche Befehl-Referenz für die einzelnen Cmdlets, einschließlich Syntax und Parameter können Sie die folgenden Links klicken. Darüber hinaus können Sie den Cmdlet-Namen zu übergeben **Get-Help** an der Windows PowerShell-Eingabeaufforderung, Weitere Informationen zu den einzelnen Befehlen.  

- [Disable-NetAdapterRss](https://technet.microsoft.com/library/jj130892). Dieser Befehl deaktiviert RSS auf dem Netzwerkadapter, den Sie angeben.

- [Enable-NetAdapterRss](https://technet.microsoft.com/library/jj130859). Dieser Befehl aktiviert die RSS auf dem Netzwerkadapter, den Sie angeben.
  
- [Get-NetAdapterRss](https://technet.microsoft.com/library/jj130912). Dieser Befehl ruft RSS-Eigenschaften des Netzwerkadapters, die Sie angeben.
  
- [Set-NetAdapterRss](https://technet.microsoft.com/library/jj130863). Dieser Befehl legt die RSS-Eigenschaften fest, auf dem Netzwerkadapter, den Sie angeben.  

#### <a name="rss-profiles"></a>RSS-Profile

Sie können die **– Profil** -Parameter des Cmdlets Set-NetAdapterRss angeben, welche logische Prozessoren zugewiesen werden, bis der Netzwerkadapter. Verfügbare Werte für diesen Parameter sind:

- **Am nächsten**. Nummern der logischen Prozessoren, die in der Nähe der Netzwerkadapter die Basis-RSS-Prozessor werden bevorzugt. Dieses Profil ist kann das Betriebssystem logische Prozessoren, die dynamisch je nach Auslastung ausgleichen.
  
- **ClosestStatic**. Nummern der logischen Prozessoren in der Nähe der Netzwerkadapter die Basis-RSS-Prozessor werden bevorzugt. Dieses Profil ist das Betriebssystem keine logische Prozessoren, die dynamisch je nach Auslastung ausgleichen.
  
- **NUMA**. Nummern der logischen Prozessoren sind in der Regel auf unterschiedlichen NUMA-Knoten ausgewählt, um die Last zu verteilen. Dieses Profil ist kann das Betriebssystem logische Prozessoren, die dynamisch je nach Auslastung ausgleichen.
  
- **NUMAStatic**. Dies ist die **Standardprofil**. Nummern der logischen Prozessoren sind in der Regel auf unterschiedlichen NUMA-Knoten ausgewählt, um die Last zu verteilen. Dieses Profil wird das Betriebssystem keine logische Prozessoren, die dynamisch je nach Auslastung ausgleichen.

- **Konservative**. Um die Last aufzufangen verwendet RSS so wenige Prozessoren wie möglich. Diese Option reduziert die Anzahl von Unterbrechungen.

Je nach Szenario und den Merkmalen der arbeitsauslastung, Sie können auch andere Parameter, der die **Set-NetAdapterRss** Windows PowerShell-Cmdlet, um Folgendes anzugeben:

- Einzelne Adapter pro-Netzwerk können wie viele logische Prozessoren für RSS verwendet werden.
- Der Startoffset für den Bereich der logischen Prozessoren.
- Der Knoten, von dem der Netzwerkadapter den Arbeitsspeicher zuweist.

Es folgen die zusätzlichen **Set-NetAdapterRss** Parameter, die Sie verwenden können, um RSS zu konfigurieren:

>[!NOTE]
>In der Beispielsyntax für jeden Parameter unten den Namen des Netzwerkadapters **Ethernet** dient als ein Beispielwert für die **– Name** Parameter, der die **Set-NetAdapterRss** -Befehl. Wenn Sie das Cmdlet ausführen, stellen Sie sicher, dass der Netzwerknamen für den Adapter, mit denen Sie für Ihre Umgebung geeignet ist.

- **\* MaxProcessors**: Legt die maximale Anzahl der RSS-Prozessoren verwendet werden. Dadurch wird sichergestellt, dass der Datenverkehr auf eine maximale Anzahl der Prozessoren auf eine bestimmte Schnittstelle gebunden ist. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessors <value>`

- **\* BaseProcessorGroup**: Legt fest, die Basis prozessorgruppe, der einem NUMA-Knoten. Dies wirkt sich die Prozessor-Array, das vom RSS verwendet wird. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorGroup <value>`
  
- **\* MaxProcessorGroup**: Legt die maximale Prozessorgruppen eines NUMA-Knotens fest. Dies wirkt sich die Prozessor-Array, das vom RSS verwendet wird. Durch Festlegen dieses Werts eine maximale prozessorgruppe eingeschränkt wird, sodass Lastenausgleich innerhalb einer k-Gruppe ausgerichtet ist. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessorGroup <value>`

- **\* BaseProcessorNumber**: Legt fest, die Basis-Prozessor-Anzahl der einem NUMA-Knoten. Dies wirkt sich die Prozessor-Array, das vom RSS verwendet wird. Dies ermöglicht die Partitionierung von Prozessoren für die Netzwerkadapter. Dies ist der erste logische Prozessor in den Bereich der RSS-Prozessoren, der die einzelnen Adapter zugewiesen ist. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorNumber <Byte Value>`

- **\* NumaNode**: Die NUMA-Knoten, dem Arbeitsspeicher von einzelnen Netzwerkadapter zugewiesen werden kann. Dies kann innerhalb einer k-Gruppe oder aus anderen k-Gruppen sein. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –NumaNodeID <value>`

- **\* NumberofReceiveQueues**: Wenn Ihre logischen Prozessoren für den eingehenden Datenverkehr nicht ausreichend ausgelastet sind anscheinend \(z. B. wie angezeigt im Task-Manager\), können Sie versuchen, erhöhen die Anzahl der RSS-Warteschlangen vom Standardwert 2 auf den Höchstwert, der durch Ihren Netzwerkadapter unterstützt wird . Ihr Netzwerkadapter möglicherweise Optionen zum Ändern der Anzahl der RSS-Warteschlangen als Teil des Treibers. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –NumberOfReceiveQueues <value>`

Weitere Informationen finden Sie den folgenden Link zum download [Scalable Networking: Beseitigen der Engpass erhalten verarbeiten – Einführung in RSS](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/NDIS_RSS.doc) im Word-Format.
  
#### <a name="understanding-rss-performance"></a>RSS-Leistung

Optimieren von RSS, ist das Verständnis der Konfiguration und die Logik des Lastenausgleichs erforderlich. Um sicherzustellen, dass die RSS-Einstellungen übernommen wurden, können Sie die Ausgabe überprüfen, beim Ausführen der **Get-NetAdapterRss** Windows PowerShell-Cmdlet. Es folgt der Ausgabe dieses Cmdlets.
  
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

Zusätzlich zum Ausgeben von Parametern, die festgelegt wurden, ist der wichtigste Aspekt der Ausgabe der Tabellenausgabe Dereferenzierung. Die Dereferenzierung Tabelle zeigt die hashbuckets für die Tabelle, die verwendet werden, um eingehenden Datenverkehr zu verteilen. In diesem Beispiel legt die N:c-Notation die Numa-KB-Gruppe: CPU-Index-Paar, das verwendet wird, um eingehenden Datenverkehr weiterleiten. Sehen Sie genau 2 eindeutiger Einträge ein (0:0 und 0.: 4), die k-Gruppe 0/CPU des 0 und k-Gruppe 0/cpu 4 bzw. darstellen.

Es gibt nur eine k-Gruppe für dieses System (k-Gruppe 0) und "n" eine (, wobei n < = 128) Tabelleneintrag Dereferenzierung. Da die Anzahl der Receive-Warteschlangen auf 2, nur 2 Prozessoren festgelegt ist (0:0, 0:4) - werden ausgewählt werden, auch wenn die maximale Anzahl an Prozessoren auf 8 festgelegt ist. Der indirektionstabelle hashing aktiviert ist, wird eingehenden Datenverkehr nur 2 CPUs aus dem 8 verwenden, die verfügbar sind.

Um den CPUs vollständig nutzen zu können, muss die Anzahl der RSS-erhalten Warteschlangen gleich oder größer als die maximale Anzahl von Prozessoren. Im vorherigen Beispiel sollte der Warteschlange zu empfangen, 8 oder höher festgelegt werden.

#### <a name="nic-teaming-and-rss"></a>NIC-Teamvorgang und RSS

RSS kann auf einem Netzwerkadapter aktiviert werden, die mit einem anderen Netzwerk-Schnittstellenkarte mit NIC-Teamvorgang in einem Team verwendet wird. In diesem Szenario kann nur der zugrunde liegenden physischen Netzwerkadapter konfiguriert werden, um RSS zu verwenden. Ein Benutzer kann nicht RSS-Cmdlets für den kombinierten Netzwerkadapter festgelegt.
  
###  <a name="bkmk_rsc"></a> Receive Segment Coalescing (RSC)

Empfang zusammengeführter Segmente \(RSC\) Leistung durch Verringern der Anzahl der IP-Header, die für einen bestimmten Zeitraum der empfangenen Daten verarbeitet werden können. Er sollte verwendet werden, können Sie die Leistung der empfangenen Daten durch Gruppieren von skalieren \(oder Zusammenfügen\) kleinere Pakete in größeren Einheiten.

Dieser Ansatz kann die Latenz Vorteile, die hauptsächlich in Durchsatzes dargestellt beeinflussen. RSC wird empfohlen, zur Steigerung des Durchsatzes für empfangene hohe Workloads. Erwägen Sie die Bereitstellung der Netzwerkadapter, RSC zu unterstützen. 

Auf diese Netzwerkadapter stellen Sie sicher, dass RSC befindet \(Dies ist die Standardeinstellung\), es sei denn, Sie haben, dass bestimmte Workloads \(z. B. geringe Latenz, der geringen Durchsatz Netzwerke\) , Show Vorteil von RSC wird deaktiviert .

#### <a name="understanding-rsc-diagnostics"></a>Grundlegendes zu RSC Diagnosen

Sie können RSC mithilfe der Windows PowerShell-Cmdlets diagnostizieren **Get-NetAdapterRsc** und **Get-NetAdapterStatistics**.

Folgendes ist Beispiel der Ausgabe aus, wenn Sie das Cmdlet Get-NetAdapterRsc ausführen.

```  

PS C:\Users\Administrator> Get-NetAdapterRsc  
  
Name                       IPv4Enabled  IPv6Enabled  IPv4Operational IPv6Operational               IPv4FailureReason              IPv6Failure  
                                            Reason  
----                           -----------  -----------  --------------- --------------- ----------------- ------------  
Ethernet                       True         False        True            False                  NoFailure       NicProperties  
  
```  

Die **erhalten** -Cmdlet zeigt, ob der RSC in der Benutzeroberfläche aktiviert ist und ob TCP für RSC in einen funktionsfähigen Zustand befinden kann. Die Fehlerursache enthält Details zu dem Fehler um RSC auf dieser Schnittstelle zu aktivieren.

Im vorherigen Szenario ist IPv4 RSC nur und operative in der Schnittstelle an. Um die Diagnose von Fehlern zu verstehen, sehen die zusammengeführte Bytes oder Ausnahmen. Dies bietet einen Überblick über die zusammenfügenden Probleme.

Folgendes ist Beispiel der Ausgabe aus, wenn Sie das Cmdlet Get-NetAdapterStatistics ausführen.

```  
PS C:\Users\Administrator> $x = Get-NetAdapterStatistics “myAdapter”   
PS C:\Users\Administrator> $x.rscstatistics  
  
CoalescedBytes       : 0  
CoalescedPackets     : 0  
CoalescingEvents     : 0  
CoalescingExceptions : 0  
  
```  

#### <a name="rsc-and-virtualization"></a>RSC und Virtualisierung

RSC wird nur auf dem physischen Host unterstützt, wenn der Netzwerkadapter des Hosts nicht mit dem virtuellen Hyper-V-Switch gebunden ist. RSC wird vom Betriebssystem deaktiviert, wenn der Host mit dem virtuellen Hyper-V-Switch gebunden ist. Darüber hinaus erhalte virtuelle Computer nicht den Vorteil, dass RSC, da virtuelle Netzwerkadapter nicht RSC unterstützen.

RSC kann für einen virtuellen Computer aktiviert werden, wenn Single Root Input/Output Virtualization \(SR-IOV\) aktiviert ist. In diesem Fall unterstützt virtuelle Funktionen, die über RSC-Funktion; Daher erhalten virtuelle Computer außerdem den Vorteil, dass RSC.

##  <a name="bkmk_resources"></a> Netzwerkressourcen-Adapter

Einige Netzwerkadapter verwalten aktiv Ressourcen, um die optimale Leistung zu erzielen. Mehrere Netzwerkadapter können Sie so konfigurieren Sie die Ressourcen manuell mithilfe der **Advanced Networking** Registerkarte für den Adapter. Für Adapter dieser Art können Sie die Werte einer Reihe von Parametern, einschließlich der Anzahl der Empfangspuffer festlegen und senden Puffer.

Konfigurieren von Netzwerkressourcen-Adapter wird durch die Verwendung der folgenden Windows PowerShell-Cmdlets vereinfacht.

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