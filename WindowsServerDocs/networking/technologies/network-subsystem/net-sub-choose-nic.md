---
title: Auswählen einer Netzwerkkarte
description: Dieses Thema ist Teil des Handbuch zur Leistungsoptimierung des Netzwerk Subsystems für Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: a6615411-83d9-495f-8a6a-1ebc8b12f164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9271cf4e5f50adf93f421e830a226507034ac454
ms.sourcegitcommit: 1c75e4b3f5895f9fa33efffd06822dca301d4835
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2020
ms.locfileid: "77517475"
---
# <a name="choosing-a-network-adapter"></a>Auswählen einer Netzwerkkarte

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über die Features von Netzwerkadaptern, die sich auf Ihre Kaufoptionen auswirken können.

Netzwerk intensive Anwendungen erfordern hochleistungsfähige Netzwerkadapter. In diesem Abschnitt werden einige Überlegungen zur Auswahl von Netzwerkadaptern behandelt, und es wird beschrieben, wie Sie verschiedene Netzwerkadapter Einstellungen konfigurieren, um die beste Netzwerkleistung zu erzielen.

> [!TIP]
>  Sie können die Einstellungen für Netzwerkadapter mithilfe von Windows PowerShell konfigurieren. Weitere Informationen finden Sie unter [Netzwerk Adapter-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/netadapter).

##  <a name="bkmk_offload"></a>Offload-Funktionen

Durch das Auslagern von Tasks von der zentralen Verarbeitungseinheit \(CPU-\) auf den Netzwerkadapter kann die CPU-Auslastung auf dem Server verringert werden, was die Gesamtsystemleistung verbessert.

Der Netzwerk Stapel in Microsoft-Produkten kann eine oder mehrere Tasks auf einen Netzwerkadapter auslagern, wenn Sie einen Netzwerkadapter auswählen, der über die entsprechenden Auslagerung-Funktionen verfügt. In der folgenden Tabelle finden Sie eine kurze Übersicht über die verschiedenen Auslagerungs Funktionen, die in Windows Server 2016 verfügbar sind.
  
|Offload-Typ|Beschreibung|
|------------------|-----------------|  
|Prüfsummenberechnung für TCP|Der Netzwerk Stapel kann die Berechnung und Validierung des Übertragungs Steuerungs Protokolls \(TCP\) Prüfsummen für Sende-und Empfangs Codepfade auslagern. Sie kann auch die Berechnung und Validierung von IPv4-und IPv6-Prüfsummen in Sende-und Empfangs Codepfade auslagern.|  
|Prüfsummenberechnung für UDP |Der Netzwerk Stapel kann die Berechnung und Überprüfung des User Datagram-Protokolls \(UDP-\) Prüfsummen für Sende-und Empfangs Code Pfade auslagern.|
|Prüfsummenberechnung für IPv4 |Der Netzwerk Stapel kann die Berechnung und Überprüfung von IPv4-Prüfsummen in Sende-und Empfangs Codepfade auslagern. |
|Prüfsummenberechnung für IPv6 |Der Netzwerk Stapel kann die Berechnung und Validierung von IPv6-Prüfsummen in Sende-und Empfangs Codepfade auslagern. | 
|Segmentierung von großen TCP-Paketen|Die TCP/IP-Transportschicht unterstützt große Sende Abladung v2 (LSOv2). Mit LSOv2 kann die TCP/IP-Transportschicht die Segmentierung von großen TCP-Paketen auf den Netzwerkadapter auslagern.|  
|Empfangs seitige Skalierung \(RSS-\)|RSS ist eine Netzwerktreiber Technologie, die die effiziente Verteilung der Netzwerk Empfangs Verarbeitung auf mehrere CPUs in Multiprozessorsystemen ermöglicht. Weitere Informationen zu RSS finden Sie weiter unten in diesem Thema.|  
|Empfangen von Segmentieren von Segmenten \(RSC\)|RSC ist die Möglichkeit, Pakete zu gruppieren, um die Header Verarbeitung zu minimieren, die für die Ausführung des Hosts erforderlich ist. Maximal 64 KB empfangene Nutzlast können zur Verarbeitung in ein einzelnes größeres Paket zusammengepackt werden. Weitere Details zu RSC finden Sie weiter unten in diesem Thema.|  
  
