---
title: Remotezugriff auf den direkten Speicher (RDMA) und Switch Embedded Teaming (SET)
description: Dieses Thema enthält Informationen zum Konfigurieren von RDMA-Schnittstellen (Remote Direct Memory Access) mit Hyper-V in Windows Server 2016 sowie Informationen zum Switch Embedded Teaming (Set).
manager: brianlic
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 68c35b64-4d24-42be-90c9-184f2b5f19be
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b39cac842f115a1828c666eec52f17f80971510c
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322712"
---
# <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-set"></a>Remote Zugriff auf den direkten Speicher \(RDMA-\) und \(Set-Switch Embedded Teaming\)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Thema enthält Informationen zum Konfigurieren des Remote Zugriffs auf den direkten Speicher \(RDMA-\) Schnittstellen mit Hyper-V in Windows Server 2016 sowie Informationen zum Switch Embedded Teaming \(Set\).  

> [!NOTE]
> Zusätzlich zu diesem Thema ist der Inhalt des folgenden Switch Embedded-Teaming verfügbar. 
> - TechNet-Katalog Download: [Windows Server 2016 NIC und Switch Embedded Teaming-Benutzerhandbuch](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)

## <a name="bkmk_rdma"></a>Konfigurieren von RDMA-Schnittstellen mit Hyper-V  

In Windows Server 2012 R2 kann die Verwendung von RDMA und Hyper-V auf demselben Computer wie die Netzwerkadapter, die RDMA-Dienste bereitstellen, nicht an einen virtuellen Hyper-V-Switch gebunden werden. Dadurch erhöht sich die Anzahl der physischen Netzwerkadapter, die auf dem Hyper-V-Host installiert werden müssen.

>[!TIP]
>In Editionen von Windows Server vor Windows Server 2016 ist es nicht möglich, RDMA auf Netzwerkadaptern zu konfigurieren, die an ein NIC-Team oder einen virtuellen Hyper-V-Switch gebunden sind. In Windows Server 2016 können Sie RDMA auf Netzwerkadaptern aktivieren, die an einen virtuellen Hyper-V-Switch mit oder ohne festgelegt sind.

In Windows Server 2016 können Sie bei Verwendung von RDMA mit oder ohne Festlegung weniger Netzwerkadapter verwenden.

Die folgende Abbildung veranschaulicht die Softwarearchitektur Änderungen zwischen Windows Server 2012 R2 und Windows Server 2016.

![Änderungen an der Architektur](../media/RDMA-and-SET/rdma_over.jpg)

Die folgenden Abschnitte enthalten Anweisungen zur Verwendung von Windows PowerShell-Befehlen zum Aktivieren von Data Center Bridging (DCB), zum Erstellen eines virtuellen Hyper-v-Switches mit einer virtuellen RDMA-NIC \(vNIC-\)und zum Erstellen eines virtuellen Hyper-v-Switches mit Set-und RDMA-vNICs.

### <a name="enable-data-center-bridging-dcb"></a>Aktivieren von Data Center Bridging \(DCB\)

Vor der Verwendung von RDMA-über konvergiertem Ethernet \(ROCE\) RDMA-Version muss DCB aktiviert werden.  Obwohl es für den Internet weiten RDMA-Protokoll \(IWarp\)-Netzwerken nicht erforderlich ist, wurde durch Tests festgestellt, dass alle Ethernet-basierten RDMA-Technologien mit DCB besser funktionieren. Aus diesem Grund sollten Sie DCB auch für IWarp RDMA-bereit Stellungen verwenden.

Die folgenden Windows PowerShell-Beispiel Befehle veranschaulichen, wie Sie DCB für SMB Direct aktivieren und konfigurieren.

Aktivieren von DCB

    Install-WindowsFeature Data-Center-Bridging

Legen Sie eine Richtlinie für SMB-Direct fest:

    New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3

Aktivieren der Fluss Steuerung für SMB:

    Enable-NetQosFlowControl  -Priority 3

Stellen Sie sicher, dass die Fluss Steuerung für anderen Datenverkehr deaktiviert ist:

    Disable-NetQosFlowControl  -Priority 0,1,2,4,5,6,7

Anwenden der Richtlinie auf die Ziel Adapter:

    Enable-NetAdapterQos  -Name "SLOT 2"

Verschaffen Sie sich eine minimale Bandbreite von SMB Direct:

`New-NetQosTrafficClass "SMB"  -Priority 3  -BandwidthPercentage 30  -Algorithm ETS`  

Wenn Sie einen Kernel Debugger im System installiert haben, müssen Sie den Debugger so konfigurieren, dass QoS durch Ausführen des folgenden Befehls festgelegt werden kann.

Überschreiben des Debuggers: standardmäßig blockiert der Debugger NetQoS:
 
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force

### <a name="create-a-hyper-v-virtual-switch-with-an-rdma-vnic"></a>Erstellen eines virtuellen Hyper-V-Switches mit einer RDMA-vNIC

Wenn für die Bereitstellung nicht festgelegt ist, können Sie die folgenden Windows PowerShell-Befehle verwenden, um einen virtuellen Hyper-V-Switch mit einer RDMA-vNIC zu erstellen.

> [!NOTE]
> Die Verwendung von Set Teams mit RDMA-fähigen physischen NICs bietet weitere RDMA-Ressourcen, die von den vNICs genutzt werden können.

    New-VMSwitch -Name RDMAswitch -NetAdapterName "SLOT 2"

Fügen Sie Host-vNICs hinzu, und machen Sie Sie RDMA-fähig:

    Add-VMNetworkAdapter -SwitchName RDMAswitch -Name SMB_1
    Enable-NetAdapterRDMA "vEthernet (SMB_1)" "SLOT 2"

Überprüfen Sie RDMA-Funktionen:

    Get-NetAdapterRdma

###  <a name="bkmk_set-rdma"></a>Erstellen eines virtuellen Hyper-V-Switches mit Set-und RDMA-vNICs

Zum Verwenden von RDMA-Unterstützung auf virtuellen Hyper-v-Host Netzwerkadaptern \(vNICs\) auf einem virtuellen Hyper-v-Switch, der RDMA-Teaming unterstützt, können Sie diese Windows PowerShell-Beispiel Befehle verwenden.

    New-VMSwitch -Name SETswitch -NetAdapterName "SLOT 2","SLOT 3" -EnableEmbeddedTeaming $true

Host-vNICs hinzufügen:

    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_1 -managementOS
    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_2 -managementOS

Viele Switches übergeben keine Informationen zur Datenverkehrs Klasse für nicht markierten VLAN-Datenverkehr. Stellen Sie daher sicher, dass sich die Host Adapter für RDMA auf VLANs befinden. In diesem Beispiel werden die beiden virtuellen SMB_ *-Host Adapter VLAN 42 zugewiesen.
    
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_1  -IsolationMode VLAN -DefaultIsolationID 42
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_2  -IsolationMode VLAN -DefaultIsolationID 42
    

Aktivieren Sie RDMA auf Host-vNICs:

    Enable-NetAdapterRDMA "vEthernet (SMB_1)","vEthernet (SMB_2)" "SLOT 2", "SLOT 3"

RDMA-Funktionen überprüfen; Stellen Sie sicher, dass die Funktionen ungleich NULL sind:

    Get-NetAdapterRdma | fl *


## <a name="switch-embedded-teaming-set"></a>Eingebetteten Teaming wechseln (Set)  

Dieser Abschnitt bietet eine Übersicht über Switch Embedded Teaming (Set) in Windows Server 2016 und enthält die folgenden Abschnitte.