###  <a name="bkmk_rss"></a>Empfangs seitige Skalierung

Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Windows Server 2008 R2 und Windows Server 2008 unterstützen die Empfangs seitige Skalierung \(RSS-\). 

Einige Server sind mit mehreren logischen Prozessoren konfiguriert, die Hardware Ressourcen gemeinsam nutzen \(z. b. ein physischer Kern\) und die als gleichzeitige Multithreading \(SMT\) Peers behandelt werden. Ein Beispiel hierfür ist die Hyper-Threading-Technologie von Intel. RSS leitet die Netzwerk Verarbeitung auf bis zu einen logischen Prozessor pro Kern um. Beispielsweise verwendet RSS auf einem Server mit Intel Hyper-Threading, 4 Kernen und 8 logischen Prozessoren höchstens 4 logische Prozessoren für die Netzwerk Verarbeitung.  

RSS verteilt eingehende Netzwerk-e/a-Pakete auf logische Prozessoren, sodass Pakete, die derselben TCP-Verbindung angehören, auf demselben logischen Prozessor verarbeitet werden, wodurch die Reihenfolge beibehalten wird. 

Außerdem führt RSS einen Lastenausgleich für UDP-Unicast-und Multicast-Datenverkehr durch und leitet Verwandte Flows \(, die durch das hashten der Quell-und Zieladressen\) auf denselben logischen Prozessor festgelegt werden, wobei die Reihenfolge verwandter Ankünfte beibehalten wird. Dies trägt zur Verbesserung der Skalierbarkeit und Leistung für Empfangs intensive Szenarien für Server bei, die weniger Netzwerkadapter aufweisen als berechtigte logische Prozessoren. 

#### <a name="configuring-rss"></a>Konfigurieren von RSS

In Windows Server 2016 können Sie RSS mithilfe von Windows PowerShell-Cmdlets und RSS-Profilen konfigurieren. 

Sie können RSS-Profile mithilfe des Parameters **– profile** des Windows PowerShell-Cmdlets **Set-netadapterrss** definieren.

**Windows PowerShell-Befehle für die RSS-Konfiguration**

Mit den folgenden Cmdlets können Sie die RSS-Parameter pro Netzwerkadapter anzeigen und ändern.
  
>[!NOTE]
>Eine ausführliche Befehlsreferenz zu den einzelnen Cmdlets, einschließlich Syntax und Parametern, finden Sie auf den folgenden Links. Außerdem können Sie den Cmdlet-Namen an **Get-Help** an der Windows PowerShell-Eingabeaufforderung übergeben, um ausführliche Informationen zu den einzelnen Befehlen zu erhalten.  

- [Deaktivieren Sie-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Disable-NetAdapterRss). Mit diesem Befehl wird RSS auf dem von Ihnen angegebenen Netzwerkadapter deaktiviert.

- [Enable-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterRss). Mit diesem Befehl wird RSS auf dem Netzwerkadapter aktiviert, den Sie angeben.
  
- [Get-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Get-NetAdapterRss). Dieser Befehl ruft die RSS-Eigenschaften des angegebenen Netzwerkadapters ab.
  
- [Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss). Mit diesem Befehl werden die RSS-Eigenschaften für den von Ihnen angegebenen Netzwerkadapter festgelegt.  

#### <a name="rss-profiles"></a>RSS-profile

Sie können den **– profile** -Parameter des Cmdlets Set-netadapterrss verwenden, um anzugeben, welche logischen Prozessoren welchem Netzwerkadapter zugewiesen sind. Für diesen Parameter sind folgende Werte verfügbar:

- **Am nächsten**. Logische Prozessor Zahlen, die sich in der Nähe des Basis-RSS-Prozessors des Netzwerkadapters befinden, werden bevorzugt Mit diesem Profil kann das Betriebssystem logische Prozessoren basierend auf der Auslastung dynamisch neu ausgleichen.
  
- **Closeststatic**. Logische Prozessor Zahlen in der Nähe des Basis-RSS-Prozessors des Netzwerkadapters werden bevorzugt. Bei diesem Profil werden logische Prozessoren vom Betriebssystem nicht dynamisch basierend auf der Auslastung neu ausgeglichen.
  
- **NUMA**. Logische Prozessor Zahlen werden im Allgemeinen auf verschiedenen NUMA-Knoten ausgewählt, um die Last zu verteilen. Mit diesem Profil kann das Betriebssystem logische Prozessoren basierend auf der Auslastung dynamisch neu ausgleichen.
  
- **Numastatic**. Dies ist das **Standardprofil**. Logische Prozessor Zahlen werden im Allgemeinen auf verschiedenen NUMA-Knoten ausgewählt, um die Last zu verteilen. Bei diesem Profil werden logische Prozessoren vom Betriebssystem nicht dynamisch basierend auf der Auslastung neu ausgeglichen.

- **Konservativ**. RSS verwendet so wenige Prozessoren wie möglich, um die Last zu bewältigen. Mit dieser Option wird die Anzahl der Interrupts reduziert.

Abhängig vom Szenario und den workloadmerkmalen können Sie auch andere Parameter des Windows PowerShell-Cmdlets " **Set-netadapterrss** " verwenden, um Folgendes anzugeben:

- Pro Netzwerkadapter: wie viele logische Prozessoren können für RSS verwendet werden.
- Der Anfangs Offset für den Bereich der logischen Prozessoren.
- Der Knoten, von dem aus der Netzwerkadapter Speicher belegt.

Im folgenden sind die zusätzlichen **Set-netadapterrss** -Parameter aufgeführt, die Sie zum Konfigurieren von RSS verwenden können:

>[!NOTE]
>In der Beispiel Syntax für jeden Parameter unten wird der Netzwerkadapter Name **Ethernet** als Beispiel Wert für den Parameter " **– Name** " des Befehls " **Set-netadapterrss** " verwendet. Wenn Sie das Cmdlet ausführen, stellen Sie sicher, dass der von Ihnen verwendete Netzwerkadapter Name für Ihre Umgebung geeignet ist.

- **\* maxprocessor**: legt die maximale Anzahl der zu verwendenden RSS-Prozessoren fest. Dadurch wird sichergestellt, dass der Anwendungs Datenverkehr an eine maximale Anzahl von Prozessoren an einer bestimmten Schnittstelle gebunden ist. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessors <value>`

- **\* baseprocessorgroup**: legt die Basis Prozessor Gruppe eines NUMA-Knotens fest. Dies wirkt sich auf das von RSS verwendete Prozessor Array aus. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorGroup <value>`
  
- **\* maxprocessorgroup**: legt die maximale Prozessor Gruppe eines NUMA-Knotens fest. Dies wirkt sich auf das von RSS verwendete Prozessor Array aus. Durch Festlegen dieser Einstellung wird eine maximale Prozessor Gruppe so eingeschränkt, dass der Lastenausgleich innerhalb einer k-Gruppe ausgerichtet wird. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –MaxProcessorGroup <value>`

- **\* baseprocessornumber**: legt die Basis Prozessornummer eines NUMA-Knotens fest. Dies wirkt sich auf das von RSS verwendete Prozessor Array aus. Dies ermöglicht die Partitionierung von Prozessoren über Netzwerkadapter hinweg. Dies ist der erste logische Prozessor in dem Bereich von RSS-Prozessoren, der den einzelnen Adaptern zugewiesen wird. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –BaseProcessorNumber <Byte Value>`