- [Übersicht festlegen](#bkmk_over)

- [Festlegen der Verfügbarkeit](#bkmk_avail)

- [Unterstützte und nicht unterstützte NICs für Set](#bkmk_nics)

- [Festlegen der Kompatibilität mit Windows Server-Netzwerktechnologien](#bkmk_compat)

- [Festlegen von Modi und Einstellungen](#bkmk_modes)

- [Set-und Virtual Machine-Warteschlangen (vmqs)](#bkmk_vmq)

- [Set und Hyper-v-Netzwerkvirtualisierung (HNV)](#bkmk_hnv)

- [Festlegen und Livemigration](#bkmk_live)

- [Mac-Adress Verwendung für übertragene Pakete](#bkmk_mac)

- [Verwalten eines Set-Teams](#bkmk_manage)

## <a name="bkmk_over"></a>Übersicht festlegen

Set ist eine Alternative NIC-Team Vorgangs Lösung, die Sie in Umgebungen mit Hyper-V und dem Software-Defined Networking \(Sdn\) Stack in Windows Server 2016 verwenden können. Set integriert einige NIC-Team Vorgangs Funktionen in den virtuellen Hyper-V-Switch.

Mit Set können Sie zwischen einem und acht physischen Ethernet-Netzwerkadaptern in einem oder mehreren softwarebasierten virtuellen Netzwerkadaptern gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.

Alle Netzwerkadapter für Mitglieder müssen auf demselben physischen Hyper-V-Host installiert sein, damit Sie in einem Team platziert werden können.

> [!NOTE]
> Die Verwendung von Set wird nur in einem virtuellen Hyper-V-Switch in Windows Server 2016 unterstützt. In Windows Server 2012 R2 kann Set nicht bereitgestellt werden.

Sie können Ihre Team eigenen NICs mit dem gleichen physischen Switch oder mit unterschiedlichen physischen Switches verbinden. Wenn Sie NICs mit verschiedenen Switches verbinden, müssen sich beide Switches im gleichen Subnetz befinden.

In der folgenden Abbildung wird die festgelegte Architektur dargestellt.

![Architektur festlegen](../media/RDMA-and-SET/set_architecture.jpg)

Da Set in den virtuellen Hyper-V-Switch integriert ist, können Sie Set nicht innerhalb eines virtuellen Computers (Virtual Machine, VM) verwenden. Sie können jedoch den NIC-Team Vorgang innerhalb von VMS verwenden.

Weitere Informationen finden Sie unter NIC-Team Vorgang [in Virtual Machines (VMS)](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nict-vms).

Außerdem werden von der Set-Architektur keine Team Schnittstellen verfügbar gemacht. Stattdessen müssen Sie virtuelle Hyper-V-Switchports konfigurieren.

## <a name="bkmk_avail"></a>Festlegen der Verfügbarkeit

Set ist in allen Versionen von Windows Server 2016 verfügbar, die Hyper-V und den Sdn-Stapel enthalten. Außerdem können Sie Windows PowerShell-Befehle und Remotedesktop Verbindungen verwenden, um die Gruppe von Remote Computern aus zu verwalten, auf denen ein Client Betriebssystem ausgeführt wird, auf dem die Tools unterstützt werden.

## <a name="bkmk_nics"></a>Unterstützte NICs für Set

Sie können eine beliebige Ethernet-NIC verwenden, die die Windows-Hardware Qualifizierung und das Logo \(WHQL\) Test in einem Set-Team in Windows Server 2016 übermittelt hat. Set erfordert, dass alle Netzwerkadapter, die Mitglieder eines Set-Teams sind, identisch sein müssen \(d. h., derselbe Hersteller, dasselbe Modell, dieselbe Firmware und dieser Treiber\). Legen Sie Unterstützung zwischen einem und acht Netzwerkadaptern in einem Team fest.
  
## <a name="bkmk_compat"></a>Festlegen der Kompatibilität mit Windows Server-Netzwerktechnologien

Set ist kompatibel mit den folgenden Netzwerktechnologien in Windows Server 2016.

- Datacenter Bridging \(DCB\)
  
- Hyper-V-Netzwerkvirtualisierung-NV-GRE und vxlan werden in Windows Server 2016 unterstützt.  
- Die Empfangs seitige Prüfsumme verlagert \(IPv4-, IPv6-und TCP-\). Diese werden unterstützt, wenn Sie von einem der Teammitglieder unterstützt werden.

- Remote Zugriff auf den direkten Speicher \(RDMA-\)

- Single-root-e/a-Virtualisierung \(SR-IOV\)

- Die Übertragungs seitige Prüfsumme verlagert \(IPv4-, IPv6-und TCP-\). Diese werden unterstützt, wenn alle Teammitglieder Sie unterstützen.

- Warteschlangen für virtuelle Computer \(VMQ-\)

- Virtuelle Empfangs seitige Skalierung \(RSS-\)

Set ist nicht kompatibel mit den folgenden Netzwerktechnologien in Windows Server 2016.

- 802.1 x-Authentifizierung. Das 802.1 x Extensible Authentication-Protokoll \(EAP-\) Pakete werden automatisch durch den virtuellen Hyper\-V-Switch in festgelegten Szenarien gelöscht.
 
- IPSec-Task Offload \(ipsecto\). Dies ist eine Legacy Technologie, die von den meisten Netzwerkadaptern nicht unterstützt wird und wo Sie vorhanden ist. Sie ist standardmäßig deaktiviert.

- Verwenden von QoS \(Pacer. exe\) auf Host-oder nativen Betriebssystemen. Diese QoS-Szenarien sind keine Hyper\-V-Szenarien, sodass sich die Technologien nicht überschneiden. Außerdem ist QoS verfügbar, aber nicht standardmäßig aktiviert. Sie müssen QoS absichtlich aktivieren.

- Empfangs seitige zusammen Fügung \(RSC\). RSC wird automatisch durch den virtuellen Hyper\-V-Switch deaktiviert.

- Empfangs seitige Skalierung \(RSS-\). Da Hyper-V die Warteschlangen für VMQ und vmmq verwendet, wird RSS immer deaktiviert, wenn Sie einen virtuellen Switch erstellen.

- TCP-Chimney-Abladung. Diese Technologie ist standardmäßig deaktiviert.

- QoS für virtuelle Computer \(VM-QoS-\). VM-QoS ist verfügbar, aber standardmäßig deaktiviert. Wenn Sie VM-QoS in einer festgelegten Umgebung konfigurieren, führen die QoS-Einstellungen zu unvorhersehbaren Ergebnissen.

## <a name="bkmk_modes"></a>Festlegen von Modi und Einstellungen

Anders als beim NIC-Team Vorgang können Sie einen Teamnamen nicht konfigurieren, wenn Sie ein Set-Team erstellen. Außerdem wird die Verwendung eines Standby-Adapters beim NIC-Team Vorgang unterstützt, wird jedoch in Set nicht unterstützt. Wenn Sie Set bereitstellen, sind alle Netzwerkadapter aktiv und keine im Standbymodus.

Ein weiterer wichtiger Unterschied zwischen dem NIC-Team Vorgang und der Festlegung besteht darin, dass der NIC-Team Vorgang die Auswahl von drei verschiedenen Team Vorgang-Modi ermöglicht, während Set unterstützt nur **Switch Independent** Mode Mit dem Schalter unabhängigen Modus sind die Schalter oder Switches, mit denen die Teammitglieder der Gruppe verbunden sind, nicht mit dem vorhanden sein des Set-Teams in Kenntnis, und es wird nicht festgelegt, wie Netzwerk Datenverkehr an Teammitglieder verteilt wird. stattdessen verteilt das Set-Team eingehende Netzwerke. Datenverkehr über die Gruppe der Teammitglieder.

Wenn Sie ein neues Set-Team erstellen, müssen Sie die folgenden Team Eigenschaften konfigurieren.

- Mitglieds Adapter

- Lasten Ausgleichs Modus

### <a name="member-adapters"></a>Mitglieds Adapter

Wenn Sie ein Set-Team erstellen, müssen Sie bis zu acht identische Netzwerkadapter angeben, die an den virtuellen Hyper-V-Switch als festgelegte Teammitglieds Adapter gebunden sind.

### <a name="load-balancing-mode"></a>Lasten Ausgleichs Modus

Die Optionen für den Verteilungsmodus "Team Lastenausgleich festlegen" sind **Hyper-V-Port** und **dynamisch**.

**Hyper-V-Port**

VMS sind mit einem Port auf dem virtuellen Hyper-V-Switch verbunden. Bei Verwendung des Hyper-v-Port Modus für Set-Teams werden der virtuelle Hyper-v-Switchport und die zugehörige Mac-Adresse verwendet, um den Netzwerk Datenverkehr zwischen den Teammitgliedern festzulegen.

> [!NOTE]
> Wenn Sie Set in Verbindung mit Packet Direct verwenden, ist der Team Vorgangs Modus **unabhängig** , und der **Hyper-V-Port** des Lasten Ausgleichs Modus ist erforderlich.

Da der angrenzende Switch immer eine bestimmte MAC-Adresse an einem bestimmten Port sieht, verteilt der Switch die Eingangs Last (den Datenverkehr vom Switch an den Host) an den Port, auf dem sich die Mac-Adresse befindet. Dies ist besonders nützlich, wenn virtuelle Computer Warteschlangen (vmqs) verwendet werden, da eine Warteschlange auf der jeweiligen NIC platziert werden kann, an der der Datenverkehr erwartet wird.

Wenn der Host jedoch nur über wenige VMS verfügt, ist dieser Modus möglicherweise nicht genau genug, um eine ausgewogene Verteilung zu erzielen. In diesem Modus wird außerdem immer eine einzelne VM (d. h. der Datenverkehr von einem einzelnen Switchport) auf die Bandbreite beschränkt, die auf einer einzelnen Schnittstelle verfügbar ist.

**Schem**

Dieser Lasten Ausgleichs Modus bietet die folgenden Vorteile:

- Ausgehende Lasten werden basierend auf einem Hash der TCP-Ports und IP-Adressen verteilt.  Der dynamische Modus gleicht Ladevorgänge auch in Echtzeit neu aus, sodass ein angegebener ausgehender Flow zwischen den festgelegten Teammitgliedern hin und her verschoben werden kann.

- Eingehende Lasten werden auf die gleiche Weise verteilt wie der Hyper-V-portmodus.

Die ausgehenden Lasten in diesem Modus werden basierend auf dem Konzept der flowlets dynamisch ausgeglichen. Ebenso wie bei der menschlichen Sprache an den Enden von Wörtern und Sätzen natürliche Unterbrechungen auftreten, sind TCP-Flows (TCP-Kommunikationsstreams) natürlich auch Unterbrechungen aufgetreten. Der Teil eines TCP-Flows zwischen zwei Unterbrechungen wird als flowlet bezeichnet.

Wenn der Algorithmus für den dynamischen Modus erkennt, dass eine flowlet-Grenze gefunden wurde (z. b. wenn im TCP-Datenfluss eine Unterbrechung der Länge aufgetreten ist), gleicht der Algorithmus den Flow automatisch an ein anderes Teammitglied aus, falls dies erforderlich ist.  In einigen seltenen Fällen kann es vorkommen, dass der Algorithmus regelmäßig auch Flows umschließt, die keine flowlets enthalten. Aus diesem Grund kann sich die Affinität zwischen TCP-Fluss und Teammitglied jederzeit ändern, da der dynamische Ausgleichs Algorithmus funktioniert, um die Arbeitsauslastung der Teammitglieder auszugleichen.

## <a name="bkmk_vmq"></a>Set-und Virtual Machine-Warteschlangen (vmqs)

VMQ und legen eine gute Zusammenarbeit fest. Sie sollten VMQ immer dann aktivieren, wenn Sie Hyper-V verwenden und festlegen.

> [!NOTE]
> Set zeigt immer die Gesamtzahl der Warteschlangen an, die für alle festgelegten Teammitglieder verfügbar sind. Beim NIC-Team Vorgang wird dies als Sum-of-Queues-Modus bezeichnet.

Die meisten Netzwerkadapter verfügen über Warteschlangen, die für die Empfangs seitige Skalierung \(RSS\) oder VMQ verwendet werden können, aber nicht beide gleichzeitig.
  
Einige VMQ-Einstellungen scheinen Einstellungen für RSS-Warteschlangen zu sein, sind aber tatsächlich Einstellungen in den generischen Warteschlangen, die sowohl von RSS als auch von VMQ abhängig davon verwendet werden, welches Feature aktuell verwendet wird. Jede NIC verfügt in ihren erweiterten Eigenschaften über Werte für `*RssBaseProcNumber` und `*MaxRssProcessors`.

Im folgenden finden Sie einige VMQ-Einstellungen, die eine bessere Systemleistung bereitstellen.

- Im Idealfall sollte für jede NIC die `*RssBaseProcNumber` auf eine gerade Zahl größer oder gleich zwei (2) festgelegt werden. Dies liegt daran, dass der erste physische Prozessor, Core 0 \(logischen Prozessoren 0 und 1\), in der Regel den größten Teil der Systemverarbeitung übernimmt, sodass die Netzwerk Verarbeitung von diesem physischen Prozessor entfernt werden sollte. 

>[!NOTE]
>Einige Computerarchitekturen haben nicht zwei logische Prozessoren pro physischem Prozessor, sodass der Basis Prozessor für solche Computer größer oder gleich 1 sein sollte. Nehmen Sie im Zweifelsfall an, dass der Host einen 2 logischen Prozessor pro physischer Prozessorarchitektur verwendet.

- Die Prozessoren der Teammitglieder sollten so groß sein, dass Sie praktisch und nicht überlappen. Beispielsweise können Sie in einem 4-Kern-Host \(8 logische Prozessoren\) mit einem Team von 2 10 Gbit/s-NICs festlegen, dass der erste Wert den Basis Prozessor 2 verwendet und vier Kerne verwendet werden sollen. der zweite Wert wird so festgelegt, dass er den Basis Prozessor 6 verwendet und 2 Kerne verwendet.

## <a name="bkmk_hnv"></a>Set und Hyper-v-Netzwerkvirtualisierung \(HNV\)

Der Satz ist vollständig kompatibel mit der Hyper-V-Netzwerkvirtualisierung in Windows Server 2016. Das HNV-Verwaltungssystem stellt Informationen für den Set-Treiber bereit, mit dem die Verteilung des Netzwerk Datenverkehrs auf eine Weise ermöglicht wird, die für den HNV-Datenverkehr optimiert ist.
  
## <a name="bkmk_live"></a>Festlegen und Livemigration

Livemigration wird in Windows Server 2016 unterstützt.

## <a name="bkmk_mac"></a>Mac-Adress Verwendung für übertragene Pakete

Wenn Sie ein Set-Team mit dynamischer Lastenverteilung konfigurieren, werden die Pakete aus einer einzelnen Quelle \(z. b. eine einzelne VM-\) gleichzeitig auf mehrere Teammitglieder verteilt. 

Um zu verhindern, dass die Switches verwirrt werden, und um Mac-Fluktuation-Alarme zu verhindern, wird durch Set die MAC-Quelladresse durch eine andere Mac-Adresse in den Frames ersetzt, die auf andere Teammitglieder als das affininitisierte Teammitglied übertragen werden. Aus diesem Grund verwendet jedes Teammitglied eine andere Mac-Adresse, und Mac-Adresskonflikte werden verhindert, wenn ein Fehler auftritt.

Wenn ein Fehler auf der primären NIC erkannt wird, beginnt die festgelegte Team Vorgang-Software mit der Mac-Adresse des virtuellen Computers auf dem Teammitglied, das als temporäres affininitialisiertes Teammitglied fungieren soll \(d. h. dem, das nun als Schnittstelle des virtuellen Computers\)angezeigt wird.

Diese Änderung gilt nur für Datenverkehr, der über die zugehörige Mac-Adresse des virtuellen Computers mit der eigenen Mac-Adresse des virtuellen Computers an die zugehörige Mac-Adresse der VM gesendet wird. Der andere Datenverkehr wird weiterhin mit der Quell-MAC-Adresse gesendet, die vor dem Auftreten des Fehlers verwendet wurde.

Im folgenden finden Sie Listen, die das Austausch Verhalten von Mac-Adressen festlegen, basierend auf der Konfiguration des Teams:

- Im Wechsel unabhängigen Modus mit der Hyper-V-Port Verteilung

    - Jeder VMSwitch-Port ist einem Teammitglied zugeordnet.
  
    - Jedes Paket wird an das Teammitglied gesendet, dem der Port zugeordnet ist.  
  
    - Keine Quell-Mac-Ersetzung durchgeführt  
  
- Im Wechsel unabhängigen Modus mit dynamischer Verteilung
  
    - Jeder VMSwitch-Port ist einem Teammitglied zugeordnet.  
  
    - Alle ARP/NS-Pakete werden an das Teammitglied gesendet, dem der Port zugeordnet ist.  
  
    - Für Pakete, die für das Teammitglied gesendet werden, dem das affininitisierte Teammitglied angehört, ist keine Quell-MAC-Adressen Ersetzung abgeschlossen  
  
    - Für Pakete, die für ein anderes Teammitglied als das affininitisierte Teammitglied gesendet werden, wird die Mac-Adresse der Quelle abgeschlossen.  
  
## <a name="bkmk_manage"></a>Verwalten eines Set-Teams

Es wird empfohlen, dass Sie System Center Virtual Machine Manager \(VMM-\) verwenden, um Set-Teams zu verwalten. Sie können jedoch auch Windows PowerShell verwenden, um die Gruppe zu verwalten. In den folgenden Abschnitten werden die Windows PowerShell-Befehle bereitgestellt, die Sie zum Verwalten von Set verwenden können.

Informationen zum Erstellen eines Set-Teams mithilfe von VMM finden Sie im Abschnitt "Einrichten eines logischen Switches" in der System Center VMM-Bibliothek unter [Erstellen logischer Switches](https://docs.microsoft.com/system-center/vmm/network-switch).
  
### <a name="create-a-set-team"></a>Erstellen eines Set-Teams

Sie müssen ein Set-Team erstellen, wenn Sie den virtuellen Hyper-V-Switch mit dem Windows PowerShell **-Befehl New-VMSwitch** erstellen.

Wenn Sie den virtuellen Hyper-V-Switch erstellen, müssen Sie den neuen Parameter " **enableembeddedteaming** " in die Befehlssyntax einschließen. Im folgenden Beispiel wird ein Hyper-V-Switch namens **teamedvswitch** mit eingebettetem Team Vorgang und zwei anfängliche Teammitglieder erstellt.
  
```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2" -EnableEmbeddedTeaming $true  
```  
  
Der **enableembeddedteaming** -Parameter wird von Windows PowerShell angenommen, wenn das Argument für **netadaptername** ein Array von NICs anstelle einer einzelnen NIC ist. Daher können Sie den vorherigen Befehl folgendermaßen überarbeiten.

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"  
```  

Wenn Sie einen Set-fähigen Switch mit einem einzelnen Teammitglied erstellen möchten, damit Sie ein Teammitglied zu einem späteren Zeitpunkt hinzufügen können, müssen Sie den enableembeddteaming-Parameter verwenden.

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1" -EnableEmbeddedTeaming $true  
```  

### <a name="adding-or-removing-a-set-team-member"></a>Hinzufügen oder Entfernen eines Set-Teammitglieds

Der Befehl **Set-vmswitchteam** schließt die Option **netadaptername** ein. Um die Teammitglieder in einem Set-Team zu ändern, geben Sie nach der Option **netadaptername** die gewünschte Liste der Teammitglieder ein. Wenn **teamedvswitch** ursprünglich mit NIC 1 und NIC 2 erstellt wurde, wird mit dem folgenden Beispiel Befehl das Teammitglied "NIC 2" gelöscht und das neue Set-Teammitglied "Nic 3" hinzugefügt.
  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 3"  
```  

### <a name="removing-a-set-team"></a>Entfernen eines Set-Teams

Sie können ein Set-Team nur entfernen, indem Sie den virtuellen Hyper-V-Switch entfernen, der das Set-Team enthält.  Verwenden Sie das Thema [Remove-VMSwitch](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/remove-vmswitch) , um zu erfahren, wie Sie den virtuellen Hyper-V-Switch entfernen. Im folgenden Beispiel wird ein virtueller Switch mit dem Namen **setvswitch**entfernt.

```  
Remove-VMSwitch "SETvSwitch"  
```  

### <a name="changing-the-load-distribution-algorithm-for-a-set-team"></a>Ändern des Auslastungs Verteilungs Algorithmus für ein Set-Team

Das **Set-vmswitchteam-** Cmdlet verfügt über eine **loadbalancingalgorithmus** -Option. Diese Option nimmt einen von zwei möglichen Werten an: **hypervport** oder **dynamisch**. Verwenden Sie diese Option, um den Lasten Verteilungs Algorithmus für ein Switch-Embedded-Team festzulegen oder zu ändern. 

Im folgenden Beispiel verwendet das vmswitchteam mit dem Namen **teamedvswitch** den **dynamischen** Lasten Ausgleichs Algorithmus.  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -LoadBalancingAlgorithm Dynamic  
```  
### <a name="affinitizing-virtual-interfaces-to-physical-team-members"></a>Zuordnen virtueller Schnittstellen zu physischen Teammitgliedern

Set ermöglicht Ihnen das Erstellen einer Affinität zwischen einer virtuellen Schnittstelle \(d.h., dem Port\) des virtuellen Hyper-V-Switches und einer der physischen NICs im Team. 

Wenn Sie z. b. zwei Host-vNICs für SMB\-Direct erstellen, können Sie wie im Abschnitt [Erstellen eines virtuellen Hyper-V-Switches mit Set-und RDMA-vNICs](#bkmk_set-rdma)sicherstellen, dass die beiden vNICs verschiedene Teammitglieder verwenden. 

Wenn Sie dem Skript in diesem Abschnitt hinzufügen, können Sie die folgenden Windows PowerShell-Befehle verwenden.

    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_1 –ManagementOS –PhysicalNetAdapterName “SLOT 2”
    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_2 –ManagementOS –PhysicalNetAdapterName “SLOT 3”

Dieses Thema wird im Abschnitt 4.2.5 des [Windows Server 2016 NIC-und Switch Embedded Teaming-Benutzerhandbuchs](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)ausführlicher erläutert.