- **\* numanode**: der NUMA-Knoten, von dem jeder Netzwerkadapter Arbeitsspeicher zuordnen kann. Dies kann sich innerhalb einer k-Gruppe oder aus unterschiedlichen k-Gruppen befinden. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –NumaNodeID <value>`

- **\*-anzahlungswarteschlangen**: Wenn Ihre logischen Prozessoren für den Empfangs Datenverkehr zu wenig ausgelastet sind \(z. b. wie im Task-Manager\)angezeigt, können Sie versuchen, die Anzahl der RSS-Warteschlangen standardmäßig auf den maximalen Wert zu erhöhen, der vom Netzwerkadapter unterstützt wird. Der Netzwerkadapter kann möglicherweise Optionen zum Ändern der Anzahl der RSS-Warteschlangen als Teil des Treibers haben. Beispielsyntax:

     `Set-NetAdapterRss –Name “Ethernet” –NumberOfReceiveQueues <value>`

Weitere Informationen erhalten Sie, indem Sie auf den folgenden Link klicken, um [skalierbare Netzwerke herunterzuladen: vermeiden des Empfangs Verarbeitungs Engpass – Einführung in RSS](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/NDIS_RSS.doc) im Word-Format.
  
#### <a name="understanding-rss-performance"></a>Verständnis der RSS-Leistung

Zum Optimieren von RSS müssen die Konfiguration und die Lasten Ausgleichs Logik verstanden werden. Wenn Sie überprüfen möchten, ob die RSS-Einstellungen wirksam sind, können Sie die Ausgabe überprüfen, wenn Sie das Windows PowerShell-Cmdlet **Get-netadapterrss** ausführen. Im folgenden finden Sie eine Beispielausgabe dieses Cmdlets.
  
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

Neben den festgelegten Parametern ist der wichtigste Aspekt der Ausgabe die Ausgabe der dereferenzierungstabelle. In der dereferenzierungstabelle werden die Hash Tabellen-Bucket angezeigt, mit denen eingehender Datenverkehr verteilt wird. In diesem Beispiel legt die n:c-Notation das NUMA K-Group: CPU-Index paar fest, das verwendet wird, um eingehenden Datenverkehr weiterzuleiten. Es werden genau 2 eindeutige Einträge (0:0 und 0:4) angezeigt, die die k-Gruppe 0/CPU0 bzw. k-Gruppe 0/CPU 4 darstellen.

Es ist nur eine k-Gruppe für dieses System (k-Group 0) und ein n-dereferenzierungstabelleneintrag (Where n < = 128) vorhanden. Da die Anzahl der Empfangs Warteschlangen auf 2 festgelegt ist, werden nur 2 Prozessoren (0:0, 0:4) ausgewählt, auch wenn die maximale Anzahl der Prozessoren auf 8 festgelegt ist. Tatsächlich ist die dereferenzierungstabelle ein Hashwert für eingehenden Datenverkehr, sodass nur 2 CPUs aus den verfügbaren 8 verwendet werden.

Um die CPUs vollständig nutzen zu können, muss die Anzahl der RSS-Empfangs Warteschlangen größer oder gleich der maximalen Anzahl von Prozessoren sein. Im vorherigen Beispiel sollte die Empfangs Warteschlange auf 8 oder höher festgelegt werden.

#### <a name="nic-teaming-and-rss"></a>Nic-Team Vorgang und RSS

RSS kann auf einem Netzwerkadapter aktiviert werden, der mithilfe des NIC-Team Vorgangs mit einer anderen Netzwerkschnittstellenkarte verbunden ist. In diesem Szenario kann nur der zugrunde liegende physische Netzwerkadapter für die Verwendung von RSS konfiguriert werden. Ein Benutzer kann keine RSS-Cmdlets auf dem kombinierten Netzwerkadapter festlegen.
  
###  <a name="bkmk_rsc"></a>Empfangen von Segmenten zusammenfügen (RSC)

Empfangen von Segmentieren von Segmenten \(RSC\) unterstützt die Leistung, indem die Anzahl der IP-Header reduziert wird, die für eine bestimmte Menge empfangener Daten verarbeitet werden. Sie sollte verwendet werden, um die Leistung der empfangenen Daten zu skalieren, indem Sie \(gruppieren oder\) kleineren Paketen in größere Einheiten gruppieren.

Diese Vorgehensweise kann sich auf die Latenz mit Vorteilen auswirken, die größtenteils in Durchsatz Steigerungen auftreten. RSC wird empfohlen, um den Durchsatz für empfangene hohe Arbeits Auslastungen zu erhöhen. Sie sollten Netzwerkadapter bereitstellen, die RSC unterstützen. 

Stellen Sie sicher, dass RSC auf diesen Netzwerkadaptern \(Dies ist die Standardeinstellung\)ist, es sei denn, Sie verfügen über bestimmte Arbeits Auslastungen \(z. b. die Netzwerk\) geringe Latenz und niedriger Durchsatz.

#### <a name="understanding-rsc-diagnostics"></a>Erläuterungen zu RSC-Diagnosen

Sie können RSC mithilfe der Windows PowerShell-Cmdlets " **Get-netadapterrsc** " und " **Get-netadapterstatistics**" diagnostizieren.

Im folgenden finden Sie eine Beispielausgabe beim Ausführen des Cmdlets Get-netadapterrsc.

```  

PS C:\Users\Administrator> Get-NetAdapterRsc  
  
Name                       IPv4Enabled  IPv6Enabled  IPv4Operational IPv6Operational               IPv4FailureReason              IPv6Failure  
                                            Reason  
----                           -----------  -----------  --------------- --------------- ----------------- ------------  
Ethernet                       True         False        True            False                  NoFailure       NicProperties  
  
```  

Das **Get** -Cmdlet zeigt, ob RSC in der Schnittstelle aktiviert ist und ob TCP sich in einem Betriebsstatus befinden kann. Die Fehlerursache enthält Details zum Fehler beim Aktivieren von RSC für diese Schnittstelle.

Im vorherigen Szenario wird IPv4 RSC in der-Schnittstelle unterstützt und funktioniert. Zum besseren Verständnis von Diagnose Fehlern können die zusammengefügten Bytes oder Ausnahmen angezeigt werden. Dies gibt Aufschluss über die zusammen fügenden Probleme.

Im folgenden finden Sie eine Beispielausgabe beim Ausführen des Cmdlets Get-netadapterstatistics.

```  
PS C:\Users\Administrator> $x = Get-NetAdapterStatistics “myAdapter”   
PS C:\Users\Administrator> $x.rscstatistics  
  
CoalescedBytes       : 0  
CoalescedPackets     : 0  
CoalescingEvents     : 0  
CoalescingExceptions : 0  
  
```  

#### <a name="rsc-and-virtualization"></a>RSC und Virtualisierung

RSC wird nur auf dem physischen Host unterstützt, wenn der Host Netzwerkadapter nicht an den virtuellen Hyper-V-Switch gebunden ist. RSC wird vom Betriebssystem deaktiviert, wenn der Host an den virtuellen Hyper-V-Switch gebunden ist. Außerdem profitieren virtuelle Computer nicht von RSC, da virtuelle Netzwerkadapter RSC nicht unterstützen.

RSC kann für einen virtuellen Computer aktiviert werden, wenn die Eingabe-/ausgabevirtualisierung mit einem einzelnen Stamm \(SR-IOV\) aktiviert ist. In diesem Fall unterstützen virtuelle Funktionen RSC-Fähigkeiten. Daher erhalten virtuelle Computer auch den Vorteil RSC.

##  <a name="bkmk_resources"></a>Netzwerk Adapter Ressourcen

Einige Netzwerkadapter verwalten ihre Ressourcen aktiv, um eine optimale Leistung zu erzielen. Mit mehreren Netzwerkadaptern können Sie Ressourcen manuell konfigurieren, indem Sie die Registerkarte **Erweiterte Netzwerke** für den Adapter verwenden. Bei solchen Adaptern können Sie die Werte für eine Reihe von Parametern festlegen, einschließlich der Anzahl der Empfangs Puffer und Sendepuffer.

Das Konfigurieren von Netzwerkadapter Ressourcen wird durch die Verwendung der folgenden Windows PowerShell-Cmdlets vereinfacht.

- [Get-netadapteradvancedproperty](https://docs.microsoft.com/powershell/module/netadapter/Get-NetAdapterAdvancedProperty)

- [Set-netadapteradvancedproperty](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterAdvancedProperty)

- [Enable-netadapter](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapte)

- [Enable-netadapterbinding](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterBinding)

- [Enable-netadapterchecksumuloffload](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterChecksumOffload)

- [Enable-netadapteripdepcoffload](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterChecksumOffload)

- [Enable-netadapterlso](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterLso)

- [Enable-netadapterpowermanagement](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterPowerManagement)

- [Enable-netadapterqos](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterQos)

- [Enable-netadapterrdma](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterRDMA)

- [Enable-netadaptersriov](https://docs.microsoft.com/powershell/module/netadapter/Enable-NetAdapterSriov)

Weitere Informationen finden Sie unter [Netzwerk Adapter-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/netadapter).

Links zu allen Themen in diesem Handbuch finden Sie unter [Network Subsystem Performance Tuning](net-sub-performance-top.md).
